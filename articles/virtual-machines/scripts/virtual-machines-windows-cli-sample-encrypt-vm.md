---
title: Azure CLI Sample Script - versleutelen van een Windows VM | Microsoft Docs
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
ms.openlocfilehash: 9574d779982c939aa970cd4bdf7df6e66793e3b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="e0768-103">Versleutelen van een virtuele Windows-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="e0768-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="e0768-104">Dit script maakt een beveiligde Azure Sleutelkluis, versleutelingssleutels, Azure Active Directory service-principal en virtuele Windows-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="e0768-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="e0768-105">De virtuele machine wordt vervolgens versleuteld met behulp van de versleutelingssleutel van de Sleutelkluis en service principal referenties.</span><span class="sxs-lookup"><span data-stu-id="e0768-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e0768-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="e0768-106">Sample script</span></span>

<span data-ttu-id="e0768-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "versleutelen VM-schijven")]</span><span class="sxs-lookup"><span data-stu-id="e0768-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e0768-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="e0768-108">Clean up deployment</span></span> 

<span data-ttu-id="e0768-109">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e0768-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e0768-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="e0768-110">Script explanation</span></span>

<span data-ttu-id="e0768-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, Azure Sleutelkluis, service-principal, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="e0768-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="e0768-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="e0768-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e0768-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="e0768-113">Command</span></span> | <span data-ttu-id="e0768-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e0768-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0768-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="e0768-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e0768-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e0768-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e0768-117">AZ keyvault maken</span><span class="sxs-lookup"><span data-stu-id="e0768-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="e0768-118">Hiermee maakt u een Azure Key Vault voor het opslaan van beveiligde gegevens, zoals versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="e0768-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="e0768-119">AZ keyvault-sleutel maken</span><span class="sxs-lookup"><span data-stu-id="e0768-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="e0768-120">Maakt een versleutelingssleutel in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="e0768-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="e0768-121">AZ ad sp maken-voor-rbac</span><span class="sxs-lookup"><span data-stu-id="e0768-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="e0768-122">Maakt een Azure Active Directory service-principal veilig verifiëren en toegang tot de versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="e0768-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="e0768-123">AZ keyvault-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="e0768-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="e0768-124">Stelt de machtigingen op de Sleutelkluis de service principal toegang verlenen tot versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="e0768-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="e0768-125">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="e0768-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e0768-126">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="e0768-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e0768-127">Met deze opdracht geeft ook de afbeelding van de virtuele machine moet worden gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="e0768-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="e0768-128">AZ vm-codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="e0768-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="e0768-129">Hiermee schakelt u versleuteling op een virtuele machine met behulp van de service principal referenties en de versleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="e0768-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="e0768-130">AZ vm versleuteling weergeven</span><span class="sxs-lookup"><span data-stu-id="e0768-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="e0768-131">Toont de status van het VM-versleutelingsproces.</span><span class="sxs-lookup"><span data-stu-id="e0768-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="e0768-132">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="e0768-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e0768-133">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="e0768-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0768-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0768-134">Next steps</span></span>

<span data-ttu-id="e0768-135">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0768-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e0768-136">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0768-136">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>
