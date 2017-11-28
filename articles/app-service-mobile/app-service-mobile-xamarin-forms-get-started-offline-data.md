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
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="53cf2-103">Offlinesynchronisatie inschakelen voor uw mobiele Xamarin.Forms-app</span><span class="sxs-lookup"><span data-stu-id="53cf2-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="53cf2-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="53cf2-104">Overview</span></span>
<span data-ttu-id="53cf2-105">Deze zelfstudie introduceert Hallo offlinesynchronisatie functie van Azure Mobile Apps voor Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="53cf2-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="53cf2-106">Offlinesynchronisatie kan eindgebruikers werken met een mobiele app--weergeven, toevoegen of wijzigen van gegevens--, zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="53cf2-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="53cf2-107">Wijzigingen worden opgeslagen in een lokale database.</span><span class="sxs-lookup"><span data-stu-id="53cf2-107">Changes are stored in a local database.</span></span> <span data-ttu-id="53cf2-108">Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met de externe service Hallo.</span><span class="sxs-lookup"><span data-stu-id="53cf2-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="53cf2-109">Deze zelfstudie is gebaseerd op Hallo Xamarin.Forms Quick Start-oplossing voor Mobile Apps die u maakt wanneer u de zelfstudie [een Xamarin iOS-app maken] voltooit.</span><span class="sxs-lookup"><span data-stu-id="53cf2-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="53cf2-110">Hallo Quick Start-oplossing voor Xamarin.Forms bevat Hallo code toosupport offlinesynchronisatie, die alleen toobe ingeschakeld moet.</span><span class="sxs-lookup"><span data-stu-id="53cf2-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="53cf2-111">In deze zelfstudie maakt bijwerken u Hallo Quick Start-oplossing tooturn op Hallo offline functies van Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="53cf2-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="53cf2-112">We ook markeren Hallo offline-specifieke code in Hallo app.</span><span class="sxs-lookup"><span data-stu-id="53cf2-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="53cf2-113">Als u geen Hallo gedownloade Quick Start-oplossing gebruikt, moet u Hallo data access-extensie pakketten tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="53cf2-114">Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="53cf2-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="53cf2-115">toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="53cf2-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="53cf2-116">Schakel offlinesynchronisatie-functionaliteit in Hallo Quick Start-oplossing</span><span class="sxs-lookup"><span data-stu-id="53cf2-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="53cf2-117">Hallo offlinesynchronisatie code is opgenomen in het Hallo-project met behulp van C# preprocessor-instructies.</span><span class="sxs-lookup"><span data-stu-id="53cf2-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="53cf2-118">Wanneer Hallo **OFFLINE\_SYNC\_ingeschakeld** symbool is gedefinieerd, wordt deze codepaden zijn opgenomen in Hallo build.</span><span class="sxs-lookup"><span data-stu-id="53cf2-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="53cf2-119">Voor Windows-apps, moet u ook Hallo SQLite-platform installeren.</span><span class="sxs-lookup"><span data-stu-id="53cf2-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="53cf2-120">In Visual Studio met de rechtermuisknop op Hallo oplossing > **NuGet-pakketten beheren voor oplossing...** , zoek vervolgens naar en installeren de **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet-pakket voor alle projecten in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="53cf2-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="53cf2-121">Open in Solution Explorer Hallo, Hallo TodoItemManager.cs bestand uit Hallo-project met **draagbare** in naam van Hallo Portable Class Library-project is, verwijder vervolgens de opmerkingen Hallo preprocessor-instructie te volgen:</span><span class="sxs-lookup"><span data-stu-id="53cf2-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="53cf2-122">Windows-apparaten (optioneel) toosupport, installeert u een Hallo SQLite runtime pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="53cf2-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="53cf2-123">**Windows 8.1 Runtime:** installeren [SQLite voor Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="53cf2-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="53cf2-124">**Windows Phone 8.1:** installeren [SQLite voor Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="53cf2-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="53cf2-125">**Universele Windows-Platform** installeren [SQLite voor universele Windows universele Hallo][5].</span><span class="sxs-lookup"><span data-stu-id="53cf2-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="53cf2-126">Hoewel Hallo Quick Start geen een universele Windows-project bevat, wordt met Xamarin Forms Hallo Universal Windows platform ondersteund.</span><span class="sxs-lookup"><span data-stu-id="53cf2-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="53cf2-127">(Optioneel) Elke Windows-app-project met de rechtermuisknop op **verwijzingen** > **verwijzing toevoegen...** , vouw Hallo **Windows** map > **extensies**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="53cf2-128">Inschakelen van de juiste Hallo **SQLite voor Windows** SDK samen met de Hallo **Visual C++ 2013-Runtime voor Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="53cf2-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="53cf2-129">Hallo verschillen SQLite SDK namen met elke Windows-platform.</span><span class="sxs-lookup"><span data-stu-id="53cf2-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="53cf2-130">Hallo-clientcode sync controleren</span><span class="sxs-lookup"><span data-stu-id="53cf2-130">Review hello client sync code</span></span>
<span data-ttu-id="53cf2-131">Hier volgt een kort overzicht van wat al in de zelfstudie code binnen Hallo Hallo opgenomen is `#if OFFLINE_SYNC_ENABLED` richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="53cf2-132">De offlinesynchronisatie-functionaliteit is in Hallo TodoItemManager.cs projectbestand in Hallo Portable Class Library-project.</span><span class="sxs-lookup"><span data-stu-id="53cf2-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="53cf2-133">Zie voor een conceptueel overzicht van de functie Hallo [Offline synchroniseren van gegevens in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="53cf2-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="53cf2-134">Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="53cf2-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="53cf2-135">Hallo lokale winkeldatabase is geïnitialiseerd in Hallo **TodoItemManager** klassen-constructor met behulp van de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="53cf2-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="53cf2-136">Deze code maakt een nieuwe lokale SQLite-database met behulp van Hallo **MobileServiceSQLiteStore** klasse.</span><span class="sxs-lookup"><span data-stu-id="53cf2-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="53cf2-137">Hallo **DefineTable** methode maakt een tabel in Hallo lokale archief die overeenkomt met de Hallo velden in Hallo opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="53cf2-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="53cf2-138">Hallo-type heeft geen tooinclude alle Hallo kolommen die zich in de externe database Hallo.</span><span class="sxs-lookup"><span data-stu-id="53cf2-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="53cf2-139">Het is mogelijk toostore een subset kolommen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="53cf2-140">Hallo **todoTable** veld **TodoItemManager** is een **IMobileServiceSyncTable** typt u in plaats van **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="53cf2-141">Deze klasse gebruikt Hallo lokale database voor alle maken, lezen, bijwerken en verwijderen (CRUD) tabel-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="53cf2-142">U besluit wanneer deze wijzigingen backend voor mobiele Apps toohello gepusht door aan te roepen **PushAsync** op Hallo **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="53cf2-143">Hallo sync context helpt tabelrelaties behouden door wijzigingen in alle tabellen die een client-app is gewijzigd wanneer worden gepusht en bij te houden **PushAsync** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="53cf2-144">Hallo volgende **SyncAsync** methode wordt aangeroepen toosync met Hallo mobiele App back-end:</span><span class="sxs-lookup"><span data-stu-id="53cf2-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

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

    <span data-ttu-id="53cf2-145">Dit voorbeeld maakt gebruik van eenvoudige foutafhandeling Hallo standaard synchronisatie handler.</span><span class="sxs-lookup"><span data-stu-id="53cf2-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="53cf2-146">Een echte toepassing hello diverse fouten zoals netwerkomstandigheden en server veroorzaakt een conflict met behulp van een aangepaste zou verwerken **IMobileServiceSyncHandler** implementatie.</span><span class="sxs-lookup"><span data-stu-id="53cf2-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="53cf2-147">Offlinesynchronisatie overwegingen</span><span class="sxs-lookup"><span data-stu-id="53cf2-147">Offline sync considerations</span></span>
