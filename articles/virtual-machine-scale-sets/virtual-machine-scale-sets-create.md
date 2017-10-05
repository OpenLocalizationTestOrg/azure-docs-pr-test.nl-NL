---
title: Maken van een Azure virtuele-machineschaalset | Microsoft Docs
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
ms.openlocfilehash: 32af01aa545c541688128a7ae6bbb82a0e046f2d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="bacb1-103">Maken en implementeren van een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="bacb1-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="bacb1-104">Virtuele-machineschaalsets kunnen gemakkelijk te implementeren en beheren van identieke virtuele machines als een set.</span><span class="sxs-lookup"><span data-stu-id="bacb1-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="bacb1-105">Schaalsets bieden een uiterst schaalbare en aanpasbare berekeningslaag voor toepassingen die grootschalig en installatiekopieën voor Windows-platform, installatiekopieën van virtuele Linux-platform, aangepaste installatiekopieën en -extensies ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="bacb1-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="bacb1-106">Zie voor meer informatie over schaalsets [virtuele-machineschaalsets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="bacb1-107">Deze zelfstudie ziet u het maken van een virtuele-machineschaalset **zonder** met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bacb1-107">This tutorial shows you how to create a virtual machine scale set **without** using the Azure portal.</span></span> <span data-ttu-id="bacb1-108">Zie voor meer informatie over het gebruik van de Azure-portal [het maken van een virtuele-machineschaalset ingesteld met de Azure-portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-108">For information about how to use the Azure portal, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="bacb1-109">Zie voor meer informatie over Azure Resource Manager-resources [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="bacb1-110">Aanmelden bij Azure</span><span class="sxs-lookup"><span data-stu-id="bacb1-110">Sign in to Azure</span></span>

<span data-ttu-id="bacb1-111">Als u Azure PowerShell of Azure CLI 2.0 een schaalset maken, moet u eerst aan te melden bij uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="bacb1-111">If you're using Azure CLI 2.0 or Azure PowerShell to create a scale set, you first need to sign in to your subscription.</span></span>

<span data-ttu-id="bacb1-112">Zie voor meer informatie over het installeren, het instellen en het aanmelden bij Azure met Azure CLI of PowerShell [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) of [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bacb1-112">For more information about how to install, set up, and sign in to Azure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="bacb1-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="bacb1-113">Create a resource group</span></span>

<span data-ttu-id="bacb1-114">U moet eerst een resourcegroep die betrekking heeft op de virtuele-machineschaalset maken.</span><span class="sxs-lookup"><span data-stu-id="bacb1-114">You first need to create a resource group that the virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="bacb1-115">Maken van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bacb1-115">Create from Azure CLI</span></span>

<span data-ttu-id="bacb1-116">U kunt een virtuele-machineschaalset ingesteld met een minimale inspanning maken met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bacb1-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="bacb1-117">Als u standaardwaarden weglaat, zijn ze beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="bacb1-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="bacb1-118">Als u de informatie van een virtueel netwerk niet opgeeft, wordt bijvoorbeeld een virtueel netwerk voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bacb1-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="bacb1-119">Als u de volgende onderdelen weglaat, wordt deze voor u gemaakt:</span><span class="sxs-lookup"><span data-stu-id="bacb1-119">If you omit the following parts, they are created for you:</span></span> 
- <span data-ttu-id="bacb1-120">Een load balancer</span><span class="sxs-lookup"><span data-stu-id="bacb1-120">A load balancer</span></span>
- <span data-ttu-id="bacb1-121">Een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="bacb1-121">A virtual network</span></span>
- <span data-ttu-id="bacb1-122">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="bacb1-122">A public IP address</span></span>

<span data-ttu-id="bacb1-123">Als u de installatiekopie van de virtuele machine die u wilt gebruiken op de virtuele-machineschaalset, hebt u enkele mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="bacb1-123">When choosing the virtual machine image that you want to use on the virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="bacb1-124">URN</span><span class="sxs-lookup"><span data-stu-id="bacb1-124">URN</span></span>  
<span data-ttu-id="bacb1-125">De id van een resource:</span><span class="sxs-lookup"><span data-stu-id="bacb1-125">The identifier of a resource:</span></span>  
<span data-ttu-id="bacb1-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="bacb1-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="bacb1-127">URN alias</span><span class="sxs-lookup"><span data-stu-id="bacb1-127">URN alias</span></span>  
<span data-ttu-id="bacb1-128">De beschrijvende naam van een URN:</span><span class="sxs-lookup"><span data-stu-id="bacb1-128">The friendly name of a URN:</span></span>  
<span data-ttu-id="bacb1-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="bacb1-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="bacb1-130">Aangepaste resource-id</span><span class="sxs-lookup"><span data-stu-id="bacb1-130">Custom resource id</span></span>  
<span data-ttu-id="bacb1-131">Het pad naar een Azure-resource:</span><span class="sxs-lookup"><span data-stu-id="bacb1-131">The path to an Azure resource:</span></span>  
<span data-ttu-id="bacb1-132">**/Subscriptions/Subscription-GUID/resourceGroups/MyResourceGroup/providers/Microsoft.COMPUTE/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="bacb1-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="bacb1-133">Webbron</span><span class="sxs-lookup"><span data-stu-id="bacb1-133">Web resource</span></span>  
<span data-ttu-id="bacb1-134">Het pad naar een HTTP-URI:</span><span class="sxs-lookup"><span data-stu-id="bacb1-134">The path to an HTTP URI:</span></span>  
<span data-ttu-id="bacb1-135">**http://contoso.BLOB.Core.Windows.NET/vhds/osdiskimage.VHD**</span><span class="sxs-lookup"><span data-stu-id="bacb1-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="bacb1-136">U kunt een lijst met beschikbare installatiekopieën met opvragen `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="bacb1-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="bacb1-137">Voor het maken van een virtuele-machineschaalset, moet u het volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="bacb1-137">To create a virtual machine scale set, you must specify the following:</span></span>

- <span data-ttu-id="bacb1-138">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="bacb1-138">Resource group</span></span> 
- <span data-ttu-id="bacb1-139">Naam</span><span class="sxs-lookup"><span data-stu-id="bacb1-139">Name</span></span>
- <span data-ttu-id="bacb1-140">Installatiekopie van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="bacb1-140">Operating system image</span></span>
- <span data-ttu-id="bacb1-141">Verificatie-informatie</span><span class="sxs-lookup"><span data-stu-id="bacb1-141">Authentication information</span></span> 
 
<span data-ttu-id="bacb1-142">Het volgende voorbeeld wordt een eenvoudige virtuele-machineschaalset (deze stap kan enkele minuten duren).</span><span class="sxs-lookup"><span data-stu-id="bacb1-142">The following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="bacb1-143">Zodra de opdracht is voltooid hebt u nu uw virtuele-machineschaalset gemaakt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bacb1-143">Once the command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="bacb1-144">Mogelijk moet u het IP-adres van de virtuele machine zodat u verbinding mee kan maken.</span><span class="sxs-lookup"><span data-stu-id="bacb1-144">You may need to get the IP address of the virtual machine so that you can connect to it.</span></span> <span data-ttu-id="bacb1-145">U kunt een groot aantal verschillende gegevens over de virtuele machine (inclusief het IP-adres) met de volgende opdracht ophalen.</span><span class="sxs-lookup"><span data-stu-id="bacb1-145">You can get a lot of different information about the virtual machine (including the IP address) with the following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="bacb1-146">Maken van PowerShell</span><span class="sxs-lookup"><span data-stu-id="bacb1-146">Create from PowerShell</span></span>

<span data-ttu-id="bacb1-147">PowerShell is gecompliceerdere te gebruiken dan de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bacb1-147">PowerShell is more complicated to use than Azure CLI.</span></span> <span data-ttu-id="bacb1-148">Terwijl Azure CLI bevat standaardinstellingen voor netwerkgerelateerde bronnen (zoals load balancers, IP-adressen en virtuele netwerken), PowerShell niet het geval.</span><span class="sxs-lookup"><span data-stu-id="bacb1-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="bacb1-149">Verwijst naar een afbeelding met PowerShell is een iets gecompliceerder te.</span><span class="sxs-lookup"><span data-stu-id="bacb1-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="bacb1-150">U kunt afbeeldingen met de volgende cmdlets krijgen:</span><span class="sxs-lookup"><span data-stu-id="bacb1-150">You can get images with the following cmdlets:</span></span>

1. <span data-ttu-id="bacb1-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="bacb1-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="bacb1-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="bacb1-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="bacb1-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="bacb1-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="bacb1-154">Het werk cmdlets kunt u de eigenschappen in de reeks.</span><span class="sxs-lookup"><span data-stu-id="bacb1-154">The cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="bacb1-155">Hier volgt een voorbeeld van hoe u alle installatiekopieën voor de **VS-West 2** regio met een uitgever met de naam **microsoft** erin.</span><span class="sxs-lookup"><span data-stu-id="bacb1-155">Here is an example of how to get all images for the **West US 2** region with a publisher that has the name **microsoft** in it.</span></span>

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

<span data-ttu-id="bacb1-156">De werkstroom voor het maken van een virtuele-machineschaalset is als volgt:</span><span class="sxs-lookup"><span data-stu-id="bacb1-156">The workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="bacb1-157">Een configuratie-object met informatie over de schaalaanpassingsset maken.</span><span class="sxs-lookup"><span data-stu-id="bacb1-157">Create a config object that holds information about the scale set.</span></span>
2. <span data-ttu-id="bacb1-158">Verwijzen naar de basisinstallatiekopie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="bacb1-158">Reference the base OS image.</span></span>
3. <span data-ttu-id="bacb1-159">Configureer de instellingen van besturingssysteem: verificatie, VM-voorvoegsel en pass-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bacb1-159">Configure the operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="bacb1-160">Netwerken configureren.</span><span class="sxs-lookup"><span data-stu-id="bacb1-160">Configure networking.</span></span>
5. <span data-ttu-id="bacb1-161">Maak de schaal.</span><span class="sxs-lookup"><span data-stu-id="bacb1-161">Create the scale set.</span></span>

<span data-ttu-id="bacb1-162">In dit voorbeeld maakt een eenvoudige twee exemplaar schaal instellen voor een computer met Windows Server 2016 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bacb1-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create the virtual network resources

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

# Attach the virtual network to the IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="bacb1-163">Met behulp van de installatiekopie van een aangepaste virtuele machine</span><span class="sxs-lookup"><span data-stu-id="bacb1-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="bacb1-164">Als u een schaal ingesteld op basis van uw eigen aangepaste installatiekopie, in plaats van die verwijzen naar de installatiekopie van een virtuele machine uit de galerie maakt de _Set AzureRmVmssStorageProfile_ opdracht er als volgt:</span><span class="sxs-lookup"><span data-stu-id="bacb1-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from the gallery, the _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="bacb1-165">Op basis van een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="bacb1-165">Create from a template</span></span>

<span data-ttu-id="bacb1-166">U kunt een virtuele-machineschaalset ingesteld met behulp van een Azure Resource Manager-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="bacb1-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="bacb1-167">U kunt uw eigen sjabloon maken of gebruik een van de [sjabloon opslagplaats](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="bacb1-167">You can create your own template or use one from the [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="bacb1-168">Deze sjablonen kunnen rechtstreeks worden geïmplementeerd in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bacb1-168">These templates can be deployed directly to your Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="bacb1-169">Als u wilt uw eigen sjabloon maakt, moet u een JSON-tekstbestand maken.</span><span class="sxs-lookup"><span data-stu-id="bacb1-169">To create your own template, you create a JSON text file.</span></span> <span data-ttu-id="bacb1-170">Raadpleeg voor algemene informatie over het maken en aanpassen van een sjabloon [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-170">For general information about how to create and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="bacb1-171">Er is een voorbeeldsjabloon beschikbaar [op GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="bacb1-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="bacb1-172">Zie voor meer informatie over het maken en gebruiken dat voorbeeld [Minimum levensvatbaar schaalset](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-172">For more information about how to create and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="bacb1-173">Maak vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bacb1-173">Create from Visual Studio</span></span>

<span data-ttu-id="bacb1-174">U kunt met Visual Studio een Azure-resourcegroepproject maken en toevoegen van dat een virtuele-machineschaalset sjabloon ingesteld op het.</span><span class="sxs-lookup"><span data-stu-id="bacb1-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template to it.</span></span> <span data-ttu-id="bacb1-175">U kunt kiezen of u wilt importeren in GitHub of de galerie van Azure Web Application.</span><span class="sxs-lookup"><span data-stu-id="bacb1-175">You can choose whether you want to import it from GitHub or the Azure Web Application Gallery.</span></span> <span data-ttu-id="bacb1-176">Een PowerShell-script-implementatie wordt ook voor u gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="bacb1-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="bacb1-177">Zie voor meer informatie [het maken van een virtuele-machineschaalset instellen met Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-177">For more information, see [How to create a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-the-azure-portal"></a><span data-ttu-id="bacb1-178">Maken van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="bacb1-178">Create from the Azure portal</span></span>

<span data-ttu-id="bacb1-179">De Azure portal biedt een handige manier om snel een scale-set maken.</span><span class="sxs-lookup"><span data-stu-id="bacb1-179">The Azure portal provides a convenient way to quickly create a scale set.</span></span> <span data-ttu-id="bacb1-180">Zie voor meer informatie [het maken van een virtuele-machineschaalset ingesteld met de Azure-portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-180">For more information, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bacb1-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bacb1-181">Next steps</span></span>

<span data-ttu-id="bacb1-182">Meer informatie over [gegevensschijven](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="bacb1-183">Meer informatie over hoe [beheren van uw apps](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="bacb1-183">Learn how to [manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
