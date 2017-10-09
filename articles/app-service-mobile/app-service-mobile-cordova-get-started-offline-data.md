---
title: aaaEnable offlinesynchronisatie voor uw mobiele Apps van Azure (Cordova) | Microsoft Docs
description: Meer informatie over hoe toouse App Service-mobiele App toocache en sync offline gegevens in uw Cordova-toepassing
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Offlinesynchronisatie voor uw Cordova mobile app inschakelen
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

Deze zelfstudie introduceert Hallo offlinesynchronisatie functie van Azure Mobile Apps voor Cordova. Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding. Wijzigingen worden opgeslagen in een lokale database.  Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service Hallo.

Deze zelfstudie is gebaseerd op Hallo Cordova Quick Start-oplossing voor Mobile Apps die u maakt na voltooiing van de zelfstudie Hallo [snel starten van Apache Cordova]. In deze zelfstudie maakt bijwerken u Hallo Quick Start-oplossing tooadd offline functies van Azure Mobile Apps.  We ook markeren Hallo offline-specifieke code in Hallo app.

toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps]. Zie voor meer informatie over het gebruik van de API van Hallo [API-documentatie](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Offlinesynchronisatie toohello Quick Start oplossing toevoegen
Hallo offlinesynchronisatie code moet worden toegevoegd als toohello app. Offline synchronisatie vereist Hallo cordova-sqlite-opslag-invoegtoepassing, die automatisch opgehaald tooyour app toegevoegd wanneer hello Azure Mobile Apps-invoegtoepassing is opgenomen in het Hallo-project. Hallo Quick Start-project bevat zowel van deze invoegtoepassingen.

1. In Visual Studio Solution Explorer openen index.js en vervang Hallo na code

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    Met deze code:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Vervang vervolgens Hallo code te volgen:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    Met deze code:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    Hallo voorafgaande code toevoegingen initialiseren van het lokale archief Hallo en definiëren van een lokale tabel die overeenkomt met de Hallo kolomwaarden die worden gebruikt in uw Azure back-end. (U hoeft niet tooinclude alle waarden in de kolom in de volgende code.)  Hallo `version` veld wordt onderhouden door Hallo mobiele back-end en wordt gebruikt voor het oplossen van conflicten.

    U een verwijzing toohello sync context ophalen door het aanroepen van **getSyncContext**. Hallo sync context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden `.push()` wordt aangeroepen.

3. Hallo toepassing URL tooyour mobiele App toepassing URL bijwerken.

4. Vervang vervolgens deze code:

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    Met deze code:

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    Hallo voorafgaande code initialiseert Hallo sync context en roept vervolgens getSyncTable (in plaats van een getTable) tooget een verwijzing toohello lokale tabel.

    Deze code maakt gebruik van Hallo lokale database voor alle maken, lezen, bijwerken en verwijderen (CRUD) tabel-bewerkingen.

    Dit voorbeeld voert eenvoudige foutafhandeling op synchronisatieconflicten. Een echte toepassing zou verwerken Hallo diverse fouten zoals netwerkomstandigheden, server conflicten en anderen. Zie voor voorbeelden van programmacode Hallo [offlinesynchronisatie voorbeeld].

5. Vervolgens voegt u deze functie tooperform Hallo werkelijke synchronisatie.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    U besluit waarop toopush backend voor mobiele Apps toohello gewijzigd door het aanroepen van **syncContext.push()**. U kunt bijvoorbeeld aanroepen **syncBackend** in een knop knop gebeurtenis-handler gebonden tooa synchronisatie.

## <a name="offline-sync-considerations"></a>Offlinesynchronisatie overwegingen

In voorbeeld Hallo Hallo **push** methode van **syncContext** alleen wordt aangeroepen voor het starten van de app in Hallo callback-functie voor aanmelding.  In een echte toepassing kan u de functionaliteit van deze synchronisatie handmatig geactiveerd of wanneer Hallo netwerk status is gewijzigd.

Wanneer een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates bijgehouden door Hallo-context, die pull-bewerking automatisch triggers een push. Bij het vernieuwen, toe te voegen en het voltooien van de items in dit voorbeeld, kunt u weglaten Hallo expliciete **push** aanroepen, omdat deze is mogelijk overbodig.

In de opgegeven Hallo code, alle records in de externe takentabel Hallo worden opgevraagd, maar het is ook mogelijk toofilter records door een query-id en de query te**push**. Zie voor meer informatie, Hallo sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps].

