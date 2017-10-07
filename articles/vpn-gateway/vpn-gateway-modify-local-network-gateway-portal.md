---
title: Hallo lokale netwerk gateway IP-adresvoorvoegsels en Hallo VPN-Gateway-IP-adres wijzigen | Azure | Portal | Microsoft Docs
description: Dit artikel begeleidt u bij het wijzigen van IP-adresvoorvoegsels voor uw lokale netwerkgateway met hello Azure-portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="258f2-103">Lokale gateway netwerkinstellingen wijzigen met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="258f2-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="258f2-104">Soms wijzigen Hallo voor uw lokale netwerkgateway AddressPrefix of GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="258f2-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="258f2-105">Dit artikel ziet u hoe toomodify gateway-instellingen van uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="258f2-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="258f2-106">U kunt deze instellingen met een andere methode door een andere optie selecteren in lijst na Hallo ook wijzigen:</span><span class="sxs-lookup"><span data-stu-id="258f2-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="258f2-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="258f2-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="258f2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="258f2-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="258f2-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="258f2-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="258f2-110"><a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen</span><span class="sxs-lookup"><span data-stu-id="258f2-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="258f2-111">Wanneer u IP-adresvoorvoegsels wijzigt, Hallo stappen die u volgt afhankelijk van of uw lokale netwerkgateway een verbinding heeft.</span><span class="sxs-lookup"><span data-stu-id="258f2-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="258f2-112"><a name="gwip"></a>Hallo gateway IP-adres wijzigen</span><span class="sxs-lookup"><span data-stu-id="258f2-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="258f2-113">Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen.</span><span class="sxs-lookup"><span data-stu-id="258f2-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="258f2-114">Wanneer u het openbare IP-adres Hallo wijzigt, Hallo stappen die u volgt afhankelijk van of uw lokale netwerkgateway een verbinding heeft.</span><span class="sxs-lookup"><span data-stu-id="258f2-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="258f2-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="258f2-115">Next steps</span></span>

<span data-ttu-id="258f2-116">U kunt de gatewayverbinding controleren.</span><span class="sxs-lookup"><span data-stu-id="258f2-116">You can verify your gateway connection.</span></span> <span data-ttu-id="258f2-117">Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="258f2-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>