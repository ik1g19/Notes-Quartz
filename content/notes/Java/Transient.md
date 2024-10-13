#java

---


In Java, the `transient` keyword is used as a modifier for instance variables (fields) to indicate that they should **not be serialized** when an object is being serialized.

>[!What is Serialization?]
>Serialization is the process of converting an object into a byte stream, which can then be stored to a file, sent over a network, or transferred in any way. Deserialization is the reverse process: converting the byte stream back into an object.


%% See also  [[Programming 2.pdf#page=29|Programming 2 P29]] %%


## Role of `transient`

When an object is serialized, all of its fields are by default included in the serialization process. However, there may be certain fields that you don’t want to serialize (for example, sensitive information like passwords, or fields that are derived and can be recalculated after deserialization). In such cases, you can mark those fields with the `transient` modifier, and Java will skip them during serialization