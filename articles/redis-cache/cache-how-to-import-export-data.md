---
title: aaaImport en exporteren van gegevens in Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe gegevens tooand van tooimport en exporteren van blob-opslag met de exemplaren van uw premium Azure Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="1fb1b-103">Importeren en exporteren van gegevens in Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="1fb1b-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="1fb1b-104">Import/Export is een Azure Redis-Cache gegevensbewerking voor het beheer, waarmee u tooimport gegevens in Azure Redis-Cache of het exporteren van gegevens van Azure Redis-Cache door te importeren en exporteren van een momentopname van een Redis-Cache Database (RDB) van een blob premium cache tooa in een Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-104">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="1fb1b-105">**Exporteren** -kunt u uw Azure Redis-Cache RDB momentopnamen tooa pagina-Blob exporteren.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-105">**Export** - you can export your Azure Redis Cache RDB snapshots tooa Page Blob.</span></span>
- <span data-ttu-id="1fb1b-106">**Importeren** -u kunt de momentopnamen van uw Redis-Cache RDB importeren uit een pagina-Blob of een blok-Blob.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="1fb1b-107">Voor importeren/exporteren kunt u toomigrate tussen verschillende exemplaren van Azure Redis-Cache of vullen Hallo cache met gegevens voor het gebruik.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-107">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="1fb1b-108">In dit artikel bevat richtlijnen voor het importeren en exporteren van gegevens met Azure Redis-Cache en vindt u antwoorden Hallo toocommonly vragen.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides hello answers toocommonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fb1b-109">Import/Export is Preview-versie en is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="1fb1b-110">Importeren</span><span class="sxs-lookup"><span data-stu-id="1fb1b-110">Import</span></span>
<span data-ttu-id="1fb1b-111">Importeren kan gebruikte toobring Redis compatibele RDB bestanden vanaf een willekeurige Redis-server uitgevoerd in een cloud of de omgeving, inclusief Redis uitgevoerd op Linux, Windows of elke cloudprovider zoals Amazon Web Services en andere zijn.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-111">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="1fb1b-112">Het importeren van gegevens is een eenvoudige manier toocreate een cache met vooraf ingestelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-112">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="1fb1b-113">Tijdens het importproces Hallo, Azure Redis-Cache Hallo RDB bestanden uit Azure storage in het geheugen geladen en vervolgens ingevoegd Hallo sleutels in Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-113">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory and then inserts hello keys into hello cache.</span></span>

