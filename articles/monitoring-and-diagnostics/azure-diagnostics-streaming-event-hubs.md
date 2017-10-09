---
title: aaaStreaming Azure Diagnostics-gegevens in de hot pad Hallo met Event Hubs | Microsoft Docs
description: Configureren van Azure Diagnostics met Event Hubs eindigen tooend, met inbegrip van de richtlijnen voor veelvoorkomende scenario's.
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="e8a49-103">Azure Diagnostics-gegevens in de hot pad Hallo streaming met behulp van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e8a49-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="e8a49-104">Azure Diagnostics biedt flexibele manieren toocollect metrische gegevens en registreert van cloud services virtuele machines (VM's) en het overdragen van resultaten tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="e8a49-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="e8a49-105">Vanaf tijdsbestek van Hallo maart 2016 (SDK 2.9), kunt u toocustom diagnostische gegevens verzenden gegevensbronnen en gegevensoverdracht hot pad (in seconden) met behulp van [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="e8a49-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="e8a49-106">Ondersteunde gegevenstypen zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="e8a49-106">Supported data types include:</span></span>

* <span data-ttu-id="e8a49-107">ETW-gebeurtenissen (Event Tracing for Windows)</span><span class="sxs-lookup"><span data-stu-id="e8a49-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="e8a49-108">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="e8a49-108">Performance counters</span></span>
* <span data-ttu-id="e8a49-109">Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="e8a49-109">Windows event logs</span></span>
* <span data-ttu-id="e8a49-110">Toepassingslogboeken</span><span class="sxs-lookup"><span data-stu-id="e8a49-110">Application logs</span></span>
* <span data-ttu-id="e8a49-111">Logboeken van Azure Diagnostics-infrastructuur</span><span class="sxs-lookup"><span data-stu-id="e8a49-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="e8a49-112">Dit artikel laat zien hoe Azure Diagnostics tooconfigure met Event Hubs van tooend eindigen.</span><span class="sxs-lookup"><span data-stu-id="e8a49-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="e8a49-113">Ook richtlijnen gegeven voor Hallo algemene scenario's te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8a49-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="e8a49-114">Hoe toocustomize Hallo registreert en metrische gegevens die tooEvent Hubs wordt verzonden</span><span class="sxs-lookup"><span data-stu-id="e8a49-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="e8a49-115">Hoe toochange configuraties in elke omgeving</span><span class="sxs-lookup"><span data-stu-id="e8a49-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="e8a49-116">Hoe de gegevens voor het streamen van tooview Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e8a49-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="e8a49-117">Hoe tootroubleshoot Hallo verbinding</span><span class="sxs-lookup"><span data-stu-id="e8a49-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="e8a49-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e8a49-118">Prerequisites</span></span>
<span data-ttu-id="e8a49-119">Event Hubs receieving gegevens van Azure Diagnostics wordt ondersteund in Cloudservices, virtuele machines, virtuele-Machineschaalsets en Service Fabric vanaf hello Azure SDK 2.9 en hello Azure Tools voor Visual Studio overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="e8a49-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="e8a49-120">Azure Diagnostics-extensie 1.6 ([Azure SDK voor .NET 2.9 of hoger](https://azure.microsoft.com/downloads/) gericht is op dit standaard)</span><span class="sxs-lookup"><span data-stu-id="e8a49-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="e8a49-121">Visual Studio 2013 of hoger</span><span class="sxs-lookup"><span data-stu-id="e8a49-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="e8a49-122">Bestaande configuraties van Azure Diagnostics in een toepassing met behulp van een *.wadcfgx* bestands- en een van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="e8a49-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="e8a49-123">Visual Studio: [diagnostische gegevens configureren voor Azure-Cloudservices en virtuele Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="e8a49-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="e8a49-124">Windows PowerShell: [diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e8a49-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="e8a49-125">Event Hubs naamruimte is ingericht per Hallo-artikel [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="e8a49-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="e8a49-126">Verbinding maken met Azure Diagnostics tooEvent Hubs sink</span><span class="sxs-lookup"><span data-stu-id="e8a49-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="e8a49-127">Standaard stuurt Azure Diagnostics altijd logboeken en metrische gegevens tooan Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8a49-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="e8a49-128">Een toepassing mogelijk gegevens tooEvent Hubs verzonden door het toevoegen van een nieuwe **Sinks** sectie onder Hallo **PublicConfig** / **WadCfg** element Hallo *.wadcfgx* bestand.</span><span class="sxs-lookup"><span data-stu-id="e8a49-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="e8a49-129">In Visual Studio Hallo *.wadcfgx* bestand wordt opgeslagen in in het pad naar Hallo: **Cloudserviceproject** > **rollen** > **() RoleName)** > **diagnostics.wadcfgx** bestand.</span><span class="sxs-lookup"><span data-stu-id="e8a49-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="e8a49-130">In dit voorbeeld Hallo event hub-URL is ingesteld toohello volledig gekwalificeerd naamruimte van Hallo event hub: Event Hubs naamruimte + "/" + naam event hub.</span><span class="sxs-lookup"><span data-stu-id="e8a49-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="e8a49-131">Hallo event hub-URL wordt weergegeven in Hallo [Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885) op Hallo Event Hubs-dashboard.</span><span class="sxs-lookup"><span data-stu-id="e8a49-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="e8a49-132">Hallo **Sink** naam kan tooany geldige tekenreeks worden ingesteld als hello dezelfde waarde wordt gebruikt consistent in Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="e8a49-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a49-133">Mogelijk zijn er extra Put, zoals *applicationInsights* geconfigureerd in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e8a49-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="e8a49-134">Azure Diagnostics kan een of meer toobe gedefinieerd als elke sink is ook gedeclareerd in het Hallo-sinks **PrivateConfig** sectie.</span><span class="sxs-lookup"><span data-stu-id="e8a49-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="e8a49-135">Hallo Event Hubs sink moet ook worden gedeclareerd en gedefinieerd in Hallo **PrivateConfig** sectie Hallo *.wadcfgx* config-bestand.</span><span class="sxs-lookup"><span data-stu-id="e8a49-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="e8a49-136">Hallo `SharedAccessKeyName` waarde moet overeenkomen met een Shared Access Signature (SAS)-sleutel en het beleid dat is gedefinieerd in Hallo **Event Hubs** naamruimte.</span><span class="sxs-lookup"><span data-stu-id="e8a49-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="e8a49-137">Blader toohello Event Hubs dashboard in Hallo [Azure-portal](https://manage.windowsazure.com), klikt u op Hallo **configureren** tabblad en instellen van een benoemde beleid (bijvoorbeeld ' SendRule') is *verzenden* machtigingen.</span><span class="sxs-lookup"><span data-stu-id="e8a49-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="e8a49-138">Hallo **StorageAccount** ook is gedeclareerd in **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="e8a49-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="e8a49-139">Hoeft niet hier toochange waarden als ze werken.</span><span class="sxs-lookup"><span data-stu-id="e8a49-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="e8a49-140">In dit voorbeeld laat we Hallo waarden leeg, dit is een teken dat een downstream asset Hallo waarden worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e8a49-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="e8a49-141">Bijvoorbeeld, Hallo *ServiceConfiguration.Cloud.cscfg* omgeving configuratiebestand stelt Hallo omgeving passende namen en -sleutels.</span><span class="sxs-lookup"><span data-stu-id="e8a49-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="e8a49-142">Hallo Event Hubs SAS-sleutel wordt opgeslagen als tekst zonder opmaak in Hallo *.wadcfgx* bestand.</span><span class="sxs-lookup"><span data-stu-id="e8a49-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="e8a49-143">Deze sleutel wordt vaak toosource code controle is ingeschakeld of is beschikbaar als een activum in uw buildserver, zodat u deze naar gelang van toepassing moet beschermen.</span><span class="sxs-lookup"><span data-stu-id="e8a49-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="e8a49-144">Het is raadzaam dat u een SAS-sleutel hier met *alleen verzenden* machtigingen zodat een kwaadwillende gebruiker kunt toohello event hub schrijven, maar die niet worden tooit luisteren of beheren.</span><span class="sxs-lookup"><span data-stu-id="e8a49-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="e8a49-145">Configureren van Azure Diagnostics toosend logboeken en metrische gegevens tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="e8a49-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="e8a49-146">Zoals eerder, besproken alle standaard en aangepaste diagnostics-gegevens, dat wil zeggen, wordt metrische gegevens en zich aanmeldt, automatisch verzonden tooAzure opslag met intervallen van Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e8a49-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="e8a49-147">Met Event Hubs en eventuele aanvullende sink, kunt u een basis- of leaf-knooppunt in Hallo hiërarchie toobe toohello event hub wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="e8a49-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="e8a49-148">Dit omvat ETW-gebeurtenissen, prestatiemeteritems, Windows-gebeurtenislogboeken en toepassingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="e8a49-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="e8a49-149">Het is belangrijk tooconsider hoeveel gegevenspunten daadwerkelijk moeten worden overgedragen tooEvent Hubs.</span><span class="sxs-lookup"><span data-stu-id="e8a49-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="e8a49-150">Normaal gesproken ontwikkelaars gegevensoverdracht lage latentie hot pad die moet worden gebruikt en geïnterpreteerd snel.</span><span class="sxs-lookup"><span data-stu-id="e8a49-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="e8a49-151">Systemen die waarschuwingen of regels voor automatisch schalen bewaken zijn voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e8a49-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="e8a49-152">Een ontwikkelaar kan ook een alternatieve analyse store configureren of zoek store--bijvoorbeeld Azure Stream Analytics, Elasticsearch, een aangepaste bewakingssysteem of een favoriete bewakingssysteem van andere regels.</span><span class="sxs-lookup"><span data-stu-id="e8a49-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="e8a49-153">Hallo hieronder vindt u enkele voorbeeldconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="e8a49-153">hello following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="e8a49-154">Hallo sink is Hallo hierboven voorbeeld, toegepaste toohello bovenliggende **PerformanceCounters** knooppunt in de hiërarchie hello, wat betekent alle onderliggende dat **PerformanceCounters** tooEvent Hubs worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="e8a49-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="e8a49-155">In het vorige voorbeeld hello, Hallo sink is drie prestatiemeteritems toegepaste tooonly: **aanvragen in wachtrij**, **aanvragen afgewezen**, en **percentage processortijd**.</span><span class="sxs-lookup"><span data-stu-id="e8a49-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="e8a49-156">Hallo volgende voorbeeld ziet u hoe een ontwikkelaar Hallo hoeveelheid verzonden gegevens toobe Hallo belangrijke metrische gegevens die worden gebruikt voor deze service health kunt beperken.</span><span class="sxs-lookup"><span data-stu-id="e8a49-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="e8a49-157">In dit voorbeeld Hallo sink is toegepaste toologs en gefilterde alleen tooerror serviceniveau traceren.</span><span class="sxs-lookup"><span data-stu-id="e8a49-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="e8a49-158">Implementeren en bijwerken van een Cloud Services-toepassing en diagnostische configuratie</span><span class="sxs-lookup"><span data-stu-id="e8a49-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="e8a49-159">Visual Studio biedt Hallo eenvoudigste pad toodeploy Hallo toepassing en configuratie van Event Hubs sink.</span><span class="sxs-lookup"><span data-stu-id="e8a49-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="e8a49-160">tooview en bewerk Hallo-bestand, open Hallo *.wadcfgx* bestand in Visual Studio, bewerken en opslaan.</span><span class="sxs-lookup"><span data-stu-id="e8a49-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="e8a49-161">Hallo-pad is **Cloudserviceproject** > **rollen** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="e8a49-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="e8a49-162">Op dit punt alle implementatie en implementatie bijwerken acties in Visual Studio, Visual Studio Team System en alle opdrachten of scripts die zijn gebaseerd op MSBuild en gebruik Hallo **/t: publiceren** doel omvatten Hallo *.wadcfgx*  in Hallo verpakking proces.</span><span class="sxs-lookup"><span data-stu-id="e8a49-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="e8a49-163">Bovendien implementeren implementaties en -updates Hallo bestand tooAzure met Hallo juiste Azure Diagnostics agentextensie op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e8a49-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="e8a49-164">Nadat u de toepassing hello en configuratie van diagnostische Azure implementeert, ziet u meteen activiteit in het dashboard Hallo van Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="e8a49-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="e8a49-165">Hiermee wordt aangegeven dat u klaar toomove op tooviewing Hallo hot pad gegevens in Hallo-listener-client of analyse hulpprogramma van uw keuze bent.</span><span class="sxs-lookup"><span data-stu-id="e8a49-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="e8a49-166">In Hallo volgende afbeelding, toont Hallo Event Hubs dashboard in orde verzending van diagnostische gegevens toohello event hub gestart ergens na 23: 00 uur.</span><span class="sxs-lookup"><span data-stu-id="e8a49-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="e8a49-167">Als Hallo toepassing werd geïmplementeerd met een bijgewerkte *.wadcfgx* -bestand en Hallo sink correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e8a49-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="e8a49-168">Wanneer u updates toohello Azure Diagnostics-configuratiebestand (.wadcfgx), verdient het aanbeveling Hallo updates toohello volledige toepassing, evenals Hallo configuratie te pushen met behulp van Visual Studio publiceren of een Windows PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="e8a49-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="e8a49-169">Gegevens in de hot pad</span><span class="sxs-lookup"><span data-stu-id="e8a49-169">View hot-path data</span></span>
<span data-ttu-id="e8a49-170">Zoals eerder besproken, zijn er veel gebruiksvoorbeelden voor luisteren tooand verwerken van Event Hubs-gegevens.</span><span class="sxs-lookup"><span data-stu-id="e8a49-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="e8a49-171">Een eenvoudige aanpak is toocreate een kleine test console toepassing toolisten toohello event hub en afdrukken Hallo uitvoerstroom.</span><span class="sxs-lookup"><span data-stu-id="e8a49-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="e8a49-172">U kunt plaatsen Hallo code, die wordt meer gedetailleerd uitgelegd in volgende [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="e8a49-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="e8a49-173">Opmerking Hallo consoletoepassing vergezeld Hallo [Event Processor Host NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="e8a49-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="e8a49-174">Houd er rekening mee tooreplace Hallo waarden punthaken in Hallo **Main** functie met waarden voor uw resources.</span><span class="sxs-lookup"><span data-stu-id="e8a49-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="e8a49-175">Event Hubs put oplossen</span><span class="sxs-lookup"><span data-stu-id="e8a49-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="e8a49-176">Hallo event hub wordt niet weergegeven voor binnenkomende of uitgaande gebeurtenisactiviteit zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="e8a49-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="e8a49-177">Controleer of uw event hub met succes is ingericht.</span><span class="sxs-lookup"><span data-stu-id="e8a49-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="e8a49-178">Alle verbindingsgegevens in Hallo **PrivateConfig** sectie van *.wadcfgx* moet overeenkomen met Hallo waarden van de bron, zoals gezien in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="e8a49-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="e8a49-179">Zorg ervoor dat u een SAS-beleid gedefinieerd ('SendRule' in hello voorbeeld) in de portal Hallo en die hebt *verzenden* machtiging is verleend.</span><span class="sxs-lookup"><span data-stu-id="e8a49-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="e8a49-180">Na een update bevat Hallo event hub niet langer binnenkomende of uitgaande activiteit.</span><span class="sxs-lookup"><span data-stu-id="e8a49-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="e8a49-181">Controleer eerst of deze Hallo event hub en informatie over de configuratie is juist zijn, zoals hierboven is uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="e8a49-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="e8a49-182">Soms Hallo **PrivateConfig** opnieuw is ingesteld in een implementatie-update.</span><span class="sxs-lookup"><span data-stu-id="e8a49-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="e8a49-183">Hallo aanbevolen oplossing is toomake alle wijzigingen te*.wadcfgx* in project Hallo en vervolgens een update van de volledige toepassing push.</span><span class="sxs-lookup"><span data-stu-id="e8a49-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="e8a49-184">Als dit niet mogelijk is, zorgt u ervoor dat Hallo diagnostische gegevens van de update een complete pushes **PrivateConfig** die Hallo SAS-sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="e8a49-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="e8a49-185">Ik probeerde Hallo suggesties en Hallo event hub is nog steeds niet werkt.</span><span class="sxs-lookup"><span data-stu-id="e8a49-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="e8a49-186">Kijk in hello Azure Storage tabel met Logboeken en fouten voor Azure Diagnostics zelf: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="e8a49-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="e8a49-187">Een optie toouse is een hulpprogramma zoals [Azure Opslagverkenner](http://www.storageexplorer.com) tooconnect toothis storage-account, deze tabel weergeven en toevoegen van een query voor het tijdstempel in Hallo afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="e8a49-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="e8a49-188">U kunt gebruiken Hallo hulpprogramma tooexport een CSV-bestand en open het in een toepassing zoals Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="e8a49-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="e8a49-189">Excel kunt u eenvoudig toosearch voor tekenreeksen kaart, zoals **EventHubs**, toosee welke fout wordt gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="e8a49-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e8a49-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8a49-190">Next steps</span></span>
<span data-ttu-id="e8a49-191">• [Meer informatie over Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="e8a49-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="e8a49-192">Bijlage: Azure Diagnostics (.wadcfgx) voorbeeldconfiguratiebestand voltooien</span><span class="sxs-lookup"><span data-stu-id="e8a49-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="e8a49-193">Hallo aanvullende *ServiceConfiguration.Cloud.cscfg* voor dit voorbeeld ziet als Hallo volgende eruit.</span><span class="sxs-lookup"><span data-stu-id="e8a49-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="e8a49-194">Equivalente Json op basis van instellingen voor virtuele machines is als volgt:</span><span class="sxs-lookup"><span data-stu-id="e8a49-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="e8a49-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8a49-195">Next steps</span></span>
<span data-ttu-id="e8a49-196">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8a49-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="e8a49-197">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="e8a49-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e8a49-198">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="e8a49-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="e8a49-199">Veelgestelde vragen over Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e8a49-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
