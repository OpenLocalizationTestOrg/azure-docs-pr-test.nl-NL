---
title: een virtuele machine met een statisch openbaar IP-adres - Azure PowerShell aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtuele machine met een statische openbare IP-adres met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="39097-103">Een virtuele machine maken met een statisch openbaar IP-adres met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="39097-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39097-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="39097-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="39097-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39097-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="39097-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39097-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="39097-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="39097-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="39097-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="39097-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="39097-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="39097-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39097-110">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39097-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="39097-111">Stap 1: uw script starten</span><span class="sxs-lookup"><span data-stu-id="39097-111">Step 1 - Start your script</span></span>
<span data-ttu-id="39097-112">U kunt downloaden Hallo volledige PowerShell-script gebruikt [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="39097-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="39097-113">Hallo stappen hieronder toochange Hallo script toowork in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="39097-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="39097-114">Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="39097-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="39097-115">Hallo waarden kaart toohello scenario gebruikt in dit artikel te volgen:</span><span class="sxs-lookup"><span data-stu-id="39097-115">hello following values map toohello scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="39097-116">Stap 2: Hallo benodigde resources voor uw virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="39097-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="39097-117">Voordat u een virtuele machine maakt, moet u een resourcegroep, VNet, openbare IP- en NIC die wordt gebruikt door VM Hallo toobe.</span><span class="sxs-lookup"><span data-stu-id="39097-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="39097-118">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="39097-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="39097-119">Maak Hallo VNet en het subnetmasker.</span><span class="sxs-lookup"><span data-stu-id="39097-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="39097-120">Hallo openbare IP-resource maken.</span><span class="sxs-lookup"><span data-stu-id="39097-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="39097-121">Hallo-netwerkinterface (NIC) maken voor Hallo VM in Hallo subnet met Hallo openbare IP-adres hierboven wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39097-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="39097-122">Let op Hallo van eerste cmdlet Hallo VNet ophalen uit Azure, dit is nodig omdat een `Set-AzureRmVirtualNetwork` is uitgevoerd toochange Hallo bestaande VNet.</span><span class="sxs-lookup"><span data-stu-id="39097-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="39097-123">Maak een storage account toohost Hallo VM OS-station.</span><span class="sxs-lookup"><span data-stu-id="39097-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="39097-124">Stap 3: Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="39097-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="39097-125">Nu dat alle benodigde resources gemaakt zijn, kunt u een nieuwe virtuele machine kunt maken.</span><span class="sxs-lookup"><span data-stu-id="39097-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="39097-126">Hallo configuration-object voor Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="39097-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="39097-127">Referenties voor Hallo VM lokale administrator-account niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="39097-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="39097-128">Maak een VM-configuratie-object.</span><span class="sxs-lookup"><span data-stu-id="39097-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="39097-129">Hallo besturingssysteeminstallatiekopie maken voor Hallo VM wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="39097-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="39097-130">Configureer Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="39097-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="39097-131">Hallo NIC toohello VM toevoegen.</span><span class="sxs-lookup"><span data-stu-id="39097-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="39097-132">Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="39097-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="39097-133">Hallo scriptbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="39097-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="39097-134">Stap 4: Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="39097-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="39097-135">Nadat de benodigde wijzigingen en kennis Hallo script weergeven hierboven, Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="39097-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="39097-136">Uitvoeren van een PowerShell-console of PowerShell ISE, Hallo script hierboven.</span><span class="sxs-lookup"><span data-stu-id="39097-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="39097-137">Hallo na uitvoer moet worden weergegeven na een paar minuten:</span><span class="sxs-lookup"><span data-stu-id="39097-137">hello following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

