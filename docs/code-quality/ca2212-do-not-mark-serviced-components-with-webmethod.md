---
title: "CA2212: Do not mark serviced components with WebMethod"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA2212"
  - "DoNotMarkServicedComponentsWithWebMethod"
helpviewer_keywords:
  - "CA2212"
  - "DoNotMarkServicedComponentsWithWebMethod"
ms.assetid: 774bc55d-e588-48ee-8f38-c228580feca2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA2212: Do not mark serviced components with WebMethod

|||
|-|-|
|TypeName|DoNotMarkServicedComponentsWithWebMethod|
|CheckId|CA2212|
|Category|Microsoft.Usage|
|Breaking change|Breaking|

## Cause

A method in a type that inherits from <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> is marked with <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>.

## Rule description

<xref:System.Web.Services.WebMethodAttribute> applies to methods within an XML web service that were created by using ASP.NET; it makes the method callable from remote web clients. The method and class must be public and executing in an ASP.NET web application. <xref:System.EnterpriseServices.ServicedComponent> types are hosted by COM+ applications and can use COM+ services. <xref:System.Web.Services.WebMethodAttribute> is not applied to <xref:System.EnterpriseServices.ServicedComponent> types because they are not intended for the same scenarios. Specifically, adding the attribute to the <xref:System.EnterpriseServices.ServicedComponent> method does not make the method callable from remote web clients. Because <xref:System.Web.Services.WebMethodAttribute> and a <xref:System.EnterpriseServices.ServicedComponent> method have conflicting behaviors and requirements for context and transaction flow, the behavior of the method will be incorrect in some scenarios.

## How to fix violations

To fix a violation of this rule, remove the attribute from the <xref:System.EnterpriseServices.ServicedComponent> method.

## When to suppress warnings

Do not suppress a warning from this rule. There are no scenarios where combining these elements is correct.

## See also

- <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName>
- <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>