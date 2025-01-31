:mod:`sys` -- system specific functions
=======================================

.. module:: sys
   :synopsis: system specific functions

|see_cpython_module| :mod:`python:sys`.

Functions
---------

.. function:: exit(retval=0, /)

   Terminate current program with a given exit code. Underlyingly, this
   function raise as `SystemExit` exception. If an argument is given, its
   value given as an argument to `SystemExit`.

Constants
---------

.. data:: argv

   A mutable list of arguments the current program was started with.

.. data:: byteorder

   The byte order of the system (``"little"`` or ``"big"``).

.. data:: implementation

   Object with information about the current Python implementation. For
   CircuitPython, it has following attributes:

   * *name* - string "circuitpython"
   * *version* - tuple (major, minor, micro), e.g. (1, 7, 0)
   * *_mpy* - supported mpy file-format version (optional attribute)

   This object is the recommended way to distinguish CircuitPython from other
   Python implementations (note that it still may not exist in the very
   minimal ports).

   .. admonition:: Difference to CPython
      :class: attention

      CPython mandates more attributes for this object, but the actual useful
      bare minimum is implemented in CircuitPython.

.. data:: maxsize

   Maximum value which a native integer type can hold on the current platform,
   or maximum value representable by CircuitPython integer type, if it's smaller
   than platform max value (that is the case for CircuitPython ports without
   long int support).

   This attribute is useful for detecting "bitness" of a platform (32-bit vs
   64-bit, etc.). It's recommended to not compare this attribute to some
   value directly, but instead count number of bits in it::

    bits = 0
    v = sys.maxsize
    while v:
        bits += 1
        v >>= 1
    if bits > 32:
        # 64-bit (or more) platform
        ...
    else:
        # 32-bit (or less) platform
        # Note that on 32-bit platform, value of bits may be less than 32
        # (e.g. 31) due to peculiarities described above, so use "> 16",
        # "> 32", "> 64" style of comparisons.

.. data:: modules

   Dictionary of loaded modules. On some ports, it may not include builtin
   modules.

.. data:: path

   A mutable list of directories to search for imported modules.

   .. admonition:: Difference to CPython
      :class: attention

      On MicroPython, an entry with the value ``".frozen"`` will indicate that import
      should search :term:`frozen modules <frozen module>` at that point in the search.
      If no frozen module is found then search will *not* look for a directory called
      ``.frozen``, instead it will continue with the next entry in ``sys.path``.

.. data:: platform

   The platform that CircuitPython is running on. For OS/RTOS ports, this is
   usually an identifier of the OS, e.g. ``"linux"``. For baremetal ports it
   is an identifier of the chip on a board, e.g. ``"MicroChip SAMD51"``.
   It thus can be used to distinguish one board from another.
   If you need to check whether your program runs on CircuitPython (vs other
   Python implementation), use `sys.implementation` instead.

.. data:: ps1
          ps2

   Mutable attributes holding strings, which are used for the REPL prompt.  The defaults
   give the standard Python prompt of ``>>>`` and ``...``.

.. data:: stderr

   Standard error ``stream``.

.. data:: stdin

   Standard input ``stream``.

.. data:: stdout

   Standard output ``stream``.

.. data:: tracebacklimit

   A mutable attribute holding an integer value which is the maximum number of traceback
   entries to store in an exception.  Set to 0 to disable adding tracebacks.  Defaults
   to 1000.

   Note: this is not available on all ports.

.. data:: version

   Python language version that this implementation conforms to, as a string.

.. data:: version_info

   Python language version that this implementation conforms to, as a tuple of ints.

    .. admonition:: Difference to CPython
      :class: attention

      Only the first three version numbers (major, minor, micro) are supported and
      they can be referenced only by index, not by name.
