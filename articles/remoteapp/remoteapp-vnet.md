---
title: aaaValidate hello Azure VNET toouse met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toomake ervoor dat uw Azure VNET is gereed toouse met Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="5486c-103">Hello Azure VNET toouse met Azure RemoteApp valideren</span><span class="sxs-lookup"><span data-stu-id="5486c-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5486c-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="5486c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5486c-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5486c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5486c-106">Voordat u een Azure-VNET met Azure RemoteApp gebruiken, kunt u toovalidate hello VNET.</span><span class="sxs-lookup"><span data-stu-id="5486c-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="5486c-107">Hiermee voorkomt u problemen met de connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="5486c-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="5486c-108">toovalidate uw Azure-VNET Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5486c-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="5486c-109">Maak een virtuele machine van Azure binnen Hallo subnet van hello Azure VNET gewenste toouse met Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5486c-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="5486c-110">Toothat VM verbinding via Hallo **Connect** optie in Hallo-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="5486c-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="5486c-111">Hallo virtuele machine toohello deelnemen aan hetzelfde domein dat u wilt dat toouse met Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5486c-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="5486c-112">Als u een hybride verzameling die tooyour on-premises netwerk verbindt, lid worden van Hallo virtuele machine tooyour lokale domein.</span><span class="sxs-lookup"><span data-stu-id="5486c-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="5486c-113">Als dit lukt, is hello Azure VNET gereed toouse met RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5486c-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="5486c-114">Zie voor meer informatie over Hallo end-to-end hybride verzameling werkstroom Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5486c-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="5486c-115">Hoe tooplan het virtuele netwerk voor Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5486c-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="5486c-116">Een hybride verzameling maken</span><span class="sxs-lookup"><span data-stu-id="5486c-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="5486c-117">Azure RemoteApp-collectie tooyour Azure Virtual Network (met ondersteuning voor ExpressRoute) implementeren</span><span class="sxs-lookup"><span data-stu-id="5486c-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

