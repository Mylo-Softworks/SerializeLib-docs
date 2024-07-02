Usage
#####

.. important::
    Objects must be serializable in order to be serialized or deserialized.
    See :ref:`serializable objects` for more information.


Serializing an object
*********************

To a stream
===========

.. tabs::
    .. code-tab:: csharp

        using SerializeLib;

        var stream = new MemoryStream();
        Serializer.Serialize(exampleObject, stream);

To a byte[]
===========
.. tabs::
    .. code-tab:: csharp

        using SerializeLib;
        byte[] bytes = Serializer.Serialize(exampleObject);


To a file
=========
.. tabs::
    .. code-tab:: csharp

        using SerializeLib;
        Serialize.SerializeToFile(exampleObject, "filename.bin")


Deserializing an object
***********************
From a stream
=============
.. tabs::
    .. code-tab:: csharp

        using SerializeLib;

        var exampleObject = Serializer.Deserialize<SerializationExample>(stream);


From a byte[]
=============
.. tabs::
    .. code-tab:: csharp

        using SerializeLib;

        var exampleObject = Serializer.Deserialize<SerializationExample>(bytes);


From a file
===========
.. tabs::
    .. code-tab:: csharp

        using SerializeLib;

        var exampleObject = Serializer.DeserializeFromFile<SerializationExample>("filename.bin");
