---
title: Een virtuele Windows-machine maken van een sjabloon in Azure | Microsoft Docs
description: Gebruik een Resource Manager-sjabloon en PowerShell eenvoudig een nieuwe Windows VM te maken.
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
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="93504-103">Een virtuele Windows-machine maken van een Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="93504-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="93504-104">In dit artikel laat zien hoe een Azure Resource Manager-sjabloon met behulp van PowerShell implementeren.</span><span class="sxs-lookup"><span data-stu-id="93504-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="93504-105">De sjabloon die u maakt implementeert een enkele virtuele machine met Windows Server in een nieuw virtueel netwerk met één subnet.</span><span class="sxs-lookup"><span data-stu-id="93504-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="93504-106">Zie voor een gedetailleerde beschrijving van de bron van de virtuele machine, [virtuele machines in een Azure Resource Manager-sjabloon](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="93504-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="93504-107">Zie voor meer informatie over de resources in een sjabloon [overzicht van Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="93504-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="93504-108">Het moet ongeveer vijf minuten duren voordat de stappen in dit artikel doen.</span><span class="sxs-lookup"><span data-stu-id="93504-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="93504-109">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="93504-109">Install Azure PowerShell</span></span>

<span data-ttu-id="93504-110">Zie [Azure PowerShell installeren en configureren](../../powershell-install-configure.md) voor informatie over het installeren van de nieuwste versie van Azure PowerShell, het selecteren van het abonnement en het aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="93504-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="93504-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="93504-111">Create a resource group</span></span>

<span data-ttu-id="93504-112">Alle bronnen moeten worden geïmplementeerd in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93504-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="93504-113">Haal een lijst op met beschikbare locaties waar resources kunnen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="93504-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="93504-114">De resourcegroep maken in de locatie die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="93504-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="93504-115">In dit voorbeeld toont het maken van een resourcegroep met de naam **myResourceGroup** in de **VS-West** locatie:</span><span class="sxs-lookup"><span data-stu-id="93504-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="93504-116">De bestanden maken</span><span class="sxs-lookup"><span data-stu-id="93504-116">Create the files</span></span>

<span data-ttu-id="93504-117">In deze stap maakt u een sjabloonbestand dat de bronnen implementeert en een parameterbestand dat parameterwaarden voor de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="93504-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="93504-118">U wordt ook een bestand met autorisatieregels die wordt gebruikt voor het Azure Resource Manager-bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="93504-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="93504-119">Maak een bestand met de naam *CreateVMTemplate.json* en voeg deze JSON-code toe:</span><span class="sxs-lookup"><span data-stu-id="93504-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

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

2. <span data-ttu-id="93504-120">Maak een bestand met de naam *Parameters.json* en voeg deze JSON-code toe:</span><span class="sxs-lookup"><span data-stu-id="93504-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

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

3. <span data-ttu-id="93504-121">Maak een nieuw opslagaccount en container:</span><span class="sxs-lookup"><span data-stu-id="93504-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="93504-122">De bestanden uploaden naar het storage-account:</span><span class="sxs-lookup"><span data-stu-id="93504-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="93504-123">Wijzig de - paden naar de locatie waar u de bestanden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="93504-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="93504-124">De resources maken</span><span class="sxs-lookup"><span data-stu-id="93504-124">Create the resources</span></span>

<span data-ttu-id="93504-125">De sjabloon met de parameters implementeren:</span><span class="sxs-lookup"><span data-stu-id="93504-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="93504-126">U kunt ook de parameters van lokale bestanden en sjablonen implementeren.</span><span class="sxs-lookup"><span data-stu-id="93504-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="93504-127">Zie voor meer informatie, [Azure PowerShell gebruiken met Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="93504-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93504-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93504-128">Next Steps</span></span>

- <span data-ttu-id="93504-129">Als er problemen met de implementatie, kunt u eens kijken [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="93504-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="93504-130">Meer informatie over het maken en beheren van een virtuele machine in [maken en beheren van Windows-VM's met de Azure PowerShell-module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93504-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