> [!NOTE]
> <span data-ttu-id="1fb1b-114">Voordat u de importbewerking Hallo begint, controleert u of uw Redis-Database (RDB) of meer bestanden zijn geüpload naar de pagina of blok-blobs in Azure-opslag in Hallo dezelfde regio en abonnement als uw Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-114">Before beginning hello import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in hello same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="1fb1b-115">Zie voor meer informatie [aan de slag met Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="1fb1b-116">Als u uw RDB-bestand met behulp van Hallo geëxporteerd [exporteren van Azure Redis-Cache](#export) functie, het bestand RDB is al opgeslagen in een pagina-blob en is gereed om te importeren.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-116">If you exported your RDB file using hello [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="1fb1b-117">tooimport een of meer blobs, cache, geëxporteerd [tooyour cache Bladeren](cache-configure.md#configure-redis-cache-settings) in hello Azure-portal en klikt u op **gegevens importeren** van Hallo **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-117">tooimport one or more exported cache blobs, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Import data** from hello **Resource menu**.</span></span>

    ![Gegevens importeren][cache-import-data]
2. <span data-ttu-id="1fb1b-119">Klik op **kiezen Blob(s)** en selecteer Hallo storage-account dat Hallo gegevens tooimport bevat.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-119">Click **Choose Blob(s)** and select hello storage account that contains hello data tooimport.</span></span>

    ![Opslagaccount kiezen][cache-import-choose-storage-account]
3. <span data-ttu-id="1fb1b-121">Klik op Hallo-container die Hallo gegevens tooimport bevat.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-121">Click hello container that contains hello data tooimport.</span></span>

    ![Kies container][cache-import-choose-container]
4. <span data-ttu-id="1fb1b-123">Selecteer een of meer blobs tooimport door te klikken op Hallo gebied toohello links van Hallo blob-naam en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-123">Select one or more blobs tooimport by clicking hello area toohello left of hello blob name, and then click **Select**.</span></span>

    ![Kies BLOB 's][cache-import-choose-blobs]
5. <span data-ttu-id="1fb1b-125">Klik op **importeren** toobegin Hallo importproces.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-125">Click **Import** toobegin hello import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1fb1b-126">Hallo-cache is niet toegankelijk is voor cacheclients tijdens het importeren van Hallo en alle bestaande gegevens in cache Hallo is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-126">hello cache is not accessible by cache clients during hello import process, and any existing data in hello cache is deleted.</span></span>
   >
   >

    ![Importeren][cache-import-blobs]

    <span data-ttu-id="1fb1b-128">U kunt voortgang Hallo van importbewerking Hallo door volgende Hallo meldingen van hello Azure-portal of door het Hallo-gebeurtenissen weergeven in Hallo [controlelogboek](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-128">You can monitor hello progress of hello import operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Voortgang importeren][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="1fb1b-130">Exporteren</span><span class="sxs-lookup"><span data-stu-id="1fb1b-130">Export</span></span>
<span data-ttu-id="1fb1b-131">Exporteren kunt u tooexport Hallo opgeslagen gegevens in Azure Redis-Cache tooRedis compatibel RDB bestanden.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-131">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB file(s).</span></span> <span data-ttu-id="1fb1b-132">U kunt deze functie toomove op gegevens uit een Azure Redis-Cache-exemplaar tooanother of tooanother Redis-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-132">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="1fb1b-133">Tijdens het exportproces hello, wordt een tijdelijk bestand op Hallo VM dat hosts Hallo server-exemplaar van Azure Redis-Cache en Hallo bestand geüploade toohello aangewezen storage-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-133">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="1fb1b-134">Wanneer de exportbewerking Hallo is voltooid met de status van slagen of mislukken, wordt Hallo tijdelijk bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-134">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

1. <span data-ttu-id="1fb1b-135">tooexport hello huidige inhoud van Hallo cache toostorage, [tooyour cache Bladeren](cache-configure.md#configure-redis-cache-settings) in hello Azure-portal en klikt u op **gegevens exporteren** van Hallo **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-135">tooexport hello current contents of hello cache toostorage, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Export data** from hello **Resource menu**.</span></span>

    ![Kies de opslagcontainer][cache-export-data-choose-storage-container]
2. <span data-ttu-id="1fb1b-137">Klik op **Opslagcontainer Kies** en selecteer de gewenste Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-137">Click **Choose Storage Container** and select hello desired storage account.</span></span> <span data-ttu-id="1fb1b-138">Hallo storage-account moet zich in Hallo hetzelfde abonnement en dezelfde regio bevinden als uw cache.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-138">hello storage account must be in hello same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1fb1b-139">Werkt met pagina-blobs, die worden ondersteund door zowel klassieke als Resource Manager storage-accounts, maar worden niet ondersteund door exporteren [Blob storage-accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) op dit moment.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Storage-account][cache-export-data-choose-account]
3. <span data-ttu-id="1fb1b-141">Kies Hallo blob-container en klik op de gewenste **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-141">Choose hello desired blob container and click **Select**.</span></span> <span data-ttu-id="1fb1b-142">toouse nieuwe container, klikt u op **Container toevoegen** tooadd het eerste en selecteer vervolgens het uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-142">toouse new a container, click **Add Container** tooadd it first and then select it from hello list.</span></span>

    ![Kies de opslagcontainer][cache-export-data-container]
4. <span data-ttu-id="1fb1b-144">Typ een **Blob voorvoegsel** en klik op **exporteren** toostart Hallo exportproces.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-144">Type a **Blob name prefix** and click **Export** toostart hello export process.</span></span> <span data-ttu-id="1fb1b-145">Hallo blob-voorvoegsel is gebruikte tooprefix Hallo namen van bestanden die door deze bewerking uitvoer gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-145">hello blob name prefix is used tooprefix hello names of files generated by this export operation.</span></span>

    ![Exporteren][cache-export-data]

    <span data-ttu-id="1fb1b-147">U kunt voortgang Hallo van de exportbewerking Hallo door volgende Hallo meldingen van hello Azure-portal of door het Hallo-gebeurtenissen weergeven in Hallo [controlelogboek](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-147">You can monitor hello progress of hello export operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Gegevens exporteren voltooien][cache-export-data-export-complete]

    <span data-ttu-id="1fb1b-149">Caches blijven beschikbaar voor gebruik tijdens het exportproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-149">Caches remain available for use during hello export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="1fb1b-150">Veelgestelde vragen over het importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="1fb1b-150">Import/Export FAQ</span></span>
<span data-ttu-id="1fb1b-151">Deze sectie bevat veelgestelde vragen over Hallo Import/Export-functie.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-151">This section contains frequently asked questions about hello Import/Export feature.</span></span>

* [<span data-ttu-id="1fb1b-152">Welke prijzen lagen kunt importeren/exporteren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="1fb1b-153">Kan ik gegevens importeren vanaf een willekeurige Redis-server?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="1fb1b-154">Welke versies RDB kan ik importeren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="1fb1b-155">Mijn cache is beschikbaar tijdens een bewerking voor importeren/exporteren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="1fb1b-156">Kan ik voor importeren/exporteren met Redis-cluster gebruiken?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="1fb1b-157">Hoe werkt voor importeren/exporteren met een aangepaste databases instellen?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="1fb1b-158">Hoe verschilt voor importeren/exporteren van Redis-persistentie?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="1fb1b-159">Kan ik automatiseren met behulp van PowerShell, CLI of andere clients management voor importeren/exporteren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="1fb1b-160">Ik heb ontvangen een time-outfout tijdens de Import/Export-bewerking. Wat betekent dit?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="1fb1b-161">Ik krijg een fout opgetreden bij het exporteren van mijn gegevens tooAzure Blob Storage. Wat is er gebeurd?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-161">I got an error when exporting my data tooAzure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="1fb1b-162">Welke prijzen lagen kunt importeren/exporteren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="1fb1b-163">Import/Export is alleen beschikbaar in Hallo premium-prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-163">Import/Export is available only in hello premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="1fb1b-164">Kan ik gegevens importeren vanaf een willekeurige Redis-server?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="1fb1b-165">Ja, Daarnaast tooimporting gegevens van exemplaren van Azure Redis-Cache hebt geëxporteerd, kunt u importeren RDB bestanden vanaf een willekeurige Redis-server in een cloud of de omgeving, zoals Linux, Windows of cloudproviders zoals Amazon Web Services wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-165">Yes, in addition tooimporting data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="1fb1b-166">toodo dit uploaden Hallo RDB bestand van Hallo gewenst Redis-server naar een pagina of het blok-blob in een Azure Storage-Account en vervolgens importeren deze naar uw premium Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-166">toodo this, upload hello RDB file from hello desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="1fb1b-167">U kunt bijvoorbeeld wilt tooexport Hallo gegevens uit uw productie-cache en importeren in een cache die wordt gebruikt als onderdeel van een testomgeving voor testdoeleinden of migratie.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-167">For example, you may want tooexport hello data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fb1b-168">toosuccessfully gegevens geëxporteerd van Redis-servers dan de Azure Redis-Cache wanneer met behulp van een pagina-blob, Hallo blob paginaformaat moet worden afgestemd op de grens van een sectorgrootte van 512 bytes importeren.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-168">toosuccessfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, hello page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="1fb1b-169">Voor een voorbeeld code tooperform vereist een byte opvulling, Zie [voorbeeld pagina blog uploaden](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-169">For sample code tooperform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="1fb1b-170">Welke versies RDB kan ik importeren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-170">What RDB versions can I import?</span></span>

<span data-ttu-id="1fb1b-171">Azure Redis-Cache ondersteunt RDB importeren tot via RDB versie 7.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="1fb1b-172">Mijn cache is beschikbaar tijdens een bewerking voor importeren/exporteren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="1fb1b-173">**Exporteren** - Caches beschikbaar blijven en u kunt toouse uw cache blijven tijdens een exportbewerking.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-173">**Export** - Caches remain available and you can continue toouse your cache during an export operation.</span></span>
* <span data-ttu-id="1fb1b-174">**Importeren** - Caches niet beschikbaar wanneer een importbewerking wordt gestart en worden beschikbaar voor gebruik wanneer Hallo importbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when hello import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="1fb1b-175">Kan ik voor importeren/exporteren met Redis-cluster gebruiken?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="1fb1b-176">Ja, en u kunt importeren/exporteren tussen een geclusterde cache en een niet-geclusterde cache.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="1fb1b-177">Sinds de Redis-cluster [alleen ondersteunt database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), alle gegevens in databases dan 0 is niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="1fb1b-178">Wanneer geclusterde cache-gegevens worden geïmporteerd, wordt Hallo sleutels herverdeeld over Hallo shards van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-178">When clustered cache data is imported, hello keys are redistributed among hello shards of hello cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="1fb1b-179">Hoe werkt voor importeren/exporteren met een aangepaste databases instellen?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="1fb1b-180">Sommige Prijscategorieën hebben verschillende [databases limieten](cache-configure.md#databases), dus er enkele overwegingen zijn bij het importeren als u een aangepaste waarde voor Hallo geconfigureerd `databases` instellen tijdens het maken van de cache.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="1fb1b-181">Bij het importeren van tooa prijscategorie met een lagere `databases` limiet dan Hallo laag die u hebt geëxporteerd:</span><span class="sxs-lookup"><span data-stu-id="1fb1b-181">When importing tooa pricing tier with a lower `databases` limit than hello tier from which you exported:</span></span>
  * <span data-ttu-id="1fb1b-182">Als u van Hallo standaardaantal gebruikmaakt `databases`, namelijk 16 voor alle Prijscategorieën, gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-182">If you are using hello default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="1fb1b-183">Als u een aangepaste aantal `databases` dat servicetier valt binnen de grenzen Hallo voor Hallo toowhich die u wilt importeren, gegevens niet verloren.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-183">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are importing, no data is lost.</span></span>
  * <span data-ttu-id="1fb1b-184">Als de geëxporteerde gegevens gegevens in een database die overschrijdt de grenzen van de nieuwe laag Hallo hello bevat, Hallo gegevens uit deze hogere databases niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-184">If your exported data contained data in a database that exceeds hello limits of hello new tier, hello data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="1fb1b-185">Hoe verschilt voor importeren/exporteren van Redis-persistentie?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="1fb1b-186">Azure Redis-Cache-persistentie kunt u toopersist opgeslagen gegevens in Redis tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-186">Azure Redis Cache persistence allows you toopersist data stored in Redis tooAzure Storage.</span></span> <span data-ttu-id="1fb1b-187">Wanneer de persistentie is geconfigureerd, persistente Azure Redis-Cache een momentopname van Hallo Redis-cache in een Redis-binaire indeling toodisk op basis van een back-upfrequentie die kunnen worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-187">When persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="1fb1b-188">Als er een onherstelbare gebeurtenis optreedt die zowel Hallo primaire en replica cache uitgeschakeld, wordt automatisch met de meest recente momentopname Hallo Hallo cachegegevens teruggezet.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-188">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache data is restored automatically using hello most recent snapshot.</span></span> <span data-ttu-id="1fb1b-189">Zie voor meer informatie [hoe tooconfigure gegevenspersistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-189">For more information, see [How tooconfigure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="1fb1b-190">Import / Export kunt u gegevens toobring in of exporteren uit Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-190">Import/ Export allows you toobring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="1fb1b-191">Deze niet configureren, back-up en herstellen met behulp van Redis-persistentie.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="1fb1b-192">Kan ik automatiseren met behulp van PowerShell, CLI of andere clients management voor importeren/exporteren?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="1fb1b-193">Ja, voor PowerShell instructies raadpleegt u [tooimport een Redis-cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) en [tooexport een Redis-cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-193">Yes, for PowerShell instructions see [tooimport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [tooexport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="1fb1b-194">Ik heb ontvangen een time-outfout tijdens de Import/Export-bewerking.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="1fb1b-195">Wat betekent dit?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-195">What does it mean?</span></span>
<span data-ttu-id="1fb1b-196">Als u op Hallo blijven **gegevens importeren** of **gegevens exporteren** blade langer dan 15 minuten voordat u begint Hallo bewerking er een foutbericht met een fout bericht vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="1fb1b-196">If you remain on hello **Import data** or **Export data** blade for longer than 15 minutes before initiating hello operation, you receive an error with an error message similar toohello following example:</span></span>

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

<span data-ttu-id="1fb1b-197">tooresolve dit initiëren Hallo import- of exportbewerking voordat 15 minuten is verstreken.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-197">tooresolve this, initiate hello import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a><span data-ttu-id="1fb1b-198">Ik krijg een fout opgetreden bij het exporteren van mijn gegevens tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-198">I got an error when exporting my data tooAzure Blob Storage.</span></span> <span data-ttu-id="1fb1b-199">Wat is er gebeurd?</span><span class="sxs-lookup"><span data-stu-id="1fb1b-199">What happened?</span></span>
<span data-ttu-id="1fb1b-200">Export werkt alleen met RDB-bestanden die zijn opgeslagen als pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="1fb1b-201">Andere typen blob worden momenteel niet ondersteund, met inbegrip van blob storage-accounts met hot en cool lagen.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="1fb1b-202">Zie voor meer informatie [Blob storage-accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="1fb1b-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fb1b-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1fb1b-203">Next steps</span></span>
<span data-ttu-id="1fb1b-204">Meer informatie over hoe meer premium toouse functies in de cache.</span><span class="sxs-lookup"><span data-stu-id="1fb1b-204">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="1fb1b-205">Inleiding toohello Azure Redis-Cache Premium-laag</span><span class="sxs-lookup"><span data-stu-id="1fb1b-205">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
