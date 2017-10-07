---
title: -Microsoft Threat Modeling Tool - aaaThreats Azure | Microsoft Docs
description: "Threat categoriepagina voor Microsoft Threat Modeling Tool Hallo met categorieën voor alle blootgesteld bedreigingen gegenereerd."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Microsoft Threat Modeling Tool bedreigingen

Hallo Threat Modeling hulpprogramma is een hoofdelement Hallo Microsoft Security Development Lifecycle (SDL). Deze software kunt architecten tooidentify en vroeg, mogelijke beveiligingsproblemen te verhelpen wanneer ze relatief eenvoudige en voordelige tooresolve zijn. Als gevolg hiervan vermindert aanzienlijk Hallo totale kosten van ontwikkeling. Bovendien ontworpen we Hallo hulpprogramma met experts van de niet voor beveiliging in acht nemen, waardoor risicomodel gemakkelijker voor alle ontwikkelaars doordat duidelijke richtlijn voor het maken en analyseren van threat modellen.

> Ga naar Hallo  **[Threat Modeling hulpprogramma](./azure-security-threat-modeling-tool.md)**  tooget gestart Vandaag!

Hallo Threat Modeling hulpprogramma kunt u bepaalde zoals Hallo onderstaande vragen beantwoorden:

* Hoe kan een aanvaller verificatiegegevens Hallo wijzigen?
* Wat is Hallo impact als een aanvaller Hallo gebruikersprofielgegevens kunt lezen?
* Wat gebeurt er als de toegang is geweigerd database met gebruikersprofielen toohello?

## <a name="stride-model"></a>STRIDE model

toobetter help formuleren van dit soort verwijzen vragen over Microsoft maakt gebruik van Hallo STRIDE model, dat verschillende soorten bedreigingen ingedeeld en vereenvoudigt Hallo algemene beveiliging conversaties.

| Category | Beschrijving |
| -------- | ----------- |
| **Adresvervalsing (spoofing)** | Omvat illegale wijze toegang tot en met behulp van de verificatiegegevens van een andere gebruiker, zoals gebruikersnaam en wachtwoord |
| **Manipulatie** | Omvat het Hallo schadelijke wijzigingen aan gegevens. Voorbeelden zijn onder meer niet-geautoriseerde wijzigingen toopersistent gegevens, zoals die ondergebracht in een database en Hallo afwijking van gegevens, zoals wordt gebruikt tussen twee computers via een open netwerk, zoals Hallo Internet |
| **Repudiation** | Die zijn gekoppeld aan gebruikers die een actie uitvoert zonder andere partijen die met elke manier tooprove anders weigeren — bijvoorbeeld een gebruiker een ongeldige bewerking in een systeem waarmee u beschikt niet over Hallo mogelijkheid tootrace Hallo verboden bewerkingen uitvoert. Niet-afwijzing verwijst toohello mogelijkheid van een systeem toocounter repudiation bedreigingen. Een gebruiker die een artikel koopt wellicht bijvoorbeeld toosign voor Hallo item na ontvangst. Hallo leverancier kan vervolgens gebruik Hallo ontvangst ondertekend als bewijs dat van die gebruiker Hallo Hallo pakket heeft ontvangen |
| **Vrijgeven van informatie** | Hallo blootstelling van gegevens tooindividuals die niet toohave toegang tooit moeten omvat — bijvoorbeeld Hallo mogelijkheid van gebruikers tooread een bestand dat ze niet zijn toegang verleend tot of hello mogelijkheid van een indringer tooread gegevens onderweg tussen twee computers |
| **Denial of Service** | DOS-aanvallen (DoS) weigeren service toovalid gebruikers, bijvoorbeeld door het maken van een webserver tijdelijk niet beschikbaar of onbruikbaar. U moet beschermen tegen een bepaalde soorten DoS bedreigingen gewoon tooimprove systeembeschikbaarheid en betrouwbaarheid |
| **Misbruik van bevoegdheden** | Een onbevoegde gebruiker bevoorrechte toegang te krijgen en waardoor heeft onvoldoende toegang toocompromise of vernietigen Hallo gehele systeem. Onrechtmatige uitbreiding van bevoegdheden bedreigingen situaties waarbij een aanvaller heeft effectief gepenetreerd alle systeem-beveiliging en deel uit van de vertrouwde Hallo systeem zelf, een gevaarlijke situatie inderdaad opnemen |

## <a name="next-steps"></a>Volgende stappen

Te gaan**[Threat Modeling hulpprogramma oplossingen](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn Hallo verschillende manieren u deze bedreigingen met Azure kunt verhelpen.
