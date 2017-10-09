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
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="b0243-103">Offlinesynchronisatie voor uw Cordova mobile app inschakelen</span><span class="sxs-lookup"><span data-stu-id="b0243-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="b0243-104">Deze zelfstudie introduceert Hallo offlinesynchronisatie functie van Azure Mobile Apps voor Cordova.</span><span class="sxs-lookup"><span data-stu-id="b0243-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="b0243-105">Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="b0243-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="b0243-106">Wijzigingen worden opgeslagen in een lokale database.</span><span class="sxs-lookup"><span data-stu-id="b0243-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="b0243-107">Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0243-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="b0243-108">Deze zelfstudie is gebaseerd op Hallo Cordova Quick Start-oplossing voor Mobile Apps die u maakt na voltooiing van de zelfstudie Hallo [snel starten van Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="b0243-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="b0243-109">In deze zelfstudie maakt bijwerken u Hallo Quick Start-oplossing tooadd offline functies van Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="b0243-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="b0243-110">We ook markeren Hallo offline-specifieke code in Hallo app.</span><span class="sxs-lookup"><span data-stu-id="b0243-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="b0243-111">toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b0243-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="b0243-112">Zie voor meer informatie over het gebruik van de API van Hallo [API-documentatie](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="b0243-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="b0243-113">Offlinesynchronisatie toohello Quick Start oplossing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0243-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="b0243-114">Hallo offlinesynchronisatie code moet worden toegevoegd als toohello app.</span><span class="sxs-lookup"><span data-stu-id="b0243-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="b0243-115">Offline synchronisatie vereist Hallo cordova-sqlite-opslag-invoegtoepassing, die automatisch opgehaald tooyour app toegevoegd wanneer hello Azure Mobile Apps-invoegtoepassing is opgenomen in het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="b0243-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="b0243-116">Hallo Quick Start-project bevat zowel van deze invoegtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="b0243-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="b0243-117">In Visual Studio Solution Explorer openen index.js en vervang Hallo na code</span><span class="sxs-lookup"><span data-stu-id="b0243-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="b0243-118">Met deze code:</span><span class="sxs-lookup"><span data-stu-id="b0243-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="b0243-119">Vervang vervolgens Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0243-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="b0243-120">Met deze code:</span><span class="sxs-lookup"><span data-stu-id="b0243-120">with this code:</span></span>

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

    <span data-ttu-id="b0243-121">Hallo voorafgaande code toevoegingen initialiseren van het lokale archief Hallo en definiëren van een lokale tabel die overeenkomt met de Hallo kolomwaarden die worden gebruikt in uw Azure back-end.</span><span class="sxs-lookup"><span data-stu-id="b0243-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="b0243-122">(U hoeft niet tooinclude alle waarden in de kolom in de volgende code.)  Hallo `version` veld wordt onderhouden door Hallo mobiele back-end en wordt gebruikt voor het oplossen van conflicten.</span><span class="sxs-lookup"><span data-stu-id="b0243-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="b0243-123">U een verwijzing toohello sync context ophalen door het aanroepen van **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="b0243-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="b0243-124">Hallo sync context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden `.push()` wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b0243-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="b0243-125">Hallo toepassing URL tooyour mobiele App toepassing URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b0243-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="b0243-126">Vervang vervolgens deze code:</span><span class="sxs-lookup"><span data-stu-id="b0243-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="b0243-127">Met deze code:</span><span class="sxs-lookup"><span data-stu-id="b0243-127">with this code:</span></span>

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

    <span data-ttu-id="b0243-128">Hallo voorafgaande code initialiseert Hallo sync context en roept vervolgens getSyncTable (in plaats van een getTable) tooget een verwijzing toohello lokale tabel.</span><span class="sxs-lookup"><span data-stu-id="b0243-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="b0243-129">Deze code maakt gebruik van Hallo lokale database voor alle maken, lezen, bijwerken en verwijderen (CRUD) tabel-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b0243-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="b0243-130">Dit voorbeeld voert eenvoudige foutafhandeling op synchronisatieconflicten.</span><span class="sxs-lookup"><span data-stu-id="b0243-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="b0243-131">Een echte toepassing zou verwerken Hallo diverse fouten zoals netwerkomstandigheden, server conflicten en anderen.</span><span class="sxs-lookup"><span data-stu-id="b0243-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="b0243-132">Zie voor voorbeelden van programmacode Hallo [offlinesynchronisatie voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="b0243-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="b0243-133">Vervolgens voegt u deze functie tooperform Hallo werkelijke synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="b0243-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="b0243-134">U besluit waarop toopush backend voor mobiele Apps toohello gewijzigd door het aanroepen van **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="b0243-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="b0243-135">U kunt bijvoorbeeld aanroepen **syncBackend** in een knop knop gebeurtenis-handler gebonden tooa synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="b0243-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="b0243-136">Offlinesynchronisatie overwegingen</span><span class="sxs-lookup"><span data-stu-id="b0243-136">Offline sync considerations</span></span>

<span data-ttu-id="b0243-137">In voorbeeld Hallo Hallo **push** methode van **syncContext** alleen wordt aangeroepen voor het starten van de app in Hallo callback-functie voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0243-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="b0243-138">In een echte toepassing kan u de functionaliteit van deze synchronisatie handmatig geactiveerd of wanneer Hallo netwerk status is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b0243-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="b0243-139">Wanneer een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates bijgehouden door Hallo-context, die pull-bewerking automatisch triggers een push.</span><span class="sxs-lookup"><span data-stu-id="b0243-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="b0243-140">Bij het vernieuwen, toe te voegen en het voltooien van de items in dit voorbeeld, kunt u weglaten Hallo expliciete **push** aanroepen, omdat deze is mogelijk overbodig.</span><span class="sxs-lookup"><span data-stu-id="b0243-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="b0243-141">In de opgegeven Hallo code, alle records in de externe takentabel Hallo worden opgevraagd, maar het is ook mogelijk toofilter records door een query-id en de query te**push**.</span><span class="sxs-lookup"><span data-stu-id="b0243-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="b0243-142">Zie voor meer informatie, Hallo sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="b0243-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="b0243-143">(Optioneel) Verificatie uit te schakelen</span><span class="sxs-lookup"><span data-stu-id="b0243-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="b0243-144">Als u niet tooset van verificatie wilt voordat u test offlinesynchronisatie, Hallo callback-functie voor aanmelding uitcommentariëren, maar laat Hallo-code in de callback-functie Hallo zonder opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="b0243-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="b0243-145">Na het commentaarteken Hallo aanmelding regels, volgt Hallo code:</span><span class="sxs-lookup"><span data-stu-id="b0243-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="b0243-146">Nu Hallo app wordt gesynchroniseerd met hello Azure back-end wanneer u Hallo app uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b0243-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="b0243-147">Hallo client-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b0243-147">Run hello client app</span></span>
<span data-ttu-id="b0243-148">Met offlinesynchronisatie is nu ingeschakeld, kunt u de clienttoepassing Hallo ten minste eenmaal uitvoeren voor elk platform Hallo winkel lokale database gevuld.</span><span class="sxs-lookup"><span data-stu-id="b0243-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="b0243-149">Later een offline-scenario te simuleren en Hallo gegevens wijzigen in het lokale archief Hallo terwijl Hallo app offline is.</span><span class="sxs-lookup"><span data-stu-id="b0243-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="b0243-150">(Optioneel) Test Hallo sync-gedrag</span><span class="sxs-lookup"><span data-stu-id="b0243-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="b0243-151">In deze sectie kunt u Hallo client project toosimulate een offline-scenario wijzigen met behulp van een ongeldige toepassings-URL voor uw back-end.</span><span class="sxs-lookup"><span data-stu-id="b0243-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="b0243-152">Wanneer u toevoegen of wijzigen van gegevensitems, worden deze wijzigingen in het lokale archief worden bewaard, maar zijn niet gesynchroniseerde toohello back-end-gegevensarchief totdat het Hallo-verbinding is hersteld.</span><span class="sxs-lookup"><span data-stu-id="b0243-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="b0243-153">In Hallo Solution Explorer, open Hallo index.js projectbestand en Hallo toepassing URL toopoint wijzigen in een ongeldige URL, zoals Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0243-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="b0243-154">Werk in index.html, Hallo CSP `<meta>` element met dezelfde ongeldige URL Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0243-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="b0243-155">Bouw en Hallo client-app uitvoeren en u ziet dat er een uitzondering wordt geregistreerd in Hallo-console wanneer Hallo app probeert te synchroniseren met Hallo back-end na aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0243-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="b0243-156">Geen nieuwe objecten die u toevoegt bestaan alleen in het lokale archief Hallo totdat ze worden gepusht toohello mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="b0243-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="b0243-157">Hallo-clientapp gedraagt zich alsof het verbonden toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="b0243-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="b0243-158">Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.</span><span class="sxs-lookup"><span data-stu-id="b0243-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="b0243-159">(Optioneel) Gebruik Visual Studio tooview uw Azure SQL Database-tabel toosee die Hallo-gegevens in Hallo back-end-database niet is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b0243-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="b0243-160">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b0243-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="b0243-161">Navigeer tooyour database in **Azure**->**SQL-Databases**.</span><span class="sxs-lookup"><span data-stu-id="b0243-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="b0243-162">Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b0243-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="b0243-163">Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren.</span><span class="sxs-lookup"><span data-stu-id="b0243-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="b0243-164">(Optioneel) Test Hallo opnieuw verbinden tooyour mobiele back-end</span><span class="sxs-lookup"><span data-stu-id="b0243-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="b0243-165">In deze sectie maakt u opnieuw verbinding maakt Hallo toohello mobiele back-end app Hallo app terug afkomstig is van een online status te simuleren.</span><span class="sxs-lookup"><span data-stu-id="b0243-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="b0243-166">Wanneer u zich aanmeldt, is gegevens gesynchroniseerde tooyour mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="b0243-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="b0243-167">Open index.js en de URL van de toepassing hello herstellen.</span><span class="sxs-lookup"><span data-stu-id="b0243-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="b0243-168">Open index.html en corrigeer Hallo toepassings-URL in Hallo CSP `<meta>` element.</span><span class="sxs-lookup"><span data-stu-id="b0243-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="b0243-169">Opnieuw en Voer Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="b0243-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="b0243-170">Hallo app probeert toosync met Hallo mobiele app back-end na aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0243-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="b0243-171">Controleer of dat er geen uitzonderingen worden geregistreerd in Hallo-console voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="b0243-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="b0243-172">(Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b0243-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="b0243-173">Kennisgeving Hallo gegevens is tussen Hallo back-end-database en het lokale archief Hallo gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="b0243-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="b0243-174">U ziet Hallo gegevens tussen Hallo-database en het lokale archief Hallo is gesynchroniseerd en bevat Hallo items die u hebt toegevoegd terwijl de verbinding van uw app is verbroken.</span><span class="sxs-lookup"><span data-stu-id="b0243-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0243-175">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b0243-175">Additional resources</span></span>
* <span data-ttu-id="b0243-176">[Offline synchroniseren van gegevens in Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="b0243-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="b0243-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="b0243-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0243-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0243-178">Next steps</span></span>
* <span data-ttu-id="b0243-179">Bekijk meer geavanceerde functies zoals conflictoplossing in Hallo offlinesynchronisatie [offlinesynchronisatie voorbeeld]</span><span class="sxs-lookup"><span data-stu-id="b0243-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="b0243-180">Bekijk Hallo offlinesynchronisatie API-verwijzing in Hallo [API-documentatie](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="b0243-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

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
