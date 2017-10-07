---
title: Hallo lokale netwerk gateway IP-adresvoorvoegsels en Hallo VPN-Gateway-IP-adres wijzigen | Azure | CLI | Microsoft Docs
description: Dit artikel begeleidt u bij het wijzigen van IP-adresvoorvoegsels voor uw lokale netwerkgateway met hello Azure CLI.
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a>Lokale gateway netwerkinstellingen wijzigen met behulp van hello Azure CLI

Soms Hallo-instellingen voor uw lokale netwerkgateway adresvoorvoegsel of IP-adres Gateway worden gewijzigd. Dit artikel ziet u hoe toomodify gateway-instellingen van uw lokale netwerk. U kunt deze instellingen met een andere methode door een andere optie selecteren in lijst na Hallo ook wijzigen:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure-CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Voordat u begint

Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger). Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <a name="gwip"></a>Hallo gateway IP-adres wijzigen

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a>Volgende stappen

U kunt de gatewayverbinding controleren. Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).

