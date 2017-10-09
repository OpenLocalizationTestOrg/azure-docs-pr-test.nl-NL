---
title: -Microsoft Threat Modeling Tool - aaaMitigations Azure | Microsoft Docs
description: Pagina met oplossingen voor Hallo Microsoft Threat Modeling Tool markeren mogelijke oplossingen toohello meest blootgesteld gegenereerd bedreigingen.
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
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Microsoft Threat Modeling Tool oplossingen

Hallo Threat Modeling hulpprogramma is een hoofdelement Hallo Microsoft Security Development Lifecycle (SDL). Deze software kunt architecten tooidentify en vroeg, mogelijke beveiligingsproblemen te verhelpen wanneer ze relatief eenvoudige en voordelige tooresolve zijn. Als gevolg hiervan vermindert aanzienlijk Hallo totale kosten van ontwikkeling. Bovendien ontworpen we Hallo hulpprogramma met experts van de niet voor beveiliging in acht nemen, waardoor risicomodel gemakkelijker voor alle ontwikkelaars doordat duidelijke richtlijn voor het maken en analyseren van threat modellen.

Ga naar Hallo  **[Threat Modeling hulpprogramma](./azure-security-threat-modeling-tool.md)**  tooget gestart Vandaag!

## <a name="mitigation-categories"></a>Risicobeperking categorieën

Hallo Threat Modeling hulpprogramma oplossingen zijn onderverdeeld op basis van Web Application Security Frame, die uit de volgende Hallo bestaat toohello:

| Category | Beschrijving |
| -------- | ----------- |
| **[Controle en logboekregistratie](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | Wie en wanneer is? Controle en logboekregistratie verwijzen toohow uw toepassing records beveiligingsgebeurtenissen |
| **[Verificatie](./azure-security-threat-modeling-tool-authentication.md)** | Wie ben jij? Authenticatie is Hallo proces waarbij een entiteit Hallo identiteit van een andere entiteit, doorgaans via referenties, zoals een gebruikersnaam en wachtwoord bewijst |
| **[Autorisatie](./azure-security-threat-modeling-tool-authorization.md)** | Wat kunt u doen? Autorisatie is hoe uw toepassing zorgt voor toegangsbeheer voor bronnen en bewerkingen |
| **[Beveiligde communicatie](./azure-security-threat-modeling-tool-communication-security.md)** | Wie zijn u praten met Beveiligde communicatie zorgt ervoor dat alle communicatie gedaan zo veilig mogelijk is |
| **[Configuratiebeheer](./azure-security-threat-modeling-tool-configuration-management.md)** | Wie uw toepassing uitvoeren als? Welke databases maakt deze verbinding? Hoe wordt uw toepassing beheerd? Hoe worden deze instellingen beveiligd? Configuratiebeheer verwijst toohow uw toepassing verwerkt deze operationele problemen |
| **[Cryptografie](./azure-security-threat-modeling-tool-cryptography.md)** | Hoe houdt u geheimen (vertrouwelijkheid)? Hoe weet u draagbare taalprogramma-bibliotheken (integriteit) of uw gegevens? Hoe biedt u zaden voor willekeurige waarden dat cryptografisch sterke zijn moeten? Cryptografie verwijst toohow uw toepassing worden afgedwongen vertrouwelijkheid en integriteit. |
| **[Uitzonderingsbeheer](./azure-security-threat-modeling-tool-exception-management.md)** | Wanneer een methodeaanroep in uw toepassing mislukt, wat is uw toepassing? Hoeveel onthullen u? U plaatsingsfout beschrijvende informatie tooend gebruikers? Geeft u de uitzondering waardevolle informatie back toohello aanroeper door? Uw toepassing probleemloos mislukt? |
| **[Validatie voor invoer](./azure-security-threat-modeling-tool-input-validation.md)** | Hoe weet u dat uw toepassing krijgt Hallo-invoer geldig en veilige is? Validatie voor invoer verwijst toohow uw toepassing filtert struikvegetaties of invoer voorafgaand aan de extra verwerking wordt geweigerd. Rekening houden met beperkingen invoer via toegangspunten en uitvoer via punten afsluiten codering. Vertrouwt u gegevens uit andere bronnen zoals databases en bestandsshares? |
| **[Gevoelige gegevens](./azure-security-threat-modeling-tool-sensitive-data.md)** | Hoe wordt gevoelige gegevens in uw toepassing verwerkt? Gevoelige gegevens verwijst toohow die uw toepassing verwerkt alle gegevens die moet worden beveiligd in het geheugen via Hallo netwerk, of in permanente winkels |
| **[Sessiebeheer](./azure-security-threat-modeling-tool-session-management.md)** | Hoe uw toepassing verwerken en gebruikerssessies beveiligen? Een sessie verwijst tooa reeks van verwante interacties tussen een gebruiker en uw webtoepassing |

Dit helpt u identificeren:

* Waar zijn Hallo meest voorkomende fouten beschreven die zijn aangebracht
* Waar zijn Hallo verbeteringen in de meeste actie worden uitgevoerd

Als gevolg hiervan gebruik van deze categorieën toofocus en prioriteiten beveiliging, zodat als u Hallo meest bekende beveiligingsproblemen optreden in de invoer-validatie, verificatie en autorisatie categorieën hello weet, u er kunt starten. Voor meer informatie gaat u naar  **[deze patent koppeling](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Volgende stappen

Ga naar  **[Threat Modeling hulpprogramma bedreigingen](./azure-security-threat-modeling-tool-threats.md)**  toolearn informatie over Hallo threat categorieën Hallo hulpprogramma maakt gebruik van toogenerate ontwerp mogelijke bedreigingen.
