---
title: aaaEnable offlinesynchronisatie voor uw mobiele Apps van Azure (Xamarin iOS)
description: Meer informatie over hoe toouse App Service-mobiele App toocache en sync offline gegevens in uw Xamarin iOS-toepassing
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>Offlinesynchronisatie inschakelen voor uw mobiele Xamarin.iOS-app
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie maakt u kennis met Hallo offlinesynchronisatie functie van Azure Mobile Apps voor Xamarin.iOS. Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app--weergeven, toevoegen of wijzigen van gegevens--, zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database. Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service Hallo.

In deze zelfstudie bijwerken Hallo Xamarin.iOS-app-project uit [een Xamarin iOS-app maken] toosupport Hallo offline functies van Azure Mobile Apps. Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo data access-extensiepakketten toevoegen aan uw project. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Hallo app toosupport offline clientfuncties bijwerken
Azure Mobile Apps offline-functies kunnen u toointeract met een lokale database als u zich in een offline-scenario. initialiseren van toouse deze functies in uw app een [SyncContext] tooa lokale archief. Verwijzen naar de tabel via Hallo [IMobileServiceSyncTable]-interface. SQLite wordt gebruikt als het lokale archief Hallo op Hallo-apparaat.

1. Open Hallo NuGet-Pakketbeheer in Hallo-project dat u in Hallo voltooid [een Xamarin iOS-app maken] zelfstudie vervolgens zoeken naar en installeren Hallo **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet het pakket.
2. Hallo QSTodoService.cs bestand openen en de opmerking verwijderen Hallo `#define OFFLINE_SYNC_ENABLED` definitie.
3. Opnieuw en Voer Hallo client-app. Hallo-app werkt het Hallo dezelfde manier als toen u offlinesynchronisatie ingeschakeld. Hallo lokale database is echter nu gevuld met gegevens die kunnen worden gebruikt in een offline-scenario.

## <a name="update-sync"></a>Hallo app toodisconnect vanuit Hallo back-end bijwerken
In deze sectie verbreekt u Hallo verbinding tooyour mobiele App back-end toosimulate een offline situatie. Wanneer u gegevens toevoegt, uitzonderings-handler uitgelegd die Hallo-app in de offlinemodus. In deze status nieuwe items toegevoegd in lokale Hallo sla en worden gesynchroniseerd als u wilt back-end voor mobiele app Hallo wanneer push vervolgens in een verbonden status wordt uitgevoerd.

