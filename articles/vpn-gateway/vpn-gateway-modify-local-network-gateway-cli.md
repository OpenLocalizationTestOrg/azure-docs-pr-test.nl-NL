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
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="b2e0c-103">Lokale gateway netwerkinstellingen wijzigen met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b2e0c-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="b2e0c-104">Soms Hallo-instellingen voor uw lokale netwerkgateway adresvoorvoegsel of IP-adres Gateway worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b2e0c-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="b2e0c-105">Dit artikel ziet u hoe toomodify gateway-instellingen van uw lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="b2e0c-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="b2e0c-106">U kunt deze instellingen met een andere methode door een andere optie selecteren in lijst na Hallo ook wijzigen:</span><span class="sxs-lookup"><span data-stu-id="b2e0c-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2e0c-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b2e0c-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="b2e0c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2e0c-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="b2e0c-109">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="b2e0c-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="b2e0c-110"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b2e0c-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="b2e0c-111">Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger).</span><span class="sxs-lookup"><span data-stu-id="b2e0c-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="b2e0c-112">Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2e0c-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="b2e0c-113"><a name="ipaddprefix"></a>IP-adresvoorvoegsels wijzigen</span><span class="sxs-lookup"><span data-stu-id="b2e0c-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="b2e0c-114"><a name="gwip"></a>Hallo gateway IP-adres wijzigen</span><span class="sxs-lookup"><span data-stu-id="b2e0c-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b2e0c-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2e0c-115">Next steps</span></span>

<span data-ttu-id="b2e0c-116">U kunt de gatewayverbinding controleren.</span><span class="sxs-lookup"><span data-stu-id="b2e0c-116">You can verify your gateway connection.</span></span> <span data-ttu-id="b2e0c-117">Zie [een gatewayverbinding controleren](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b2e0c-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

