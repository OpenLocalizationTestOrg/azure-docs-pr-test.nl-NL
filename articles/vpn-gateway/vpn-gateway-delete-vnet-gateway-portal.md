---
title: 'Verwijderen van een virtuele netwerkgateway: Azure-portal: Resource Manager | Microsoft Docs'
description: Verwijder de gateway van een virtueel netwerk met behulp van de Azure-portal in het Resource Manager-implementatiemodel.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="c46a7-103">Verwijder de gateway van een virtueel netwerk met behulp van de portal</span><span class="sxs-lookup"><span data-stu-id="c46a7-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c46a7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c46a7-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="c46a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c46a7-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="c46a7-106">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="c46a7-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="c46a7-107">Er zijn verschillende manieren die kunt u uw als u wilt verwijderen van een virtuele netwerkgateway voor de configuratie van een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="c46a7-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="c46a7-108">Als u wilt Alles verwijderen en opnieuw beginnen, zoals in het geval van een testomgeving kunt u de resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="c46a7-109">Wanneer u een resourcegroep verwijdert, worden alle resources binnen de groep verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c46a7-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="c46a7-110">Deze methode is wordt alleen aanbevolen als u niet wilt dat de bronnen in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c46a7-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="c46a7-111">U kunt alleen een aantal bronnen met deze benadering selectief niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="c46a7-112">Als u wilt dat een aantal van de resources in de resourcegroep, verwijderen van een virtuele netwerkgateway enigszins iets gecompliceerder.</span><span class="sxs-lookup"><span data-stu-id="c46a7-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="c46a7-113">Voordat u de virtuele netwerkgateway verwijderen kunt, moet u eerst alle bronnen die afhankelijk van de gateway zijn te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="c46a7-114">De stappen die u volgt, is afhankelijk van het type van de verbindingen die u hebt gemaakt en de afhankelijke resources voor elke verbinding.</span><span class="sxs-lookup"><span data-stu-id="c46a7-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="c46a7-115">Een VPN-gateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46a7-115">Delete a VPN gateway</span></span>

<span data-ttu-id="c46a7-116">Als u wilt verwijderen van een virtuele netwerkgateway, moet u eerst elke bron die betrekking op de virtuele netwerkgateway hebben verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="c46a7-117">Resources moeten worden verwijderd in een bepaalde volgorde vanwege afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="c46a7-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="c46a7-118">Op dit punt wordt wordt de virtuele netwerkgateway verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c46a7-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="c46a7-119">De volgende stappen kunt u alle resources verwijderen die niet langer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c46a7-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="c46a7-120">De lokale netwerkgateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46a7-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="c46a7-121">In **alle resources**, Ga naar de lokale netwerkgateways die gekoppeld aan elke verbinding zijn.</span><span class="sxs-lookup"><span data-stu-id="c46a7-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="c46a7-122">Op de **overzicht** blade voor de lokale netwerkgateway, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="c46a7-123">De bron van de openbare IP-adres voor de gateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46a7-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="c46a7-124">In **alle resources**, de bron van openbare IP-adres dat gekoppeld aan de gateway is gevonden.</span><span class="sxs-lookup"><span data-stu-id="c46a7-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="c46a7-125">Als de virtuele netwerkgateway actief-actief is, ziet u twee openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="c46a7-126">Op de **overzicht** pagina voor het openbare IP-adres, klikt u op **verwijderen**, klikt u vervolgens **Ja** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="c46a7-127">Het gatewaysubnet verwijderen</span><span class="sxs-lookup"><span data-stu-id="c46a7-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="c46a7-128">In **alle resources**, zoek het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c46a7-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="c46a7-129">Op de **subnetten** blade, klikt u op de **GatewaySubnet**, klikt u vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="c46a7-130">Klik op **Ja** om te bevestigen dat u wilt verwijderen van het gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="c46a7-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="c46a7-131"><a name="deleterg"></a>Een VPN-gateway verwijderen door het verwijderen van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="c46a7-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="c46a7-132">Als u zich geen zorgen over het houden van uw resources in de resourcegroep en u wilt beginnen, kunt u een hele resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="c46a7-133">Dit is een snelle manier om alles verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="c46a7-134">De volgende stappen gelden alleen voor het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="c46a7-135">In **alle resources**, zoek de resourcegroep en klik op om de blade te openen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="c46a7-136">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-136">Click **Delete**.</span></span> <span data-ttu-id="c46a7-137">Bekijk de betrokken bronnen op de blade verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c46a7-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="c46a7-138">Zorg ervoor dat u wilt verwijderen van al deze resources.</span><span class="sxs-lookup"><span data-stu-id="c46a7-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="c46a7-139">Als dit niet het geval is, gebruik de stappen in [verwijderen van een VPN-gateway](#deletegw) boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c46a7-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="c46a7-140">Typ de naam van de resourcegroep die u wilt verwijderen en klik vervolgens op om door te gaan **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c46a7-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>