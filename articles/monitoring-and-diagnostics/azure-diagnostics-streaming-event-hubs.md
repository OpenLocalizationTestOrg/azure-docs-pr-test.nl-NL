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
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Azure Diagnostics-gegevens in de hot pad Hallo streaming met behulp van Event Hubs
Azure Diagnostics biedt flexibele manieren toocollect metrische gegevens en registreert van cloud services virtuele machines (VM's) en het overdragen van resultaten tooAzure opslag. Vanaf tijdsbestek van Hallo maart 2016 (SDK 2.9), kunt u toocustom diagnostische gegevens verzenden gegevensbronnen en gegevensoverdracht hot pad (in seconden) met behulp van [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).

Ondersteunde gegevenstypen zijn onder andere:

* ETW-gebeurtenissen (Event Tracing for Windows)
* Prestatiemeteritems
* Windows-gebeurtenislogboeken
* Toepassingslogboeken
* Logboeken van Azure Diagnostics-infrastructuur

Dit artikel laat zien hoe Azure Diagnostics tooconfigure met Event Hubs van tooend eindigen. Ook richtlijnen gegeven voor Hallo algemene scenario's te volgen:

* Hoe toocustomize Hallo registreert en metrische gegevens die tooEvent Hubs wordt verzonden
* Hoe toochange configuraties in elke omgeving
* Hoe de gegevens voor het streamen van tooview Event Hubs
* Hoe tootroubleshoot Hallo verbinding  

## <a name="prerequisites"></a>Vereisten
Event Hubs receieving gegevens van Azure Diagnostics wordt ondersteund in Cloudservices, virtuele machines, virtuele-Machineschaalsets en Service Fabric vanaf hello Azure SDK 2.9 en hello Azure Tools voor Visual Studio overeenkomt.

* Azure Diagnostics-extensie 1.6 ([Azure SDK voor .NET 2.9 of hoger](https://azure.microsoft.com/downloads/) gericht is op dit standaard)
* [Visual Studio 2013 of hoger](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Bestaande configuraties van Azure Diagnostics in een toepassing met behulp van een *.wadcfgx* bestands- en een van de volgende methoden Hallo:
  * Visual Studio: [diagnostische gegevens configureren voor Azure-Cloudservices en virtuele Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen](../cloud-services/cloud-services-diagnostics-powershell.md)
* Event Hubs naamruimte is ingericht per Hallo-artikel [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Verbinding maken met Azure Diagnostics tooEvent Hubs sink
Standaard stuurt Azure Diagnostics altijd logboeken en metrische gegevens tooan Azure Storage-account. Een toepassing mogelijk gegevens tooEvent Hubs verzonden door het toevoegen van een nieuwe **Sinks** sectie onder Hallo **PublicConfig** / **WadCfg** element Hallo *.wadcfgx* bestand. In Visual Studio Hallo *.wadcfgx* bestand wordt opgeslagen in in het pad naar Hallo: **Cloudserviceproject** > **rollen** > **() RoleName)** > **diagnostics.wadcfgx** bestand.

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

In dit voorbeeld Hallo event hub-URL is ingesteld toohello volledig gekwalificeerd naamruimte van Hallo event hub: Event Hubs naamruimte + "/" + naam event hub.  

Hallo event hub-URL wordt weergegeven in Hallo [Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885) op Hallo Event Hubs-dashboard.  

Hallo **Sink** naam kan tooany geldige tekenreeks worden ingesteld als hello dezelfde waarde wordt gebruikt consistent in Hallo-configuratiebestand.

> [!NOTE]
> Mogelijk zijn er extra Put, zoals *applicationInsights* geconfigureerd in deze sectie. Azure Diagnostics kan een of meer toobe gedefinieerd als elke sink is ook gedeclareerd in het Hallo-sinks **PrivateConfig** sectie.  
>
>

Hallo Event Hubs sink moet ook worden gedeclareerd en gedefinieerd in Hallo **PrivateConfig** sectie Hallo *.wadcfgx* config-bestand.

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

Hallo `SharedAccessKeyName` waarde moet overeenkomen met een Shared Access Signature (SAS)-sleutel en het beleid dat is gedefinieerd in Hallo **Event Hubs** naamruimte. Blader toohello Event Hubs dashboard in Hallo [Azure-portal](https://manage.windowsazure.com), klikt u op Hallo **configureren** tabblad en instellen van een benoemde beleid (bijvoorbeeld ' SendRule') is *verzenden* machtigingen. Hallo **StorageAccount** ook is gedeclareerd in **PrivateConfig**. Hoeft niet hier toochange waarden als ze werken. In dit voorbeeld laat we Hallo waarden leeg, dit is een teken dat een downstream asset Hallo waarden worden ingesteld. Bijvoorbeeld, Hallo *ServiceConfiguration.Cloud.cscfg* omgeving configuratiebestand stelt Hallo omgeving passende namen en -sleutels.  

> [!WARNING]
> Hallo Event Hubs SAS-sleutel wordt opgeslagen als tekst zonder opmaak in Hallo *.wadcfgx* bestand. Deze sleutel wordt vaak toosource code controle is ingeschakeld of is beschikbaar als een activum in uw buildserver, zodat u deze naar gelang van toepassing moet beschermen. Het is raadzaam dat u een SAS-sleutel hier met *alleen verzenden* machtigingen zodat een kwaadwillende gebruiker kunt toohello event hub schrijven, maar die niet worden tooit luisteren of beheren.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Configureren van Azure Diagnostics toosend logboeken en metrische gegevens tooEvent Hubs
Zoals eerder, besproken alle standaard en aangepaste diagnostics-gegevens, dat wil zeggen, wordt metrische gegevens en zich aanmeldt, automatisch verzonden tooAzure opslag met intervallen van Hallo geconfigureerd. Met Event Hubs en eventuele aanvullende sink, kunt u een basis- of leaf-knooppunt in Hallo hiërarchie toobe toohello event hub wordt verzonden. Dit omvat ETW-gebeurtenissen, prestatiemeteritems, Windows-gebeurtenislogboeken en toepassingslogboeken.   

Het is belangrijk tooconsider hoeveel gegevenspunten daadwerkelijk moeten worden overgedragen tooEvent Hubs. Normaal gesproken ontwikkelaars gegevensoverdracht lage latentie hot pad die moet worden gebruikt en geïnterpreteerd snel. Systemen die waarschuwingen of regels voor automatisch schalen bewaken zijn voorbeelden. Een ontwikkelaar kan ook een alternatieve analyse store configureren of zoek store--bijvoorbeeld Azure Stream Analytics, Elasticsearch, een aangepaste bewakingssysteem of een favoriete bewakingssysteem van andere regels.

Hallo hieronder vindt u enkele voorbeeldconfiguraties.

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

Hallo sink is Hallo hierboven voorbeeld, toegepaste toohello bovenliggende **PerformanceCounters** knooppunt in de hiërarchie hello, wat betekent alle onderliggende dat **PerformanceCounters** tooEvent Hubs worden verzonden.  

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

In het vorige voorbeeld hello, Hallo sink is drie prestatiemeteritems toegepaste tooonly: **aanvragen in wachtrij**, **aanvragen afgewezen**, en **percentage processortijd**.  

Hallo volgende voorbeeld ziet u hoe een ontwikkelaar Hallo hoeveelheid verzonden gegevens toobe Hallo belangrijke metrische gegevens die worden gebruikt voor deze service health kunt beperken.  

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

In dit voorbeeld Hallo sink is toegepaste toologs en gefilterde alleen tooerror serviceniveau traceren.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Implementeren en bijwerken van een Cloud Services-toepassing en diagnostische configuratie
Visual Studio biedt Hallo eenvoudigste pad toodeploy Hallo toepassing en configuratie van Event Hubs sink. tooview en bewerk Hallo-bestand, open Hallo *.wadcfgx* bestand in Visual Studio, bewerken en opslaan. Hallo-pad is **Cloudserviceproject** > **rollen** > **(RoleName)** > **diagnostics.wadcfgx**.  

Op dit punt alle implementatie en implementatie bijwerken acties in Visual Studio, Visual Studio Team System en alle opdrachten of scripts die zijn gebaseerd op MSBuild en gebruik Hallo **/t: publiceren** doel omvatten Hallo *.wadcfgx*  in Hallo verpakking proces. Bovendien implementeren implementaties en -updates Hallo bestand tooAzure met Hallo juiste Azure Diagnostics agentextensie op uw virtuele machines.

Nadat u de toepassing hello en configuratie van diagnostische Azure implementeert, ziet u meteen activiteit in het dashboard Hallo van Hallo event hub. Hiermee wordt aangegeven dat u klaar toomove op tooviewing Hallo hot pad gegevens in Hallo-listener-client of analyse hulpprogramma van uw keuze bent.  

In Hallo volgende afbeelding, toont Hallo Event Hubs dashboard in orde verzending van diagnostische gegevens toohello event hub gestart ergens na 23: 00 uur. Als Hallo toepassing werd geïmplementeerd met een bijgewerkte *.wadcfgx* -bestand en Hallo sink correct is geconfigureerd.

![][0]  

> [!NOTE]
> Wanneer u updates toohello Azure Diagnostics-configuratiebestand (.wadcfgx), verdient het aanbeveling Hallo updates toohello volledige toepassing, evenals Hallo configuratie te pushen met behulp van Visual Studio publiceren of een Windows PowerShell-script.  
>
>

## <a name="view-hot-path-data"></a>Gegevens in de hot pad
Zoals eerder besproken, zijn er veel gebruiksvoorbeelden voor luisteren tooand verwerken van Event Hubs-gegevens.

Een eenvoudige aanpak is toocreate een kleine test console toepassing toolisten toohello event hub en afdrukken Hallo uitvoerstroom. U kunt plaatsen Hallo code, die wordt meer gedetailleerd uitgelegd in volgende [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in een consoletoepassing.  

Opmerking Hallo consoletoepassing vergezeld Hallo [Event Processor Host NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Houd er rekening mee tooreplace Hallo waarden punthaken in Hallo **Main** functie met waarden voor uw resources.   

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

## <a name="troubleshoot-event-hubs-sinks"></a>Event Hubs put oplossen
* Hallo event hub wordt niet weergegeven voor binnenkomende of uitgaande gebeurtenisactiviteit zoals verwacht.

    Controleer of uw event hub met succes is ingericht. Alle verbindingsgegevens in Hallo **PrivateConfig** sectie van *.wadcfgx* moet overeenkomen met Hallo waarden van de bron, zoals gezien in Hallo-portal. Zorg ervoor dat u een SAS-beleid gedefinieerd ('SendRule' in hello voorbeeld) in de portal Hallo en die hebt *verzenden* machtiging is verleend.  
* Na een update bevat Hallo event hub niet langer binnenkomende of uitgaande activiteit.

    Controleer eerst of deze Hallo event hub en informatie over de configuratie is juist zijn, zoals hierboven is uitgelegd. Soms Hallo **PrivateConfig** opnieuw is ingesteld in een implementatie-update. Hallo aanbevolen oplossing is toomake alle wijzigingen te*.wadcfgx* in project Hallo en vervolgens een update van de volledige toepassing push. Als dit niet mogelijk is, zorgt u ervoor dat Hallo diagnostische gegevens van de update een complete pushes **PrivateConfig** die Hallo SAS-sleutel bevat.  
* Ik probeerde Hallo suggesties en Hallo event hub is nog steeds niet werkt.

    Kijk in hello Azure Storage tabel met Logboeken en fouten voor Azure Diagnostics zelf: **WADDiagnosticInfrastructureLogsTable**. Een optie toouse is een hulpprogramma zoals [Azure Opslagverkenner](http://www.storageexplorer.com) tooconnect toothis storage-account, deze tabel weergeven en toevoegen van een query voor het tijdstempel in Hallo afgelopen 24 uur. U kunt gebruiken Hallo hulpprogramma tooexport een CSV-bestand en open het in een toepassing zoals Microsoft Excel. Excel kunt u eenvoudig toosearch voor tekenreeksen kaart, zoals **EventHubs**, toosee welke fout wordt gerapporteerd.  

## <a name="next-steps"></a>Volgende stappen
• [Meer informatie over Event Hubs](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Bijlage: Azure Diagnostics (.wadcfgx) voorbeeldconfiguratiebestand voltooien
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

Hallo aanvullende *ServiceConfiguration.Cloud.cscfg* voor dit voorbeeld ziet als Hallo volgende eruit.

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

Equivalente Json op basis van instellingen voor virtuele machines is als volgt:
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

## <a name="next-steps"></a>Volgende stappen
U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Event Hubs-overzicht](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Een Event Hub maken](../event-hubs/event-hubs-create.md)
* [Veelgestelde vragen over Event Hubs](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
