---
title: aaaEncrypt schijven op een Linux VM in Azure | Microsoft Docs
description: Hoe virtuele schijven op een Linux-VM voor het gebruik van de verbeterde beveiliging tooencrypt hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="1408b-103">Hoe tooencrypt virtuele schijven op een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="1408b-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="1408b-104">Voor de uitgebreide virtuele machine (VM) beveiliging en naleving, kunnen virtuele schijven in Azure worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="1408b-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="1408b-105">Schijven worden versleuteld met behulp van de cryptografische sleutels die worden beveiligd in een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="1408b-106">U kunt het gebruik ervan controleren en beheren van deze cryptografische sleutels.</span><span class="sxs-lookup"><span data-stu-id="1408b-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="1408b-107">Dit artikel wordt beschreven hoe virtuele schijven op een Linux-VM met tooencrypt hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="1408b-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="1408b-108">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1408b-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1408b-109">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="1408b-109">Quick commands</span></span>
<span data-ttu-id="1408b-110">Als u moet tooquickly Hallo taak, na de sectie details Hallo base Hallo opdrachten tooencrypt virtuele schijven op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1408b-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="1408b-111">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="1408b-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="1408b-112">Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1408b-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="1408b-113">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="1408b-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1408b-114">De namen van de voorbeeld-parameter *myResourceGroup*, *myKey*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1408b-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="1408b-115">Schakel eerst hello Azure Key Vault provider binnen uw Azure-abonnement met [az provider registreren](/cli/azure/provider#register) en maak een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1408b-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1408b-116">Hallo volgende voorbeeld wordt een Resourcegroepnaam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="1408b-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="1408b-117">Maken van een Azure Key Vault met [az keyvault maken](/cli/azure/keyvault#create) en Hallo Sleutelkluis voor gebruik met schijfversleuteling inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1408b-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="1408b-118">Geef een unieke naam van de Sleutelkluis voor *keyvault_name* als volgt:</span><span class="sxs-lookup"><span data-stu-id="1408b-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="1408b-119">Maken van een cryptografische sleutel in uw Sleutelkluis met [az keyvault-sleutel maken](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="1408b-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="1408b-120">Hallo volgende voorbeeld wordt een sleutel met de naam *myKey*:</span><span class="sxs-lookup"><span data-stu-id="1408b-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="1408b-121">Maken van een service-principal met Azure Active Directory met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="1408b-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="1408b-122">Hallo-service-principal ingangen Hallo verificatie en uitwisseling van de cryptografische sleutels uit Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="1408b-123">Hallo volgende voorbeeld wordt gelezen in Hallo waarden op voor de service-principal Hallo-Id en wachtwoord voor gebruik in latere opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1408b-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="1408b-124">Hallo wachtwoord wordt alleen uitgevoerd wanneer u Hallo-service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="1408b-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="1408b-125">Indien gewenst, weergeven en registreren Hallo wachtwoord (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="1408b-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="1408b-126">U kunt uw service-principals met lijst [az ad sp lijst](/cli/azure/ad/sp#list) en aanvullende informatie weergeven over een specifieke service-principal met [az ad sp weergeven](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="1408b-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="1408b-127">Machtigingen instellen voor uw Sleutelkluis met [az keyvault-beleid instellen](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="1408b-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="1408b-128">Hallo in Hallo voorbeeld te volgen, service-principal-ID wordt geleverd door de voorgaande opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="1408b-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="1408b-129">Maak een VM met [az vm maken](/cli/azure/vm#create) en koppelt u een gegevensschijf 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="1408b-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="1408b-130">Alleen bepaalde marketplace-installatiekopieën ondersteuning bieden voor schijfversleuteling.</span><span class="sxs-lookup"><span data-stu-id="1408b-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="1408b-131">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met behulp van een **CentOS 7.2n** afbeelding:</span><span class="sxs-lookup"><span data-stu-id="1408b-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="1408b-132">SSH tooyour met behulp van VM Hallo `publicIpAddress` weergegeven in de uitvoer Hallo Hallo voorafgaand aan de opdracht.</span><span class="sxs-lookup"><span data-stu-id="1408b-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="1408b-133">Maak een partitie en het bestandssysteem en Hallo gegevensschijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="1408b-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="1408b-134">Zie voor meer informatie [tooa Linux VM toomount Hallo nieuwe schijf verbinding](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="1408b-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="1408b-135">Sluit uw SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="1408b-135">Close your SSH session.</span></span>

<span data-ttu-id="1408b-136">Versleutelen van uw virtuele machine met [az vm versleuteling inschakelen](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="1408b-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="1408b-137">Hallo volgende voorbeeld wordt Hallo `$sp_id` en `$sp_password` variabelen in de voorgaande Hallo `ad sp create-for-rbac` opdracht:</span><span class="sxs-lookup"><span data-stu-id="1408b-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="1408b-138">Het duurt enige tijd Hallo schijf versleuteling proces toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1408b-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="1408b-139">Hallo-status van Hallo proces met bewaken [az vm versleuteling weergeven](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="1408b-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1408b-140">status bevat Hallo **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="1408b-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="1408b-141">Wacht totdat het Hallo-status voor Hallo OS schijf rapporten **VMRestartPending**, start u uw virtuele machine met [az vm opnieuw](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="1408b-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1408b-142">Hallo versleutelingsproces schijf voltooid tijdens het opstartproces hello, dus wacht een paar minuten voordat het controleren van de status van versleuteling opnieuw met Hallo **az vm versleuteling weergeven**:</span><span class="sxs-lookup"><span data-stu-id="1408b-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1408b-143">Hallo moet nu statusrapport zowel Hallo OS en de gegevensschijf als **versleutelde**.</span><span class="sxs-lookup"><span data-stu-id="1408b-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="1408b-144">Overzicht van schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="1408b-144">Overview of disk encryption</span></span>
<span data-ttu-id="1408b-145">Virtuele schijven op virtuele Linux-machines zijn versleuteld met behulp van rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="1408b-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="1408b-146">Er zijn geen kosten voor het versleutelen van virtuele schijven in Azure.</span><span class="sxs-lookup"><span data-stu-id="1408b-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="1408b-147">Cryptografische sleutels worden opgeslagen in Azure Key Vault met software-beveiliging, of u kunt importeren of genereren van uw tooFIPS gecertificeerde sleutels in Hardware Security Modules (HSM's) 140-2 level 2-standaarden.</span><span class="sxs-lookup"><span data-stu-id="1408b-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="1408b-148">U beheer behouden over deze cryptografische sleutels en het gebruik ervan kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="1408b-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="1408b-149">Deze cryptografische sleutels zijn gebruikte tooencrypt en ontsleutelen van virtuele schijven gekoppelde tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="1408b-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="1408b-150">Een Azure Active Directory service-principal biedt een veilige mechanisme voor het uitgeven van deze cryptografische sleutels als virtuele machines van stroom in- of uitschakelen voorzien worden.</span><span class="sxs-lookup"><span data-stu-id="1408b-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="1408b-151">Hallo-proces voor het versleutelen van een virtuele machine is als volgt:</span><span class="sxs-lookup"><span data-stu-id="1408b-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="1408b-152">Maak een cryptografische sleutel in een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="1408b-153">Configureer Hallo cryptografische sleutel toobe kan worden gebruikt voor het versleutelen van schijven.</span><span class="sxs-lookup"><span data-stu-id="1408b-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="1408b-154">tooread hello cryptografiesleutel van hello Azure Sleutelkluis, maak een Azure Active Directory-service principal met de juiste machtigingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="1408b-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="1408b-155">Uitgeven Hallo opdracht tooencrypt uw virtuele schijven, opgeven hello Azure Active Directory-service-principal en de juiste cryptografische sleutel toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1408b-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="1408b-156">Hello Azure Active Directory-principal serviceaanvragen Hallo vereist cryptografiesleutel van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="1408b-157">Hallo virtuele schijven worden versleuteld met behulp van de cryptografische sleutel Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1408b-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="1408b-158">Versleutelingsproces</span><span class="sxs-lookup"><span data-stu-id="1408b-158">Encryption process</span></span>
<span data-ttu-id="1408b-159">Schijfversleuteling is afhankelijk van Hallo extra onderdelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1408b-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="1408b-160">**Azure Sleutelkluis** -toosafeguard cryptografische sleutels en geheimen die worden gebruikt voor Hallo schijf tokenversleuteling /-ontsleuteling proces gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1408b-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="1408b-161">Als dit bestaat, kunt u een bestaande Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="1408b-162">U hoeft geen toodedicate een Sleutelkluis tooencrypting schijven.</span><span class="sxs-lookup"><span data-stu-id="1408b-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="1408b-163">tooseparate administratieve grenzen en sleutel zichtbaarheid, kunt u een speciale Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="1408b-164">**Azure Active Directory** - ingangen Hallo veilig uitwisselen van vereiste cryptografische sleutels en verificatie voor acties aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="1408b-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="1408b-165">Doorgaans kunt u een bestaand Azure Active Directory-exemplaar waarin de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1408b-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="1408b-166">Hallo service-principal biedt een mechanisme voor beveiligde toorequest en de juiste cryptografische sleutels Hallo worden uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="1408b-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="1408b-167">U ontwikkelt een werkelijke toepassing die is geïntegreerd met Azure Active Directory niet.</span><span class="sxs-lookup"><span data-stu-id="1408b-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="1408b-168">Vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="1408b-168">Requirements and limitations</span></span>
<span data-ttu-id="1408b-169">Ondersteunde scenario's en vereisten voor de schijfversleuteling:</span><span class="sxs-lookup"><span data-stu-id="1408b-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="1408b-170">Hallo Linux server SKU's - Ubuntu, CentOS, SUSE en SUSE Linux Enterprise Server (SLES) en Red Hat Enterprise Linux te volgen.</span><span class="sxs-lookup"><span data-stu-id="1408b-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="1408b-171">Alle resources (zoals Sleutelkluis, een opslagaccount en een VM) moet in Hallo dezelfde Azure-regio en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="1408b-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="1408b-172">Standard A, D, DS, G en GS-serie biedt virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1408b-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="1408b-173">Schijfversleuteling is momenteel niet ondersteund in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="1408b-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="1408b-174">Basisstaffel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1408b-174">Basic tier VMs.</span></span>
* <span data-ttu-id="1408b-175">Virtuele machines gemaakt met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1408b-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="1408b-176">OS-schijfversleuteling op Linux VM's uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="1408b-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="1408b-177">Hallo cryptografische sleutels op een al is versleuteld Linux-VM wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1408b-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="1408b-178">Azure Sleutelkluis en de sleutels maken</span><span class="sxs-lookup"><span data-stu-id="1408b-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="1408b-179">Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1408b-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="1408b-180">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="1408b-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1408b-181">De namen van de voorbeeld-parameter *myResourceGroup*, *myKey*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1408b-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="1408b-182">de eerste stap Hallo toocreate een toostore Azure Sleutelkluis is de cryptografiesleutels.</span><span class="sxs-lookup"><span data-stu-id="1408b-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="1408b-183">Azure Sleutelkluis sleutels en geheimen, kunnen opslaan of wachtwoorden die u toelaten om toosecurely ze implementeert in uw toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="1408b-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="1408b-184">Voor versleuteling van de virtuele schijf, Sleutelkluis toostore een cryptografische sleutel die is gebruikt tooencrypt gebruiken of ontsleutelen van de virtuele schijven.</span><span class="sxs-lookup"><span data-stu-id="1408b-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="1408b-185">Hello Azure Key Vault provider binnen uw Azure-abonnement met ingeschakeld [az provider registreren](/cli/azure/provider#register) en maak een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1408b-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1408b-186">Hallo volgende voorbeeld wordt een Resourcegroepnaam *myResourceGroup* in Hallo `eastus` locatie:</span><span class="sxs-lookup"><span data-stu-id="1408b-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="1408b-187">Hello Azure Key Vault met Hallo cryptografische sleutels en het bijbehorende compute resources, zoals opslag en virtuele machine zelf Hallo moeten zich bevinden in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="1408b-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="1408b-188">Maken van een Azure Key Vault met [az keyvault maken](/cli/azure/keyvault#create) en Hallo Sleutelkluis voor gebruik met schijfversleuteling inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1408b-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="1408b-189">Geef een unieke naam van de Sleutelkluis voor *keyvault_name* als volgt:</span><span class="sxs-lookup"><span data-stu-id="1408b-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="1408b-190">U kunt met behulp van software of Hardware Security Model (HSM) protection cryptografiesleutels opslaan.</span><span class="sxs-lookup"><span data-stu-id="1408b-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="1408b-191">Een HSM, moet een premium Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="1408b-192">Er is een extra kosten toocreating premium Sleutelkluis in plaats van standaard Sleutelkluis waarmee softwarematige beveiligde sleutels worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1408b-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="1408b-193">toevoegen van een premium Sleutelkluis, in de voorgaande stap Hallo toocreate `--sku Premium` toohello opdracht.</span><span class="sxs-lookup"><span data-stu-id="1408b-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="1408b-194">Hallo volgende voorbeeld wordt softwarematige beveiligde sleutels omdat er een standaard Sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1408b-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="1408b-195">Voor beide beveiligingsmodellen moet hello Azure-platform toobe toorequest-Hallo cryptografiesleutels toegang verleend als Hallo VM wordt opgestart toodecrypt Hallo virtuele schijven.</span><span class="sxs-lookup"><span data-stu-id="1408b-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="1408b-196">Maken van een cryptografische sleutel in uw Sleutelkluis met [az keyvault-sleutel maken](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="1408b-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="1408b-197">Hallo volgende voorbeeld wordt een sleutel met de naam *myKey*:</span><span class="sxs-lookup"><span data-stu-id="1408b-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="1408b-198">Hello Azure Active Directory-service-principal maken</span><span class="sxs-lookup"><span data-stu-id="1408b-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="1408b-199">Wanneer virtuele schijven worden versleuteld en ontsleuteld, geeft u een account toohandle Hallo-authenticatie en uitwisselen van cryptografische sleutels uit Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="1408b-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="1408b-200">Dit account, een Azure Active Directory service-principal kunt hello Azure-platform toorequest Hallo juiste cryptografische sleutels namens Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1408b-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="1408b-201">Een standaardexemplaar van de Azure Active Directory is beschikbaar in uw abonnement, hoewel veel organisaties hebben speciale mappen van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1408b-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="1408b-202">Maken van een service-principal met Azure Active Directory met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="1408b-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="1408b-203">Hallo volgende voorbeeld wordt gelezen in Hallo waarden op voor de service-principal Hallo-Id en wachtwoord voor gebruik in latere opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1408b-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="1408b-204">Hallo-wachtwoord wordt alleen weergegeven wanneer u Hallo service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="1408b-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="1408b-205">Indien gewenst, weergeven en registreren Hallo wachtwoord (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="1408b-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="1408b-206">U kunt uw service-principals met lijst [az ad sp lijst](/cli/azure/ad/sp#list) en aanvullende informatie weergeven over een specifieke service-principal met [az ad sp weergeven](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="1408b-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="1408b-207">toosuccessfully versleutelen of ontsleutelen van virtuele schijven, machtigingen op Hallo cryptografische sleutel die wordt opgeslagen in de Sleutelkluis moet set toopermit hello Azure Active Directory service principal tooread Hallo sleutels.</span><span class="sxs-lookup"><span data-stu-id="1408b-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="1408b-208">Machtigingen instellen voor uw Sleutelkluis met [az keyvault-beleid instellen](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="1408b-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="1408b-209">Hallo in Hallo voorbeeld te volgen, service-principal-ID wordt geleverd door de voorgaande opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="1408b-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="1408b-210">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="1408b-210">Create virtual machine</span></span>
<span data-ttu-id="1408b-211">tooactually bepaalde virtuele schijven te versleutelen, kunt een virtuele machine maken en een gegevensschijf toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1408b-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="1408b-212">Maak een VM-tooencrypt met [az vm maken](/cli/azure/vm#create) en koppelt u een gegevensschijf 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="1408b-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="1408b-213">Alleen bepaalde marketplace-installatiekopieën ondersteuning bieden voor schijfversleuteling.</span><span class="sxs-lookup"><span data-stu-id="1408b-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="1408b-214">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* met behulp van een **CentOS 7.2n** afbeelding:</span><span class="sxs-lookup"><span data-stu-id="1408b-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="1408b-215">SSH tooyour met behulp van VM Hallo `publicIpAddress` weergegeven in de uitvoer Hallo Hallo voorafgaand aan de opdracht.</span><span class="sxs-lookup"><span data-stu-id="1408b-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="1408b-216">Maak een partitie en het bestandssysteem en Hallo gegevensschijf koppelen.</span><span class="sxs-lookup"><span data-stu-id="1408b-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="1408b-217">Zie voor meer informatie [tooa Linux VM toomount Hallo nieuwe schijf verbinding](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="1408b-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="1408b-218">Sluit uw SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="1408b-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="1408b-219">Virtuele machine versleutelen</span><span class="sxs-lookup"><span data-stu-id="1408b-219">Encrypt virtual machine</span></span>
<span data-ttu-id="1408b-220">tooencrypt hello virtuele schijven, u samenbrengen alle vorige Hallo-onderdelen:</span><span class="sxs-lookup"><span data-stu-id="1408b-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="1408b-221">Hello Azure Active Directory service-principal en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="1408b-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="1408b-222">Hallo Sleutelkluis toostore Hallo metagegevens voor uw versleutelde schijven opgeven.</span><span class="sxs-lookup"><span data-stu-id="1408b-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="1408b-223">Hallo cryptografische sleutels toouse voor Hallo daadwerkelijke versleuteling en ontsleuteling opgeven.</span><span class="sxs-lookup"><span data-stu-id="1408b-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="1408b-224">Geef op of u tooencrypt Hallo OS schijf, Hallo gegevensschijven of alle wilt.</span><span class="sxs-lookup"><span data-stu-id="1408b-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="1408b-225">Versleutelen van uw virtuele machine met [az vm versleuteling inschakelen](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="1408b-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="1408b-226">Hallo volgende voorbeeld wordt Hallo `$sp_id` en `$sp_password` variabelen in de voorgaande Hallo `ad sp create-for-rbac` opdracht:</span><span class="sxs-lookup"><span data-stu-id="1408b-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="1408b-227">Het duurt enige tijd Hallo schijf versleuteling proces toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1408b-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="1408b-228">Hallo-status van Hallo proces met bewaken [az vm versleuteling weergeven](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="1408b-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1408b-229">Hallo uitvoer is vergelijkbaar toohello volgende ingekorte voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1408b-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="1408b-230">Wacht totdat het Hallo-status voor Hallo OS schijf rapporten **VMRestartPending**, start u uw virtuele machine met [az vm opnieuw](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="1408b-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1408b-231">Hallo versleutelingsproces schijf voltooid tijdens het opstartproces hello, dus wacht een paar minuten voordat het controleren van de status van versleuteling opnieuw met Hallo **az vm versleuteling weergeven**:</span><span class="sxs-lookup"><span data-stu-id="1408b-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1408b-232">Hallo moet nu statusrapport zowel Hallo OS en de gegevensschijf als **versleutelde**.</span><span class="sxs-lookup"><span data-stu-id="1408b-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="1408b-233">Toevoegen van extra gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="1408b-233">Add additional data disks</span></span>
<span data-ttu-id="1408b-234">Nadat u uw gegevensschijven hebt versleuteld, kunt u later toevoegen als u meer virtuele schijven tooyour VM en ook versleutelen.</span><span class="sxs-lookup"><span data-stu-id="1408b-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="1408b-235">U kunt bijvoorbeeld een tweede virtuele schijf tooyour VM als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1408b-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="1408b-236">Voer Hallo opdracht tooencrypt Hallo virtuele schijven als volgt:</span><span class="sxs-lookup"><span data-stu-id="1408b-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="1408b-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1408b-237">Next steps</span></span>
* <span data-ttu-id="1408b-238">Zie voor meer informatie over het beheren van Azure Sleutelkluis, met inbegrip van verwijderen van de cryptografische sleutels en kluizen, [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="1408b-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="1408b-239">Zie voor meer informatie over schijfversleuteling, zoals het voorbereiden van een versleutelde aangepaste VM tooupload tooAzure, [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="1408b-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
