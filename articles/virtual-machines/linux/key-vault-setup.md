---
title: Instellen van Azure Sleutelkluis voor virtuele Linux-machines | Microsoft Docs
description: Het instellen van de Sleutelkluis voor gebruik met een virtuele machine van Azure Resource Manager met de CLI 2.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 2cc9b4c978e9a4deb0c8443c4b0f9e301a7cf492
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="68a85-103">Het instellen van de Sleutelkluis voor virtuele machines met de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="68a85-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="68a85-104">In de Azure Resource Manager-stack zijn geheimen/certificaten gemodelleerd als resources die worden geleverd door de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="68a85-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="68a85-105">Zie voor meer informatie over Azure Sleutelkluis, [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="68a85-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="68a85-106">In de volgorde voor Sleutelkluis moet worden gebruikt met Azure Resource Manager virtuele machines, de *EnabledForDeployment* eigenschap voor Sleutelkluis moet zijn ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="68a85-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="68a85-107">In dit artikel leest u hoe Sleutelkluis instellen voor gebruik met virtuele Azure-machines (VM's) met behulp van de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="68a85-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="68a85-108">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68a85-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="68a85-109">Als u wilt deze stappen uitvoert, moet u de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="68a85-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="68a85-110">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="68a85-110">Create a Key Vault</span></span>
<span data-ttu-id="68a85-111">Een sleutelkluis maken en toewijzen van het implementatiebeleid voor met [az keyvault maken](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="68a85-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="68a85-112">Het volgende voorbeeld wordt een sleutelkluis met de naam `myKeyVault` in de `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="68a85-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="68a85-113">Een Sleutelkluis voor gebruik met virtuele machines bijwerken</span><span class="sxs-lookup"><span data-stu-id="68a85-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="68a85-114">Stel het beleid voor implementatie op een bestaande sleutel vault met [az keyvault update](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="68a85-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="68a85-115">De volgende updates de sleutelkluis met de naam `myKeyVault` in de `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="68a85-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="68a85-116">Sjablonen gebruiken voor het instellen van de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="68a85-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="68a85-117">Wanneer u een sjabloon gebruikt, moet u om in te stellen de `enabledForDeployment` eigenschap `true` voor de sleutel Vault resource als volgt:</span><span class="sxs-lookup"><span data-stu-id="68a85-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="68a85-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68a85-118">Next steps</span></span>
<span data-ttu-id="68a85-119">Zie voor andere opties die u configureren kunt wanneer u een Sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="68a85-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
