---
title: implementatie van Mobile Engagement aaaAzure voor Gaming-App
description: Gaming-app scenario tooimplement Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Mobile Engagement met Gaming-App implementeren
## <a name="overview"></a>Overzicht
Een gaming-opstarten heeft een nieuwe visserij gebaseerd role play/strategie gameapps gestart. Hallo game is actief en werkend gedurende 6 maanden. Dit spel is een grote voltooid en heeft miljoenen downloads en Hallo bewaartermijn is zeer hoog in vergelijking tooother opstarten game apps. Op Hallo elk kwartaal revisie vergadering akkoord belanghebbenden moeten tooincrease gemiddelde omzet per gebruiker (ARPU). Premium in de game-pakketten zijn beschikbaar als speciale aanbiedingen. Deze game packs toestaan gebruikers tooupgrade Hallo vormgeving en prestaties van hun visserij regels en stelen of tackles in Hallo spel. Er zijn echter pakket verkoop zeer lage. Zodat zij beslissen eerste tooanalyze Hallo klant ervaring met een hulpprogramma voor analyse en vervolgens toodevelop een engagement program tooincrease verkoop met behulp van advanced segmentering.

Op basis van Hallo [Azure Mobile Engagement - instructiehandleiding met aanbevolen procedures](mobile-engagement-getting-started-best-practices.md) ze bouwen engagement-strategie.

## <a name="objectives-and-kpis"></a>Doelstellingen en KPI 's
Voldoen aan de belangrijkste belanghebbenden voor Hallo spel. Alle overeenstemming worden bereikt over een hoofddoel - tooincrease premium pakket omzet per 15%. Ze maken toomeasure Business Key Performance Indicators (KPI's) en het station deze doelstelling

* Op welk niveau van Hallo spel worden deze pakketten gekocht?
* Wat is Hallo omzet per gebruiker, per sessie, per week en per maand?
* Wat zijn Hallo favoriete aankoop typen?

Deel 1 van Hallo [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) wordt uitgelegd hoe toodefine Hallo doelstellingen en KPI's. 

Hallo Mobile Product Manager maakt met de Hallo die zakelijke KPI's nu gedefinieerd, Betrokkenheids-KPI's toodetermine nieuwe gebruiker trends en te bewaren.

* Bewaken van de retentie en het gebruik in Hallo intervallen volgen: dagelijks, 2 dagen, wekelijks, maandelijks en elke 3 maanden
* Actieve gebruikers
* app-classificatie in Hallo Hallo opslaan

Op basis van de aanbevelingen van Hallo IT-team, zijn Hallo technische KPI's te volgen tooanswer Hallo vragen volgende toegevoegd:

* Wat is er een pad naar de gebruiker (welke bezochte hoeveel gebruikers besteden aan het)
* Aantal crashes of fouten aangetroffen per sessie
* Welke versies van het besturingssysteem worden uitgevoerd voor Mijn gebruikers?
* Wat is de gemiddelde grootte Hallo van het scherm voor Mijn gebruikers?
* Wat voor soort verbinding met internet hebt mijn gebruikers?

Voor elke KPI geeft Hallo Mobile Product Manager Hallo gegevens die ze nodig heeft en waar deze zich bevindt in haar playbook.

## <a name="engagement-program-and-integration"></a>Betrokkenheidsprogramma en integratie
Vóór het bouwen van een geavanceerde betrokkenheidsprogramma moet Hallo Mobile Project directeur verantwoordelijk Hallo project een grondige kennis van hoe en wanneer producten worden verbruikt door Hallo gebruikers hebben.

Na drie maanden heeft Hallo Mobile Project directeur verzameld voldoende tooenhance gegevens zijn in-app-push notification-verkoop. Hij leert die:

* de eerste aankoop Hallo gebeurt doorgaans op Hallo-niveau 14. Hallo aankoop is voor 90% van de gevallen, nieuwe legendarische wapens voor $3.
* 80% van de gevallen aankopen van gebruikers die u hebt aangebracht kopen, doorgaan met Hallo product en meer.
* Gebruikers die zijn geslaagd Hallo niveau 20, starten toospend meer dan $10/ week.
* Gebruikers vaak toobuy premium pakketten op niveau 16, 24 en 32.

Bedankt toothis analysis Hallo Mobile Project directeur besluit toocreate specifieke push notification-reeksen tooincrease in app verkoop. Hij maakt drie push reeksen die hij aanroept: Welkom programma, verkoop-programma en niet-actieve programma. Raadpleeg voor meer informatie toohello [hulpmiddelen marketing en verkoop](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
