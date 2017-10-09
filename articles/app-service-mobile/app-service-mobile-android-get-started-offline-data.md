---
title: aaaEnable offlinesynchronisatie voor uw Azure Mobile Apps (Android)
description: Meer informatie over hoe toouse App Service Mobile Apps toocache en sync offline gegevens in uw Android-toepassing
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="25938-103">Offlinesynchronisatie voor uw mobiele Android-app inschakelen</span><span class="sxs-lookup"><span data-stu-id="25938-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="25938-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="25938-104">Overview</span></span>
<span data-ttu-id="25938-105">Deze zelfstudie behandelt Hallo offlinesynchronisatie-functie van Azure Mobile Apps voor Android.</span><span class="sxs-lookup"><span data-stu-id="25938-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="25938-106">Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="25938-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="25938-107">Wijzigingen worden opgeslagen in een lokale database.</span><span class="sxs-lookup"><span data-stu-id="25938-107">Changes are stored in a local database.</span></span> <span data-ttu-id="25938-108">Zodra Hallo apparaat weer online is, worden deze wijzigingen gesynchroniseerd met Hallo externe back-end.</span><span class="sxs-lookup"><span data-stu-id="25938-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="25938-109">Als dit uw eerste ervaring met Azure Mobile Apps is, moet u eerst Hallo zelfstudie uitvoeren [maken van een Android-App].</span><span class="sxs-lookup"><span data-stu-id="25938-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="25938-110">Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo data access-extensie pakketten tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="25938-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="25938-111">Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="25938-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="25938-112">toolearn meer informatie over Hallo offlinesynchronisatie functie, Zie Hallo onderwerp [Offline synchroniseren van gegevens in Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="25938-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="25938-113">Hallo app toosupport offlinesynchronisatie bijwerken</span><span class="sxs-lookup"><span data-stu-id="25938-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="25938-114">Met het offline synchroniseren die u lezen tooand schrijven van een *synchronisatietabel* (met behulp van Hallo *IMobileServiceSyncTable* interface), die deel uitmaakt van een **SQLite** database op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="25938-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="25938-115">toopush en pull wijzigingen tussen Hallo-apparaat en Azure Mobile Services die u gebruikt een *synchronisatiecontext* (*MobileServiceClient.SyncContext*), die u met de lokale database Hallo initialiseren lokaal toostore gegevens.</span><span class="sxs-lookup"><span data-stu-id="25938-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="25938-116">In `TodoActivity.java`, commentaar Hallo bestaande definitie van `mToDoTable` en verwijder het commentaarteken Hallo tabel synchronisatieversie:</span><span class="sxs-lookup"><span data-stu-id="25938-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="25938-117">In Hallo `onCreate` methode, commentaar Hallo bestaande initialisatie van `mToDoTable` en het commentaar verwijderen van deze definitie voor:</span><span class="sxs-lookup"><span data-stu-id="25938-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="25938-118">In `refreshItemsFromTable` commentaar Hallo definitie van `results` en het commentaar verwijderen van deze definitie voor:</span><span class="sxs-lookup"><span data-stu-id="25938-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="25938-119">Commentaar Hallo definitie van `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="25938-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="25938-120">Verwijder de definitie van Hallo opmerkingen `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="25938-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="25938-121">Verwijder de definitie van Hallo opmerkingen `sync`:</span><span class="sxs-lookup"><span data-stu-id="25938-121">Uncomment hello definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a><span data-ttu-id="25938-122">Test Hallo app</span><span class="sxs-lookup"><span data-stu-id="25938-122">Test hello app</span></span>
<span data-ttu-id="25938-123">In deze sectie kunt u testen Hallo gedrag met Wi-Fi op, en schakelt u vervolgens Wi-Fi toocreate een offline-scenario.</span><span class="sxs-lookup"><span data-stu-id="25938-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="25938-124">Wanneer u gegevens toevoegt, ze worden beheerd in Hallo lokale SQLite archief, maar niet gesynchroniseerde toohello mobiele service, totdat u op Hallo **vernieuwen** knop.</span><span class="sxs-lookup"><span data-stu-id="25938-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="25938-125">Andere apps kunnen verschillende vereisten met betrekking tot wanneer gegevens toobe gesynchroniseerd moet, maar voor demonstratiedoeleinden in deze zelfstudie heeft Hallo gebruiker deze aanvragen.</span><span class="sxs-lookup"><span data-stu-id="25938-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="25938-126">Wanneer u op deze knop klikt, wordt er een nieuwe achtergrondtaak gestart.</span><span class="sxs-lookup"><span data-stu-id="25938-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="25938-127">Deze duwt eerst alle wijzigingen toohello lokale archief met synchronisatiecontext, wordt de gegevens worden gewijzigd van Azure toohello lokale tabel.</span><span class="sxs-lookup"><span data-stu-id="25938-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="25938-128">Offline testen</span><span class="sxs-lookup"><span data-stu-id="25938-128">Offline testing</span></span>
1. <span data-ttu-id="25938-129">Plaats Hallo apparaat of emulator in *vliegtuigmodus*.</span><span class="sxs-lookup"><span data-stu-id="25938-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="25938-130">Hiermee maakt u een offline-scenario.</span><span class="sxs-lookup"><span data-stu-id="25938-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="25938-131">Voeg enkele toe *ToDo* items of bepaalde items als voltooid markeren.</span><span class="sxs-lookup"><span data-stu-id="25938-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="25938-132">Hallo apparaat of emulator (of geforceerd sluiten Hallo app) afsluiten en opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="25938-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="25938-133">Controleer of dat uw wijzigingen zijn opgeslagen op Hallo apparaat omdat ze worden beheerd in Hallo lokale SQLite-archief.</span><span class="sxs-lookup"><span data-stu-id="25938-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="25938-134">Hallo-inhoud van hello Azure *TodoItem* tabel met een SQL-hulpprogramma zoals *SQL Server Management Studio*, of een REST-client, zoals *Fiddler* of  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="25938-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="25938-135">Controleer of de nieuwe items Hallo hebt *niet* is gesynchroniseerde toohello server</span><span class="sxs-lookup"><span data-stu-id="25938-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="25938-136">Ga voor een Node.js-end toohello [Azure-portal](https://portal.azure.com/), en in uw Mobile App back-end op **gemakkelijk tabellen** > **TodoItem** tooview Hallo inhoud Hallo `TodoItem` tabel.</span><span class="sxs-lookup"><span data-stu-id="25938-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="25938-137">Voor een .NET-backend weergave Hallo tabel inhoud met een SQL-hulpprogramma zoals *SQL Server Management Studio*, of een REST-client, zoals *Fiddler* of *Postman*.</span><span class="sxs-lookup"><span data-stu-id="25938-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="25938-138">Wi-Fi inschakelen in Hallo-apparaat of simulator.</span><span class="sxs-lookup"><span data-stu-id="25938-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="25938-139">Klik vervolgens op Hallo **vernieuwen** knop.</span><span class="sxs-lookup"><span data-stu-id="25938-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="25938-140">Hallo takentabel gegevens weer in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="25938-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="25938-141">Hallo die nieuwe en gewijzigde taken wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="25938-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25938-142">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="25938-142">Additional Resources</span></span>
* <span data-ttu-id="25938-143">[Offline synchroniseren van gegevens in Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="25938-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="25938-144">[Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services] \(Opmerking: Hallo video in Mobile Services, maar offlinesynchronisatie werkt op een vergelijkbare manier als in Azure Mobile Apps\)</span><span class="sxs-lookup"><span data-stu-id="25938-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[Offline synchroniseren van gegevens in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md

[maken van een Android-App]: app-service-mobile-android-get-started.md

[Cloud behandeld: Offlinesynchronisatie in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

