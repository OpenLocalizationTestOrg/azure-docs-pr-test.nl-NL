---
title: logboeken met behulp van Azure Diagnostics aaaCollect | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van Azure Diagnostics toocollect registreert van een Service Fabric-cluster in Azure wordt uitgevoerd.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Logboeken verzamelen met Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee toocollect Hallo Logboeken uit alle Hallo knooppunten in een centrale locatie. Hallo-logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in Hallo toepassingen en services die worden uitgevoerd in het cluster.

Een manier tooupload en verzamelen van Logboeken is toouse hello Azure extensie voor diagnostische gegevens, welke uploads logboeken tooAzure opslag, Azure Application Insights of Azure Event Hubs. Er zijn geen Hallo logboeken die handig zijn in de opslag of in Event Hubs. Maar u kunt een extern proces tooread Hallo gebeurtenissen uit de opslag gebruiken en plaats deze in een product zoals [logboekanalyse](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) wordt geleverd met een uitgebreide zoeken en analytics logboekservice ingebouwde.

## <a name="prerequisites"></a>Vereisten
Gebruik van deze hulpprogramma's voor tooperform aantal Hallo-bewerkingen in dit document:

* [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (gerelateerde tooAzure Cloudservices met een goede informatie over en voorbeelden)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager-client](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Meld u bronnen die u wilt misschien toocollect
* **Service Fabric-logboeken**: van Hallo platform toostandard Event Tracing voor Windows (ETW) en EventSource kanalen verzonden. Logboeken kunnen een van de verschillende typen zijn:
  * Operationele gebeurtenissen: logboeken voor bewerkingen waarvoor Hallo Service Fabric-platform wordt uitgevoerd. Voorbeelden zijn onder meer het maken van toepassingen en services, knooppunt statuswijzigingen en informatie over de upgrade.
  * [Reliable Actors programming model gebeurtenissen](service-fabric-reliable-actors-diagnostics.md)
  * [Reliable Services programming model gebeurtenissen](service-fabric-reliable-services-diagnostics.md)
* **Toepassingsgebeurtenissen**: gebeurtenissen verzonden vanuit de code van uw service en met behulp van de klasse van Help voor Hallo EventSource opgegeven in de Visual Studio-sjablonen Hallo uitgeschreven. Zie voor meer informatie over hoe toowrite vanuit uw App registreert, [bewaken en onderzoeken van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Hallo-extensie voor diagnostische gegevens implementeren
Hallo eerste stap bij het verzamelen van Logboeken is toodeploy Hallo-extensie voor diagnostische gegevens op elk van de VM Hallo in Hallo Service Fabric-cluster. Hallo-extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload toohello storage-account die u opgeeft. Hallo stappen verschillen enigszins op basis van of u hello Azure-portal of Azure Resource Manager gebruiken. Hallo stappen ook variëren, afhankelijk van of Hallo implementatie maakt deel uit van het maken van het cluster of voor een cluster dat al bestaat. Bekijk Hallo stappen voor elk scenario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster via Hallo portal implementeren
toodeploy hello Diagnostics extensie toohello virtuele machines in de cluster Hallo als onderdeel van het maken van het cluster, u Hallo Diagnostics paneel met toepassingsinstellingen in Hallo volgende afbeelding wordt weergegeven. tooenable Reliable Actors of Reliable Services gebeurtenissen verzamelen, moet het diagnostische gegevens te instellen**op** (Hallo standaardinstelling). Nadat u Hallo-cluster maakt, kunt u deze instellingen niet wijzigen met behulp van Hallo-portal.

![Azure Diagnostics-instellingen in Hallo-portal voor het maken van het cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Hallo ondersteuningsteam van Azure *vereist* ondersteuning logboeken toohelp los ondersteuningsaanvragen die u maakt. Deze logboeken worden in realtime verzameld en worden opgeslagen in een van de storage-accounts Hallo gemaakt in resourcegroep Hallo. Hallo diagnostische instellingen configureren op toepassingsniveau gebeurtenissen. Deze gebeurtenissen opnemen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) gebeurtenissen, [Reliable Services](service-fabric-reliable-services-diagnostics.md) gebeurtenissen en sommige systeemniveau Service Fabric gebeurtenissen toobe opgeslagen in Azure Storage.

Producten zoals [Elasticsearch](https://www.elastic.co/guide/index.html) of uw eigen proces Hallo gebeurtenissen kan worden opgehaald van Hallo storage-account. Er is momenteel geen manier toofilter of opschoondagen Hallo gebeurtenissen die worden verzonden toohello tabel. Als u een proces tooremove gebeurtenissen uit de tabel Hallo niet implementeert, blijven Hallo tabel toogrow.

Wanneer u een cluster met behulp van Hallo portal maakt, wordt ten zeerste aanbevolen dat u het Hallo-sjabloon downloaden **voordat u op OK** toocreate Hallo-cluster. Voor meer informatie, Raadpleeg te[een Service Fabric-cluster instellen met behulp van een Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md). Omdat u geen enkele wijzigingen aanbrengen met behulp van de portal Hallo, hebt u de Sjabloonwijzigingen toomake hello later nodig.

U kunt sjablonen exporteren vanuit de portal Hallo met behulp van de volgende stappen uit Hallo. Deze sjablonen kunnen echter moeilijker toouse zijn omdat ze wellicht hebben null-waarden die vereiste informatie ontbreekt.

1. Open uw resourcegroep.
2. Selecteer **instellingen** toodisplay Hallo paneel met toepassingsinstellingen.
3. Selecteer **implementaties** deelvenster Historie toodisplay Hallo-implementatie.
4. Selecteer een implementatie toodisplay Hallo details van Hallo-implementatie.
5. Selecteer **exportsjabloon** toodisplay Hallo sjabloon Configuratiescherm.
6. Selecteer **opslaan toofile** tooexport een ZIP-bestand dat Hallo-sjabloon, parameter en PowerShell-bestanden bevat.

Nadat u de bestanden Hallo exporteert, moet u toomake een wijziging. Hallo parameters.json bestand bewerken en verwijderen van Hallo **adminPassword** element. Hierdoor wordt een prompt voor wachtwoord Hallo wanneer Hallo implementatiescript wordt uitgevoerd. Wanneer u het implementatiescript Hallo uitvoert, hebt u mogelijk toofix null-parameterwaarden.

Hallo toouse gedownload sjabloon tooupdate een configuratie:

1. Pak Hallo inhoud tooa map op uw lokale computer.
2. Hallo inhoud tooreflect Hallo nieuwe configuratie wijzigen.
3. Start PowerShell en wijzig toohello map waar u Hallo inhoud hebt uitgepakt.
4. Uitvoeren **deploy.ps1** en vul Hallo abonnements-ID, naam resourcegroep hello (gebruik Hallo dezelfde naam tooupdate Hallo configuratie), en de naam van een unieke implementatie.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Hallo-extensie voor diagnostische gegevens als onderdeel van het maken van het cluster implementeren met behulp van Azure Resource Manager
toocreate een cluster met Resource Manager, moet u tooadd Hallo Diagnostics configuratie JSON toohello volledige cluster Resource Manager-sjabloon voordat u Hallo-cluster maakt. We een voorbeeldsjabloon vijf VM-cluster Resource Manager voorzien van configuratie van diagnostische toegevoegd tooit als onderdeel van onze voorbeelden Resource Manager-sjabloon. Kunt u deze bekijken op deze locatie in de galerie met hello Azure Samples: [cluster met vijf knooppunten met diagnostische gegevens van Resource Manager-sjabloon voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

toosee hello diagnostische instelling in Hallo Resource Manager-sjabloon, open Hallo azuredeploy.json bestand en zoek naar **IaaSDiagnostics**. een cluster met behulp van deze sjabloon, selecteer Hallo toocreate **tooAzure implementeren** beschikbaar op de vorige koppeling Hallo knop.

U kunt ook u kunt Hallo Resource Manager voorbeeld downloaden, tooit wijzigingen aanbrengen en Hallo met een cluster maken met de gewijzigde sjabloon Hallo `New-AzureRmResourceGroupDeployment` opdracht in een Azure PowerShell-venster. Zie Hallo code voor Hallo-parameters die u in toohello opdracht doorgeeft te volgen. Zie voor gedetailleerde informatie over hoe een resource toodeploy groeperen met behulp van PowerShell, Hallo artikel [een resourcegroep implementeren met Azure Resource Manager-sjabloon voor Hallo](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Bijwerken van diagnostische gegevens toocollect status en load-gebeurtenissen

Vanaf Hallo 5.4 versie van Service Fabric, zijn status en load metrische gebeurtenissen beschikbaar voor de verzameling. Deze gebeurtenissen gebeurtenissen die zijn gegenereerd door Hallo systeem of uw code via Hallo health of rapportage-API's, zoals load [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) of [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Hierdoor kan voor het aggregeren en weergeven van systeemstatus na verloop van tijd en voor waarschuwingen op basis van status- of load-gebeurtenissen. Deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen tooview ' Microsoft-ServiceFabric:4:0x4000000000000008 ' toohello lijst met ETW-providers.

toocollect hello gebeurtenissen, wijzigen Hallo resource manager-sjabloon tooinclude

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Bijwerken van diagnostische gegevens toocollect en logboeken van de nieuwe EventSource kanalen uploaden
tooupdate Diagnostics toocollect logboeken van de nieuwe EventSource kanalen die een nieuwe toepassing die u over toodeploy, vertegenwoordigen voeren dezelfde stappen als in Hallo Hallo [vorige sectie](#deploywadarm) voor het instellen van diagnostische gegevens voor een bestaande cluster.

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

## <a name="next-steps"></a>Volgende stappen
toounderstand in meer detail welke gebeurtenissen u moet letten tijdens het oplossen van problemen, Zie Hallo diagnostische gebeurtenissen die worden verzonden voor [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) en [Reliable Services](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Verwante artikelen:
* [Meer informatie over hoe toocollect prestatiemeteritems of de logboeken met behulp van Hallo extensie voor diagnostische gegevens](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Service Fabric-oplossing in Log Analytics](../log-analytics/log-analytics-service-fabric.md)

