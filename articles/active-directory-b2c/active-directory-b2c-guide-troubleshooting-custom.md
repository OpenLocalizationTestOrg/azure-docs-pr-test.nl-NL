---
title: 'Azure Active Directory B2C: Aangepaste beleidsproblemen oplossen | Microsoft Docs'
description: Meer informatie over benaderingen toosolving fouten bij het werken met aangepaste beleidsregels in Azure Active Directory.
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Problemen oplossen met Azure AD B2C aangepaste beleidsregels en identiteit ervaring Framework

Als u gebruikmaakt van Azure Active Directory B2C (Azure AD B2C) aangepast beleid, kunt u uitdagingen Hallo identiteit ondervinden Framework in het XML-indeling van de beleid-taal instellen tegenkomen.  Learning toowrite aangepaste beleidsregels kunnen worden zoals leren werken met een andere taal. In dit artikel beschreven tools en tips waarmee u kunnen snel opsporen en oplossen van problemen. 

> [!NOTE]
> Dit artikel is gericht op de configuratie van uw Azure AD B2C aangepast beleid voor het oplossen van problemen. Het adres Hallo relying party-toepassing of een identity-bibliotheek niet.

## <a name="xml-editing"></a>XML-bewerken

Hallo meest voorkomende fout bij het instellen van een aangepast beleid is niet goed opgemaakt XML. Er is een goede XML-editor bijna essentieel. Een goede XML-editor XML systeemeigen wordt weergegeven, gekleurd inhoud prefills algemene voorwaarden, houdt XML-elementen die zijn geïndexeerd en kunt valideren met schema. Hier vindt u twee van onze favoriete XML-editors:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Kladblok ++](https://notepad-plus-plus.org/)

XML-schemavalidatie identificeert fouten voordat u uw XML-bestand uploaden. In de hoofdmap van Hallo starter pack Hallo Hallo XML-schemadefinitie TrustFrameworkPolicy_0.3.0.0.xsd worden opgehaald. Voor meer informatie in de documentatie van uw XML-editor Hallo zoekt *XML-hulpprogramma's* en *XML-validatie*.

Mogelijk vindt u een overzicht van XML-regels handig zijn. Azure AD B2C wordt geweigerd eventuele XML opmaakfouten die worden gedetecteerd. In sommige gevallen kan een onjuiste indeling XML mogelijk foutberichten die misleidend zijn.

## <a name="upload-policies-and-policy-validation"></a>Beleid en de validatie van het uploaden

 XML-bestand uploaden validatie is automatisch. De meeste fouten veroorzaken Hallo uploaden toofail. Validatie omvat Hallo beleidsbestand dat u uploadt. Dit omvat ook Hallo keten van bestanden Hallo uploadbestand te verwijst (Hallo relying party beleidsbestand, Hallo uitbreidingen en base Hallo-bestand). 
 
 Algemene validatiefouten bevatten Hallo volgende.

Fout-fragment:`... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Hallo ClaimType waarde kan worden getypt of bestaat niet in het Hallo-schema.
* ClaimType waarden moeten ten minste één Hallo-bestanden in het Hallo-beleid worden gedefinieerd. 
    Bijvoorbeeld: ` <ClaimType Id="socialIdpUserId">`
* Als ClaimType in Hallo extensiebestand is gedefinieerd, maar kan ook worden gebruikt in een waarde TechnicalProfile in base Hallo-bestand, base Hallo-bestand uploadt in een fout resulteert.

Fout-fragment:`...makes a reference tooa ClaimsTransformation with id...`
* Hallo oorzaken voor Hallo fout mogelijk worden Hallo dezelfde als voor Hallo ClaimType fout.

Fout-fragment:`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Controleer dat Hallo TenantId waarde in Hallo  **\<TrustFrameworkPolicy\>**  en  **\<BasePolicy\>**  elementen overeen met het doel-Azure AD B2C tenant.  

## <a name="troubleshoot-hello-runtime"></a>Hallo runtime oplossen

* Gebruik `Run Now` en `https://jwt.io` tootest uw beleid onafhankelijk van uw web- of mobiele toepassing. Deze website fungeert als een relying party-toepassing. Hallo inhoud Hallo JSON Web Token (JWT) die wordt gegenereerd door het beleid van uw Azure AD B2C wordt weergegeven. toocreate een testtoepassing in identiteit ervaring Framework, gebruik Hallo volgende waarden:
    * Naam: TestApp
    * Web-App of Web-API: Nee
    * Native client: Nee

* tootrace hello uitwisseling van berichten tussen de clientbrowser en de Azure AD B2C, gebruik [Fiddler](http://www.telerik.com/fiddler). Dit kunt u een indicatie van waar de gebruiker reis in stappen van de orchestration kan niet ophalen.

* In **Ontwikkelingsmodus**, gebruik **Application Insights** tootrace Hallo activiteit van uw identiteit ervaring Framework gebruiker reis. In **Ontwikkelingsmodus**, ziet u Hallo uitwisseling van claims tussen Hallo identiteit ervaring Framework en hello verschillende claims providers die zijn gedefinieerd door technische profielen, zoals id-providers, op basis van een API-services Hello Azure AD B2C-gebruikerslijst en andere services, zoals Azure meerdere-multi-factor-verificatie.  

## <a name="recommended-practices"></a>Aanbevolen procedures

**Houd meerdere versies van uw scenario's. Ze te groeperen in een project met uw toepassing.** Hallo base, uitbreidingen en relying party-bestanden zijn rechtstreeks van elkaar afhankelijk. Opslaan als een groep. Als nieuwe functies worden tooyour beleid toegevoegd, kunt u afzonderlijke werkende versies bewaren. Fase werkende versies in uw eigen bestandssysteem met ze met communiceren de Hallo toepassingscode.  Uw toepassingen mogelijk veel verschillende relying party beleidsregels in een tenant worden aangeroepen. Deze is mogelijk afhankelijk van het Hallo-claims die ze van uw Azure AD B2C-beleid verwachten.

**Ontwikkelen en testen van technische profielen met bekende gebruikers reizen.** Geteste starter pack beleid tooset van uw technische profielen gebruiken. Ze afzonderlijk testen voordat u ze in uw eigen trajecten gebruiker opnemen.

**Ontwikkelen en testen van de gebruiker trajecten met geteste technische profielen.** Hallo indelingsstappen van een gebruiker reis incrementeel wijzigen. Geleidelijk bouw uw beoogde scenario's.

## <a name="next-steps"></a>Volgende stappen

* Download Hallo [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) ZIP-bestand in GitHub.
