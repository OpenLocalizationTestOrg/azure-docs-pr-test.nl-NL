---
title: aaaEnable offlinesynchronisatie voor uw mobiele Apps van Azure (Xamarin Android)
description: Meer informatie over hoe toouse App Service-mobiele App toocache en sync offline gegevens in uw Xamarin Android-toepassing
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a>Offlinesynchronisatie voor uw mobiele app voor Xamarin.Android inschakelen
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie maakt u kennis met Hallo offlinesynchronisatie functie van Azure Mobile Apps voor Xamarin.Android. Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app--weergeven, toevoegen of wijzigen van gegevens--, zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database.
Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service Hallo.

In deze zelfstudie maakt u Hallo client-project uit Hallo zelfstudie bijwerken [een Xamarin.android-app maken] toosupport Hallo offline functies van Azure Mobile Apps. Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo data access-extensie pakketten tooyour project toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Hallo app toosupport offline clientfuncties bijwerken
Azure Mobile Apps offline-functies kunnen u toointeract met een lokale database als u zich in een offline-scenario. toouse deze functies in uw app initialiseren een [SyncContext] tooa lokale archief. Vervolgens verwijzen naar de tabel via Hallo [IMobileServiceSyncTable] [IMobileServiceSyncTable] interface. SQLite wordt gebruikt als het lokale archief Hallo op Hallo-apparaat.

1. Open in Visual Studio Hallo NuGet-Pakketbeheer in Hallo-project dat u in Hallo voltooid [een Xamarin.android-app maken] zelfstudie.  Zoek en installeer Hallo **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket.
2. Hallo ToDoActivity.cs bestand openen en de opmerking verwijderen Hallo `#define OFFLINE_SYNC_ENABLED` definitie.
3. Druk in Visual Studio op Hallo **F5** belangrijke toorebuild en Voer Hallo client-app. Hallo-app werkt het Hallo dezelfde manier als toen u offlinesynchronisatie ingeschakeld. Hallo lokale database is echter nu gevuld met gegevens die kunnen worden gebruikt in een offline-scenario.

## <a name="update-sync"></a>Hallo app toodisconnect vanuit Hallo back-end bijwerken
In deze sectie verbreekt u Hallo verbinding tooyour mobiele App back-end toosimulate een offline situatie. Wanneer u gegevens toevoegt, uitzonderings-handler uitgelegd die Hallo-app in de offlinemodus. In deze status nieuwe items toegevoegd in lokale Hallo sla en worden gesynchroniseerd met de back-end van Hallo mobiele app als een push wordt uitgevoerd in een verbonden status.

