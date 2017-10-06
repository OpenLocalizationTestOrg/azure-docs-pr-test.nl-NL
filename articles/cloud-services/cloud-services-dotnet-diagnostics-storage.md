---
title: aaaStore en diagnostische gegevens weergeven in Azure Storage | Microsoft Docs
description: Azure diagnostics-gegevens ophalen voor Azure Storage en bekijken
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="96c17-103">Diagnostische gegevens opslaan en weergeven in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="96c17-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="96c17-104">Diagnostische gegevens is niet permanent opgeslagen tenzij u deze toohello Microsoft Azure-opslagemulator of tooAzure opslag overdragen.</span><span class="sxs-lookup"><span data-stu-id="96c17-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="96c17-105">Eenmaal in de opslag, kunnen deze worden bekeken met een van de verschillende beschikbare hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="96c17-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="96c17-106">Storage-account opgeven</span><span class="sxs-lookup"><span data-stu-id="96c17-106">Specify a storage account</span></span>
<span data-ttu-id="96c17-107">U opgeven Hallo storage-account dat u wilt dat toouse in Hallo ServiceConfiguration.cscfg bestand.</span><span class="sxs-lookup"><span data-stu-id="96c17-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="96c17-108">Hallo-accountgegevens wordt gedefinieerd als een verbindingsreeks in een configuratie-instelling.</span><span class="sxs-lookup"><span data-stu-id="96c17-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="96c17-109">Hallo toont volgende voorbeeld Hallo standaard-verbindingsreeks is gemaakt voor een nieuwe Cloudservice-project in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="96c17-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="96c17-110">U kunt deze tooprovide account verbindingsinformatie voor een Azure storage-account wijzigen.</span><span class="sxs-lookup"><span data-stu-id="96c17-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="96c17-111">Afhankelijk van het type Hallo van diagnostische gegevens worden verzameld, maakt gebruik van Azure Diagnostics Hallo Blob-service of Hallo tabel-service.</span><span class="sxs-lookup"><span data-stu-id="96c17-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="96c17-112">Hallo volgende tabel toont Hallo gegevensbronnen die worden doorgevoerd en hun notatie.</span><span class="sxs-lookup"><span data-stu-id="96c17-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="96c17-113">Gegevensbron</span><span class="sxs-lookup"><span data-stu-id="96c17-113">Data source</span></span> | <span data-ttu-id="96c17-114">Opslagindeling</span><span class="sxs-lookup"><span data-stu-id="96c17-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="96c17-115">Azure-Logboeken</span><span class="sxs-lookup"><span data-stu-id="96c17-115">Azure logs</span></span> |<span data-ttu-id="96c17-116">Tabel</span><span class="sxs-lookup"><span data-stu-id="96c17-116">Table</span></span> |
| <span data-ttu-id="96c17-117">IIS 7.0-Logboeken</span><span class="sxs-lookup"><span data-stu-id="96c17-117">IIS 7.0 logs</span></span> |<span data-ttu-id="96c17-118">Blob</span><span class="sxs-lookup"><span data-stu-id="96c17-118">Blob</span></span> |
| <span data-ttu-id="96c17-119">Logboeken van Azure Diagnostics-infrastructuur</span><span class="sxs-lookup"><span data-stu-id="96c17-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="96c17-120">Tabel</span><span class="sxs-lookup"><span data-stu-id="96c17-120">Table</span></span> |
| <span data-ttu-id="96c17-121">Logboeken met traceringen aanvraag is mislukt</span><span class="sxs-lookup"><span data-stu-id="96c17-121">Failed Request Trace logs</span></span> |<span data-ttu-id="96c17-122">Blob</span><span class="sxs-lookup"><span data-stu-id="96c17-122">Blob</span></span> |
| <span data-ttu-id="96c17-123">Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="96c17-123">Windows Event logs</span></span> |<span data-ttu-id="96c17-124">Tabel</span><span class="sxs-lookup"><span data-stu-id="96c17-124">Table</span></span> |
| <span data-ttu-id="96c17-125">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="96c17-125">Performance counters</span></span> |<span data-ttu-id="96c17-126">Tabel</span><span class="sxs-lookup"><span data-stu-id="96c17-126">Table</span></span> |
| <span data-ttu-id="96c17-127">Crashdumps</span><span class="sxs-lookup"><span data-stu-id="96c17-127">Crash dumps</span></span> |<span data-ttu-id="96c17-128">Blob</span><span class="sxs-lookup"><span data-stu-id="96c17-128">Blob</span></span> |
| <span data-ttu-id="96c17-129">Aangepaste foutenlogboeken</span><span class="sxs-lookup"><span data-stu-id="96c17-129">Custom error logs</span></span> |<span data-ttu-id="96c17-130">Blob</span><span class="sxs-lookup"><span data-stu-id="96c17-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="96c17-131">Diagnostische gegevens overbrengen</span><span class="sxs-lookup"><span data-stu-id="96c17-131">Transfer diagnostic data</span></span>
<span data-ttu-id="96c17-132">Voor SDK 2.5 en hoger kan Hallo aanvraag tootransfer diagnostische gegevens via het configuratiebestand Hallo optreden.</span><span class="sxs-lookup"><span data-stu-id="96c17-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="96c17-133">U kunt diagnostische gegevens overbrengen met regelmatige tussenpozen zoals opgegeven in het Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="96c17-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="96c17-134">Voor SDK-2.4 en vorige kunt u tootransfer Hallo diagnostische gegevens als programmatisch via Hallo configuratiebestand ook vragen.</span><span class="sxs-lookup"><span data-stu-id="96c17-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="96c17-135">Hallo programmatische aanpak kunt u ook toodo op aanvraag overdrachten.</span><span class="sxs-lookup"><span data-stu-id="96c17-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96c17-136">Wanneer u diagnostische gegevens tooan Azure storage-account overdraagt, u kosten in rekening worden voor opslagbronnen Hallo die gebruikmaakt van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="96c17-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="96c17-137">Diagnostische gegevens op te slaan</span><span class="sxs-lookup"><span data-stu-id="96c17-137">Store diagnostic data</span></span>
<span data-ttu-id="96c17-138">Logboekgegevens worden opgeslagen in Blob of Table storage met Hallo namen te volgen:</span><span class="sxs-lookup"><span data-stu-id="96c17-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="96c17-139">**Tabellen**</span><span class="sxs-lookup"><span data-stu-id="96c17-139">**Tables**</span></span>

