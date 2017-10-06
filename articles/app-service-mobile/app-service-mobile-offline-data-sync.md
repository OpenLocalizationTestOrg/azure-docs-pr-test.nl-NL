---
title: aaaOffline synchroniseren van gegevens in Azure Mobile Apps | Microsoft Docs
description: Overzicht van Hallo offlinegegevensgateway synchronisatiefunctie voor Azure Mobile Apps en voor conceptuele verwijzing in
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Offlinesynchronisatie van gegevens in Azure Mobile Apps
## <a name="what-is-offline-data-sync"></a>Wat is offline synchroniseren van gegevens?
Offline synchroniseren van gegevens is een client en server SDK-functie van Azure Mobile Apps waarmee u gemakkelijk voor ontwikkelaars toocreate apps die functionele zonder een netwerkverbinding zijn.

Wanneer uw app in de offlinemodus bevindt, kunt u nog steeds maken en wijzigen van gegevens, die het lokale archief tooa worden opgeslagen. Wanneer Hallo app weer online is, kunnen lokale wijzigingen worden gesynchroniseerd met uw back-end voor mobiele Apps van Azure. Hallo-functie biedt ook ondersteuning voor het opsporen van conflicten wanneer dezelfde record wordt gewijzigd op zowel Hallo Hallo van client en Hallo back-end. Conflicten kunnen vervolgens worden verwerkt op Hallo-server of op Hallo-client.

Offline synchronisatie heeft verschillende voordelen:

* Reactietijd van de app door de servergegevens lokaal op Hallo apparaat cache te verbeteren
* Robuuste apps die nuttig blijven wanneer er netwerkproblemen maken
* Gegevens wijzigen, zelfs wanneer er geen toegang tot het netwerk, ondersteuning van scenario's met weinig of geen connectiviteit en end gebruikers toocreate toestaan
* Synchroniseren van gegevens op meerdere apparaten en het opsporen van conflicten als hello dezelfde record wordt gewijzigd door twee apparaten
* Netwerkgebruik op hoge latentie of gecontroleerde netwerken beperken

Hallo volgende zelfstudies tonen hoe tooadd offline tooyour mobiele clients met Azure Mobile Apps synchroniseren:

