---
title: offline synchronisatie van aaaEnable met mobiele iOS-apps | Microsoft Docs
description: Meer informatie over hoe toouse Azure App Service mobile apps toocache en sync offline gegevens in iOS-toepassingen.
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="d6898-103">Offline synchronisatie met de mobiele iOS-apps inschakelen</span><span class="sxs-lookup"><span data-stu-id="d6898-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="d6898-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d6898-104">Overview</span></span>
<span data-ttu-id="d6898-105">Deze zelfstudie wordt behandeld offline synchronisatie met de functie van Azure App Service Mobile Apps voor iOS Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6898-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="d6898-106">Met offline synchroniseert eindgebruikers kunnen communiceren met een mobiele app tooview, toevoegen of wijzigen van gegevens, zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="d6898-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="d6898-107">Wijzigingen worden opgeslagen in een lokale database.</span><span class="sxs-lookup"><span data-stu-id="d6898-107">Changes are stored in a local database.</span></span> <span data-ttu-id="d6898-108">Nadat het Hallo-apparaat weer online is, worden Hallo wijzigingen gesynchroniseerd met de Hallo externe back-end.</span><span class="sxs-lookup"><span data-stu-id="d6898-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="d6898-109">Als dit uw eerste ervaring met Mobile Apps is, moet u eerst Hallo zelfstudie uitvoeren [maken van een iOS-App].</span><span class="sxs-lookup"><span data-stu-id="d6898-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="d6898-110">Als u snel starten-serverproject Hallo gedownload niet gebruikt, moet u Hallo gegevenstoegang pakketten tooyour extensieproject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d6898-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="d6898-111">Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d6898-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="d6898-112">toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie [Offline synchroniseren van gegevens in mobiele Apps].</span><span class="sxs-lookup"><span data-stu-id="d6898-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="d6898-113"><a name="review-sync"></a>Hallo-clientcode sync controleren</span><span class="sxs-lookup"><span data-stu-id="d6898-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="d6898-114">Hallo client-project dat u hebt gedownload voor Hallo [maken van een iOS-App] zelfstudie bevat al de code die ondersteuning biedt voor offlinesynchronisatie met behulp van een lokale database op basis van gegevens van de Core.</span><span class="sxs-lookup"><span data-stu-id="d6898-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="d6898-115">Deze sectie bevat een overzicht van wat is al opgenomen in de zelfstudie Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="d6898-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="d6898-116">Zie voor een conceptueel overzicht van de functie Hallo [Offline synchroniseren van gegevens in mobiele Apps].</span><span class="sxs-lookup"><span data-stu-id="d6898-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="d6898-117">Met de functie voor het offline synchroniseren van gegevens van Hallo van Mobile Apps, kunnen eindgebruikers communiceren met een lokale database zelfs wanneer het Hallo-netwerk is niet toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="d6898-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="d6898-118">toouse wanneer u Hallo sync context van deze functies in uw app initialiseren `MSClient` en verwijzen naar een lokaal archief.</span><span class="sxs-lookup"><span data-stu-id="d6898-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="d6898-119">Vervolgens u verwijzen naar de tabel via Hallo **MSSyncTable** interface.</span><span class="sxs-lookup"><span data-stu-id="d6898-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="d6898-120">In **QSTodoService.m** (Objective-C) of **ToDoTableViewController.swift** (Swift), u ziet dat het type van lid Hallo Hallo **syncTable** is  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="d6898-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="d6898-121">Offline synchronisatie maakt gebruik van deze synchronisatie tabel interface in plaats van **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="d6898-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="d6898-122">Wanneer een synchronisatietabel wordt gebruikt, alle bewerkingen gaat u het lokale archief toohello en zijn gesynchroniseerd met de Hallo externe back-end met expliciete push en pull-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d6898-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="d6898-123">tooget een tooa sync verwijzingstabel, gebruik Hallo **syncTableWithName** methode op `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="d6898-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="d6898-124">functie voor het offline synchroniseren van tooremove, gebruik **tableWithName** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d6898-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="d6898-125">Voordat u tabelbewerkingen kunnen uitvoeren, moet het lokale archief Hallo worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="d6898-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="d6898-126">Dit is de relevante code Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6898-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="d6898-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="d6898-127">**Objective-C**.</span></span> <span data-ttu-id="d6898-128">In Hallo **QSTodoService.init** methode:</span><span class="sxs-lookup"><span data-stu-id="d6898-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="d6898-129">**SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="d6898-129">**Swift**.</span></span> <span data-ttu-id="d6898-130">In Hallo **ToDoTableViewController.viewDidLoad** methode:</span><span class="sxs-lookup"><span data-stu-id="d6898-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="d6898-131">Deze methode maakt u een lokaal archief met behulp van Hallo `MSCoreDataStore` interface, waardoor Hallo Mobile Apps SDK biedt.</span><span class="sxs-lookup"><span data-stu-id="d6898-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="d6898-132">U kunt ook een ander lokaal archief opgeven door het implementeren van Hallo `MSSyncContextDataSource` protocol.</span><span class="sxs-lookup"><span data-stu-id="d6898-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="d6898-133">Bovendien Hallo eerste parameter van **MSSyncContext** gebruikte toospecify is een conflict-handler.</span><span class="sxs-lookup"><span data-stu-id="d6898-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="d6898-134">Omdat we hebt doorgegeven `nil`, krijgen we Hallo standaard conflict handler, die niet bij een conflict.</span><span class="sxs-lookup"><span data-stu-id="d6898-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="d6898-135">Nu gaan we de werkelijke synchronisatiebewerking Hallo uitvoeren en gegevens ophalen uit externe back-end van Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6898-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="d6898-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="d6898-136">**Objective-C**.</span></span> <span data-ttu-id="d6898-137">`syncData`eerst pushes nieuwe wijzigingen en roept vervolgens **pullData** tooget gegevens van Hallo externe back-end.</span><span class="sxs-lookup"><span data-stu-id="d6898-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="d6898-138">Op zijn beurt Hallo **pullData** methode haalt nieuwe gegevens die overeenkomt met een query:</span><span class="sxs-lookup"><span data-stu-id="d6898-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="d6898-139">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="d6898-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="d6898-140">Hallo Objective-C-versie in `syncData`, noemen we eerst **pushWithCompletion** op Hallo sync context.</span><span class="sxs-lookup"><span data-stu-id="d6898-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="d6898-141">Deze methode maakt deel uit van `MSSyncContext` (en niet Hallo synchronisatietabel zelf) omdat deze wijzigingen pushes in alle tabellen.</span><span class="sxs-lookup"><span data-stu-id="d6898-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="d6898-142">Alleen de records die zijn gewijzigd op een bepaalde manier lokaal (via CUD bewerkingen) worden toohello server verzonden.</span><span class="sxs-lookup"><span data-stu-id="d6898-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="d6898-143">Vervolgens Hallo helper **pullData** wordt genoemd, welke aanroepen **MSSyncTable.pullWithQuery** tooretrieve externe gegevens en op te slaan in de lokale database Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6898-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="d6898-144">Hallo Swift versie, omdat het Hallo-push-bewerking is niet strikt noodzakelijk is, er is geen aanroep te**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="d6898-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="d6898-145">Als er wijzigingen in behandeling in Hallo sync context voor Hallo-tabel die een push-bewerking doet zijn, pull-altijd problemen met een push eerst.</span><span class="sxs-lookup"><span data-stu-id="d6898-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="d6898-146">Als er meer dan één synchronisatietabel, is het beste tooexplicitly aanroep push tooensure dat alles consistent is voor alle gerelateerde tabellen.</span><span class="sxs-lookup"><span data-stu-id="d6898-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="d6898-147">In Hallo Objective-C en Swift versies, kunt u Hallo **pullWithQuery** methode toospecify een query toofilter Hallo gewenste tooretrieve records.</span><span class="sxs-lookup"><span data-stu-id="d6898-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="d6898-148">In dit voorbeeld Hallo query haalt u alle records in externe Hallo `TodoItem` tabel.</span><span class="sxs-lookup"><span data-stu-id="d6898-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="d6898-149">tweede parameter van Hallo **pullWithQuery** een query-id die wordt gebruikt voor *incrementele synchronisatie*. Incrementele synchronisatie alleen records die zijn gewijzigd sinds de laatste synchronisatie hello, met behulp van de record Hallo haalt `UpdatedAt` tijdstempel (aangeroepen `updatedAt` in Hallo lokale opslag.) Hallo query-ID moet een beschrijvende tekenreeks die uniek is voor elke logische query uw app.</span><span class="sxs-lookup"><span data-stu-id="d6898-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="d6898-150">tooopt incrementele synchroon doorgeven `nil` zoals Hallo query-ID.</span><span class="sxs-lookup"><span data-stu-id="d6898-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="d6898-151">Deze methode kan worden mogelijk inefficiënt, omdat het ophalen van alle records op elk pull-bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6898-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="d6898-152">Hallo Objective-C-app wordt gesynchroniseerd wanneer u wijzigen of toevoegen van gegevens, wanneer een gebruiker Hallo vernieuwen gebaar uitvoert, en op starten.</span><span class="sxs-lookup"><span data-stu-id="d6898-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="d6898-153">Hallo Swift app wordt gesynchroniseerd wanneer Hallo gebruiker Hallo vernieuwen gebaar uitvoert en op starten.</span><span class="sxs-lookup"><span data-stu-id="d6898-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="d6898-154">Omdat hello app wordt gesynchroniseerd wanneer de gegevens zijn gewijzigd (Objective-C) of wanneer het Hallo-app gestart (Objective-C en Swift), Hallo-app wordt ervan uitgegaan dat die gebruiker Hallo online.</span><span class="sxs-lookup"><span data-stu-id="d6898-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="d6898-155">In een volgende sectie wordt u Hallo app bijwerken zodat gebruikers bewerken kunnen, zelfs als ze offline zijn.</span><span class="sxs-lookup"><span data-stu-id="d6898-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="d6898-156"><a name="review-core-data"></a>Bekijk Hallo Core-gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="d6898-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="d6898-157">Wanneer u Hallo Core offline gegevensarchief gebruikt, moet u bepaalde tabellen en velden definiëren in het gegevensmodel.</span><span class="sxs-lookup"><span data-stu-id="d6898-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="d6898-158">Hallo voorbeeld-app bevat al een gegevensmodel met de juiste notatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6898-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="d6898-159">In deze sectie bekijken we deze tabellen tooshow hoe ze worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6898-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="d6898-160">Open **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="d6898-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="d6898-161">Vier tabellen zijn gedefinieerd--drie die worden gebruikt door de SDK Hallo en één die wordt gebruikt voor de taak Hallo zelf-items:</span><span class="sxs-lookup"><span data-stu-id="d6898-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="d6898-162">MS_TableOperations: Houdt Hallo items die u toobe gesynchroniseerd met de Hallo-server moet.</span><span class="sxs-lookup"><span data-stu-id="d6898-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="d6898-163">MS_TableOperationErrors: Houdt eventuele fouten die tijdens het offline synchroniseren optreden.</span><span class="sxs-lookup"><span data-stu-id="d6898-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="d6898-164">MS_TableConfig: Houdt Hallo laatst bijgewerkt voor de laatste synchronisatiebewerking Hallo voor alle pull-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d6898-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="d6898-165">Takentabel: Slaat Hallo taakitems.</span><span class="sxs-lookup"><span data-stu-id="d6898-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="d6898-166">Hallo systeemkolommen **createdAt**, **updatedAt**, en **versie** zijn optionele Systeemeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d6898-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="d6898-167">Hallo Mobile Apps SDK reserveert kolomnamen die met beginnen '**``**'.</span><span class="sxs-lookup"><span data-stu-id="d6898-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="d6898-168">Dit voorvoegsel niet gebruiken voor iets anders dan systeemkolommen.</span><span class="sxs-lookup"><span data-stu-id="d6898-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="d6898-169">Anders wordt uw kolomnamen gewijzigd wanneer u Hallo externe back-end.</span><span class="sxs-lookup"><span data-stu-id="d6898-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="d6898-170">Wanneer u Hallo offlinesynchronisatie functie gebruikt, definiëren Hallo drie tabellen en Hallo gegevenstabel.</span><span class="sxs-lookup"><span data-stu-id="d6898-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="d6898-171">Systeemtabellen</span><span class="sxs-lookup"><span data-stu-id="d6898-171">System tables</span></span>

