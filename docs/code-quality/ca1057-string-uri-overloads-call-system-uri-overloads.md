---
title: "CA1057: String URI overloads call System.Uri overloads"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1057"
  - "StringUriOverloadsCallSystemUriOverloads"
helpviewer_keywords:
  - "StringUriOverloadsCallSystemUriOverloads"
  - "CA1057"
ms.assetid: ef1e983e-9ca7-404b-82d7-65740ba0ce20
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CPP
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1057: String URI overloads call System.Uri overloads

|||
|-|-|
|TypeName|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|Category|Microsoft.Design|
|Breaking change|Non-breaking|

## Cause

A type declares method overloads that differ only by the replacement of a string parameter with a <xref:System.Uri?displayProperty=fullName> parameter, and the overload that takes the string parameter does not call the overload that takes the <xref:System.Uri> parameter.

## Rule description
Because the overloads differ only by the string or <xref:System.Uri> parameter, the string is assumed to represent a uniform resource identifier (URI). A string representation of a URI is prone to parsing and encoding errors, and can lead to security vulnerabilities. The <xref:System.Uri> class provides these services in a safe and secure manner. To reap the benefits of the <xref:System.Uri> class, the string overload should call the <xref:System.Uri> overload using the string argument.

## How to fix violations
Reimplement the method that uses the string representation of the URI so that it creates an instance of the <xref:System.Uri> class using the string argument, and then passes the <xref:System.Uri> object to the overload that has the <xref:System.Uri> parameter.

## When to suppress warnings
It is safe to suppress a warning from this rule if the string parameter does not represent a URI.

## Example
The following example shows a correctly implemented string overload.

[!code-csharp[FxCop.Design.CallUriOverload#1](../code-quality/codesnippet/CSharp/ca1057-string-uri-overloads-call-system-uri-overloads_1.cs)]
[!code-cpp[FxCop.Design.CallUriOverload#1](../code-quality/codesnippet/CPP/ca1057-string-uri-overloads-call-system-uri-overloads_1.cpp)]
[!code-vb[FxCop.Design.CallUriOverload#1](../code-quality/codesnippet/VisualBasic/ca1057-string-uri-overloads-call-system-uri-overloads_1.vb)]

## Related rules
[CA2234: Pass System.Uri objects instead of strings](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

[CA1056: URI properties should not be strings](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

[CA1054: URI parameters should not be strings](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

[CA1055: URI return values should not be strings](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)