* [Android: Offlinesynchronisatie inschakelen]
* [Apache Cordova: Offlinesynchronisatie inschakelen](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: offlinesynchronisatie inschakelen]
* [Xamarin iOS: offlinesynchronisatie inschakelen]
* [Xamarin Android: Offlinesynchronisatie inschakelen]
* [Xamarin.Forms: Offlinesynchronisatie inschakelen](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [universele Windows-Platform: inschakelen offlinesynchronisatie]

## <a name="what-is-a-sync-table"></a>Wat is een tabel synchroniseren?
tooaccess Hallo '/ tabellen' eindpunt, hello Azure Mobile client SDK's Geef interfaces, zoals `IMobileServiceTable` (.NET client SDK) of `MSTable` (iOS-client). Deze API's toohello mobiele Apps van Azure back-end rechtstreeks verbinding gemaakt en mislukken als het clientapparaat Hallo niet over een netwerkverbinding beschikt.

off line gebruik toosupport, Hallo moet in plaats daarvan gebruiken in uw app *synchronisatietabel* API's, zoals `IMobileServiceSyncTable` (.NET client SDK) of `MSSyncTable` (iOS-client). Alle Hallo dezelfde CRUD-bewerkingen (maken, lezen, bijwerken, verwijderen) in combinatie met synchronisatie tabel API's, behalve nu ze lezen uit of schrijven tooa *lokale archief*. Voordat u synchronisatie tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd.

## <a name="what-is-a-local-store"></a>Wat is een lokaal archief?
Een lokaal archief is laag voor gegevenspersistentie Hallo op Hallo-clientapparaat. Hello Azure Mobile Apps client SDK's bieden een standaard lokale uitvoering opslaan. Op Windows, Xamarin en Android, is gebaseerd op SQLite. In iOS, is gebaseerd op gegevens van de Core.

toouse hello SQLite-implementatie op basis van op Windows Phone of Windows Store 8.1, moet u tooinstall een SQLite-extensie. Zie voor meer informatie [universele Windows-Platform: inschakelen offlinesynchronisatie]. Android en iOS worden geleverd met een versie van SQLite Hallo apparaat besturingssysteem zelf, zodat het niet nodig tooreference uw eigen versie van SQLite.

Ontwikkelaars kunnen ook hun eigen lokale store implementeren. Als u toostore gegevens in een versleutelde indeling op Hallo mobiele client wenst, kunt u bijvoorbeeld een lokaal archief die gebruikmaakt van SQLCipher voor versleuteling definiëren.

## <a name="what-is-a-sync-context"></a>Wat is er een synchronisatie-context?
Een *sync context* is gekoppeld aan een object mobiele clients (zoals `IMobileServiceClient` of `MSClient`) en bijgehouden wijzigingen die zijn aangebracht met synchronisatie tabellen. Hallo sync context onderhoudt een *bewerking wachtrij*, waarvan een geordende lijst met CUD bewerkingen (maken, bijwerken, verwijderen) die later valt houdt toohello server worden verzonden.

Een lokaal archief is gekoppeld aan Hallo sync context met een initialisatiemethode zoals `IMobileServicesSyncContext.InitializeAsync(localstore)` in Hallo [SDK voor .NET-clients].

## <a name="how-sync-works"></a>Hoe offline synchronisatie werkt
Wanneer u de synchronisatie-tabellen, bepaalt de clientcode als lokale wijzigingen worden gesynchroniseerd met een back-end voor mobiele Apps van Azure. Niets toohello back-end wordt verzonden, totdat er een aanroep te*push* lokale wijzigingen. Op deze manier Hallo lokale archief is gevuld met nieuwe gegevens alleen als er een aanroep te*pull* gegevens.

* **Push**: Push is een bewerking op Hallo sync context en alle CUD wijzigingen sinds de laatste push Hallo verzendt. Houd er rekening mee dat deze is niet mogelijk toosend omdat anders operations kunnen worden verzonden volgorde alleen wijzigingen voor een afzonderlijke tabel. Push voert een reeks REST-aanroepen tooyour mobiele Apps van Azure back-end die op zijn beurt Hiermee wijzigt u de server-database.
* **Pull-**: Pull wordt uitgevoerd op basis van per tabel en kan worden aangepast met een query tooretrieve slechts een subset van Hallo-servergegevens. Hallo van client-SDK's van Azure Mobile vervolgens Hallo resulterende gegevens invoegen in het lokale archief Hallo.
* **Impliciete Pushes**: als een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates, Hallo pull eerst voert een `push()` op Hallo sync context. Deze push helpt te beperken van conflicten tussen wijzigingen die al in de wachtrij en nieuwe gegevens van Hallo-server.
* **Incrementele synchronisatie**: Hallo eerste parameter toohello pull-bewerking is een *querynaam* die alleen op Hallo-client wordt gebruikt. Als u een naam voor de niet-null gebruikt, hello Azure Mobile SDK wordt uitgevoerd een *incrementele synchronisatie*. Telkens wanneer een pullbewerking een set resultaten retourneert, recente Hallo `updatedAt` tijdstempel van die resultaatset wordt opgeslagen in Hallo SDK lokale systeemtabellen. Alleen records ophalen opeenvolgende pull-bewerkingen na tijdstempel.

  incrementele synchronisatie toouse, de server moet retourneren zinvolle `updatedAt` waarden en moet ook ondersteuning voor sortering op dit veld. Echter, aangezien Hallo SDK een eigen sorteren op Hallo updatedAt veld voegt, u geen gebruik een pull-query zijn eigen heeft `orderBy` component.

  Hallo querynaam mag elke tekenreeks die u kiest, maar het moet uniek zijn voor elke logische query in uw app.
  Anders verschillende pull-bewerkingen Hallo kunnen overschrijven dezelfde incrementele synchronisatie tijdstempel en uw query's kunnen onjuiste resultaten retourneren.

  Als Hallo query een parameter heeft, is het eenrichtingssessie toocreate een unieke naam tooincorporate Hallo parameterwaarde.
  Als u op gebruikers-id filtert, kan de querynaam van uw als volgt (in C#) zijn:

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Als u wilt dat tooopt incrementele synchroon, doorgeven `null` zoals Hallo query-ID. In dit geval alle records opgehaald bij elke aanroep te`PullAsync`, dit is mogelijk niet efficiënt.
* **Opschonen van**: U kunt inhoud van het gebruik van de lokale archief Hallo Hallo wissen `IMobileServiceSyncTable.PurgeAsync`.
  Opschonen van mogelijk nodig als u verouderde gegevens in Hallo client-database hebt of als u alle wijzigingen in behandeling toodiscard wenst.

  Een opschonen wordt een tabel uit het lokale archief Hallo gewist. Als er bewerkingen in afwachting van synchronisatie met Hallo server-database Hallo opschonen er wordt een uitzondering gegenereerd tenzij Hallo *forceren opschonen* parameter is ingesteld.

  Als een voorbeeld van verouderde gegevens op de client hello, Stel dat in Hallo 'todo list' bijvoorbeeld Device1 haalt alleen items die niet zijn voltooid. Een stukje 'Melk koopt' is gemarkeerd als voltooid op Hallo server door een ander apparaat. Device1 heeft echter nog steeds Hallo 'Melk koopt' taken in het lokale archief omdat deze is alleen binnenhalen van items die niet als voltooid gemarkeerd. Een opschonen wordt dit item verouderde gewist.

## <a name="next-steps"></a>Volgende stappen
* [iOS: offlinesynchronisatie inschakelen]
* [Xamarin iOS: offlinesynchronisatie inschakelen]
* [Xamarin Android: Offlinesynchronisatie inschakelen]
* [universele Windows-Platform: inschakelen offlinesynchronisatie]

<!-- Links -->
[SDK voor .NET-clients]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: Offlinesynchronisatie inschakelen]: app-service-mobile-android-get-started-offline-data.md
[iOS: offlinesynchronisatie inschakelen]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: offlinesynchronisatie inschakelen]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: Offlinesynchronisatie inschakelen]: app-service-mobile-xamarin-android-get-started-offline-data.md
[universele Windows-Platform: inschakelen offlinesynchronisatie]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