<span data-ttu-id="d6898-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="d6898-172">**MS_TableOperations**</span></span>  

![MS_TableOperations tabelkenmerken][defining-core-data-tableoperations-entity]

| <span data-ttu-id="d6898-174">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="d6898-174">Attribute</span></span> | <span data-ttu-id="d6898-175">Type</span><span class="sxs-lookup"><span data-stu-id="d6898-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="d6898-176">id</span><span class="sxs-lookup"><span data-stu-id="d6898-176">id</span></span> | <span data-ttu-id="d6898-177">Geheel getal 64</span><span class="sxs-lookup"><span data-stu-id="d6898-177">Integer 64</span></span> |
| <span data-ttu-id="d6898-178">itemId</span><span class="sxs-lookup"><span data-stu-id="d6898-178">itemId</span></span> | <span data-ttu-id="d6898-179">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-179">String</span></span> |
| <span data-ttu-id="d6898-180">properties</span><span class="sxs-lookup"><span data-stu-id="d6898-180">properties</span></span> | <span data-ttu-id="d6898-181">Binaire gegevens</span><span class="sxs-lookup"><span data-stu-id="d6898-181">Binary Data</span></span> |
| <span data-ttu-id="d6898-182">Tabel</span><span class="sxs-lookup"><span data-stu-id="d6898-182">table</span></span> | <span data-ttu-id="d6898-183">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-183">String</span></span> |
| <span data-ttu-id="d6898-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="d6898-184">tableKind</span></span> | <span data-ttu-id="d6898-185">Geheel getal 16</span><span class="sxs-lookup"><span data-stu-id="d6898-185">Integer 16</span></span> |


