---
title: aaaEnable offlinesynchronisatie voor uw mobiele Apps van Azure (Xamarin.Forms) | Microsoft Docs
description: Meer informatie over hoe App Service-mobiele App toocache en sync offline gegevens in uw toepassing Xamarin.Forms toouse
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Offlinesynchronisatie inschakelen voor uw mobiele Xamarin.Forms-app
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie introduceert Hallo offlinesynchronisatie functie van Azure Mobile Apps voor Xamarin.Forms. Offlinesynchronisatie kan eindgebruikers werken met een mobiele app--weergeven, toevoegen of wijzigen van gegevens--, zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database. Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service Hallo.

Deze zelfstudie is gebaseerd op Hallo Xamarin.Forms Quick Start-oplossing voor Mobile Apps die u maakt wanneer u de zelfstudie [een Xamarin iOS-app maken] voltooit. Hallo Quick Start-oplossing voor Xamarin.Forms bevat Hallo code toosupport offlinesynchronisatie, die alleen toobe ingeschakeld moet. In deze zelfstudie maakt bijwerken u Hallo Quick Start-oplossing tooturn op Hallo offline functies van Azure Mobile Apps. We ook markeren Hallo offline-specifieke code in Hallo app. Als u geen Hallo gedownloade Quick Start-oplossing gebruikt, moet u Hallo data access-extensie pakketten tooyour project toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][1].

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Schakel offlinesynchronisatie-functionaliteit in Hallo Quick Start-oplossing
Hallo offlinesynchronisatie code is opgenomen in het Hallo-project met behulp van C# preprocessor-instructies. Wanneer Hallo **OFFLINE\_SYNC\_ingeschakeld** symbool is gedefinieerd, wordt deze codepaden zijn opgenomen in Hallo build. Voor Windows-apps, moet u ook Hallo SQLite-platform installeren.

1. In Visual Studio met de rechtermuisknop op Hallo oplossing > **NuGet-pakketten beheren voor oplossing...** , zoek vervolgens naar en installeren de **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket voor alle projecten in Hallo-oplossing.
2. Open in Solution Explorer Hallo, Hallo TodoItemManager.cs bestand uit Hallo-project met **draagbare** in naam van Hallo Portable Class Library-project is, verwijder vervolgens de opmerkingen Hallo preprocessor-instructie te volgen:

        #define OFFLINE_SYNC_ENABLED
3. Windows-apparaten (optioneel) toosupport, installeert u een Hallo SQLite runtime pakketten te volgen:

   * **Windows 8.1 Runtime:** installeren [SQLite voor Windows 8.1][3].
   * **Windows Phone 8.1:** installeren [SQLite voor Windows Phone 8.1][4].
   * **Universele Windows-Platform** installeren [SQLite voor universele Windows universele Hallo][5].

     Hoewel Hallo Quick Start geen een universele Windows-project bevat, wordt met Xamarin Forms Hallo Universal Windows platform ondersteund.
4. (Optioneel) Elke Windows-app-project met de rechtermuisknop op **verwijzingen** > **verwijzing toevoegen...** , vouw Hallo **Windows** map > **extensies**.
    Inschakelen van de juiste Hallo **SQLite voor Windows** SDK samen met de Hallo **Visual C++ 2013-Runtime voor Windows** SDK.
    Hallo verschillen SQLite SDK namen met elke Windows-platform.

## <a name="review-hello-client-sync-code"></a>Hallo-clientcode sync controleren
Hier volgt een kort overzicht van wat al in de zelfstudie code binnen Hallo Hallo opgenomen is `#if OFFLINE_SYNC_ENABLED` richtlijnen. De offlinesynchronisatie-functionaliteit is in Hallo TodoItemManager.cs projectbestand in Hallo Portable Class Library-project. Zie voor een conceptueel overzicht van de functie Hallo [Offline synchroniseren van gegevens in Azure Mobile Apps][2].

* Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd. Hallo lokale winkeldatabase is geïnitialiseerd in Hallo **TodoItemManager** klassen-constructor met behulp van de volgende code Hallo:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Deze code maakt een nieuwe lokale SQLite-database met behulp van Hallo **MobileServiceSQLiteStore** klasse.

    Hallo **DefineTable** methode maakt een tabel in Hallo lokale archief die overeenkomt met de Hallo velden in Hallo opgegeven type.  Hallo-type heeft geen tooinclude alle Hallo kolommen die zich in de externe database Hallo. Het is mogelijk toostore een subset kolommen.
* Hallo **todoTable** veld **TodoItemManager** is een **IMobileServiceSyncTable** typt u in plaats van **IMobileServiceTable**. Deze klasse gebruikt Hallo lokale database voor alle maken, lezen, bijwerken en verwijderen (CRUD) tabel-bewerkingen. U besluit wanneer deze wijzigingen backend voor mobiele Apps toohello gepusht door aan te roepen **PushAsync** op Hallo **IMobileServiceSyncContext**. Hallo sync context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden **PushAsync** wordt aangeroepen.

    Hallo volgende **SyncAsync** methode wordt aangeroepen toosync met Hallo mobiele App back-end:

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    Dit voorbeeld maakt gebruik van eenvoudige foutafhandeling Hallo standaard synchronisatie handler. Een echte toepassing hello diverse fouten zoals netwerkomstandigheden en server veroorzaakt een conflict met behulp van een aangepaste zou verwerken **IMobileServiceSyncHandler** implementatie.

