---
title: aaaVirtual-machines in een Azure Resource Manager-sjabloon | Microsoft Azure
description: Meer informatie over hoe de bron van de virtuele machine Hallo is gedefinieerd in een Azure Resource Manager-sjabloon.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Virtuele machines in een Azure Resource Manager-sjabloon

Dit artikel wordt beschreven aspecten van een Azure Resource Manager-sjabloon die van toepassing zijn toovirtual machines. Een volledige sjabloon voor het maken van een virtuele machine; wordt niet beschreven in dit artikel daarvoor moet u resourcedefinities voor storage-accounts, netwerkinterfaces, openbare IP-adressen en virtuele netwerken. Zie voor meer informatie over hoe deze resources samen kunnen worden gedefinieerd, Hallo [overzicht voor Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Er zijn veel [sjablonen in de galerie Hallo](https://azure.microsoft.com/documentation/templates/?term=VM) die Hallo VM-resource bevatten. Niet alle elementen die kunnen worden opgenomen in een sjabloon worden hier beschreven.

Dit voorbeeld toont een typische resource-gedeelte van een sjabloon voor het maken van een opgegeven aantal virtuele machines:

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>In dit voorbeeld is afhankelijk van een opslagaccount dat eerder is gemaakt. U kunt Hallo storage-account maken door het implementeren van Hallo-sjabloon. Hallo-voorbeeld is ook afhankelijk van een netwerkinterface en de bijbehorende afhankelijke bronnen die zouden worden gedefinieerd in Hallo-sjabloon. Deze resources worden niet weergegeven in het Hallo-voorbeeld.
>
>

## <a name="api-version"></a>API-versie

Wanneer u resources met behulp van een sjabloon implementeert, hebt u toospecify een versie van Hallo API toouse. Hallo-voorbeeld ziet u de bron van de virtuele machine Hallo met behulp van dit element apiVersion:

```
"apiVersion": "2016-04-30-preview",
```

Hallo-versie van Hallo API die u in de sjabloon opgeeft is van invloed op welke eigenschappen u in de sjabloon Hallo kunt definiëren. In het algemeen moet u de meest recente API-versie Hallo bij het maken van sjablonen. Voor bestaande sjablonen, kunt u beslissen of u wilt dat met een eerdere versie van de API toocontinue of bijwerken van de sjabloon voor Hallo meest recente versie tootake profiteren van nieuwe functies.

Deze mogelijkheden voor het ophalen van de nieuwste API-versies hello gebruiken:

- REST-API - [alle resourceproviders vermelden](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- Azure CLI 2.0 - [az provider weergeven](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Parameters en variabelen

[Parameters](../../resource-group-authoring-templates.md) eenvoudiger voor u toospecify waarden voor Hallo sjabloon wanneer u het uitvoert. Deze sectie parameters wordt gebruikt in Hallo-voorbeeld:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Wanneer u Hallo voorbeeldsjabloon implementeert, voert u de waarden voor Hallo naam en het wachtwoord van Hallo administrator-account voor elke virtuele machine en Hallo aantal virtuele machines toocreate. U hebt de optie Hallo van het opgeven van parameterwaarden in een afzonderlijk bestand dat wordt beheerd met Hallo-sjabloon of geef dezelfde waarden als u wordt gevraagd.

[Variabelen](../../resource-group-authoring-templates.md) eenvoudiger voor u tooset waarden in Hallo-sjabloon die in deze herhaaldelijk worden gebruikt of die na verloop van tijd kunt wijzigen. Deze sectie variabelen wordt gebruikt in Hallo-voorbeeld:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Wanneer u Hallo voorbeeldsjabloon implementeert, worden de waarden van variabelen worden gebruikt voor Hallo naam en id van het opslagaccount Hallo eerder hebt gemaakt. Variabelen zijn ook gebruikte tooprovide Hallo-instellingen voor diagnostische Hallo-extensie. Gebruik Hallo [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](../../resource-manager-template-best-practices.md) toohelp u bepalen hoe u toostructure Hallo parameters en variabelen in de sjabloon.

## <a name="resource-loops"></a>Resource lussen

Als u meer dan één virtuele machine nodig hebt voor uw toepassing, kunt u een kopie-element in een sjabloon. Dit element optioneel doorlopen Hallo aantal virtuele machines die u hebt opgegeven als parameter maken:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

In voorbeeld Hallo Hallo lusindex wordt ook gebruikt bij het opgeven aantal Hallo waarden voor Hallo resource. Als u een aantal exemplaren van drie, Hallo namen van Hallo besturingssysteem schijven ingevoerd zijn bijvoorbeeld myOSDisk1, myOSDisk2 en myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>In dit voorbeeld worden beheerde schijven gebruikt voor Hallo virtuele machines.
>
>

Houd er rekening mee dat een lus voor één resource maken in de sjabloon Hallo kan u toouse Hallo lus bij het maken of openen van andere bronnen in beslag. Meerdere virtuele machines niet dezelfde netwerkinterface, dus als uw sjabloon doorlopen voor het maken van drie virtuele machines die deze ook maken doorlopen moet drie netwerkinterfaces Hallo bijvoorbeeld niet gebruiken. Bij het toewijzen van een network interface tooa VM Hallo lusindex gebruikte tooidentify wordt deze:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Afhankelijkheden

De meeste bronnen hangen af van andere bronnen toowork correct. Virtuele machines moet worden gekoppeld aan een virtueel netwerk en toodo dat het moet een netwerkinterface. Hallo [dependsOn](../../resource-group-define-dependencies.md) element heeft de gebruikte toomake ervoor Hallo netwerkinterface is gereed toobe gebruikt voordat VMs Hallo worden gemaakt:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager implementeert parallel alle bronnen die zijn niet afhankelijk van een andere resource wordt geïmplementeerd. Wees voorzichtig bij het instellen van afhankelijkheden, omdat u uw implementatie per ongeluk afnemen kan door te geven, afhankelijkheden niet nodig. Afhankelijkheden kunnen koppelen via meerdere bronnen. Bijvoorbeeld, afhankelijk Hallo netwerkinterface Hallo openbaar IP-adres en resources van een virtueel netwerk.

Hoe weet u of een afhankelijkheid vereist is? Hallo-waarden in Hallo sjabloon kijken. Als een element in de resourcedefinitie Hallo-virtuele machine verwijst tooanother resource die is geïmplementeerd in Hallo dezelfde sjabloon, moet u een afhankelijkheid. Uw voorbeeld van de virtuele machine wordt bijvoorbeeld een netwerkprofiel gedefinieerd:

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset deze eigenschap Hallo netwerkinterface moet bestaan. Daarom moet u een afhankelijkheid. U moet ook een afhankelijkheid tooset als één resource (een onderliggende) is gedefinieerd in een andere resource (bovenliggend). Bijvoorbeeld, Hallo diagnostische instellingen en aangepaste scriptextensies zijn gedefinieerd als onderliggende resources van Hallo virtuele machine. Ze kunnen niet worden gemaakt totdat Hallo virtuele machine bestaat. Beide resources zijn daarom gemarkeerd als afhankelijke op Hallo virtuele machine.

## <a name="profiles"></a>Profielen

Verschillende profiel elementen worden gebruikt bij het definiëren van de bron van een virtuele machine. Sommige zijn vereist en sommige zijn optioneel. Bijvoorbeeld, Hallo het hardwareProfile, osProfile storageProfile en Schaalaanpassingsset elementen zijn vereist, maar Hallo diagnosticsProfile is optioneel. Deze profielen definiëren instellingen zoals:
   
- [grootte](sizes.md)
- [naam](/architecture/best-practices/naming-conventions) en referenties
- schijf en [besturingssysteeminstellingen](cli-ps-findimage.md)
- [netwerkinterface](../../virtual-network/virtual-networks-multiple-nics.md) 
- Diagnostische gegevens over opstarten

## <a name="disks-and-images"></a>Schijven en installatiekopieën
   
In Azure, vhd-bestanden kunnen geven [schijven of installatiekopieën](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Wanneer het Hallo-besturingssysteem in een vhd-bestand is gespecialiseerde toobe een specifieke virtuele machine, is het waarnaar wordt verwezen tooas een schijf. Wanneer het Hallo-besturingssysteem in een vhd-bestand is gegeneraliseerd toobe gebruikt toocreate veel VM's, waarnaar wordt verwezen tooas een afbeelding is.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Nieuwe virtuele machines en nieuwe schijven van een platforminstallatiekopie maken

Wanneer u een virtuele machine maakt, moet u bepalen welke toouse besturingssysteem. Hallo imageReference element heeft de gebruikte toodefine Hallo-besturingssysteem van een nieuwe virtuele machine. Hallo-voorbeeld ziet u een definitie voor een Windows-serverbesturingssysteem:

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Als u een Linux-besturingssysteem toocreate wilt, kunt u deze definitie voor:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Configuratie-instellingen voor de besturingssysteemschijf Hallo zijn met Hallo osDisk element toegewezen. Hallo voorbeeld definieert een nieuwe beheerde schijf Hello te opslaan in cache-modus ingesteld**ReadWrite** en die Hallo schijf wordt gemaakt van een [platforminstallatiekopie](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Nieuwe virtuele machines maken van bestaande beheerde schijven

Als u toocreate virtuele machines van de bestaande schijven wilt, verwijder Hallo imageReference en Hallo osProfile elementen en definieer de Schijfinstellingen van deze:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Nieuwe virtuele machines maken van een begeleide afbeelding

Desgewenst kunt u een virtuele machine van een begeleide afbeelding toocreate hello imageReference element wijzigen en definieer de Schijfinstellingen van deze:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Gegevensschijven koppelen

U kunt desgewenst gegevens schijven toohello virtuele machines toevoegen. Hallo [aantal schijven](sizes.md) afhankelijk Hallo grootte van de schijf van het besturingssysteem die u gebruikt. Grootte van virtuele machines Hallo ingesteld Hello tooStandard_DS1_v2, Hallo kunt u het maximum aantal gegevensschijven dat ze is twee toohello kan worden toegevoegd. In Hallo bijvoorbeeld wordt één beheerde gegevensschijf toegevoegd tooeach VM:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Extensies

Hoewel [extensies](extensions-features.md) zijn van een afzonderlijke resource, nauw gebonden tooVMs. Uitbreidingen kunnen worden toegevoegd als een onderliggende resource Hallo VM of als een afzonderlijke resource. Hallo-voorbeeld ziet u Hallo [extensie voor diagnostische gegevens](extensions-diagnostics-template.md) toohello virtuele machines worden toegevoegd:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Deze uitbreiding resource Hallo storageName variabele en diagnostische variabelewaarden tooprovide Hallo gebruikt. Als u toochange Hallo gegevens die door deze uitbreiding worden verzameld wilt, kunt u meer prestaties tellers toohello wadperfcounters variabele toevoegen. U kunt ook tooput Hallo diagnostics-gegevens in een ander opslagaccount dan waar Hallo VM-schijven zijn opgeslagen.

Er zijn veel uitbreidingen die u op een virtuele machine installeren kunt, maar vooral handig Hallo is waarschijnlijk Hallo [aangepaste Scriptextensie](extensions-customscript.md). In voorbeeld hello, een PowerShell-script met de naam start.ps1 wordt uitgevoerd op elke virtuele machine wanneer deze eerst wordt gestart:

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

Hallo start.ps1 script kunt veel configuratietaken uitvoeren. Hallo gegevensschijven die toohello virtuele machines worden toegevoegd in Hallo voorbeeld zijn bijvoorbeeld niet geïnitialiseerd; u kunt een aangepast script tooinitialize ze. Als u meerdere starten van de taken toodo hebt, kunt u Hallo start.ps1 bestand toocall andere PowerShell-scripts in Azure-opslag. Hallo voorbeeld PowerShell gebruikt, maar u kunt elke scripting methode gebruiken die beschikbaar is op het Hallo-besturingssysteem die u gebruikt.

Hallo-status van Hallo geïnstalleerd uitbreidingen van Hallo extensies instellingen in Hallo-portal, kunt u zien:

![Status van extensie ophalen](./media/template-description/virtual-machines-show-extensions.png)

U kunt ook extensie informatie opvragen met behulp van Hallo **Get-AzureRmVMExtension** PowerShell opdracht hello **vm-extensie get** Azure CLI 2.0 opdracht of Hallo **extensie informatie ophalen**  REST-API.

## <a name="deployments"></a>Implementaties

Wanneer u een sjabloon, Azure houdt Hallo bronnen die u hebt geïmplementeerd als een groep en automatisch implementeert, wordt een toothis geïmplementeerd naam groep toegewezen. Hallo-naam van het Hallo-implementatie is dezelfde is als naam van de sjabloon Hallo HALLO hallo.

Als u meer wilt weten over Hallo status van resources in Hallo-implementatie, kunt u de blade resourcegroep Hallo in hello Azure-portal:

![Ophalen van informatie over de implementatie](./media/template-description/virtual-machines-deployment-info.png)
    
Het is niet een probleem toouse Hallo dezelfde sjabloon toocreate resources of tooupdate bestaande resources. Wanneer u opdrachten toodeploy sjablonen gebruikt, hebt u Hallo kans toosay die [modus](../../resource-group-template-deploy.md) gewenste toouse. Hallo-modus kan worden ingesteld op tooeither **Complete** of **incrementele**. Hallo standaardwaarde is toodo incrementele updates. Wees voorzichtig met het gebruik van Hallo **Complete** modus omdat u per ongeluk de resources verwijdert mogelijk. Tijdens het instellen van Hallo-modus te**Complete**, Resource Manager worden alle resources in de resourcegroep Hallo die zich niet in de sjabloon Hallo verwijderd.

## <a name="next-steps"></a>Volgende stappen

- Maak uw eigen sjabloon met [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).
- Hallo-sjabloon die u hebt gemaakt met implementeren [virtuele Windows-machine maken met Resource Manager-sjabloon](ps-template.md).
- Meer informatie over hoe toomanage virtuele machines die u hebt gemaakt aan de hand van Hallo [maken en beheren van Windows-VM's met Azure PowerShell-module Hallo](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
