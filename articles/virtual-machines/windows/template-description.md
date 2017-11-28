---
title: Virtuele machines in een Azure Resource Manager-sjabloon | Microsoft Azure
description: Meer informatie over hoe de bron van de virtuele machine in een Azure Resource Manager-sjabloon is gedefinieerd.
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
ms.openlocfilehash: d9b9121bc5e38396ba4def6c17f9b373c2b48056
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="8b404-103">Virtuele machines in een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="8b404-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="8b404-104">Dit artikel wordt beschreven aspecten van een Azure Resource Manager-sjabloon die betrekking hebben op virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b404-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="8b404-105">Een volledige sjabloon voor het maken van een virtuele machine; wordt niet beschreven in dit artikel daarvoor moet u resourcedefinities voor storage-accounts, netwerkinterfaces, openbare IP-adressen en virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="8b404-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="8b404-106">Zie voor meer informatie over hoe deze resources samen kunnen worden gedefinieerd, de [overzicht voor Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8b404-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="8b404-107">Er zijn veel [sjablonen in de galerie](https://azure.microsoft.com/documentation/templates/?term=VM) die de VM-resource bevatten.</span><span class="sxs-lookup"><span data-stu-id="8b404-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="8b404-108">Niet alle elementen die kunnen worden opgenomen in een sjabloon worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="8b404-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="8b404-109">Dit voorbeeld toont een typische resource-gedeelte van een sjabloon voor het maken van een opgegeven aantal virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="8b404-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="8b404-110">In dit voorbeeld is afhankelijk van een opslagaccount dat eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8b404-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="8b404-111">U kunt het storage-account maken door het implementeren van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8b404-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="8b404-112">In het voorbeeld is ook afhankelijk van een netwerkinterface en de bijbehorende afhankelijke bronnen die zouden worden gedefinieerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8b404-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="8b404-113">Deze resources worden niet weergegeven in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8b404-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="8b404-114">API-versie</span><span class="sxs-lookup"><span data-stu-id="8b404-114">API Version</span></span>

<span data-ttu-id="8b404-115">Wanneer u resources met behulp van een sjabloon implementeert, moet u opgeven van een versie van de API te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b404-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="8b404-116">Het voorbeeld wordt de bron van de virtuele machine met behulp van dit element apiVersion:</span><span class="sxs-lookup"><span data-stu-id="8b404-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="8b404-117">De versie van de API die u in de sjabloon opgeeft is van invloed op welke eigenschappen u in de sjabloon definiëren kunt.</span><span class="sxs-lookup"><span data-stu-id="8b404-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="8b404-118">In het algemeen moet u de meest recente API-versie selecteren bij het maken van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="8b404-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="8b404-119">Voor bestaande sjablonen, kunt u beslissen of u wilt doorgaan met een eerdere versie van de API of de sjabloon voor de nieuwste versie om te profiteren van nieuwe functies bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="8b404-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="8b404-120">Gebruik deze mogelijkheden voor het ophalen van de nieuwste API-versies:</span><span class="sxs-lookup"><span data-stu-id="8b404-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="8b404-121">REST-API - [alle resourceproviders vermelden](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="8b404-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="8b404-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="8b404-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="8b404-123">Azure CLI 2.0 - [az provider weergeven](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="8b404-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="8b404-124">Parameters en variabelen</span><span class="sxs-lookup"><span data-stu-id="8b404-124">Parameters and variables</span></span>

<span data-ttu-id="8b404-125">[Parameters](../../resource-group-authoring-templates.md) eenvoudiger voor u waarden opgeven voor de sjabloon wanneer u het uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8b404-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="8b404-126">Deze sectie parameters wordt gebruikt in het voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8b404-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="8b404-127">Wanneer u de voorbeeldsjabloon implementeert, voert u de waarden voor de naam en het wachtwoord van de administrator-account op elke virtuele machine en het aantal virtuele machines te maken.</span><span class="sxs-lookup"><span data-stu-id="8b404-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="8b404-128">U hebt de mogelijkheid voor het opgeven van parameterwaarden in een afzonderlijk bestand dat wordt beheerd met de sjabloon of geef dezelfde waarden als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="8b404-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="8b404-129">[Variabelen](../../resource-group-authoring-templates.md) eenvoudig instellen van waarden in de sjabloon die in deze herhaaldelijk worden gebruikt of die na verloop van tijd kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8b404-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="8b404-130">Deze sectie variabelen wordt gebruikt in het voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8b404-130">This variables section is used in the example:</span></span>

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

<span data-ttu-id="8b404-131">Wanneer u de voorbeeldsjabloon implementeert, worden de waarden van variabelen voor de naam en de id van het eerder gemaakte opslagaccount gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b404-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="8b404-132">Variabelen worden ook gebruikt om de instellingen voor de extensie voor diagnostische te geven.</span><span class="sxs-lookup"><span data-stu-id="8b404-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="8b404-133">Gebruik de [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](../../resource-manager-template-best-practices.md) om te bepalen hoe u wilt de structuur van de parameters en variabelen in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8b404-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="8b404-134">Resource lussen</span><span class="sxs-lookup"><span data-stu-id="8b404-134">Resource loops</span></span>

<span data-ttu-id="8b404-135">Als u meer dan één virtuele machine nodig hebt voor uw toepassing, kunt u een kopie-element in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8b404-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="8b404-136">Dit element optioneel doorlopen voor het maken van het aantal virtuele machines die u als een parameter opgegeven:</span><span class="sxs-lookup"><span data-stu-id="8b404-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="8b404-137">U ziet ook in het voorbeeld dat de lusindex wordt gebruikt bij het opgeven van sommige van de waarden voor de resource.</span><span class="sxs-lookup"><span data-stu-id="8b404-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="8b404-138">Als u een aantal exemplaren van drie hebt ingevoerd, zijn de namen van de schijven van het besturingssysteem bijvoorbeeld myOSDisk1, myOSDisk2 en myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="8b404-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="8b404-139">In dit voorbeeld worden beheerde schijven gebruikt voor de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b404-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="8b404-140">Houd er rekening mee dat het maken van een lus voor één resource in de sjabloon mogelijk wanneer u het gebruik van de lus bij het maken of openen van andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="8b404-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="8b404-141">Bijvoorbeeld kunnen meerdere virtuele machines gebruiken dezelfde netwerkinterface als uw sjabloon doorlopen drie virtuele machines maken ook herhalen moet bij het maken van drie netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="8b404-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="8b404-142">Wanneer u een netwerkinterface toewijst aan een VM, wordt de lusindex wordt gebruikt bij het identificeren ervan:</span><span class="sxs-lookup"><span data-stu-id="8b404-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="8b404-143">Afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="8b404-143">Dependencies</span></span>

<span data-ttu-id="8b404-144">De meeste bronnen afhankelijk zijn van andere bronnen correct te laten werken.</span><span class="sxs-lookup"><span data-stu-id="8b404-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="8b404-145">Virtuele machines moet worden gekoppeld aan een virtueel netwerk en dat het een netwerkinterface moet doen.</span><span class="sxs-lookup"><span data-stu-id="8b404-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="8b404-146">De [dependsOn](../../resource-group-define-dependencies.md) element wordt gebruikt om ervoor te zorgen dat de netwerkinterface gereed om te worden gebruikt is voordat de virtuele machines worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="8b404-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="8b404-147">Resource Manager implementeert parallel alle bronnen die zijn niet afhankelijk van een andere resource wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8b404-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="8b404-148">Wees voorzichtig bij het instellen van afhankelijkheden, omdat u uw implementatie per ongeluk afnemen kan door te geven, afhankelijkheden niet nodig.</span><span class="sxs-lookup"><span data-stu-id="8b404-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="8b404-149">Afhankelijkheden kunnen koppelen via meerdere bronnen.</span><span class="sxs-lookup"><span data-stu-id="8b404-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="8b404-150">Bijvoorbeeld, de netwerkinterface is afhankelijk van het openbare IP-adres en virtuele netwerkbronnen.</span><span class="sxs-lookup"><span data-stu-id="8b404-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="8b404-151">Hoe weet u of een afhankelijkheid vereist is?</span><span class="sxs-lookup"><span data-stu-id="8b404-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="8b404-152">Bekijk de waarden die u in de sjabloon is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8b404-152">Look at the values you set in the template.</span></span> <span data-ttu-id="8b404-153">Als een element in de virtuele machine resource definition verwijst naar een andere resource die wordt geïmplementeerd in dezelfde sjabloon, moet u een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="8b404-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="8b404-154">Uw voorbeeld van de virtuele machine wordt bijvoorbeeld een netwerkprofiel gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="8b404-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="8b404-155">Deze eigenschap wilt instellen, moet de netwerkinterface bestaan.</span><span class="sxs-lookup"><span data-stu-id="8b404-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="8b404-156">Daarom moet u een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="8b404-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="8b404-157">U moet ook een afhankelijkheid ingesteld als één resource (een onderliggende) is gedefinieerd in een andere resource (bovenliggend).</span><span class="sxs-lookup"><span data-stu-id="8b404-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="8b404-158">Bijvoorbeeld, de diagnostische instellingen en aangepaste scriptextensies zijn gedefinieerd als onderliggende resources van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b404-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="8b404-159">Ze kunnen niet worden gemaakt totdat de virtuele machine bestaat.</span><span class="sxs-lookup"><span data-stu-id="8b404-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="8b404-160">Beide resources zijn daarom gemarkeerd als afhankelijk van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b404-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="8b404-161">Profielen</span><span class="sxs-lookup"><span data-stu-id="8b404-161">Profiles</span></span>

<span data-ttu-id="8b404-162">Verschillende profiel elementen worden gebruikt bij het definiëren van de bron van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b404-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="8b404-163">Sommige zijn vereist en sommige zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="8b404-163">Some are required and some are optional.</span></span> <span data-ttu-id="8b404-164">Bijvoorbeeld, het hardwareProfile, osProfile storageProfile en Schaalaanpassingsset elementen zijn vereist, maar de diagnosticsProfile is optioneel.</span><span class="sxs-lookup"><span data-stu-id="8b404-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="8b404-165">Deze profielen definiëren instellingen zoals:</span><span class="sxs-lookup"><span data-stu-id="8b404-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="8b404-166">grootte</span><span class="sxs-lookup"><span data-stu-id="8b404-166">size</span></span>](sizes.md)
- <span data-ttu-id="8b404-167">[naam](/architecture/best-practices/naming-conventions) en referenties</span><span class="sxs-lookup"><span data-stu-id="8b404-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="8b404-168">schijf en [besturingssysteeminstellingen](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="8b404-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="8b404-169">netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="8b404-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="8b404-170">Diagnostische gegevens over opstarten</span><span class="sxs-lookup"><span data-stu-id="8b404-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="8b404-171">Schijven en installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="8b404-171">Disks and images</span></span>
   
<span data-ttu-id="8b404-172">In Azure, vhd-bestanden kunnen geven [schijven of installatiekopieën](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b404-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8b404-173">Wanneer het besturingssysteem in een vhd-bestand is speciaal bedoeld om te worden van een specifieke virtuele machine, wordt dit aangeduid als een schijf.</span><span class="sxs-lookup"><span data-stu-id="8b404-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="8b404-174">Wanneer het besturingssysteem in een vhd-bestand is gegeneraliseerd moeten worden gebruikt voor het maken van veel VM's, wordt dit aangeduid als een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="8b404-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="8b404-175">Nieuwe virtuele machines en nieuwe schijven van een platforminstallatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="8b404-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="8b404-176">Wanneer u een virtuele machine maakt, moet u bepalen welk besturingssysteem moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b404-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="8b404-177">Het element imageReference wordt gebruikt voor het definiëren van het besturingssysteem van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8b404-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="8b404-178">Het voorbeeld toont een definitie voor een Windows-serverbesturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="8b404-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="8b404-179">Als u maken van een Linux-besturingssysteem wilt, kunt u deze definitie voor:</span><span class="sxs-lookup"><span data-stu-id="8b404-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="8b404-180">Configuratie-instellingen voor de besturingssysteemschijf zijn toegewezen aan het element osDisk.</span><span class="sxs-lookup"><span data-stu-id="8b404-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="8b404-181">Het voorbeeld wordt een nieuwe beheerde schijf gedefinieerd met de cache-modus ingesteld op **ReadWrite** en dat de schijf wordt gemaakt van een [platforminstallatiekopie](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="8b404-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="8b404-182">Nieuwe virtuele machines maken van bestaande beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="8b404-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="8b404-183">Als u maken van virtuele machines van bestaande schijven wilt, verwijder de imageReference en de osProfile-elementen en definieer de Schijfinstellingen van deze:</span><span class="sxs-lookup"><span data-stu-id="8b404-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="8b404-184">Nieuwe virtuele machines maken van een begeleide afbeelding</span><span class="sxs-lookup"><span data-stu-id="8b404-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="8b404-185">Als u maken van een virtuele machine van een begeleide afbeelding wilt, wijzigen van het element imageReference en definieer de Schijfinstellingen van deze:</span><span class="sxs-lookup"><span data-stu-id="8b404-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="8b404-186">Gegevensschijven koppelen</span><span class="sxs-lookup"><span data-stu-id="8b404-186">Attach data disks</span></span>

<span data-ttu-id="8b404-187">U kunt eventueel gegevensschijven toevoegen aan de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b404-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="8b404-188">De [aantal schijven](sizes.md) is afhankelijk van de grootte van de schijf van het besturingssysteem die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b404-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="8b404-189">Met de grootte van de virtuele machines ingesteld op Standard_DS1_v2, is het maximum aantal gegevensschijven dat kan worden toegevoegd aan deze twee.</span><span class="sxs-lookup"><span data-stu-id="8b404-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="8b404-190">In het voorbeeld wordt wordt een beheerde gegevensschijf toegevoegd aan elke virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="8b404-190">In the example, one managed data disk is being added to each VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="8b404-191">Extensies</span><span class="sxs-lookup"><span data-stu-id="8b404-191">Extensions</span></span>

<span data-ttu-id="8b404-192">Hoewel [extensies](extensions-features.md) zijn van een afzonderlijke resource, ze zijn nauw gekoppeld aan virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8b404-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="8b404-193">Uitbreidingen kunnen worden toegevoegd als een onderliggende resource van de virtuele machine of als een afzonderlijke resource.</span><span class="sxs-lookup"><span data-stu-id="8b404-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="8b404-194">Het voorbeeld ziet u de [extensie voor diagnostische gegevens](extensions-diagnostics-template.md) wordt toegevoegd aan de virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="8b404-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

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

<span data-ttu-id="8b404-195">Deze extensie-resource maakt gebruik van de variabele storageName en de diagnostische variabelen waarden op te geven.</span><span class="sxs-lookup"><span data-stu-id="8b404-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="8b404-196">Als u wijzigen van de gegevens die door deze uitbreiding is verzameld wilt, kunt u meer prestatiemeteritems toevoegen aan de variabele wadperfcounters.</span><span class="sxs-lookup"><span data-stu-id="8b404-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="8b404-197">U kunt ook plaats de diagnostics-gegevens in een ander opslagaccount dan waar de VM-schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8b404-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="8b404-198">Er zijn veel uitbreidingen die u op een virtuele machine installeren kunt, maar het meest geschikt is waarschijnlijk het [aangepaste Scriptextensie](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="8b404-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="8b404-199">In het voorbeeld wordt een PowerShell-script met de naam start.ps1 wordt uitgevoerd op elke virtuele machine wanneer deze eerst wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="8b404-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="8b404-200">Het script start.ps1 kunt veel configuratietaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8b404-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="8b404-201">De gegevensschijven die zijn toegevoegd aan de virtuele machines in het voorbeeld zijn bijvoorbeeld niet geïnitialiseerd; u kunt een aangepast script gebruiken ze initialiseren.</span><span class="sxs-lookup"><span data-stu-id="8b404-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="8b404-202">Als er meerdere starten van de taken te doen, kunt u het bestand start.ps1 aan te roepen andere PowerShell-scripts in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="8b404-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="8b404-203">In het voorbeeld PowerShell gebruikt, maar u kunt elke scripting methode gebruiken die beschikbaar is op het besturingssysteem die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b404-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="8b404-204">Hier ziet u de status van de geïnstalleerde uitbreidingen van de instellingen van de uitbreidingen in de portal:</span><span class="sxs-lookup"><span data-stu-id="8b404-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![Status van extensie ophalen](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="8b404-206">U kunt ook extensie informatie opvragen met behulp van de **Get-AzureRmVMExtension** PowerShell-opdracht de **vm-extensie get** Azure CLI 2.0-opdracht, of de **extensiegegevensophalen** REST-API.</span><span class="sxs-lookup"><span data-stu-id="8b404-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="8b404-207">Implementaties</span><span class="sxs-lookup"><span data-stu-id="8b404-207">Deployments</span></span>

<span data-ttu-id="8b404-208">Wanneer u een sjabloon implementeert, worden de resources geïmplementeerd als een groep uit te voeren en automatisch een naam toegewezen aan deze groep geïmplementeerde bijgehouden in Azure.</span><span class="sxs-lookup"><span data-stu-id="8b404-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="8b404-209">De naam van de implementatie is hetzelfde als de naam van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8b404-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="8b404-210">Als u meer wilt weten over de status van resources in de implementatie, kunt u de blade resourcegroep in de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="8b404-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![Ophalen van informatie over de implementatie](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="8b404-212">Het is niet een probleem met de dezelfde sjabloon gebruiken om resources te maken of bijwerken van bestaande resources.</span><span class="sxs-lookup"><span data-stu-id="8b404-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="8b404-213">Wanneer u opdrachten gebruiken om sjablonen te implementeren, hebt u de mogelijkheid om in te spreken die [modus](../../resource-group-template-deploy.md) u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b404-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="8b404-214">De modus kan worden ingesteld op **Complete** of **incrementele**.</span><span class="sxs-lookup"><span data-stu-id="8b404-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="8b404-215">De standaardwaarde is doen incrementele updates.</span><span class="sxs-lookup"><span data-stu-id="8b404-215">The default is to do incremental updates.</span></span> <span data-ttu-id="8b404-216">Wees voorzichtig wanneer u de **Complete** modus omdat u per ongeluk de resources verwijdert mogelijk.</span><span class="sxs-lookup"><span data-stu-id="8b404-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="8b404-217">Als u de modus instelt op **Complete**, Resource Manager alle resources in de resourcegroep die zich niet in de sjabloon wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8b404-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b404-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b404-218">Next Steps</span></span>

- <span data-ttu-id="8b404-219">Maak uw eigen sjabloon met [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8b404-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="8b404-220">Implementeren van de sjabloon die u hebt gemaakt met [virtuele Windows-machine maken met Resource Manager-sjabloon](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="8b404-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="8b404-221">Informatie over het beheren van de virtuele machines die u hebt gemaakt aan de hand van [maken en beheren van Windows-VM's met de Azure PowerShell-module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b404-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
