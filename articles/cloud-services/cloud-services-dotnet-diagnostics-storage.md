---
title: Diagnostische gegevens opslaan en weergeven in Azure Storage | Microsoft Docs
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="95e10-103">Diagnostische gegevens opslaan en weergeven in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="95e10-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="95e10-104">Diagnostische gegevens is niet permanent opgeslagen tenzij u deze naar de Microsoft Azure-opslagemulator of naar Azure storage overdragen.</span><span class="sxs-lookup"><span data-stu-id="95e10-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="95e10-105">Eenmaal in de opslag, kunnen deze worden bekeken met een van de verschillende beschikbare hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="95e10-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="95e10-106">Storage-account opgeven</span><span class="sxs-lookup"><span data-stu-id="95e10-106">Specify a storage account</span></span>
<span data-ttu-id="95e10-107">U opgeven het opslagaccount dat u wilt gebruiken in het bestand ServiceConfiguration.cscfg.</span><span class="sxs-lookup"><span data-stu-id="95e10-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="95e10-108">De accountgegevens wordt gedefinieerd als een verbindingsreeks in een configuratie-instelling.</span><span class="sxs-lookup"><span data-stu-id="95e10-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="95e10-109">Het volgende voorbeeld ziet u de standaardverbindingsreeks gemaakt voor een nieuwe Cloudservice-project in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="95e10-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="95e10-110">U kunt deze verbindingsreeks met account-informatie voor een Azure storage-account wijzigen.</span><span class="sxs-lookup"><span data-stu-id="95e10-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="95e10-111">Afhankelijk van het type diagnostische gegevens worden verzameld, maakt gebruik van Azure Diagnostics de Blob-service of de tabel-service.</span><span class="sxs-lookup"><span data-stu-id="95e10-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="95e10-112">De volgende tabel toont de gegevensbronnen die worden doorgevoerd en hun notatie.</span><span class="sxs-lookup"><span data-stu-id="95e10-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="95e10-113">Gegevensbron</span><span class="sxs-lookup"><span data-stu-id="95e10-113">Data source</span></span> | <span data-ttu-id="95e10-114">Opslagindeling</span><span class="sxs-lookup"><span data-stu-id="95e10-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="95e10-115">Azure-Logboeken</span><span class="sxs-lookup"><span data-stu-id="95e10-115">Azure logs</span></span> |<span data-ttu-id="95e10-116">Tabel</span><span class="sxs-lookup"><span data-stu-id="95e10-116">Table</span></span> |
| <span data-ttu-id="95e10-117">IIS 7.0-Logboeken</span><span class="sxs-lookup"><span data-stu-id="95e10-117">IIS 7.0 logs</span></span> |<span data-ttu-id="95e10-118">Blob</span><span class="sxs-lookup"><span data-stu-id="95e10-118">Blob</span></span> |
| <span data-ttu-id="95e10-119">Logboeken van Azure Diagnostics-infrastructuur</span><span class="sxs-lookup"><span data-stu-id="95e10-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="95e10-120">Tabel</span><span class="sxs-lookup"><span data-stu-id="95e10-120">Table</span></span> |
| <span data-ttu-id="95e10-121">Logboeken met traceringen aanvraag is mislukt</span><span class="sxs-lookup"><span data-stu-id="95e10-121">Failed Request Trace logs</span></span> |<span data-ttu-id="95e10-122">Blob</span><span class="sxs-lookup"><span data-stu-id="95e10-122">Blob</span></span> |
| <span data-ttu-id="95e10-123">Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="95e10-123">Windows Event logs</span></span> |<span data-ttu-id="95e10-124">Tabel</span><span class="sxs-lookup"><span data-stu-id="95e10-124">Table</span></span> |
| <span data-ttu-id="95e10-125">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="95e10-125">Performance counters</span></span> |<span data-ttu-id="95e10-126">Tabel</span><span class="sxs-lookup"><span data-stu-id="95e10-126">Table</span></span> |
| <span data-ttu-id="95e10-127">Crashdumps</span><span class="sxs-lookup"><span data-stu-id="95e10-127">Crash dumps</span></span> |<span data-ttu-id="95e10-128">Blob</span><span class="sxs-lookup"><span data-stu-id="95e10-128">Blob</span></span> |
| <span data-ttu-id="95e10-129">Aangepaste foutenlogboeken</span><span class="sxs-lookup"><span data-stu-id="95e10-129">Custom error logs</span></span> |<span data-ttu-id="95e10-130">Blob</span><span class="sxs-lookup"><span data-stu-id="95e10-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="95e10-131">Diagnostische gegevens overbrengen</span><span class="sxs-lookup"><span data-stu-id="95e10-131">Transfer diagnostic data</span></span>
<span data-ttu-id="95e10-132">Voor de SDK 2.5 of hoger, kan de aanvraag voor diagnostische gegevens overdragen via het configuratiebestand optreden.</span><span class="sxs-lookup"><span data-stu-id="95e10-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="95e10-133">U kunt diagnostische gegevens overbrengen met regelmatige tussenpozen zoals opgegeven in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="95e10-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="95e10-134">Voor SDK-2.4 en vorige kunt u de diagnostische gegevens als programmatisch overdragen via het configuratiebestand ook vragen.</span><span class="sxs-lookup"><span data-stu-id="95e10-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="95e10-135">De programmatische aanpak kunt u doen op aanvraag overdrachten.</span><span class="sxs-lookup"><span data-stu-id="95e10-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95e10-136">Wanneer u diagnostische gegevens naar Azure storage-account overdraagt, u kosten in rekening worden voor de storage-resources die gebruikmaakt van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="95e10-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="95e10-137">Diagnostische gegevens op te slaan</span><span class="sxs-lookup"><span data-stu-id="95e10-137">Store diagnostic data</span></span>
<span data-ttu-id="95e10-138">Logboekgegevens worden opgeslagen in Blob of Table storage met de volgende namen:</span><span class="sxs-lookup"><span data-stu-id="95e10-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="95e10-139">**Tabellen**</span><span class="sxs-lookup"><span data-stu-id="95e10-139">**Tables**</span></span>

