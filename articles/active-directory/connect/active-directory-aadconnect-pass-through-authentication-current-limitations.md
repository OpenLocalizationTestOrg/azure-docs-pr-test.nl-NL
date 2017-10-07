---
title: 'Azure AD Connect: Pass through-verificatie - huidige beperkingen | Microsoft Docs'
description: Dit artikel worden de huidige beperkingen Hallo van Azure Active Directory (Azure AD) Pass through-verificatie.
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
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Azure Active Directory Pass-through-verificatie: Huidige beperkingen

>[!IMPORTANT]
>Azure AD Pass-through-verificatie is momenteel in preview. Dit is een gratis functie en hoeft u niet alle betaald edities van Azure AD-toouse deze. Pass through-verificatie is alleen beschikbaar in hello world wide exemplaar van Azure AD en niet op [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) en [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Ondersteunde scenario 's

Hallo volgen scenario's worden volledig ondersteund tijdens de preview:

- Gebruikersaanmeldingen in alle web browser gebaseerde toepassingen.
- Gebruikersaanmeldingen in Office 365-clienttoepassingen die ondersteuning bieden voor [moderne verificatie](https://aka.ms/modernauthga).
- Azure AD Join voor Windows 10-apparaten.
- Ondersteuning voor Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Niet-ondersteunde scenario 's

Hallo volgende scenario's zijn _niet_ ondersteund tijdens de preview:

- Gebruikersaanmeldingen in clienttoepassingen verouderde Office (Office 2013 of lager). Organisaties zijn aangemoedigd tooswitch toomodern verificatie, indien mogelijk. Moderne verificatie kunt u ondersteuning voor Pass-through-verificatie, maar ook helpt bij het beveiligen van uw gebruikers gebruikersaccounts via [voorwaardelijke toegang](../active-directory-conditional-access.md) functies zoals multi-factor Authentication (MFA).
- Gebruikersaanmeldingen in Skype voor bedrijven-clienttoepassingen, met inbegrip van Skype voor bedrijven 2016.
- Gebruikersaanmeldingen in PowerShell v1.0. Het wordt aanbevolen v2.0 PowerShell te gebruiken.

>[!IMPORTANT]
>Als tijdelijke oplossing voor niet-ondersteunde scenario's, schakel u synchronisatie van wachtwoordhash op Hallo [optionele functies](active-directory-aadconnect-get-started-custom.md#optional-features) pagina in hello Azure AD Connect-wizard. Synchronisatie van wachtwoordhash fungeert als een opvang voor Hallo voorafgaand aan scenario's _alleen_ (en _niet_ als algemene tooPass via Terugvalverificatie). Als u deze scenario's hoeft, gebruikt u de uitschakelen van synchronisatie van wachtwoordhash.

## <a name="next-steps"></a>Volgende stappen
- [**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.
- [**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
