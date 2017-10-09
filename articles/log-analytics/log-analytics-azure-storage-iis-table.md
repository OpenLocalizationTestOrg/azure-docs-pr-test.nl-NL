---
title: aaaUse blob storage voor IIS en tabel opslag voor gebeurtenissen in de Azure Log Analytics | Microsoft Docs
description: Log Analytics kunt lezen Hallo-logboeken voor Azure-services die diagnostics tootable opslag schrijven of IIS-logboeken geschreven tooblob opslag.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="11086-103">Azure blob storage gebruiken voor IIS en Azure-tabelopslag voor gebeurtenissen met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="11086-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="11086-104">Log Analytics kunt lezen Hallo-logboeken voor Hallo services die schrijven diagnostics tootable opslag of IIS-logboeken geschreven tooblob opslag te volgen:</span><span class="sxs-lookup"><span data-stu-id="11086-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="11086-105">Service Fabric-clusters (Preview)</span><span class="sxs-lookup"><span data-stu-id="11086-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="11086-106">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="11086-106">Virtual Machines</span></span>
* <span data-ttu-id="11086-107">Web/werkrollen</span><span class="sxs-lookup"><span data-stu-id="11086-107">Web/Worker Roles</span></span>

<span data-ttu-id="11086-108">Voordat u Log Analytics kunt verzamelen van gegevens voor deze bronnen, kan Azure diagnostics moet zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11086-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="11086-109">Als diagnostische gegevens zijn ingeschakeld, kunt u hello Azure-portal of PowerShell logboekanalyse toocollect Hallo logboeken configureren.</span><span class="sxs-lookup"><span data-stu-id="11086-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="11086-110">Azure Diagnostics is een Azure-uitbreiding waarmee u toocollect diagnostische gegevens van een werkrol, Webrol of virtuele machine in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11086-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="11086-111">Hallo-gegevens worden opgeslagen in Azure storage-account en vervolgens kan worden verzameld door Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="11086-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="11086-112">Voor logboekanalyse toocollect deze logboeken Azure Diagnostics Hallo logboeken moet in de volgende locaties Hallo:</span><span class="sxs-lookup"><span data-stu-id="11086-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="11086-113">Logboektype</span><span class="sxs-lookup"><span data-stu-id="11086-113">Log Type</span></span> | <span data-ttu-id="11086-114">Resourcetype</span><span class="sxs-lookup"><span data-stu-id="11086-114">Resource Type</span></span> | <span data-ttu-id="11086-115">Locatie</span><span class="sxs-lookup"><span data-stu-id="11086-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11086-116">IIS-logboeken</span><span class="sxs-lookup"><span data-stu-id="11086-116">IIS logs</span></span> |<span data-ttu-id="11086-117">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="11086-117">Virtual Machines</span></span> <br> <span data-ttu-id="11086-118">Web-rollen</span><span class="sxs-lookup"><span data-stu-id="11086-118">Web roles</span></span> <br> <span data-ttu-id="11086-119">Werkrollen</span><span class="sxs-lookup"><span data-stu-id="11086-119">Worker roles</span></span> |<span data-ttu-id="11086-120">af-iis-logboekbestanden (Blob-opslag)</span><span class="sxs-lookup"><span data-stu-id="11086-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="11086-121">Syslog</span><span class="sxs-lookup"><span data-stu-id="11086-121">Syslog</span></span> |<span data-ttu-id="11086-122">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="11086-122">Virtual Machines</span></span> |<span data-ttu-id="11086-123">LinuxsyslogVer2v0 (tabel opslag)</span><span class="sxs-lookup"><span data-stu-id="11086-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="11086-124">Operationele gebeurtenissen van de service Fabric</span><span class="sxs-lookup"><span data-stu-id="11086-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="11086-125">Service Fabric-knooppunten</span><span class="sxs-lookup"><span data-stu-id="11086-125">Service Fabric nodes</span></span> |<span data-ttu-id="11086-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="11086-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="11086-127">Gebeurtenissen van de service Fabric betrouwbare Actor</span><span class="sxs-lookup"><span data-stu-id="11086-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="11086-128">Service Fabric-knooppunten</span><span class="sxs-lookup"><span data-stu-id="11086-128">Service Fabric nodes</span></span> |<span data-ttu-id="11086-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="11086-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="11086-130">Gebeurtenissen van betrouwbare Service voor service Fabric</span><span class="sxs-lookup"><span data-stu-id="11086-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="11086-131">Service Fabric-knooppunten</span><span class="sxs-lookup"><span data-stu-id="11086-131">Service Fabric nodes</span></span> |<span data-ttu-id="11086-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="11086-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="11086-133">Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="11086-133">Windows Event logs</span></span> |<span data-ttu-id="11086-134">Service Fabric-knooppunten</span><span class="sxs-lookup"><span data-stu-id="11086-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="11086-135">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="11086-135">Virtual Machines</span></span> <br> <span data-ttu-id="11086-136">Web-rollen</span><span class="sxs-lookup"><span data-stu-id="11086-136">Web roles</span></span> <br> <span data-ttu-id="11086-137">Werkrollen</span><span class="sxs-lookup"><span data-stu-id="11086-137">Worker roles</span></span> |<span data-ttu-id="11086-138">WADWindowsEventLogsTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="11086-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="11086-139">Logboeken van Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="11086-139">Windows ETW logs</span></span> |<span data-ttu-id="11086-140">Service Fabric-knooppunten</span><span class="sxs-lookup"><span data-stu-id="11086-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="11086-141">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="11086-141">Virtual Machines</span></span> <br> <span data-ttu-id="11086-142">Web-rollen</span><span class="sxs-lookup"><span data-stu-id="11086-142">Web roles</span></span> <br> <span data-ttu-id="11086-143">Werkrollen</span><span class="sxs-lookup"><span data-stu-id="11086-143">Worker roles</span></span> |<span data-ttu-id="11086-144">WADETWEventTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="11086-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="11086-145">IIS-logboeken van Azure Websites worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="11086-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="11086-146">Voor virtuele machines die u hebt de optie Hallo Hallo installeren [logboekanalyse agent](log-analytics-azure-vm-extension.md) in uw virtuele machine tooenable extra inzichten.</span><span class="sxs-lookup"><span data-stu-id="11086-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="11086-147">Bovendien kunt u aanvullende analyse, waaronder configuratie bijhouden, SQL-evaluatie en update-evaluatie uitvoeren toobeing kunnen tooanalyze IIS-logboeken en gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="11086-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="11086-148">Inschakelen van Azure diagnostics in een virtuele machine voor het logboek met systeemgebeurtenissen en IIS Meld verzameling</span><span class="sxs-lookup"><span data-stu-id="11086-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="11086-149">Gebruik hello te volgen procedure tooenable Azure diagnostics in een virtuele machine voor het logboek met systeemgebeurtenissen en IIS Meld u met behulp van Microsoft Azure-portal Hallo verzameling.</span><span class="sxs-lookup"><span data-stu-id="11086-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="11086-150">tooenable Azure diagnostische gegevens in een virtuele machine met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="11086-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="11086-151">Hallo VM-Agent installeren wanneer u een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="11086-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="11086-152">Als Hallo virtuele machine al bestaat, controleert u dat Hallo die VM-Agent is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="11086-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="11086-153">In hello Azure-portal, gaat u toohello virtuele machine, selecteert u **optionele configuratie**, klikt u vervolgens **Diagnostics** en stel **Status** te**op**.</span><span class="sxs-lookup"><span data-stu-id="11086-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="11086-154">Na voltooiing heeft Hallo VM hello Azure Diagnostics extensie geïnstalleerd en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11086-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="11086-155">Deze uitbreiding is verantwoordelijk voor het verzamelen van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11086-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="11086-156">Controle inschakelen en configureren van logboekregistratie in een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="11086-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="11086-157">U kunt diagnostische gegevens op Hallo VM-niveau inschakelen.</span><span class="sxs-lookup"><span data-stu-id="11086-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="11086-158">tooenable diagnostische gegevens en configureer vervolgens de logboekregistratie van gebeurtenissen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11086-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="11086-159">Selecteer Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="11086-159">Select hello VM.</span></span>
   2. <span data-ttu-id="11086-160">Klik op **bewaking**.</span><span class="sxs-lookup"><span data-stu-id="11086-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="11086-161">Klik op **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="11086-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="11086-162">Set Hallo **Status** te**ON**.</span><span class="sxs-lookup"><span data-stu-id="11086-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="11086-163">Selecteer elk diagnostics logboek dat u wilt dat toocollect.</span><span class="sxs-lookup"><span data-stu-id="11086-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="11086-164">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="11086-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="11086-165">Inschakelen van Azure diagnostics in een Webrol voor IIS-logboek en gebeurtenis-verzameling</span><span class="sxs-lookup"><span data-stu-id="11086-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="11086-166">Raadpleeg te[hoe diagnostische gegevens in een Cloudservice tooEnable](../cloud-services/cloud-services-dotnet-diagnostics.md) voor algemene stappen over het inschakelen van Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="11086-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="11086-167">Hallo onderstaande instructies deze gegevens gebruiken en aanpassen voor gebruik met logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="11086-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="11086-168">Met Azure diagnostics ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="11086-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="11086-169">IIS-logboeken worden standaard opgeslagen met logboekgegevens op Hallo scheduledTransferPeriod overdrachtsinterval overgedragen.</span><span class="sxs-lookup"><span data-stu-id="11086-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="11086-170">Windows-gebeurtenislogboeken worden standaard niet worden overgedragen.</span><span class="sxs-lookup"><span data-stu-id="11086-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="11086-171">tooenable diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="11086-171">tooenable diagnostics</span></span>
