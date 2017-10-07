---
title: 'Toevoegen van meerdere VPN-gateway Site-naar-Site-verbindingen tooa VNet: Azure-Portal: Resource Manager | Microsoft Docs'
description: Toevoegen van meerdere sites S2S-verbindingen tooa VPN-gateway met een bestaande verbinding
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="84486-103">Toevoegen van een Site-naar-Site-verbinding tooa VNet met een bestaande VPN-gateway-verbinding</span><span class="sxs-lookup"><span data-stu-id="84486-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84486-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="84486-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="84486-105">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="84486-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="84486-106">Dit artikel begeleidt u bij hello Azure portal tooadd Site-naar-Site (S2S)-verbindingen tooa VPN-gateway met een bestaande verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="84486-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="84486-107">Dit type verbinding is vaak waarnaar wordt verwezen tooas een 'multi-site'-configuratie.</span><span class="sxs-lookup"><span data-stu-id="84486-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="84486-108">U kunt een S2S-verbinding tooa VNet waarop al een S2S-verbinding, een punt-naar-Site-verbinding of een VNet-naar-VNet-verbinding toevoegen.</span><span class="sxs-lookup"><span data-stu-id="84486-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="84486-109">Er zijn enkele beperkingen bij het toevoegen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="84486-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="84486-110">Controleer de Hallo [voordat u begint met](#before) sectie in dit artikel tooverify voordat u uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="84486-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="84486-111">In dit artikel van toepassing is gemaakt met Resource Manager-implementatiemodel Hallo tooVNets waarvoor een RouteBased VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="84486-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="84486-112">Deze stappen zijn niet van toepassing tooExpressRoute/Site-naar-Site naast elkaar bestaande verbinding configuraties.</span><span class="sxs-lookup"><span data-stu-id="84486-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="84486-113">Zie [ExpressRoute/S2S naast elkaar bestaande verbindingen](../expressroute/expressroute-howto-coexist-resource-manager.md) voor informatie over naast elkaar bestaande verbindingen.</span><span class="sxs-lookup"><span data-stu-id="84486-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="84486-114">Implementatiemodellen en -methoden</span><span class="sxs-lookup"><span data-stu-id="84486-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="84486-115">Deze tabel wordt bijgewerkt als er nieuwe artikelen en aanvullende hulpprogramma's beschikbaar zijn voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="84486-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="84486-116">Wanneer een artikel beschikbaar is, koppelen we rechtstreeks tooit uit deze tabel.</span><span class="sxs-lookup"><span data-stu-id="84486-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="84486-117"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="84486-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="84486-118">Controleer of de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="84486-118">Verify hello following items:</span></span>

