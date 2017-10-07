---
title: aaaMobile Engagement-concepten | Microsoft Docs
description: Azure Mobile Engagement-concepten
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Azure Mobile Engagement-concepten
Mobile Engagement definieert een paar concepten algemene tooall ondersteunde platforms. Dit artikel biedt een korte beschrijving van deze concepten.

Dit artikel is een goede start als u nieuwe tooMobile Engagement. Zorg ervoor dat tooread Hallo documentatie specifieke toohello platform die u gebruikt, ook omdat daarin Hallo concepten die worden beschreven in dit artikel met meer details en voorbeelden evenals eventuele beperkingen.

## <a name="devices-and-users"></a>Apparaten en gebruikers
Mobile Engagement identificeert gebruikers door een unieke id voor elk apparaat te genereren. Deze id heet de apparaat-id hello (of `deviceid`). Deze wordt gegenereerd zodanig dat alle toepassingen die worden uitgevoerd van dezelfde Hallo apparaat share Hallo dezelfde apparaat-id.

Dit betekent dat Mobile Engagement ervan uitgaat dat één apparaat toobelong tooexactly één gebruiker en dus gebruikers en apparaten equivalente concepten zijn.

## <a name="sessions-and-activities"></a>Sessies en activiteiten
Een sessie is een gebruik van Hallo toepassing door een gebruiker, het Hallo tijd Hallo gebruiker begint gebruik tot Hallo gebruiker stopt.

Een activiteit is een gebruik van een bepaald gedeelte van de toepassing hello door één gebruiker (meestal is dit een scherm, maar alles geschikte toohello toepassing kan zijn).

Een gebruiker kan slechts één activiteit tegelijk uitvoeren.

Een activiteit wordt aangeduid met een naam (beperkte too64 tekens) en kan eventueel extra gegevens insluiten (in Hallo maximaal 1024 bytes).

Sessies worden automatisch berekend op basis van het Hallo-volgorde van activiteiten uitgevoerd door gebruikers. Een sessie begint wanneer Hallo gebruiker de eerste activiteit Start en stopt wanneer de laatste activiteit is voltooid. Dit betekent dat een sessie niet hoeft toobe expliciet gestart of gestopt. In plaats daarvan worden activiteiten expliciet gestart of gestopt. Als er geen activiteit wordt gerapporteerd, wordt er ook geen sessie gerapporteerd.

## <a name="events"></a>Gebeurtenissen
Gebeurtenissen zijn gebruikte tooreport directe acties (zoals knop is ingedrukt of artikelen gelezen door gebruikers).

Een gebeurtenis kan gerelateerde toohello huidige sessie tooa die u uitvoert, of een zelfstandige gebeurtenis.

Een gebeurtenis wordt aangeduid met een naam (beperkte too64 tekens) en kan eventueel extra gegevens insluiten (in Hallo maximaal 1024 bytes).

## <a name="error"></a>Fout
Fouten zijn gebruikte tooreport problemen correct worden gedetecteerd door de toepassing hello (zoals onjuist gebruikersacties of mislukte API-aanroepen).

Een fout kan gerelateerde toohello huidige sessie tooa die u uitvoert, of een zelfstandige fout.

Een fout wordt aangeduid met een naam (beperkte too64 tekens) en kan eventueel extra gegevens insluiten (in Hallo maximaal 1024 bytes).

## <a name="job"></a>Job
Taken zijn gebruikte tooreport acties met een duur (zoals de duur van API-aanroepen weergegeven tijd dat advertenties, de duur van achtergrondtaken of de duur van gebruikersacties).

Een taak is niet gerelateerd tooa sessie, omdat een taak kan worden uitgevoerd op de achtergrond hello, zonder tussenkomst van de gebruiker.

Een taak wordt aangeduid met een naam (beperkte too64 tekens) en kan eventueel extra gegevens insluiten (in Hallo maximaal 1024 bytes).

## <a name="crash"></a>Crash
Crashes worden automatisch uitgegeven door Hallo Mobile Engagement SDK tooreport toepassing fouten waar problemen niet gedetecteerd door de toepassing hello het maken vastlopen.

## <a name="application-information"></a>Toepassingsgegevens
Toepassingsgegevens (of app-info) wordt gebruikt tootag gebruikers, dat wil zeggen tooassociate sommige gegevens toohello gebruikers van een toepassing (dit is vergelijkbaar tooweb cookies, behalve dat app gegevens worden opgeslagen op Hallo serverzijde op Hallo Azure Mobile Engagement-platform).

App-gegevens kan worden geregistreerd met behulp van Hallo Mobile Engagement SDK-API of met behulp van Mobile Engagement-platform Hallo apparaat-API.

App-gegevens is een sleutel/waarde-paar gekoppeld tooa apparaat. Hallo-sleutel is Hallo-naam van Hallo app-gegevens (beperkte too64 ASCII-letters [a-zA-Z], cijfers [0-9] en onderstrepingstekens [_]). Hallo-waarde (beperkte too1024 tekens) is een tekenreeks, geheel getal, datum (jjjj-MM-dd) of Booleaanse waarde (true of false).

Een willekeurig aantal app-gegevens kan worden gekoppeld tooa apparaat binnen Hallo-limieten die zijn gedefinieerd door Hallo Mobile Engagement-prijsvoorwaarden. Voor elke sleutel Mobile Engagement alleen houdt van Hallo meest recente waarde is ingesteld (geen geschiedenis). Het instellen of wijzigen van Hallo-waarde van app-gegevens forceert Mobile Engagement toore-doelgroepcriteria hierop is ingesteld voor deze app evalueren info (indien aanwezig) wat betekent dat app-gegevens kan worden gebruikt tootrigger realtime pushes.

## <a name="extra-data"></a>Extra gegevens
Extra gegevens (of extra's) zijn willekeurige gegevens die aangesloten tooevents, fouten, activiteiten en taken worden kunnen.

Extra's zijn geordend op dezelfde manier tooJSON objecten: ze worden gemaakt van een structuur van sleutel-waardeparen. Sleutels zijn beperkt too64 ASCII-letters [a-zA-Z], cijfers [0-9] en onderstrepingstekens [_]) en de totale grootte Hallo van extra's is beperkt too1024 tekens (eenmaal gecodeerd in JSON door Hallo Mobile Engagement SDK).

Hallo volledige structuur van sleutel-waardeparen wordt opgeslagen als een JSON-object. Niettemin alleen Hallo eerste niveau van sleutels/waarden opgesplitst toobe is rechtstreeks toegankelijk toosome functies zoals segmenten geavanceerde (bijvoorbeeld, u kunt eenvoudig een segment definiëren genaamd 'SF-fans' die is gemaakt van alle gebruikers die minstens 10 keer Hallo gebeurtenis met de naam 'content_viewed ' hebben verstuurd met Hallo extra sleutel 'content_type' set toohello waarde 'SF' in hello afgelopen maand). Het is dus raadzaam toosend alleen extra's bestaan uit eenvoudige lijsten met sleutel-/ waardeparen met scalaire waarden (bijvoorbeeld tekenreeksen, datums, gehele getallen of Booleaanse waarde).

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van universele Windows-SDK voor Azure Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md)
* [Overzicht van Windows Phone Silverlight-SDK voor Azure Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)
* [iOS-SDK voor Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [Android-SDK voor Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

