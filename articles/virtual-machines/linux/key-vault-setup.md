---
title: aaaSet van Azure Sleutelkluis voor virtuele Linux-machines | Microsoft Docs
description: Hoe Hallo tooset up Sleutelkluis voor gebruik met een virtuele machine van Azure Resource Manager met CLI 2.0.
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
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="634d8-103">Hoe tooset up Sleutelkluis voor virtuele machines met Azure CLI 2.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="634d8-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="634d8-104">In Azure Resource Manager-stack hello, worden geheimen/certificaten gemodelleerd als resources die worden geleverd door de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="634d8-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="634d8-105">Zie toolearn meer informatie over Azure Key Vault [wat is Azure Sleutelkluis?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="634d8-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="634d8-106">Hallo in volgorde voor Sleutelkluis toobe gebruikt met virtuele machines van Azure Resource Manager *EnabledForDeployment* eigenschap op Sleutelkluis tootrue moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="634d8-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="634d8-107">Dit artikel ziet u hoe tooset up Sleutelkluis voor gebruik met virtuele Azure-machines (VM's) met behulp van Azure CLI 2.0 Hallo.</span><span class="sxs-lookup"><span data-stu-id="634d8-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="634d8-108">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="634d8-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="634d8-109">tooperform deze stappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="634d8-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="634d8-110">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="634d8-110">Create a Key Vault</span></span>
<span data-ttu-id="634d8-111">Een sleutelkluis maken en toewijzen van beleid voor Hallo-implementatie met [az keyvault maken](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="634d8-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="634d8-112">Hallo volgende voorbeeld wordt een sleutelkluis met de naam `myKeyVault` in Hallo `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="634d8-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="634d8-113">Een Sleutelkluis voor gebruik met virtuele machines bijwerken</span><span class="sxs-lookup"><span data-stu-id="634d8-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="634d8-114">Hallo implementatiebeleid instellen op een bestaande sleutelkluis met [az keyvault update](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="634d8-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="634d8-115">Hallo volgende updates Hallo met de naam sleutelkluis `myKeyVault` in Hallo `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="634d8-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="634d8-116">Gebruik sjablonen tooset up Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="634d8-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="634d8-117">Wanneer u een sjabloon gebruikt, moet u tooset hello `enabledForDeployment` eigenschap te`true` voor Hallo Sleutelkluis resource als volgt:</span><span class="sxs-lookup"><span data-stu-id="634d8-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="634d8-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="634d8-118">Next steps</span></span>
<span data-ttu-id="634d8-119">Zie voor andere opties die u configureren kunt wanneer u een Sleutelkluis maken met behulp van sjablonen, [een sleutelkluis maken](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="634d8-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
