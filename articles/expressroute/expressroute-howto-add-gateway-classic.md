---
title: 'Een VNet-gateway configureren voor ExpressRoute met behulp van PowerShell: klassieke: Azure | Microsoft Docs'
description: Configureer een VNet-gateway voor een klassieke implementatie model VNet met behulp van PowerShell voor een ExpressRoute-configuratie.
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="a238c-103">Configureren van een virtuele netwerkgateway voor ExpressRoute met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="a238c-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a238c-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a238c-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="a238c-105">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a238c-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="a238c-106">Video - Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="a238c-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="a238c-107">In dit artikel begeleidt u via Hallo stappen tooadd, vergroten of verkleinen, en verwijder de gateway van een virtueel netwerk (VNet) voor een bestaande VNet.</span><span class="sxs-lookup"><span data-stu-id="a238c-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="a238c-108">Hallo stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met de Hallo **klassieke implementatiemodel** en die worden gebruikt in een ExpressRoute-configuratie.</span><span class="sxs-lookup"><span data-stu-id="a238c-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="a238c-109">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="a238c-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="a238c-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a238c-110">Before beginning</span></span>
<span data-ttu-id="a238c-111">Controleer of u hello Azure PowerShell-cmdlets die nodig zijn voor deze configuratie hebt geïnstalleerd (1.0.2 of hoger).</span><span class="sxs-lookup"><span data-stu-id="a238c-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="a238c-112">Als het Hallo-cmdlets kunt u dit nog niet hebt geïnstalleerd, moet u toodo geval voordat u begint met Hallo configuratiestappen.</span><span class="sxs-lookup"><span data-stu-id="a238c-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="a238c-113">Zie voor meer informatie over het installeren van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a238c-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a238c-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a238c-114">Next steps</span></span>
<span data-ttu-id="a238c-115">Nadat u Hallo VNet gateway hebt gemaakt, kunt u uw VNet tooan ExpressRoute-circuit kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="a238c-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="a238c-116">Zie [koppelen van een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="a238c-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

