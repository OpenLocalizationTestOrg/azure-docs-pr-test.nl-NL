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
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="3f807-103">Configureren van een virtuele netwerkgateway voor ExpressRoute met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="3f807-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f807-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f807-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="3f807-105">Klassieke - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f807-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="3f807-106">Video - Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="3f807-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="3f807-107">In dit artikel begeleidt u bij de stappen voor het toevoegen en verwijderen van de gateway van een virtueel netwerk (VNet) voor een bestaande VNet vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="3f807-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="3f807-108">De stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met de **klassieke implementatiemodel** en die worden gebruikt in een ExpressRoute-configuratie.</span><span class="sxs-lookup"><span data-stu-id="3f807-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="3f807-109">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="3f807-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="3f807-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="3f807-110">Before beginning</span></span>
<span data-ttu-id="3f807-111">Controleer of u de Azure PowerShell-cmdlets die nodig zijn voor deze configuratie hebt geïnstalleerd (1.0.2 of hoger).</span><span class="sxs-lookup"><span data-stu-id="3f807-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="3f807-112">Als u de cmdlets nog niet hebt geïnstalleerd, moet u dit doen voordat u begint met de configuratiestappen.</span><span class="sxs-lookup"><span data-stu-id="3f807-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="3f807-113">Zie voor meer informatie over het installeren van Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f807-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3f807-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f807-114">Next steps</span></span>
<span data-ttu-id="3f807-115">Nadat u de VNet-gateway hebt gemaakt, kunt u uw VNet koppelen aan een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="3f807-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="3f807-116">Zie [een virtueel netwerk koppelen aan een ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="3f807-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

