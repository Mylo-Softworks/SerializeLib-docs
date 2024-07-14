Usage
#####

.. important::
    Objects must be serializable in order to be serialized or deserialized.
    See :ref:`serializable objects` for more information.

.. important::
    The endianness for serializing and deserializing must be the same, the default is based on the system it runs on.
    See :ref:`endianness` for more information.


Serializing an object
*********************

To a stream
===========

.. tabs::
    .. code-tab:: csharp

        var stream = new MemoryStream();
        Serializer.Serialize(exampleObject, stream);

    .. code-tab:: kotlin

        val stream = ByteArrayOutputStream()
        Serializer.serialize(exampleObject, stream)

To a byte[]
===========
.. tabs::
    .. code-tab:: csharp

        byte[] bytes = Serializer.Serialize(exampleObject);

    .. code-tab:: kotlin

        val bytes = Serializer.serialize(exampleObject)

To a file
=========
.. tabs::
    .. code-tab:: csharp

        Serializer.SerializeToFile(exampleObject, "filename.bin")

    .. code-tab:: kotlin

        Serializer.serializeToFile(exampleObject, "filename.bin")

Deserializing an object
***********************
From a stream
=============
.. tabs::
    .. code-tab:: csharp

        var exampleObject = Serializer.Deserialize<SerializationExample>(stream);

    .. code-tab:: kotlin

        val exampleObject = Serializer.deserialize<SerializationExample>(stream)

From a byte[]
=============
.. tabs::
    .. code-tab:: csharp

        var exampleObject = Serializer.Deserialize<SerializationExample>(bytes);

    .. code-tab:: kotlin

        val exampleObject = Serializer.deserialize<SerializationExample>(bytes)

From a file
===========
.. tabs::
    .. code-tab:: csharp

        var exampleObject = Serializer.DeserializeFromFile<SerializationExample>("filename.bin");

    .. code-tab:: kotlin

        val exampleObject = Serializer.deserializeFromFile<SerializationExample>("filename.bin")


Endianness
**********

When deserializing, the endianness must be the same as when serializing. The default endianness is your system's endianness.

.. note::
    x86 systems are little endian, but many file formats, like png, use big endian. To work around this, simply set the `UseBigEndian` field of the `Serializer` object.

.. tabs::
    .. code-tab:: csharp

        Serializer.UseBigEndian = true;

    .. code-tab:: kotlin

        Serializer.UseBigEndian = true