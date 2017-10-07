---
title: aaaEnable offlinesynchronisatie voor uw app Universal Windows Platform (UWP) met Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toouse een Azure Mobile Apps toocache en sync offline gegevens in uw app Universal Windows Platform (UWP).
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Offlinesynchronisatie voor uw Windows-app inschakelen
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe de offline tooadd tooa Universal Windows Platform (UWP)-app met behulp van een back-end voor mobiele Apps van Azure ondersteunen. Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app--weergeven, toevoegen of wijzigen van gegevens -, zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database. Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met Hallo externe back-end.

In deze zelfstudie maakt u Hallo UWP-appproject uit Hallo zelfstudie bijwerken [maken van een Windows-app] toosupport Hallo offline functies van Azure Mobile Apps. Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo data access-extensie pakketten tooyour project toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="requirements"></a>Vereisten
Deze zelfstudie vereist Hallo volgende vereisten:

* Visual Studio 2013 met Windows 8.1 of hoger.
* Voltooiing van [maken van een Windows-app][een windows-app maken].
* [Azure Mobile Services SQLite Store][sqlite store nuget]
* [SQLite voor de ontwikkeling van universele Windows-Platform](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Hallo app toosupport offline clientfuncties bijwerken
Azure Mobile Apps offline-functies kunnen u toointeract met een lokale database als u zich in een offline-scenario. toouse deze functies in uw app initialiseren een [SyncContext] [ synccontext] tooa lokale archief. Vervolgens verwijzen naar de tabel via Hallo [IMobileServiceSyncTable][IMobileServiceSyncTable] interface. SQLite wordt gebruikt als het lokale archief Hallo op Hallo-apparaat.

1. Hallo installeren [SQLite-runtime voor Hallo universele Windows-Platform](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. Open in Visual Studio Hallo NuGet package manager voor Hallo UWP-appproject die u in Hallo voltooid [maken van een Windows-app] zelfstudie.
    Zoek en installeer Hallo **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket.
3. Klik in Solution Explorer met de rechtermuisknop op **verwijzingen** > **verwijzing toevoegen...** >**Universeel Windows** > **extensies**, schakelt u beide **SQLite voor Universal Windows Platform** en **Visual C++-2015-Runtime voor universele Windows-Platform-apps**.

    ![SQLite UWP-verwijzing toevoegen][1]
4. Hallo MainPage.xaml.cs bestand openen en de opmerking verwijderen Hallo `#define OFFLINE_SYNC_ENABLED` definitie.
5. Druk in Visual Studio op Hallo **F5** belangrijke toorebuild en Voer Hallo client-app. Hallo-app werkt het Hallo dezelfde manier als toen u offlinesynchronisatie ingeschakeld. Hallo lokale database is echter nu gevuld met gegevens die kunnen worden gebruikt in een offline-scenario.

## <a name="update-sync"></a>Hallo app toodisconnect vanuit Hallo back-end bijwerken
In deze sectie verbreekt u Hallo verbinding tooyour mobiele App back-end toosimulate een offline situatie. Wanneer u gegevens toevoegt, uitzonderings-handler uitgelegd die Hallo-app in de offlinemodus. In deze status nieuwe items toegevoegd in lokale Hallo sla en worden gesynchroniseerd als u wilt back-end voor mobiele app Hallo wanneer push vervolgens in een verbonden status wordt uitgevoerd.

1. App.xaml.cs in Hallo gedeeld project bewerken. Hallo-initialisatie van Hallo commentaar **MobileServiceClient** en Hallo volgt regel dat gebruikmaakt van een ongeldige mobiele app-URL toe te voegen:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    U kunt ook offline gedrag demonstreren door Wi-Fi- en mobiele netwerken op Hallo apparaat uit te schakelen of vliegtuigmodus gebruiken.
2. Druk op **F5** toobuild en Voer Hallo-app. U ziet de synchronisatie is mislukt bij vernieuwen wanneer Hallo app gestart.
3. Nieuwe items en Let op dat push is mislukt met een [CancelledByNetworkError] status telkens wanneer u klikt **opslaan**. Hallo nieuwe todo-items bestaan echter in het lokale archief Hallo totdat ze back-end van toohello mobiele app kunnen worden geactiveerd.  In een productie verbonden-app, als u deze uitzonderingen Hallo client-app gedraagt zich alsof deze nog steeds onderdrukken toohello mobiele app back-end.
4. Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.
5. (Optioneel) Open in Visual Studio **Server Explorer**. Navigeer tooyour database in **Azure**->**SQL-Databases**. Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**. Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren. Controleer of dat Hallo-gegevens in Hallo back-end-database niet is gewijzigd.
6. (Optioneel) Gebruik een REST-hulpprogramma zoals Fiddler of Postman tooquery uw mobiele back-end, met een GET-query in de vorm `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Hallo app tooreconnect backend voor mobiele Apps bijwerken
In deze sectie maakt u opnieuw verbinding maakt Hallo app toohello mobiele app back-end. Deze wijzigingen simuleren opnieuw op Hallo app verbinden met een netwerk.

Wanneer u Hallo-toepassing voor het eerst uitvoert, Hallo `OnNavigatedTo` aanroepen gebeurtenis-handler `InitLocalStoreAsync`. Deze methode aanroept op zijn beurt `SyncAsync` toosync uw lokale opslaan met Hallo back-end-database. Hallo app probeert toosync bij het opstarten.

1. Open App.xaml.cs in Hallo gedeeld project en verwijder de opmerkingen in de vorige initialisatie van `MobileServiceClient` toouse Hallo juist Hallo mobiele app-URL.
2. Druk op Hallo **F5** belangrijke toorebuild en Voer Hallo-app. Hallo app uw lokale worden wijzigingen gesynchroniseerd met Hallo mobiele Apps van Azure back-end push als pull-bewerkingen wanneer hello `OnNavigatedTo` gebeurtenis-handler wordt uitgevoerd.
3. (Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler. Kennisgeving Hallo gegevens is tussen Hallo mobiele Apps van Azure back-end-database en het lokale archief Hallo gesynchroniseerd.
4. Klik in Hallo-app op Hallo controleren vak naast enkele items toocomplete ze in het lokale archief Hallo.

   `UpdateCheckedTodoItem`aanroepen `SyncAsync` toosync elke voltooid item met de back-end van Hallo mobiele App. `SyncAsync`Zowel push als pull-aanroepen. Echter, **wanneer het uitvoeren van een pull op basis van een tabel die Hallo-client heeft wijzigingen aangebracht in, een push altijd automatisch wordt uitgevoerd**. Dit gedrag zorgt ervoor dat alle tabellen in het lokale archief Hallo samen met relaties consistent blijven. Dit gedrag kan resulteren in een onverwachte push.  Zie voor meer informatie over dit gedrag [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="api-summary"></a>API-overzicht
toosupport hello offline functies van mobiele services, hebben we Hallo gebruikt [IMobileServiceSyncTable] interface en geïnitialiseerd [MobileServiceClient.SyncContext] [ synccontext] met een lokale SQLite-database. Als offline, Hallo normale CRUD-bewerkingen voor mobiele Apps werken alsof Hallo app nog steeds verbinding terwijl Hallo-bewerkingen op basis van het lokale archief Hallo plaatsvinden. Hallo volgende methoden zijn gebruikte toosynchronize Hallo lokale opslag met Hallo-server:

* **[PushAsync]**  omdat deze methode deel uit van maakt [IMobileServicesSyncContext], wijzigingen in alle tabellen worden gepusht toohello back-end. Alleen records met lokale wijzigingen worden toohello server verzonden.
* **[PullAsync]**  een pull wordt gestart vanuit een [IMobileServiceSyncTable]. Wanneer er wijzigingen in de tabel hello, is een impliciete push toomake u ervoor zorgen dat alle tabellen in het lokale archief Hallo samen met relaties consistent blijven uitvoeren. Hallo *pushOtherTables* parameter besturingselementen in een impliciete push of andere tabellen in de context van Hallo worden gepusht. Hallo *query* parameter heeft een [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] of OData-query-tekenreeks toofilter Hallo gegevens geretourneerd. Hallo *queryId* parameter wordt gebruikt toodefine incrementele synchronisatie. Zie voor meer informatie [Offline synchroniseren van gegevens in Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  uw app moet periodiek aanroepen van deze methode toopurge verouderde gegevens uit het lokale archief Hallo. Gebruik Hallo *forceren* parameter als u alle wijzigingen die nog niet zijn gesynchroniseerd toopurge nodig.

Zie voor meer informatie over deze concepten [Offline synchroniseren van gegevens in Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Meer informatie
Hallo volgende onderwerpen bieden aanvullende achtergrondinformatie over Hallo offlinesynchronisatie functie van mobiele Apps:

* [Offline synchroniseren van gegevens in Azure Mobile Apps]
* [Azure Mobile Apps .NET SDK procedure][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[een windows-app maken]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