<span data-ttu-id="d6898-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="d6898-186">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors tabelkenmerken][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="d6898-188">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="d6898-188">Attribute</span></span> | <span data-ttu-id="d6898-189">Type</span><span class="sxs-lookup"><span data-stu-id="d6898-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="d6898-190">id</span><span class="sxs-lookup"><span data-stu-id="d6898-190">id</span></span> |<span data-ttu-id="d6898-191">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-191">String</span></span> |
| <span data-ttu-id="d6898-192">operationId</span><span class="sxs-lookup"><span data-stu-id="d6898-192">operationId</span></span> |<span data-ttu-id="d6898-193">Geheel getal 64</span><span class="sxs-lookup"><span data-stu-id="d6898-193">Integer 64</span></span> |
| <span data-ttu-id="d6898-194">properties</span><span class="sxs-lookup"><span data-stu-id="d6898-194">properties</span></span> |<span data-ttu-id="d6898-195">Binaire gegevens</span><span class="sxs-lookup"><span data-stu-id="d6898-195">Binary Data</span></span> |
| <span data-ttu-id="d6898-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="d6898-196">tableKind</span></span> |<span data-ttu-id="d6898-197">Geheel getal 16</span><span class="sxs-lookup"><span data-stu-id="d6898-197">Integer 16</span></span> |

 <span data-ttu-id="d6898-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="d6898-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="d6898-199">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="d6898-199">Attribute</span></span> | <span data-ttu-id="d6898-200">Type</span><span class="sxs-lookup"><span data-stu-id="d6898-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="d6898-201">id</span><span class="sxs-lookup"><span data-stu-id="d6898-201">id</span></span> |<span data-ttu-id="d6898-202">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-202">String</span></span> |
