---
title: 'Azure AD Connect: Pass through-verificatie - Upgrade preview verificatie Agents | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooupgrade de configuratie van uw Azure Active Directory (Azure AD) Pass through-verificatie.
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Azure Active Directory Pass-through-verificatie: Upgrade preview verificatie Agents

## <a name="overview"></a>Overzicht

In dit artikel is bedoeld voor klanten die gebruikmaken van Azure AD Pass-through-verificatie via preview. We onlangs bijgewerkt (en rebranded) Hallo agentsoftware voor verificatie. U moet too_manually_ upgrade preview verificatie Agents moeten worden geïnstalleerd op uw on-premises servers. Deze handmatige upgrade wordt alleen een eenmalige bewerking. Alle toekomstige updates tooAuthentication Agents zijn automatische. Hallo redenen tooupgrade zijn als volgt:

- Hallo preview-versies van Agents verificatie ontvangen niet alle verdere beveiligings- of oplossingen voor problemen.
-   Hallo preview-versies van Agents verificatie kunnen niet worden geïnstalleerd op extra servers voor hoge beschikbaarheid.

## <a name="check-versions-of-your-authentication-agents"></a>Versies van de Agents verificatie controleren

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Stap 1: Controleer waarbij de verificatie-Agents zijn geïnstalleerd

Volg deze stappen toocheck waarbij de verificatie-Agents zijn geïnstalleerd:

1. Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met Hallo hoofdbeheerder referenties voor uw tenant.
2. Selecteer **Azure Active Directory** op de linkernavigatiebalk Hallo.
3. Selecteer **Azure AD Connect**. 
4. Selecteer **Pass through-verificatie**. Deze blade worden Hallo servers weergegeven waarop de verificatie-Agents zijn geïnstalleerd.

![Azure Active Directory-beheercentrum - blade Pass through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>Stap 2: Controleert Hallo versies van de verificatie-Agents

toocheck hello versies van de verificatie-Agents op elke server in de voorgaande stap Hallo geïdentificeerd als volgt:

1. Ga te**Configuratiescherm -> programma's -> programma's en onderdelen** op Hallo on-premises server.
2. Als er een vermelding voor '**Microsoft Azure AD Connect-verificatie Agent**', hoeft u niet tootake geen actie op deze server.
3. Als er een vermelding voor '**Microsoft Azure AD Connector voor toepassingsproxy**', versies 1.5.132.0 of eerder, moet u toomanually upgrade op deze server.

![Preview-versie van de verificatie-Agent](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Aanbevolen procedures toofollow voordat het Hallo-upgrade wordt gestart

Zorg ervoor dat u de volgende items erin Hallo hebt alvorens te upgraden:

1. **Alleen in de cloud globale beheerdersaccount maken**: geen upgrade zonder een alleen-hoofdbeheerder account toouse in noodsituaties, waarbij de Agents van Pass through-verificatie niet goed werken. Meer informatie over [toevoegen van een cloudconfiguratie globale beheerdersaccount](../active-directory-users-create-azure-portal.md). Deze stap is van essentieel belang en zorgt ervoor dat u geen toegang buiten uw tenant.
2.  **Hoge beschikbaarheid garanderen**: als niet eerder is voltooid, installeert u een tweede zelfstandige verificatie-Agent tooprovide hoge beschikbaarheid voor aanmelden aanvragen, gebruik van deze [instructies](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>Hallo verificatie-Agent op uw Azure AD Connect-server upgraden

U moet Azure AD Connect upgraden voordat u de upgrade Hallo verificatie-Agent op Hallo dezelfde server. Volg deze stappen op uw primaire- en staging-Azure AD Connect-servers:

1. **Azure AD Connect upgraden**: voert u [artikel](./active-directory-aadconnect-upgrade-previous-version.md) en toohello meest recente Azure AD Connect versie upgraden.
2. **Hallo preview-versie van Hallo verificatie-Agent verwijderen**: downloaden [dit PowerShell-script](https://aka.ms/rmpreviewagent) en deze worden uitgevoerd als een Administrator op Hallo-server.
3. **Download de nieuwste versie Hallo Hallo verificatie-Agent (versies 1.5.193.0 of hoger)**: aanmelden toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met uw globale tenantbeheerderreferenties. Selecteer **Azure Active Directory -> Azure AD Connect -> Pass through-verificatie-agent downloaden >**. Hallo gebruiksrechtovereenkomst accepteren en de meest recente versie Hallo Hallo verificatie-Agent downloaden.
4. **Installeer de meest recente versie Hallo Hallo verificatie-Agent**: Voer Hallo uitvoerbare gedownload in stap 3. Geef uw tenant hoofdbeheerder referenties wanneer u wordt gevraagd.
5. **Controleer of de nieuwste versie van die Hallo is geïnstalleerd**: zoals eerder aangegeven, gaat u te**Configuratiescherm -> programma's -> programma's en onderdelen** en controleer of er een vermelding voor '**Microsoft Azure AD Connect Verificatie-Agent**'.

>[!NOTE]
>Als u het selectievakje Hallo Pass through-verificatie-blade op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) na het voltooien van de vorige stappen Hallo ziet u twee verificatie-Agent vermeldingen per server - één vermelding Hallo weergeven Verificatie-Agent als **Active** en andere als Hallo **inactief**. Dit is _verwacht_. Hallo **inactief** vermelding automatisch wordt verbroken na een paar dagen.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>Hallo verificatie-Agent op andere servers bijwerken

Volg deze stappen tooupgrade verificatie Agents op andere servers (waar Azure AD Connect is niet geïnstalleerd):

1. **Hallo preview-versie van Hallo verificatie-Agent verwijderen**: downloaden [dit PowerShell-script](https://aka.ms/rmpreviewagent) en deze worden uitgevoerd als een Administrator op Hallo-server.
2. **Download de nieuwste versie Hallo Hallo verificatie-Agent (versies 1.5.193.0 of hoger)**: aanmelden toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met uw globale tenantbeheerderreferenties. Selecteer **Azure Active Directory -> Azure AD Connect -> Pass through-verificatie-agent downloaden >**. Hallo gebruiksrechtovereenkomst accepteren en download de nieuwste versie Hallo.
3. **Installeer de meest recente versie Hallo Hallo verificatie-Agent**: uitvoeren Hallo uitvoerbare in stap 2 hebt gedownload. Geef uw tenant hoofdbeheerder referenties wanneer u wordt gevraagd.
4. **Controleer of de nieuwste versie van die Hallo is geïnstalleerd**: zoals eerder aangegeven, gaat u te**Configuratiescherm -> programma's -> programma's en onderdelen** en controleer of er een vermelding aangeroepen **Microsoft Azure AD Connect Verificatie-Agent**.

>[!NOTE]
>Als u het selectievakje Hallo Pass through-verificatie-blade op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) na het voltooien van de vorige stappen Hallo ziet u twee verificatie-Agent vermeldingen per server - één vermelding Hallo weergeven Verificatie-Agent als **Active** en andere als Hallo **inactief**. Dit is _verwacht_. Hallo **inactief** vermelding automatisch wordt verbroken na een paar dagen.

## <a name="next-steps"></a>Volgende stappen
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
