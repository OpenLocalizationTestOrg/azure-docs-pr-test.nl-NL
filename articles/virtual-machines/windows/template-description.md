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
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="4012d-103">Virtuele machines in een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="4012d-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="4012d-104">Dit artikel wordt beschreven aspecten van een Azure Resource Manager-sjabloon die van toepassing zijn toovirtual machines.</span><span class="sxs-lookup"><span data-stu-id="4012d-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="4012d-105">Een volledige sjabloon voor het maken van een virtuele machine; wordt niet beschreven in dit artikel daarvoor moet u resourcedefinities voor storage-accounts, netwerkinterfaces, openbare IP-adressen en virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="4012d-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="4012d-106">Zie voor meer informatie over hoe deze resources samen kunnen worden gedefinieerd, Hallo [overzicht voor Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="4012d-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="4012d-107">Er zijn veel [sjablonen in de galerie Hallo](https://azure.microsoft.com/documentation/templates/?term=VM) die Hallo VM-resource bevatten.</span><span class="sxs-lookup"><span data-stu-id="4012d-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="4012d-108">Niet alle elementen die kunnen worden opgenomen in een sjabloon worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="4012d-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="4012d-109">Dit voorbeeld toont een typische resource-gedeelte van een sjabloon voor het maken van een opgegeven aantal virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="4012d-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="4012d-110">In dit voorbeeld is afhankelijk van een opslagaccount dat eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4012d-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="4012d-111">U kunt Hallo storage-account maken door het implementeren van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4012d-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="4012d-112">Hallo-voorbeeld is ook afhankelijk van een netwerkinterface en de bijbehorende afhankelijke bronnen die zouden worden gedefinieerd in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4012d-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="4012d-113">Deze resources worden niet weergegeven in het Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4012d-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="4012d-114">API-versie</span><span class="sxs-lookup"><span data-stu-id="4012d-114">API Version</span></span>

<span data-ttu-id="4012d-115">Wanneer u resources met behulp van een sjabloon implementeert, hebt u toospecify een versie van Hallo API toouse.</span><span class="sxs-lookup"><span data-stu-id="4012d-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="4012d-116">Hallo-voorbeeld ziet u de bron van de virtuele machine Hallo met behulp van dit element apiVersion:</span><span class="sxs-lookup"><span data-stu-id="4012d-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="4012d-117">Hallo-versie van Hallo API die u in de sjabloon opgeeft is van invloed op welke eigenschappen u in de sjabloon Hallo kunt definiëren.</span><span class="sxs-lookup"><span data-stu-id="4012d-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="4012d-118">In het algemeen moet u de meest recente API-versie Hallo bij het maken van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="4012d-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="4012d-119">Voor bestaande sjablonen, kunt u beslissen of u wilt dat met een eerdere versie van de API toocontinue of bijwerken van de sjabloon voor Hallo meest recente versie tootake profiteren van nieuwe functies.</span><span class="sxs-lookup"><span data-stu-id="4012d-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="4012d-120">Deze mogelijkheden voor het ophalen van de nieuwste API-versies hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4012d-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="4012d-121">REST-API - [alle resourceproviders vermelden](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="4012d-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="4012d-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="4012d-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="4012d-123">Azure CLI 2.0 - [az provider weergeven](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="4012d-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="4012d-124">Parameters en variabelen</span><span class="sxs-lookup"><span data-stu-id="4012d-124">Parameters and variables</span></span>

<span data-ttu-id="4012d-125">[Parameters](../../resource-group-authoring-templates.md) eenvoudiger voor u toospecify waarden voor Hallo sjabloon wanneer u het uitvoert.</span><span class="sxs-lookup"><span data-stu-id="4012d-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="4012d-126">Deze sectie parameters wordt gebruikt in Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4012d-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="4012d-127">Wanneer u Hallo voorbeeldsjabloon implementeert, voert u de waarden voor Hallo naam en het wachtwoord van Hallo administrator-account voor elke virtuele machine en Hallo aantal virtuele machines toocreate.</span><span class="sxs-lookup"><span data-stu-id="4012d-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="4012d-128">U hebt de optie Hallo van het opgeven van parameterwaarden in een afzonderlijk bestand dat wordt beheerd met Hallo-sjabloon of geef dezelfde waarden als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="4012d-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="4012d-129">[Variabelen](../../resource-group-authoring-templates.md) eenvoudiger voor u tooset waarden in Hallo-sjabloon die in deze herhaaldelijk worden gebruikt of die na verloop van tijd kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4012d-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="4012d-130">Deze sectie variabelen wordt gebruikt in Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4012d-130">This variables section is used in hello example:</span></span>

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

<span data-ttu-id="4012d-131">Wanneer u Hallo voorbeeldsjabloon implementeert, worden de waarden van variabelen worden gebruikt voor Hallo naam en id van het opslagaccount Hallo eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4012d-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="4012d-132">Variabelen zijn ook gebruikte tooprovide Hallo-instellingen voor diagnostische Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="4012d-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="4012d-133">Gebruik Hallo [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](../../resource-manager-template-best-practices.md) toohelp u bepalen hoe u toostructure Hallo parameters en variabelen in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4012d-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="4012d-134">Resource lussen</span><span class="sxs-lookup"><span data-stu-id="4012d-134">Resource loops</span></span>

<span data-ttu-id="4012d-135">Als u meer dan één virtuele machine nodig hebt voor uw toepassing, kunt u een kopie-element in een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4012d-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="4012d-136">Dit element optioneel doorlopen Hallo aantal virtuele machines die u hebt opgegeven als parameter maken:</span><span class="sxs-lookup"><span data-stu-id="4012d-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="4012d-137">In voorbeeld Hallo Hallo lusindex wordt ook gebruikt bij het opgeven aantal Hallo waarden voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="4012d-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="4012d-138">Als u een aantal exemplaren van drie, Hallo namen van Hallo besturingssysteem schijven ingevoerd zijn bijvoorbeeld myOSDisk1, myOSDisk2 en myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="4012d-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="4012d-139">In dit voorbeeld worden beheerde schijven gebruikt voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4012d-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="4012d-140">Houd er rekening mee dat een lus voor één resource maken in de sjabloon Hallo kan u toouse Hallo lus bij het maken of openen van andere bronnen in beslag.</span><span class="sxs-lookup"><span data-stu-id="4012d-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="4012d-141">Meerdere virtuele machines niet dezelfde netwerkinterface, dus als uw sjabloon doorlopen voor het maken van drie virtuele machines die deze ook maken doorlopen moet drie netwerkinterfaces Hallo bijvoorbeeld niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4012d-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="4012d-142">Bij het toewijzen van een network interface tooa VM Hallo lusindex gebruikte tooidentify wordt deze:</span><span class="sxs-lookup"><span data-stu-id="4012d-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="4012d-143">Afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="4012d-143">Dependencies</span></span>

<span data-ttu-id="4012d-144">De meeste bronnen hangen af van andere bronnen toowork correct.</span><span class="sxs-lookup"><span data-stu-id="4012d-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="4012d-145">Virtuele machines moet worden gekoppeld aan een virtueel netwerk en toodo dat het moet een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="4012d-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="4012d-146">Hallo [dependsOn](../../resource-group-define-dependencies.md) element heeft de gebruikte toomake ervoor Hallo netwerkinterface is gereed toobe gebruikt voordat VMs Hallo worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4012d-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="4012d-147">Resource Manager implementeert parallel alle bronnen die zijn niet afhankelijk van een andere resource wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4012d-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="4012d-148">Wees voorzichtig bij het instellen van afhankelijkheden, omdat u uw implementatie per ongeluk afnemen kan door te geven, afhankelijkheden niet nodig.</span><span class="sxs-lookup"><span data-stu-id="4012d-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="4012d-149">Afhankelijkheden kunnen koppelen via meerdere bronnen.</span><span class="sxs-lookup"><span data-stu-id="4012d-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="4012d-150">Bijvoorbeeld, afhankelijk Hallo netwerkinterface Hallo openbaar IP-adres en resources van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="4012d-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="4012d-151">Hoe weet u of een afhankelijkheid vereist is?</span><span class="sxs-lookup"><span data-stu-id="4012d-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="4012d-152">Hallo-waarden in Hallo sjabloon kijken.</span><span class="sxs-lookup"><span data-stu-id="4012d-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="4012d-153">Als een element in de resourcedefinitie Hallo-virtuele machine verwijst tooanother resource die is geïmplementeerd in Hallo dezelfde sjabloon, moet u een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="4012d-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="4012d-154">Uw voorbeeld van de virtuele machine wordt bijvoorbeeld een netwerkprofiel gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="4012d-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="4012d-155">tooset deze eigenschap Hallo netwerkinterface moet bestaan.</span><span class="sxs-lookup"><span data-stu-id="4012d-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="4012d-156">Daarom moet u een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="4012d-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="4012d-157">U moet ook een afhankelijkheid tooset als één resource (een onderliggende) is gedefinieerd in een andere resource (bovenliggend).</span><span class="sxs-lookup"><span data-stu-id="4012d-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="4012d-158">Bijvoorbeeld, Hallo diagnostische instellingen en aangepaste scriptextensies zijn gedefinieerd als onderliggende resources van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4012d-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="4012d-159">Ze kunnen niet worden gemaakt totdat Hallo virtuele machine bestaat.</span><span class="sxs-lookup"><span data-stu-id="4012d-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="4012d-160">Beide resources zijn daarom gemarkeerd als afhankelijke op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4012d-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="4012d-161">Profielen</span><span class="sxs-lookup"><span data-stu-id="4012d-161">Profiles</span></span>

<span data-ttu-id="4012d-162">Verschillende profiel elementen worden gebruikt bij het definiëren van de bron van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4012d-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="4012d-163">Sommige zijn vereist en sommige zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="4012d-163">Some are required and some are optional.</span></span> <span data-ttu-id="4012d-164">Bijvoorbeeld, Hallo het hardwareProfile, osProfile storageProfile en Schaalaanpassingsset elementen zijn vereist, maar Hallo diagnosticsProfile is optioneel.</span><span class="sxs-lookup"><span data-stu-id="4012d-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="4012d-165">Deze profielen definiëren instellingen zoals:</span><span class="sxs-lookup"><span data-stu-id="4012d-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="4012d-166">grootte</span><span class="sxs-lookup"><span data-stu-id="4012d-166">size</span></span>](sizes.md)
- <span data-ttu-id="4012d-167">[naam](/architecture/best-practices/naming-conventions) en referenties</span><span class="sxs-lookup"><span data-stu-id="4012d-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="4012d-168">schijf en [besturingssysteeminstellingen](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="4012d-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="4012d-169">netwerkinterface</span><span class="sxs-lookup"><span data-stu-id="4012d-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="4012d-170">Diagnostische gegevens over opstarten</span><span class="sxs-lookup"><span data-stu-id="4012d-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="4012d-171">Schijven en installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="4012d-171">Disks and images</span></span>
   
<span data-ttu-id="4012d-172">In Azure, vhd-bestanden kunnen geven [schijven of installatiekopieën](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4012d-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="4012d-173">Wanneer het Hallo-besturingssysteem in een vhd-bestand is gespecialiseerde toobe een specifieke virtuele machine, is het waarnaar wordt verwezen tooas een schijf.</span><span class="sxs-lookup"><span data-stu-id="4012d-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="4012d-174">Wanneer het Hallo-besturingssysteem in een vhd-bestand is gegeneraliseerd toobe gebruikt toocreate veel VM's, waarnaar wordt verwezen tooas een afbeelding is.</span><span class="sxs-lookup"><span data-stu-id="4012d-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="4012d-175">Nieuwe virtuele machines en nieuwe schijven van een platforminstallatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="4012d-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="4012d-176">Wanneer u een virtuele machine maakt, moet u bepalen welke toouse besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="4012d-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="4012d-177">Hallo imageReference element heeft de gebruikte toodefine Hallo-besturingssysteem van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4012d-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="4012d-178">Hallo-voorbeeld ziet u een definitie voor een Windows-serverbesturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="4012d-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="4012d-179">Als u een Linux-besturingssysteem toocreate wilt, kunt u deze definitie voor:</span><span class="sxs-lookup"><span data-stu-id="4012d-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="4012d-180">Configuratie-instellingen voor de besturingssysteemschijf Hallo zijn met Hallo osDisk element toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4012d-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="4012d-181">Hallo voorbeeld definieert een nieuwe beheerde schijf Hello te opslaan in cache-modus ingesteld**ReadWrite** en die Hallo schijf wordt gemaakt van een [platforminstallatiekopie](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="4012d-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="4012d-182">Nieuwe virtuele machines maken van bestaande beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="4012d-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="4012d-183">Als u toocreate virtuele machines van de bestaande schijven wilt, verwijder Hallo imageReference en Hallo osProfile elementen en definieer de Schijfinstellingen van deze:</span><span class="sxs-lookup"><span data-stu-id="4012d-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="4012d-184">Nieuwe virtuele machines maken van een begeleide afbeelding</span><span class="sxs-lookup"><span data-stu-id="4012d-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="4012d-185">Desgewenst kunt u een virtuele machine van een begeleide afbeelding toocreate hello imageReference element wijzigen en definieer de Schijfinstellingen van deze:</span><span class="sxs-lookup"><span data-stu-id="4012d-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="4012d-186">Gegevensschijven koppelen</span><span class="sxs-lookup"><span data-stu-id="4012d-186">Attach data disks</span></span>

<span data-ttu-id="4012d-187">U kunt desgewenst gegevens schijven toohello virtuele machines toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4012d-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="4012d-188">Hallo [aantal schijven](sizes.md) afhankelijk Hallo grootte van de schijf van het besturingssysteem die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4012d-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="4012d-189">Grootte van virtuele machines Hallo ingesteld Hello tooStandard_DS1_v2, Hallo kunt u het maximum aantal gegevensschijven dat ze is twee toohello kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4012d-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="4012d-190">In Hallo bijvoorbeeld wordt één beheerde gegevensschijf toegevoegd tooeach VM:</span><span class="sxs-lookup"><span data-stu-id="4012d-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="4012d-191">Extensies</span><span class="sxs-lookup"><span data-stu-id="4012d-191">Extensions</span></span>

<span data-ttu-id="4012d-192">Hoewel [extensies](extensions-features.md) zijn van een afzonderlijke resource, nauw gebonden tooVMs.</span><span class="sxs-lookup"><span data-stu-id="4012d-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="4012d-193">Uitbreidingen kunnen worden toegevoegd als een onderliggende resource Hallo VM of als een afzonderlijke resource.</span><span class="sxs-lookup"><span data-stu-id="4012d-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="4012d-194">Hallo-voorbeeld ziet u Hallo [extensie voor diagnostische gegevens](extensions-diagnostics-template.md) toohello virtuele machines worden toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="4012d-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

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

<span data-ttu-id="4012d-195">Deze uitbreiding resource Hallo storageName variabele en diagnostische variabelewaarden tooprovide Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4012d-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="4012d-196">Als u toochange Hallo gegevens die door deze uitbreiding worden verzameld wilt, kunt u meer prestaties tellers toohello wadperfcounters variabele toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4012d-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="4012d-197">U kunt ook tooput Hallo diagnostics-gegevens in een ander opslagaccount dan waar Hallo VM-schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4012d-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="4012d-198">Er zijn veel uitbreidingen die u op een virtuele machine installeren kunt, maar vooral handig Hallo is waarschijnlijk Hallo [aangepaste Scriptextensie](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="4012d-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="4012d-199">In voorbeeld hello, een PowerShell-script met de naam start.ps1 wordt uitgevoerd op elke virtuele machine wanneer deze eerst wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="4012d-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="4012d-200">Hallo start.ps1 script kunt veel configuratietaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4012d-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="4012d-201">Hallo gegevensschijven die toohello virtuele machines worden toegevoegd in Hallo voorbeeld zijn bijvoorbeeld niet geïnitialiseerd; u kunt een aangepast script tooinitialize ze.</span><span class="sxs-lookup"><span data-stu-id="4012d-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="4012d-202">Als u meerdere starten van de taken toodo hebt, kunt u Hallo start.ps1 bestand toocall andere PowerShell-scripts in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="4012d-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="4012d-203">Hallo voorbeeld PowerShell gebruikt, maar u kunt elke scripting methode gebruiken die beschikbaar is op het Hallo-besturingssysteem die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4012d-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="4012d-204">Hallo-status van Hallo geïnstalleerd uitbreidingen van Hallo extensies instellingen in Hallo-portal, kunt u zien:</span><span class="sxs-lookup"><span data-stu-id="4012d-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Status van extensie ophalen](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="4012d-206">U kunt ook extensie informatie opvragen met behulp van Hallo **Get-AzureRmVMExtension** PowerShell opdracht hello **vm-extensie get** Azure CLI 2.0 opdracht of Hallo **extensie informatie ophalen**  REST-API.</span><span class="sxs-lookup"><span data-stu-id="4012d-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="4012d-207">Implementaties</span><span class="sxs-lookup"><span data-stu-id="4012d-207">Deployments</span></span>

<span data-ttu-id="4012d-208">Wanneer u een sjabloon, Azure houdt Hallo bronnen die u hebt geïmplementeerd als een groep en automatisch implementeert, wordt een toothis geïmplementeerd naam groep toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4012d-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="4012d-209">Hallo-naam van het Hallo-implementatie is dezelfde is als naam van de sjabloon Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="4012d-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="4012d-210">Als u meer wilt weten over Hallo status van resources in Hallo-implementatie, kunt u de blade resourcegroep Hallo in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="4012d-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Ophalen van informatie over de implementatie](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="4012d-212">Het is niet een probleem toouse Hallo dezelfde sjabloon toocreate resources of tooupdate bestaande resources.</span><span class="sxs-lookup"><span data-stu-id="4012d-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="4012d-213">Wanneer u opdrachten toodeploy sjablonen gebruikt, hebt u Hallo kans toosay die [modus](../../resource-group-template-deploy.md) gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="4012d-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="4012d-214">Hallo-modus kan worden ingesteld op tooeither **Complete** of **incrementele**.</span><span class="sxs-lookup"><span data-stu-id="4012d-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="4012d-215">Hallo standaardwaarde is toodo incrementele updates.</span><span class="sxs-lookup"><span data-stu-id="4012d-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="4012d-216">Wees voorzichtig met het gebruik van Hallo **Complete** modus omdat u per ongeluk de resources verwijdert mogelijk.</span><span class="sxs-lookup"><span data-stu-id="4012d-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="4012d-217">Tijdens het instellen van Hallo-modus te**Complete**, Resource Manager worden alle resources in de resourcegroep Hallo die zich niet in de sjabloon Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4012d-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4012d-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4012d-218">Next Steps</span></span>

- <span data-ttu-id="4012d-219">Maak uw eigen sjabloon met [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4012d-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="4012d-220">Hallo-sjabloon die u hebt gemaakt met implementeren [virtuele Windows-machine maken met Resource Manager-sjabloon](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="4012d-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="4012d-221">Meer informatie over hoe toomanage virtuele machines die u hebt gemaakt aan de hand van Hallo [maken en beheren van Windows-VM's met Azure PowerShell-module Hallo](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4012d-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
