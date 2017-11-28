---
title: aaaAzure voorbeeldscript CLI - versleutelen van een virtuele machine van Windows | Microsoft Docs
description: Azure CLI Sample Script - versleutelen van een Windows VM
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="58f39-103">Versleutelen van een virtuele Windows-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="58f39-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="58f39-104">Dit script maakt een beveiligde Azure Sleutelkluis, versleutelingssleutels, Azure Active Directory service-principal en virtuele Windows-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="58f39-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="58f39-105">Hallo VM wordt vervolgens versleuteld met de versleutelingssleutel Hallo van Sleutelkluis en de service principal referenties.</span><span class="sxs-lookup"><span data-stu-id="58f39-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="58f39-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="58f39-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="58f39-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="58f39-107">Clean up deployment</span></span> 

<span data-ttu-id="58f39-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="58f39-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="58f39-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="58f39-109">Script explanation</span></span>

<span data-ttu-id="58f39-110">Dit script gebruikt Hallo opdrachten toocreate na een resource groep Azure Key Vault service principal, virtuele machine, en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="58f39-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="58f39-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="58f39-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="58f39-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="58f39-112">Command</span></span> | <span data-ttu-id="58f39-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="58f39-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58f39-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="58f39-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="58f39-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="58f39-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58f39-116">AZ keyvault maken</span><span class="sxs-lookup"><span data-stu-id="58f39-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="58f39-117">Hiermee maakt u een beveiligde gegevens van Azure Sleutelkluis toostore zoals versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="58f39-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="58f39-118">AZ keyvault-sleutel maken</span><span class="sxs-lookup"><span data-stu-id="58f39-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="58f39-119">Maakt een versleutelingssleutel in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="58f39-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="58f39-120">AZ ad sp maken-voor-rbac</span><span class="sxs-lookup"><span data-stu-id="58f39-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="58f39-121">Hiermee maakt u een Azure Active Directory-service principal toosecurely verifiëren en toegang tooencryption sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="58f39-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="58f39-122">AZ keyvault-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="58f39-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="58f39-123">Machtigingen op Hallo Sleutelkluis toogrant Hallo service principal tooencryption toegangstoetsen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="58f39-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="58f39-124">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="58f39-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="58f39-125">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="58f39-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="58f39-126">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="58f39-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="58f39-127">AZ vm-codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="58f39-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="58f39-128">Hiermee schakelt u versleuteling op een virtuele machine met behulp van de principal Servicereferenties Hallo en versleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="58f39-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="58f39-129">AZ vm versleuteling weergeven</span><span class="sxs-lookup"><span data-stu-id="58f39-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="58f39-130">Geeft de status Hallo Hallo versleutelingsproces VM.</span><span class="sxs-lookup"><span data-stu-id="58f39-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="58f39-131">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="58f39-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="58f39-132">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="58f39-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58f39-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58f39-133">Next steps</span></span>

<span data-ttu-id="58f39-134">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58f39-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="58f39-135">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58f39-135">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>