* <span data-ttu-id="84486-119">Geen maakt u een ExpressRoute/S2S naast elkaar bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="84486-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="84486-120">U hebt een virtueel netwerk dat is gemaakt met de Hallo Resource Manager-implementatiemodel met een bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="84486-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="84486-121">de virtuele netwerkgateway Hallo voor uw VNet is RouteBased.</span><span class="sxs-lookup"><span data-stu-id="84486-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="84486-122">Als u een PolicyBased VPN-gateway hebt, moet u Hallo virtuele netwerkgateway verwijderen en maak een nieuwe VPN-gateway als RouteBased.</span><span class="sxs-lookup"><span data-stu-id="84486-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="84486-123">Geen Hallo-adresbereiken voor een van de VNets die dit VNet verbinding met maakt Hallo niet overlappen.</span><span class="sxs-lookup"><span data-stu-id="84486-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="84486-124">U hebt compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze.</span><span class="sxs-lookup"><span data-stu-id="84486-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="84486-125">Zie [About VPN Devices](vpn-gateway-about-vpn-devices.md) (Over VPN-apparaten).</span><span class="sxs-lookup"><span data-stu-id="84486-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="84486-126">Als u niet bekend bent met het configureren van uw VPN-apparaat of niet bekend met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie bent, moet u toocoordinate met iemand die deze details voor u verstrekken kan.</span><span class="sxs-lookup"><span data-stu-id="84486-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="84486-127">U hebt een extern gericht openbaar IP-adres voor uw VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="84486-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="84486-128">Dit IP-adres kan zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="84486-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="84486-129"><a name="part1"></a>Deel 1: een verbinding configureren</span><span class="sxs-lookup"><span data-stu-id="84486-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="84486-130">Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en, indien nodig, meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="84486-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="84486-131">Klik op **alle resources** en zoek uw **virtuele netwerkgateway** uit Hallo lijst met resources en klik erop.</span><span class="sxs-lookup"><span data-stu-id="84486-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="84486-132">Op Hallo **virtuele netwerkgateway** blade, klikt u op **verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="84486-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="84486-133">![Blade Verbindingen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Blade Verbindingen")</span><span class="sxs-lookup"><span data-stu-id="84486-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="84486-134">Op Hallo **verbindingen** blade, klikt u op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84486-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="84486-135">![De knop verbinding toevoegen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "de knop verbinding toevoegen")</span><span class="sxs-lookup"><span data-stu-id="84486-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="84486-136">Op Hallo **verbinding toevoegen** blade Vul Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="84486-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="84486-137">**Naam:** gewenste toogive toohello site die u verbinding met Hallo maakt Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="84486-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="84486-138">**Verbindingstype:** Selecteer **Site-naar-site (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="84486-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="84486-139">![Tabblad van de verbinding toevoegen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "verbinding-tabblad toevoegen")</span><span class="sxs-lookup"><span data-stu-id="84486-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="84486-140"><a name="part2"></a>Deel 2: een lokale netwerkgateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="84486-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="84486-141">Klik op **lokale netwerkgateway** ***een lokale netwerkgateway kiezen***.</span><span class="sxs-lookup"><span data-stu-id="84486-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="84486-142">Hiermee opent u Hallo **de lokale netwerkgateway kiezen** blade.</span><span class="sxs-lookup"><span data-stu-id="84486-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="84486-143">![De lokale netwerkgateway kiezen](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "de lokale netwerkgateway kiezen")</span><span class="sxs-lookup"><span data-stu-id="84486-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="84486-144">Klik op **nieuw** tooopen hello **de lokale netwerkgateway maken** blade.</span><span class="sxs-lookup"><span data-stu-id="84486-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="84486-145">![Blade lokale netwerkgateway maken](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "de lokale netwerkgateway maken")</span><span class="sxs-lookup"><span data-stu-id="84486-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="84486-146">Op Hallo **de lokale netwerkgateway maken** blade Vul Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="84486-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="84486-147">**Naam:** gewenste toogive toohello lokale gateway netwerkbron Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="84486-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="84486-148">**IP-adres:** Hallo openbaar IP-adres van VPN-apparaat Hallo op Hallo-site die u wilt dat tooconnect naar.</span><span class="sxs-lookup"><span data-stu-id="84486-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="84486-149">**Adresruimte:** Hallo-adresruimte die u wilt dat toobe toohello nieuwe lokale netwerksite gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="84486-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="84486-150">Klik op **OK** op Hallo **de lokale netwerkgateway maken** blade toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="84486-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="84486-151"><a name="part3"></a>Deel 3: Hallo gedeelde sleutel toevoegen en Hallo verbinding maken</span><span class="sxs-lookup"><span data-stu-id="84486-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="84486-152">Op Hallo **verbinding toevoegen** blade Hallo gedeelde sleutel die u wilt dat toouse toocreate uw verbinding toevoegen.</span><span class="sxs-lookup"><span data-stu-id="84486-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="84486-153">U kunt gedeelde sleutel Hallo ophalen van uw VPN-apparaat, of een hier en configureer vervolgens uw VPN-apparaat toouse Hallo dezelfde gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="84486-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="84486-154">Hallo belangrijk ding wordt Hallo sleutels zijn exact Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="84486-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="84486-155">![Gedeelde sleutel](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Gedeelde sleutel")</span><span class="sxs-lookup"><span data-stu-id="84486-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="84486-156">Hallo onderaan de blade hello, klikt u op **OK** toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="84486-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="84486-157"><a name="part4"></a>Deel 4 – Hallo VPN-verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="84486-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="84486-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84486-158">Next steps</span></span>

<span data-ttu-id="84486-159">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="84486-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="84486-160">Zie Hallo virtuele machines [leertraject](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="84486-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
