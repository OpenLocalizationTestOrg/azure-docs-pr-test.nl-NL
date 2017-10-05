---
title: Het lokale netwerk gateway IP-adresvoorvoegsels en het VPN-Gateway-IP-adres wijzigen | Azure | Portal | Microsoft Docs
description: Dit artikel begeleidt u bij het wijzigen van IP-adresvoorvoegsels voor uw lokale netwerkgateway met de Azure portal.
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
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="1391f-103">Lokale gateway netwerkinstellingen wijzigen met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="1391f-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="1391f-104">Soms worden de instellingen voor uw lokale netwerkgateway AddressPrefix of GatewayIPAddress gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1391f-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="1391f-105">In dit artikel leest u hoe uw lokale netwerk gateway-instellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1391f-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="1391f-106">Ook kunt u deze instellingen met een andere methode door een andere optie te selecteren in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="1391f-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1391f-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1391f-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="1391f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1391f-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="1391f-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="1391f-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="1391f-110"><a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen</span><span class="sxs-lookup"><span data-stu-id="1391f-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="1391f-111">Wanneer u IP-adresvoorvoegsels wijzigen, afhankelijk van de stappen die u volgt of uw lokale netwerkgateway een verbinding heeft.</span><span class="sxs-lookup"><span data-stu-id="1391f-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="1391f-112"><a name="gwip"></a>Het IP-adres wijzigen</span><span class="sxs-lookup"><span data-stu-id="1391f-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="1391f-113">Als van het VPN-apparaat waarmee u verbinding wilt maken het openbare IP-adres is gewijzigd, moet u de gateway van het lokale netwerk aanpassen met deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="1391f-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="1391f-114">Wanneer u het openbare IP-adres verandert, afhankelijk van de stappen die u volgt of uw lokale netwerkgateway een verbinding heeft.</span><span class="sxs-lookup"><span data-stu-id="1391f-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1391f-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1391f-115">Next steps</span></span>

<span data-ttu-id="1391f-116">U kunt de gatewayverbinding controleren.</span><span class="sxs-lookup"><span data-stu-id="1391f-116">You can verify your gateway connection.</span></span> <span data-ttu-id="1391f-117">Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1391f-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>