<span data-ttu-id="11086-172">Windows-gebeurtenislogboeken tooenable of toochange Hallo scheduledTransferPeriod, configureren van Azure Diagnostics Hallo XML-configuratiebestand (diagnostics.wadcfg), zoals wordt weergegeven in [stap 4: maken van uw configuratiebestand diagnostische gegevens en Hallo installeren de extensie](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="11086-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="11086-173">Hallo verzamelt volgende voorbeeldconfiguratiebestand IIS-logboeken en alle gebeurtenissen van Hallo toepassing en het systeemlogboek in Logboeken:</span><span class="sxs-lookup"><span data-stu-id="11086-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="11086-174">Zorg ervoor dat uw ConfigurationSettings geeft u een opslagaccount, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="11086-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="11086-175">Hallo **AccountName** en **AccountKey** waarden zijn gevonden in hello Azure-portal op Hallo storage account dashboard onder toegangssleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="11086-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="11086-176">Hallo-protocol voor het Hallo-verbindingsreeks moet **https**.</span><span class="sxs-lookup"><span data-stu-id="11086-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="11086-177">Nadat bijgewerkte diagnostische configuratie Hallo is toegepast wordt tooyour cloudservice en het geschreven diagnostics tooAzure opslag, en u bent klaar tooconfigure logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="11086-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="11086-178">Hello Azure portal toocollect logboeken van Azure Storage gebruiken</span><span class="sxs-lookup"><span data-stu-id="11086-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="11086-179">U kunt hello Azure portal tooconfigure logboekanalyse toocollect Hallo Logboeken kunt gebruiken voor hello Azure-services te volgen:</span><span class="sxs-lookup"><span data-stu-id="11086-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="11086-180">Service Fabric-clusters</span><span class="sxs-lookup"><span data-stu-id="11086-180">Service Fabric clusters</span></span>
* <span data-ttu-id="11086-181">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="11086-181">Virtual Machines</span></span>
* <span data-ttu-id="11086-182">Web/werkrollen</span><span class="sxs-lookup"><span data-stu-id="11086-182">Web/Worker Roles</span></span>

<span data-ttu-id="11086-183">Werkruimte voor logboekanalyse tooyour navigeren in hello Azure-portal, en Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="11086-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="11086-184">Klik op *opslagaccounts Logboeken*</span><span class="sxs-lookup"><span data-stu-id="11086-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="11086-185">Klik op Hallo *toevoegen* taak</span><span class="sxs-lookup"><span data-stu-id="11086-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="11086-186">Selecteer Hallo opslagaccount waarin Hallo diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="11086-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="11086-187">Dit account kan worden een klassieke storage-account of een Azure Resource Manager-storage-account</span><span class="sxs-lookup"><span data-stu-id="11086-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="11086-188">Selecteer Hallo gewenste toocollect logboeken voor gegevenstype</span><span class="sxs-lookup"><span data-stu-id="11086-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="11086-189">Hallo-opties zijn IIS-logboeken; Gebeurtenissen; Syslog (Linux); ETW-Logboeken; Service Fabric-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="11086-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="11086-190">Hallo-waarde voor de gegevensbron wordt automatisch ingevuld op basis van Hallo gegevenstype en kan niet worden gewijzigd</span><span class="sxs-lookup"><span data-stu-id="11086-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="11086-191">Klik op OK toosave Hallo configuratie</span><span class="sxs-lookup"><span data-stu-id="11086-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="11086-192">Herhaal stappen 2 tot en met 6 voor extra opslagruimte accounts en gegevenstypen die u wilt dat Log Analytics toocollect.</span><span class="sxs-lookup"><span data-stu-id="11086-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="11086-193">U bent kunnen toosee gegevens van Hallo storage-account in logboekanalyse in ongeveer 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="11086-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="11086-194">U ziet alleen de gegevens die worden geschreven toostorage nadat Hallo-configuratie is toegepast.</span><span class="sxs-lookup"><span data-stu-id="11086-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="11086-195">Log Analytics biedt Hallo bestaande gegevens niet lezen uit Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="11086-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="11086-196">Hallo portal die Hallo-bron in Hallo storage-account bestaat niet valideren of als er nieuwe gegevens worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="11086-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="11086-197">Inschakelen van Azure diagnostics in een virtuele machine voor het logboek met systeemgebeurtenissen en IIS Meld verzameling met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="11086-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="11086-198">Gebruik Hallo stappen in [tooindex logboekanalyse configureren van Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread van Azure diagnostics die tootable opslag zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="11086-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="11086-199">Met Azure PowerShell kunt u preciezer Hallo gebeurtenissen opgeven die tooAzure opslag zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="11086-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="11086-200">Zie voor meer informatie [Diagnostics inschakelen in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="11086-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="11086-201">U kunt inschakelen en Azure diagnostics met behulp van de volgende PowerShell-script Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="11086-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="11086-202">U kunt dit script ook gebruiken met een aangepaste configuratie voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="11086-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="11086-203">Hallo script tooset Hallo storage-account, servicenaam en de naam van de virtuele machine wijzigen.</span><span class="sxs-lookup"><span data-stu-id="11086-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="11086-204">Hallo script maakt gebruik van cmdlets voor klassieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="11086-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="11086-205">Hallo volgende voorbeeldscript bekijken, kopieert u deze zo nodig wijzigen, Hallo voorbeeld opslaan als een PowerShell-scriptbestand en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="11086-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="11086-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11086-206">Next steps</span></span>
* <span data-ttu-id="11086-207">[Verzamelen van Logboeken en metrische gegevens voor Azure-services](log-analytics-azure-storage.md) voor ondersteunde Azure-services.</span><span class="sxs-lookup"><span data-stu-id="11086-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="11086-208">[Inschakelen van oplossingen](log-analytics-add-solutions.md) tooprovide inzicht in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="11086-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="11086-209">[Gebruik zoekquery's](log-analytics-log-searches.md) tooanalyze Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="11086-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
