---
title: Configureren van Azure Diagnostics om gegevens te verzenden naar Application Insights | Microsoft Docs
description: De openbare configuratie van Azure Diagnostics om gegevens te verzenden naar Application Insights bijwerken.
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
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="e9035-103">Cloud-Service, virtuele Machine of Service Fabric diagnostische gegevens verzenden naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="e9035-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="e9035-104">De extensie Azure Diagnostics-cloudservices, virtuele Machines, virtuele-Machineschaalsets en Service Fabric alle gebruiken om gegevens te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="e9035-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="e9035-105">Azure diagnostics verzendt gegevens naar Azure Storage-tabellen.</span><span class="sxs-lookup"><span data-stu-id="e9035-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="e9035-106">U kunt echter ook alle pipe of een subset van de gegevens naar andere locaties met de extensie Azure Diagnostics 1.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e9035-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="e9035-107">In dit artikel wordt beschreven hoe gegevens van de extensie Azure Diagnostics verzenden naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e9035-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="e9035-108">Configuratie van diagnostische uitgelegd</span><span class="sxs-lookup"><span data-stu-id="e9035-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="e9035-109">De extensie Azure diagnostics 1.5 geïntroduceerd Put, die zijn extra locaties waar u diagnostische gegevens kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="e9035-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="e9035-110">Van de voorbeeldconfiguratie van een sink voor Application Insights:</span><span class="sxs-lookup"><span data-stu-id="e9035-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="e9035-111">De **Sink** *naam* kenmerk is een tekenreekswaarde die een unieke identificatie van de sink.</span><span class="sxs-lookup"><span data-stu-id="e9035-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="e9035-112">De **ApplicationInsights** element geeft de instrumentatiesleutel van de Application insights-resource waarnaar de gegevens van Azure diagnostics is verzonden.</span><span class="sxs-lookup"><span data-stu-id="e9035-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="e9035-113">Als u een bestaande Application Insights-resource niet hebt, raadpleegt u [Maak een nieuwe Application Insights-resource](../application-insights/app-insights-create-new-resource.md) voor meer informatie over het maken van een resource en de instrumentatiesleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="e9035-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="e9035-114">Als u een Cloudservice met de Azure SDK 2.8 of hoger ontwikkelt, wordt deze instrumentatiesleutel automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="e9035-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="e9035-115">De waarde is gebaseerd op de **APPINSIGHTS_INSTRUMENTATIONKEY** service van configuratie-instelling wanneer het verpakken van de Cloud Services-project.</span><span class="sxs-lookup"><span data-stu-id="e9035-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="e9035-116">Zie [gebruik Application Insights met Azure Diagnostics problemen met Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="e9035-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="e9035-117">De **kanalen** element bevat een of meer **kanaal** elementen.</span><span class="sxs-lookup"><span data-stu-id="e9035-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="e9035-118">De *naam* kenmerk unieke verwijst naar dat kanaal.</span><span class="sxs-lookup"><span data-stu-id="e9035-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="e9035-119">De *loglevel* kenmerk kunt u het logboekniveau waarmee het kanaal opgeven.</span><span class="sxs-lookup"><span data-stu-id="e9035-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="e9035-120">De beschikbare logboekniveaus in volgorde van meest naar minst informatie zijn:</span><span class="sxs-lookup"><span data-stu-id="e9035-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="e9035-121">Uitgebreide</span><span class="sxs-lookup"><span data-stu-id="e9035-121">Verbose</span></span>
        - <span data-ttu-id="e9035-122">Informatie</span><span class="sxs-lookup"><span data-stu-id="e9035-122">Information</span></span>
        - <span data-ttu-id="e9035-123">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="e9035-123">Warning</span></span>
        - <span data-ttu-id="e9035-124">Fout</span><span class="sxs-lookup"><span data-stu-id="e9035-124">Error</span></span>
        - <span data-ttu-id="e9035-125">Kritieke</span><span class="sxs-lookup"><span data-stu-id="e9035-125">Critical</span></span>

<span data-ttu-id="e9035-126">Een kanaal dat fungeert als een filter, en kunt u specifieke logboekniveaus verzenden naar de doel-sink selecteren.</span><span class="sxs-lookup"><span data-stu-id="e9035-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="e9035-127">U kan bijvoorbeeld uitgebreide logboeken verzamelen en ze verzenden naar de opslag, maar alleen fouten verzenden naar de sink.</span><span class="sxs-lookup"><span data-stu-id="e9035-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="e9035-128">De volgende afbeelding ziet u deze relatie.</span><span class="sxs-lookup"><span data-stu-id="e9035-128">The following graphic shows this relationship.</span></span>

