---
title: aaaConfigure Azure Diagnostics toosend gegevens tooApplication Insights | Microsoft Docs
description: Hello Azure Diagnostics openbare configuratie toosend gegevens tooApplication Insights bijwerken.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="d5779-103">Cloud-Service, virtuele Machine of Service Fabric diagnostische gegevens tooApplication Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="d5779-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="d5779-104">Cloudservices, virtuele Machines, virtuele-Machineschaalsets en Service Fabric alle hello Azure Diagnostics extensie toocollect gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5779-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="d5779-105">Azure diagnostics verzendt gegevens tooAzure Storage-tabellen.</span><span class="sxs-lookup"><span data-stu-id="d5779-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="d5779-106">U kunt echter ook alle pipe of een subset van Hallo tooother gegevenslocaties met behulp van Azure Diagnostics extensie 1.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d5779-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="d5779-107">Dit artikel wordt beschreven hoe toosend gegevens van Azure Diagnostics extensie tooApplication Insights Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5779-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="d5779-108">Configuratie van diagnostische uitgelegd</span><span class="sxs-lookup"><span data-stu-id="d5779-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="d5779-109">Hello Azure diagnostics extensie 1.5 geïntroduceerd put zijn extra locaties waar u diagnostische gegevens kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="d5779-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="d5779-110">Van de voorbeeldconfiguratie van een sink voor Application Insights:</span><span class="sxs-lookup"><span data-stu-id="d5779-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="d5779-111">Hallo **Sink** *naam* kenmerk is een tekenreekswaarde die een unieke identificatie van Hallo sink.</span><span class="sxs-lookup"><span data-stu-id="d5779-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="d5779-112">Hallo **ApplicationInsights** element geeft instrumentatiesleutel Hallo Application insights-resource waar hello Azure diagnostics-gegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="d5779-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="d5779-113">Als u een bestaande Application Insights-resource niet hebt, raadpleegt u [Maak een nieuwe Application Insights-resource](../application-insights/app-insights-create-new-resource.md) voor meer informatie over het maken van een bron en het Hallo-instrumentatiesleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="d5779-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="d5779-114">Als u een Cloudservice met de Azure SDK 2.8 of hoger ontwikkelt, wordt deze instrumentatiesleutel automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="d5779-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="d5779-115">Hallo-waarde is gebaseerd op Hallo **APPINSIGHTS_INSTRUMENTATIONKEY** service van configuratie-instelling wanneer verpakking Hallo Cloud Services-project.</span><span class="sxs-lookup"><span data-stu-id="d5779-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="d5779-116">Zie [gebruik Application Insights met Azure Diagnostics tootroubleshoot Cloudservice problemen](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="d5779-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="d5779-117">Hallo **kanalen** element bevat een of meer **kanaal** elementen.</span><span class="sxs-lookup"><span data-stu-id="d5779-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="d5779-118">Hallo *naam* kenmerk unieke toothat kanaal verwijst.</span><span class="sxs-lookup"><span data-stu-id="d5779-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="d5779-119">Hallo *loglevel* kenmerk kunt u het Hallo-registratieniveau dat kanaal Hallo kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="d5779-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="d5779-120">Hallo beschikbaar logboekniveaus in volgorde van de meeste tooleast gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="d5779-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="d5779-121">Uitgebreide</span><span class="sxs-lookup"><span data-stu-id="d5779-121">Verbose</span></span>
        - <span data-ttu-id="d5779-122">Informatie</span><span class="sxs-lookup"><span data-stu-id="d5779-122">Information</span></span>
        - <span data-ttu-id="d5779-123">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="d5779-123">Warning</span></span>
        - <span data-ttu-id="d5779-124">Fout</span><span class="sxs-lookup"><span data-stu-id="d5779-124">Error</span></span>
        - <span data-ttu-id="d5779-125">Kritieke</span><span class="sxs-lookup"><span data-stu-id="d5779-125">Critical</span></span>

<span data-ttu-id="d5779-126">Een kanaal fungeert als een filter, en kunt u tooselect specifieke logboek niveaus toosend toohello doel sink.</span><span class="sxs-lookup"><span data-stu-id="d5779-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="d5779-127">U kan bijvoorbeeld uitgebreide logboeken verzamelen en ze toostorage verzenden, maar alleen fouten toohello sink verzenden.</span><span class="sxs-lookup"><span data-stu-id="d5779-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="d5779-128">Hallo volgende afbeelding ziet u deze relatie.</span><span class="sxs-lookup"><span data-stu-id="d5779-128">hello following graphic shows this relationship.</span></span>

![De openbare configuratie voor diagnostische gegevens](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="d5779-130">Hallo volgende afbeelding wordt samengevat configuratiewaarden Hallo en hoe ze werken.</span><span class="sxs-lookup"><span data-stu-id="d5779-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="d5779-131">U kunt meerdere put opnemen in de configuratie op verschillende niveaus in de hiërarchie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5779-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="d5779-132">Hallo sink op het hoogste niveau Hallo fungeert als een algemene instelling en hello een opgegeven op afzonderlijke Hallo element fungeert als een onderdrukking toothat globale instelling.</span><span class="sxs-lookup"><span data-stu-id="d5779-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Diagnostische gegevens Sinks configuratie met Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="d5779-134">Volledige sink configuratievoorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5779-134">Complete sink configuration example</span></span>
<span data-ttu-id="d5779-135">Hier volgt een compleet voorbeeld van de openbare configuratie Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="d5779-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="d5779-136">alle fouten tooApplication Insights verzendt (opgegeven op Hallo **DiagnosticMonitorConfiguration** knooppunt)</span><span class="sxs-lookup"><span data-stu-id="d5779-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="d5779-137">verzendt ook uitgebreide niveau logboeken voor Hallo toepassingslogboeken (opgegeven op Hallo **logboeken** knooppunt).</span><span class="sxs-lookup"><span data-stu-id="d5779-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="d5779-138">Hallo volgende regels hebben in de vorige configuratie hello, Hallo betekenis te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5779-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="d5779-139">Alle Hallo-gegevens worden verzameld door Azure diagnostics verzenden</span><span class="sxs-lookup"><span data-stu-id="d5779-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="d5779-140">Alleen fout logboeken toohello Application Insights sink verzenden</span><span class="sxs-lookup"><span data-stu-id="d5779-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="d5779-141">Uitgebreide toepassingslogboeken tooApplication Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="d5779-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="d5779-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="d5779-142">Limitations</span></span>

- <span data-ttu-id="d5779-143">**Kanalen zich alleen aanmelden type niet prestatiemeteritems als.**</span><span class="sxs-lookup"><span data-stu-id="d5779-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="d5779-144">Als u een kanaal met een element van de teller prestaties opgeeft, wordt dit genegeerd.</span><span class="sxs-lookup"><span data-stu-id="d5779-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="d5779-145">**Hallo logboekniveau voor een kanaal kan Hallo logboekniveau voor wat wordt er door Azure diagnostics wordt verzameld niet overschrijden.**</span><span class="sxs-lookup"><span data-stu-id="d5779-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="d5779-146">U kan bijvoorbeeld fouten toepassingslogboek in Logboeken-element Hallo verzamelen en probeer toosend uitgebreide logboeken toohello toepassing inzicht sink.</span><span class="sxs-lookup"><span data-stu-id="d5779-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="d5779-147">Hallo *scheduledTransferLogLevelFilter* kenmerk moet altijd gelijk verzamelen of meer logboeken dan Hallo Hiermee meldt u zich probeert toosend tooa sink.</span><span class="sxs-lookup"><span data-stu-id="d5779-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="d5779-148">**U kunt geen blob-gegevens verzameld door Azure diagnostics extensie tooApplication Insights verzenden.**</span><span class="sxs-lookup"><span data-stu-id="d5779-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="d5779-149">Bijvoorbeeld, iets opgegeven onder Hallo *mappen* knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d5779-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="d5779-150">TooApplication Insights wordt verzonden door voor crashdumps Hallo werkelijke crashdump tooblob opslag wordt verzonden en alleen een melding dat crashdump Hallo is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d5779-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5779-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5779-151">Next Steps</span></span>
* <span data-ttu-id="d5779-152">Meer informatie over hoe te[uw Azure diagnostics-gegevens weergeven](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d5779-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="d5779-153">Gebruik [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics-extensie voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d5779-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="d5779-154">Gebruik [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics-extensie voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="d5779-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
