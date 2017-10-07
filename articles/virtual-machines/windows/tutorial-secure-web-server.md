---
title: aaaSecure IIS met SSL-certificaten in Azure | Microsoft Docs
description: Meer informatie over hoe toosecure Hallo IIS web server SSL-certificaten op een Windows-virtuele machine in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>IIS-webserver met SSL-certificaten op een virtuele Windows-machine in Azure beveiligen
toosecure webservers, een certificaat Later SSL (Secure Sockets) kan worden gebruikt tooencrypt internetverkeer. Deze SSL-certificaten kunnen worden opgeslagen in Azure Sleutelkluis en beveiligde implementaties van certificaten tooWindows virtuele machines (VM's) in Azure toestaan. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maken van een Azure Sleutelkluis
> * Upload een certificaat toohello Sleutelkluis of genereren
> * Een virtuele machine maken en Hallo IIS-webserver installeren
> * Hallo certificaat invoeren in Hallo VM en IIS te configureren met een SSL-binding

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).


## <a name="overview"></a>Overzicht
Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden. Sleutelkluis helpt Hallo certificate management stroomlijnen en kunt u toomaintain beheer van sleutels die toegang hebben tot deze certificaten. U kunt een zelfondertekend certificaat in de Sleutelkluis maken of een bestaande, vertrouwd certificaat dat u al bezit uploaden.

In plaats van met een aangepaste VM-installatiekopie die certificaten bevat standaard uitbreidbaar module u certificaten kunt invoeren in een actieve virtuele machine. Dit proces zorgt ervoor dat de meest recente certificaten Hallo tijdens de implementatie op een webserver zijn geïnstalleerd. Als u vernieuwen of vervangen van een certificaat, hebt u niet ook toocreate een nieuwe aangepaste VM-installatiekopie. Hallo nieuwste certificaten worden automatisch ingevoegd als u extra virtuele machines maken. Tijdens het hele proces hello, Hallo certificaten nooit laat hello Azure-platform of beschikbaar worden gesteld in een script, opdrachtregel geschiedenis of sjabloon.


## <a name="create-an-azure-key-vault"></a>Maken van een Azure Sleutelkluis
Voordat u certificaten en een Sleutelkluis maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupSecureWeb* in Hallo *VS-Oost* locatie:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

Maak vervolgens een Sleutelkluis met [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault). Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters. Vervang `<mykeyvault>` in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis Hallo:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Een certificaat genereren en opslaan in de Sleutelkluis
Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [importeren AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate). Voor deze zelfstudie hello volgende voorbeeld ziet u hoe u een zelfondertekend certificaat met genereren [toevoegen AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) dat wordt gebruikt certificaat standaardbeleid uit Hallo [ Nieuwe AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy). 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a>Een virtuele machine maken
Een gebruikersnaam voor de beheerder en het wachtwoord voor virtuele machine met Hallo set [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Nu kunt u de virtuele machine met Hallo [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hallo volgende voorbeeld maakt Hallo vereist virtuele netwerkonderdelen, Hallo OS-configuratie, en maakt vervolgens een virtuele machine met de naam *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

Het duurt enkele minuten duren voordat Hallo VM toobe gemaakt. Hallo laatste stap maakt gebruik van hello Azure aangepaste Scriptextensie tooinstall Hallo IIS-webserver met [Set AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).


## <a name="add-a-certificate-toovm-from-key-vault"></a>Een certificaat tooVM van Sleutelkluis toevoegen
tooadd hello certificaat van de Sleutelkluis tooa VM, Hallo-ID van uw certificaat met aanvragen [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret). Hallo certificaat toohello VM toevoegen met [toevoegen AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>IIS toouse Hallo certificaat configureren
Gebruik de aangepaste Scriptextensie opnieuw met Hallo [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate Hallo IIS-configuratie. Deze update is van toepassing hello certificaat van de Sleutelkluis tooIIS ingevoegd en Hallo web binding configureert:

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a>Test Hallo beveiligde web-app
Hallo openbare IP-adres van uw virtuele machine met [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress). Hallo volgende voorbeeld Hallo IP-adres krijgt voor `myPublicIP` eerder hebt gemaakt:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

Nu kunt u een webbrowser openen en voer `https://<myPublicIP>` in de adresbalk Hallo. Selecteer tooaccept Hallo beveiligingswaarschuwing als u een zelfondertekend certificaat gebruikt **Details** en vervolgens **gaat u op de webpagina toohello**:

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-secure-web-server/browser-warning.png)

Uw beveiligde IIS-website wordt weergegeven zoals in het volgende voorbeeld Hallo:

![Weergave actief beveiligde IIS-website](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt beveiligd u een IIS-webserver met een SSL-certificaat dat is opgeslagen in Azure Sleutelkluis. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Maken van een Azure Sleutelkluis
> * Upload een certificaat toohello Sleutelkluis of genereren
> * Een virtuele machine maken en Hallo IIS-webserver installeren
> * Hallo certificaat invoeren in Hallo VM en IIS te configureren met een SSL-binding

Volg deze link toosee vooraf gemaakte virtuele machine scriptvoorbeelden.

> [!div class="nextstepaction"]
> [Windows virtuele machine scriptvoorbeelden](./powershell-samples.md)