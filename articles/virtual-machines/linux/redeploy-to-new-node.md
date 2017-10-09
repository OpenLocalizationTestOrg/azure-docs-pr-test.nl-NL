---
title: aaaRedeploy Linux virtuele Machines in Azure | Microsoft Docs
description: Hoe problemen die tooredeploy Linux virtuele machines in Azure toomitigate SSH-verbinding.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="82e00-103">Linux-virtuele machine toonew Azure knooppunt opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="82e00-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="82e00-104">Als u problemen bij het oplossen van SSH wordt geconfronteerd of toepassing access tooa Linux virtuele machine (VM) in Azure, kan Hallo VM opnieuw distribueren helpen.</span><span class="sxs-lookup"><span data-stu-id="82e00-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="82e00-105">Wanneer u een virtuele machine opnieuw implementeert, wordt verplaatst Hallo VM tooa nieuw knooppunt binnen hello Azure-infrastructuur en wordt deze vervolgens weer ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="82e00-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="82e00-106">Alle configuratie-opties en bijbehorende bronnen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="82e00-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="82e00-107">Dit artikel ziet u hoe tooredeploy een VM die gebruikmaakt van Azure CLI of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="82e00-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="82e00-108">Nadat u een virtuele machine opnieuw implementeren, is Hallo tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="82e00-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="82e00-109">U kunt een virtuele machine met behulp van een Hallo volgend opties voor opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="82e00-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="82e00-110">U hoeft alleen toochoose één optie tooredeploy uw virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="82e00-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="82e00-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="82e00-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="82e00-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="82e00-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="82e00-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="82e00-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="82e00-114">Hello Azure CLI 2.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="82e00-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="82e00-115">Meest recente installatie Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="82e00-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="82e00-116">Implementeren van uw virtuele machine met [az vm opnieuw distribueren](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="82e00-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="82e00-117">voorbeeld redeploys na Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="82e00-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="82e00-118">Gebruik hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="82e00-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="82e00-119">Hallo installeren [nieuwste Azure CLI 1.0](../../cli-install-nodejs.md)tooan Azure-account aanmelden en zorg ervoor dat u in de modus Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="82e00-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="82e00-120">voorbeeld redeploys na Hallo Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="82e00-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="82e00-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82e00-121">Next steps</span></span>
<span data-ttu-id="82e00-122">Als u verbinding maken met tooyour VM problemen ondervindt, kunt u Help-informatie vinden op [probleemoplossing SSH-verbindingen](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [gedetailleerde stappen voor probleemoplossing SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82e00-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="82e00-123">Als u geen toegang een toepassing die wordt uitgevoerd op de virtuele machine tot, kunt u ook lezen [toepassing het oplossen van problemen](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82e00-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