| <span data-ttu-id="d6898-203">sleutel</span><span class="sxs-lookup"><span data-stu-id="d6898-203">key</span></span> |<span data-ttu-id="d6898-204">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-204">String</span></span> |
| <span data-ttu-id="d6898-205">KeyType</span><span class="sxs-lookup"><span data-stu-id="d6898-205">keyType</span></span> |<span data-ttu-id="d6898-206">Geheel getal 64</span><span class="sxs-lookup"><span data-stu-id="d6898-206">Integer 64</span></span> |
| <span data-ttu-id="d6898-207">Tabel</span><span class="sxs-lookup"><span data-stu-id="d6898-207">table</span></span> |<span data-ttu-id="d6898-208">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-208">String</span></span> |
| <span data-ttu-id="d6898-209">waarde</span><span class="sxs-lookup"><span data-stu-id="d6898-209">value</span></span> |<span data-ttu-id="d6898-210">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="d6898-211">Gegevenstabel</span><span class="sxs-lookup"><span data-stu-id="d6898-211">Data table</span></span>

<span data-ttu-id="d6898-212">**Takentabel**</span><span class="sxs-lookup"><span data-stu-id="d6898-212">**TodoItem**</span></span>

| <span data-ttu-id="d6898-213">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="d6898-213">Attribute</span></span> | <span data-ttu-id="d6898-214">Type</span><span class="sxs-lookup"><span data-stu-id="d6898-214">Type</span></span> | <span data-ttu-id="d6898-215">Opmerking</span><span class="sxs-lookup"><span data-stu-id="d6898-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6898-216">id</span><span class="sxs-lookup"><span data-stu-id="d6898-216">id</span></span> | <span data-ttu-id="d6898-217">Tekenreeks is gemarkeerd als vereist</span><span class="sxs-lookup"><span data-stu-id="d6898-217">String, marked required</span></span> |<span data-ttu-id="d6898-218">primaire sleutel in externe opslag</span><span class="sxs-lookup"><span data-stu-id="d6898-218">Primary key in remote store</span></span> |
| <span data-ttu-id="d6898-219">Voltooien</span><span class="sxs-lookup"><span data-stu-id="d6898-219">complete</span></span> | <span data-ttu-id="d6898-220">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d6898-220">Boolean</span></span> | <span data-ttu-id="d6898-221">Taak itemveld</span><span class="sxs-lookup"><span data-stu-id="d6898-221">To-do item field</span></span> |
| <span data-ttu-id="d6898-222">Tekst</span><span class="sxs-lookup"><span data-stu-id="d6898-222">text</span></span> |<span data-ttu-id="d6898-223">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-223">String</span></span> |<span data-ttu-id="d6898-224">Taak itemveld</span><span class="sxs-lookup"><span data-stu-id="d6898-224">To-do item field</span></span> |
| <span data-ttu-id="d6898-225">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="d6898-225">createdAt</span></span> | <span data-ttu-id="d6898-226">Date</span><span class="sxs-lookup"><span data-stu-id="d6898-226">Date</span></span> | <span data-ttu-id="d6898-227">(optioneel) Toegewezen te**createdAt** systeemeigenschap</span><span class="sxs-lookup"><span data-stu-id="d6898-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="d6898-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="d6898-228">updatedAt</span></span> | <span data-ttu-id="d6898-229">Date</span><span class="sxs-lookup"><span data-stu-id="d6898-229">Date</span></span> | <span data-ttu-id="d6898-230">(optioneel) Toegewezen te**updatedAt** systeemeigenschap</span><span class="sxs-lookup"><span data-stu-id="d6898-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="d6898-231">Versie</span><span class="sxs-lookup"><span data-stu-id="d6898-231">version</span></span> | <span data-ttu-id="d6898-232">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d6898-232">String</span></span> | <span data-ttu-id="d6898-233">(optioneel) Gebruikte toodetect conflicten, maps tooversion</span><span class="sxs-lookup"><span data-stu-id="d6898-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="d6898-234"><a name="setup-sync"></a>Hallo sync-gedrag Hallo app wijzigen</span><span class="sxs-lookup"><span data-stu-id="d6898-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="d6898-235">In deze sectie maakt wijzigen u Hallo app zodat deze wordt niet gesynchroniseerd op app starten of als u invoegen en items bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d6898-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="d6898-236">Synchronisatie alleen wanneer de knop voor vernieuwen gebaar hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d6898-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="d6898-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d6898-237">**Objective-C**:</span></span>

