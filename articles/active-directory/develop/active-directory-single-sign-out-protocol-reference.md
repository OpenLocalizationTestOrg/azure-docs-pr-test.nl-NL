---
title: Eenmalige aanmelding uit SAML Protocol aaaAzure | Microsoft Docs
description: "Dit artikel wordt beschreven Hallo één Sign-Out SAML-Protocol in Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Één afmelden SAML-Protocol
Azure Active Directory (Azure AD) ondersteunt hello SAML 2.0 web browser één afmelden profiel. Voor één afmelden toowork correct Hallo **LogoutURL** voor Hallo toepassing moet expliciet worden geregistreerd bij Azure AD tijdens de toepassingsregistratie. Azure AD gebruikt Hallo LogoutURL tooredirect gebruikers nadat ze zich afgemeld.

Dit diagram toont Hallo werkstroom van hello Azure AD enkel afmelden proces.

![Eenmalige aanmelding van de werkstroom](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Hallo cloud service verzendt een `LogoutRequest` bericht tooAzure AD tooindicate dat een sessie is beëindigd. Hallo volgende fragment toont een voorbeeld van een `LogoutRequest` element.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Hallo `LogoutRequest` element verzonden tooAzure AD vereist Hallo volgende kenmerken:

* `ID`: Dit identificeert afmelden Hallo-aanvraag. waarde van Hallo `ID` mogen niet beginnen met een getal. Hallo gangbare praktijk is tooappend **id** toohello tekenreeksweergave van een GUID.
* `Version`: Stel Hallo-waarde van dit element te**2.0**. Deze waarde is verplicht.
* `IssueInstant`: Dit is een `DateTime` tekenreeks met een waarde coördineren Universal Time (UTC) en [round trip-indeling ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD een waarde van dit type verwacht, maar worden niet afgedwongen.

### certificaatverlener
Hallo `Issuer` -element in een `LogoutRequest` moet exact overeenkomen met een Hallo **ServicePrincipalNames** in de cloudservice Hallo in Azure AD. Dit is normaal gesproken toohello ingesteld **App ID URI** die is opgegeven tijdens de toepassingsregistratie.

### NameID
waarde van Hallo Hallo `NameID` element moet exact overeenkomen met de Hallo `NameID` van Hallo-gebruiker die wordt afgemeld.

## LogoutResponse
Azure AD-verzendt een `LogoutResponse` in antwoord tooa `LogoutRequest` element. Hallo volgende fragment toont een voorbeeld van een `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD ingesteld Hallo `ID`, `Version` en `IssueInstant` waarden in Hallo `LogoutResponse` element. Stelt ook Hallo `InResponseTo` toohello elementwaarde Hallo `ID` kenmerk Hallo `LogoutRequest` die antwoord Hallo opgewekt door.

### certificaatverlener
Azure AD stelt deze waarde te`https://login.microsoftonline.com/<TenantIdGUID>/` waar <TenantIdGUID> hello tenant-ID van hello Azure AD-tenant is.

tooevaluate hello waarde Hallo `Issuer` element, gebruik Hallo waarde Hallo **App ID URI** opgegeven tijdens de toepassingsregistratie.

### Status
Azure AD gebruikt Hallo `StatusCode` -element in Hallo `Status` element tooindicate Hallo slagen of mislukken van afmelding plaatsvindt. Wanneer Hallo afmelden niet lukt, hello `StatusCode` -element kan ook aangepaste foutberichten bevatten.