1. ToDoActivity.cs in Hallo gedeeld project bewerken. Wijziging Hallo **applicationURL** toopoint tooan ongeldige URL:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    U kunt ook offline gedrag met Wi-Fi- en mobiele netwerken op Hallo apparaat uitschakelen of met vliegtuigmodus aantonen.
2. Druk op **F5** toobuild en Voer Hallo-app. U ziet de synchronisatie is mislukt bij vernieuwen wanneer Hallo app gestart.
3. Nieuwe items en Let op dat push is mislukt met de status [CancelledByNetworkError] telkens wanneer u klikt **opslaan**. Hallo nieuwe todo-items bestaan echter in het lokale archief Hallo totdat ze back-end van toohello mobiele app kunnen worden geactiveerd.  In een productie verbonden-app, als u deze uitzonderingen Hallo client-app gedraagt zich alsof deze nog steeds onderdrukken toohello mobiele app back-end.
4. Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.
5. (Optioneel) Open in Visual Studio **Server Explorer**. Navigeer tooyour database in **Azure**->**SQL-Databases**. Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**. Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren. Controleer of dat Hallo-gegevens in Hallo back-end-database niet is gewijzigd.
6. (Optioneel) Gebruik een REST-hulpprogramma zoals Fiddler of Postman tooquery uw mobiele back-end, met een GET-query in de vorm `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Hallo app tooreconnect backend voor mobiele Apps bijwerken
Opnieuw verbinden Hallo toohello mobiele app back-end apps in deze sectie. Wanneer u Hallo-toepassing voor het eerst uitvoert, Hallo `OnCreate` aanroepen gebeurtenis-handler `OnRefreshItemsSelected`. Deze methode aanroept `SyncAsync` toosync uw lokale opslaan met Hallo back-end-database.

1. ToDoActivity.cs in Hallo gedeeld project openen en herstellen van de wijziging van Hallo **applicationURL** eigenschap.
2. Druk op Hallo **F5** belangrijke toorebuild en Voer Hallo-app. Hallo app uw lokale worden wijzigingen gesynchroniseerd met Hallo mobiele Apps van Azure back-end push als pull-bewerkingen wanneer hello `OnRefreshItemsSelected` methode wordt uitgevoerd.
3. (Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler. Kennisgeving Hallo gegevens is tussen Hallo mobiele Apps van Azure back-end-database en het lokale archief Hallo gesynchroniseerd.
4. Klik in Hallo-app op Hallo controleren vak naast enkele items toocomplete ze in het lokale archief Hallo.

   `CheckItem`aanroepen `SyncAsync` toosync elke voltooid item met de back-end van Hallo mobiele App. `SyncAsync`Zowel push als pull-aanroepen. **Wanneer u een pull op basis van een tabel uitvoeren die Hallo-client heeft wijzigingen aangebracht in, een push altijd automatisch wordt uitgevoerd**. Hierdoor worden dat alle tabellen in het lokale archief samen met relaties consistent blijven. Dit gedrag kan resulteren in een onverwachte push. Zie voor meer informatie over dit gedrag [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="review-hello-client-sync-code"></a>Hallo-clientcode sync controleren
Hallo Xamarin client-project dat u hebt gedownload wanneer u Hallo-zelfstudie voltooid [een Xamarin.android-app maken] bevat al de code die offline synchronisatie met een lokale SQLite-database ondersteunt. Hier volgt een kort overzicht van wat al in de zelfstudie Hallo-code opgenomen is. Zie voor een conceptueel overzicht van de functie Hallo [Offline synchroniseren van gegevens in Azure Mobile Apps].

* Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd. Hallo lokale winkeldatabase is geïnitialiseerd als `ToDoActivity.OnCreate()` voert `ToDoActivity.InitLocalStoreAsync()`. Deze methode maakt u een lokale SQLite-database met behulp van Hallo `MobileServiceSQLiteStore` klasse zoals opgegeven door hello Azure Mobile Apps client SDK.

    Hallo `DefineTable` methode maakt een tabel in Hallo lokale archief dat overeenkomt met de velden Hallo in Hallo opgegeven type `ToDoItem` in dit geval. Hallo-type heeft geen tooinclude alle Hallo kolommen die zich in de externe database Hallo. Het is mogelijk toostore een subset kolommen.

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* Hallo `toDoTable` lid is van `ToDoActivity` is Hallo `IMobileServiceSyncTable` typt u in plaats van `IMobileServiceTable`. Hallo IMobileServiceSyncTable zorgt ervoor dat alle maken, lezen, bijwerken en verwijderen (CRUD) tabel operations toohello winkel lokale-database.

    U besluit wanneer wijzigingen toohello mobiele Apps van Azure back-end gepusht door het aanroepen van `IMobileServiceSyncContext.PushAsync()`. Hallo sync context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden `PushAsync` wordt aangeroepen.

    Hallo opgegeven code aanroepen `ToDoActivity.SyncAsync()` toosync wanneer Hallo takentabel lijst wordt vernieuwd of een todoitem is toegevoegd of voltooid. Hallo code synchronisaties na elke wijziging van de lokale.

    In de opgegeven Hallo code, alle records in externe Hallo `TodoItem` tabel worden opgevraagd, maar het is ook mogelijk toofilter records door een query-id en de query te`PushAsync`. Zie voor meer informatie, Hallo sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps].

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a>Aanvullende resources
* [Offline synchroniseren van gegevens in Azure Mobile Apps]
* [Azure Mobile Apps .NET SDK procedure][8]

<!-- URLs. -->
[een Xamarin.android-app maken]: ../app-service-mobile-xamarin-android-get-started.md
[Offline synchroniseren van gegevens in Azure Mobile Apps]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Een Xamarin.android-app maken]: app-service-mobile-xamarin-android-get-started.md
[Offlinesynchronisatie van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
