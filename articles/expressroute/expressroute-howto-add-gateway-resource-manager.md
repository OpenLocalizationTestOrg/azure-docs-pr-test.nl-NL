---
title: 'Toevoegen van een virtueel netwerk gateway tooa VNet voor ExpressRoute: PowerShell: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het toevoegen van een VNet gateway tooan al gemaakt Resource Manager VNet voor ExpressRoute.
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
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="61452-103">Een virtuele netwerkgateway configureren voor ExpressRoute met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="61452-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61452-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61452-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="61452-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="61452-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="61452-106">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="61452-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="61452-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="61452-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="61452-108">Dit artikel begeleidt u bij Hallo stappen tooadd, vergroten of verkleinen en de gateway van een virtueel netwerk (VNet) verwijderen voor een bestaande VNet.</span><span class="sxs-lookup"><span data-stu-id="61452-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="61452-109">Hallo-stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met behulp van Hallo Resource Manager-implementatiemodel dat wordt gebruikt in een ExpressRoute-configuratie.</span><span class="sxs-lookup"><span data-stu-id="61452-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="61452-110">Zie voor meer informatie over virtuele netwerkgateways en configuratie-instellingen voor ExpressRoute gateway [over virtuele netwerkgateways voor ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="61452-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="61452-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="61452-111">Before beginning</span></span>
<span data-ttu-id="61452-112">Controleer of u de nieuwste Azure PowerShell-cmdlets Hallo hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="61452-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="61452-113">Als u de meest recente cmdlets Hallo nog niet hebt geïnstalleerd, moet u toodo geval voordat u begint met Hallo configuratiestappen.</span><span class="sxs-lookup"><span data-stu-id="61452-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="61452-114">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="61452-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="61452-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61452-115">Next steps</span></span>
<span data-ttu-id="61452-116">Nadat u Hallo VNet gateway hebt gemaakt, kunt u uw VNet tooan ExpressRoute-circuit kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="61452-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="61452-117">Zie [koppelen van een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="61452-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

