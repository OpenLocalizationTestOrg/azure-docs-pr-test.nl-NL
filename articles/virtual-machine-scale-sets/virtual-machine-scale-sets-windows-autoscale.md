---
title: aaaAutoscale Windows virtuele-Machineschaalsets | Microsoft Docs
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
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="921e2-103">Automatisch schalen machines in een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="921e2-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="921e2-104">Virtuele-machineschaalsets eenvoudiger voor u toodeploy en identieke virtuele machines beheren als een set.</span><span class="sxs-lookup"><span data-stu-id="921e2-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="921e2-105">Schaalsets bieden een uiterst schaalbare en aanpasbare berekeningslaag voor toepassingen die grootschalig en installatiekopieën voor Windows-platform, installatiekopieën van virtuele Linux-platform, aangepaste installatiekopieën en -extensies ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="921e2-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="921e2-106">Zie voor meer informatie over schaalsets [virtuele Machine Scale ingesteld](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="921e2-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="921e2-107">Deze zelfstudie laat zien hoe een schaalset van virtuele machines van Windows en automatisch schalen Hallo machines in Hallo toocreate instelt.</span><span class="sxs-lookup"><span data-stu-id="921e2-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="921e2-108">U maakt Hallo schaal en instellen schalen door een Azure Resource Manager-sjabloon maken en implementeren met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="921e2-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="921e2-109">Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) voor meer informatie over sjablonen.</span><span class="sxs-lookup"><span data-stu-id="921e2-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="921e2-110">toolearn meer informatie over automatisch schalen van schaalsets, Zie [automatisch schalen en Virtual Machine-schaal stelt](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="921e2-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="921e2-111">In dit artikel hebt u volgende Hallo implementeert bronnen en -extensies:</span><span class="sxs-lookup"><span data-stu-id="921e2-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="921e2-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="921e2-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="921e2-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="921e2-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="921e2-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="921e2-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="921e2-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="921e2-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="921e2-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="921e2-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="921e2-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="921e2-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="921e2-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="921e2-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="921e2-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="921e2-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="921e2-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="921e2-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="921e2-121">Zie voor meer informatie over het Resource Manager-resources [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="921e2-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="921e2-122">Stap 1: Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="921e2-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="921e2-123">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooAzure aanmelden.</span><span class="sxs-lookup"><span data-stu-id="921e2-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="921e2-124">Stap 2: Een resourcegroep en een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="921e2-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="921e2-125">**Een resourcegroep maken** – alle resources moet geïmplementeerde tooa resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="921e2-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="921e2-126">Gebruik [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate een resourcegroep met de naam **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="921e2-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="921e2-127">**Een opslagaccount maken** – dit opslagaccount is waar Hallo-sjabloon is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="921e2-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="921e2-128">Gebruik [nieuw AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate een opslagaccount met de naam **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="921e2-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="921e2-129">Stap 3: Hallo-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="921e2-129">Step 3: Create hello template</span></span>
<span data-ttu-id="921e2-130">Een Azure Resource Manager-sjabloon maakt het mogelijk dat u toodeploy en gezamenlijk Azure-resources beheren met behulp van een JSON-beschrijving van Hallo resources en de bijbehorende implementatie-parameters.</span><span class="sxs-lookup"><span data-stu-id="921e2-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="921e2-131">In uw favoriete editor Hallo bestand C:\VMSSTemplate.json maken en toevoegen van Hallo initiële JSON-structuur toosupport Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="921e2-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="921e2-132">Parameters zijn niet altijd vereist, maar ze bieden een manier tooinput waarden wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="921e2-133">Toevoegen van deze parameters onder Hallo parameters bovenliggende element dat u de sjabloon toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="921e2-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="921e2-134">Een naam voor het afzonderlijke virtuele machine hello, die gebruikte tooaccess Hallo-machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e2-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="921e2-135">Hallo-naam van Hallo storage-account waarin Hallo-sjabloon is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="921e2-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="921e2-136">het aantal virtuele machines tooinitially Hallo maken in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e2-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="921e2-137">Hallo-naam en het wachtwoord van Hallo administrator-account op Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="921e2-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="921e2-138">Een voorvoegsel voor Hallo-resources die zijn gemaakt toosupport Hallo scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="921e2-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="921e2-139">Variabelen kunnen worden gebruikt in een sjabloon toospecify-waarden die kunnen worden regelmatig gewijzigd of waarden die toobe moet gemaakt uit een combinatie van parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="921e2-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="921e2-140">Voeg deze variabelen onder Hallo variabelen bovenliggende element dat u de sjabloon toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="921e2-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
   
    * <span data-ttu-id="921e2-141">DNS-namen die worden gebruikt door Hallo netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="921e2-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="921e2-142">namen van Hallo IP-adres en de voorvoegsels voor het virtuele netwerk Hallo en subnetten.</span><span class="sxs-lookup"><span data-stu-id="921e2-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="921e2-143">Hallo namen en id van het virtuele netwerk hello, en voor de load balancer, netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="921e2-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="921e2-144">Namen van opslagaccounts voor Hallo-accounts die zijn gekoppeld aan het Hallo-machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e2-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="921e2-145">Instellingen voor het Hallo-extensie voor diagnostische gegevens die op Hallo virtuele machines is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="921e2-146">Zie voor meer informatie over het Hallo-extensie voor diagnostische gegevens [maken van een virtuele Windows-machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="921e2-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="921e2-147">Hallo storage account resource onder Hallo resources bovenliggende element dat u hebt toegevoegd toohello sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="921e2-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="921e2-148">Deze sjabloon worden gebruikt in een lus toocreate Hallo aanbevolen vijf opslagaccounts waar Hallo besturingssysteem schijven en diagnostische gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="921e2-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="921e2-149">Deze set accounts kan van too100 virtuele machines in een schaalset, die staat voor de huidige maximaal Hallo ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="921e2-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="921e2-150">De naam van elk opslagaccount is met een letter eenheidsaanduiding die is gedefinieerd in gecombineerd met Hallo-voorvoegsel dat u in het Hallo-parameters voor de sjabloon Hallo opgeeft Hallo-variabelen.</span><span class="sxs-lookup"><span data-stu-id="921e2-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

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

5. <span data-ttu-id="921e2-151">Hallo virtueel netwerk resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="921e2-151">Add hello virtual network resource.</span></span> <span data-ttu-id="921e2-152">Zie voor meer informatie [Netwerkresourceprovider](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="921e2-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="921e2-153">Voeg Hallo openbare IP-adres resources die worden gebruikt door Hallo load balancer en netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="921e2-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="921e2-154">Hallo load balancerresource die wordt gebruikt door Hallo scale set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="921e2-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="921e2-155">Zie voor meer informatie [Azure Resource Manager-ondersteuning voor de Load Balancer](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="921e2-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="921e2-156">Hallo network interface-resource die wordt gebruikt door Hallo afzonderlijke virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="921e2-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="921e2-157">Omdat computers in een scale-set niet toegankelijk zijn via een openbaar IP-adres, een aparte virtuele machine wordt gemaakt in Hallo hetzelfde virtuele netwerk tooremotely toegang Hallo-machines.</span><span class="sxs-lookup"><span data-stu-id="921e2-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="921e2-158">Hallo afzonderlijke virtuele machine in Hallo netwerk als Hallo scale set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="921e2-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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

10. <span data-ttu-id="921e2-159">Hallo virtuele-machineschaalset resource toevoegen en geef Hallo-extensie voor diagnostische gegevens die op alle virtuele machines in de schaalset Hallo is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="921e2-160">Veel van Hallo-instellingen voor deze resource zijn vergelijkbaar met de bron van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e2-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="921e2-161">de belangrijkste verschillen Hallo zijn Hallo capaciteit element waarmee Hallo aantal virtuele machines in de schaalset hello en upgradePolicy waarmee wordt aangegeven hoe updates toovirtual machines worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="921e2-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="921e2-162">Hallo scale set wordt niet gemaakt totdat alle Hallo-opslagaccounts worden gemaakt die is opgegeven met Hallo dependsOn element.</span><span class="sxs-lookup"><span data-stu-id="921e2-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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

11. <span data-ttu-id="921e2-163">Hallo autoscaleSettings resource die definieert hoe Hallo scale set wordt aangepast op basis van Hallo processorgebruik op Hallo-machines in de schaalset Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="921e2-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

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

    <span data-ttu-id="921e2-164">Deze waarden zijn belangrijk voor deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="921e2-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="921e2-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="921e2-165">**metricName**</span></span>  
    <span data-ttu-id="921e2-166">Deze waarde is hetzelfde als het Hallo-prestatiemeteritem dat is gedefinieerd in Hallo wadperfcounter variabele Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e2-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="921e2-167">Met behulp van die variabele Hallo extensie voor diagnostische gegevens verzamelt Hallo **processor(_Totaal)\% processortijd** teller.</span><span class="sxs-lookup"><span data-stu-id="921e2-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="921e2-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="921e2-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="921e2-169">Deze waarde is Hallo resource-id van de virtuele-machineschaalset Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="921e2-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="921e2-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="921e2-170">**timeGrain**</span></span>  
    <span data-ttu-id="921e2-171">Deze waarde is Hallo granulatie van Hallo metrische gegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="921e2-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="921e2-172">In deze sjabloon is ingesteld tooone minuut.</span><span class="sxs-lookup"><span data-stu-id="921e2-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="921e2-173">**statistiek**</span><span class="sxs-lookup"><span data-stu-id="921e2-173">**statistic**</span></span>  
    <span data-ttu-id="921e2-174">Deze waarde bepaalt hoe Hallo metrische gegevens worden gecombineerd tooaccommodate Hallo automatisch vergroten / verkleinen in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="921e2-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="921e2-175">Hallo mogelijke waarden zijn: gemiddelde, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="921e2-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="921e2-176">In deze sjabloon Hallo gemiddelde totale CPU-gebruik van Hallo virtuele machines worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="921e2-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="921e2-177">**waarde voor timeWindow**</span><span class="sxs-lookup"><span data-stu-id="921e2-177">**timeWindow**</span></span>  
    <span data-ttu-id="921e2-178">Deze waarde is Hallo tijdbereik waarin de gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="921e2-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="921e2-179">Deze moet tussen 5 minuten en 12 uur.</span><span class="sxs-lookup"><span data-stu-id="921e2-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="921e2-180">**TimeAggregation van**</span><span class="sxs-lookup"><span data-stu-id="921e2-180">**timeAggregation**</span></span>  
    <span data-ttu-id="921e2-181">de waarde bepaalt hoe Hallo-gegevens die worden verzameld gedurende een bepaalde periode moeten worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="921e2-182">Hallo-standaardwaarde is de gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="921e2-182">hello default value is Average.</span></span> <span data-ttu-id="921e2-183">Hallo mogelijke waarden zijn: gemiddeld, Minimum, Maximum, laatste, totaal, Count.</span><span class="sxs-lookup"><span data-stu-id="921e2-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="921e2-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="921e2-184">**operator**</span></span>  
    <span data-ttu-id="921e2-185">Deze waarde is Hallo-operator die wordt gebruikt toocompare Hallo metrische gegevens en Hallo drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="921e2-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="921e2-186">Hallo mogelijke waarden zijn: gelijk is aan NotEquals, groter dan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="921e2-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="921e2-187">**drempelwaarde**</span><span class="sxs-lookup"><span data-stu-id="921e2-187">**threshold**</span></span>  
    <span data-ttu-id="921e2-188">Deze waarde is Hallo-waarde waarmee de schaalactie hello wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="921e2-189">In deze sjabloon wordt toegevoegd machines toohello schaal instellen als de gemiddelde CPU-gebruik Hallo tussen computers in het Hallo-set is meer dan 50%.</span><span class="sxs-lookup"><span data-stu-id="921e2-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="921e2-190">**richting**</span><span class="sxs-lookup"><span data-stu-id="921e2-190">**direction**</span></span>  
    <span data-ttu-id="921e2-191">Deze waarde bepaalt Hallo-actie die wordt uitgevoerd wanneer het Hallo-drempelwaarde wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="921e2-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="921e2-192">Hallo mogelijke waarden zijn vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="921e2-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="921e2-193">In deze sjabloon wordt hello aantal virtuele machines in de schaalset hello verhoogd als Hallo drempelwaarde meer dan 50% in tijdvenster Hallo gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="921e2-194">**type**</span><span class="sxs-lookup"><span data-stu-id="921e2-194">**type**</span></span>  
    <span data-ttu-id="921e2-195">Deze waarde is Hallo type actie dat moet worden uitgevoerd en tooChangeCount moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="921e2-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="921e2-196">**waarde**</span><span class="sxs-lookup"><span data-stu-id="921e2-196">**value**</span></span>  
    <span data-ttu-id="921e2-197">Deze waarde is het aantal virtuele machines die zijn toegevoegd of verwijderd uit schaalset Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="921e2-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="921e2-198">Deze waarde moet 1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="921e2-198">This value must be 1 or greater.</span></span> <span data-ttu-id="921e2-199">Hallo-standaardwaarde is 1.</span><span class="sxs-lookup"><span data-stu-id="921e2-199">hello default value is 1.</span></span> <span data-ttu-id="921e2-200">In deze sjabloon Hallo aantal machines in Hallo schaal instellen toeneemt 1 wanneer Hallo drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="921e2-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="921e2-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="921e2-201">**cooldown**</span></span>  
    <span data-ttu-id="921e2-202">Deze waarde is Hallo hoeveelheid tijd toowait sinds de laatste vergroten/verkleinen actie Hallo voordat de volgende actie Hallo optreedt.</span><span class="sxs-lookup"><span data-stu-id="921e2-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="921e2-203">Deze waarde moet tussen 1 minuut en één week.</span><span class="sxs-lookup"><span data-stu-id="921e2-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="921e2-204">Hallo-sjabloonbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="921e2-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="921e2-205">Stap 4: Hallo sjabloon toostorage uploaden</span><span class="sxs-lookup"><span data-stu-id="921e2-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="921e2-206">Hallo-sjabloon kan worden geüpload, zolang u weet Hallo naam en de primaire sleutel van Hallo storage-account dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="921e2-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="921e2-207">In Hallo Microsoft Azure PowerShell-venster, stelt u een variabele waarmee Hallo-naam van het Hallo-opslagaccount dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="921e2-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="921e2-208">Een variabele waarin de primaire sleutel van het opslagaccount Hallo Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="921e2-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="921e2-209">U kunt deze sleutel verkrijgen door te klikken op het sleutelpictogram Hallo wanneer u bekijkt hello storage account resource in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="921e2-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="921e2-210">Hallo storage account context-object dat is gebruikt toovalidate bewerkingen met Hallo storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="921e2-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="921e2-211">Hallo-container voor het opslaan van Hallo-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="921e2-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="921e2-212">Hallo sjabloon bestand toohello nieuwe container uploaden.</span><span class="sxs-lookup"><span data-stu-id="921e2-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="921e2-213">Stap 5: Hallo sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="921e2-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="921e2-214">Nu dat u Hallo sjabloon hebt gemaakt, kunt u beginnen met het Hallo-resources te implementeren.</span><span class="sxs-lookup"><span data-stu-id="921e2-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="921e2-215">Gebruik deze opdracht toostart Hallo proces:</span><span class="sxs-lookup"><span data-stu-id="921e2-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="921e2-216">Wanneer u op invoeren, vraag tooprovide waarden voor Hallo variabelen die u hebt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="921e2-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="921e2-217">Deze waarden bevatten:</span><span class="sxs-lookup"><span data-stu-id="921e2-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="921e2-218">Het duurt ongeveer 15 minuten voor alle Hallo resources toosuccessfully worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="921e2-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="921e2-219">U kunt ook Hallo-portal mogelijkheid toodeploy Hallo resources gebruiken.</span><span class="sxs-lookup"><span data-stu-id="921e2-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="921e2-220">Gebruik deze koppeling: ' https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>'</span><span class="sxs-lookup"><span data-stu-id="921e2-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="921e2-221">Stap 6: Monitor resources</span><span class="sxs-lookup"><span data-stu-id="921e2-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="921e2-222">U kunt sommige informatie ophalen over virtuele-machineschaalsets met behulp van deze methoden:</span><span class="sxs-lookup"><span data-stu-id="921e2-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="921e2-223">Azure-portal Hallo - kunt u een beperkte hoeveelheid informatie met Hallo portal momenteel krijgen.</span><span class="sxs-lookup"><span data-stu-id="921e2-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="921e2-224">Hallo [Azure Resource Explorer](https://resources.azure.com/) -dit hulpprogramma is Hallo aanbevolen voor de huidige status van uw scale set Hallo verkennen.</span><span class="sxs-lookup"><span data-stu-id="921e2-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="921e2-225">Volg dit pad en ziet u Hallo instantieweergave van de schaal Hallo instellen die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="921e2-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="921e2-226">abonnementen > {uw abonnement} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtuele machines</span><span class="sxs-lookup"><span data-stu-id="921e2-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="921e2-227">Azure PowerShell - Gebruik deze opdracht tooget sommige informatie:</span><span class="sxs-lookup"><span data-stu-id="921e2-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="921e2-228">of</span><span class="sxs-lookup"><span data-stu-id="921e2-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="921e2-229">Verbinding maken met afzonderlijke virtuele machine die toohello net zoals u zou een andere machine en klikt u op afstand toegang Hallo virtuele machines in Hallo scale set toomonitor afzonderlijke processen tot.</span><span class="sxs-lookup"><span data-stu-id="921e2-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="921e2-230">Een complete REST-API voor het verkrijgen van informatie over schaalsets vindt u in [virtuele Machine Scale ingesteld](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="921e2-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="921e2-231">Stap 7: Hallo resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="921e2-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="921e2-232">Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd een goede gewoonte toodelete-resources die niet langer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="921e2-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="921e2-233">U hoeft niet toodelete elke resource afzonderlijk van een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="921e2-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="921e2-234">U kunt Hallo resourcegroep verwijderen en de bijhorende resources automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="921e2-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="921e2-235">Als u uw resourcegroep tookeep wilt, kunt u Hallo scale ingesteld alleen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="921e2-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="921e2-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="921e2-236">Next steps</span></span>
* <span data-ttu-id="921e2-237">Beheren van Hallo scale set die u zojuist hebt gemaakt met behulp van de informatie in Hallo [beheren van virtuele machines in een virtuele-Machineschaalset](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="921e2-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="921e2-238">Raadpleeg [Verticaal automatisch schalen met virtuele-machineschaalsets](virtual-machine-scale-sets-vertical-scale-reprovision.md) voor meer informatie over verticaal schalen</span><span class="sxs-lookup"><span data-stu-id="921e2-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="921e2-239">Voorbeelden van Azure Monitor bewakingsfuncties in [Azure Monitor PowerShell snel starten-voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="921e2-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="921e2-240">Meer informatie over functies in [gebruiken voor automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="921e2-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="921e2-241">Meer informatie over hoe te[gebruik auditlogboeken toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="921e2-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

