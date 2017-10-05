---
title: Het lokale netwerk gateway IP-adresvoorvoegsels en het VPN-Gateway-IP-adres wijzigen | Azure | PowerShell | Microsoft Docs
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
ms.openlocfilehash: 2a095b96a8c352abeca72640d37c0d629b447763
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="fd097-103">Instellingen voor lokale netwerkgateway wijzigen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd097-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="fd097-104">Soms worden de instellingen voor uw lokale netwerkgateway AddressPrefix of GatewayIPAddress gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fd097-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="fd097-105">In dit artikel leest u hoe uw lokale netwerk gateway-instellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fd097-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="fd097-106">Ook kunt u deze instellingen met een andere methode door een andere optie te selecteren in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="fd097-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd097-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fd097-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="fd097-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd097-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="fd097-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="fd097-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="fd097-110"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fd097-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="fd097-111">Installeer de meest recente versie van de PowerShell-cmdlets van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fd097-111">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="fd097-112">Zie [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Azure PowerShell installeren en configureren) voor meer informatie over het installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="fd097-112">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <span data-ttu-id="fd097-113"><a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen</span><span class="sxs-lookup"><span data-stu-id="fd097-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="fd097-114"><a name="gwip"></a>Het IP-adres wijzigen</span><span class="sxs-lookup"><span data-stu-id="fd097-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="fd097-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fd097-115">Next steps</span></span>

<span data-ttu-id="fd097-116">U kunt de gatewayverbinding controleren.</span><span class="sxs-lookup"><span data-stu-id="fd097-116">You can verify your gateway connection.</span></span> <span data-ttu-id="fd097-117">Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fd097-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>