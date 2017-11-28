---
title: aaaAzure voorbeeldscript CLI - een Linux-VM versleutelen | Microsoft Docs
description: Azure CLI Script voorbeeld - een virtuele Linux-machine versleutelen
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="942e4-103">Versleutelen van een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="942e4-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="942e4-104">Dit script maakt een beveiligde Azure Sleutelkluis, versleutelingssleutels, Azure Active Directory service-principal en virtuele Linux-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="942e4-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="942e4-105">Hallo VM wordt vervolgens versleuteld met de versleutelingssleutel Hallo van Sleutelkluis en de service principal referenties.</span><span class="sxs-lookup"><span data-stu-id="942e4-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="942e4-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="942e4-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="942e4-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="942e4-107">Clean up deployment</span></span> 

<span data-ttu-id="942e4-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="942e4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="942e4-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="942e4-109">Script explanation</span></span>

<span data-ttu-id="942e4-110">Dit script gebruikt Hallo opdrachten toocreate na een resource groep Azure Key Vault service principal, virtuele machine, en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="942e4-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="942e4-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="942e4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="942e4-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="942e4-112">Command</span></span> | <span data-ttu-id="942e4-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="942e4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="942e4-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="942e4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="942e4-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="942e4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="942e4-116">AZ keyvault maken</span><span class="sxs-lookup"><span data-stu-id="942e4-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="942e4-117">Hiermee maakt u een beveiligde gegevens van Azure Sleutelkluis toostore zoals versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="942e4-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="942e4-118">AZ keyvault-sleutel maken</span><span class="sxs-lookup"><span data-stu-id="942e4-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="942e4-119">Maakt een versleutelingssleutel in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="942e4-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="942e4-120">AZ ad sp maken-voor-rbac</span><span class="sxs-lookup"><span data-stu-id="942e4-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="942e4-121">Hiermee maakt u een Azure Active Directory-service principal toosecurely verifiëren en toegang tooencryption sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="942e4-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="942e4-122">AZ keyvault-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="942e4-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="942e4-123">Machtigingen op Hallo Sleutelkluis toogrant Hallo service principal tooencryption toegangstoetsen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="942e4-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="942e4-124">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="942e4-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="942e4-125">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="942e4-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="942e4-126">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="942e4-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="942e4-127">AZ vm-codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="942e4-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="942e4-128">Hiermee schakelt u versleuteling op een virtuele machine met behulp van de principal Servicereferenties Hallo en versleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="942e4-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="942e4-129">AZ vm versleuteling weergeven</span><span class="sxs-lookup"><span data-stu-id="942e4-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="942e4-130">Geeft de status Hallo Hallo versleutelingsproces VM.</span><span class="sxs-lookup"><span data-stu-id="942e4-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="942e4-131">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="942e4-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="942e4-132">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="942e4-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="942e4-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="942e4-133">Next steps</span></span>

<span data-ttu-id="942e4-134">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="942e4-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="942e4-135">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="942e4-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
