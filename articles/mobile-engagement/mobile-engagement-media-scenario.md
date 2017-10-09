---
title: implementatie van Mobile Engagement aaaAzure voor Media-App
description: Media-app scenario tooimplement Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Mobile Engagement met Media-App implementeren
## <a name="overview"></a>Overzicht
Johan is een mobiele projectmanager voor een bedrijf big media. Hij onlangs een nieuwe app die een zeer hoge downloaden heeft gestart. Hij zijn doelstellingen voor het downloaden is bereikt, maar nog steeds zijn retourneren op Investment(ROI) per gebruiker niet voldoet aan de vereisten. 

Jeroen heeft al geïdentificeerd daarom zijn rendement te laag is. Gebruikers stop vaak zijn app na alleen 2 weken gebruiken en de meeste van deze nooit terugkeren. Hij tooincrease Hallo retentie van de app.

Na enkele initiële tests heeft hij geleerd wanneer hij voert de gebruikers met pushmeldingen, hebben ze vaak toocontinue met behulp van de app. Ook wordt toohello app afhankelijk van de meldingen hij deze verzendt vaak geretourneerd door gebruikers die niet actief zijn. John besluit tooinvest in een soort Betrokkenheidsprogramma voor de app die gebruikmaakt van geavanceerde doelen met pushmeldingen.

Jeroen heeft onlangs Hallo gelezen [Azure Mobile Engagement - instructiehandleiding met aanbevolen procedures](mobile-engagement-getting-started-best-practices.md) tooimplement Hallo aanbevelingen uit Hallo handleiding heeft gekozen.

