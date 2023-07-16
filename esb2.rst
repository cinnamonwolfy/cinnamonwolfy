********************************************
The Embedded Standard Base 2.0 Draft
********************************************

by pocketlinux32
----------------

The Embedded Standard Base is a standard meant to standardize POSIX-compatible embedded systems, mainly Linux- and BSD-based
embedded systems. It can also be used as a replacement to LSB.

Base Commands
-------------

Here are a list of commands that have to be part of any ESB-compliant system:

External Commands
=================

Filesystem Utilities
####################

- ``basename``
- ``cat``
- ``chgrp``
- ``chmod``
- ``chown``
- ``cp``
- ``dd``
- ``df``
- ``du``
- ``dirname``
- ``file``
- ``find``
- ``link``
- ``ln``
- ``ls``
- ``mkdir``
- ``mkfifo``
- ``mv``
- ``pathchk``
- ``pwd``
- ``rm``
- ``rmdir``
- ``touch``
- ``unlink``

Text Processing Utilities
#########################

- ``cut``
- ``diff``
- ``head``
- ``less``
- ``sed``
- ``tail``
- ``tee``
- ``tr``
- ``uniq``
- ``wc``

Process Management Utilities
############################

- ``kill``
- ``ps``
- ``time``

Shell Programming Utilities
###########################

- ``expr``
- ``sh``
- ``sleep``

Archival Utilities
##################

- ``cpio``
- ``gzip``

System Administration Utilities
###############################
- ``init``
- ``who``

Miscellaneous Utilities
#######################

- ``date``
- ``env``
- ``grep``
- ``id``
- ``tty``
- ``uname``

Shell Builtins
==============

- ``cd``
- ``command``
- ``read``
- ``echo`` (Can be external)
- ``false`` (Can be external)
- ``printf`` (Can be external)
- ``test`` (Can be external)
- ``true`` (Can be external)

Base System API
---------------

The base system API of any ESB-compliant or ESB-compatible system is as follows:

- PortaLinux POSIX API Subset
	- ``open``
	- ``close``
	- ``read``
	- ``write``
	- ``mmap``
	- ``lseek``
	- ``fork`` (optional)
	- ``vfork`` (optional)
	- ``posix_spawn``
	- ``link``
	- ``unlink``
- The PortaLinux Runtime API
	- Memory Tracker
		- ``plMTInit``
		- ``plMTAlloc``
		- ``plMTAllocE``
		- ``plMTCalloc``
		- ``plMTRealloc``
		- ``plMTStop``
	- Array Operations
		- ``plArrayCreate``
		- ``plArrayFree``
		- ``plArrayReallocate``
	- String Operations
		- ``plUStrFromCStr``
		- ``plUStrCompress``
		- ``plUStrchr``
		- ``plUStrstr``
		- ``plUStrtok``
	- File Operations
		- ``plFOpen``
		- ``plFClose``
		- ``plFOpenFD``
		- ``plFRead``
		- ``plFWrite``
		- ``plFPuts``
		- ``plFGets``
		- ``plFPutC``
		- ``plFGetC``
		- ``plFSeek``
		- ``plFTell``
	- PLML Parsing
		- ``plMLParse``
		- ``plMLParseFile``

Simply put, any ESB-compliant/compatible system must support the PortaLinux POSIX API Subset and the PortaLinux Runtime API.

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
    - ``etc``: Contains the configuration files for all the external programs.
    - ``share``: Contains miscellaneous files for all the external programs.
    - ``var``: This where other miscellaneous information for external programs will be stored. This is mostly used for files that change very often
- ``/dev``: Device nodes are created here.
- ``/run``: Usually a ramdisk mountpoint. It is used as a secondary ``/tmp`` folder, usually for programs that will need to write a lot of data very quickly and often.
- ``/etc``, ``/lib``, ``/var``, ``/bin``, ``/sbin``: These are all symbolic links for both FHS and kernel compatibility. For the kernel to even boot up the base system, ``/sbin`` and ``/etc`` must be at the root of the filesystem. While everything else is not necessary, it increases compatibility with FHS and thus makes it so more software can run with fewer modifications to the code
