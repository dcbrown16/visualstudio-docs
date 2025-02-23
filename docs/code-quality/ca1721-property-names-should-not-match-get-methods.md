---
title: "CA1721: Property names should not match get methods"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "CA1721"
  - "PropertyNamesShouldNotMatchGetMethods"
helpviewer_keywords:
  - "CA1721"
  - "PropertyNamesShouldNotMatchGetMethods"
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1721: Property names should not match get methods

|||
|-|-|
|TypeName|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|Category|Microsoft.Naming|
|Breaking change|Breaking|

## Cause

The name of a member starts with 'Get' and otherwise matches the name of a property. For example, a type that contains a method that is named 'GetColor' and a property that is named 'Color' cause a rule violation.

By default, this rule only looks at externally visible members and properties, but this is [configurable](#configurability).

## Rule description

"Get" methods and properties should have names that clearly distinguish their function.

Naming conventions provide a common look for libraries that target the common language runtime. This consistency reduces the time that's required to learn a new software library and increases customer confidence that the library was developed by someone who has expertise in developing managed code.

## How to fix violations

Change the name so that it does not match the name of a method that is prefixed with 'Get'.

## When to suppress warnings

Do not suppress a warning from this rule.

> [!NOTE]
> This warning may be excluded if the "Get" method is caused by implementing IExtenderProvider interface.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1721.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Naming). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example

The following example contains a method and property that violate this rule.

[!code-csharp[FxCop.Naming.GetMethod#1](../code-quality/codesnippet/CSharp/ca1721-property-names-should-not-match-get-methods_1.cs)]
[!code-vb[FxCop.Naming.GetMethod#1](../code-quality/codesnippet/VisualBasic/ca1721-property-names-should-not-match-get-methods_1.vb)]

## Related rules

- [CA1024: Use properties where appropriate](../code-quality/ca1024-use-properties-where-appropriate.md)