1. QSToDoService.cs in Hallo gedeeld project bewerken. Wijziging Hallo **applicationURL** toopoint tooan ongeldige URL:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    U kunt ook offline gedrag met Wi-Fi- en mobiele netwerken op Hallo apparaat uitschakelen of met vliegtuigmodus aantonen.
2. Ontwikkel en Voer Hallo-app. U ziet de synchronisatie is mislukt bij vernieuwen wanneer Hallo app gestart.
3. Nieuwe items en Let op dat push is mislukt met de status [CancelledByNetworkError] telkens wanneer u klikt **opslaan**. Hallo nieuwe todo-items bestaan echter in het lokale archief Hallo totdat ze back-end van toohello mobiele app kunnen worden geactiveerd.  In een productie verbonden-app, als u deze uitzonderingen Hallo client-app gedraagt zich alsof deze nog steeds onderdrukken toohello mobiele app back-end.
4. Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.
5. (Optioneel) Als u Visual Studio geïnstalleerd op een PC is, open **Server Explorer**. Navigeer tooyour database in **Azure**-> **SQL-Databases**. Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**. Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren. Controleer of dat Hallo-gegevens in Hallo back-end-database niet is gewijzigd.
6. (Optioneel) Gebruik een REST-hulpprogramma zoals Fiddler of Postman tooquery uw mobiele back-end, met een GET-query in de vorm `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Hallo app tooreconnect backend voor mobiele Apps bijwerken
Opnieuw verbinden Hallo toohello mobiele app back-end apps in deze sectie. Dit wordt gesimuleerd Hallo app verplaatsen van een online status van offlinestatus tooan met Hallo mobiele app back-end.   Als u Hallo netwerk breuken gesimuleerd door het uitschakelen van verbinding met het netwerk, worden er geen codewijzigingen nodig.
Hallo netwerk weer inschakelen.  Wanneer u Hallo-toepassing voor het eerst uitvoert, Hallo `RefreshDataAsync` methode wordt aangeroepen. Dit wordt opgeroepen `SyncAsync` toosync uw lokale opslaan met Hallo back-end-database.

1. QSToDoService.cs in Hallo gedeeld project openen en herstellen van de wijziging van Hallo **applicationURL** eigenschap.
2. Bouwen en uitvoeren Hallo-app. Hallo app uw lokale worden wijzigingen gesynchroniseerd met Hallo mobiele Apps van Azure back-end push als pull-bewerkingen wanneer hello `OnRefreshItemsSelected` methode wordt uitgevoerd.
3. (Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler. Kennisgeving Hallo gegevens is tussen Hallo mobiele Apps van Azure back-end-database en het lokale archief Hallo gesynchroniseerd.
4. Klik in Hallo-app op Hallo controleren vak naast enkele items toocomplete ze in het lokale archief Hallo.

   `CompleteItemAsync`aanroepen `SyncAsync` toosync elke voltooid item met de back-end van Hallo mobiele App. `SyncAsync`Zowel push als pull-aanroepen.
   **Wanneer u een pull op basis van een tabel uitvoeren die Hallo-client heeft wijzigingen aangebracht in, een push op Hallo sync clientcontext wordt altijd eerst uitgevoerd automatisch**. Hallo impliciete push zorgt ervoor dat alle tabellen in het lokale archief Hallo samen met relaties consistent blijven. Zie voor meer informatie over dit gedrag [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="review-hello-client-sync-code"></a>Hallo-clientcode sync controleren
Hallo Xamarin client-project dat u hebt gedownload wanneer u Hallo-zelfstudie voltooid [een Xamarin iOS-app maken] bevat al de code die offline synchronisatie met een lokale SQLite-database ondersteunt. Hier volgt een kort overzicht van wat al in de zelfstudie Hallo-code opgenomen is. Zie voor een conceptueel overzicht van de functie Hallo [Offline synchroniseren van gegevens in Azure Mobile Apps].

* Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd. Hallo lokale winkeldatabase is geïnitialiseerd als `QSTodoListViewController.ViewDidLoad()` voert `QSTodoService.InitializeStoreAsync()`. Deze methode maakt u een nieuwe lokale SQLite-database met behulp van Hallo `MobileServiceSQLiteStore` klasse zoals opgegeven door hello Azure Mobile Apps client SDK.

    Hallo `DefineTable` methode maakt een tabel in Hallo lokale archief dat overeenkomt met de velden Hallo in Hallo opgegeven type `ToDoItem` in dit geval. Hallo-type heeft geen tooinclude alle Hallo kolommen die zich in de externe database Hallo. Het is mogelijk toostore een subset kolommen.

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* Hallo `todoTable` lid is van `QSTodoService` is Hallo `IMobileServiceSyncTable` typt u in plaats van `IMobileServiceTable`. Hallo IMobileServiceSyncTable zorgt ervoor dat alle maken, lezen, bijwerken en verwijderen (CRUD) tabel operations toohello winkel lokale-database.

    U besluit wanneer deze wijzigingen toohello mobiele Apps van Azure back-end gepusht door het aanroepen van `IMobileServiceSyncContext.PushAsync()`. Hallo sync context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden `PushAsync` wordt aangeroepen.

    Hallo opgegeven code aanroepen `QSTodoService.SyncAsync()` toosync wanneer Hallo takentabel lijst wordt vernieuwd of een todoitem is toegevoegd of voltooid. De app wordt gesynchroniseerd na elke wijziging van de lokale. Als een pull wordt uitgevoerd op basis van een tabel die nog in behandeling zijnde lokale updates bijgehouden door de Hallo context, wordt die pullbewerking automatisch geactiveerd een context push eerst.

    In de opgegeven Hallo code, alle records in externe Hallo `TodoItem` tabel worden opgevraagd, maar het is ook mogelijk toofilter records door een query-id en de query te`PushAsync`. Zie voor meer informatie, Hallo sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps].

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>Aanvullende resources
* [Offline synchroniseren van gegevens in Azure Mobile Apps]
* [Azure Mobile Apps .NET SDK procedure][8]

<!-- Images -->

<!-- URLs. -->
[een Xamarin iOS-app maken]: app-service-mobile-xamarin-ios-get-started.md
[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
