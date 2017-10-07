---
title: aaaEncrypt schijven op een Windows-VM in Azure | Microsoft Docs
description: Hoe tooencrypt virtuele schijven op een Windows-VM voor verbeterde beveiliging met Azure PowerShell
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Hoe tooencrypt virtuele schijven op een virtuele machine van Windows
Voor de uitgebreide virtuele machine (VM) beveiliging en naleving, kunnen virtuele schijven in Azure worden versleuteld. Schijven worden versleuteld met behulp van de cryptografische sleutels die worden beveiligd in een Azure Sleutelkluis. U kunt het gebruik ervan controleren en beheren van deze cryptografische sleutels. Dit artikel details hoe tooencrypt virtuele schijven op een Windows-VM met Azure PowerShell. U kunt ook [versleutelen van een Linux-VM met hello Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Overzicht van schijfversleuteling
Virtuele schijven op Windows-VM's zijn versleuteld in rust met Bitlocker. Er zijn geen kosten voor het versleutelen van virtuele schijven in Azure. Cryptografische sleutels worden opgeslagen in Azure Key Vault met software-beveiliging, of u kunt importeren of genereren van uw tooFIPS gecertificeerde sleutels in Hardware Security Modules (HSM's) 140-2 level 2-standaarden. Deze cryptografische sleutels zijn gebruikte tooencrypt en ontsleutelen van virtuele schijven gekoppelde tooyour VM. U beheer behouden over deze cryptografische sleutels en het gebruik ervan kunt controleren. Een Azure Active Directory service-principal biedt een veilige mechanisme voor het uitgeven van deze cryptografische sleutels als virtuele machines van stroom in- of uitschakelen voorzien worden.

Hallo-proces voor het versleutelen van een virtuele machine is als volgt:

1. Maak een cryptografische sleutel in een Azure Sleutelkluis.
2. Configureer Hallo cryptografische sleutel toobe kan worden gebruikt voor het versleutelen van schijven.
3. tooread hello cryptografiesleutel van hello Azure Sleutelkluis, maak een Azure Active Directory-service principal met de juiste machtigingen Hallo.
4. Uitgeven Hallo opdracht tooencrypt uw virtuele schijven, opgeven hello Azure Active Directory-service-principal en de juiste cryptografische sleutel toobe gebruikt.
5. Hello Azure Active Directory-principal serviceaanvragen Hallo vereist cryptografiesleutel van Azure Sleutelkluis.
6. Hallo virtuele schijven worden versleuteld met behulp van de cryptografische sleutel Hallo opgegeven.

## <a name="encryption-process"></a>Versleutelingsproces
Schijfversleuteling is afhankelijk van Hallo extra onderdelen te volgen:

* **Azure Sleutelkluis** -toosafeguard cryptografische sleutels en geheimen die worden gebruikt voor Hallo schijf tokenversleuteling /-ontsleuteling proces gebruikt. 
  * Als dit bestaat, kunt u een bestaande Azure Sleutelkluis. U hoeft geen toodedicate een Sleutelkluis tooencrypting schijven.
  * tooseparate administratieve grenzen en sleutel zichtbaarheid, kunt u een speciale Sleutelkluis.
* **Azure Active Directory** - ingangen Hallo veilig uitwisselen van vereiste cryptografische sleutels en verificatie voor acties aangevraagd. 
  * Doorgaans kunt u een bestaand Azure Active Directory-exemplaar waarin de toepassing.
  * Hallo service-principal biedt een mechanisme voor beveiligde toorequest en de juiste cryptografische sleutels Hallo worden uitgegeven. U ontwikkelt een werkelijke toepassing die is geïntegreerd met Azure Active Directory niet.

## <a name="requirements-and-limitations"></a>Vereisten en beperkingen
Ondersteunde scenario's en vereisten voor de schijfversleuteling:

* Inschakelen van versleuteling op nieuwe Windows VM's van Azure Marketplace-installatiekopieën of aangepaste VHD-installatiekopie.
* Inschakelen van versleuteling op bestaande Windows virtuele machines in Azure.
* Inschakelen van versleuteling op Windows-virtuele machines die zijn geconfigureerd met behulp van opslagruimten.
* Het uitschakelen van versleuteling op besturingssysteem en stations voor VM's van Windows.
* Alle resources (zoals Sleutelkluis, een opslagaccount en een VM) moet in Hallo dezelfde Azure-regio en -abonnement.
* Standard-laag VM's, zoals een, D, DS, G en GS-serie virtuele machines.

Schijfversleuteling is momenteel niet ondersteund in Hallo volgen scenario's:

* Basisstaffel virtuele machines.
* Virtuele machines gemaakt met behulp van Hallo klassieke implementatiemodel.
* Hallo cryptografische sleutels op een al is versleuteld virtuele machine wordt bijgewerkt.
* Integratie met on-premises-Service voor sleutelbeheer.