## <a name="objectives-and-kpis"></a>Doelstellingen en KPI 's
Voldoen aan de belangrijkste belanghebbenden voor Johan app. Zakelijke is gegenereerd op basis van advertenties als gebruikers zijn media gebruiken. Jeroen verhoogt doordat inhoud verbruikt per gebruiker zijn opbrengsten. Alle overeenstemming worden bereikt over een hoofddoel: tooincrease verkoop van advertenties met 25%. Ze maken toomeasure Business Key Performance Indicators (KPI's) en het station deze doelstelling

* Aantal advertenties waarop is geklikt per gebruiker
* Hoeveel artikel's bezocht (per gebruiker / per sessie / per week / maand...)
* Wat zijn de favoriete categorieën

Op basis van Johan vergadering met de belangrijkste belanghebbenden heeft hij zijn zakelijke KPI's gedefinieerd. Hij volgt deel 1 van Hallo [Azure Mobile Engagement - instructiehandleiding met aanbevolen procedures](mobile-engagement-getting-started-best-practices.md). 

Vervolgens maakt hij Hallo na tooensure Betrokkenheids-KPI's die doelstellingen worden bereikt:

* Bewaken van de bewaarperiode voor Hallo intervallen volgen: dagelijks, wekelijks, tweewekelijks en maandelijkse.
* Telt het aantal actieve gebruikers
* app-classificatie Hallo in Hallo-app worden opgeslagen

Op basis van de aanbevelingen van Hallo IT-team, zijn Hallo technische KPI's te volgen tooanswer Hallo vragen volgende toegevoegd:

* Wat is er een pad naar de gebruiker (welke bezochte hoeveel gebruikers besteden aan het)
* Het aantal crashes en fouten per sessie opgetreden?
* Welke versies van het besturingssysteem worden uitgevoerd voor Mijn gebruikers?
* Wat is de gemiddelde grootte Hallo van het scherm voor Mijn gebruikers?
* Wat voor soort internet-verbindingen hebt mijn gebruikers?

Hij classificeert Hallo gegevens die nodig zijn voor elke KPI en hij deze op de juiste locatie Hallo van diens playbook registreert.

## <a name="engagement-program-and-integration"></a>Betrokkenheidsprogramma en integratie
Nu dat Jeroen klaar is met het definiëren van de KPI's, begint zijn Engagement-strategie fase hij door 4 betrokkenheidsprogramma's en hun doelstellingen te definiëren:![][1]

Vervolgens gaat John diepere door met gedetailleerde informatie over pushmeldingen voor elk programma. Push-bericht zijn gedefinieerd door vijf elementen:

1. Doelstelling: Wat is Hallo doelstelling Hallo melding
2. Hoe Hallo doelstelling wordt bereikt
3. Doel: ontvangt die Hallo melding?
4. Inhoud: Wat is tekst hello en Hallo-indeling van Hallo melding (In App/Out van App)
5. Wanneer: Wat is Hallo beste moment toosend deze pushmelding
   
    ![][2]

Raadpleeg voor meer informatie toohello [hulpmiddelen marketing en verkoop](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

Op basis van toohello deel 2 van Hallo white paper die Jeroen gebruikt doel sectie toodefine welke gegevens die hij heeft toocollect- en schrijfbewerkingen zijn Tagplan samen met de IT-team tooimplement Hallo-oplossing. Jeroen na 1 week van de implementatie en gebruikersacceptatietests kunt ten slotte zijn programma's starten.

## <a name="program-results"></a>Programma resultaten
4 maanden later neemt Jeroen de prestaties van programma's. Hallo Welkomstprogramma en Hallo wekelijkse programma zijn doelstellingen zijn. Hallo-nummer van de gebruiker met slechts één sessie afname, meer functies van de app hello worden gebruikt en het aantal verbindingen per week Hallo is verdubbeld.

Hallo **inactieve programma** helpt John gebruiker instinct begrijpen. Het lijkt erop dat 15% van de inactieve gebruikers Hallo toohello app terugkeren. Maar deze meestal niet blijven actief meer dan 1 maand. Jeroen voorziet in een potentiële optimalisatie van deze reeks met extra meldingen en zijn inhoud keuzes uitbreiden.

Hallo **programma Discover** niet goed werkt. De bijbehorende waarde stijgt kruislings verkopen, maar er is onvoldoende tooreach zijn doelstellingen. Jeroen identificeert dat hij niet voldoende gegevens toomake relevante doelen en betreffende inhoud voorstellen. Hij dit programma wordt gestopt en legt de nadruk op 'redactionele pushmeldingen' met Azure Mobile Engagement verzenden. Nog een oplossing voor CMS toosend pushmeldingen zijn journalisten en ze niet toochange.

John besluit toouse Hallo Reach API die een HTTP REST-API waarmee het beheer van Reach-campagnes zonder toouse AZME Web interface. Met deze methode John kan worden verzameld Hallo hij nodig heeft en zijn schrijvers toestaan tookeep met behulp van Hallo CMS-oplossing.

tooensure die correct werkt, John vraagt de IT-team toobe vigilant op Hallo volgende punten:

1. **Bewerking systemen** : ze alle hebben hun eigen pushmeldingen regels tooadministrate zodat Jan toolist beslist alle aanvragen en controles als Hallo API's verwerkt.
   Bijvoorbeeld: Android push-systeem kan grote afbeelding die geen Hallo geval met iOS.
2. **Tijdsbestek**: Jeroen wil een API die Hallo tijdsbestek instellen en stelt u een end-toocampaigns. Hij toopreserve gebruikers van elke verstoren melding bombing.
3. **Categorieën**: marketingteam bereidt een sjabloon voor elk type waarschuwingen. Jeroen vraagt de IT-team tooset categorieën binnen Hallo API.

Johan is na een bepaalde tests tevreden. Met vriendelijke groet toothis API, journalisten kunnen nog steeds pushmeldingen verzenden via hun CMS en Azure Mobile Engagement verzamelt alle gebruikersgedrag gegevens voor deze

Na deze 4 eerst maanden, resultaten weer een goede algehele prestaties en biedt betrouwbaarheid voor John en zijn mededelingenbord, ROI per gebruiker toeneemt per 15% en mobiele verkoop 17,5% van de totale verkoop een toename van 7.5% in slechts vier maanden vertegenwoordigen.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
