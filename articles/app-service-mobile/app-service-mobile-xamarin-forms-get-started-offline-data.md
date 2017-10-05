---
title: Offlinesynchronisatie inschakelen voor uw mobiele Apps van Azure (Xamarin.Forms) | Microsoft Docs
description: Informatie over het gebruik van App Service-mobiele App aan cache en sync offline gegevens in uw toepassing Xamarin.Forms
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
ms.openlocfilehash: f2bed0a7124517319cc82405c4ab6b4d79aacfe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="9ecde-103">Offlinesynchronisatie inschakelen voor uw mobiele Xamarin.Forms-app</span><span class="sxs-lookup"><span data-stu-id="9ecde-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="9ecde-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9ecde-104">Overview</span></span>
<span data-ttu-id="9ecde-105">Deze zelfstudie maakt u kennis met de functie offline synchroniseren van Azure Mobile Apps voor Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="9ecde-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="9ecde-106">Offlinesynchronisatie kan eindgebruikers werken met een mobiele app--weergeven, toevoegen of wijzigen van gegevens--, zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="9ecde-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="9ecde-107">Wijzigingen worden opgeslagen in een lokale database.</span><span class="sxs-lookup"><span data-stu-id="9ecde-107">Changes are stored in a local database.</span></span> <span data-ttu-id="9ecde-108">Zodra het apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service.</span><span class="sxs-lookup"><span data-stu-id="9ecde-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="9ecde-109">Deze zelfstudie is gebaseerd op de Xamarin.Forms-Quick Start-oplossing voor Mobile Apps die u maakt wanneer u de zelfstudie [een Xamarin iOS-app maken] voltooit.</span><span class="sxs-lookup"><span data-stu-id="9ecde-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="9ecde-110">De Quick Start-oplossing voor Xamarin.Forms bevat de code ter ondersteuning van offlinesynchronisatie die moet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9ecde-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="9ecde-111">In deze zelfstudie maakt bijwerken u de Quick Start-oplossing de offline functies van Azure Mobile Apps inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="9ecde-112">We markeren de offline-specifieke code in de app ook.</span><span class="sxs-lookup"><span data-stu-id="9ecde-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="9ecde-113">Als u de gedownloade Quick Start-oplossing niet gebruikt, moet u de data access-extensiepakketten toevoegen aan uw project.</span><span class="sxs-lookup"><span data-stu-id="9ecde-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="9ecde-114">Zie voor meer informatie over server extensiepakketten [werken met de .NET-back-endserver SDK voor Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="9ecde-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="9ecde-115">Zie het onderwerp voor meer informatie over de functie offlinesynchronisatie [Offline synchroniseren van gegevens in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="9ecde-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="9ecde-116">Schakel offlinesynchronisatie-functionaliteit in de Quick Start-oplossing</span><span class="sxs-lookup"><span data-stu-id="9ecde-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="9ecde-117">De code offlinesynchronisatie is opgenomen in het project met behulp van C# preprocessor-instructies.</span><span class="sxs-lookup"><span data-stu-id="9ecde-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="9ecde-118">Wanneer de **OFFLINE\_SYNC\_ingeschakeld** symbool is gedefinieerd, wordt deze codepaden zijn opgenomen in de build.</span><span class="sxs-lookup"><span data-stu-id="9ecde-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="9ecde-119">Voor Windows-apps, moet u ook de SQLite-platform installeren.</span><span class="sxs-lookup"><span data-stu-id="9ecde-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="9ecde-120">Met de rechtermuisknop op de oplossing in Visual Studio > **NuGet-pakketten beheren voor oplossing...** , zoek vervolgens naar en installeren de **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket voor alle projecten in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="9ecde-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="9ecde-121">Open in Solution Explorer het TodoItemManager.cs-bestand uit het project met **draagbare** in de naam die Portable Class Library-project, klikt u vervolgens Opmerkingen bij de volgende preprocessor-instructie:</span><span class="sxs-lookup"><span data-stu-id="9ecde-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="9ecde-122">(Optioneel) Ter ondersteuning van Windows-apparaten, een van de volgende SQLite-runtime-pakketten te installeren:</span><span class="sxs-lookup"><span data-stu-id="9ecde-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="9ecde-123">**Windows 8.1 Runtime:** installeren [SQLite voor Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="9ecde-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="9ecde-124">**Windows Phone 8.1:** installeren [SQLite voor Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="9ecde-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="9ecde-125">**Universal Windows Platform** installeren [SQLite voor de Universal Windows universele][5].</span><span class="sxs-lookup"><span data-stu-id="9ecde-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>

     <span data-ttu-id="9ecde-126">Hoewel de Quick Start geen een universele Windows-project bevat, wordt het universele Windows-platform ondersteund met Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="9ecde-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="9ecde-127">(Optioneel) Elke Windows-app-project met de rechtermuisknop op **verwijzingen** > **verwijzing toevoegen...** , vouw de **Windows** map > **extensies**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="9ecde-128">Schakel de juiste **SQLite voor Windows** SDK samen met de **Visual C++ 2013-Runtime voor Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="9ecde-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="9ecde-129">De namen van SQLite SDK verschillen met elke Windows-platform.</span><span class="sxs-lookup"><span data-stu-id="9ecde-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="9ecde-130">Bekijk de clientcode voor synchronisatie</span><span class="sxs-lookup"><span data-stu-id="9ecde-130">Review the client sync code</span></span>
<span data-ttu-id="9ecde-131">Hier volgt een kort overzicht van wat is al opgenomen in de zelfstudie code binnen de `#if OFFLINE_SYNC_ENABLED` richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="9ecde-132">De offlinesynchronisatie-functionaliteit is in het projectbestand TodoItemManager.cs in het project Portable Class Library.</span><span class="sxs-lookup"><span data-stu-id="9ecde-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="9ecde-133">Zie voor een conceptueel overzicht van de functie [Offline synchroniseren van gegevens in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="9ecde-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="9ecde-134">Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="9ecde-135">De database van het lokale archief is geïnitialiseerd de **TodoItemManager** klassen-constructor met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="9ecde-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="9ecde-136">Deze code maakt een nieuwe lokale SQLite database met de **MobileServiceSQLiteStore** klasse.</span><span class="sxs-lookup"><span data-stu-id="9ecde-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="9ecde-137">De **DefineTable** methode maakt een tabel in het lokale archief die overeenkomt met de velden in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="9ecde-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="9ecde-138">Het type heeft geen om op te nemen van de kolommen die zich in de externe database.</span><span class="sxs-lookup"><span data-stu-id="9ecde-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="9ecde-139">Het is mogelijk voor het opslaan van een subset kolommen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="9ecde-140">De **todoTable** veld **TodoItemManager** is een **IMobileServiceSyncTable** typt u in plaats van **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="9ecde-141">Deze klasse maakt gebruik van de lokale database voor alle maken, lezen, bijwerken en verwijderen (CRUD) tabel-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="9ecde-142">U besluit wanneer deze wijzigingen worden gepusht back-end van de mobiele App door aan te roepen **PushAsync** op de **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="9ecde-143">De synchronisatie-context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden **PushAsync** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="9ecde-144">De volgende **SyncAsync** methode wordt aangeroepen om te synchroniseren met de back-end voor de mobiele App:</span><span class="sxs-lookup"><span data-stu-id="9ecde-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>

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
                        //Update failed, reverting to server's copy.
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

    <span data-ttu-id="9ecde-145">Dit voorbeeld maakt gebruik van eenvoudige foutafhandeling met de standaard synchronisatie-handler.</span><span class="sxs-lookup"><span data-stu-id="9ecde-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="9ecde-146">Het afhandelen van een echte toepassing zou de verschillende fouten zoals netwerkomstandigheden en server conflicten met behulp van een aangepaste **IMobileServiceSyncHandler** implementatie.</span><span class="sxs-lookup"><span data-stu-id="9ecde-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="9ecde-147">Offlinesynchronisatie overwegingen</span><span class="sxs-lookup"><span data-stu-id="9ecde-147">Offline sync considerations</span></span>
<span data-ttu-id="9ecde-148">In het voorbeeld de **SyncAsync** methode alleen wordt aangeroepen voor opstarten en waarop een synchronisatie wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="9ecde-149">Voor het initiëren van een synchronisatie in een Android- of iOS-app trek omlaag in de lijst met items; voor Windows, gebruikt de **Sync** knop.</span><span class="sxs-lookup"><span data-stu-id="9ecde-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="9ecde-150">In een echte toepassing kan u de trigger sync wanneer de status van het netwerk wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="9ecde-151">Wanneer een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates bijgehouden door de context die pull-bewerking automatisch triggers een voorgaande context push.</span><span class="sxs-lookup"><span data-stu-id="9ecde-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="9ecde-152">Bij het vernieuwen, toe te voegen en het voltooien van de items in dit voorbeeld kunt u weglaten de expliciete **PushAsync** aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="9ecde-153">In de opgegeven code alle records in de externe takentabel worden opgevraagd, maar het is ook mogelijk records filteren op het doorgeven van een query-id en opvragen voor **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="9ecde-154">Zie voor meer informatie de sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="9ecde-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="9ecde-155">De clientapp uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9ecde-155">Run the client app</span></span>
<span data-ttu-id="9ecde-156">Met offlinesynchronisatie is nu ingeschakeld, uitgevoerd bij de clienttoepassing ten minste eenmaal voor elk platform voor het vullen van de lokale database.</span><span class="sxs-lookup"><span data-stu-id="9ecde-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="9ecde-157">Later een offline-scenario te simuleren en de gegevens in het lokale archief niet wijzigen terwijl de app offline is.</span><span class="sxs-lookup"><span data-stu-id="9ecde-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="9ecde-158">Het gedrag van de synchronisatie van de client-app bijwerken</span><span class="sxs-lookup"><span data-stu-id="9ecde-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="9ecde-159">In deze sectie wijzigt het clientproject te simuleren van een offline-scenario met een ongeldige toepassings-URL voor uw back-end.</span><span class="sxs-lookup"><span data-stu-id="9ecde-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="9ecde-160">U kunt ook netwerkverbindingen uitschakelen door te verplaatsen van het apparaat naar 'Vliegtuigmodus'.</span><span class="sxs-lookup"><span data-stu-id="9ecde-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="9ecde-161">Wanneer u toevoegen of wijzigen van gegevensitems, zijn deze wijzigingen ondergebracht in het lokale archief, maar niet gesynchroniseerd met de back-end-gegevensopslag totdat de verbinding opnieuw tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="9ecde-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="9ecde-162">Open het projectbestand Constants.cs uit in de Solution Explorer de **draagbare** project en wijzig de waarde van `ApplicationURL` om te verwijzen naar een ongeldige URL:</span><span class="sxs-lookup"><span data-stu-id="9ecde-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="9ecde-163">Open het bestand TodoItemManager.cs uit de **draagbare** project en voeg een **catch** voor de base **uitzondering** klasse naar de **try... catch**blokkeren in **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="9ecde-164">Dit **catch** blok het uitzonderingsbericht schrijft naar de console als volgt:</span><span class="sxs-lookup"><span data-stu-id="9ecde-164">This **catch** block writes the exception message to the console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="9ecde-165">Ontwikkel en voer de client-app.</span><span class="sxs-lookup"><span data-stu-id="9ecde-165">Build and run the client app.</span></span>  <span data-ttu-id="9ecde-166">Aantal nieuwe items toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-166">Add some new items.</span></span> <span data-ttu-id="9ecde-167">U ziet dat er een uitzondering wordt geregistreerd in de console voor elke poging om te synchroniseren met de back-end.</span><span class="sxs-lookup"><span data-stu-id="9ecde-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="9ecde-168">Deze nieuwe items bestaan alleen in het lokale archief totdat ze naar de mobiele back-end kunnen worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="9ecde-169">De clientapp gedraagt zich als deze is verbonden met de back-end, ondersteunen die alle maken, lezen, update, delete (CRUD)-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9ecde-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="9ecde-170">De toepassing sluiten en opnieuw om te controleren dat de nieuwe items die u hebt gemaakt met het lokale archief worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="9ecde-171">(Optioneel) Met Visual Studio kunt u uw Azure SQL Database-tabel om te zien dat de gegevens in de back-end-database niet is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="9ecde-172">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="9ecde-173">Navigeer naar de database in **Azure**->**SQL-Databases**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="9ecde-174">Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9ecde-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="9ecde-175">Nu kunt u bladeren naar de tabel van uw SQL-database en de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="9ecde-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="9ecde-176">Update de client-app opnieuw verbinding maken met uw mobiele back-end</span><span class="sxs-lookup"><span data-stu-id="9ecde-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="9ecde-177">In deze sectie opnieuw verbinding worden de mobiele back-end die de app een online status terugkomst simuleert met de app.</span><span class="sxs-lookup"><span data-stu-id="9ecde-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="9ecde-178">Wanneer u de gebaar vernieuwen uitvoert, worden gegevens wordt gesynchroniseerd met uw mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="9ecde-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="9ecde-179">Open Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="9ecde-179">Reopen Constants.cs.</span></span> <span data-ttu-id="9ecde-180">Corrigeer de `applicationURL` om te verwijzen naar de juiste URL.</span><span class="sxs-lookup"><span data-stu-id="9ecde-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="9ecde-181">Bouwen en uitvoeren van de client-app.</span><span class="sxs-lookup"><span data-stu-id="9ecde-181">Rebuild and run the client app.</span></span> <span data-ttu-id="9ecde-182">De app probeert te synchroniseren met de back-end voor de mobiele app nadat u hebt.</span><span class="sxs-lookup"><span data-stu-id="9ecde-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="9ecde-183">Controleer of dat er geen uitzonderingen worden geregistreerd in de console voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="9ecde-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="9ecde-184">(Optioneel) De bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler weergeven of [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="9ecde-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="9ecde-185">U ziet dat de gegevens tussen de back-end-database en het lokale archief is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="9ecde-185">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="9ecde-186">U ziet de gegevens tussen de database en het lokale archief is gesynchroniseerd en bevat de items die u hebt toegevoegd terwijl de verbinding van uw app is verbroken.</span><span class="sxs-lookup"><span data-stu-id="9ecde-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ecde-187">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="9ecde-187">Additional Resources</span></span>
* <span data-ttu-id="9ecde-188">[Offline synchroniseren van gegevens in Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="9ecde-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="9ecde-189">[Azure Mobile Apps .NET SDK procedure][8]</span><span class="sxs-lookup"><span data-stu-id="9ecde-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