## <a name="create-azure-key-vault-and-keys"></a>Azure Sleutelkluis en de sleutels maken
Voordat u begint, Controleer of de nieuwste versie van die Hallo van hello Azure PowerShell-module is geïnstalleerd. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). In de gehele opdrachtvoorbeelden hello, vervangen door alle voorbeeldparameters uw eigen namen, locatie en sleutelwaarden. Hallo volgende voorbeelden wordt gebruikt een conventie *myResourceGroup*, *myKeyVault*, *myVM*, enzovoort.

de eerste stap Hallo toocreate een toostore Azure Sleutelkluis is de cryptografiesleutels. Azure Sleutelkluis sleutels en geheimen, kunnen opslaan of wachtwoorden die u toelaten om toosecurely ze implementeert in uw toepassingen en services. Voor versleuteling van de virtuele schijf, een Sleutelkluis toostore een cryptografische sleutel die is gebruikt tooencrypt maken of ontsleutelen van de virtuele schijven. 

Hello Azure Key Vault provider binnen uw Azure-abonnement met ingeschakeld [registreren AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld wordt een Resourcegroepnaam *myResourceGroup* in Hallo *VS-Oost* locatie:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Hello Azure Key Vault met Hallo cryptografische sleutels en het bijbehorende compute resources, zoals opslag en virtuele machine zelf Hallo moeten zich bevinden in Hallo dezelfde regio. Maken van een Azure Key Vault met [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) en Hallo Sleutelkluis voor gebruik met schijfversleuteling inschakelen. Geef een unieke naam van de Sleutelkluis voor *keyVaultName* als volgt:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

U kunt met behulp van software of Hardware Security Model (HSM) protection cryptografiesleutels opslaan. Een HSM, moet een premium Sleutelkluis. Er is een extra kosten toocreating premium Sleutelkluis in plaats van standaard Sleutelkluis waarmee softwarematige beveiligde sleutels worden opgeslagen. een premium Sleutelkluis, in de voorgaande stap Hallo toocreate toevoegen Hallo *- Sku 'Premium'* parameters. Hallo volgende voorbeeld wordt softwarematige beveiligde sleutels omdat er een standaard Sleutelkluis hebt gemaakt. 

Voor beide beveiligingsmodellen moet hello Azure-platform toobe toorequest-Hallo cryptografiesleutels toegang verleend als Hallo VM wordt opgestart toodecrypt Hallo virtuele schijven. Maken van een cryptografische sleutel in uw Sleutelkluis met [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Hallo volgende voorbeeld wordt een sleutel met de naam *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Hello Azure Active Directory-service-principal maken
Wanneer virtuele schijven worden versleuteld en ontsleuteld, geeft u een account toohandle Hallo-authenticatie en uitwisselen van cryptografische sleutels uit Sleutelkluis. Dit account, een Azure Active Directory service-principal kunt hello Azure-platform toorequest Hallo juiste cryptografische sleutels namens Hallo VM. Een standaardexemplaar van de Azure Active Directory is beschikbaar in uw abonnement, hoewel veel organisaties hebben speciale mappen van Azure Active Directory.

Een service-principal maken in Azure Active Directory met [nieuw AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). een beveiligd wachtwoord toospecify Volg Hallo [wachtwoordbeleid en -beperkingen in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully versleutelen of ontsleutelen van virtuele schijven, machtigingen op Hallo cryptografische sleutel die wordt opgeslagen in de Sleutelkluis moet set toopermit hello Azure Active Directory service principal tooread Hallo sleutels. Machtigingen instellen voor uw Sleutelkluis met [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Virtuele machine maken
tootest Hallo versleutelingsproces, gaan we een virtuele machine te maken. Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* met behulp van een *Windows Server 2016 Datacenter* afbeelding:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Virtuele machine versleutelen
tooencrypt hello virtuele schijven, u samenbrengen alle vorige Hallo-onderdelen:

1. Hello Azure Active Directory service-principal en wachtwoord opgeven.
2. Hallo Sleutelkluis toostore Hallo metagegevens voor uw versleutelde schijven opgeven.
3. Hallo cryptografische sleutels toouse voor Hallo daadwerkelijke versleuteling en ontsleuteling opgeven.
4. Geef op of u tooencrypt Hallo OS schijf, Hallo gegevensschijven of alle wilt.

Versleutelen van uw virtuele machine met [Set AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) hello Azure Key Vault sleutel en Azure Active Directory-service-principal referenties gebruiken. Hallo volgende voorbeeld haalt alle Hallo belangrijke informatie en vervolgens versleutelt Hallo VM met de naam *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Hallo vragen toocontinue met Hallo VM versleuteling accepteren. Hallo VM wordt opnieuw gestart tijdens het Hallo-proces. Zodra het Hallo-codering is voltooid en hello VM opnieuw is opgestart, lezen Hallo coderingsstatus met [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het beheren van Azure Sleutelkluis [Sleutelkluis instellen voor virtuele machines](key-vault-setup.md).
* Zie voor meer informatie over schijfversleuteling, zoals het voorbereiden van een versleutelde aangepaste VM tooupload tooAzure, [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).
