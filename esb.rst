********************************************
The Embedded Standard Base 1.0 First Draft
********************************************

by pocketlinux32
----------------

The Embedded Standard Base is a standard meant to standardize POSIX-compatible embedded systems, mainly Linux- and BSD-based embedded systems. It can also be used as a replacement to LSB.

Base Commands
=============

Here are a list of commands that have to be part of any ESB-compliant system:

External Commands
#################

- ``basename`` (Filesystem)
- ``cat`` (Filesystem)
- ``chgrp`` (Filesystem)
- ``chmod`` (Filesystem)
- ``chown`` (Filesystem)
- ``cp`` (Filesystem)
- ``cpio`` (Archival Utilities)
- ``cut`` (Text Processing)
- ``date`` (Misc.)
- ``dd`` (Filesystem)
- ``df`` (Filesystem)
- ``diff`` (Text Processing)
- ``dirname`` (Filesystem)
- ``du`` (Filesystem)
- ``env`` (Misc.)
- ``expr`` (Shell Programming)
- ``file`` (Filesystem)
- ``find`` (Filesystem)
- ``grep`` (Misc.)
- ``gzip`` (Archival Utilities)
- ``head`` (Text Processing)
- ``id`` (Misc.)
- ``init`` (System Initialization)
- ``kill`` (Process Management)
- ``less`` (Text Processing)
- ``link`` (Filesystem)
- ``ln`` (Filesystem)
- ``ls`` (Filesystem)
- ``mkdir`` (Filesystem)
- ``mkfifo`` (Filesystem)
- ``mv`` (Filesystem)
- ``pathchk`` (Filesystem)
- ``ps`` (Process Management)
- ``pwd`` (Filesystem)
- ``rm`` (Filesystem)
- ``rmdir`` (Filesystem)
- ``sed`` (Text Processing)
- ``sh`` (Shell Programming)
- ``tail`` (Text Processing)
- ``tee`` (Text Processing)
- ``time`` (Process Management)
- ``touch`` (Filesystem)
- ``tr`` (Text Processing)
- ``tty`` (Misc.)
- ``uname`` (Misc.)
- ``uniq`` (Text Processing)
- ``unlink`` (Filesystem)
- ``wc`` (Text Processing)
- ``who`` (System Administration)

Shell Builtins
##############

- ``cd``
- ``read``
- ``printf``
- ``echo``
- ``false``
- ``true``
- ``test``
- ``sleep``
- ``command``

Base System API
---------------

The base system API of any ESB-compliant or ESB-compatible system is as follows:

- A C99- and POSIX-compatible C library
- The base pl32lib API
- The plml API

Simply put, any ESB-compliant/compatible system must have a C99- and POSIX-compatible libc, pl32lib and libplml.

Root Filesystem Hierarchy
-------------------------

The root filesystem of any ESB is structured as such:

- ``/usr``: Read-only base system is installed here.
    - ``lib``: All base system libraries are installed here, such as ``libc.so``, ``libpl32.so`` and ``libplml.so``.
    - ``bin``: All base system programs/utilities are installed here, such as the shell interpreter (``sh``).
    - ``etc`` or ``etc.cpio(.gz)``: Contains the configuration files for the base system. These files are used for configuring base system utilities such as init.
    - ``sbin``: A symbolic link to ``/usr/bin`` for FHS compatibility.
- ``/opt``: Read-write changes partition. This is where all external packages will be installed.
    - ``data``: Miscellaneous read-write storage
        - ``etc``: The base system configuration files are copied here so that they can be modified.
        - ``home``: This is where interactive user accounts store all of their local files.
    - ``bin``: All external program/utilities are installed here, such as HTTP, SSH and display servers.
    - ``lib``: All external libraries are installed here, such as graphics libraries like Mesa/OpenGL
    - ``etc`` or ``share``: Contains the configuration and miscellaneous files for all the external programs.
    - ``var``: This where other miscellaneous information for external programs will be stored. This is mostly used for files that change very often
- ``/run``: Usually a ramdisk mountpoint. It is used as a secondary ``/tmp`` folder, usually for programs that will need to write a lot of data very quickly and often.
- ``/etc``, ``/lib``, ``/var``, ``/bin``, ``/sbin``: These are all symbolic links for both FHS and kernel compatibility. For the kernel to even boot up the base system, ``/sbin`` and ``/etc`` must be at the root of the filesystem. While everything else is not necessary, it increases compatibility with FHS and thus makes it so more software can run with fewer modifications to the code