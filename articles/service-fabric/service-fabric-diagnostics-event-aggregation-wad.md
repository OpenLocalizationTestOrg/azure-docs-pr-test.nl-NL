---
title: Aggregatie van Service Fabric-gebeurtenis met Windows Azure Diagnostics aaaAzure | Microsoft Docs
description: Meer informatie over het aggregeren en het verzamelen van gebeurtenissen met af voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Gebeurtenis-aggregatie en verzameling op basis van Windows Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee toocollect Hallo Logboeken uit alle Hallo knooppunten in een centrale locatie. Hallo-logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in Hallo toepassingen en services die worden uitgevoerd in het cluster.

Een manier tooupload en verzamelen van Logboeken is toouse Hallo Windows Azure Diagnostics (af) extensie, die u uploadt logboeken tooAzure opslag, en heeft ook Hallo optie toosend logboeken tooAzure Application Insights of Event Hubs. U kunt ook gebruikt een extern proces tooread Hallo gebeurtenissen uit de opslag en plaats deze in een analyse platform-product, zoals [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek.

## <a name="prerequisites"></a>Vereisten
Deze hulpprogramma's zijn gebruikte tooperform aantal Hallo-bewerkingen in dit document:

* [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (gerelateerde tooAzure Cloudservices met een goede informatie over en voorbeelden)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager-client](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Logboekbestand en de gebeurtenis

### <a name="service-fabric-platform-events"></a>Gebeurtenissen voor service Fabric-platform
Zoals beschreven in [in dit artikel](service-fabric-diagnostics-event-generation-infra.md), Service Fabric stelt u met enkele out-of-the-box-logboekregistratie kanalen, van die Hallo eenvoudig volgende kanalen zijn geconfigureerd met af toosend controle en diagnostische gegevens tooa opslag gegevenstabel of elders:
  * Operationele gebeurtenissen: een hoger niveau bewerkingen die Hallo Service Fabric-platform wordt uitgevoerd. Voorbeelden zijn onder meer het maken van toepassingen en services, knooppunt statuswijzigingen en informatie over de upgrade. Deze worden verzonden als Logboeken Event Tracing voor Windows (ETW)
  * [Reliable Actors programming model gebeurtenissen](service-fabric-reliable-actors-diagnostics.md)
  * [Reliable Services programming model gebeurtenissen](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Toepassingsgebeurtenissen
 Gebeurtenissen van uw toepassingen en services code verzonden en geschreven met behulp van Hallo EventSource helper-klasse die is opgegeven in Hallo Visual Studio-sjablonen. Zie voor meer informatie over hoe toowrite EventSource vanuit uw App registreert, [bewaken en onderzoeken van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Hallo-extensie voor diagnostische gegevens implementeren
Hallo eerste stap bij het verzamelen van Logboeken is toodeploy Hallo-extensie voor diagnostische gegevens op elk van de VM Hallo in Hallo Service Fabric-cluster. Hallo-extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload toohello storage-account die u opgeeft. Hallo stappen verschillen enigszins op basis van of u hello Azure-portal of Azure Resource Manager gebruiken. Hallo stappen ook variëren, afhankelijk van of Hallo implementatie maakt deel uit van het maken van het cluster of voor een cluster dat al bestaat. Bekijk Hallo stappen voor elk scenario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster via Azure portal implementeren
toodeploy hello Diagnostics extensie toohello virtuele machines in de cluster Hallo als onderdeel van het maken van het cluster, u Hallo Diagnostics paneel met toepassingsinstellingen weergegeven in de volgende Hallo afbeelding: Controleer of de diagnostische gegevens te is ingesteld**op** (Hallo standaardinstelling) . Nadat u Hallo-cluster maakt, kunt u deze instellingen niet wijzigen met behulp van Hallo-portal.

![Azure Diagnostics-instellingen in Hallo-portal voor het maken van het cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Wanneer u een cluster met behulp van Hallo portal maakt, wordt ten zeerste aanbevolen dat u het Hallo-sjabloon downloaden **voordat u op OK** toocreate Hallo-cluster. Voor meer informatie, Raadpleeg te[een Service Fabric-cluster instellen met behulp van een Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md). Omdat u geen enkele wijzigingen aanbrengen met behulp van de portal Hallo, hebt u de Sjabloonwijzigingen toomake hello later nodig.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster implementeren met behulp van Azure Resource Manager
toocreate een cluster met Resource Manager, moet u tooadd Hallo Diagnostics configuratie JSON toohello volledige cluster Resource Manager-sjabloon voordat u Hallo-cluster maakt. We een voorbeeldsjabloon vijf VM-cluster Resource Manager voorzien van configuratie van diagnostische toegevoegd tooit als onderdeel van onze voorbeelden Resource Manager-sjabloon. Kunt u deze bekijken op deze locatie in de galerie met hello Azure Samples: [cluster met vijf knooppunten met diagnostische gegevens van Resource Manager-sjabloon voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

toosee hello diagnostische instelling in Hallo Resource Manager-sjabloon, open Hallo azuredeploy.json bestand en zoek naar **IaaSDiagnostics**. een cluster met behulp van deze sjabloon, selecteer Hallo toocreate **tooAzure implementeren** beschikbaar op de vorige koppeling Hallo knop.

U kunt ook u kunt Hallo Resource Manager voorbeeld downloaden, tooit wijzigingen aanbrengen en Hallo met een cluster maken met de gewijzigde sjabloon Hallo `New-AzureRmResourceGroupDeployment` opdracht in een Azure PowerShell-venster. Zie Hallo code voor Hallo-parameters die u in toohello opdracht doorgeeft te volgen. Zie voor gedetailleerde informatie over hoe een resource toodeploy groeperen met behulp van PowerShell, Hallo artikel [een resourcegroep implementeren met Azure Resource Manager-sjabloon voor Hallo](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Hallo Diagnostics extensie tooan bestaande cluster implementeren
Als er een bestaand cluster dat geen diagnostische gegevens die zijn geïmplementeerd, of als u een bestaande configuratie toomodify wilt, kunt u deze kunt toevoegen of bijwerken. Hallo Resource Manager-sjabloon die wordt gebruikt toocreate Hallo bestaand cluster wijzigen of Hallo sjabloon downloaden van Hallo beheerportal, zoals eerder beschreven. Hallo template.json bestand wijzigen door het uitvoeren van Hallo taken te volgen.

Voeg een nieuwe opslag resource toohello sjabloon door toohello bronnensectie toe te voegen.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Vervolgens voegt u parameters toohello sectie direct na Hallo storage account definities tussen `supportLogStorageAccountName` en `vmNodeType0Name`. Hallo tijdelijke aanduiding voor tekst vervangen *opslagaccountnaam hier* met de naam van het opslagaccount Hallo Hallo.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Werk vervolgens, Hallo `VirtualMachineProfile` sectie van Hallo template.json bestand door toe te voegen Hallo code binnen Hallo extensies matrix te volgen. Niet zeker tooadd een komma aan Hallo begin of einde van de hello, afhankelijk van waar het ingevoegd.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Nadat u gewijzigd Hallo template.json bestand, zoals wordt beschreven, opnieuw publiceren Hallo Resource Manager-sjabloon. Als Hallo-sjabloon is geëxporteerd, rapport uitvoeren Hallo deploy.ps1 van bestand opnieuw publiceert Hallo-sjabloon. Nadat u hebt geïmplementeerd, zorg ervoor dat **ProvisioningState** is **geslaagd**.

## <a name="collect-health-and-load-events"></a>Health verzamelen en laden van gebeurtenissen

Vanaf Hallo 5.4 versie van Service Fabric, zijn status en load metrische gebeurtenissen beschikbaar voor de verzameling. Deze gebeurtenissen gebeurtenissen die zijn gegenereerd door Hallo systeem of uw code via Hallo health of rapportage-API's, zoals load [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) of [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Hierdoor kan voor het aggregeren en weergeven van systeemstatus na verloop van tijd en voor waarschuwingen op basis van status- of load-gebeurtenissen. Deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen tooview ' Microsoft-ServiceFabric:4:0x4000000000000008 ' toohello lijst met ETW-providers.

toocollect hello gebeurtenissen, wijzigen Hallo Resource Manager-sjabloon tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Omgekeerde proxy-gebeurtenissen verzamelen

Vanaf versie van Service Fabric Hallo 5.7 [omgekeerde proxy](service-fabric-reverseproxy.md) gebeurtenissen zijn beschikbaar voor de verzameling.
Omgekeerde proxy verzendt gebeurtenissen naar twee kanalen, één met fout gebeurtenissen opgetreden bij het weergeven mislukte verwerkingen aanvragen en andere uitgebreide gebeurtenissen over alle Hallo-aanvragen op Hallo omgekeerde proxy verwerkt met een Hallo. 

1. Verzamelen van foutgebeurtenissen: tooview deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen ' Microsoft-ServiceFabric:4:0x4000000000000010 ' toohello lijst met ETW-providers.
toocollect hello gebeurtenissen van Azure clusters wijzigen Hallo Resource Manager-sjabloon tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Verzamelt alle verwerking van gebeurtenissen aanvragen: In Visual Studio van diagnostische logboeken update Hallo Microsoft ServiceFabric vermelding in de lijst voor ETW-provider te Hallo ' Microsoft-ServiceFabric:4:0x4000000000000020 '.
Voor de Azure Service Fabric-clusters, wijzigt u tooinclude Hallo resource manager-sjabloon

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> Het verdient toojudiciously inschakelen verzamelen gebeurtenissen van dit kanaal omdat dit al het verkeer via de omgekeerde proxy Hallo verzamelt en opslagcapaciteit snel kan gebruiken.

Voor Azure Service Fabric-clusters Hallo gebeurtenissen van alle knooppunten van het Hallo verzameld en geaggregeerd in Hallo SystemEventTable.
Voor gedetailleerde probleemoplossing van Hallo reverse proxy-gebeurtenissen, Raadpleeg Hallo [omgekeerde proxy diagnostics handleiding](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Verzamelen van nieuwe EventSource kanalen

tooupdate Diagnostics toocollect logboeken van de nieuwe EventSource kanalen die een nieuwe toepassing die u over toodeploy, vertegenwoordigen uitvoeren Hallo dezelfde stappen als eerder beschreven voor het instellen van de Hallo van diagnostische gegevens voor een bestaand cluster.

Hallo bijwerken `EtwEventSourceProviderConfiguration` sectie in Hallo template.json bestandsvermeldingen tooadd Hallo nieuwe EventSource kanalen voordat u Hallo configuratie toepassen met behulp van Hallo werk `New-AzureRmResourceGroupDeployment` PowerShell-opdracht. Hallo-naam van de gebeurtenisbron Hallo is gedefinieerd als onderdeel van uw code in Hallo ServiceEventSource.cs Visual Studio gegenereerd bestand.

Als uw gebeurtenisbron mijn Eventsource heet, bijvoorbeeld Hallo volgende code tooplace Hallo gebeurtenissen uit mijn Eventsource in een tabel met de naam MyDestinationTableName toevoegen.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

toocollect-prestatiemeteritems of gebeurtenislogboeken Hallo Resource Manager-sjabloon wijzigen met behulp van Hallo-voorbeelden vindt u in [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van een Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vervolgens opnieuw publiceren Hallo Resource Manager-sjabloon.

## <a name="collect-performance-counters"></a>Verzamelen van prestatiemeteritems

Hallo prestaties tellers tooyour 'WadCfg > DiagnosticMonitorConfiguration' toevoegen toocollect maatstaven voor prestaties van het cluster in Hallo Resource Manager-sjabloon voor uw cluster. Zie [Service Fabric-prestatiemeteritems](service-fabric-diagnostics-event-generation-perf.md) voor prestatiemeteritems die wordt aangeraden verzamelen.

Bijvoorbeeld: Hier wordt een prestatiemeteritem dat elke 15 seconden instellen (dit kan worden gewijzigd en volgt de indeling van Hallo ' PT\<tijd >\<eenheid > ', bijvoorbeeld PT3M zou een steekproef nemen uit drie minuten durende intervallen), en toohello overgedragen de juiste opslag tabel om één minuut.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Als u een Application Insights-sink gebruikt zoals beschreven in onderstaande sectie voor Hallo en deze metrische gegevens tooshow-up in Application Insights wilt, moet u ervoor tooadd Hallo sink-naam in Hallo 'put' sectie zoals hierboven. Bovendien kunt u een afzonderlijke tabel toosend uw prestatiemeteritems, zodat ze niet uit Hallo opnemen die afkomstig zijn van Hallo andere logboekkanalen die u hebt ingeschakeld.


## <a name="send-logs-tooapplication-insights"></a>Verzenden logboeken tooApplication Insights

Verzenden van controle en diagnostische gegevens tooApplication Insights (AI) kan worden uitgevoerd als onderdeel van Hallo af configuratie. Als u toouse AI voor analyse van gebeurtenis en visualisatie besluit, lezen [analyse van gebeurtenis en visualisatie met Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset van een AI Sink als onderdeel van uw 'WadCfg'.

## <a name="next-steps"></a>Volgende stappen

Nadat u Azure diagnostics correct hebt geconfigureerd, ziet u gegevens in de tabellen bij opslag van EventSource logboeken en Hallo ETW. Als u toouse OMS, moet Kibana of een andere gegevens analytics en visualisatie platform dat niet rechtstreeks in het Hallo-Resource Manager-sjabloon is geconfigureerd dat tooset Hallo platform van uw keuze tooread in Hallo gegevens uit deze opslagtabellen. Hierdoor voor OMS is relatief eenvoudig en wordt uitgelegd in [analyse van gebeurtenis- en logboekbestanden via OMS](service-fabric-diagnostics-event-analysis-oms.md). Application Insights is een bit van een speciaal geval in dit opzicht, omdat deze kan worden geconfigureerd als onderdeel van de configuratie van diagnostische gegevens uitbreiding hello, raadpleegt u dus toohello [juiste artikel](service-fabric-diagnostics-event-analysis-appinsights.md) als u ervoor toouse AI kiest.

>[!NOTE]
>Er is momenteel geen manier toofilter of opschoondagen Hallo gebeurtenissen die worden verzonden toohello tabel. Als u een proces tooremove gebeurtenissen uit de tabel Hallo niet implementeert, blijven Hallo tabel toogrow. Er is een voorbeeld van een gegevensservice opschonen uitgevoerd in de Hallo [Watchdog voorbeeld](https://github.com/Azure-Samples/service-fabric-watchdog-service), en wordt aanbevolen dat u één voor uzelf, schrijft tenzij er een goede reden voor u toostore Logboeken na een periode 30 of 90 dagen.

* [Meer informatie over hoe toocollect prestatiemeteritems of de logboeken met behulp van Hallo extensie voor diagnostische gegevens](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Analyse van gebeurtenis en visualisatie met Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analyse van gebeurtenis en visualisatie met OMS](service-fabric-diagnostics-event-analysis-oms.md)