<span data-ttu-id="53cf2-148">In voorbeeld Hallo Hallo **SyncAsync** methode alleen wordt aangeroepen voor opstarten en waarop een synchronisatie wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="53cf2-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="53cf2-149">tooinitiate een synchronisatie in een Android- of iOS-app, pull omlaag in de lijst items Hallo; Gebruik voor Windows hello **Sync** knop.</span><span class="sxs-lookup"><span data-stu-id="53cf2-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="53cf2-150">In een echte toepassing kan u Hallo synchronisatie activeren wanneer Hallo netwerk status verandert.</span><span class="sxs-lookup"><span data-stu-id="53cf2-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="53cf2-151">Wanneer een pull wordt uitgevoerd op basis van een tabel met wachtende lokale updates bijgehouden door Hallo-context, die pull-bewerking automatisch triggers een voorgaande context push.</span><span class="sxs-lookup"><span data-stu-id="53cf2-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="53cf2-152">Bij het vernieuwen, toe te voegen en het voltooien van de items in dit voorbeeld, kunt u weglaten Hallo expliciete **PushAsync** aanroepen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="53cf2-153">In de opgegeven Hallo code, alle records in de externe takentabel Hallo worden opgevraagd, maar het is ook mogelijk toofilter records door een query-id en de query te**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="53cf2-154">Zie voor meer informatie, Hallo sectie *incrementele synchronisatie* in [Offline synchroniseren van gegevens in Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="53cf2-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="53cf2-155">Hallo client-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="53cf2-155">Run hello client app</span></span>
<span data-ttu-id="53cf2-156">Ten minste eenmaal uitgevoerd Hallo-clienttoepassing op elk platform toopopulate Hallo winkel lokale database met het offline synchroniseren van nu is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="53cf2-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="53cf2-157">Later een offline-scenario te simuleren en Hallo gegevens wijzigen in het lokale archief Hallo terwijl Hallo app offline is.</span><span class="sxs-lookup"><span data-stu-id="53cf2-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="53cf2-158">Hallo sync-gedrag Hallo client-app bijwerken</span><span class="sxs-lookup"><span data-stu-id="53cf2-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="53cf2-159">In deze sectie Hallo client project toosimulate een offline-scenario te wijzigen met behulp van een ongeldige toepassings-URL voor uw back-end.</span><span class="sxs-lookup"><span data-stu-id="53cf2-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="53cf2-160">U kunt ook netwerkverbindingen uitschakelen door het apparaat te verplaatsen 'Vliegtuigmodus'.</span><span class="sxs-lookup"><span data-stu-id="53cf2-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="53cf2-161">Wanneer u toevoegen of wijzigen van gegevensitems, deze wijzigingen zijn ondergebracht in het lokale archief hello, maar niet gesynchroniseerd toohello back-endgegevens opslaan totdat het Hallo-verbinding is hersteld.</span><span class="sxs-lookup"><span data-stu-id="53cf2-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="53cf2-162">Open in Solution Explorer Hallo, Hallo Constants.cs projectbestand van Hallo **draagbare** project en wijzig de waarde Hallo van `ApplicationURL` toopoint tooan ongeldige URL:</span><span class="sxs-lookup"><span data-stu-id="53cf2-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="53cf2-163">Open Hallo TodoItemManager.cs bestand van Hallo **draagbare** project en voeg een **catch** voor Hallo base **uitzondering** klasse toohello **try... catch** blokkeren in **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="53cf2-164">Dit **catch** blok schrijft Hallo uitzondering bericht toohello-console als volgt:</span><span class="sxs-lookup"><span data-stu-id="53cf2-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="53cf2-165">Ontwikkel en Voer Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="53cf2-165">Build and run hello client app.</span></span>  <span data-ttu-id="53cf2-166">Aantal nieuwe items toevoegen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-166">Add some new items.</span></span> <span data-ttu-id="53cf2-167">U ziet dat er een uitzondering wordt geregistreerd in de console Hallo voor elke poging toosync met Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="53cf2-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="53cf2-168">Deze nieuwe items bestaan alleen in het lokale archief Hallo totdat ze toohello mobiele back-end kunnen worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="53cf2-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="53cf2-169">Hallo-clientapp gedraagt zich alsof het verbonden toohello backend, ondersteunen die alle maken, lezen, update, delete (CRUD)-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="53cf2-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="53cf2-170">Hallo-app sluiten en opnieuw tooverify dat Hallo nieuwe items die u hebt gemaakt het lokale archief persistente toohello zijn.</span><span class="sxs-lookup"><span data-stu-id="53cf2-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="53cf2-171">(Optioneel) Gebruik Visual Studio tooview uw Azure SQL Database-tabel toosee die Hallo-gegevens in Hallo back-end-database niet is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="53cf2-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="53cf2-172">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="53cf2-173">Navigeer tooyour database in **Azure**->**SQL-Databases**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="53cf2-174">Met de rechtermuisknop op de database en selecteer **openen in SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="53cf2-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="53cf2-175">Nu kunt u de SQL-databasetabel tooyour en de bijbehorende inhoud bladeren.</span><span class="sxs-lookup"><span data-stu-id="53cf2-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="53cf2-176">Uw mobiele back-end voor Hallo client app tooreconnect bijwerken</span><span class="sxs-lookup"><span data-stu-id="53cf2-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="53cf2-177">In deze sectie opnieuw verbinding Hallo toohello mobiele back-end app Hallo app terugkomen tooan online status te simuleren.</span><span class="sxs-lookup"><span data-stu-id="53cf2-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="53cf2-178">Wanneer u Hallo vernieuwen gebaar uitvoert, is gegevens gesynchroniseerde tooyour mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="53cf2-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="53cf2-179">Open Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="53cf2-179">Reopen Constants.cs.</span></span> <span data-ttu-id="53cf2-180">Juiste Hallo `applicationURL` toopoint toohello Corrigeer de URL.</span><span class="sxs-lookup"><span data-stu-id="53cf2-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="53cf2-181">Opnieuw en Voer Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="53cf2-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="53cf2-182">Hallo app probeert toosync met Hallo mobiele app back-end nadat u hebt.</span><span class="sxs-lookup"><span data-stu-id="53cf2-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="53cf2-183">Controleer of dat er geen uitzonderingen worden geregistreerd in Hallo-console voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="53cf2-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="53cf2-184">(Optioneel) Weergave Hallo bijgewerkte gegevens met behulp van SQL Server Object Explorer of een REST-hulpprogramma zoals Fiddler of [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="53cf2-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="53cf2-185">Kennisgeving Hallo gegevens is tussen Hallo back-end-database en het lokale archief Hallo gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="53cf2-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="53cf2-186">U ziet Hallo gegevens tussen Hallo-database en het lokale archief Hallo is gesynchroniseerd en bevat Hallo items die u hebt toegevoegd terwijl de verbinding van uw app is verbroken.</span><span class="sxs-lookup"><span data-stu-id="53cf2-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53cf2-187">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="53cf2-187">Additional Resources</span></span>
* <span data-ttu-id="53cf2-188">[Offline synchroniseren van gegevens in Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="53cf2-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="53cf2-189">[Azure Mobile Apps .NET SDK procedure][8]</span><span class="sxs-lookup"><span data-stu-id="53cf2-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
