---
title: "Over Linux-VM-installatiekopieën in Azure | Microsoft Docs"
description: "Meer informatie over hoe de Linux-installatiekopieën worden gebruikt met virtuele machines in Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: e6ea8adc-4e7a-467a-9394-cd05e67898b7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/21/2016
ms.author: cynthn
ms.openlocfilehash: 187642db18806f4034dcecf4c25b5c71028fdfe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-linux-virtual-machines"></a><span data-ttu-id="73f1e-103">Over de installatiekopieën voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="73f1e-103">About images for Linux virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="73f1e-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="73f1e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="73f1e-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="73f1e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="73f1e-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="73f1e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="73f1e-107">Zie voor informatie over installatiekopieën van het Resource Manager-model met [hier](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73f1e-107">For information about images using the Resource Manager model, see [here](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="73f1e-108">Werken met installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="73f1e-108">Working with images</span></span>
<span data-ttu-id="73f1e-109">U kunt de Azure-opdrachtregelinterface (CLI) voor Mac, Linux en Windows gebruiken voor het beheren van de beschikbare installatiekopieën naar uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="73f1e-109">You can use the Azure Command-Line Interface (CLI) for Mac, Linux, and Windows to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="73f1e-110">U kunt de Azure-portal ook gebruiken voor een aantal taken van de installatiekopie, maar de opdrachtregel biedt u meer mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="73f1e-110">You also can use the Azure portal for some image tasks, but the command line gives you more options.</span></span>

<span data-ttu-id="73f1e-111">Zie voor voorbeelden van het gebruik van de hulpprogramma's [algemene Azure CLI-opdrachten in Linux en Mac](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73f1e-111">For examples of using the tools, see [Common Azure CLI commands on Linux and Mac](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73f1e-112">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73f1e-112">Next steps</span></span>
<span data-ttu-id="73f1e-113">U kunt ook [uw eigen installatiekopie uploaden](create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="73f1e-113">You can also [upload your own image](create-upload-vhd.md).</span></span>
