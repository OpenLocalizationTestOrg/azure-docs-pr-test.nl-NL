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
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="c8da4-103">IIS-webserver met SSL-certificaten op een virtuele Windows-machine in Azure beveiligen</span><span class="sxs-lookup"><span data-stu-id="c8da4-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="c8da4-104">toosecure webservers, een certificaat Later SSL (Secure Sockets) kan worden gebruikt tooencrypt internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="c8da4-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="c8da4-105">Deze SSL-certificaten kunnen worden opgeslagen in Azure Sleutelkluis en beveiligde implementaties van certificaten tooWindows virtuele machines (VM's) in Azure toestaan.</span><span class="sxs-lookup"><span data-stu-id="c8da4-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="c8da4-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="c8da4-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8da4-107">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c8da4-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="c8da4-108">Upload een certificaat toohello Sleutelkluis of genereren</span><span class="sxs-lookup"><span data-stu-id="c8da4-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="c8da4-109">Een virtuele machine maken en Hallo IIS-webserver installeren</span><span class="sxs-lookup"><span data-stu-id="c8da4-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="c8da4-110">Hallo certificaat invoeren in Hallo VM en IIS te configureren met een SSL-binding</span><span class="sxs-lookup"><span data-stu-id="c8da4-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="c8da4-111">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c8da4-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c8da4-112">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="c8da4-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="c8da4-113">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c8da4-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="c8da4-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c8da4-114">Overview</span></span>
<span data-ttu-id="c8da4-115">Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="c8da4-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="c8da4-116">Sleutelkluis helpt Hallo certificate management stroomlijnen en kunt u toomaintain beheer van sleutels die toegang hebben tot deze certificaten.</span><span class="sxs-lookup"><span data-stu-id="c8da4-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="c8da4-117">U kunt een zelfondertekend certificaat in de Sleutelkluis maken of een bestaande, vertrouwd certificaat dat u al bezit uploaden.</span><span class="sxs-lookup"><span data-stu-id="c8da4-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="c8da4-118">In plaats van met een aangepaste VM-installatiekopie die certificaten bevat standaard uitbreidbaar module u certificaten kunt invoeren in een actieve virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c8da4-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="c8da4-119">Dit proces zorgt ervoor dat de meest recente certificaten Hallo tijdens de implementatie op een webserver zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c8da4-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="c8da4-120">Als u vernieuwen of vervangen van een certificaat, hebt u niet ook toocreate een nieuwe aangepaste VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c8da4-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="c8da4-121">Hallo nieuwste certificaten worden automatisch ingevoegd als u extra virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="c8da4-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="c8da4-122">Tijdens het hele proces hello, Hallo certificaten nooit laat hello Azure-platform of beschikbaar worden gesteld in een script, opdrachtregel geschiedenis of sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c8da4-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="c8da4-123">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c8da4-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="c8da4-124">Voordat u certificaten en een Sleutelkluis maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c8da4-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c8da4-125">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupSecureWeb* in Hallo *VS-Oost* locatie:</span><span class="sxs-lookup"><span data-stu-id="c8da4-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="c8da4-126">Maak vervolgens een Sleutelkluis met [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="c8da4-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="c8da4-127">Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="c8da4-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="c8da4-128">Vervang `<mykeyvault>` in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis Hallo:</span><span class="sxs-lookup"><span data-stu-id="c8da4-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="c8da4-129">Een certificaat genereren en opslaan in de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c8da4-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="c8da4-130">Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [importeren AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="c8da4-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="c8da4-131">Voor deze zelfstudie hello volgende voorbeeld ziet u hoe u een zelfondertekend certificaat met genereren [toevoegen AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) dat wordt gebruikt certificaat standaardbeleid uit Hallo [ Nieuwe AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="c8da4-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="c8da4-132">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="c8da4-132">Create a virtual machine</span></span>
<span data-ttu-id="c8da4-133">Een gebruikersnaam voor de beheerder en het wachtwoord voor virtuele machine met Hallo set [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="c8da4-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="c8da4-134">Nu kunt u de virtuele machine met Hallo [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c8da4-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="c8da4-135">Hallo volgende voorbeeld maakt Hallo vereist virtuele netwerkonderdelen, Hallo OS-configuratie, en maakt vervolgens een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="c8da4-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="c8da4-136">Het duurt enkele minuten duren voordat Hallo VM toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c8da4-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="c8da4-137">Hallo laatste stap maakt gebruik van hello Azure aangepaste Scriptextensie tooinstall Hallo IIS-webserver met [Set AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="c8da4-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="c8da4-138">Een certificaat tooVM van Sleutelkluis toevoegen</span><span class="sxs-lookup"><span data-stu-id="c8da4-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="c8da4-139">tooadd hello certificaat van de Sleutelkluis tooa VM, Hallo-ID van uw certificaat met aanvragen [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="c8da4-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="c8da4-140">Hallo certificaat toohello VM toevoegen met [toevoegen AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="c8da4-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="c8da4-141">IIS toouse Hallo certificaat configureren</span><span class="sxs-lookup"><span data-stu-id="c8da4-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="c8da4-142">Gebruik de aangepaste Scriptextensie opnieuw met Hallo [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate Hallo IIS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c8da4-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="c8da4-143">Deze update is van toepassing hello certificaat van de Sleutelkluis tooIIS ingevoegd en Hallo web binding configureert:</span><span class="sxs-lookup"><span data-stu-id="c8da4-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

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


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="c8da4-144">Test Hallo beveiligde web-app</span><span class="sxs-lookup"><span data-stu-id="c8da4-144">Test hello secure web app</span></span>
<span data-ttu-id="c8da4-145">Hallo openbare IP-adres van uw virtuele machine met [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="c8da4-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="c8da4-146">Hallo volgende voorbeeld Hallo IP-adres krijgt voor `myPublicIP` eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="c8da4-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="c8da4-147">Nu kunt u een webbrowser openen en voer `https://<myPublicIP>` in de adresbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8da4-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="c8da4-148">Selecteer tooaccept Hallo beveiligingswaarschuwing als u een zelfondertekend certificaat gebruikt **Details** en vervolgens **gaat u op de webpagina toohello**:</span><span class="sxs-lookup"><span data-stu-id="c8da4-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="c8da4-150">Uw beveiligde IIS-website wordt weergegeven zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="c8da4-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Weergave actief beveiligde IIS-website](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="c8da4-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8da4-152">Next steps</span></span>

<span data-ttu-id="c8da4-153">In deze zelfstudie maakt beveiligd u een IIS-webserver met een SSL-certificaat dat is opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="c8da4-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="c8da4-154">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="c8da4-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8da4-155">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="c8da4-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="c8da4-156">Upload een certificaat toohello Sleutelkluis of genereren</span><span class="sxs-lookup"><span data-stu-id="c8da4-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="c8da4-157">Een virtuele machine maken en Hallo IIS-webserver installeren</span><span class="sxs-lookup"><span data-stu-id="c8da4-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="c8da4-158">Hallo certificaat invoeren in Hallo VM en IIS te configureren met een SSL-binding</span><span class="sxs-lookup"><span data-stu-id="c8da4-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="c8da4-159">Volg deze link toosee vooraf gemaakte virtuele machine scriptvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c8da4-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8da4-160">Windows virtuele machine scriptvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="c8da4-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)