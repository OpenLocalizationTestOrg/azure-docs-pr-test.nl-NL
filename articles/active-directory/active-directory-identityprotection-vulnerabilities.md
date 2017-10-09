---
title: 'aaaVulnerabilities gedetecteerd door Azure Active Directory: Identity Protection | Microsoft Docs'
description: 'Overzicht van Hallo beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection.'
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection
Zwakke plekken zijn zwakke punten in uw omgeving die door een aanvaller kan worden misbruikt. U wordt aangeraden deze beveiligingsproblemen tooimprove Hallo beveiligingsstatus van uw organisatie adres en voorkomen dat aanvallers deze nu aanvalt.


![beveiligingsproblemen](./media/active-directory-identityprotection-vulnerabilities/101.png "beveiligingsproblemen")



Hallo volgende secties vindt u een overzicht van Hallo zwakke plekken die zijn gerapporteerd door Identity Protection.

## <a name="multi-factor-authentication-registration-not-configured"></a>Multi-factor authentication-registratie niet geconfigureerd
Deze kwetsbaarheid helpt u bij Hallo-implementatie van Azure multi-factor Authentication in uw organisatie beheren. 

Azure multi-factor authentication-Server biedt een tweede beveiligingslaag toouser beveiligingsverificatie. Het helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Sterke verificatie via een bereik van eenvoudige verificatie-opties levert: telefoonoproep, tekstbericht of mobiele app melding of verificatie van code en 3rd party OATH-tokens.

Het is raadzaam dat u Azure multi-factor Authentication voor gebruikersaanmelding nodig hebt. Multi-factorauthenticatie speelt een belangrijke rol in de beleidsregels voor voorwaardelijke toegang op basis van risico's beschikbaar via Identity Protection.

Zie voor meer informatie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Niet-beheerde cloud-apps
Deze kwetsbaarheid helpt u identificeren onbeheerde cloud-apps in uw organisatie.

In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle Hallo cloud-toepassingen dat gebruikers in hun organisatie toodo hun werk gebruiken. Het is gemakkelijk toosee waarom beheerders twijfels over onbevoegde toegang toocorporate gegevens, mogelijk gegevenslekken en andere beveiligingsrisico's hebt zou. 

We raden aan dat uw organisatie implementeren Cloud App Discovery toodiscover zonder begeleiding cloud-toepassingen en toomanage deze toepassingen met Azure Active Directory.

Zie voor meer informatie [zoeken naar niet-beheerde cloud-toepassingen met Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Beveiligingswaarschuwingen van Privileged Identity Management
Deze kwetsbaarheid helpt u bij het opsporen en oplossen van waarschuwingen over bevoegde identiteiten in uw organisatie.  

tooenable gebruikers toocarry bevoorrechte bewerkingen, moeten organisaties toogrant gebruikers tijdelijke of permanente bevoegde toegang in Azure AD, Azure of Office 365-bronnen of andere SaaS-apps. Elk van deze kwetsbaarheid bevoegde gebruikers toeneemt Hallo van uw organisatie. Deze kwetsbaarheid kunt u gebruikers identificeren met onnodige bevoorrechte toegang, en tooreduce passende maatregelen nemen of elimineren Hallo risico die ze vormen. 

We raden aan dat uw organisatie gebruikmaakt van Azure AD Privileged Identity Management toomanage, beheren en monitor bevoegde identiteiten en hun access tooresources in Azure AD, alsmede andere Microsoft online services zoals Office 365 of Microsoft Intune.

Zie voor meer informatie [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Zie ook
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