* <span data-ttu-id="95e10-140">**WadLogsTable** - Logboeken geschreven in code met behulp van de traceringslistener.</span><span class="sxs-lookup"><span data-stu-id="95e10-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="95e10-141">**WADDiagnosticInfrastructureLogsTable** -diagnostische monitor en configuratie van wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="95e10-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="95e10-142">**WADDirectoriesTable** – mappen die wordt bewaakt door de diagnostische monitor.</span><span class="sxs-lookup"><span data-stu-id="95e10-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="95e10-143">Dit omvat IIS-logboeken, IIS kan niet logboeken aanvragen en aangepaste mappen.</span><span class="sxs-lookup"><span data-stu-id="95e10-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="95e10-144">De locatie van het logboekbestand van de blob is opgegeven in het veld Container en de naam van de blob is in het veld RelativePath.</span><span class="sxs-lookup"><span data-stu-id="95e10-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="95e10-145">Het veld AbsolutePath geeft de locatie en de naam van het bestand zoals deze waren aanwezig op de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="95e10-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="95e10-146">**WADPerformanceCountersTable** – prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="95e10-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="95e10-147">**WADWindowsEventLogsTable** – Windows-gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="95e10-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="95e10-148">**Blobs**</span><span class="sxs-lookup"><span data-stu-id="95e10-148">**Blobs**</span></span>

* <span data-ttu-id="95e10-149">**af-besturingselement-container** – (alleen voor SDK-2.4 en vorige) bevat de XML-configuratiebestanden die bepaalt van Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="95e10-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="95e10-150">**af-iis-failedreqlogfiles** – bevat gegevens uit logboeken IIS aanvragen is mislukt.</span><span class="sxs-lookup"><span data-stu-id="95e10-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="95e10-151">**af-iis-logboekbestanden** : bevat informatie over IIS-logboeken.</span><span class="sxs-lookup"><span data-stu-id="95e10-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="95e10-152">**'aangepaste'** – op basis van een aangepaste container over het configureren van mappen die worden bewaakt door de diagnostische monitor.</span><span class="sxs-lookup"><span data-stu-id="95e10-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="95e10-153">De naam van deze blob-container wordt in WADDirectoriesTable worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="95e10-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="95e10-154">Hulpprogramma's om diagnostische gegevens weer te geven</span><span class="sxs-lookup"><span data-stu-id="95e10-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="95e10-155">Er zijn verschillende hulpprogramma's beschikbaar zijn voor het weergeven van de gegevens nadat deze zijn overgebracht naar de opslag.</span><span class="sxs-lookup"><span data-stu-id="95e10-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="95e10-156">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="95e10-156">For example:</span></span>

* <span data-ttu-id="95e10-157">Server Explorer in Visual Studio - als u de hulpprogramma's Azure hebt geïnstalleerd voor Microsoft Visual Studio, kunt u het Azure Storage-knooppunt in Server Explorer blob voor alleen-lezen en tabelgegevens weergeven van uw Azure storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="95e10-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="95e10-158">U kunt gegevens weergeven vanuit uw lokale opslagaccount voor de emulator en ook van storage-accounts u hebt gemaakt voor Azure.</span><span class="sxs-lookup"><span data-stu-id="95e10-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="95e10-159">Zie voor meer informatie [surfen en het beheren van opslagbronnen met Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="95e10-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="95e10-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app waardoor u eenvoudig werken met Azure Storage-gegevens op Windows, OSX en Linux.</span><span class="sxs-lookup"><span data-stu-id="95e10-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="95e10-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) bevat Azure Diagnostics Manager zodat u kunt bekijken, downloaden en beheren van de diagnostische gegevens verzameld door de toepassingen die worden uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="95e10-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95e10-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95e10-162">Next Steps</span></span>
[<span data-ttu-id="95e10-163">De stroom in een Cloud Services-toepassing met Azure Diagnostics traceren</span><span class="sxs-lookup"><span data-stu-id="95e10-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

