---
title: aaaEncrypt schijven op een Linux-VM met hello Azure CLI 1.0 | Microsoft Docs
description: Hoe tooencrypt schijven op een Linux-VM met hello Azure CLI 1.0 en Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="64d12-103">Versleutelen van schijven op een Linux-VM met hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="64d12-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="64d12-104">Voor de uitgebreide virtuele machine (VM) beveiliging en naleving, kunnen virtuele schijven in Azure worden versleuteld in rust.</span><span class="sxs-lookup"><span data-stu-id="64d12-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="64d12-105">Schijven worden versleuteld met behulp van de cryptografische sleutels die worden beveiligd in een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="64d12-106">U kunt het gebruik ervan controleren en beheren van deze cryptografische sleutels.</span><span class="sxs-lookup"><span data-stu-id="64d12-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="64d12-107">Dit artikel wordt beschreven hoe virtuele schijven op een Linux-VM met tooencrypt hello Azure CLI 1.0 en Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="64d12-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="64d12-108">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="64d12-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="64d12-109">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="64d12-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="64d12-110">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="64d12-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="64d12-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="64d12-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="64d12-112">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="64d12-112">Quick commands</span></span>
<span data-ttu-id="64d12-113">Als u moet tooquickly Hallo taak, na de sectie details Hallo base Hallo opdrachten tooencrypt virtuele schijven op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="64d12-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="64d12-114">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="64d12-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="64d12-115">U moet Hallo [nieuwste Azure CLI 1.0](../../xplat-cli-install.md) geïnstalleerd en geregistreerd in het Hallo-Resource Manager-modus als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="64d12-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="64d12-116">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="64d12-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="64d12-117">De namen van de voorbeeld-parameter `myResourceGroup`, `myKeyVault`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="64d12-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="64d12-118">Eerst hello Azure Key Vault provider binnen uw Azure-abonnement ingeschakeld en een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="64d12-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="64d12-119">Hallo volgende voorbeeld wordt een Resourcegroepnaam `myResourceGroup` in Hallo `WestUS` locatie:</span><span class="sxs-lookup"><span data-stu-id="64d12-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="64d12-120">Maak een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="64d12-121">Hallo volgende voorbeeld wordt een Sleutelkluis met de naam `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="64d12-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="64d12-122">Een cryptografische sleutel in uw Sleutelkluis maken en inschakelen voor schijfversleuteling.</span><span class="sxs-lookup"><span data-stu-id="64d12-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="64d12-123">Hallo volgende voorbeeld wordt een sleutel met de naam `myKey`:</span><span class="sxs-lookup"><span data-stu-id="64d12-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="64d12-124">Maak een eindpunt met Azure Active Directory voor het verwerken van Hallo verificatie en uitwisselen van cryptografische sleutels uit Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="64d12-125">Hallo `--home-page` en `--identifier-uris` hoeft geen toobe Werkelijke routeerbare adresruimte.</span><span class="sxs-lookup"><span data-stu-id="64d12-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="64d12-126">Voor Hallo hoogste niveau van beveiliging, worden clientgeheimen gebruikt in plaats van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="64d12-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="64d12-127">Hello Azure CLI kan momenteel niet clientgeheimen genereren.</span><span class="sxs-lookup"><span data-stu-id="64d12-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="64d12-128">Clientgeheimen kunnen alleen worden gegenereerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="64d12-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="64d12-129">Hallo volgende voorbeeld wordt een Azure Active Directory-eindpunt met de naam `myAADApp` en maakt gebruik van een wachtwoord van `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="64d12-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="64d12-130">Geef uw eigen wachtwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="64d12-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="64d12-131">Opmerking Hallo `applicationId` in Hallo-uitvoer van de voorgaande opdracht hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64d12-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="64d12-132">Deze toepassing-ID wordt gebruikt in Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64d12-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="64d12-133">Een data schijf tooan bestaande virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="64d12-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="64d12-134">Hallo volgende voorbeeld wordt een schijf tooa van gegevens met de naam VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="64d12-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="64d12-135">Controleer de details Hallo voor uw Sleutelkluis en Hallo sleutel die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64d12-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="64d12-136">U moet de kluis-ID sleutel, URI en sleutel Hallo URL in de laatste stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="64d12-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="64d12-137">Hallo volgende voorbeeld bekijkt hello details voor een Sleutelkluis met de naam `myKeyVault` en de sleutel met de naam `myKey`:</span><span class="sxs-lookup"><span data-stu-id="64d12-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="64d12-138">Versleutelen van uw schijven als volgt invoeren van uw eigen namen van parameters in:</span><span class="sxs-lookup"><span data-stu-id="64d12-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="64d12-139">Hello Azure CLI biedt geen uitgebreide fouten tijdens het versleutelingsproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="64d12-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="64d12-140">Raadpleeg voor aanvullende informatie voor probleemoplossing `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="64d12-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="64d12-141">Als Hallo veel variabelen voorafgaand aan de opdracht heeft en u krijgt niet veel opgave toowhy Hallo mislukt, een voorbeeld van de volledige opdracht is als volgt:</span><span class="sxs-lookup"><span data-stu-id="64d12-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="64d12-142">Controleer ten slotte coderingsstatus Hallo opnieuw tooconfirm dat uw virtuele schijven nu zijn gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="64d12-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="64d12-143">Hallo volgende voorbeeld controleert Hallo status van een virtuele machine met de naam `myVM` in Hallo `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="64d12-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="64d12-144">Overzicht van schijfversleuteling</span><span class="sxs-lookup"><span data-stu-id="64d12-144">Overview of disk encryption</span></span>
<span data-ttu-id="64d12-145">Virtuele schijven op virtuele Linux-machines zijn versleuteld met behulp van rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="64d12-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="64d12-146">Er zijn geen kosten voor het versleutelen van virtuele schijven in Azure.</span><span class="sxs-lookup"><span data-stu-id="64d12-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="64d12-147">Cryptografische sleutels worden opgeslagen in Azure Key Vault met software-beveiliging, of u kunt importeren of genereren van uw tooFIPS gecertificeerde sleutels in Hardware Security Modules (HSM's) 140-2 level 2-standaarden.</span><span class="sxs-lookup"><span data-stu-id="64d12-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="64d12-148">U beheer behouden over deze cryptografische sleutels en het gebruik ervan kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="64d12-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="64d12-149">Deze cryptografische sleutels zijn gebruikte tooencrypt en ontsleutelen van virtuele schijven gekoppelde tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="64d12-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="64d12-150">Een Azure Active Directory-eindpunt biedt een veilige mechanisme voor het uitgeven van deze cryptografische sleutels als virtuele machines van stroom in- of uitschakelen voorzien worden.</span><span class="sxs-lookup"><span data-stu-id="64d12-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="64d12-151">Hallo-proces voor het versleutelen van een virtuele machine is als volgt:</span><span class="sxs-lookup"><span data-stu-id="64d12-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="64d12-152">Maak een cryptografische sleutel in een Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="64d12-153">Configureer Hallo cryptografische sleutel toobe kan worden gebruikt voor het versleutelen van schijven.</span><span class="sxs-lookup"><span data-stu-id="64d12-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="64d12-154">een eindpunt met Azure Active Directory met de juiste machtigingen Hallo tooread Hallo cryptografiesleutel van hello Azure Key Vault maken</span><span class="sxs-lookup"><span data-stu-id="64d12-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="64d12-155">Uitgeven Hallo opdracht tooencrypt uw virtuele schijven, geven hello Azure Active Directory-eindpunt en de juiste cryptografische sleutel toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="64d12-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="64d12-156">Hello Azure Active Directory-eindpunt vereist cryptografische sleutel Hallo-aanvragen van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="64d12-157">Hallo virtuele schijven worden versleuteld met behulp van de cryptografische sleutel Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="64d12-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="64d12-158">Ondersteuning van services en versleuteling</span><span class="sxs-lookup"><span data-stu-id="64d12-158">Supporting services and encryption process</span></span>
<span data-ttu-id="64d12-159">Schijfversleuteling is afhankelijk van Hallo extra onderdelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64d12-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="64d12-160">**Azure Sleutelkluis** -toosafeguard cryptografische sleutels en geheimen die worden gebruikt voor Hallo schijf tokenversleuteling /-ontsleuteling proces gebruikt.</span><span class="sxs-lookup"><span data-stu-id="64d12-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="64d12-161">Als dit bestaat, kunt u een bestaande Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="64d12-162">U hoeft geen toodedicate een Sleutelkluis tooencrypting schijven.</span><span class="sxs-lookup"><span data-stu-id="64d12-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="64d12-163">tooseparate administratieve grenzen en sleutel zichtbaarheid, kunt u een speciale Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="64d12-164">**Azure Active Directory** - ingangen Hallo veilig uitwisselen van vereiste cryptografische sleutels en verificatie voor acties aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="64d12-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="64d12-165">Doorgaans kunt u een bestaand Azure Active Directory-exemplaar waarin de toepassing.</span><span class="sxs-lookup"><span data-stu-id="64d12-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="64d12-166">Hallo toepassing is van een eindpunt voor Hallo Sleutelkluis en de virtuele Machine services toorequest en ophalen van de juiste cryptografische sleutels Hallo uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="64d12-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="64d12-167">U ontwikkelt een werkelijke toepassing die is geïntegreerd met Azure Active Directory niet.</span><span class="sxs-lookup"><span data-stu-id="64d12-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="64d12-168">Vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="64d12-168">Requirements and limitations</span></span>
<span data-ttu-id="64d12-169">Ondersteunde scenario's en vereisten voor de schijfversleuteling:</span><span class="sxs-lookup"><span data-stu-id="64d12-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="64d12-170">Hallo Linux server SKU's - Ubuntu, CentOS, SUSE en SUSE Linux Enterprise Server (SLES) en Red Hat Enterprise Linux te volgen.</span><span class="sxs-lookup"><span data-stu-id="64d12-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="64d12-171">Alle resources (zoals Sleutelkluis, een opslagaccount en een VM) moet in Hallo dezelfde Azure-regio en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="64d12-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="64d12-172">Standard A, D, DS, G en GS-serie biedt virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="64d12-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="64d12-173">Schijfversleuteling is momenteel niet ondersteund in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="64d12-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="64d12-174">Basisstaffel virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="64d12-174">Basic tier VMs.</span></span>
* <span data-ttu-id="64d12-175">Virtuele machines gemaakt met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="64d12-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="64d12-176">OS-schijfversleuteling op Linux VM's uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="64d12-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="64d12-177">Hallo cryptografische sleutels op een al is versleuteld Linux-VM wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="64d12-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="64d12-178">Maak hello Azure Sleutelkluis en de sleutels</span><span class="sxs-lookup"><span data-stu-id="64d12-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="64d12-179">toocomplete hello rest van deze handleiding, moet u Hallo [nieuwste Azure CLI 1.0](../../xplat-cli-install.md) geïnstalleerd en geregistreerd in het Hallo-Resource Manager-modus als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="64d12-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="64d12-180">In de gehele opdrachtvoorbeelden hello, vervangen door alle voorbeeldparameters uw eigen namen, locatie en sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="64d12-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="64d12-181">Hallo volgende voorbeelden wordt gebruikt een conventie `myResourceGroup`, `myKeyVault`, `myAADApp`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="64d12-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="64d12-182">de eerste stap Hallo toocreate een toostore Azure Sleutelkluis is de cryptografiesleutels.</span><span class="sxs-lookup"><span data-stu-id="64d12-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="64d12-183">Azure Sleutelkluis sleutels en geheimen, kunnen opslaan of wachtwoorden die u toelaten om toosecurely ze implementeert in uw toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="64d12-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="64d12-184">Voor versleuteling van de virtuele schijf, Sleutelkluis toostore een cryptografische sleutel die is gebruikt tooencrypt gebruiken of ontsleutelen van de virtuele schijven.</span><span class="sxs-lookup"><span data-stu-id="64d12-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="64d12-185">Hello Azure Sleutelkluis-provider in uw Azure-abonnement inschakelen en vervolgens een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="64d12-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="64d12-186">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUS` locatie:</span><span class="sxs-lookup"><span data-stu-id="64d12-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="64d12-187">Hello Azure Key Vault met Hallo cryptografische sleutels en het bijbehorende compute resources, zoals opslag en virtuele machine zelf Hallo moeten zich bevinden in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="64d12-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="64d12-188">Hallo volgende voorbeeld wordt een Azure Sleutelkluis met de naam `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="64d12-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="64d12-189">U kunt met behulp van software of Hardware Security Model (HSM) protection cryptografiesleutels opslaan.</span><span class="sxs-lookup"><span data-stu-id="64d12-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="64d12-190">Een HSM, moet een premium Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="64d12-191">Er is een extra kosten toocreating premium Sleutelkluis in plaats van standaard Sleutelkluis waarmee softwarematige beveiligde sleutels worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="64d12-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="64d12-192">toevoegen van een premium Sleutelkluis, in de voorgaande stap Hallo toocreate `--sku Premium` toohello opdracht.</span><span class="sxs-lookup"><span data-stu-id="64d12-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="64d12-193">Hallo volgende voorbeeld wordt softwarematige beveiligde sleutels omdat er een standaard Sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64d12-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="64d12-194">Voor beide beveiligingsmodellen moet hello Azure-platform toobe toorequest-Hallo cryptografiesleutels toegang verleend als Hallo VM wordt opgestart toodecrypt Hallo virtuele schijven.</span><span class="sxs-lookup"><span data-stu-id="64d12-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="64d12-195">Een coderingssleutel binnen uw Sleutelkluis maken en inschakelen voor gebruik met versleuteling van de virtuele schijf.</span><span class="sxs-lookup"><span data-stu-id="64d12-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="64d12-196">Hallo volgende voorbeeld wordt een sleutel met de naam `myKey` en schakelt u deze voor de schijfversleuteling:</span><span class="sxs-lookup"><span data-stu-id="64d12-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="64d12-197">Hello Azure Active Directory-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="64d12-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="64d12-198">Wanneer virtuele schijven worden versleuteld en ontsleuteld, gebruikt u een eindpunt toohandle Hallo-authenticatie en uitwisselen van cryptografische sleutels uit Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="64d12-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="64d12-199">Dit eindpunt, een Azure Active Directory-toepassing kunt hello Azure-platform toorequest Hallo juiste cryptografische sleutels namens Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="64d12-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="64d12-200">Een standaardexemplaar van de Azure Active Directory is beschikbaar in uw abonnement, hoewel veel organisaties hebben speciale mappen van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64d12-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="64d12-201">Als u niet een volledige Azure Active Directory-toepassing maakt, Hallo `--home-page` en `--identifier-uris` parameters in het volgende voorbeeld Hallo hoeft geen toobe Werkelijke routeerbare adresruimte.</span><span class="sxs-lookup"><span data-stu-id="64d12-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="64d12-202">Hallo bepaalt volgende voorbeeld ook een geheim op basis van wachtwoorden in plaats van genereren van sleutels van binnen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="64d12-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="64d12-203">Als deze tijd kan niet genereren van sleutels worden uitgevoerd vanuit hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="64d12-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="64d12-204">Uw Azure Active Directory-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="64d12-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="64d12-205">Hallo volgende voorbeeld maakt u een toepassing met de naam `myAADApp` en maakt gebruik van een wachtwoord van `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="64d12-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="64d12-206">Geef uw eigen wachtwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="64d12-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="64d12-207">Maak een notitie van Hallo `applicationId` die wordt geretourneerd als Hallo uitvoer van de voorgaande opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="64d12-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="64d12-208">Deze toepassing-ID wordt gebruikt in een aantal Hallo resterende stappen.</span><span class="sxs-lookup"><span data-stu-id="64d12-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="64d12-209">Maak vervolgens een service principal name (SPN) zodat de toepassing hello toegankelijk binnen uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="64d12-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="64d12-210">toosuccessfully versleutelen of ontsleutelen van virtuele schijven, machtigingen op Hallo cryptografische sleutel die wordt opgeslagen in de Sleutelkluis moet set toopermit hello tooread Hallo-sleutels Azure Active Directory-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="64d12-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="64d12-211">Hallo SPN maken en de juiste machtigingen Hallo als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="64d12-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="64d12-212">Toevoegen van een virtuele schijf en versleutelingsstatus controleren</span><span class="sxs-lookup"><span data-stu-id="64d12-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="64d12-213">tooactually bepaalde virtuele schijven te versleutelen, kunt een schijf tooan bestaande virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="64d12-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="64d12-214">Voeg een 5Gb gegevens schijf tooan bestaande VM als volgt:</span><span class="sxs-lookup"><span data-stu-id="64d12-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="64d12-215">Hallo virtuele schijven zijn momenteel niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="64d12-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="64d12-216">Hallo huidige coderingsstatus van uw virtuele machine als volgt bekijken:</span><span class="sxs-lookup"><span data-stu-id="64d12-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="64d12-217">Versleutelen van virtuele schijven</span><span class="sxs-lookup"><span data-stu-id="64d12-217">Encrypt virtual disks</span></span>
<span data-ttu-id="64d12-218">toonow versleutelen Hallo virtuele schijven, samenbrengen van alle vorige Hallo-onderdelen:</span><span class="sxs-lookup"><span data-stu-id="64d12-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="64d12-219">Hello Azure Active Directory-toepassing en het wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="64d12-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="64d12-220">Hallo Sleutelkluis toostore Hallo metagegevens voor uw versleutelde schijven opgeven.</span><span class="sxs-lookup"><span data-stu-id="64d12-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="64d12-221">Hallo cryptografische sleutels toouse voor Hallo daadwerkelijke versleuteling en ontsleuteling opgeven.</span><span class="sxs-lookup"><span data-stu-id="64d12-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="64d12-222">Geef op of u tooencrypt Hallo OS schijf, Hallo gegevensschijven of alle wilt.</span><span class="sxs-lookup"><span data-stu-id="64d12-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="64d12-223">U kunt Hallo gedetailleerde gegevens voor uw Azure Sleutelkluis en Hallo sleutel die u hebt gemaakt, als u nodig hebt Hallo Sleutelkluis-ID, URI, en vervolgens sleutel URL in de laatste stap Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="64d12-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="64d12-224">Versleutelen van uw virtuele schijven met Hallo-uitvoer van Hallo `azure keyvault show` en `azure keyvault key show` opdrachten als volgt:</span><span class="sxs-lookup"><span data-stu-id="64d12-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="64d12-225">Aangezien hello voorgaande opdracht veel variabelen heeft, hello volgende voorbeeld is de volledige opdracht Hallo ter referentie:</span><span class="sxs-lookup"><span data-stu-id="64d12-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="64d12-226">Hello Azure CLI biedt geen uitgebreide fouten tijdens het versleutelingsproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="64d12-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="64d12-227">Raadpleeg voor aanvullende informatie voor probleemoplossing `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` op Hallo VM u versleutelt.</span><span class="sxs-lookup"><span data-stu-id="64d12-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="64d12-228">Ten slotte kunt Hallo versleutelingsstatus controleren opnieuw tooconfirm dat uw virtuele schijven nu zijn gecodeerd:</span><span class="sxs-lookup"><span data-stu-id="64d12-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="64d12-229">Toevoegen van extra gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="64d12-229">Add additional data disks</span></span>
<span data-ttu-id="64d12-230">Nadat u uw gegevensschijven hebt versleuteld, kunt u later toevoegen als u meer virtuele schijven tooyour VM en ook versleutelen.</span><span class="sxs-lookup"><span data-stu-id="64d12-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="64d12-231">Bij het uitvoeren van Hallo `azure vm enable-disk-encryption` opdracht, verhoging Hallo sequence versie met behulp van Hallo `--sequence-version` parameter.</span><span class="sxs-lookup"><span data-stu-id="64d12-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="64d12-232">Deze reeks versie-parameter kunt u tooperform herhaalde bewerkingen op Hallo dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="64d12-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="64d12-233">U kunt bijvoorbeeld een tweede virtuele schijf tooyour VM als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="64d12-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="64d12-234">Deze keer Hallo toe te voegen als Hallo opdracht tooencrypt Hallo virtuele schijven, opnieuw `--sequence-version` parameter en stijgende Hallo waarde van de eerste als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="64d12-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="64d12-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64d12-235">Next steps</span></span>
* <span data-ttu-id="64d12-236">Zie voor meer informatie over het beheren van Azure Sleutelkluis, met inbegrip van verwijderen van de cryptografische sleutels en kluizen, [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="64d12-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="64d12-237">Zie voor meer informatie over schijfversleuteling, zoals het voorbereiden van een versleutelde aangepaste VM tooupload tooAzure, [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="64d12-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
