---
title: aaaAzure voorwaardelijke toegang tot Active Directory Veelgestelde vragen | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over voorwaardelijke toegang in Azure Active Directory worden opgehaald.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Voorwaardelijke toegang van Azure Active Directory Veelgestelde vragen

## <a name="which-applications-work-with-conditional-access-policies"></a>Welke toepassingen werken met beleid voor voorwaardelijke toegang?

Zie voor meer informatie over toepassingen die met beleid voor voorwaardelijke toegang werken [toepassingen en browsers die gebruikmaken van regels voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>Afgedwongen beleid voor voorwaardelijke toegang voor B2B-samenwerking en gastgebruikers?

Beleid wordt afgedwongen voor business-to-business (B2B) samenwerking gebruikers. Echter, in sommige gevallen kan een gebruiker mogelijk niet kunnen toosatisfy Hallo beleidsvereisten. De organisatie van de gastgebruiker van een mogelijk bijvoorbeeld geen ondersteuning voor multi-factor authentication-server. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>Is een SharePoint Online-beleid ook van toepassing tooOneDrive voor bedrijven?

Ja. Een SharePoint Online-beleid geldt ook tooOneDrive voor bedrijven.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Waarom niet kan ik een beleid op ClientApps, zoals Word of Outlook instellen?

Beleid voor voorwaardelijke toegang stelt vereisten voor het openen van een service. Het wordt afgedwongen wanneer toothat verificatieservice optreedt. Hallo-beleid is niet rechtstreeks op een clienttoepassing ingesteld. In plaats daarvan wordt toegepast wanneer een client een service aanroept. Een beleid dat is ingesteld op SharePoint geldt bijvoorbeeld tooclients aanroepen van SharePoint. Een beleid dat is ingesteld op Exchange geldt tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Is een beleid voor voorwaardelijke toegang van toepassing tooservice accounts?

Beleid voor voorwaardelijke toegang toepassen tooall gebruikersaccounts. Dit omvat de gebruikersaccounts die worden gebruikt als serviceaccounts. Vaak Hallo vereisten van een beleid voor voorwaardelijke toegang kan niet voldoen aan een serviceaccount dat wordt uitgevoerd zonder toezicht. Multi-factor authentication-server zijn vereist. Service-accounts kunnen worden uitgesloten van een beleid met behulp van de instellingen voor beleid voor voorwaardelijke toegang. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>Graph API's beschikbaar zijn voor beleid voor voorwaardelijke toegang configureren?

Op dit moment niet. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>Wat is een standaardbeleid met uitsluiting van Hallo voor niet-ondersteunde platforms?

Beleid voor voorwaardelijke toegang worden op dit moment selectief afgedwongen voor gebruikers van iOS- en Android-apparaten. Toepassingen op andere apparaatplatforms, standaard niet worden beïnvloed door Hallo-beleid voor voorwaardelijke toegang voor iOS en Android-apparaten. Een tenantbeheerder kunt toooverride Hallo globaal beleid toodisallow toegang toousers op platforms die niet worden ondersteund.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Hoe werken beleidsregels voor voorwaardelijke toegang voor Microsoft-Teams?  

Microsoft-Teams is sterk afhankelijk van Exchange Online en SharePoint Online voor core productiviteit scenario's, zoals vergaderingen, agenda's en bestanden delen. Beleid voor voorwaardelijke toegang die zijn ingesteld voor deze cloud-apps van toepassing tooMicrosoft Teams wanneer een gebruiker zich aanmeldt.

Microsoft-Teams wordt ook ondersteund afzonderlijk als een cloud-app in Azure Active Directory-beleid voor voorwaardelijke toegang. Certificaat autoriteit beleidsregels die zijn ingesteld voor een cloud-app toepassing tooMicrosoft Teams wanneer een gebruiker zich aanmeldt.

Microsoft-Teams bureaublad-clients voor Windows en Mac ondersteuning voor moderne verificatie. Moderne verificatie brengt op aanmelden op basis van hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office-clienttoepassingen in verschillende platforms. 