## <a name="optional-disable-authentication"></a>(Optioneel) Verificatie uit te schakelen

Als u niet tooset van verificatie wilt voordat u test offlinesynchronisatie, Hallo callback-functie voor aanmelding uitcommentariëren, maar laat Hallo-code in de callback-functie Hallo zonder opmerkingen.  Na het commentaarteken Hallo aanmelding regels, volgt Hallo code:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Nu Hallo app wordt gesynchroniseerd met hello Azure back-end wanneer u Hallo app uitvoert.

## <a name="run-hello-client-app"></a>Hallo client-app uitvoeren
Met offlinesynchronisatie is nu ingeschakeld, kunt u de clienttoepassing Hallo ten minste eenmaal uitvoeren voor elk platform Hallo winkel lokale database gevuld. Later een offline-scenario te simuleren en Hallo gegevens wijzigen in het lokale archief Hallo terwijl Hallo app offline is.

## <a name="optional-test-hello-sync-behavior"></a>(Optioneel) Test Hallo sync-gedrag
In deze sectie kunt u Hallo client project toosimulate een offline-scenario wijzigen met behulp van een ongeldige toepassings-URL voor uw back-end. Wanneer u toevoegen of wijzigen van gegevensitems, worden deze wijzigingen in het lokale archief worden bewaard, maar zijn niet gesynchroniseerde toohello back-end-gegevensarchief totdat het Hallo-verbinding is hersteld.

1. In Hallo Solution Explorer, open Hallo index.js projectbestand en Hallo toepassing URL toopoint wijzigen in een ongeldige URL, zoals Hallo code te volgen:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. Werk in index.html, Hallo CSP `<meta>` element met dezelfde ongeldige URL Hallo.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Bouw en Hallo client-app uitvoeren en u ziet dat er een uitzondering wordt geregistreerd in Hallo-console wanneer Hallo app probeert te synchroniseren met Hallo back-end na aanmelding. Geen nieuwe objecten die u toevoegt bestaan alleen in het lokale archief Hallo totdat ze worden gepusht toohello mobiele back-end. Hallo-clientapp gedraagt zich alsof het verbonden toohello back-end.

4. Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.

5. (Optioneel) Gebruik Visual Studio tooview uw Azure SQL Database-tabel toosee die Hallo-gegevens in Hallo back-end-database niet is gewijzigd.

    Open in Visual Studio **Server Explorer**. Navigeer tooyour database in **Azure**->**SQL-Databases**. Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**. Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Optioneel) Test Hallo opnieuw verbinden tooyour mobiele back-end

In deze sectie maakt u opnieuw verbinding maakt Hallo toohello mobiele back-end app Hallo app terug afkomstig is van een online status te simuleren. Wanneer u zich aanmeldt, is gegevens gesynchroniseerde tooyour mobiele back-end.

1. Open index.js en de URL van de toepassing hello herstellen.
2. Open index.html en corrigeer Hallo toepassings-URL in Hallo CSP `<meta>` element.
3. Opnieuw en Voer Hallo client-app. Hallo app probeert toosync met Hallo mobiele app back-end na aanmelding. Controleer of dat er geen uitzonderingen worden geregistreerd in Hallo-console voor foutopsporing.
4. (Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler. Kennisgeving Hallo gegevens is tussen Hallo back-end-database en het lokale archief Hallo gesynchroniseerd.

    U ziet Hallo gegevens tussen Hallo-database en het lokale archief Hallo is gesynchroniseerd en bevat Hallo items die u hebt toegevoegd terwijl de verbinding van uw app is verbroken.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Offline synchroniseren van gegevens in Azure Mobile Apps]
* [Visual Studio Tools for Apache Cordova]

## <a name="next-steps"></a>Volgende stappen
* Bekijk meer geavanceerde functies zoals conflictoplossing in Hallo offlinesynchronisatie [offlinesynchronisatie voorbeeld]
* Bekijk Hallo offlinesynchronisatie API-verwijzing in Hallo [API-documentatie](https://azure.github.io/azure-mobile-apps-js-client).

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[snel starten van Apache Cordova]: app-service-mobile-cordova-get-started.md
[offlinesynchronisatie voorbeeld]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
