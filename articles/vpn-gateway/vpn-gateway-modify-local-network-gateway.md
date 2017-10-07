---
title: Hallo lokale netwerk gateway IP-adresvoorvoegsels en Hallo VPN-Gateway-IP-adres wijzigen | Azure | PowerShell | Microsoft Docs
description: Dit artikel begeleidt u bij het wijzigen van IP-adresvoorvoegsels voor uw lokale netwerkgateway met behulp van PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Instellingen voor lokale netwerkgateway wijzigen met PowerShell

Soms wijzigen Hallo voor uw lokale netwerkgateway AddressPrefix of GatewayIPAddress. Dit artikel ziet u hoe toomodify gateway-instellingen van uw lokale netwerk. U kunt deze instellingen met een andere methode door een andere optie selecteren in lijst na Hallo ook wijzigen:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure-CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Voordat u begint

Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.

## <a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Hallo gateway IP-adres wijzigen

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Volgende stappen

U kunt de gatewayverbinding controleren. Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).