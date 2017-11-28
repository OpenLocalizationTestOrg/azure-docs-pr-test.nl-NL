---
title: een klassieke virtuele Linux-machine met aaaCreate hello Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe een virtuele Linux-machine met het gebruik van Azure CLI 1.0 Hallo toocreate Hallo klassieke implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="24b75-103">Hoe tooCreate een klassieke Linux-VM met Azure CLI 1.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="24b75-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="24b75-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="24b75-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="24b75-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="24b75-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="24b75-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="24b75-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="24b75-107">Zie voor de Resource Manager-versie Hallo [hier](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24b75-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="24b75-108">Dit onderwerp wordt beschreven hoe toocreate virtuele Linux-machine (VM) met het gebruik van Azure CLI 1.0 Hallo Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="24b75-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="24b75-109">We gebruiken de installatiekopie van een Linux van Hallo beschikbaar **INSTALLATIEKOPIEËN** op Azure.</span><span class="sxs-lookup"><span data-stu-id="24b75-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="24b75-110">Hello Azure CLI 1.0 opdrachten geven Hallo na configuratie-opties, onder andere:</span><span class="sxs-lookup"><span data-stu-id="24b75-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="24b75-111">Hallo VM tooa virtueel netwerk verbinden</span><span class="sxs-lookup"><span data-stu-id="24b75-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="24b75-112">Hallo VM tooan bestaande cloudservice toevoegen</span><span class="sxs-lookup"><span data-stu-id="24b75-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="24b75-113">Hallo VM tooan bestaande opslagaccount toevoegen</span><span class="sxs-lookup"><span data-stu-id="24b75-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="24b75-114">Hallo VM tooan beschikbaarheidsset of locatie toe te voegen</span><span class="sxs-lookup"><span data-stu-id="24b75-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24b75-115">Als u uw VM toouse een virtueel netwerk, wilt zodat u verbinding met tooit rechtstreeks door de hostnaam of het instellen van de cross-premises verbindingen maken kunt, zorg er dan voor dat u opgeeft Hallo virtueel netwerk wanneer u Hallo VM maakt.</span><span class="sxs-lookup"><span data-stu-id="24b75-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="24b75-116">Een virtuele machine kan geconfigureerde toojoin een virtueel netwerk worden alleen wanneer u Hallo VM maakt.</span><span class="sxs-lookup"><span data-stu-id="24b75-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="24b75-117">Zie voor meer informatie over virtuele netwerken, [Azure Virtual Network-overzicht](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="24b75-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="24b75-118">Hoe toocreate een Linux-VM met Hallo klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="24b75-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

