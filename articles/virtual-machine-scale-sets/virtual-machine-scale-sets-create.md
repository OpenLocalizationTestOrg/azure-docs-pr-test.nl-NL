---
title: aaaCreate een virtuele machine van Azure-schaalset | Microsoft Docs
description: Maken en implementeren van een Linux- of Windows Azure virtuele-machineschaalset ingesteld met Azure CLI, PowerShell, een sjabloon of Visual Studio.
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="8bd72-103">Maken en implementeren van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="8bd72-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="8bd72-104">Virtuele-machineschaalsets eenvoudiger voor u toodeploy en identieke virtuele machines beheren als een set.</span><span class="sxs-lookup"><span data-stu-id="8bd72-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="8bd72-105">Schaalsets bieden een uiterst schaalbare en aanpasbare berekeningslaag voor toepassingen die grootschalig en installatiekopieën voor Windows-platform, installatiekopieën van virtuele Linux-platform, aangepaste installatiekopieën en -extensies ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="8bd72-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="8bd72-106">Zie voor meer informatie over schaalsets [virtuele-machineschaalsets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="8bd72-107">Deze zelfstudie laat zien hoe toocreate een virtuele-machineschaalset **zonder** met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8bd72-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="8bd72-108">Zie voor meer informatie over hoe toouse hello Azure-portal [hoe toocreate een virtuele-machineschaalset Hello Azure-portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="8bd72-109">Zie voor meer informatie over Azure Resource Manager-resources [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="8bd72-110">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="8bd72-110">Sign in tooAzure</span></span>

<span data-ttu-id="8bd72-111">Als u Azure PowerShell of Azure CLI 2.0 toocreate een schaal instelt, moet u eerst toosign in tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="8bd72-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="8bd72-112">Voor meer informatie over hoe tooinstall, instellen, en u aanmelden tooAzure met Azure CLI of PowerShell, Zie [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) of [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8bd72-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8bd72-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="8bd72-113">Create a resource group</span></span>

<span data-ttu-id="8bd72-114">U moet eerst toocreate een resourcegroep die Hallo virtuele-machineschaalset is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8bd72-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="8bd72-115">Maken van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8bd72-115">Create from Azure CLI</span></span>

<span data-ttu-id="8bd72-116">U kunt een virtuele-machineschaalset ingesteld met een minimale inspanning maken met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8bd72-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="8bd72-117">Als u standaardwaarden weglaat, zijn ze beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="8bd72-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="8bd72-118">Als u de informatie van een virtueel netwerk niet opgeeft, wordt bijvoorbeeld een virtueel netwerk voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bd72-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="8bd72-119">Als u de volgende onderdelen Hallo weglaat, wordt deze voor u gemaakt:</span><span class="sxs-lookup"><span data-stu-id="8bd72-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="8bd72-120">Een load balancer</span><span class="sxs-lookup"><span data-stu-id="8bd72-120">A load balancer</span></span>
- <span data-ttu-id="8bd72-121">Een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="8bd72-121">A virtual network</span></span>
- <span data-ttu-id="8bd72-122">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="8bd72-122">A public IP address</span></span>

