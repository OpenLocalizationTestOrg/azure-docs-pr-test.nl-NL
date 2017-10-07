---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Push/Reach
description: Problemen met het gebruiker interactie en notification in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Handleiding voor het oplossen van Push- en bereikproblemen
Hallo volgen mogelijke problemen die optreden bij hoe Azure Mobile Engagement informatie tooyour gebruikers verzendt.

## <a name="push-failures"></a>Mislukte push
### <a name="issue"></a>Probleem
* Pushmeldingen werken (per app buiten de app, of beide) niet.

### <a name="causes"></a>Oorzaken
* Vaak een push-fout geeft aan dat Azure Mobile Engagement, bereik of een andere geavanceerde functie van Azure Mobile Engagement is niet correct worden geïntegreerd en dat er een upgrade is vereist in Hallo SDK toofix een bekend probleem met een nieuw besturingssysteem of de apparaat-platform.
* Test een In-App-push en slechts een van de App push toodetermine als er een probleem In App- of Out of App.
* Testen van zowel Hallo gebruikersinterface als Hallo API als een probleemoplossing stap toosee welke aanvullende foutinformatie beschikbaar is beide plaatsen.
* Buiten de App werken pushes alleen als zowel Azure Mobile Engagement en het bereik zijn geïntegreerd in Hallo SDK.
* Pushes werkt niet als certificaten ongeldig zijn of PROD tegenover gebruikt. DEV correct (alleen iOS). (**Opmerking:** 'out of app' pushmeldingen kunnen niet worden bezorgd tooiOS, als u beide Hallo-ontwikkeling (DEV) hebt en (PROD) Productieversies van uw toepassing dat is geïnstalleerd op Hallo dezelfde apparaat sinds hello security token dat is gekoppeld met uw certificaat mogelijk ongeldig worden gemaakt van Apple. tooresolve dit probleem Hallo DEV zowel PROD-versies van uw toepassing verwijderen en opnieuw installeren één versie alleen Hallo op uw apparaat.)
* Buiten de App push aantallen anders afgehandeld op verschillende platforms (iOS ziet minder informatie dan Android als systeemeigen pushes zijn uitgeschakeld op een apparaat, Hallo API voor meer informatie dan Hallo gebruikersinterface op push statistieken).
* Buiten de App kunnen pushes worden geblokkeerd door klanten op niveau van het besturingssysteem (iOS en Android).
* Buiten de App wordt pushes weergegeven als uitgeschakeld in hello Azure Mobile Engagement gebruikersinterface als ze zijn niet correct worden geïntegreerd, maar in de achtergrond van Hallo API mislukken.
* In-App werken pushes alleen als zowel Azure Mobile Engagement en het bereik zijn geïntegreerd in Hallo SDK.
* GCM en ADM pushes werken alleen als Azure Mobile Engagement en specifieke server Hallo zijn geïntegreerd in Hallo SDK (alleen Android).
* In-App en van de App pushes moeten worden getest afzonderlijk toodetermine als het een probleem met de Push- of bereiken.
* In de App pushes vereist die app Hallo open toobe ontvangen worden.
* In-App zijn pushes vaak setup toobe gefilterd door een opt-in- of opt-out app info-tag.
* Als u een aangepaste categorie in Reach toodisplay in-app-meldingen gebruiken, moet u toofollow Hallo juist levenscyclus van Hallo-bericht, anders Hallo-bericht kan niet worden gewist wanneer Hallo gebruiker genegeerd.
* Als u een campagne met geen einddatum start en een apparaat Hallo in app-melding ontvangt, maar niet wordt weergegeven het nog, Hallo gebruiker nog steeds ontvangt Hallo melding Hallo volgende keer dat ze zich in Hallo-app aanmelden, zelfs als u Hallo campagne handmatig beëindigen.
* Bevestig dat u echt toouse Hallo API Push in plaats van Hallo Reach API wilt (omdat Hallo Reach API vaker wordt gebruikt) en dat u niet verwarrend Hallo 'nettolading' en 'melder'-parameters bent voor problemen met Hallo Push-API.
* Test uw pushcampagne met zowel een apparaat is verbonden via Wi-Fi- en 3G tooeliminate Hallo netwerkverbinding als mogelijke bron van problemen.

## <a name="push-testing"></a>Push testen
### <a name="issue"></a>Probleem
* Pushes kunnen worden verzonden tooa specifiek apparaat op basis van een apparaat-ID.

### <a name="causes"></a>Oorzaken
* Testapparaten setup anders voor elk platform zijn, maar veroorzaakt door een gebeurtenis in uw app op een testapparaat en en zoekt u uw apparaat-ID in de portal Hallo moeten werken toofind uw apparaat-ID voor alle platforms.
* Testapparaten werken anders met IDFA vs. IDFV (alleen iOS).

## <a name="push-customization"></a>Push-aanpassing
### <a name="issue"></a>Probleem
* Geavanceerde push inhoud item werkt niet (badge, ring, Trillen, afbeeldingen, enzovoort).
* Koppelingen van pushes werken (buiten de app, in-app, tooa website, tooa locatie in-app) niet.
* Push statistieken weergeven die een push niet is verzonden tooas veel mensen zoals verwacht (te veel of is niet voldoende).
* Push gedupliceerd en twee keer ontvangen.
* Kan testapparaat niet registreren voor Azure Mobile Engagement Pushes (met uw eigen app Prod of DEV).

