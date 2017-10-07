---
title: instellingen voor het beleid en MDM van aaaGroup | Microsoft Docs
description: Bevat informatie over Groepsbeleid en het mobiele apparaat management (MDM)-instellingen die moeten worden gebruikt op apparaten in Bedrijfseigendom. Deze beleidsregels zijn van de gebruiker van de toegepaste toohello gehele apparaat.
services: active-directory
keywords: Wat zijn groep beleid en de MDM-instellingen voor Enterprise State Roaming, Enterprise State Roaming, windows cloud
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Instellingen voor Groepsbeleid en MDM
Gebruik deze instellingen voor Groepsbeleid en het management (MDM)-instellingen voor mobiele apparaten alleen op apparaten in Bedrijfseigendom omdat deze beleidsregels van de gebruiker van de toegepaste toohello gehele apparaat zijn. Toepassen van een MDM-beleid toodisable instellingen synchronisatie voor een persoonlijke invloed apparaat is eigendom van gebruiker negatieve op Hallo gebruik van het apparaat. Bovendien worden andere gebruikersaccounts op Hallo apparaat ook beïnvloed door het beleid voor Hallo.

Ondernemingen die toomanage zwervende voor persoonlijke (niet-beheerde)-apparaten kunt gebruiken met Azure portal tooenable Hallo- of uitschakelen van roaming in plaats van met behulp van Groepsbeleid of MDM
Hallo volgende tabellen beschrijven Hallo beleidsinstellingen beschikbaar.

## <a name="mdm-settings"></a>MDM-instellingen
Hallo MDM-beleidsinstellingen toepassing tooboth Windows 10 en Windows 10 Mobile.  Windows 10 Mobile-ondersteuning geldt alleen voor Microsoft-account op basis van roaming via OneDrive-account van de gebruiker.  Raadpleeg te synchroniseren op basis van 'Apparaten en eindpunten' sectie voor meer informatie over welke apparaten worden ondersteund voor Azure AD.

| Naam | Beschrijving |
| --- | --- |
| Microsoft-Account verbinding toestaan |Hiermee kunt gebruikers tooauthenticate met een Microsoft-account op Hallo-apparaat |
| Synchronisatie van instellingen toestaan |Kunnen gebruikers tooroam Windows-instellingen en app-gegevens; Als u dit beleid uitschakelt, wordt uitgeschakeld sync, evenals een back-ups op mobiele apparaten |

## <a name="group-policy-settings"></a>Instellingen voor Groepsbeleid
Hallo-instellingen voor Groepsbeleid van toepassing tooWindows 10-apparaten die gekoppeld tooan Active Directory-domein zijn. Hallo tabel bevat ook verouderde instellingen die toomanage synchronisatie-instellingen wordt weergegeven, maar die niet werken voor Enterprise status zwervende voor Windows 10, die met 'Gebruik niet' in de beschrijving van de Hallo worden vermeld.

| Naam | Beschrijving |
| --- | --- |
| Accounts: Blok Microsoft-Accounts |Met deze beleidsinstelling wordt voorkomen dat gebruikers nieuwe Microsoft-accounts op deze computer toevoegen |
| Synchroniseer niet |Voorkomt u dat gebruikers tooroam Windows-instellingen en app-gegevens |
| Synchroniseer niet aanpassen |Uitschakelen van de groep thema's Hallo synchroniseren |
| Synchroniseer niet browserinstellingen |Uitschakelen van Internet Explorer-groep Hallo synchroniseren |
| Synchroniseert geen wachtwoorden |Schakelt synchronisatie van wachtwoorden groep |
| Synchroniseert geen andere Windows-instellingen |Schakelt synchroniseren van de groep van andere Windows-instellingen |
| Synchroniseer niet bureaubladinstellingen |Gebruik geen; heeft geen effect |
| Synchroniseer niet op verbindingen met datalimieten |Schakelt roaming op verbindingen, zoals mobiele 3 G datalimiet |
| Synchroniseer de apps niet |Gebruik geen; heeft geen effect |
| Synchroniseert geen app-instellingen |Schakelt roaming van app-gegevens |
| Synchroniseert geen instellingen van start |Gebruik geen; heeft geen effect |

## <a name="related-topics"></a>Verwante onderwerpen
* [Overzicht van Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Enterprise-status roaming in Azure Active Directory inschakelen](active-directory-windows-enterprise-state-roaming-enable.md)
* [Instellingen en veelgestelde vragen voor dataroaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Windows 10 zwervende naslaginformatie](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Problemen oplossen](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

