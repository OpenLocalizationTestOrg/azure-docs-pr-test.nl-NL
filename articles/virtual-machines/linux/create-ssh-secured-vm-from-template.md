---
title: aaaCreate een Linux VM in Azure uit een sjabloon | Microsoft Docs
description: Hoe toouse hello Azure CLI 2.0 toocreate een Linux-VM met een Resource Manager-sjabloon
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="7de57-103">Hoe toocreate virtuele Linux-machine met Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7de57-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="7de57-104">Dit artikel laat zien hoe tooquickly virtuele Linux-machine (VM) met Azure Resource Manager-sjablonen en hello Azure CLI 2.0 implementeren.</span><span class="sxs-lookup"><span data-stu-id="7de57-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="7de57-105">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7de57-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="7de57-106">Overzicht van sjablonen</span><span class="sxs-lookup"><span data-stu-id="7de57-106">Templates overview</span></span>
<span data-ttu-id="7de57-107">Azure Resource Manager-sjablonen zijn JSON-bestanden die Hallo-infrastructuur en configuratie van uw Azure-oplossing te definiëren.</span><span class="sxs-lookup"><span data-stu-id="7de57-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="7de57-108">Door het gebruik van een sjabloon kunt u gedurende de levenscyclus de oplossing herhaaldelijk implementeren en erop vertrouwen dat uw resources consistent worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="7de57-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="7de57-109">toolearn meer informatie over het Hallo-indeling van het Hallo-sjabloon en de manier waarop u samenstelt, Zie [maken van uw eerste Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7de57-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="7de57-110">tooview hello JSON-syntaxis voor de typen resources, Zie [resources in Azure Resource Manager-sjablonen definiëren](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="7de57-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="7de57-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="7de57-111">Create resource group</span></span>
<span data-ttu-id="7de57-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="7de57-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="7de57-113">Een resourcegroep moet worden gemaakt voordat een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7de57-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="7de57-114">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupVM* in Hallo *eastus* regio:</span><span class="sxs-lookup"><span data-stu-id="7de57-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="7de57-115">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="7de57-115">Create virtual machine</span></span>
<span data-ttu-id="7de57-116">Hallo volgende voorbeeld wordt een virtuele machine uit [deze Azure Resource Manager-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) met [az implementatie maken](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="7de57-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="7de57-117">Geef een waarde van uw eigen openbare SSH-sleutel, zoals de inhoud van Hallo Hallo *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="7de57-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="7de57-118">Als u een SSH-sleutelpaar toocreate nodig hebt, raadpleegt u [hoe toocreate en gebruikt een SSH sleutelpaar voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="7de57-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="7de57-119">In dit voorbeeld moet u een sjabloon die is opgeslagen in GitHub opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7de57-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="7de57-120">U kunt ook downloaden of een sjabloon maken en geef het lokale pad Hallo Hello dezelfde `--template-file` parameter.</span><span class="sxs-lookup"><span data-stu-id="7de57-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="7de57-121">tooSSH tooyour VM, verkrijgen Hallo openbare IP-adres met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="7de57-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="7de57-122">U kunt vervolgens SSH tooyour VM als normale:</span><span class="sxs-lookup"><span data-stu-id="7de57-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="7de57-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7de57-123">Next steps</span></span>
<span data-ttu-id="7de57-124">In dit voorbeeld moet u een basis Linux VM gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7de57-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="7de57-125">Ga voor meer Resource Manager-sjablonen die complexere omgevingen maken of toepassingsframeworks bevatten, Hallo [Azure-sjablonen snelstartgalerie](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="7de57-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