* <span data-ttu-id="96c17-140">**WadLogsTable** - Logboeken geschreven in code met behulp van de traceringslistener Hallo.</span><span class="sxs-lookup"><span data-stu-id="96c17-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="96c17-141">**WADDiagnosticInfrastructureLogsTable** -diagnostische monitor en configuratie van wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="96c17-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="96c17-142">**WADDirectoriesTable** – mappen die Hallo diagnostische monitor wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="96c17-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="96c17-143">Dit omvat IIS-logboeken, IIS kan niet logboeken aanvragen en aangepaste mappen.</span><span class="sxs-lookup"><span data-stu-id="96c17-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="96c17-144">Hallo-locatie van Hallo blob-logboekbestand is opgegeven in Hallo containerveld en Hallo-naam van Hallo blob in Hallo RelativePath veld.</span><span class="sxs-lookup"><span data-stu-id="96c17-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="96c17-145">Hallo AbsolutePath veld geeft aan Hallo locatie en naam van bestand Hallo zoals deze bestond op Hallo virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="96c17-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="96c17-146">**WADPerformanceCountersTable** – prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="96c17-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="96c17-147">**WADWindowsEventLogsTable** – Windows-gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="96c17-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="96c17-148">**Blobs**</span><span class="sxs-lookup"><span data-stu-id="96c17-148">**Blobs**</span></span>

* <span data-ttu-id="96c17-149">**af-besturingselement-container** – (alleen voor SDK-2.4 en vorige) bevat Hallo XML-configuratiebestanden die bepaalt hello Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="96c17-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="96c17-150">**af-iis-failedreqlogfiles** – bevat gegevens uit logboeken IIS aanvragen is mislukt.</span><span class="sxs-lookup"><span data-stu-id="96c17-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="96c17-151">**af-iis-logboekbestanden** : bevat informatie over IIS-logboeken.</span><span class="sxs-lookup"><span data-stu-id="96c17-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="96c17-152">**'aangepaste'** – op basis van een aangepaste container over het configureren van mappen die worden bewaakt door Hallo diagnostische monitor.</span><span class="sxs-lookup"><span data-stu-id="96c17-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="96c17-153">Hallo-naam van deze blob-container wordt in WADDirectoriesTable worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="96c17-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="96c17-154">Hulpprogramma's voor tooview diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="96c17-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="96c17-155">Er zijn verschillende hulpprogramma's beschikbaar tooview Hallo gegevens nadat deze overgedragen toostorage is.</span><span class="sxs-lookup"><span data-stu-id="96c17-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="96c17-156">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="96c17-156">For example:</span></span>

* <span data-ttu-id="96c17-157">Server Explorer in Visual Studio - als u hulpprogramma's hello Azure hebt geïnstalleerd voor Microsoft Visual Studio, kunt u hello Azure Storage-knooppunt in Server Explorer tooview alleen-lezen blob- en gegevens van uw Azure storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="96c17-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="96c17-158">U kunt gegevens weergeven vanuit uw lokale opslagaccount voor de emulator en ook van storage-accounts u hebt gemaakt voor Azure.</span><span class="sxs-lookup"><span data-stu-id="96c17-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="96c17-159">Zie voor meer informatie [surfen en het beheren van opslagbronnen met Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="96c17-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="96c17-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app waarmee u tooeasily werken met Azure Storage-gegevens op Windows, OSX en Linux.</span><span class="sxs-lookup"><span data-stu-id="96c17-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="96c17-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) bevat Azure Diagnostics Manager waarmee u tooview, downloaden en Hallo diagnostische gegevens verzameld door Hallo toepassingen die worden uitgevoerd op Azure beheren.</span><span class="sxs-lookup"><span data-stu-id="96c17-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96c17-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96c17-162">Next Steps</span></span>
[<span data-ttu-id="96c17-163">Hallo-stroom in een Cloud Services-toepassing met Azure Diagnostics traceren</span><span class="sxs-lookup"><span data-stu-id="96c17-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