![De openbare configuratie voor diagnostische gegevens](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="e9035-130">De volgende afbeelding ziet u de configuratiewaarden en hoe ze werken.</span><span class="sxs-lookup"><span data-stu-id="e9035-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="e9035-131">U kunt meerdere put opnemen in de configuratie op verschillende niveaus in de hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="e9035-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="e9035-132">De sink op het hoogste niveau fungeert als een algemene instelling en die is opgegeven in de afzonderlijke element fungeert als een onderdrukking die algemene instelling.</span><span class="sxs-lookup"><span data-stu-id="e9035-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Diagnostische gegevens Sinks configuratie met Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="e9035-134">Volledige sink configuratievoorbeeld</span><span class="sxs-lookup"><span data-stu-id="e9035-134">Complete sink configuration example</span></span>
<span data-ttu-id="e9035-135">Hier volgt een compleet voorbeeld van de openbare configuratie voor het bestand dat</span><span class="sxs-lookup"><span data-stu-id="e9035-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="e9035-136">alle fouten naar Application Insights verzendt (opgegeven in de **DiagnosticMonitorConfiguration** knooppunt)</span><span class="sxs-lookup"><span data-stu-id="e9035-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="e9035-137">verzendt ook uitgebreide niveau logboeken voor de toepassingslogboeken (opgegeven in de **logboeken** knooppunt).</span><span class="sxs-lookup"><span data-stu-id="e9035-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
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
<span data-ttu-id="e9035-138">In de vorige configuratie hebben de volgende regels in de volgende betekenis:</span><span class="sxs-lookup"><span data-stu-id="e9035-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="e9035-139">Alle gegevens worden verzameld door Azure diagnostics verzenden</span><span class="sxs-lookup"><span data-stu-id="e9035-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="e9035-140">Alleen foutenlogboeken verzenden naar de Application Insights-sink</span><span class="sxs-lookup"><span data-stu-id="e9035-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="e9035-141">Uitgebreide toepassingslogboeken naar Application Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="e9035-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="e9035-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="e9035-142">Limitations</span></span>

- <span data-ttu-id="e9035-143">**Kanalen zich alleen aanmelden type niet prestatiemeteritems als.**</span><span class="sxs-lookup"><span data-stu-id="e9035-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="e9035-144">Als u een kanaal met een element van de teller prestaties opgeeft, wordt dit genegeerd.</span><span class="sxs-lookup"><span data-stu-id="e9035-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="e9035-145">**Het logboekniveau voor een kanaal kan niet groter zijn dan het logboekniveau voor wat wordt er door Azure diagnostics wordt verzameld.**</span><span class="sxs-lookup"><span data-stu-id="e9035-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="e9035-146">Bijvoorbeeld, u kan niet toepassingslogboek fouten in het element logboeken verzamelen en verzend uitgebreid logboeken voor de toepassing inzicht sink.</span><span class="sxs-lookup"><span data-stu-id="e9035-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="e9035-147">De *scheduledTransferLogLevelFilter* kenmerk moet altijd gelijk verzamelen of meer logboeken dan de logboeken u probeert te verzenden naar een sink.</span><span class="sxs-lookup"><span data-stu-id="e9035-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="e9035-148">**U kunt geen blob-gegevens verzameld door de extensie voor Azure diagnostische gegevens naar Application Insights verzenden.**</span><span class="sxs-lookup"><span data-stu-id="e9035-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="e9035-149">Bijvoorbeeld, iets opgegeven onder het *mappen* knooppunt.</span><span class="sxs-lookup"><span data-stu-id="e9035-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="e9035-150">Voor crashdumps de crashdump werkelijke is verzonden naar de blob storage en alleen een melding dat de crashdump is gegenereerd naar Application Insights wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="e9035-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9035-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9035-151">Next Steps</span></span>
* <span data-ttu-id="e9035-152">Meer informatie over hoe [uw Azure diagnostics-gegevens weergeven](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e9035-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="e9035-153">Gebruik [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) de extensie Azure diagnostics voor uw toepassing inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e9035-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="e9035-154">Gebruik [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) de extensie Azure diagnostics voor uw toepassing inschakelen</span><span class="sxs-lookup"><span data-stu-id="e9035-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
