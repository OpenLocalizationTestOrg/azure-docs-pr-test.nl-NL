---
title: Logboeken verzamelen met behulp van Azure Diagnostics | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Diagnostics instelt voor het verzamelen van Logboeken van een Service Fabric-cluster in Azure wordt uitgevoerd.
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
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Logboeken verzamelen met Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Wanneer u een Azure Service Fabric-cluster uitvoert, is het een goed idee de logboeken verzamelen van alle knooppunten in een centrale locatie. De logboeken die in een centrale locatie, helpt u bij het analyseren en oplossen van problemen in het cluster of problemen in de toepassingen en services die worden uitgevoerd in het cluster.

Een manier om te uploaden en verzamelen van Logboeken is het gebruik van de extensie Azure Diagnostics, die logboeken naar Azure Storage of Azure Application Insights Azure Event Hubs uploadt. Er zijn geen de logboeken die handig zijn in de opslag of in Event Hubs. Maar u kunt een extern proces gebruiken om te lezen van de gebeurtenissen uit de opslag en plaats deze in een product zoals [logboekanalyse](../log-analytics/log-analytics-service-fabric.md) of een andere oplossing voor het parseren van het logboek. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) wordt geleverd met een uitgebreide zoeken en analytics logboekservice ingebouwde.

## <a name="prerequisites"></a>Vereisten
U kunt deze hulpprogramma's gebruiken enkele bewerkingen uitvoeren in dit document:

