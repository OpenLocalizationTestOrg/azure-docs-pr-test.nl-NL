---
title: een Windows-VM met een sjabloon in Azure aaaCreate | Microsoft Docs
description: Gebruik Resource Manager-sjabloon en PowerShell tooeasily Maak een nieuwe Windows VM.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="aa8f6-103">Een virtuele Windows-machine maken van een Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="aa8f6-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="aa8f6-104">Dit artikel ziet u hoe toodeploy een Azure Resource Manager-sjabloon met gebruik van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="aa8f6-105">Hallo-sjabloon die u maakt implementeert een enkele virtuele machine met Windows Server in een nieuw virtueel netwerk met één subnet.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="aa8f6-106">Zie voor een gedetailleerde beschrijving van de bron van de virtuele machine Hallo [virtuele machines in een Azure Resource Manager-sjabloon](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="aa8f6-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="aa8f6-107">Zie voor meer informatie over alle Hallo resources in een sjabloon [overzicht van Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="aa8f6-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="aa8f6-108">Het duurt ongeveer 5 minuten toodo Hallo in dit artikel stappen.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="aa8f6-109">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="aa8f6-109">Install Azure PowerShell</span></span>

<span data-ttu-id="aa8f6-110">Zie [hoe tooinstall en configureren van Azure PowerShell](../../powershell-install-configure.md) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="aa8f6-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="aa8f6-111">Create a resource group</span></span>

<span data-ttu-id="aa8f6-112">Alle bronnen moeten worden geïmplementeerd in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa8f6-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="aa8f6-113">Haal een lijst op met beschikbare locaties waar resources kunnen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="aa8f6-114">Hallo-resourcegroep maken op Hallo locatie die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="aa8f6-115">Dit voorbeeld ziet u het maken van een resourcegroep met de naam van Hallo **myResourceGroup** in Hallo **VS-West** locatie:</span><span class="sxs-lookup"><span data-stu-id="aa8f6-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="aa8f6-116">Hallo-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="aa8f6-116">Create hello files</span></span>

<span data-ttu-id="aa8f6-117">In deze stap maakt u een sjabloonbestand die Hallo resources implementeert en een parameterbestand dat parameter waarden toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="aa8f6-118">U wordt ook een bestand met autorisatieregels die gebruikte tooperform Azure Resource Manager-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="aa8f6-119">Maak een bestand met de naam *CreateVMTemplate.json* en voeg deze code JSON tooit:</span><span class="sxs-lookup"><span data-stu-id="aa8f6-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
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
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="aa8f6-120">Maak een bestand met de naam *Parameters.json* en voeg deze code JSON tooit:</span><span class="sxs-lookup"><span data-stu-id="aa8f6-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="aa8f6-121">Maak een nieuw opslagaccount en container:</span><span class="sxs-lookup"><span data-stu-id="aa8f6-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="aa8f6-122">Hallo bestanden toohello storage-account uploaden:</span><span class="sxs-lookup"><span data-stu-id="aa8f6-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="aa8f6-123">Wijziging Hallo - paden toohello bestandslocatie waar u Hallo-bestanden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="aa8f6-124">Hallo resources maken</span><span class="sxs-lookup"><span data-stu-id="aa8f6-124">Create hello resources</span></span>

<span data-ttu-id="aa8f6-125">Hallo-sjabloon met gebruik van parameters Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="aa8f6-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="aa8f6-126">U kunt ook de parameters van lokale bestanden en sjablonen implementeren.</span><span class="sxs-lookup"><span data-stu-id="aa8f6-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="aa8f6-127">toolearn meer, Zie [Azure PowerShell gebruiken met Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="aa8f6-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa8f6-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa8f6-128">Next Steps</span></span>

- <span data-ttu-id="aa8f6-129">Als er problemen met de Hallo-implementatie, kunt u eens kijken [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="aa8f6-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="aa8f6-130">Meer informatie over hoe toocreate en beheren van een virtuele machine in [maken en beheren van Windows-VM's met Azure PowerShell-module Hallo](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa8f6-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

