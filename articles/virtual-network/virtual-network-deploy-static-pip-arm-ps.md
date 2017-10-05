---
title: Een virtuele machine maken met statische openbare IP-adres - Azure PowerShell | Microsoft Docs
description: Informatie over het maken van een virtuele machine met een statische openbare IP-adres met behulp van PowerShell.
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
ms.openlocfilehash: e4c413d3cb5c242a16f3e534dafe322785a35141
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="9820f-103">Een virtuele machine maken met een statisch openbaar IP-adres met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9820f-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9820f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9820f-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="9820f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9820f-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="9820f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9820f-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="9820f-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="9820f-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="9820f-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="9820f-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9820f-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9820f-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9820f-110">In dit artikel wordt behandeld met het implementatiemodel van Resource Manager, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel aanbeveelt.</span><span class="sxs-lookup"><span data-stu-id="9820f-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="9820f-111">Stap 1: uw script starten</span><span class="sxs-lookup"><span data-stu-id="9820f-111">Step 1 - Start your script</span></span>
<span data-ttu-id="9820f-112">U kunt de volledige PowerShell-script gebruikt downloaden [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="9820f-112">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="9820f-113">Volg onderstaande stappen voor het wijzigen van het script te laten werken in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="9820f-113">Follow the steps below to change the script to work in your environment.</span></span>

<span data-ttu-id="9820f-114">Wijzig de waarden van de variabelen op basis van de waarden die u wilt gebruiken voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="9820f-114">Change the values of the variables below based on the values you want to use for your deployment.</span></span> <span data-ttu-id="9820f-115">De volgende waarden worden toegewezen aan het scenario in dit artikel gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9820f-115">The following values map to the scenario used in this article:</span></span>

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

## <a name="step-2---create-the-necessary-resources-for-your-vm"></a><span data-ttu-id="9820f-116">Stap 2: de benodigde resources voor uw virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="9820f-116">Step 2 - Create the necessary resources for your VM</span></span>
<span data-ttu-id="9820f-117">Voordat u een virtuele machine maakt, moet u een resourcegroep, VNet, openbare IP-adres en NIC moet worden gebruikt door de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9820f-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC to be used by the VM.</span></span>

1. <span data-ttu-id="9820f-118">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9820f-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="9820f-119">Het VNet en een subnet maken.</span><span class="sxs-lookup"><span data-stu-id="9820f-119">Create the VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="9820f-120">Het openbare IP-resource maken.</span><span class="sxs-lookup"><span data-stu-id="9820f-120">Create the public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="9820f-121">De netwerkinterface (NIC) maken voor de virtuele machine in het bovenstaande gemaakt met het openbare IP-subnet.</span><span class="sxs-lookup"><span data-stu-id="9820f-121">Create the network interface (NIC) for the VM in the subnet created above, with the public IP.</span></span> <span data-ttu-id="9820f-122">Let op de eerste cmdlet bij het ophalen van het VNet van Azure, dit is nodig omdat een `Set-AzureRmVirtualNetwork` om te wijzigen van het bestaande VNet is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9820f-122">Notice the first cmdlet retrieving the VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed to change the existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="9820f-123">Een opslagaccount voor het hosten van de VM-OS-schijf maken.</span><span class="sxs-lookup"><span data-stu-id="9820f-123">Create a storage account to host the VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-the-vm"></a><span data-ttu-id="9820f-124">Stap 3: de virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="9820f-124">Step 3 - Create the VM</span></span>
<span data-ttu-id="9820f-125">Nu dat alle benodigde resources gemaakt zijn, kunt u een nieuwe virtuele machine kunt maken.</span><span class="sxs-lookup"><span data-stu-id="9820f-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="9820f-126">Het configuratieobject voor de virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="9820f-126">Create the configuration object for the VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="9820f-127">Referenties voor het lokale beheerdersaccount van de virtuele machine niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="9820f-127">Get credentials for the VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

3. <span data-ttu-id="9820f-128">Maak een VM-configuratie-object.</span><span class="sxs-lookup"><span data-stu-id="9820f-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="9820f-129">Installatiekopie van besturingssysteem instellen voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9820f-129">Set the operating system image for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="9820f-130">Configureer de OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="9820f-130">Configure the OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="9820f-131">De NIC toevoegen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9820f-131">Add the NIC to the VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="9820f-132">De virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="9820f-132">Create the VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="9820f-133">Sla het scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="9820f-133">Save the script file.</span></span>

## <a name="step-4---run-the-script"></a><span data-ttu-id="9820f-134">Stap 4: Voer het script</span><span class="sxs-lookup"><span data-stu-id="9820f-134">Step 4 - Run the script</span></span>
<span data-ttu-id="9820f-135">Nadat u wijzigingen nodig en kennis van het script weergeven hierboven, voert u het script.</span><span class="sxs-lookup"><span data-stu-id="9820f-135">After making any necessary changes, and understanding the script show above, run the script.</span></span> 

1. <span data-ttu-id="9820f-136">Voer het bovenstaande script van een PowerShell-console of de PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="9820f-136">From a PowerShell console, or PowerShell ISE, run the script above.</span></span>
2. <span data-ttu-id="9820f-137">De volgende uitvoer moet worden weergegeven na een paar minuten:</span><span class="sxs-lookup"><span data-stu-id="9820f-137">The following output should be displayed after a few minutes:</span></span>
   
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