* [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (gerelateerd aan Azure Cloud Services, maar heeft goede informatie over en voorbeelden)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager-client](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a>Logboek bronnen die u wilt verzamelen
* **Service Fabric-logboeken**: van het platform standaard Event Tracing voor Windows (ETW) en EventSource kanalen verzonden. Logboeken kunnen een van de verschillende typen zijn:
  * Operationele gebeurtenissen: logboeken voor bewerkingen waarmee de Service Fabric-platform. Voorbeelden zijn onder meer het maken van toepassingen en services, knooppunt statuswijzigingen en informatie over de upgrade.
  * [Reliable Actors programming model gebeurtenissen](service-fabric-reliable-actors-diagnostics.md)
  * [Reliable Services programming model gebeurtenissen](service-fabric-reliable-services-diagnostics.md)
* **Toepassingsgebeurtenissen**: gebeurtenissen verzonden vanuit de code van uw service en geschreven met behulp van de EventSource helperklasse opgegeven in de Visual Studio-sjablonen. Zie voor meer informatie over het schrijven van Logboeken van uw toepassing [bewaken en onderzoeken van services in de instellingen voor een lokale computer ontwikkeling](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-the-diagnostics-extension"></a>De extensie voor diagnostische gegevens implementeren
De eerste stap bij het verzamelen van Logboeken is voor het implementeren van de extensie voor diagnostische gegevens over elk van de virtuele machines in het Service Fabric-cluster. De extensie voor diagnostische gegevens verzamelt logboeken op elke virtuele machine en geüpload naar het opslagaccount dat u opgeeft. De stappen verschillen enigszins op basis van of u de Azure portal of Azure Resource Manager gebruiken. De stappen ook variëren, afhankelijk van of de implementatie maakt deel uit van het maken van het cluster of voor een cluster dat al bestaat. Bekijk de stappen voor elk scenario.

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a>De extensie voor diagnostische gegevens als onderdeel van het maken van het cluster via de portal implementeren
Als u wilt implementeren de extensie voor diagnostische gegevens op de virtuele machines in het cluster als onderdeel van het maken van het cluster, moet u het instellingenpaneel voor diagnostische gegevens dat wordt weergegeven in de volgende afbeelding gebruiken. Zorg ervoor dat Diagnostics is ingesteld op zodat Reliable Actors of Reliable Services gebeurtenisverzameling **op** (de standaardinstelling). Nadat u het cluster hebt gemaakt, kunt u deze instellingen niet wijzigen met behulp van de portal.

![Azure Diagnostics-instellingen in de portal voor het maken van het cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Het ondersteuningsteam van Azure *vereist* ondersteuning voor de logboeken om te helpen bij het oplossen van eventuele ondersteuningsaanvragen die u maakt. Deze logboeken worden in realtime verzameld en worden opgeslagen in een van de storage-accounts in de resourcegroep hebt gemaakt. De diagnostische instellingen configureren op toepassingsniveau gebeurtenissen. Deze gebeurtenissen opnemen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) gebeurtenissen, [Reliable Services](service-fabric-reliable-services-diagnostics.md) en sommige gebeurtenissen op systeemniveau Service Fabric worden opgeslagen in Azure Storage.

Producten zoals [Elasticsearch](https://www.elastic.co/guide/index.html) of uw eigen proces, krijgen de gebeurtenissen van het opslagaccount. Er is momenteel geen manier om te filteren of Let op de gebeurtenissen die worden verzonden naar de tabel. Als u een proces voor het verwijderen van gebeurtenissen uit de tabel niet implementeert, wordt de tabel blijven groeien.

Wanneer u een cluster met behulp van de portal maakt, wordt ten zeerste aanbevolen dat u de sjabloon downloaden **voordat u op OK** om het cluster te maken. Raadpleeg voor meer informatie, [een Service Fabric-cluster instellen met behulp van een Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md). U moet de sjabloon wijzigingen later aanbrengen omdat u geen enkele wijzigingen aanbrengen met behulp van de portal.

U kunt sjablonen exporteren vanuit de portal met behulp van de volgende stappen uit. Deze sjablonen mag moeilijker te gebruiken, omdat ze wellicht hebben null-waarden die vereiste informatie ontbreekt.

1. Open uw resourcegroep.
2. Selecteer **instellingen** om het deelvenster instellingen openen.
3. Selecteer **implementaties** om het deelvenster implementatie historie weer te geven.
4. Selecteer een implementatie om de details van de implementatie weer te geven.
5. Selecteer **exportsjabloon** om het deelvenster sjabloon weer te geven.
6. Selecteer **opslaan naar bestand** exporteren van een ZIP-bestand dat de sjabloon, een parameter en een PowerShell-bestanden bevat.

Nadat u de bestanden hebt geëxporteerd, moet u een wijziging aanbrengt. Bewerk het bestand parameters.json en verwijder de **adminPassword** element. Hierdoor wordt een wachtwoord wordt gevraagd wanneer het script voor implementatie wordt uitgevoerd. Wanneer u het script voor implementatie uitvoert, moet u wellicht los van null-parameterwaarden.

De gedownloade sjabloon gebruiken een configuratie bij te werken:

1. Pak de inhoud naar een map op uw lokale computer.
2. De inhoud naar aanleiding van de nieuwe configuratie niet wijzigen.
3. Start PowerShell en Ga naar de map waar u de inhoud hebt uitgepakt.
4. Voer **deploy.ps1** en vul de abonnements-ID, de Resourcegroepnaam (Gebruik dezelfde naam van de configuratie bijwerken) en de naam van een unieke implementatie.

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>De extensie voor diagnostische gegevens als onderdeel van het maken van het cluster implementeren met behulp van Azure Resource Manager
Voor het maken van een cluster met Resource Manager, moet u de configuratie van diagnostische JSON toevoegen aan het volledige cluster Resource Manager-sjabloon voordat u het cluster maakt. We bieden een voorbeeldsjabloon vijf VM-cluster Resource Manager met de configuratie van diagnostische toegevoegd als onderdeel van onze voorbeelden Resource Manager-sjabloon. U kunt het zien op deze locatie in de galerie van Azure Samples: [cluster met vijf knooppunten met diagnostische gegevens van Resource Manager-sjabloon voorbeeld](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

Als u de instelling van de diagnostische gegevens in de Resource Manager-sjabloon, open het bestand azuredeploy.json en zoeken naar **IaaSDiagnostics**. Als u een cluster met behulp van deze sjabloon, selecteert de **implementeren in Azure** knop beschikbaar op de vorige koppeling.

U kunt ook u kunt het Resource Manager-voorbeeld downloaden, wijzigingen aanbrengen en een cluster maken met de gewijzigde sjabloon met behulp van de `New-AzureRmResourceGroupDeployment` opdracht in een Azure PowerShell-venster. Zie de volgende code voor de parameters die u aan de opdracht doorgeeft. Zie het artikel voor gedetailleerde informatie over het implementeren van een resourcegroep met behulp van PowerShell [een resourcegroep implementeren met de Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a>De extensie voor diagnostische gegevens aan een bestaand cluster implementeren
Als u een bestaand cluster dat geen diagnostische gegevens die zijn geïmplementeerd, of als u wilt wijzigen van een bestaande configuratie, kunt u deze kunt toevoegen of bijwerken. Wijzig de Resource Manager-sjabloon die wordt gebruikt voor het maken van het bestaande cluster of de sjabloon downloaden van de portal, zoals eerder beschreven. Het bestand template.json wijzigen door de volgende taken uitvoeren.

Een nieuwe opslagresource toevoegen aan de sjabloon door toe te voegen aan de bronnensectie.

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

 Vervolgens voegt u het gedeelte parameters direct na de definities van de account opslag tussen `supportLogStorageAccountName` en `vmNodeType0Name`. Vervang de tijdelijke aanduiding voor tekst *opslagaccountnaam hier* met de naam van het opslagaccount.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
Werk vervolgens de `VirtualMachineProfile` gedeelte van het bestand template.json door de volgende code binnen de matrix extensies toe te voegen. Zorg ervoor dat een komma toe te voegen aan het begin of einde, afhankelijk van waar het ingevoegd.

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

Nadat u het bestand template.json aanpassen zoals is beschreven, publiceert u de Resource Manager-sjabloon opnieuw. Als de sjabloon is geëxporteerd, het bestand deploy.ps1 uitvoert rapport opnieuw publiceert de sjabloon. Nadat u hebt geïmplementeerd, zorg ervoor dat **ProvisioningState** is **geslaagd**.

## <a name="update-diagnostics-to-collect-health-and-load-events"></a>Bijwerken van diagnostische gegevens te verzamelen health gebeurtenissen laden

Beginnen met de 5,4 release van Service Fabric, zijn status en load metrische gebeurtenissen beschikbaar voor de verzameling. Deze gebeurtenissen gebeurtenissen die door het systeem of uw code worden gegenereerd met behulp van de status aangeven of rapportage-API's, zoals laden [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) of [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Hierdoor kan voor het aggregeren en weergeven van systeemstatus na verloop van tijd en voor waarschuwingen op basis van status- of load-gebeurtenissen. Om weer te geven deze gebeurtenissen in Visual Studio diagnostische logboeken toevoegen ' Microsoft-ServiceFabric:4:0x4000000000000008 ' aan de lijst met ETW-providers.

Voor het verzamelen van gebeurtenissen, wijzigt u de resource manager-sjabloon wilt opnemen

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

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a>Bijwerken van diagnostische gegevens om te verzamelen en logboeken van de nieuwe EventSource kanalen uploaden
Voor het bijwerken van diagnostische gegevens voor het verzamelen van Logboeken van de nieuwe EventSource kanalen die vertegenwoordigen een nieuwe toepassing die u wilt implementeren, voeren dezelfde stappen als in de [vorige sectie](#deploywadarm) voor het instellen van diagnostische gegevens voor een bestaand cluster.

Werk de `EtwEventSourceProviderConfiguration` sectie in het bestand template.json vermeldingen toevoegen voor de nieuwe EventSource kanalen voordat u de configuratie toepassen met behulp van bijwerken de `New-AzureRmResourceGroupDeployment` PowerShell-opdracht. De naam van de bron van de gebeurtenis wordt gedefinieerd als onderdeel van uw code in het bestand ServiceEventSource.cs Visual Studio gegenereerd.

Als uw gebeurtenisbron mijn Eventsource heet, bijvoorbeeld de volgende code om de gebeurtenissen uit mijn Eventsource plaatsen in een tabel met de naam MyDestinationTableName toevoegen.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

Wijzigen voor het verzamelen van prestatiemeteritems of de gebeurtenislogboeken van de Resource Manager-sjabloon met behulp van de voorbeelden die is opgegeven in [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van een Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vervolgens publiceert u de Resource Manager-sjabloon opnieuw.

## <a name="next-steps"></a>Volgende stappen
Zie de diagnostische gebeurtenissen verzonden voor inzicht in meer detail welke gebeurtenissen u letten moet tijdens het oplossen van problemen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) en [Reliable Services](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Verwante artikelen:
* [Meer informatie over het verzamelen van prestatiemeteritems of logboeken met behulp van de extensie voor diagnostische gegevens](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Service Fabric-oplossing in Log Analytics](../log-analytics/log-analytics-service-fabric.md)