## <a name="offline-sync-considerations"></a>Offlinesynchronisatie overwegingen
In voorbeeld Hallo Hallo **SyncAsync** methode alleen wordt aangeroepen voor opstarten en waarop een synchronisatie wordt aangevraagd.  tooinitiate een synchronisatie in een Android- of iOS-app, pull omlaag in de lijst items Hallo; Gebruik voor Windows hello **Sync** knop. In een echte toepassing kan u Hallo synchronisatie activeren wanneer Hallo netwerk status verandert.

Wanneer een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates bijgehouden door Hallo-context, die pull-bewerking automatisch triggers een voorgaande context push. Bij het vernieuwen, toe te voegen en het voltooien van de items in dit voorbeeld, kunt u weglaten Hallo expliciete **PushAsync** aanroepen.

In de opgegeven Hallo code, alle records in de externe takentabel Hallo worden opgevraagd, maar het is ook mogelijk toofilter records door een query-id en de query te**PushAsync**. Zie voor meer informatie, Hallo sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps][2].

## <a name="run-hello-client-app"></a>Hallo client-app uitvoeren
Ten minste eenmaal uitgevoerd Hallo-clienttoepassing op elk platform toopopulate Hallo winkel lokale database met het offline synchroniseren van nu is ingeschakeld. Later een offline-scenario te simuleren en Hallo gegevens wijzigen in het lokale archief Hallo terwijl Hallo app offline is.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Hallo sync-gedrag Hallo client-app bijwerken
In deze sectie Hallo client project toosimulate een offline-scenario te wijzigen met behulp van een ongeldige toepassings-URL voor uw back-end. U kunt ook netwerkverbindingen uitschakelen door het apparaat te verplaatsen 'Vliegtuigmodus'.  Wanneer u toevoegen of wijzigen van gegevensitems, deze wijzigingen zijn ondergebracht in het lokale archief hello, maar niet gesynchroniseerd toohello back-endgegevens opslaan totdat het Hallo-verbinding is hersteld.

1. Open in Solution Explorer Hallo, Hallo Constants.cs projectbestand van Hallo **draagbare** project en wijzig de waarde Hallo van `ApplicationURL` toopoint tooan ongeldige URL:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Open Hallo TodoItemManager.cs bestand van Hallo **draagbare** project en voeg een **catch** voor Hallo base **uitzondering** klasse toohello **try... catch** blokkeren in **SyncAsync**. Dit **catch** blok schrijft Hallo uitzondering bericht toohello-console als volgt:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Ontwikkel en Voer Hallo client-app.  Aantal nieuwe items toevoegen. U ziet dat er een uitzondering wordt geregistreerd in de console Hallo voor elke poging toosync met Hallo back-end. Deze nieuwe items bestaan alleen in het lokale archief Hallo totdat ze toohello mobiele back-end kunnen worden geactiveerd. Hallo-clientapp gedraagt zich alsof het verbonden toohello backend, ondersteunen die alle maken, lezen, update, delete (CRUD)-bewerkingen.
4. Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.
5. (Optioneel) Gebruik Visual Studio tooview uw Azure SQL Database-tabel toosee die Hallo-gegevens in Hallo back-end-database niet is gewijzigd.

    Open in Visual Studio **Server Explorer**. Navigeer tooyour database in **Azure**->**SQL-Databases**. Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**. Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Uw mobiele back-end voor Hallo client app tooreconnect bijwerken
In deze sectie opnieuw verbinding Hallo toohello mobiele back-end app Hallo app terugkomen tooan online status te simuleren. Wanneer u Hallo vernieuwen gebaar uitvoert, is gegevens gesynchroniseerde tooyour mobiele back-end.

1. Open Constants.cs. Juiste Hallo `applicationURL` toopoint toohello Corrigeer de URL.
2. Opnieuw en Voer Hallo client-app. Hallo app probeert toosync met Hallo mobiele app back-end nadat u hebt. Controleer of dat er geen uitzonderingen worden geregistreerd in Hallo-console voor foutopsporing.
3. (Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler of [Postman][6]. Kennisgeving Hallo gegevens is tussen Hallo back-end-database en het lokale archief Hallo gesynchroniseerd.

    U ziet Hallo gegevens tussen Hallo-database en het lokale archief Hallo is gesynchroniseerd en bevat Hallo items die u hebt toegevoegd terwijl de verbinding van uw app is verbroken.

## <a name="additional-resources"></a>Aanvullende resources
* [Offline synchroniseren van gegevens in Azure Mobile Apps][2]
* [Azure Mobile Apps .NET SDK procedure][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
