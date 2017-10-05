---
title: Offlinesynchronisatie inschakelen voor uw mobiele Apps van Azure (Cordova) | Microsoft Docs
description: Informatie over het gebruik van App Service-mobiele App aan cache en sync offline gegevens in uw Cordova-toepassing
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
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="80416-103">Offlinesynchronisatie voor uw Cordova mobile app inschakelen</span><span class="sxs-lookup"><span data-stu-id="80416-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="80416-104">Deze zelfstudie maakt u kennis met de functie offline synchroniseren van Azure Mobile Apps voor Cordova.</span><span class="sxs-lookup"><span data-stu-id="80416-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="80416-105">Offlinesynchronisatie kunnen eindgebruikers werken met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="80416-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="80416-106">Wijzigingen worden opgeslagen in een lokale database.</span><span class="sxs-lookup"><span data-stu-id="80416-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="80416-107">Zodra het apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service.</span><span class="sxs-lookup"><span data-stu-id="80416-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="80416-108">Deze zelfstudie is gebaseerd op de Cordova-Quick Start-oplossing voor Mobile Apps die u maakt wanneer u de zelfstudie hebt voltooid [snel starten van Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="80416-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="80416-109">In deze zelfstudie maakt bijwerken u de Quick Start-oplossing voor het toevoegen van offline functies van Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="80416-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="80416-110">We markeren de offline-specifieke code in de app ook.</span><span class="sxs-lookup"><span data-stu-id="80416-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="80416-111">Zie het onderwerp voor meer informatie over de functie offlinesynchronisatie [Offline synchroniseren van gegevens in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="80416-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="80416-112">Zie voor meer informatie over het gebruik van de API van de [API-documentatie](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="80416-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="80416-113">Offlinesynchronisatie toevoegen aan de Quick Start-oplossing</span><span class="sxs-lookup"><span data-stu-id="80416-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="80416-114">De code offlinesynchronisatie moet worden toegevoegd aan de app.</span><span class="sxs-lookup"><span data-stu-id="80416-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="80416-115">Offline synchronisatie is vereist voor de invoegtoepassing cordova-sqlite-opslag, die automatisch wordt toegevoegd aan uw app wanneer de Azure Mobile Apps-invoegtoepassing is opgenomen in het project.</span><span class="sxs-lookup"><span data-stu-id="80416-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="80416-116">De Quick Start-project bevat zowel van deze invoegtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="80416-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="80416-117">Open index.js in Visual Studio Solution Explorer en vervang de volgende code</span><span class="sxs-lookup"><span data-stu-id="80416-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="80416-118">Met deze code:</span><span class="sxs-lookup"><span data-stu-id="80416-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="80416-119">Vervang vervolgens de volgende code:</span><span class="sxs-lookup"><span data-stu-id="80416-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="80416-120">Met deze code:</span><span class="sxs-lookup"><span data-stu-id="80416-120">with this code:</span></span>

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

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="80416-121">De voorgaande code toevoegingen initialiseren van het lokale archief en definiëren van een lokale tabel die overeenkomt met de kolomwaarden gebruikt in uw Azure back-end.</span><span class="sxs-lookup"><span data-stu-id="80416-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="80416-122">(U hoeft niet alle kolomwaarden wilt opnemen in deze code.)  De `version` veld wordt beheerd door de mobiele back-end en wordt gebruikt voor het oplossen van conflicten.</span><span class="sxs-lookup"><span data-stu-id="80416-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="80416-123">Ontvangt u een verwijzing naar de synchronisatie-context door aan te roepen **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="80416-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="80416-124">De synchronisatie-context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden `.push()` wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="80416-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="80416-125">De URL van de toepassing worden bijgewerkt naar de URL van uw mobiele App-toepassing.</span><span class="sxs-lookup"><span data-stu-id="80416-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="80416-126">Vervang vervolgens deze code:</span><span class="sxs-lookup"><span data-stu-id="80416-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="80416-127">Met deze code:</span><span class="sxs-lookup"><span data-stu-id="80416-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="80416-128">De bovenstaande code initialiseert de synchronisatie-context en roept vervolgens getSyncTable (in plaats van een getTable) als u verwijst naar de lokale tabel.</span><span class="sxs-lookup"><span data-stu-id="80416-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="80416-129">Deze code maakt gebruik van de lokale database voor alle maken, lezen, bijwerken en verwijderen (CRUD) tabel-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="80416-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="80416-130">Dit voorbeeld voert eenvoudige foutafhandeling op synchronisatieconflicten.</span><span class="sxs-lookup"><span data-stu-id="80416-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="80416-131">Een echte toepassing zou de verschillende fouten zoals netwerkomstandigheden, server conflicten en anderen verwerken.</span><span class="sxs-lookup"><span data-stu-id="80416-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="80416-132">Zie voor codevoorbeelden van de [offlinesynchronisatie voorbeeld].</span><span class="sxs-lookup"><span data-stu-id="80416-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="80416-133">Vervolgens voegt u deze functie om uit te voeren van de werkelijke synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="80416-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="80416-134">U bepalen wanneer wijzigingen naar de back-end voor de mobiele App forceren door aan te roepen **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="80416-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="80416-135">U kunt bijvoorbeeld aanroepen **syncBackend** in een knop gebeurtenis-handler gekoppeld aan een knop synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="80416-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="80416-136">Offlinesynchronisatie overwegingen</span><span class="sxs-lookup"><span data-stu-id="80416-136">Offline sync considerations</span></span>

<span data-ttu-id="80416-137">In het voorbeeld de **push** methode van **syncContext** alleen wordt aangeroepen voor het starten van de app in de callback-functie voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="80416-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="80416-138">In een echte toepassing kan u de functionaliteit van deze synchronisatie handmatig geactiveerd of wanneer de netwerk-status is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="80416-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="80416-139">Wanneer een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates bijgehouden door de context die pull-bewerking automatisch triggers een push.</span><span class="sxs-lookup"><span data-stu-id="80416-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="80416-140">Bij het vernieuwen, toe te voegen en het voltooien van de items in dit voorbeeld kunt u weglaten de expliciete **push** aanroepen, omdat deze is mogelijk overbodig.</span><span class="sxs-lookup"><span data-stu-id="80416-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="80416-141">In de opgegeven code alle records in de externe takentabel worden opgevraagd, maar het is ook mogelijk records filteren op het doorgeven van een query-id en opvragen voor **push**.</span><span class="sxs-lookup"><span data-stu-id="80416-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="80416-142">Zie voor meer informatie de sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="80416-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="80416-143">(Optioneel) Verificatie uit te schakelen</span><span class="sxs-lookup"><span data-stu-id="80416-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="80416-144">Als u niet wilt testen offlinesynchronisatie na verificatie instellen, uitcommentariëren de callback-functie voor aanmelding, maar laat u de code in de functie voor retouraanroepen zonder opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="80416-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="80416-145">Na de aanmelding regels commentaarteken, volgt de code:</span><span class="sxs-lookup"><span data-stu-id="80416-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="80416-146">Nu de app wordt gesynchroniseerd met de Azure back-end wanneer u de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="80416-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="80416-147">De clientapp uitvoeren</span><span class="sxs-lookup"><span data-stu-id="80416-147">Run the client app</span></span>
<span data-ttu-id="80416-148">Met offlinesynchronisatie is nu ingeschakeld, kunt u de clienttoepassing ten minste eenmaal uitvoeren voor elk platform voor het vullen van de lokale database.</span><span class="sxs-lookup"><span data-stu-id="80416-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="80416-149">Later een offline-scenario te simuleren en de gegevens in het lokale archief niet wijzigen terwijl de app offline is.</span><span class="sxs-lookup"><span data-stu-id="80416-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="80416-150">(Optioneel) Het gedrag van de synchronisatie te testen</span><span class="sxs-lookup"><span data-stu-id="80416-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="80416-151">In deze sectie kunt u het clientproject om te simuleren van een offline-scenario met een ongeldige toepassings-URL voor uw back-end wijzigen.</span><span class="sxs-lookup"><span data-stu-id="80416-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="80416-152">Wanneer u toevoegen of wijzigen van gegevensitems, worden deze wijzigingen in het lokale archief worden bewaard, maar niet is gesynchroniseerd met de back-end-gegevensopslag totdat de verbinding opnieuw tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="80416-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="80416-153">Open het projectbestand index.js in Solution Explorer en wijzig de URL van de toepassing om te verwijzen naar een ongeldige URL, zoals de volgende code:</span><span class="sxs-lookup"><span data-stu-id="80416-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="80416-154">Werk de CSP in index.html, `<meta>` element met dezelfde URL ongeldig.</span><span class="sxs-lookup"><span data-stu-id="80416-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="80416-155">Bouwen en uitvoeren van de client-app en u ziet dat er een uitzondering wordt geregistreerd in de console wanneer de app probeert te synchroniseren met de back-end na aanmelding.</span><span class="sxs-lookup"><span data-stu-id="80416-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="80416-156">Geen nieuwe objecten die u toevoegt bestaan alleen in het lokale archief totdat ze naar de mobiele back-end worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="80416-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="80416-157">De clientapp gedraagt zich als deze is verbonden met de back-end.</span><span class="sxs-lookup"><span data-stu-id="80416-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="80416-158">De toepassing sluiten en opnieuw om te controleren dat de nieuwe items die u hebt gemaakt met het lokale archief worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="80416-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="80416-159">(Optioneel) Met Visual Studio kunt u uw Azure SQL Database-tabel om te zien dat de gegevens in de back-end-database niet is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="80416-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="80416-160">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="80416-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="80416-161">Navigeer naar de database in **Azure**->**SQL-Databases**.</span><span class="sxs-lookup"><span data-stu-id="80416-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="80416-162">Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="80416-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="80416-163">Nu kunt u bladeren naar de tabel van uw SQL-database en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="80416-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="80416-164">(Optioneel) Het opnieuw verbinden met uw mobiele back-end testen</span><span class="sxs-lookup"><span data-stu-id="80416-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="80416-165">In deze sectie kunt u de app naar de mobiele back-end die de app een online status terugkomst simuleert herstellen.</span><span class="sxs-lookup"><span data-stu-id="80416-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="80416-166">Wanneer u zich aanmeldt, worden gegevens wordt gesynchroniseerd met uw mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="80416-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="80416-167">Open index.js en herstellen van de URL van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="80416-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="80416-168">Open index.html en corrigeer de URL van de toepassing in de CSP `<meta>` element.</span><span class="sxs-lookup"><span data-stu-id="80416-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="80416-169">Bouwen en uitvoeren van de client-app.</span><span class="sxs-lookup"><span data-stu-id="80416-169">Rebuild and run the client app.</span></span> <span data-ttu-id="80416-170">De app probeert te synchroniseren met de back-end voor de mobiele app na aanmelding.</span><span class="sxs-lookup"><span data-stu-id="80416-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="80416-171">Controleer of dat er geen uitzonderingen worden geregistreerd in de console voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="80416-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="80416-172">(Optioneel) De bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler weergeven.</span><span class="sxs-lookup"><span data-stu-id="80416-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="80416-173">U ziet dat de gegevens tussen de back-end-database en het lokale archief is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="80416-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="80416-174">U ziet de gegevens tussen de database en het lokale archief is gesynchroniseerd en bevat de items die u hebt toegevoegd terwijl de verbinding van uw app is verbroken.</span><span class="sxs-lookup"><span data-stu-id="80416-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80416-175">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="80416-175">Additional resources</span></span>
* <span data-ttu-id="80416-176">[Offline synchroniseren van gegevens in Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="80416-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="80416-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="80416-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="80416-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80416-178">Next steps</span></span>
* <span data-ttu-id="80416-179">Bekijk meer geavanceerde functies zoals conflictoplossing in offlinesynchronisatie de [offlinesynchronisatie voorbeeld]</span><span class="sxs-lookup"><span data-stu-id="80416-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="80416-180">Bekijk de offlinesynchronisatie API-verwijzing in de [API-documentatie](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="80416-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="80416-181">[snel starten van Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="80416-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="80416-182">[offlinesynchronisatie voorbeeld]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="80416-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="80416-183">[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="80416-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="80416-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="80416-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
