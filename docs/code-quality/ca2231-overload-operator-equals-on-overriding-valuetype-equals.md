---
title: "CA2231: Overload operator equals on overriding ValueType.Equals"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "OverloadOperatorEqualsOnOverridingValueTypeEquals"
  - "CA2231"
  - "OverrideOperatorEqualsOnOverridingValueTypeEquals"
helpviewer_keywords:
  - "OverloadOperatorEqualsOnOverridingValueTypeEquals"
  - "CA2231"
ms.assetid: 114c0161-261a-40ad-8b2c-0932d6909d2a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA2231: Overload operator equals on overriding ValueType.Equals

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverridingValueTypeEquals|
|CheckId|CA2231|
|Category|Microsoft.Usage|
|Breaking change|Non-breaking|

## Cause

A value type overrides <xref:System.Object.Equals%2A?displayProperty=fullName> but does not implement the equality operator.

By default, this rule only looks at externally visible types, but this is [configurable](#configurability).

## Rule description

In most programming languages, there is no default implementation of the equality operator (==) for value types. If your programming language supports operator overloads, you should consider implementing the equality operator. Its behavior should be identical to that of <xref:System.Object.Equals%2A>.

You cannot use the default equality operator in an overloaded implementation of the equality operator. Doing so will cause a stack overflow. To implement the equality operator, use the Object.Equals method in your implementation. For example:

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## How to fix violations

To fix a violation of this rule, implement the equality operator.

## When to suppress warnings

It is safe to suppress a warning from this rule; however, we recommend that you provide the equality operator if possible.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca2231.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Usage). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

The following example defines a type that violates this rule:

[!code-csharp[FxCop.Usage.EqualsGetHashCode#1](../code-quality/codesnippet/CSharp/ca2231-overload-operator-equals-on-overriding-valuetype-equals_1.cs)]

## Related rules

- [CA1046: Do not overload operator equals on reference types](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)
- [CA2225: Operator overloads have named alternates](../code-quality/ca2225-operator-overloads-have-named-alternates.md)
- [CA2226: Operators should have symmetrical overloads](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)
- [CA2224: Override equals on overloading operator equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)
- [CA2218: Override GetHashCode on overriding Equals](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

## See also

- <xref:System.Object.Equals%2A?displayProperty=fullName>