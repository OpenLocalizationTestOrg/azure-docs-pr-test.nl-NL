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
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="2f200-103">Hoe tooencrypt virtuele schijven op een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="2f200-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="2f200-104">Voor de uitgebreide virtuele machine (VM) beveiliging en naleving, kunnen virtuele schijven in Azure worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="2f200-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="2f200-105">Schijven worden versleuteld met behulp van de cryptografische sleutels die worden beveiligd in een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="2f200-106">U kunt het gebruik ervan controleren en beheren van deze cryptografische sleutels.</span><span class="sxs-lookup"><span data-stu-id="2f200-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="2f200-107">Dit artikel details hoe tooencrypt virtuele schijven op een Windows-VM met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f200-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="2f200-108">U kunt ook [versleutelen van een Linux-VM met hello Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="2f200-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="2f200-109">Overzicht van schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="2f200-109">Overview of disk encryption</span></span>
<span data-ttu-id="2f200-110">Virtuele schijven op Windows-VM's zijn versleuteld in rust met Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="2f200-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="2f200-111">Er zijn geen kosten voor het versleutelen van virtuele schijven in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f200-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="2f200-112">Cryptografische sleutels worden opgeslagen in Azure Key Vault met software-beveiliging, of u kunt importeren of genereren van uw tooFIPS gecertificeerde sleutels in Hardware Security Modules (HSM's) 140-2 level 2-standaarden.</span><span class="sxs-lookup"><span data-stu-id="2f200-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="2f200-113">Deze cryptografische sleutels zijn gebruikte tooencrypt en ontsleutelen van virtuele schijven gekoppelde tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="2f200-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="2f200-114">U beheer behouden over deze cryptografische sleutels en het gebruik ervan kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="2f200-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="2f200-115">Een Azure Active Directory service-principal biedt een veilige mechanisme voor het uitgeven van deze cryptografische sleutels als virtuele machines van stroom in- of uitschakelen voorzien worden.</span><span class="sxs-lookup"><span data-stu-id="2f200-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="2f200-116">Hallo-proces voor het versleutelen van een virtuele machine is als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f200-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="2f200-117">Maak een cryptografische sleutel in een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="2f200-118">Configureer Hallo cryptografische sleutel toobe kan worden gebruikt voor het versleutelen van schijven.</span><span class="sxs-lookup"><span data-stu-id="2f200-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="2f200-119">tooread hello cryptografiesleutel van hello Azure Sleutelkluis, maak een Azure Active Directory-service principal met de juiste machtigingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f200-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="2f200-120">Uitgeven Hallo opdracht tooencrypt uw virtuele schijven, opgeven hello Azure Active Directory-service-principal en de juiste cryptografische sleutel toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2f200-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="2f200-121">Hello Azure Active Directory-principal serviceaanvragen Hallo vereist cryptografiesleutel van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="2f200-122">Hallo virtuele schijven worden versleuteld met behulp van de cryptografische sleutel Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2f200-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="2f200-123">Versleutelingsproces</span><span class="sxs-lookup"><span data-stu-id="2f200-123">Encryption process</span></span>
<span data-ttu-id="2f200-124">Schijfversleuteling is afhankelijk van Hallo extra onderdelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f200-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="2f200-125">**Azure Sleutelkluis** -toosafeguard cryptografische sleutels en geheimen die worden gebruikt voor Hallo schijf tokenversleuteling /-ontsleuteling proces gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2f200-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="2f200-126">Als dit bestaat, kunt u een bestaande Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="2f200-127">U hoeft geen toodedicate een Sleutelkluis tooencrypting schijven.</span><span class="sxs-lookup"><span data-stu-id="2f200-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="2f200-128">tooseparate administratieve grenzen en sleutel zichtbaarheid, kunt u een speciale Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="2f200-129">**Azure Active Directory** - ingangen Hallo veilig uitwisselen van vereiste cryptografische sleutels en verificatie voor acties aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="2f200-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="2f200-130">Doorgaans kunt u een bestaand Azure Active Directory-exemplaar waarin de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2f200-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="2f200-131">Hallo service-principal biedt een mechanisme voor beveiligde toorequest en de juiste cryptografische sleutels Hallo worden uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="2f200-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="2f200-132">U ontwikkelt een werkelijke toepassing die is geïntegreerd met Azure Active Directory niet.</span><span class="sxs-lookup"><span data-stu-id="2f200-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="2f200-133">Vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="2f200-133">Requirements and limitations</span></span>
<span data-ttu-id="2f200-134">Ondersteunde scenario's en vereisten voor de schijfversleuteling:</span><span class="sxs-lookup"><span data-stu-id="2f200-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="2f200-135">Inschakelen van versleuteling op nieuwe Windows VM's van Azure Marketplace-installatiekopieën of aangepaste VHD-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="2f200-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="2f200-136">Inschakelen van versleuteling op bestaande Windows virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f200-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="2f200-137">Inschakelen van versleuteling op Windows-virtuele machines die zijn geconfigureerd met behulp van opslagruimten.</span><span class="sxs-lookup"><span data-stu-id="2f200-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="2f200-138">Het uitschakelen van versleuteling op besturingssysteem en stations voor VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="2f200-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="2f200-139">Alle resources (zoals Sleutelkluis, een opslagaccount en een VM) moet in Hallo dezelfde Azure-regio en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f200-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="2f200-140">Standard-laag VM's, zoals een, D, DS, G en GS-serie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2f200-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="2f200-141">Schijfversleuteling is momenteel niet ondersteund in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="2f200-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="2f200-142">Basisstaffel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2f200-142">Basic tier VMs.</span></span>
* <span data-ttu-id="2f200-143">Virtuele machines gemaakt met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2f200-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="2f200-144">Hallo cryptografische sleutels op een al is versleuteld virtuele machine wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="2f200-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="2f200-145">Integratie met on-premises-Service voor sleutelbeheer.</span><span class="sxs-lookup"><span data-stu-id="2f200-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="2f200-146">Azure Sleutelkluis en de sleutels maken</span><span class="sxs-lookup"><span data-stu-id="2f200-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="2f200-147">Voordat u begint, Controleer of de nieuwste versie van die Hallo van hello Azure PowerShell-module is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2f200-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="2f200-148">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f200-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2f200-149">In de gehele opdrachtvoorbeelden hello, vervangen door alle voorbeeldparameters uw eigen namen, locatie en sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="2f200-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="2f200-150">Hallo volgende voorbeelden wordt gebruikt een conventie *myResourceGroup*, *myKeyVault*, *myVM*, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="2f200-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="2f200-151">de eerste stap Hallo toocreate een toostore Azure Sleutelkluis is de cryptografiesleutels.</span><span class="sxs-lookup"><span data-stu-id="2f200-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="2f200-152">Azure Sleutelkluis sleutels en geheimen, kunnen opslaan of wachtwoorden die u toelaten om toosecurely ze implementeert in uw toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="2f200-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="2f200-153">Voor versleuteling van de virtuele schijf, een Sleutelkluis toostore een cryptografische sleutel die is gebruikt tooencrypt maken of ontsleutelen van de virtuele schijven.</span><span class="sxs-lookup"><span data-stu-id="2f200-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="2f200-154">Hello Azure Key Vault provider binnen uw Azure-abonnement met ingeschakeld [registreren AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), maakt u een resourcegroep met [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="2f200-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="2f200-155">Hallo volgende voorbeeld wordt een Resourcegroepnaam *myResourceGroup* in Hallo *VS-Oost* locatie:</span><span class="sxs-lookup"><span data-stu-id="2f200-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="2f200-156">Hello Azure Key Vault met Hallo cryptografische sleutels en het bijbehorende compute resources, zoals opslag en virtuele machine zelf Hallo moeten zich bevinden in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="2f200-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="2f200-157">Maken van een Azure Key Vault met [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) en Hallo Sleutelkluis voor gebruik met schijfversleuteling inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2f200-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="2f200-158">Geef een unieke naam van de Sleutelkluis voor *keyVaultName* als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f200-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="2f200-159">U kunt met behulp van software of Hardware Security Model (HSM) protection cryptografiesleutels opslaan.</span><span class="sxs-lookup"><span data-stu-id="2f200-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="2f200-160">Een HSM, moet een premium Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="2f200-161">Er is een extra kosten toocreating premium Sleutelkluis in plaats van standaard Sleutelkluis waarmee softwarematige beveiligde sleutels worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2f200-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="2f200-162">een premium Sleutelkluis, in de voorgaande stap Hallo toocreate toevoegen Hallo *- Sku 'Premium'* parameters.</span><span class="sxs-lookup"><span data-stu-id="2f200-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="2f200-163">Hallo volgende voorbeeld wordt softwarematige beveiligde sleutels omdat er een standaard Sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f200-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="2f200-164">Voor beide beveiligingsmodellen moet hello Azure-platform toobe toorequest-Hallo cryptografiesleutels toegang verleend als Hallo VM wordt opgestart toodecrypt Hallo virtuele schijven.</span><span class="sxs-lookup"><span data-stu-id="2f200-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="2f200-165">Maken van een cryptografische sleutel in uw Sleutelkluis met [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="2f200-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="2f200-166">Hallo volgende voorbeeld wordt een sleutel met de naam *myKey*:</span><span class="sxs-lookup"><span data-stu-id="2f200-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="2f200-167">Hello Azure Active Directory-service-principal maken</span><span class="sxs-lookup"><span data-stu-id="2f200-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="2f200-168">Wanneer virtuele schijven worden versleuteld en ontsleuteld, geeft u een account toohandle Hallo-authenticatie en uitwisselen van cryptografische sleutels uit Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f200-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="2f200-169">Dit account, een Azure Active Directory service-principal kunt hello Azure-platform toorequest Hallo juiste cryptografische sleutels namens Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="2f200-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="2f200-170">Een standaardexemplaar van de Azure Active Directory is beschikbaar in uw abonnement, hoewel veel organisaties hebben speciale mappen van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2f200-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="2f200-171">Een service-principal maken in Azure Active Directory met [nieuw AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="2f200-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="2f200-172">een beveiligd wachtwoord toospecify Volg Hallo [wachtwoordbeleid en -beperkingen in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="2f200-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="2f200-173">toosuccessfully versleutelen of ontsleutelen van virtuele schijven, machtigingen op Hallo cryptografische sleutel die wordt opgeslagen in de Sleutelkluis moet set toopermit hello Azure Active Directory service principal tooread Hallo sleutels.</span><span class="sxs-lookup"><span data-stu-id="2f200-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="2f200-174">Machtigingen instellen voor uw Sleutelkluis met [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="2f200-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="2f200-175">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2f200-175">Create virtual machine</span></span>
<span data-ttu-id="2f200-176">tootest Hallo versleutelingsproces, gaan we een virtuele machine te maken.</span><span class="sxs-lookup"><span data-stu-id="2f200-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="2f200-177">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* met behulp van een *Windows Server 2016 Datacenter* afbeelding:</span><span class="sxs-lookup"><span data-stu-id="2f200-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="2f200-178">Virtuele machine versleutelen</span><span class="sxs-lookup"><span data-stu-id="2f200-178">Encrypt virtual machine</span></span>
<span data-ttu-id="2f200-179">tooencrypt hello virtuele schijven, u samenbrengen alle vorige Hallo-onderdelen:</span><span class="sxs-lookup"><span data-stu-id="2f200-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="2f200-180">Hello Azure Active Directory service-principal en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="2f200-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="2f200-181">Hallo Sleutelkluis toostore Hallo metagegevens voor uw versleutelde schijven opgeven.</span><span class="sxs-lookup"><span data-stu-id="2f200-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="2f200-182">Hallo cryptografische sleutels toouse voor Hallo daadwerkelijke versleuteling en ontsleuteling opgeven.</span><span class="sxs-lookup"><span data-stu-id="2f200-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="2f200-183">Geef op of u tooencrypt Hallo OS schijf, Hallo gegevensschijven of alle wilt.</span><span class="sxs-lookup"><span data-stu-id="2f200-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="2f200-184">Versleutelen van uw virtuele machine met [Set AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) hello Azure Key Vault sleutel en Azure Active Directory-service-principal referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f200-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="2f200-185">Hallo volgende voorbeeld haalt alle Hallo belangrijke informatie en vervolgens versleutelt Hallo VM met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2f200-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

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

<span data-ttu-id="2f200-186">Hallo vragen toocontinue met Hallo VM versleuteling accepteren.</span><span class="sxs-lookup"><span data-stu-id="2f200-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="2f200-187">Hallo VM wordt opnieuw gestart tijdens het Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="2f200-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="2f200-188">Zodra het Hallo-codering is voltooid en hello VM opnieuw is opgestart, lezen Hallo coderingsstatus met [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="2f200-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="2f200-189">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f200-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="2f200-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f200-190">Next steps</span></span>
* <span data-ttu-id="2f200-191">Zie voor meer informatie over het beheren van Azure Sleutelkluis [Sleutelkluis instellen voor virtuele machines](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="2f200-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="2f200-192">Zie voor meer informatie over schijfversleuteling, zoals het voorbereiden van een versleutelde aangepaste VM tooupload tooAzure, [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="2f200-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
