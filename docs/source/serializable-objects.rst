Serializable objects
####################

There are three ways to define a class as serializable. The `[SerializeClass]` attribute, the `ISerializable` interface, and the `ISerializeOverride` interface.

Attributes
**********

The attributes `[SerializeClass]` and `[SerializeField(order)]` are used to mark fields and classes as serializable. Automatic serialization will be attempted.

.. tabs::
    .. code-tab:: csharp

        [SerializeClass]
        public class SerializableClass
        {
            [SerializeField(0)] public bool ExampleBool;
            [SerializeField(1)] public string ExampleString;
        }


ISerializable interface
***********************

The ISerializable interface can be implemented to serialize manually.

.. tabs::
    .. code-tab:: csharp

        public class SerializableClass : ISerializableClass<ManualSerializeClass> {
            public int Number = 0;
            
            public void Serialize(Stream s)
            {
                Serializer.SerializeValue(Number, s); // Generic, so type is auto-detected here
            }

            public ManualSerializeClass Deserialize(Stream s)
            {
                Number = Serializer.DeserializeValue<int>(s); // Generic, type is specified here
                
                return this;
            }
        }


ISerializableOverride interface
*******************************

The ISerializableOverride interface allows you to add serialization to predefined classes.  
Example: Making `Guid` serializable.

Define the class:

.. tabs::
    .. code-tab:: csharp

        public class GuidSerializeOverride : ISerializableOverride<Guid>
        {
            private int size = 16;
            
            public void Serialize(Guid target, Stream s)
            {
                s.Write(target.ToByteArray());
            }

            public Guid Deserialize(Stream s)
            {
                var buffer = new byte[size];
                s.Read(buffer, 0, buffer.Length);
                return new Guid(buffer);
            }
        }


Register the override (pick your preferred option):

.. tabs::
    .. code-tab:: csharp

        // Generic
        Serializer.RegisterOverride<GuidSerializeOverride, Guid>();

        // With instance
        Serializer.RegisterOverride(new GuidSerializeOverride());
