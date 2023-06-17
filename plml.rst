**********************************
The PortaLinux Markup Language 1.1
**********************************

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
- Variable: Follows the ``name = value`` format. Name cannot have spaces, and value must be of type ``int``, ``string``, ``bool``, ``float``, ``array``.
    - Example (``int``): ``variable = 1234``
    - Example (``string``): ``variable = "string"`` or ``variable = 'string'``
        - There are two types of strings. Basic (``"``) or literal (``'``). PLML treats them both as a string, this is only a parser distinction 
    - Example (``bool``): ``variable = true`` or ``variable = false``
    - Example (``float``: ``variable = 123.456``
    - Example (``array``): ``variable = [ 123, 1999, 6502 ]`` or ``variable = [ 123.456, 23.45, 1.25 ]`` or ``[ "string1", 'string2', "string3 ]``
	- PLML arrays, just like TOML arrays, do not allow for multiple data types to be stored in an array
        - pl32lib-ng's PLML implementation allows this due to a parser quirk of PLML arrays being arrays of parsed PLML tokens, therefore allowing for multiple data types per array. This is a bug, not a feature or an extension
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
    property4 = 1.5 # Float
    property5 = [ 123, 2011, 6502 ] # Array
