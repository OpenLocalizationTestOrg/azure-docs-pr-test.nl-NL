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
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="2f691-103">Instellingen voor lokale netwerkgateway wijzigen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f691-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="2f691-104">Soms wijzigen Hallo voor uw lokale netwerkgateway AddressPrefix of GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="2f691-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="2f691-105">Dit artikel ziet u hoe toomodify gateway-instellingen van uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="2f691-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="2f691-106">U kunt deze instellingen met een andere methode door een andere optie selecteren in lijst na Hallo ook wijzigen:</span><span class="sxs-lookup"><span data-stu-id="2f691-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f691-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2f691-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="2f691-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f691-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="2f691-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="2f691-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="2f691-110"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2f691-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="2f691-111">Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2f691-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="2f691-112">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2f691-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="2f691-113"><a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen</span><span class="sxs-lookup"><span data-stu-id="2f691-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="2f691-114"><a name="gwip"></a>Hallo gateway IP-adres wijzigen</span><span class="sxs-lookup"><span data-stu-id="2f691-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2f691-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f691-115">Next steps</span></span>

<span data-ttu-id="2f691-116">U kunt de gatewayverbinding controleren.</span><span class="sxs-lookup"><span data-stu-id="2f691-116">You can verify your gateway connection.</span></span> <span data-ttu-id="2f691-117">Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2f691-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>