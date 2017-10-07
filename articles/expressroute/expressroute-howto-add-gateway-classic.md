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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Configureren van een virtuele netwerkgateway voor ExpressRoute met behulp van PowerShell (klassiek)
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Klassieke - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure-Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

In dit artikel begeleidt u via Hallo stappen tooadd, vergroten of verkleinen, en verwijder de gateway van een virtueel netwerk (VNet) voor een bestaande VNet. Hallo stappen voor deze configuratie zijn specifiek voor VNets die zijn gemaakt met de Hallo **klassieke implementatiemodel** en die worden gebruikt in een ExpressRoute-configuratie. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Voordat u begint
Controleer of u hello Azure PowerShell-cmdlets die nodig zijn voor deze configuratie hebt geïnstalleerd (1.0.2 of hoger). Als het Hallo-cmdlets kunt u dit nog niet hebt geïnstalleerd, moet u toodo geval voordat u begint met Hallo configuratiestappen. Zie voor meer informatie over het installeren van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Volgende stappen
Nadat u Hallo VNet gateway hebt gemaakt, kunt u uw VNet tooan ExpressRoute-circuit kunt koppelen. Zie [koppelen van een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md).

