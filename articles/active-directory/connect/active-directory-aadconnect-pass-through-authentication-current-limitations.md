---
title: 'Azure AD Connect: Pass through-verificatie - huidige beperkingen | Microsoft Docs'
description: Dit artikel worden de huidige beperkingen van Azure Active Directory (Azure AD) Pass through-verificatie.
services: active-directory
keywords: Azure AD Connect Pass through-verificatie, install Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Azure Active Directory Pass-through-verificatie: Huidige beperkingen

>[!IMPORTANT]
>Azure AD Pass-through-verificatie is momenteel in preview. Er is een gratis functie en u hoeft niet elke betaald edities van Azure AD om deze te gebruiken. Pass through-verificatie is alleen beschikbaar in het wereldwijde exemplaar van Azure AD en niet op [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) en [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Ondersteunde scenario 's

De volgende scenario's worden volledig ondersteund tijdens de preview:

- Gebruikersaanmeldingen in alle web browser gebaseerde toepassingen.
- Gebruikersaanmeldingen in Office 365-clienttoepassingen die ondersteuning bieden voor [moderne verificatie](https://aka.ms/modernauthga).
- Azure AD Join voor Windows 10-apparaten.
- Ondersteuning voor Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Niet-ondersteunde scenario 's

De volgende scenario's zijn _niet_ ondersteund tijdens de preview:

- Gebruikersaanmeldingen in clienttoepassingen verouderde Office (Office 2013 of lager). Organisaties aangemoedigd overschakelen naar moderne verificatie, indien mogelijk. Moderne verificatie kunt u ondersteuning voor Pass-through-verificatie, maar ook helpt bij het beveiligen van uw gebruikers gebruikersaccounts via [voorwaardelijke toegang](../active-directory-conditional-access.md) functies zoals multi-factor Authentication (MFA).
- Gebruikersaanmeldingen in Skype voor bedrijven-clienttoepassingen, met inbegrip van Skype voor bedrijven 2016.
- Gebruikersaanmeldingen in PowerShell v1.0. Het wordt aanbevolen v2.0 PowerShell te gebruiken.

>[!IMPORTANT]
>Inschakelen als tijdelijke oplossing voor niet-ondersteunde scenario's, synchronisatie van wachtwoordhash op de [optionele functies](active-directory-aadconnect-get-started-custom.md#optional-features) pagina in de Azure AD Connect-wizard. Synchronisatie van wachtwoordhash fungeert als een opvang voor de bovenstaande scenario's _alleen_ (en _niet_ als een algemene terugvallen op Pass through-verificatie). Als u deze scenario's hoeft, gebruikt u de uitschakelen van synchronisatie van wachtwoordhash.

## <a name="next-steps"></a>Volgende stappen
- [**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.
- [**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -antwoorden op veelgestelde vragen.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over het oplossen van veelvoorkomende problemen met de functie.
- [**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