### <a name="causes"></a>Oorzaken
* toolink tooa specifieke locatie in de app is vereist 'categorieën' (alleen Android).
* Grondige schema's koppelen tooredirect gebruikers tooan alternatieve locatie wanneer u een push-melding op moet toobe in hebt gemaakt en beheerd door uw toepassing en Hallo besturingssysteem van het apparaat niet door de Mobile Engagement rechtstreeks. (**Opmerking:** buiten de app meldingen kunnen geen koppeling rechtstreeks tooin app locaties met iOS zoals dat bij Android.)
* De installatiekopie van de externe servers moeten toobe kunnen toouse HTTP 'GET' en 'HEAD"voor grote afbeelding pushes toowork (alleen Android).
* In uw code kunt u uitschakelen hello Azure Mobile Engagement agent wanneer Hallo toetsenbord wordt geopend en hebt u uw code opnieuw activeren hello Azure Mobile Engagement agent als Hallo toetsenbord is gesloten, zodat hello toetsenbord niet van invloed op Hallo uiterlijk van uw melding (alleen iOS).
* Sommige items werken niet in de test simulaties, maar alleen echte campagnes (badge, ring, Trillen, afbeeldingen, enzovoort).
* Er zijn geen gegevens worden geregistreerd wanneer u de knop Hallo serverzijde te 'test' duwt. Gegevens worden alleen geregistreerd voor echte pushcampagnes.
* toohelp isoleren van uw probleem, oplossen met: test, simuleren, en een echte campagne omdat ze elk iets anders werkt.
* Hallo tijdsduur die uw "in de app' en 'elke keer' campagnes geplande toorun zijn kan van invloed zijn levering getallen omdat een campagne worden alleen geleverd toousers die zich 'in de app' terwijl Hallo campagne wordt uitgevoerd (en gebruikers die hun apparaatinstellingen hebben ingesteld tooreceive meldingen 'out of app').
* Hallo verschillen tussen hoe Android en iOS-ingang buiten de app-meldingen het moeilijk toodirectly maakt push statistieken vergelijken tussen Hallo Android en iOS-versie van uw toepassing. Android biedt meer OS niveau melding informatie dan iOS. Android rapporten wanneer een systeemeigen melding is ontvangen, geklikt of verwijderd uit het meldingencentrum hello, maar iOS wordt deze informatie niet gerapporteerd, tenzij het Hallo-melding wordt geklikt. 
* belangrijkste reden Hallo 'pushed' getallen anders dan andere dan 'geleverd' getallen voor campagnes bereikt dat 'in-app' en 'out of app' meldingen worden geteld anders zijn. 'In-app' meldingen worden verwerkt door de Mobile Engagement, maar 'out of app' meldingen worden verwerkt door het meldingencentrum Hallo in Hallo OS van uw apparaat.

## <a name="push-targeting"></a>Push-doelen
### <a name="issue"></a>Probleem
* Ingebouwd in als doel niet werkt zoals verwacht.
* App-gegevens Tag targeting werkt niet zoals verwacht.
* Geografische locatie als doel werkt niet zoals verwacht.
* Taalopties werken niet zoals verwacht.

### <a name="causes"></a>Oorzaken
* Zorg ervoor dat u app-info labels via hello Azure Mobile Engagement-gebruikersinterface of API hebt geüpload.
* Bandbreedtebeperking Hallo push snelheid of push quotum op toepassingsniveau Hallo of beperkende Hallo doelgroep op Hallo campagne niveau kunt voorkomen dat een persoon ontvangt een specifieke push zelfs als ze voldoen aan uw doel criteria. 
* Het instellen van een 'taal' is anders dan die gericht is op basis van land of landinstellingen, dit ook anders is dan die gericht is op basis van geografische locatie op basis van een telefoon locatie of GPS-locatie.
* Hallo-bericht in Hallo 'standaardtaal' tooany klant die hun apparaat instellen tooone Hallo alternatieve talen die u opgeeft niet verzonden.

## <a name="push-scheduling"></a>Push plannen
### <a name="issue"></a>Probleem
* Push planning werkt niet zoals verwacht (verzonden te vroeg of vertraagde).

### <a name="causes"></a>Oorzaken
* Tijdzones kunnen problemen met het plannen, met name wanneer u de tijdzone Hallo eindgebruikers.
* Geavanceerde push-functies kunnen pushes uitstellen.
* Die gericht is op basis van de telefoon instellingen (in plaats van de labels van App-Info) kunnen uitstellen duwt aangezien Azure Mobile Engagement toorequest gegevens van realtime Hallo-telefoon voor het verzenden van een push kan hebben.
* Campagnes gemaakt zonder een einddatum Hallo push lokaal opslaan op Hallo-apparaat en weergeven Hallo volgende keer Hallo-app wordt geopend, zelfs als Hallo campagne handmatig wordt beëindigd.
* Meer dan een campagne wordt gestart op Hallo dezelfde tijd kan duren voordat een langere tijd tooscan uw gebruikersgroep (tooonly start een campagne probeer op een tijdstip met een maximum van vier, ook alleen tooyour actieve gebruikers als doel zodat oude gebruikers hoeven geen toobe gescand).
* Als u 'Doelgroep negeren, push wordt verzonden toousers via API Hallo' Hallo-optie gebruikt in 'Campagne' Hallo-sectie van een Reach-campagne Hallo campagne wordt niet automatisch verzenden, moet u toosend handmatig via Hallo Reach API.
* Als u een aangepaste categorie in Reach toodisplay in-app-meldingen gebruiken, moet u toofollow Hallo juist levenscyclus van een melding, anders Hallo-bericht kan niet worden gewist wanneer Hallo gebruiker genegeerd.

