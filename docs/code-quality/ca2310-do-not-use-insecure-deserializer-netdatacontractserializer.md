---
title: "CA2310: Do not use insecure deserializer NetDataContractSerializer"
ms.date: 05/01/2019
ms.topic: reference
author: dotpaul
ms.author: paulming
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
f1_keywords:
  - "CA2310"
  - "DoNotUseInsecureDeserializerNetDataContractSerializer"
---
# CA2310: Do not use insecure deserializer NetDataContractSerializer

|||
|-|-|
|TypeName|DoNotUseInsecureDeserializerNetDataContractSerializer|
|CheckId|CA2310|
|Category|Microsoft.Security|
|Breaking change|Non-breaking|

## Cause

A <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=nameWithType> deserialization method was called or referenced.

## Rule description

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

This rule finds <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=nameWithType> deserialization method calls or references. If you want to deserialize only when the <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder> property is set to restrict types, disable this rule and enable rules [CA2311](ca2311-do-not-deserialize-without-first-setting-netdatacontractserializer-binder.md) and [CA2312](ca2312-ensure-netdatacontractserializer-binder-is-set-before-deserializing.md) instead.

## How to fix violations

- If possible, use a secure serializer instead, and **don't allow an attacker to specify an arbitrary type to deserialize**. Some safer serializers include:
  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType> - Never use <xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>. If you must use a type resolver, restrict deserialized types to an expected list.
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - Newtonsoft Json.NET - Use TypeNameHandling.None. If you must use another value for TypeNameHandling, restrict deserialized types to an expected list with a custom ISerializationBinder.
  - Protocol Buffers
- Make the serialized data tamper-proof. After serialization, cryptographically sign the serialized data. Before deserialization, validate the cryptographic signature. Protect the cryptographic key from being disclosed and design for key rotations.
- Restrict deserialized types. Implement a custom <xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType>. Before deserializing with <xref:System.Runtime.Serialization.NetDataContractSerializer>, set the <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder> property to an instance of your custom <xref:System.Runtime.Serialization.SerializationBinder>. In the overridden <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> method, if the type is unexpected, throw an exception to stop deserialization.
  - If you restrict deserialized types, you may want to disable this rule and enable rules [CA2311](ca2311-do-not-deserialize-without-first-setting-netdatacontractserializer-binder.md) and [CA2312](ca2312-ensure-netdatacontractserializer-binder-is-set-before-deserializing.md). Rules [CA2311](ca2311-do-not-deserialize-without-first-setting-netdatacontractserializer-binder.md) and [CA2312](ca2312-ensure-netdatacontractserializer-binder-is-set-before-deserializing.md) help to ensure that the <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder> property is always set before deserializing.

## When to suppress warnings

[!INCLUDE[insecure-deserializers-common-safe-to-suppress](includes/insecure-deserializers-common-safe-to-suppress-md.md)]

## Pseudo-code examples

### Violation

```csharp
using System.IO;
using System.Runtime.Serialization;

public class ExampleClass
{
    public object MyDeserialize(byte[] bytes)
    {
        NetDataContractSerializer serializer = new NetDataContractSerializer();
        return serializer.Deserialize(new MemoryStream(bytes));
    }
}
```

```vb
Imports System.IO
Imports System.Runtime.Serialization

Public Class ExampleClass
    Public Function MyDeserialize(bytes As Byte()) As Object
        Dim serializer As NetDataContractSerializer = New NetDataContractSerializer()
        Return serializer.Deserialize(New MemoryStream(bytes))
    End Function
End Class
```

## Related rules

[CA2311: Do not deserialize without first setting NetDataContractSerializer.Binder](ca2311-do-not-deserialize-without-first-setting-netdatacontractserializer-binder.md)

[CA2312: Ensure NetDataContractSerializer.Binder is set before deserializing](ca2312-ensure-netdatacontractserializer-binder-is-set-before-deserializing.md)
