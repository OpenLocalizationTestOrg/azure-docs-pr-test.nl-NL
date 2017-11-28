---
title: 'Maken en een ExpressRoute-circuit aanpassen: Azure portal | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toocreate, inrichten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="82462-103">Maken en een ExpressRoute-circuit wijzigen</span><span class="sxs-lookup"><span data-stu-id="82462-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82462-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="82462-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="82462-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82462-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="82462-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="82462-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="82462-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="82462-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="82462-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="82462-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="82462-109">Dit artikel wordt beschreven hoe een Azure ExpressRoute-circuit met behulp van toocreate hello Azure portal en hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="82462-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="82462-110">volgende stappen uit ook Hallo ziet u hoe toocheck Hallo status van het Hallo-circuit, bijwerken of verwijderen en deze inrichting ervan ongedaan.</span><span class="sxs-lookup"><span data-stu-id="82462-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="82462-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="82462-111">Before you begin</span></span>
* <span data-ttu-id="82462-112">Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="82462-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="82462-113">Zorg ervoor dat u toegang toohello hebt [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82462-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="82462-114">Zorg ervoor dat u machtigingen toocreate nieuwe netwerkresources.</span><span class="sxs-lookup"><span data-stu-id="82462-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="82462-115">Neem contact op met uw accountbeheerder als u niet de juiste machtigingen Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="82462-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="82462-116">U kunt [Bekijk een video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) voordat u begint in volgorde toobetter Hallo stappen begrijpen.</span><span class="sxs-lookup"><span data-stu-id="82462-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="82462-117">Maken en een ExpressRoute-circuit inrichten</span><span class="sxs-lookup"><span data-stu-id="82462-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="82462-118">1. Meld u aan toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="82462-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="82462-119">Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="82462-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="82462-120">2. Een nieuwe ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="82462-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="82462-121">Uw ExpressRoute-circuit worden gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="82462-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="82462-122">Zorg ervoor dat u deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="82462-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="82462-123">U kunt een ExpressRoute-circuit maken door het selecteren van Hallo optie toocreate een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="82462-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="82462-124">Klik op **nieuw** > **Networking** > **ExpressRoute**, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="82462-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Een ExpressRoute-circuit maken](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="82462-126">Nadat u op **ExpressRoute**, ziet u Hallo **maken ExpressRoute-circuit** blade.</span><span class="sxs-lookup"><span data-stu-id="82462-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="82462-127">Wanneer u Hallo waarden op deze blade hebt ingevuld, zorg ervoor dat u opgeeft dat de juiste SKU-laag Hallo en gegevensmeters.</span><span class="sxs-lookup"><span data-stu-id="82462-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="82462-128">**Laag** bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="82462-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="82462-129">U kunt opgeven **standaard** tooget Hallo standaard SKU of **Premium** voor Hallo premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="82462-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="82462-130">**Gegevensmeters** bepaalt Hallo facturering type.</span><span class="sxs-lookup"><span data-stu-id="82462-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="82462-131">U kunt opgeven **Metered** voor een plan datalimiet en **onbeperkt** voor een onbeperkte gegevens-plan.</span><span class="sxs-lookup"><span data-stu-id="82462-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="82462-132">Houd er rekening mee dat u kunt facturering type Hallo van wijzigen **Metered** te**onbeperkt**, maar niet Hallo type uit **onbeperkt** te**Metered**.</span><span class="sxs-lookup"><span data-stu-id="82462-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Hallo SKU-laag en gegevensmeters configureren](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="82462-134">Zorg ervoor dat Hallo Peering locatie geeft Hallo [fysieke locatie](expressroute-locations.md) waar u peering met Microsoft.</span><span class="sxs-lookup"><span data-stu-id="82462-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="82462-135">Dit is **niet** gekoppeld te 'Locatie'-eigenschap die verwijst toohello Geografie waar hello Azure Network-Resource Provider zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="82462-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="82462-136">Hoewel ze niet zijn gerelateerd, is een goede gewoonte toochoose een Netwerkresourceprovider geografisch sluiten toohello Peering-locatie van het Hallo-circuit.</span><span class="sxs-lookup"><span data-stu-id="82462-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="82462-137">3. Weergave Hallo circuits en -eigenschappen</span><span class="sxs-lookup"><span data-stu-id="82462-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="82462-138">**Alle Hallo circuits weergeven**</span><span class="sxs-lookup"><span data-stu-id="82462-138">**View all hello circuits**</span></span>

<span data-ttu-id="82462-139">U vindt alle Hallo-circuits die u hebt gemaakt door te selecteren **alle resources** Hallo aan de linkerkant menu.</span><span class="sxs-lookup"><span data-stu-id="82462-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Weergave circuits](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="82462-141">**Hallo-eigenschappen weergeven**</span><span class="sxs-lookup"><span data-stu-id="82462-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Eigenschappen weergeven](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="82462-143">4. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden</span><span class="sxs-lookup"><span data-stu-id="82462-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="82462-144">Op deze blade **providerstatus** bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde.</span><span class="sxs-lookup"><span data-stu-id="82462-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="82462-145">**Status circuit** Hallo status biedt op Hallo Microsoft aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="82462-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="82462-146">Zie voor meer informatie over het circuit inrichtingstatuswaarden hello [werkstromen](expressroute-workflows.md#expressroute-circuit-provisioning-states) artikel.</span><span class="sxs-lookup"><span data-stu-id="82462-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="82462-147">Bij het maken van nieuwe ExpressRoute-circuit liggen Hallo circuit Hallo status te volgen:</span><span class="sxs-lookup"><span data-stu-id="82462-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="82462-148">Providerstatus: niet ingericht</span><span class="sxs-lookup"><span data-stu-id="82462-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="82462-149">Circuit status: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="82462-149">Circuit status: Enabled</span></span>

![Inrichting te initiëren](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="82462-151">Hallo circuit verandert toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:</span><span class="sxs-lookup"><span data-stu-id="82462-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="82462-152">Providerstatus: inrichting</span><span class="sxs-lookup"><span data-stu-id="82462-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="82462-153">Circuit status: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="82462-153">Circuit status: Enabled</span></span>

<span data-ttu-id="82462-154">Voor u toobe kunnen toouse een ExpressRoute-circuit, moet het Hallo status volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="82462-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="82462-155">Providerstatus: ingericht</span><span class="sxs-lookup"><span data-stu-id="82462-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="82462-156">Circuit status: ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="82462-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="82462-157">5. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren</span><span class="sxs-lookup"><span data-stu-id="82462-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="82462-158">U kunt weergeven Hallo-eigenschappen van het Hallo-circuit dat u geïnteresseerd bent in het door deze te selecteren.</span><span class="sxs-lookup"><span data-stu-id="82462-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="82462-159">Controleer Hallo **providerstatus** en zorg ervoor dat deze te verplaatst**ingericht** voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="82462-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Status van circuit en -provider](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="82462-161">6. Maken van uw configuratie van de routering</span><span class="sxs-lookup"><span data-stu-id="82462-161">6. Create your routing configuration</span></span>
<span data-ttu-id="82462-162">Raadpleeg voor stapsgewijze instructies toohello [ExpressRoute-circuit routeringsconfiguratie](expressroute-howto-routing-portal-resource-manager.md) toocreate artikel en circuit peerings wijzigen.</span><span class="sxs-lookup"><span data-stu-id="82462-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82462-163">Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="82462-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="82462-164">Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.</span><span class="sxs-lookup"><span data-stu-id="82462-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="82462-165">7. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="82462-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="82462-166">Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="82462-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="82462-167">Gebruik Hallo [tooExpressRoute circuits koppelt virtuele netwerken](expressroute-howto-linkvnet-arm.md) artikel als u met Hallo Resource Manager-implementatiemodel werkt.</span><span class="sxs-lookup"><span data-stu-id="82462-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="82462-168">Hallo-status van een ExpressRoute-circuit ophalen</span><span class="sxs-lookup"><span data-stu-id="82462-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="82462-169">U kunt de status van een circuit Hallo weergeven door deze te selecteren.</span><span class="sxs-lookup"><span data-stu-id="82462-169">You can view hello status of a circuit by selecting it.</span></span> 

![Status van een ExpressRoute-circuit](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="82462-171">Wijzigen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="82462-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="82462-172">U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="82462-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="82462-173">U kunt doen Hallo zonder uitvaltijd te volgen:</span><span class="sxs-lookup"><span data-stu-id="82462-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="82462-174">In- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="82462-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="82462-175">Hallo-bandbreedte verhoging van uw ExpressRoute-circuit mits capaciteit beschikbaar op Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="82462-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="82462-176">Houd er rekening mee dat Hallo bandbreedte van een circuit downgraden wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="82462-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="82462-177">Hallo softwarelicentiecontrole plan van gegevens Datalimiet tooUnlimited gegevens wijzigen.</span><span class="sxs-lookup"><span data-stu-id="82462-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="82462-178">Houd er rekening mee dat veranderende Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="82462-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="82462-179">U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.</span><span class="sxs-lookup"><span data-stu-id="82462-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="82462-180">Raadpleeg voor meer informatie over limieten en beperkingen toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="82462-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="82462-181">toomodify een ExpressRoute-circuit, klikt u op Hallo **configuratie** zoals weergegeven in onderstaande afbeelding ziet Hallo.</span><span class="sxs-lookup"><span data-stu-id="82462-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Circuit wijzigen](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="82462-183">U kunt Hallo bandbreedte, SKU, factureringsmodel wijzigen en kunnen klassieke bewerkingen binnen Hallo configuratie blade.</span><span class="sxs-lookup"><span data-stu-id="82462-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82462-184">Mogelijk hebt u toorecreate hello ExpressRoute-circuit als er onvoldoende capaciteit op de bestaande poort Hallo.</span><span class="sxs-lookup"><span data-stu-id="82462-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="82462-185">U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.</span><span class="sxs-lookup"><span data-stu-id="82462-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="82462-186">U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren.</span><span class="sxs-lookup"><span data-stu-id="82462-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="82462-187">Downgraden bandbreedte, moet u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="82462-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="82462-188">Premium-invoegtoepassing uit te schakelen kunnen mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="82462-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="82462-189">Opheffen van inrichting en een ExpressRoute-circuit verwijderen</span><span class="sxs-lookup"><span data-stu-id="82462-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="82462-190">U kunt uw ExpressRoute-circuit verwijderen door het selecteren van Hallo **verwijderen** pictogram.</span><span class="sxs-lookup"><span data-stu-id="82462-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="82462-191">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="82462-191">Note hello following:</span></span>

* <span data-ttu-id="82462-192">U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="82462-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="82462-193">Als deze bewerking is mislukt, controleert u of er geen virtuele netwerken zijn gekoppeld toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="82462-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="82462-194">Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht** moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant.</span><span class="sxs-lookup"><span data-stu-id="82462-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="82462-195">We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.</span><span class="sxs-lookup"><span data-stu-id="82462-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="82462-196">Als serviceprovider Hallo heeft gemaakt Hallo circuit (Hallo serviceprovider Inrichtingsstatus te is ingesteld**niet ingericht**) kunt u Hallo circuit verwijderen.</span><span class="sxs-lookup"><span data-stu-id="82462-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="82462-197">Hiermee stopt u facturering voor Hallo circuit</span><span class="sxs-lookup"><span data-stu-id="82462-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="82462-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82462-198">Next steps</span></span>
<span data-ttu-id="82462-199">Nadat u het circuit hebt gemaakt, moet u Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="82462-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="82462-200">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="82462-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="82462-201">Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="82462-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

