---
title: aaaAutoscale Linux virtuele-Machineschaalsets | Microsoft Docs
description: Automatisch schalen instellen voor een Linux VM-Schaalset met Azure CLI
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="a992b-103">Linux-machines automatisch schalen in een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="a992b-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="a992b-104">Virtuele-machineschaalsets eenvoudiger voor u toodeploy en identieke virtuele machines beheren als een set.</span><span class="sxs-lookup"><span data-stu-id="a992b-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="a992b-105">Schaalsets bieden een uiterst schaalbare en aanpasbare berekeningslaag voor toepassingen die grootschalig en installatiekopieën voor Windows-platform, installatiekopieën van virtuele Linux-platform, aangepaste installatiekopieën en -extensies ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="a992b-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="a992b-106">toolearn meer, Zie [overzicht van virtuele machines Scale Sets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="a992b-107">Deze zelfstudie leert u hoe toocreate een schaal van Linux virtuele machines met behulp van de meest recente versie Hallo van Ubuntu Linux instelt.</span><span class="sxs-lookup"><span data-stu-id="a992b-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="a992b-108">Hallo zelfstudie ook ziet u hoe tooautomatically scale Hallo-machines in Hallo instelt.</span><span class="sxs-lookup"><span data-stu-id="a992b-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="a992b-109">U maakt Hallo schaal en instellen schalen door een Azure Resource Manager-sjabloon maken en implementeren met behulp van Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a992b-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="a992b-110">Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) voor meer informatie over sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a992b-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a992b-111">toolearn meer informatie over automatisch schalen van schaalsets, Zie [automatisch schalen en Virtual Machine-schaal stelt](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="a992b-112">In deze zelfstudie maakt u de volgende Hallo implementeren bronnen en -extensies:</span><span class="sxs-lookup"><span data-stu-id="a992b-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="a992b-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="a992b-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="a992b-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="a992b-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="a992b-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="a992b-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="a992b-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="a992b-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="a992b-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="a992b-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="a992b-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="a992b-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="a992b-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="a992b-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="a992b-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="a992b-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="a992b-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="a992b-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="a992b-122">Zie voor meer informatie over het Resource Manager-resources [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="a992b-123">Voordat u aan de slag met Hallo stappen in deze zelfstudie [hello Azure CLI installeren](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="a992b-124">Stap 1: Een resourcegroep en een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="a992b-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="a992b-125">**Meld u aan tooMicrosoft Azure**</span><span class="sxs-lookup"><span data-stu-id="a992b-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="a992b-126">In de opdrachtregelinterface (Bash, Terminal-opdrachtprompt), overschakelen tooResource Manager-modus, en vervolgens [Meld u aan met uw werk of school-id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Volg de aanwijzingen Hallo voor een interactieve aanmelding ervaring tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a992b-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="a992b-127">Als u hebt een werk- of schoolaccount ID en u niet tweeledige verificatie zijn ingeschakeld, gebruikt u `azure login -u` met Hallo ID toolog in zonder een interactieve sessie.</span><span class="sxs-lookup"><span data-stu-id="a992b-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="a992b-128">Als u niet een werk- of schoolaccount ID hebt, kunt u [maakt u een werk- of schoolaccount-id van uw persoonlijke Microsoft-account](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="a992b-129">**Een resourcegroep maken**</span><span class="sxs-lookup"><span data-stu-id="a992b-129">**Create a resource group**</span></span>  
<span data-ttu-id="a992b-130">Alle resources moet geïmplementeerde tooa resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a992b-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="a992b-131">Voor deze zelfstudie Hallo resourcegroep een naam **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="a992b-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="a992b-132">**Implementeren van een opslagaccount in de nieuwe resourcegroep Hallo**</span><span class="sxs-lookup"><span data-stu-id="a992b-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="a992b-133">Dit opslagaccount is waar Hallo sjabloon wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a992b-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="a992b-134">Maken van een opslagaccount met de naam **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="a992b-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="a992b-135">Stap 2: Hallo-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a992b-135">Step 2: Create hello template</span></span>
<span data-ttu-id="a992b-136">Een Azure Resource Manager-sjabloon maakt het mogelijk dat u toodeploy en gezamenlijk Azure-resources beheren met behulp van een JSON-beschrijving van Hallo resources en de bijbehorende implementatie-parameters.</span><span class="sxs-lookup"><span data-stu-id="a992b-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="a992b-137">In uw favoriete editor Hallo bestand VMSSTemplate.json maken en toevoegen van Hallo initiële JSON-structuur toosupport Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a992b-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="a992b-138">Parameters zijn niet altijd vereist, maar ze bieden een manier tooinput waarden wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a992b-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="a992b-139">Toevoegen van deze parameters onder Hallo parameters bovenliggende element dat u de sjabloon toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a992b-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="a992b-140">Een naam voor het afzonderlijke virtuele machine hello, die gebruikte tooaccess Hallo-machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="a992b-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="a992b-141">Een naam voor het opslagaccount Hallo waar Hallo sjabloon wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a992b-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="a992b-142">het aantal exemplaren van virtuele machines tooinitially Hallo maken in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="a992b-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="a992b-143">Een naam en het wachtwoord van Hallo administrator-account op Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a992b-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="a992b-144">Een voorvoegsel voor Hallo-resources die zijn gemaakt toosupport Hallo scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a992b-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="a992b-145">Variabelen kunnen worden gebruikt in een sjabloon toospecify-waarden die kunnen worden regelmatig gewijzigd of waarden die toobe moet gemaakt uit een combinatie van parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="a992b-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="a992b-146">Voeg deze variabelen onder Hallo variabelen bovenliggende element dat u de sjabloon toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a992b-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="a992b-147">DNS-namen die worden gebruikt door Hallo netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="a992b-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="a992b-148">namen van Hallo IP-adres en de voorvoegsels voor het virtuele netwerk Hallo en subnetten.</span><span class="sxs-lookup"><span data-stu-id="a992b-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="a992b-149">Hallo namen en id van het virtuele netwerk hello, en voor de load balancer, netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="a992b-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="a992b-150">Namen van opslagaccounts voor Hallo-accounts die zijn gekoppeld aan het Hallo-machines in de schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="a992b-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="a992b-151">Instellingen voor het Hallo-extensie voor diagnostische gegevens die op Hallo virtuele machines is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a992b-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="a992b-152">Zie voor meer informatie over het Hallo-extensie voor diagnostische gegevens [maken van een virtuele Windows-machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a992b-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="a992b-153">Hallo storage account resource onder Hallo resources bovenliggende element dat u hebt toegevoegd toohello sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a992b-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="a992b-154">Deze sjabloon worden gebruikt in een lus toocreate Hallo aanbevolen vijf opslagaccounts waar Hallo besturingssysteem schijven en diagnostische gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a992b-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="a992b-155">Deze set accounts kan van too100 virtuele machines in een schaalset, die staat voor de huidige maximaal Hallo ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="a992b-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="a992b-156">De naam van elk opslagaccount is met een letter eenheidsaanduiding die is gedefinieerd in gecombineerd met Hallo-achtervoegsel dat u in het Hallo-parameters voor de sjabloon Hallo opgeeft Hallo-variabelen.</span><span class="sxs-lookup"><span data-stu-id="a992b-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="a992b-157">Hallo virtueel netwerk resource toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a992b-157">Add hello virtual network resource.</span></span> <span data-ttu-id="a992b-158">Zie voor meer informatie [Netwerkresourceprovider](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="a992b-159">Voeg Hallo openbare IP-adres resources die worden gebruikt door Hallo load balancer en netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="a992b-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="a992b-160">Hallo load balancerresource die wordt gebruikt door Hallo scale set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a992b-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="a992b-161">Zie voor meer informatie [Azure Resource Manager-ondersteuning voor de Load Balancer](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a992b-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="a992b-162">Hallo network interface-resource die wordt gebruikt door Hallo afzonderlijke virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a992b-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="a992b-163">Omdat computers in een scale-set niet toegankelijk zijn via een openbaar IP-adres, een aparte virtuele machine wordt gemaakt in Hallo hetzelfde virtuele netwerk tooremotely toegang Hallo-machines.</span><span class="sxs-lookup"><span data-stu-id="a992b-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="a992b-164">Hallo afzonderlijke virtuele machine in Hallo netwerk als Hallo scale set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a992b-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. <span data-ttu-id="a992b-165">Hallo virtuele-machineschaalset resource toevoegen en geef Hallo-extensie voor diagnostische gegevens die op alle virtuele machines in de schaalset Hallo is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a992b-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="a992b-166">Veel van Hallo-instellingen voor deze resource zijn vergelijkbaar met de bron van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="a992b-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="a992b-167">de belangrijkste verschillen Hallo zijn Hallo capaciteit element waarmee Hallo aantal virtuele machines in de schaalset hello en upgradePolicy waarmee wordt aangegeven hoe updates toovirtual machines worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a992b-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="a992b-168">Hallo scale set wordt niet gemaakt totdat alle Hallo-opslagaccounts worden gemaakt die is opgegeven met Hallo dependsOn element.</span><span class="sxs-lookup"><span data-stu-id="a992b-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="a992b-169">Hallo autoscaleSettings resource die definieert hoe Hallo scale set wordt aangepast op basis van het processorgebruik op Hallo virtuele machines in Hallo set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a992b-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    
    <span data-ttu-id="a992b-170">Deze waarden zijn belangrijk voor deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="a992b-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="a992b-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="a992b-171">**metricName**</span></span>  
    <span data-ttu-id="a992b-172">Deze waarde is hetzelfde als het Hallo-prestatiemeteritem dat is gedefinieerd in Hallo wadperfcounter variabele Hallo.</span><span class="sxs-lookup"><span data-stu-id="a992b-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="a992b-173">Met behulp van die variabele Hallo extensie voor diagnostische gegevens verzamelt Hallo **Processor\PercentProcessorTime** teller.</span><span class="sxs-lookup"><span data-stu-id="a992b-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="a992b-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="a992b-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="a992b-175">Deze waarde is Hallo resource-id van de virtuele-machineschaalset Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="a992b-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="a992b-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="a992b-176">**timeGrain**</span></span>  
    <span data-ttu-id="a992b-177">Deze waarde is Hallo granulatie van Hallo metrische gegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="a992b-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="a992b-178">In deze sjabloon is ingesteld tooone minuut.</span><span class="sxs-lookup"><span data-stu-id="a992b-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="a992b-179">**statistiek**</span><span class="sxs-lookup"><span data-stu-id="a992b-179">**statistic**</span></span>  
    <span data-ttu-id="a992b-180">Deze waarde bepaalt hoe Hallo metrische gegevens worden gecombineerd tooaccommodate Hallo automatisch vergroten / verkleinen in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="a992b-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="a992b-181">Hallo mogelijke waarden zijn: gemiddelde, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="a992b-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="a992b-182">In deze sjabloon Hallo gemiddelde totale CPU-gebruik van Hallo virtuele machines worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="a992b-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="a992b-183">**waarde voor timeWindow**</span><span class="sxs-lookup"><span data-stu-id="a992b-183">**timeWindow**</span></span>  
    <span data-ttu-id="a992b-184">Deze waarde is Hallo tijdbereik waarin de gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="a992b-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="a992b-185">Deze moet tussen 5 minuten en 12 uur.</span><span class="sxs-lookup"><span data-stu-id="a992b-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="a992b-186">**TimeAggregation van**</span><span class="sxs-lookup"><span data-stu-id="a992b-186">**timeAggregation**</span></span>  
    <span data-ttu-id="a992b-187">de waarde bepaalt hoe Hallo-gegevens die worden verzameld gedurende een bepaalde periode moeten worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="a992b-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="a992b-188">Hallo-standaardwaarde is de gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="a992b-188">hello default value is Average.</span></span> <span data-ttu-id="a992b-189">Hallo mogelijke waarden zijn: gemiddeld, Minimum, Maximum, laatste, totaal, Count.</span><span class="sxs-lookup"><span data-stu-id="a992b-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="a992b-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="a992b-190">**operator**</span></span>  
    <span data-ttu-id="a992b-191">Deze waarde is Hallo-operator die wordt gebruikt toocompare Hallo metrische gegevens en Hallo drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="a992b-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="a992b-192">Hallo mogelijke waarden zijn: gelijk is aan NotEquals, groter dan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="a992b-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="a992b-193">**drempelwaarde**</span><span class="sxs-lookup"><span data-stu-id="a992b-193">**threshold**</span></span>  
    <span data-ttu-id="a992b-194">Deze waarde activeert Hallo schaalactie.</span><span class="sxs-lookup"><span data-stu-id="a992b-194">This value triggers hello scale action.</span></span> <span data-ttu-id="a992b-195">In deze sjabloon wordt toegevoegd machines toohello schaal instellen als de gemiddelde CPU-gebruik Hallo tussen computers in het Hallo-set is meer dan 50%.</span><span class="sxs-lookup"><span data-stu-id="a992b-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="a992b-196">**richting**</span><span class="sxs-lookup"><span data-stu-id="a992b-196">**direction**</span></span>  
    <span data-ttu-id="a992b-197">Deze waarde bepaalt Hallo-actie die wordt uitgevoerd wanneer het Hallo-drempelwaarde wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="a992b-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="a992b-198">Hallo mogelijke waarden zijn vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="a992b-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="a992b-199">In deze sjabloon wordt hello aantal virtuele machines in de schaalset hello verhoogd als Hallo drempelwaarde meer dan 50% in tijdvenster Hallo gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a992b-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="a992b-200">**type**</span><span class="sxs-lookup"><span data-stu-id="a992b-200">**type**</span></span>  
    <span data-ttu-id="a992b-201">Deze waarde is Hallo type actie dat moet worden uitgevoerd en tooChangeCount moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a992b-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="a992b-202">**waarde**</span><span class="sxs-lookup"><span data-stu-id="a992b-202">**value**</span></span>  
    <span data-ttu-id="a992b-203">Deze waarde is het aantal virtuele machines die zijn toegevoegd of verwijderd uit schaalset Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a992b-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="a992b-204">Deze waarde moet 1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a992b-204">This value must be 1 or greater.</span></span> <span data-ttu-id="a992b-205">Hallo-standaardwaarde is 1.</span><span class="sxs-lookup"><span data-stu-id="a992b-205">hello default value is 1.</span></span> <span data-ttu-id="a992b-206">In deze sjabloon Hallo aantal machines in Hallo schaal instellen toeneemt 1 wanneer Hallo drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="a992b-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="a992b-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="a992b-207">**cooldown**</span></span>  
    <span data-ttu-id="a992b-208">Deze waarde is Hallo hoeveelheid tijd toowait sinds de laatste vergroten/verkleinen actie Hallo voordat de volgende actie Hallo optreedt.</span><span class="sxs-lookup"><span data-stu-id="a992b-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="a992b-209">Deze waarde moet tussen 1 minuut en één week.</span><span class="sxs-lookup"><span data-stu-id="a992b-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="a992b-210">Hallo-sjabloonbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="a992b-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="a992b-211">Stap 3: Hallo sjabloon toostorage uploaden</span><span class="sxs-lookup"><span data-stu-id="a992b-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="a992b-212">Hallo-sjabloon kan worden geüpload, zolang u weet Hallo naam en de primaire sleutel van Hallo storage-account dat u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a992b-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="a992b-213">In de opdrachtregelinterface (Bash, Terminal-opdrachtprompt), voer deze opdrachten tooset Hallo omgevingsvariabelen nodig tooaccess Hallo storage-account:</span><span class="sxs-lookup"><span data-stu-id="a992b-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="a992b-214">U kunt Hallo sleutel verkrijgen door te klikken op het sleutelpictogram Hallo wanneer u bekijkt hello storage account resource in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a992b-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="a992b-215">Wanneer u een Windows-opdrachtprompt, typ **ingesteld** in plaats van de export.</span><span class="sxs-lookup"><span data-stu-id="a992b-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="a992b-216">Hallo-container voor het opslaan van Hallo-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="a992b-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="a992b-217">Hallo sjabloon bestand toohello nieuwe container uploaden.</span><span class="sxs-lookup"><span data-stu-id="a992b-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="a992b-218">Stap 4: Hallo sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="a992b-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="a992b-219">Nu dat u Hallo sjabloon hebt gemaakt, kunt u beginnen met het Hallo-resources te implementeren.</span><span class="sxs-lookup"><span data-stu-id="a992b-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="a992b-220">Gebruik deze opdracht toostart Hallo proces:</span><span class="sxs-lookup"><span data-stu-id="a992b-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="a992b-221">Wanneer u op invoeren, vraag tooprovide waarden voor Hallo variabelen die u hebt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a992b-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="a992b-222">Deze waarden bevatten:</span><span class="sxs-lookup"><span data-stu-id="a992b-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="a992b-223">Het duurt ongeveer 15 minuten voor alle Hallo resources toosuccessfully worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a992b-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="a992b-224">U kunt ook Hallo-portal mogelijkheid toodeploy Hallo resources gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a992b-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="a992b-225">Gebruik deze koppeling: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="a992b-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="a992b-226">Stap 5: Monitor resources</span><span class="sxs-lookup"><span data-stu-id="a992b-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="a992b-227">U kunt sommige informatie ophalen over virtuele-machineschaalsets met behulp van deze methoden:</span><span class="sxs-lookup"><span data-stu-id="a992b-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="a992b-228">Azure-portal Hallo - kunt u een beperkte hoeveelheid informatie met Hallo portal momenteel krijgen.</span><span class="sxs-lookup"><span data-stu-id="a992b-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="a992b-229">Hallo [Azure Resource Explorer](https://resources.azure.com/) -dit hulpprogramma is Hallo aanbevolen voor de huidige status van uw scale set Hallo verkennen.</span><span class="sxs-lookup"><span data-stu-id="a992b-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="a992b-230">Volg dit pad en ziet u Hallo instantieweergave van de schaal Hallo instellen die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="a992b-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="a992b-231">Azure CLI - Gebruik deze opdracht tooget sommige informatie:</span><span class="sxs-lookup"><span data-stu-id="a992b-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="a992b-232">Net zoals u zou een andere machine en klikt u op afstand toegang Hallo virtuele machines in Hallo scale set toomonitor afzonderlijke processen tot, verbinding maken met toohello jumpbox virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a992b-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a992b-233">Een complete REST-API voor het verkrijgen van informatie over schaalsets vindt u in [virtuele Machine Scale ingesteld](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="a992b-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="a992b-234">Stap 6: Hallo resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="a992b-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="a992b-235">Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd een goede gewoonte toodelete-resources die niet langer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="a992b-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="a992b-236">U hoeft niet toodelete elke resource afzonderlijk van een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a992b-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="a992b-237">U kunt Hallo resourcegroep verwijderen en de bijhorende resources automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a992b-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="a992b-238">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a992b-238">Next steps</span></span>
* <span data-ttu-id="a992b-239">Voorbeelden van Azure Monitor bewakingsfuncties in [Azure Monitor platformoverschrijdende CLI snel starten voorbeelden](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="a992b-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="a992b-240">Meer informatie over functies in [gebruiken voor automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a992b-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="a992b-241">Meer informatie over hoe te[gebruik auditlogboeken toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a992b-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="a992b-242">Bekijk Hallo [demo-app automatisch schalen op Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sjabloon instellen van een Python/bottle app tooexercise Hallo automatisch vergroten / verkleinen functionaliteit van de virtuele Machine Scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a992b-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