1. <span data-ttu-id="d6898-238">In **QSTodoListViewController.m**, Hallo wijzigen **viewDidLoad** methode tooremove Hallo aanroep te`[self refresh]` achter Hallo Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="d6898-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="d6898-239">Hallo-gegevens is nu niet gesynchroniseerd met de server Hallo op app starten.</span><span class="sxs-lookup"><span data-stu-id="d6898-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="d6898-240">In plaats daarvan wordt deze gesynchroniseerd met inhoud van het lokale archief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6898-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="d6898-241">In **QSTodoService.m**, Wijzig definitie van Hallo `addItem` zodat deze niet synchroniseren nadat het Hallo-item is ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="d6898-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="d6898-242">Hallo verwijderen `self syncData` blokkeren en vervang deze door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6898-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="d6898-243">Wijzigen van de definitie van Hallo `completeItem` zoals eerder is vermeld.</span><span class="sxs-lookup"><span data-stu-id="d6898-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="d6898-244">Hallo-blokkering voor verwijderen `self syncData` en vervang deze door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6898-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="d6898-245">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="d6898-245">**Swift**:</span></span>

<span data-ttu-id="d6898-246">In `viewDidLoad`in **ToDoTableViewController.swift**, commentaar Hallo twee regels hier, toostop synchroniseren bij starten van de app weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6898-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="d6898-247">Op moment van schrijven van dit Hallo Hallo Swift Todo-app niet Hallo-service bijgewerkt wanneer iemand toevoegt of een item is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d6898-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="d6898-248">Hallo-service alleen op app starten wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d6898-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="d6898-249"><a name="test-app"></a>Test Hallo app</span><span class="sxs-lookup"><span data-stu-id="d6898-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="d6898-250">In deze sectie maakt verbinding u tooan ongeldige URL toosimulate een offline-scenario.</span><span class="sxs-lookup"><span data-stu-id="d6898-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="d6898-251">Wanneer u gegevens toevoegt, zijn ze ondergebracht in Hallo lokale Core gegevens opslaan, maar ze zijn niet gesynchroniseerd met de Hallo back-end van mobile app.</span><span class="sxs-lookup"><span data-stu-id="d6898-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="d6898-252">Wijzig Hallo mobiele app-URL in **QSTodoService.m** tooan ongeldige URL en opnieuw uitvoeren Hallo-app:</span><span class="sxs-lookup"><span data-stu-id="d6898-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="d6898-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="d6898-253">**Objective-C**.</span></span> <span data-ttu-id="d6898-254">In QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="d6898-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="d6898-255">**SWIFT**.</span><span class="sxs-lookup"><span data-stu-id="d6898-255">**Swift**.</span></span> <span data-ttu-id="d6898-256">In ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="d6898-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="d6898-257">Sommige taakitems toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d6898-257">Add some to-do items.</span></span> <span data-ttu-id="d6898-258">Sluit simulator hello (of geforceerd sluiten Hallo app) af en start deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d6898-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="d6898-259">Controleer of uw wijzigingen blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="d6898-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="d6898-260">Hallo-inhoud van de externe Hallo weergeven **TodoItem** tabel:</span><span class="sxs-lookup"><span data-stu-id="d6898-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="d6898-261">Ga voor Node.js-back-end toohello [Azure-portal](https://portal.azure.com/) en op uw mobiele app back-end, **gemakkelijk tabellen** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="d6898-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="d6898-262">Voor een .NET terug beëindigen, gebruikt u een SQL-hulpprogramma, zoals SQL Server Management Studio of een REST-client, zoals Fiddler of Postman.</span><span class="sxs-lookup"><span data-stu-id="d6898-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="d6898-263">Controleer of de nieuwe items Hallo hebt *niet* is gesynchroniseerd met de Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="d6898-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="d6898-264">Wijziging Hallo URL back toohello corrigeren in **QSTodoService.m**, en Voer Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="d6898-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="d6898-265">Hallo vernieuwen gebaar uitvoeren met het binnenhalen van Hallo lijst met items.</span><span class="sxs-lookup"><span data-stu-id="d6898-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="d6898-266">Een spinner voortgang wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6898-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="d6898-267">Weergave Hallo **TodoItem** gegevens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d6898-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="d6898-268">nieuwe en gewijzigde taakitems Hallo moeten nu worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6898-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="d6898-269">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d6898-269">Summary</span></span>
<span data-ttu-id="d6898-270">toosupport hello offlinesynchronisatie functie we Hallo gebruikt `MSSyncTable` interface en geïnitialiseerd `MSClient.syncContext` met een lokaal archief.</span><span class="sxs-lookup"><span data-stu-id="d6898-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="d6898-271">In dit geval is het lokale archief Hallo een database op basis van gegevens van de Core.</span><span class="sxs-lookup"><span data-stu-id="d6898-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="d6898-272">Wanneer u een Core lokale gegevensarchief gebruikt, moet u verschillende tabellen met Hallo definiëren [corrigeren Systeemeigenschappen](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="d6898-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="d6898-273">Hallo normaal maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen voor mobiele apps werken alsof Hallo app nog steeds is verbonden, maar alle Hallo acties moeten worden uitgevoerd tegen Hallo lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="d6898-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="d6898-274">Wanneer we het lokale archief Hallo gesynchroniseerd met de Hallo-server, hebben we Hallo gebruikt **MSSyncTable.pullWithQuery** methode.</span><span class="sxs-lookup"><span data-stu-id="d6898-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6898-275">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d6898-275">Additional resources</span></span>
* <span data-ttu-id="d6898-276">[Offline synchroniseren van gegevens in mobiele Apps]</span><span class="sxs-lookup"><span data-stu-id="d6898-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="d6898-277">[Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services] \(Hallo video gaat over Mobile Services, maar Mobile Apps offline synchronisatie werkt op een vergelijkbare manier.\)</span><span class="sxs-lookup"><span data-stu-id="d6898-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[maken van een iOS-App]: app-service-mobile-ios-get-started.md
[Offline synchroniseren van gegevens in mobiele Apps]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
