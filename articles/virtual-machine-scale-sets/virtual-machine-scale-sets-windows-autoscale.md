---
title: Automatisch schalen Windows virtuele-Machineschaalsets | Microsoft Docs
description: Automatisch schalen instellen voor een Windows virtuele-Machineschaalset met Azure PowerShell
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 91f731bec46c005221f4e66e95822994070d4c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="4c74d-103">Automatisch schalen machines in een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="4c74d-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="4c74d-104">Virtuele-machineschaalsets kunnen gemakkelijk te implementeren en beheren van identieke virtuele machines als een set.</span><span class="sxs-lookup"><span data-stu-id="4c74d-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="4c74d-105">Schaalsets bieden een uiterst schaalbare en aanpasbare berekeningslaag voor toepassingen die grootschalig en installatiekopieën voor Windows-platform, installatiekopieën van virtuele Linux-platform, aangepaste installatiekopieën en -extensies ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="4c74d-106">Zie voor meer informatie over schaalsets [virtuele Machine Scale ingesteld](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c74d-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="4c74d-107">Deze zelfstudie laat zien hoe u een scale set Windows virtuele machines maken en de machines automatisch schalen in de set.</span><span class="sxs-lookup"><span data-stu-id="4c74d-107">This tutorial shows you how to create a scale set of Windows virtual machines and automatically scale the machines in the set.</span></span> <span data-ttu-id="4c74d-108">Hebt u de schaal en instellen schalen door een Azure Resource Manager-sjabloon maken en implementeren met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c74d-108">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="4c74d-109">Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) voor meer informatie over sjablonen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="4c74d-110">Zie voor meer informatie over automatisch schalen van schaalsets, [automatisch schalen en Virtual Machine-schaal stelt](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c74d-110">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="4c74d-111">In dit artikel implementeert u de volgende bronnen en -extensies:</span><span class="sxs-lookup"><span data-stu-id="4c74d-111">In this article, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="4c74d-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="4c74d-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="4c74d-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="4c74d-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="4c74d-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="4c74d-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="4c74d-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="4c74d-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="4c74d-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="4c74d-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="4c74d-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="4c74d-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="4c74d-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="4c74d-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="4c74d-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="4c74d-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="4c74d-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="4c74d-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="4c74d-121">Zie voor meer informatie over het Resource Manager-resources [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4c74d-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="4c74d-122">Stap 1: Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="4c74d-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="4c74d-123">Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) selecteren voor informatie over het installeren van de meest recente versie van Azure PowerShell, uw abonnement en aanmelden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="4c74d-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to Azure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="4c74d-124">Stap 2: Een resourcegroep en een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="4c74d-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="4c74d-125">**Een resourcegroep maken** – alle bronnen moeten worden geïmplementeerd in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4c74d-125">**Create a resource group** – All resources must be deployed to a resource group.</span></span> <span data-ttu-id="4c74d-126">Gebruik [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) voor het maken van een resourcegroep met de naam **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="4c74d-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) to create a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="4c74d-127">**Een opslagaccount maken** – dit opslagaccount is waar de sjabloon is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-127">**Create a storage account** – This storage account is where the template is stored.</span></span> <span data-ttu-id="4c74d-128">Gebruik [nieuw AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) voor het maken van een opslagaccount met de naam **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="4c74d-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) to create a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-the-template"></a><span data-ttu-id="4c74d-129">Stap 3: De sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="4c74d-129">Step 3: Create the template</span></span>
<span data-ttu-id="4c74d-130">Een Azure Resource Manager-sjabloon maakt het u mogelijk te implementeren en beheren van de Azure-resources samen met behulp van een JSON-beschrijving van de resources en de bijbehorende implementatie-parameters.</span><span class="sxs-lookup"><span data-stu-id="4c74d-130">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="4c74d-131">In uw favoriete editor het bestand C:\VMSSTemplate.json maken en voeg de initiële JSON-structuur ter ondersteuning van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4c74d-131">In your favorite editor, create the file C:\VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="4c74d-132">Parameters zijn niet altijd vereist, maar ze bieden een manier voor het invoeren van waarden wanneer de sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4c74d-132">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="4c74d-133">Deze parameters onder het bovenliggende element voor parameters die u hebt toegevoegd aan de sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-133">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="4c74d-134">Een naam voor de afzonderlijke virtuele machine die wordt gebruikt voor toegang tot de machines in de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4c74d-134">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
    * <span data-ttu-id="4c74d-135">De naam van het opslagaccount waarin de sjabloon is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-135">The name of the storage account where the template is stored.</span></span>
    * <span data-ttu-id="4c74d-136">Het aantal virtuele machines in eerste instantie maken in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="4c74d-136">The number of virtual machines to initially create in the scale set.</span></span>
    * <span data-ttu-id="4c74d-137">De naam en het wachtwoord van de administrator-account op de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4c74d-137">The name and password of the administrator account on the virtual machines.</span></span>
    * <span data-ttu-id="4c74d-138">Een voorvoegsel voor de resources die worden gemaakt ter ondersteuning van de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4c74d-138">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="4c74d-139">Variabelen kunnen worden gebruikt in een sjabloon om op te geven waarden die kunnen worden regelmatig gewijzigd of waarden die moeten worden gemaakt uit een combinatie van parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="4c74d-139">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="4c74d-140">Deze variabelen onder het bovenliggende element van variabelen die u hebt toegevoegd aan de sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-140">Add these variables under the variables parent element that you added to the template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="4c74d-141">DNS-namen die door de netwerkinterfaces worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4c74d-141">DNS names that are used by the network interfaces.</span></span>

        * <span data-ttu-id="4c74d-142">De namen van de IP-adres en de voorvoegsels voor het virtuele netwerk en de subnetten.</span><span class="sxs-lookup"><span data-stu-id="4c74d-142">The IP address names and prefixes for the virtual network and subnets.</span></span>
        * <span data-ttu-id="4c74d-143">De namen en id's van het virtuele netwerk en voor de load balancer, netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="4c74d-143">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="4c74d-144">Namen van opslagaccounts voor de accounts die zijn gekoppeld aan de computers in de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4c74d-144">Storage account names for the accounts associated with the machines in the scale set.</span></span>
        * <span data-ttu-id="4c74d-145">Instellingen voor de extensie voor diagnostische gegevens die op de virtuele machines is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4c74d-145">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="4c74d-146">Zie voor meer informatie over de extensie voor diagnostische gegevens [maken van een virtuele Windows-machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c74d-146">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="4c74d-147">De storage-account resource onder het bovenliggende element van resources die u hebt toegevoegd aan de sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-147">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="4c74d-148">Deze sjabloon worden gebruikt voor een lus aanbevolen vijf storage-accounts maken waarin het besturingssysteem schijven en diagnostische gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-148">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="4c74d-149">Deze set accounts kan maximaal 100 virtuele machines in een schaalset, de huidige maximale is ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-149">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="4c74d-150">De naam van elk opslagaccount is met een letter eenheidsaanduiding die is gedefinieerd in de variabelen die in combinatie met het voorvoegsel op dat u in de parameters voor de sjabloon opgeeft.</span><span class="sxs-lookup"><span data-stu-id="4c74d-150">Each storage account is named with a letter designator that was defined in the variables combined with the prefix that you provide in the parameters for the template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="4c74d-151">Het virtuele netwerk resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-151">Add the virtual network resource.</span></span> <span data-ttu-id="4c74d-152">Zie voor meer informatie [Netwerkresourceprovider](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="4c74d-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="4c74d-153">Het openbare IP-adres resources die worden gebruikt door de load balancer en network interface toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-153">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="4c74d-154">De load balancer-resource die wordt gebruikt door de schaalaanpassingsset toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-154">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="4c74d-155">Zie voor meer informatie [Azure Resource Manager-ondersteuning voor de Load Balancer](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4c74d-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="4c74d-156">De netwerkbron van de interface die wordt gebruikt door de afzonderlijke virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-156">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="4c74d-157">Omdat computers in een scale-set niet toegankelijk zijn via een openbaar IP-adres, wordt een aparte virtuele machine gemaakt in hetzelfde virtuele netwerk voor extern toegang tot de machines.</span><span class="sxs-lookup"><span data-stu-id="4c74d-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="4c74d-158">De afzonderlijke virtuele machine in hetzelfde netwerk bevindt als de scale-set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-158">Add the separate virtual machine in the same network as the scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
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
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="4c74d-159">De virtuele-machineschaalset resource toevoegen en geef de extensie voor diagnostische gegevens die is geïnstalleerd op alle virtuele machines in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="4c74d-159">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="4c74d-160">Veel van de instellingen voor deze resource zijn vergelijkbaar met de bron van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4c74d-160">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="4c74d-161">De belangrijkste verschillen zijn de capaciteit-element waarmee het aantal virtuele machines in de schaalset en upgradePolicy waarmee wordt aangegeven hoe updates worden aangebracht in virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4c74d-161">The main differences are the capacity element that specifies the number of virtual machines in the scale set, and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="4c74d-162">De set scale is niet gemaakt totdat alle opslagaccounts zijn gemaakt met het element dependsOn zoals is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="4c74d-162">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="4c74d-163">De resource autoscaleSettings die definieert hoe de schaalaanpassingsset worden aangepast op basis van het processorgebruik op de virtuele machines in de schaalset toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-163">Add the autoscaleSettings resource that defines how the scale set adjusts based on the processor usage on the machines in the scale set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="4c74d-164">Deze waarden zijn belangrijk voor deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="4c74d-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="4c74d-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="4c74d-165">**metricName**</span></span>  
    <span data-ttu-id="4c74d-166">Deze waarde is hetzelfde als het prestatiemeteritem dat is gedefinieerd in de variabele wadperfcounter.</span><span class="sxs-lookup"><span data-stu-id="4c74d-166">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="4c74d-167">De extensie voor diagnostische gegevens worden verzameld met behulp van die variabele, de **processor(_Totaal)\% processortijd** teller.</span><span class="sxs-lookup"><span data-stu-id="4c74d-167">Using that variable, the Diagnostics extension collects the  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="4c74d-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="4c74d-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="4c74d-169">Deze waarde is de resource-id van de virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="4c74d-169">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="4c74d-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="4c74d-170">**timeGrain**</span></span>  
    <span data-ttu-id="4c74d-171">Deze waarde is de granulatie van de metrische gegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="4c74d-171">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="4c74d-172">In deze sjabloon wordt deze ingesteld op 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="4c74d-172">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="4c74d-173">**statistiek**</span><span class="sxs-lookup"><span data-stu-id="4c74d-173">**statistic**</span></span>  
    <span data-ttu-id="4c74d-174">Deze waarde bepaalt hoe de metrische gegevens voor het automatisch vergroten/verkleinen actie worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="4c74d-174">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="4c74d-175">De mogelijke waarden zijn: gemiddelde, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="4c74d-175">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="4c74d-176">Het gemiddelde totale CPU-gebruik van de virtuele machines in deze sjabloon is verzameld.</span><span class="sxs-lookup"><span data-stu-id="4c74d-176">In this template, the average total CPU usage of the virtual machines is collected.</span></span>
    
    * <span data-ttu-id="4c74d-177">**waarde voor timeWindow**</span><span class="sxs-lookup"><span data-stu-id="4c74d-177">**timeWindow**</span></span>  
    <span data-ttu-id="4c74d-178">Deze waarde is het tijdbereik waarin de gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="4c74d-178">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="4c74d-179">Deze moet tussen 5 minuten en 12 uur.</span><span class="sxs-lookup"><span data-stu-id="4c74d-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="4c74d-180">**TimeAggregation van**</span><span class="sxs-lookup"><span data-stu-id="4c74d-180">**timeAggregation**</span></span>  
    <span data-ttu-id="4c74d-181">de waarde bepaalt hoe de gegevens die worden verzameld gedurende een bepaalde periode moeten worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="4c74d-181">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="4c74d-182">De standaardwaarde is de gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="4c74d-182">The default value is Average.</span></span> <span data-ttu-id="4c74d-183">De mogelijke waarden zijn: gemiddeld, Minimum, Maximum, laatste, totaal, Count.</span><span class="sxs-lookup"><span data-stu-id="4c74d-183">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="4c74d-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="4c74d-184">**operator**</span></span>  
    <span data-ttu-id="4c74d-185">Deze waarde is de operator die wordt gebruikt om de metrische gegevens en de drempelwaarde te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="4c74d-185">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="4c74d-186">De mogelijke waarden zijn: gelijk is aan NotEquals, groter dan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="4c74d-186">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="4c74d-187">**drempelwaarde**</span><span class="sxs-lookup"><span data-stu-id="4c74d-187">**threshold**</span></span>  
    <span data-ttu-id="4c74d-188">Deze waarde is de waarde die de schaalactie activeert.</span><span class="sxs-lookup"><span data-stu-id="4c74d-188">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="4c74d-189">Machines worden in deze sjabloon wordt toegevoegd aan de schaal ingesteld als het gemiddelde CPU-gebruik door machines in de set meer dan 50 is %.</span><span class="sxs-lookup"><span data-stu-id="4c74d-189">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="4c74d-190">**richting**</span><span class="sxs-lookup"><span data-stu-id="4c74d-190">**direction**</span></span>  
    <span data-ttu-id="4c74d-191">Deze waarde bepaalt de actie die wordt uitgevoerd wanneer de drempelwaarde wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="4c74d-191">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="4c74d-192">De mogelijke waarden zijn vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-192">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="4c74d-193">In deze sjabloon wordt het aantal virtuele machines in de schaalset verhoogd als de drempelwaarde meer dan 50% van de gedefinieerde tijdsduur is.</span><span class="sxs-lookup"><span data-stu-id="4c74d-193">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>
    
    * <span data-ttu-id="4c74d-194">**type**</span><span class="sxs-lookup"><span data-stu-id="4c74d-194">**type**</span></span>  
    <span data-ttu-id="4c74d-195">Deze waarde is het type actie die moet worden uitgevoerd en moet worden ingesteld op ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="4c74d-195">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="4c74d-196">**waarde**</span><span class="sxs-lookup"><span data-stu-id="4c74d-196">**value**</span></span>  
    <span data-ttu-id="4c74d-197">Deze waarde is het aantal virtuele machines die worden toegevoegd of verwijderd uit de schaalaanpassingsset.</span><span class="sxs-lookup"><span data-stu-id="4c74d-197">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="4c74d-198">Deze waarde moet 1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4c74d-198">This value must be 1 or greater.</span></span> <span data-ttu-id="4c74d-199">De standaardwaarde is 1.</span><span class="sxs-lookup"><span data-stu-id="4c74d-199">The default value is 1.</span></span> <span data-ttu-id="4c74d-200">In deze sjabloon, het aantal machines in de schaal instellen toeneemt 1 als de drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="4c74d-200">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>
    
    * <span data-ttu-id="4c74d-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="4c74d-201">**cooldown**</span></span>  
    <span data-ttu-id="4c74d-202">Deze waarde is de hoeveelheid tijd sinds de laatste vergroten/verkleinen actie wachten voordat de volgende actie optreedt.</span><span class="sxs-lookup"><span data-stu-id="4c74d-202">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="4c74d-203">Deze waarde moet tussen 1 minuut en één week.</span><span class="sxs-lookup"><span data-stu-id="4c74d-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="4c74d-204">Sla het sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="4c74d-204">Save the template file.</span></span>    

## <a name="step-4-upload-the-template-to-storage"></a><span data-ttu-id="4c74d-205">Stap 4: De sjabloon uploaden naar de opslag</span><span class="sxs-lookup"><span data-stu-id="4c74d-205">Step 4: Upload the template to storage</span></span>
<span data-ttu-id="4c74d-206">De sjabloon kan worden geüpload, zolang u weet dat de naam en de primaire sleutel van het opslagaccount dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c74d-206">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="4c74d-207">Stel een variabele die u specificeert de naam van het opslagaccount dat u in stap 1 hebt gemaakt in de Microsoft Azure PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="4c74d-207">In the Microsoft Azure PowerShell window, set a variable that specifies the name of the storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="4c74d-208">Instellen van een variabele waarin de primaire sleutel van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4c74d-208">Set a variable that specifies the primary key of the storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="4c74d-209">U kunt deze sleutel verkrijgen door te klikken op het sleutelpictogram wanneer u de opslagbronnen account bekijkt in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4c74d-209">You can get this key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span>
3. <span data-ttu-id="4c74d-210">Maak het storage account context-object dat wordt gebruikt voor bewerkingen met de storage-account te valideren.</span><span class="sxs-lookup"><span data-stu-id="4c74d-210">Create the storage account context object that is used to validate operations with the storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="4c74d-211">De container voor het opslaan van de sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="4c74d-211">Create the container for storing the template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="4c74d-212">Het sjabloonbestand uploaden naar de nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="4c74d-212">Upload the template file to the new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-the-template"></a><span data-ttu-id="4c74d-213">Stap 5: De sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="4c74d-213">Step 5: Deploy the template</span></span>
<span data-ttu-id="4c74d-214">Nu dat u de sjabloon hebt gemaakt, kunt u beginnen met het implementeren van de resources.</span><span class="sxs-lookup"><span data-stu-id="4c74d-214">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="4c74d-215">Gebruik deze opdracht om het proces te starten:</span><span class="sxs-lookup"><span data-stu-id="4c74d-215">Use this command to start the process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="4c74d-216">Wanneer u op invoert, wordt u gevraagd waarden op te geven voor de variabelen die u hebt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-216">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="4c74d-217">Deze waarden bevatten:</span><span class="sxs-lookup"><span data-stu-id="4c74d-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="4c74d-218">Het duurt ongeveer 15 minuten voor alle resources worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4c74d-218">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="4c74d-219">U kunt ook de mogelijkheid van de portal gebruiken voor het implementeren van de resources.</span><span class="sxs-lookup"><span data-stu-id="4c74d-219">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="4c74d-220">Gebruik deze koppeling: ' https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>'</span><span class="sxs-lookup"><span data-stu-id="4c74d-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="4c74d-221">Stap 6: Monitor resources</span><span class="sxs-lookup"><span data-stu-id="4c74d-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="4c74d-222">U kunt sommige informatie ophalen over virtuele-machineschaalsets met behulp van deze methoden:</span><span class="sxs-lookup"><span data-stu-id="4c74d-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="4c74d-223">De Azure portal - momenteel krijgt u een beperkte hoeveelheid informatie via de portal.</span><span class="sxs-lookup"><span data-stu-id="4c74d-223">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>
* <span data-ttu-id="4c74d-224">De [Azure Resource Explorer](https://resources.azure.com/) -dit hulpprogramma is het meest geschikt voor de huidige status van uw scale set verkennen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-224">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="4c74d-225">Volg dit pad en ziet u de instantieweergave van de schaalaanpassingsset die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4c74d-225">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    <span data-ttu-id="4c74d-226">abonnementen > {uw abonnement} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtuele machines</span><span class="sxs-lookup"><span data-stu-id="4c74d-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="4c74d-227">Azure PowerShell - Gebruik deze opdracht kunt u enkele gegevens:</span><span class="sxs-lookup"><span data-stu-id="4c74d-227">Azure PowerShell - Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="4c74d-228">of</span><span class="sxs-lookup"><span data-stu-id="4c74d-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="4c74d-229">Verbinding maken met de afzonderlijke virtuele machine net zoals u zou een andere machine en klikt u op afstand toegang de virtuele machines in de schaal instelt tot voor het bewaken van afzonderlijke processen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-229">Connect to the separate virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="4c74d-230">Een complete REST-API voor het verkrijgen van informatie over schaalsets vindt u in [virtuele Machine Scale ingesteld](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="4c74d-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-the-resources"></a><span data-ttu-id="4c74d-231">Stap 7: De resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="4c74d-231">Step 7: Remove the resources</span></span>
<span data-ttu-id="4c74d-232">Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd een goede gewoonte resources verwijderen die niet langer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="4c74d-232">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="4c74d-233">U hoeft niet elke resource afzonderlijk verwijderen uit een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4c74d-233">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="4c74d-234">U kunt de resourcegroep verwijderen en de bijhorende resources automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4c74d-234">You can delete the resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="4c74d-235">Als u behouden van de resourcegroep wilt, kunt u de schaal instelt alleen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4c74d-235">If you want to keep your resource group, you can delete the scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="4c74d-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c74d-236">Next steps</span></span>
* <span data-ttu-id="4c74d-237">Beheren van de schaalaanpassingsset die u zojuist hebt gemaakt met de informatie in [beheren van virtuele machines in een virtuele-Machineschaalset](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4c74d-237">Manage the scale set that you just created using the information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="4c74d-238">Raadpleeg [Verticaal automatisch schalen met virtuele-machineschaalsets](virtual-machine-scale-sets-vertical-scale-reprovision.md) voor meer informatie over verticaal schalen</span><span class="sxs-lookup"><span data-stu-id="4c74d-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="4c74d-239">Voorbeelden van Azure Monitor bewakingsfuncties in [Azure Monitor PowerShell snel starten-voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="4c74d-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="4c74d-240">Meer informatie over functies in [acties automatisch schalen gebruiken voor het verzenden van e-mail en -webhook-waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="4c74d-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="4c74d-241">Meer informatie over hoe [controlelogboeken voor gebruik met het verzenden van e-mail en webhook-waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="4c74d-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

