---
title: IIS beveiligen met SSL-certificaten in Azure | Microsoft Docs
description: Meer informatie over het beveiligen van de IIS-webserver met SSL-certificaten op een Windows-virtuele machine in Azure
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
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="bfbed-103">IIS-webserver met SSL-certificaten op een virtuele Windows-machine in Azure beveiligen</span><span class="sxs-lookup"><span data-stu-id="bfbed-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="bfbed-104">Beveiligde webservers, kan een certificaat Later SSL (Secure Sockets) worden gebruikt voor het versleutelen van internetverkeer.</span><span class="sxs-lookup"><span data-stu-id="bfbed-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="bfbed-105">Deze SSL-certificaten kunnen worden opgeslagen in Azure Sleutelkluis en beveiligde implementaties van certificaten aan Windows virtuele machines (VM's) in Azure toestaan.</span><span class="sxs-lookup"><span data-stu-id="bfbed-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="bfbed-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="bfbed-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bfbed-107">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bfbed-108">Genereren of een certificaat uploaden naar de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="bfbed-109">Een virtuele machine maken en de IIS-webserver installeren</span><span class="sxs-lookup"><span data-stu-id="bfbed-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="bfbed-110">Het certificaat invoeren in de virtuele machine en IIS te configureren met een SSL-binding</span><span class="sxs-lookup"><span data-stu-id="bfbed-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bfbed-111">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="bfbed-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bfbed-112">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="bfbed-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="bfbed-113">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bfbed-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="bfbed-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bfbed-114">Overview</span></span>
<span data-ttu-id="bfbed-115">Azure Sleutelkluis beschermt cryptografische sleutels en geheimen, zoals certificaten of wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="bfbed-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="bfbed-116">Sleutelkluis helpt het beheerproces van het certificaat te stroomlijnen en kunt u controle houdt over sleutels die toegang hebben tot deze certificaten.</span><span class="sxs-lookup"><span data-stu-id="bfbed-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="bfbed-117">U kunt een zelfondertekend certificaat in de Sleutelkluis maken of een bestaande, vertrouwd certificaat dat u al bezit uploaden.</span><span class="sxs-lookup"><span data-stu-id="bfbed-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="bfbed-118">In plaats van met een aangepaste VM-installatiekopie die certificaten bevat standaard uitbreidbaar module u certificaten kunt invoeren in een actieve virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfbed-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="bfbed-119">Dit proces zorgt ervoor dat de meest recente certificaten tijdens de implementatie op een webserver zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bfbed-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="bfbed-120">Als u vernieuwen of vervangen van een certificaat, hebt u niet ook een nieuwe aangepaste VM-installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="bfbed-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="bfbed-121">De meest recente certificaten worden automatisch toegevoegd als u extra virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="bfbed-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="bfbed-122">Tijdens het hele proces, de certificaten nooit laat u de Azure-platform of beschikbaar worden gesteld in een script, opdrachtregel geschiedenis of sjabloon.</span><span class="sxs-lookup"><span data-stu-id="bfbed-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="bfbed-123">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="bfbed-124">Voordat u certificaten en een Sleutelkluis maken kunt, maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bfbed-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bfbed-125">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroupSecureWeb* in de *VS-Oost* locatie:</span><span class="sxs-lookup"><span data-stu-id="bfbed-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="bfbed-126">Maak vervolgens een Sleutelkluis met [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="bfbed-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="bfbed-127">Elke Sleutelkluis moet een unieke naam hebben en moet alle kleine letters.</span><span class="sxs-lookup"><span data-stu-id="bfbed-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="bfbed-128">Vervang `<mykeyvault>` in het volgende voorbeeld met de naam van uw eigen unieke Sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="bfbed-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="bfbed-129">Een certificaat genereren en opslaan in de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="bfbed-130">Voor gebruik in productieomgevingen, moet u een geldig certificaat dat is ondertekend door een vertrouwde provider met importeren [importeren AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="bfbed-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="bfbed-131">Voor deze zelfstudie, het volgende voorbeeld toont hoe kunt u een zelfondertekend certificaat met genereren [toevoegen AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) die gebruikmaakt van het standaardbeleid voor het certificaat van [ Nieuwe AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="bfbed-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="bfbed-132">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="bfbed-132">Create a virtual machine</span></span>
<span data-ttu-id="bfbed-133">Stel dat een beheerder gebruikersnaam en wachtwoord voor de virtuele machine met [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="bfbed-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bfbed-134">Nu kunt u de virtuele machine met [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bfbed-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="bfbed-135">Het volgende voorbeeld maakt de vereiste virtuele netwerkonderdelen, de configuratie van het besturingssysteem, en maakt vervolgens een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="bfbed-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="bfbed-136">Het duurt enkele minuten duren voordat de virtuele machine moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bfbed-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="bfbed-137">De laatste stap de Azure-extensie voor aangepaste scripts gebruikt voor het installeren van de IIS-webserver met [Set AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="bfbed-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="bfbed-138">Een certificaat toevoegen aan de virtuele machine uit Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="bfbed-139">Om het certificaat van de Sleutelkluis toevoegen aan een virtuele machine, krijgen de ID van het certificaat met [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="bfbed-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="bfbed-140">Het certificaat toevoegen aan de virtuele machine met [toevoegen AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="bfbed-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="bfbed-141">IIS configureren voor het gebruik van het certificaat</span><span class="sxs-lookup"><span data-stu-id="bfbed-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="bfbed-142">Gebruik de aangepaste Scriptextensie opnieuw met [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) de IIS-configuratie bij te werken.</span><span class="sxs-lookup"><span data-stu-id="bfbed-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="bfbed-143">Deze update van toepassing is het certificaat van de Sleutelkluis ingevoegd op IIS en configureert u de web-binding:</span><span class="sxs-lookup"><span data-stu-id="bfbed-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

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


### <a name="test-the-secure-web-app"></a><span data-ttu-id="bfbed-144">Testen van de beveiligde web-app</span><span class="sxs-lookup"><span data-stu-id="bfbed-144">Test the secure web app</span></span>
<span data-ttu-id="bfbed-145">Het openbare IP-adres van uw virtuele machine met [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bfbed-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bfbed-146">Het volgende voorbeeld verkrijgt het IP-adres voor `myPublicIP` eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="bfbed-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="bfbed-147">Nu kunt u een webbrowser openen en voer `https://<myPublicIP>` in de adresbalk.</span><span class="sxs-lookup"><span data-stu-id="bfbed-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="bfbed-148">Voor het accepteren van de beveiligingswaarschuwing als u een zelfondertekend certificaat gebruikt, selecteert u **Details** en vervolgens **gaat u naar de webpagina**:</span><span class="sxs-lookup"><span data-stu-id="bfbed-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![Beveiligingswaarschuwing voor web browser accepteren](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="bfbed-150">Uw beveiligde IIS-website wordt weergegeven zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="bfbed-150">Your secured IIS website is then displayed as in the following example:</span></span>

![Weergave actief beveiligde IIS-website](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="bfbed-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfbed-152">Next steps</span></span>

<span data-ttu-id="bfbed-153">In deze zelfstudie maakt beveiligd u een IIS-webserver met een SSL-certificaat dat is opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="bfbed-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="bfbed-154">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="bfbed-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bfbed-155">Maken van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bfbed-156">Genereren of een certificaat uploaden naar de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="bfbed-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="bfbed-157">Een virtuele machine maken en de IIS-webserver installeren</span><span class="sxs-lookup"><span data-stu-id="bfbed-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="bfbed-158">Het certificaat invoeren in de virtuele machine en IIS te configureren met een SSL-binding</span><span class="sxs-lookup"><span data-stu-id="bfbed-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bfbed-159">Volg deze link om te zien van de vooraf gemaakte virtuele machine scriptvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="bfbed-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfbed-160">Windows virtuele machine scriptvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="bfbed-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)