<span data-ttu-id="8bd72-123">Bij het kiezen van de installatiekopie van de virtuele machine die u wilt toouse op Hallo virtuele-machineschaalset hello, hebt u enkele mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="8bd72-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="8bd72-124">URN</span><span class="sxs-lookup"><span data-stu-id="8bd72-124">URN</span></span>  
<span data-ttu-id="8bd72-125">Hallo-id van een resource:</span><span class="sxs-lookup"><span data-stu-id="8bd72-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="8bd72-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="8bd72-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="8bd72-127">URN alias</span><span class="sxs-lookup"><span data-stu-id="8bd72-127">URN alias</span></span>  
<span data-ttu-id="8bd72-128">Hallo beschrijvende naam van een URN:</span><span class="sxs-lookup"><span data-stu-id="8bd72-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="8bd72-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="8bd72-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="8bd72-130">Aangepaste resource-id</span><span class="sxs-lookup"><span data-stu-id="8bd72-130">Custom resource id</span></span>  
<span data-ttu-id="8bd72-131">Hallo pad tooan Azure-resource:</span><span class="sxs-lookup"><span data-stu-id="8bd72-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="8bd72-132">**/Subscriptions/Subscription-GUID/resourceGroups/MyResourceGroup/providers/Microsoft.COMPUTE/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="8bd72-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="8bd72-133">Webbron</span><span class="sxs-lookup"><span data-stu-id="8bd72-133">Web resource</span></span>  
<span data-ttu-id="8bd72-134">Hallo pad tooan HTTP-URI:</span><span class="sxs-lookup"><span data-stu-id="8bd72-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="8bd72-135">**http://contoso.BLOB.Core.Windows.NET/vhds/osdiskimage.VHD**</span><span class="sxs-lookup"><span data-stu-id="8bd72-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="8bd72-136">U kunt een lijst met beschikbare installatiekopieën met opvragen `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="8bd72-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="8bd72-137">toocreate een virtuele-machineschaalset, moet u de volgende Hallo opgeven:</span><span class="sxs-lookup"><span data-stu-id="8bd72-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="8bd72-138">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="8bd72-138">Resource group</span></span> 
- <span data-ttu-id="8bd72-139">Naam</span><span class="sxs-lookup"><span data-stu-id="8bd72-139">Name</span></span>
- <span data-ttu-id="8bd72-140">Installatiekopie van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="8bd72-140">Operating system image</span></span>
- <span data-ttu-id="8bd72-141">Verificatie-informatie</span><span class="sxs-lookup"><span data-stu-id="8bd72-141">Authentication information</span></span> 
 
<span data-ttu-id="8bd72-142">Hallo volgende voorbeeld maakt een eenvoudige virtuele-machineschaalset (deze stap kan enkele minuten duren).</span><span class="sxs-lookup"><span data-stu-id="8bd72-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="8bd72-143">Zodra het Hallo-opdracht is voltooid hebt u nu uw virtuele-machineschaalset gemaakt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8bd72-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="8bd72-144">U moet mogelijk tooget Hallo IP-adres van Hallo virtuele machine zodat u tooit verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="8bd72-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="8bd72-145">Met de volgende opdracht Hallo krijgt u een groot aantal verschillende gegevens over Hallo virtuele machine (inclusief Hallo IP-adres).</span><span class="sxs-lookup"><span data-stu-id="8bd72-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="8bd72-146">Maken van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd72-146">Create from PowerShell</span></span>

<span data-ttu-id="8bd72-147">PowerShell is gecompliceerdere toouse dan Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8bd72-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="8bd72-148">Terwijl Azure CLI bevat standaardinstellingen voor netwerkgerelateerde bronnen (zoals load balancers, IP-adressen en virtuele netwerken), PowerShell niet het geval.</span><span class="sxs-lookup"><span data-stu-id="8bd72-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="8bd72-149">Verwijst naar een afbeelding met PowerShell is een iets gecompliceerder te.</span><span class="sxs-lookup"><span data-stu-id="8bd72-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="8bd72-150">U kunt afbeeldingen krijgen Hello cmdlets volgen:</span><span class="sxs-lookup"><span data-stu-id="8bd72-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="8bd72-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="8bd72-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="8bd72-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="8bd72-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="8bd72-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="8bd72-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="8bd72-154">Hallo-cmdlets werk kunt u de eigenschappen in de reeks.</span><span class="sxs-lookup"><span data-stu-id="8bd72-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="8bd72-155">Hier volgt een voorbeeld van hoe tooget alle installatiekopieën voor Hallo **VS-West 2** regio met een uitgever met de naam Hallo **microsoft** erin.</span><span class="sxs-lookup"><span data-stu-id="8bd72-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="8bd72-156">Hallo-werkstroom voor het maken van een virtuele-machineschaalset is als volgt:</span><span class="sxs-lookup"><span data-stu-id="8bd72-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="8bd72-157">Een configuratie-object met informatie over Hallo schaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bd72-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="8bd72-158">Verwijzing Hallo base installatiekopie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="8bd72-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="8bd72-159">Hallo-instellingen configureren: verificatie, VM-voorvoegsel en pass-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8bd72-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="8bd72-160">Netwerken configureren.</span><span class="sxs-lookup"><span data-stu-id="8bd72-160">Configure networking.</span></span>
5. <span data-ttu-id="8bd72-161">Hallo scale set maken.</span><span class="sxs-lookup"><span data-stu-id="8bd72-161">Create hello scale set.</span></span>

<span data-ttu-id="8bd72-162">In dit voorbeeld maakt een eenvoudige twee exemplaar schaal instellen voor een computer met Windows Server 2016 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8bd72-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="8bd72-163">Met behulp van de installatiekopie van een aangepaste virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8bd72-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="8bd72-164">Als u een schaal ingesteld op basis van uw eigen aangepaste installatiekopie, in plaats van die verwijzen naar de installatiekopie van een virtuele machine uit Hallo-galerie maakt Hallo _Set AzureRmVmssStorageProfile_ opdracht er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8bd72-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="8bd72-165">Op basis van een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="8bd72-165">Create from a template</span></span>

<span data-ttu-id="8bd72-166">U kunt een virtuele-machineschaalset ingesteld met behulp van een Azure Resource Manager-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="8bd72-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="8bd72-167">U kunt uw eigen sjabloon maken of gebruik een van de Hallo [sjabloon opslagplaats](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="8bd72-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="8bd72-168">Deze sjablonen kunnen worden geïmplementeerd rechtstreeks tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8bd72-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="8bd72-169">toocreate uw eigen sjabloon maakt u een JSON-tekst-bestand.</span><span class="sxs-lookup"><span data-stu-id="8bd72-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="8bd72-170">Voor algemene informatie over het toocreate en een sjabloon aanpassen, Zie [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="8bd72-171">Er is een voorbeeldsjabloon beschikbaar [op GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="8bd72-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="8bd72-172">Voor meer informatie over hoe toocreate en gebruik die steekproef, Zie [Minimum levensvatbaar schaalset](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="8bd72-173">Maak vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8bd72-173">Create from Visual Studio</span></span>

<span data-ttu-id="8bd72-174">U kunt met Visual Studio een Azure-resourcegroepproject maken en toevoegen van dat een virtuele-machineschaalset sjabloon tooit.</span><span class="sxs-lookup"><span data-stu-id="8bd72-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="8bd72-175">U kunt kiezen of u wilt dat tooimport in GitHub of Hallo galerie van Azure Web Application.</span><span class="sxs-lookup"><span data-stu-id="8bd72-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="8bd72-176">Een PowerShell-script-implementatie wordt ook voor u gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8bd72-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="8bd72-177">Zie voor meer informatie [hoe toocreate een virtuele-machineschaalset met Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="8bd72-178">Maken van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8bd72-178">Create from hello Azure portal</span></span>

<span data-ttu-id="8bd72-179">Hello Azure-portal biedt een handige manier tooquickly maken een schaalset.</span><span class="sxs-lookup"><span data-stu-id="8bd72-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="8bd72-180">Zie voor meer informatie [hoe toocreate een virtuele-machineschaalset Hello Azure-portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd72-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bd72-181">Next steps</span></span>

<span data-ttu-id="8bd72-182">Meer informatie over [gegevensschijven](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="8bd72-183">Meer informatie over hoe te[beheren van uw apps](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="8bd72-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
