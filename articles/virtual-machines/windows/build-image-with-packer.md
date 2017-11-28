---
title: "aaaHow toocreate Windows Azure VM-installatiekopieën met verpakker | Microsoft Docs"
description: "Meer informatie over hoe toouse verpakker toocreate installatiekopieën van Windows virtuele machines in Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="98f92-103">Hoe installatiekopieën van toouse verpakker toocreate Windows virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="98f92-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="98f92-104">Elke virtuele machine (VM) in Azure wordt gemaakt van een installatiekopie die Hallo Windows-distributie en versie van het besturingssysteem definieert.</span><span class="sxs-lookup"><span data-stu-id="98f92-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="98f92-105">Voorbeelden van afbeeldingen zijn vooraf geïnstalleerde toepassingen en configuraties.</span><span class="sxs-lookup"><span data-stu-id="98f92-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="98f92-106">Hello Azure Marketplace biedt veel installatiekopieën van het eerste en derde partij voor de meest voorkomende OS en omgevingen met toepassingen, of u kunt de behoeften van uw eigen aangepaste installatiekopieën die zijn afgestemd tooyour maken.</span><span class="sxs-lookup"><span data-stu-id="98f92-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="98f92-107">Dit artikel wordt uitgelegd hoe de bron-hulpprogramma voor het openen van toouse Hallo [verpakker](https://www.packer.io/) toodefine en build aangepaste installatiekopieën in Azure.</span><span class="sxs-lookup"><span data-stu-id="98f92-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="98f92-108">Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="98f92-108">Create Azure resource group</span></span>
<span data-ttu-id="98f92-109">Tijdens Hallo maken maakt verpakker tijdelijke Azure-resources als builds Hallo bron-VM.</span><span class="sxs-lookup"><span data-stu-id="98f92-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="98f92-110">toocapture die VM voor gebruik als een installatiekopie van een gegevensbron, moet u een resourcegroep definiëren.</span><span class="sxs-lookup"><span data-stu-id="98f92-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="98f92-111">Hallo wordt uitvoer van Hallo verpakker buildproces opgeslagen in deze resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="98f92-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="98f92-112">Maak een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="98f92-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="98f92-113">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="98f92-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="98f92-114">Azure-referenties maken</span><span class="sxs-lookup"><span data-stu-id="98f92-114">Create Azure credentials</span></span>
<span data-ttu-id="98f92-115">Verpakker verifieert met Azure met behulp van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="98f92-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="98f92-116">Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals verpakker kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="98f92-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="98f92-117">U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="98f92-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="98f92-118">Maken van een service principal met [nieuw AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) en machtigingen voor Hallo service principal toocreate toewijzen en -resources beheren met [New AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="98f92-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="98f92-119">tooauthenticate tooAzure, moet u ook tooobtain uw Azure-tenant en de abonnement-id's met [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="98f92-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="98f92-120">U gebruikt deze twee id's in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="98f92-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="98f92-121">Verpakker sjabloon definiëren</span><span class="sxs-lookup"><span data-stu-id="98f92-121">Define Packer template</span></span>
<span data-ttu-id="98f92-122">toobuild afbeeldingen, maakt u een sjabloon als een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="98f92-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="98f92-123">In de sjabloon hello, definieert u opbouwfuncties en buildproces provisioners die Hallo werkelijke uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="98f92-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="98f92-124">Verpakker heeft een [provisioner voor Azure](https://www.packer.io/docs/builders/azure.html) waarmee u toodefine Azure resources, zoals Hallo principal Servicereferenties in Hallo voorgaande stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="98f92-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="98f92-125">Maak een bestand met de naam *windows.json* en inhoud te plakken Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="98f92-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="98f92-126">Geef uw eigen waarden voor Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="98f92-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="98f92-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="98f92-127">Parameter</span></span>                           | <span data-ttu-id="98f92-128">Waar tooobtain</span><span class="sxs-lookup"><span data-stu-id="98f92-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="98f92-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="98f92-129">*client_id*</span></span>                         | <span data-ttu-id="98f92-130">Weergave service principal-ID met`$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="98f92-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="98f92-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="98f92-131">*client_secret*</span></span>                     | <span data-ttu-id="98f92-132">U hebt opgegeven in wachtwoord`$securePassword`</span><span class="sxs-lookup"><span data-stu-id="98f92-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="98f92-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="98f92-133">*tenant_id*</span></span>                         | <span data-ttu-id="98f92-134">De uitvoer van `$sub.TenantId` opdracht</span><span class="sxs-lookup"><span data-stu-id="98f92-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="98f92-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="98f92-135">*subscription_id*</span></span>                   | <span data-ttu-id="98f92-136">De uitvoer van `$sub.SubscriptionId` opdracht</span><span class="sxs-lookup"><span data-stu-id="98f92-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="98f92-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="98f92-137">*object_id*</span></span>                         | <span data-ttu-id="98f92-138">Weergave service-principal-object-ID met`$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="98f92-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="98f92-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="98f92-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="98f92-140">Naam van resourcegroep die u hebt gemaakt in de eerste stap Hallo</span><span class="sxs-lookup"><span data-stu-id="98f92-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="98f92-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="98f92-141">*managed_image_name*</span></span>                | <span data-ttu-id="98f92-142">Naam voor Hallo beheerde installatiekopie die is gemaakt</span><span class="sxs-lookup"><span data-stu-id="98f92-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="98f92-143">Deze sjabloon maakt een virtuele machine van Windows Server 2016, IIS installeert en vervolgens generaliseert Hallo VM met Sysprep.</span><span class="sxs-lookup"><span data-stu-id="98f92-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="98f92-144">Verpakker installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="98f92-144">Build Packer image</span></span>
<span data-ttu-id="98f92-145">Als u nog niet geïnstalleerd op uw lokale machine verpakker hebt [Volg Hallo verpakker installatie-instructies](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="98f92-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="98f92-146">Hallo image samenstellen door te geven van uw verpakker sjabloonbestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="98f92-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="98f92-147">Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:</span><span class="sxs-lookup"><span data-stu-id="98f92-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="98f92-148">Het duurt enkele minuten voor verpakker toobuild Hallo VM, Hallo provisioners, uitvoeren en opschonen Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="98f92-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="98f92-149">Virtuele machine van de afbeelding voor Azure maken</span><span class="sxs-lookup"><span data-stu-id="98f92-149">Create VM from Azure Image</span></span>
<span data-ttu-id="98f92-150">Stel dat een beheerder gebruikersnaam en wachtwoord voor Hallo VM's met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="98f92-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="98f92-151">U kunt nu een virtuele machine maken van de installatiekopie met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="98f92-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="98f92-152">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* van *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="98f92-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="98f92-153">Het duurt enkele minuten toocreate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="98f92-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="98f92-154">Virtuele machine en IIS testen</span><span class="sxs-lookup"><span data-stu-id="98f92-154">Test VM and IIS</span></span>
<span data-ttu-id="98f92-155">Hallo openbare IP-adres van uw virtuele machine met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="98f92-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="98f92-156">Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="98f92-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="98f92-157">Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren.</span><span class="sxs-lookup"><span data-stu-id="98f92-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Standaardsite van IIS](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="98f92-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98f92-159">Next steps</span></span>
<span data-ttu-id="98f92-160">In dit voorbeeld gebruikt u verpakker toocreate een VM-installatiekopie met IIS al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="98f92-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="98f92-161">U kunt deze VM-installatiekopie samen met de bestaande implementatiewerkstromen, zoals uw app tooVMs van de installatiekopie met Team Services, Ansible, Chef of Puppet hello gemaakt toodeploy gebruiken.</span><span class="sxs-lookup"><span data-stu-id="98f92-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="98f92-162">Zie voor aanvullende voorbeeld verpakker sjablonen voor andere Windows-distributies, [deze GitHub-repo-](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="98f92-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>