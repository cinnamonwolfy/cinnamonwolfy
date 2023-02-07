******************************
The PortaLinux Markup Language
******************************

by: pocketlinux32
-----------------


The PortaLinux Markup Language, PLML for short, is a simple markup language
that is mainly used for configuring PortaLinux system software, such as
``pl-srv``.

The PLML syntax is based on TOML. PLML is basically an attempt to simplify TOML
into an INI-like language. Because of PLML being a subset of TOML, any PLML file
is a valid TOML file and can be parsed by any TOML parsing library.

Syntax
------

The PLML syntax only has three types of tokens:

- Header: Starts with ``[``, ends with ``]``. Header cannot have spaces.
    - Example: ``[header]``
- Variable: Follows the ``name = value`` format. Name cannot have spaces, and value must be of type ``int``, ``string``, or ``bool``.
    - Example (``int``): ``variable = 1234``
    - Example (``string``): ``variable = "string"`` or ``variable = 'string'``
        - There are two types of strings. Basic (``"``) or literal (``'``).
    - Example (``bool``): ``variable = true`` or ``variable = false``
- Comment: Starts with ``#`` and anything past that character gets ignored by the parser
    - Example: ``name = 123 # This will get ignored by the parser :3``

Example File
------------

.. code-block:: toml

    # This is an example PLML File
    [example-header]
    property1 = "test string 123" # Basic string
    property2 = 1234 # Integer
    property3 = true # Boolean
