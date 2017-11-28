---
title: 'Een virtueel netwerkgateway toevoegen aan een VNet voor ExpressRoute: PowerShell: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het toevoegen van een VNet-gateway naar een bestaande Resource Manager VNet voor ExpressRoute.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="f68fe-103">Een virtuele netwerkgateway configureren voor ExpressRoute met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f68fe-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f68fe-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f68fe-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="f68fe-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f68fe-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="f68fe-106">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f68fe-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="f68fe-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="f68fe-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="f68fe-108">Dit artikel begeleidt u bij de stappen voor het toevoegen en verwijderen van de gateway van een virtueel netwerk (VNet) voor een bestaande VNet vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="f68fe-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="f68fe-109">De stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met het implementatiemodel van Resource Manager dat wordt gebruikt in een ExpressRoute-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f68fe-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="f68fe-110">Zie voor meer informatie over virtuele netwerkgateways en configuratie-instellingen voor ExpressRoute gateway [over virtuele netwerkgateways voor ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="f68fe-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="f68fe-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f68fe-111">Before beginning</span></span>
<span data-ttu-id="f68fe-112">Controleer of de nieuwste Azure PowerShell-cmdlets zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f68fe-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f68fe-113">Als u de meest recente cmdlets nog niet hebt geïnstalleerd, moet u dit doen voordat u begint met de configuratiestappen.</span><span class="sxs-lookup"><span data-stu-id="f68fe-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="f68fe-114">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f68fe-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f68fe-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f68fe-115">Next steps</span></span>
<span data-ttu-id="f68fe-116">Nadat u de VNet-gateway hebt gemaakt, kunt u uw VNet koppelen aan een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="f68fe-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="f68fe-117">Zie [een virtueel netwerk koppelen aan een ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f68fe-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

