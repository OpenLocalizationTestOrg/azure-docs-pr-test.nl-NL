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
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a>Hoe installatiekopieën van toouse verpakker toocreate Windows virtuele machine in Azure
Elke virtuele machine (VM) in Azure wordt gemaakt van een installatiekopie die Hallo Windows-distributie en versie van het besturingssysteem definieert. Voorbeelden van afbeeldingen zijn vooraf geïnstalleerde toepassingen en configuraties. Hello Azure Marketplace biedt veel installatiekopieën van het eerste en derde partij voor de meest voorkomende OS en omgevingen met toepassingen, of u kunt de behoeften van uw eigen aangepaste installatiekopieën die zijn afgestemd tooyour maken. Dit artikel wordt uitgelegd hoe de bron-hulpprogramma voor het openen van toouse Hallo [verpakker](https://www.packer.io/) toodefine en build aangepaste installatiekopieën in Azure.


## <a name="create-azure-resource-group"></a>Azure-resourcegroep maken
Tijdens Hallo maken maakt verpakker tijdelijke Azure-resources als builds Hallo bron-VM. toocapture die VM voor gebruik als een installatiekopie van een gegevensbron, moet u een resourcegroep definiëren. Hallo wordt uitvoer van Hallo verpakker buildproces opgeslagen in deze resourcegroep.

Maak een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a>Azure-referenties maken
Verpakker verifieert met Azure met behulp van een service-principal. Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals verpakker kunt gebruiken. U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt.

Maken van een service principal met [nieuw AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) en machtigingen voor Hallo service principal toocreate toewijzen en -resources beheren met [New AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

tooauthenticate tooAzure, moet u ook tooobtain uw Azure-tenant en de abonnement-id's met [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

U gebruikt deze twee id's in de volgende stap Hallo.


## <a name="define-packer-template"></a>Verpakker sjabloon definiëren
toobuild afbeeldingen, maakt u een sjabloon als een JSON-bestand. In de sjabloon hello, definieert u opbouwfuncties en buildproces provisioners die Hallo werkelijke uitvoeren. Verpakker heeft een [provisioner voor Azure](https://www.packer.io/docs/builders/azure.html) waarmee u toodefine Azure resources, zoals Hallo principal Servicereferenties in Hallo voorgaande stap hebt gemaakt.

Maak een bestand met de naam *windows.json* en inhoud te plakken Hallo volgen. Geef uw eigen waarden voor Hallo volgende:

| Parameter                           | Waar tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Weergave service principal-ID met`$sp.applicationId` |
| *client_secret*                     | U hebt opgegeven in wachtwoord`$securePassword` |
| *tenant_id*                         | De uitvoer van `$sub.TenantId` opdracht |
| *subscription_id*                   | De uitvoer van `$sub.SubscriptionId` opdracht |
| *object_id*                         | Weergave service-principal-object-ID met`$sp.Id` |
| *managed_image_resource_group_name* | Naam van resourcegroep die u hebt gemaakt in de eerste stap Hallo |
| *managed_image_name*                | Naam voor Hallo beheerde installatiekopie die is gemaakt |

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

Deze sjabloon maakt een virtuele machine van Windows Server 2016, IIS installeert en vervolgens generaliseert Hallo VM met Sysprep.


## <a name="build-packer-image"></a>Verpakker installatiekopie maken
Als u nog niet geïnstalleerd op uw lokale machine verpakker hebt [Volg Hallo verpakker installatie-instructies](https://www.packer.io/docs/install/index.html).

Hallo image samenstellen door te geven van uw verpakker sjabloonbestand als volgt:

```bash
./packer build windows.json
```

Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:

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

Het duurt enkele minuten voor verpakker toobuild Hallo VM, Hallo provisioners, uitvoeren en opschonen Hallo-implementatie.


## <a name="create-vm-from-azure-image"></a>Virtuele machine van de afbeelding voor Azure maken
Stel dat een beheerder gebruikersnaam en wachtwoord voor Hallo VM's met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).

```powershell
$cred = Get-Credential
```

U kunt nu een virtuele machine maken van de installatiekopie met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* van *myPackerImage*.

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

Het duurt enkele minuten toocreate Hallo VM.


## <a name="test-vm-and-iis"></a>Virtuele machine en IIS testen
Hallo openbare IP-adres van uw virtuele machine met [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hallo volgende voorbeeld Hallo IP-adres krijgt voor *myPublicIP* eerder hebt gemaakt:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

Vervolgens kunt u in de webbrowser tooa Hallo openbaar IP-adres invoeren.

![Standaardsite van IIS](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld gebruikt u verpakker toocreate een VM-installatiekopie met IIS al geïnstalleerd. U kunt deze VM-installatiekopie samen met de bestaande implementatiewerkstromen, zoals uw app tooVMs van de installatiekopie met Team Services, Ansible, Chef of Puppet hello gemaakt toodeploy gebruiken.

Zie voor aanvullende voorbeeld verpakker sjablonen voor andere Windows-distributies, [deze GitHub-repo-](https://github.com/hashicorp/packer/tree/master/examples/azure).