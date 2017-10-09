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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>Een virtuele netwerkgateway configureren voor ExpressRoute met behulp van PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Klassieke - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure-portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Dit artikel begeleidt u bij Hallo stappen tooadd, vergroten of verkleinen en de gateway van een virtueel netwerk (VNet) verwijderen voor een bestaande VNet. Hallo-stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met behulp van Hallo Resource Manager-implementatiemodel dat wordt gebruikt in een ExpressRoute-configuratie. Zie voor meer informatie over virtuele netwerkgateways en configuratie-instellingen voor ExpressRoute gateway [over virtuele netwerkgateways voor ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Voordat u begint
Controleer of u de nieuwste Azure PowerShell-cmdlets Hallo hebt geïnstalleerd. Als u de meest recente cmdlets Hallo nog niet hebt geïnstalleerd, moet u toodo geval voordat u begint met Hallo configuratiestappen. Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Volgende stappen
Nadat u Hallo VNet gateway hebt gemaakt, kunt u uw VNet tooan ExpressRoute-circuit kunt koppelen. Zie [koppelen van een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md).

