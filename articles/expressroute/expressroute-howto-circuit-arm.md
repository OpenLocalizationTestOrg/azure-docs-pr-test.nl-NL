---
title: 'Maken en een ExpressRoute-circuit wijzigen: PowerShell: Azure Resource Manager | Microsoft Docs'
description: Dit artikel wordt beschreven hoe toocreate, inrichten, controleren, bijwerken, verwijderen en een ExpressRoute-circuit inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="9d9dd-103">Maken en een ExpressRoute-circuit met PowerShell wijzigen</span><span class="sxs-lookup"><span data-stu-id="9d9dd-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d9dd-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9d9dd-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="9d9dd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d9dd-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="9d9dd-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="9d9dd-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="9d9dd-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9d9dd-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="9d9dd-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="9d9dd-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="9d9dd-109">Dit artikel wordt beschreven hoe toocreate een Azure ExpressRoute-circuit met behulp van PowerShell-cmdlets en hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="9d9dd-110">Dit artikel ziet u ook hoe toocheck Hallo status van het Hallo-circuit, bijwerken of verwijderen en deze inrichting ervan ongedaan.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9d9dd-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9d9dd-111">Before you begin</span></span>
* <span data-ttu-id="9d9dd-112">Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9d9dd-113">Zie voor meer informatie [overzicht van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d9dd-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="9d9dd-114">Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="9d9dd-115">Maken en een ExpressRoute-circuit inrichten</span><span class="sxs-lookup"><span data-stu-id="9d9dd-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="9d9dd-116">1. Meld u aan tooyour Azure-account en uw abonnement te selecteren</span><span class="sxs-lookup"><span data-stu-id="9d9dd-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="9d9dd-117">toobegin uw configuratie, aanmelden tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="9d9dd-118">Gebruik Hallo volgen voorbeelden toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9d9dd-119">Controleer Hallo abonnementen voor Hallo-account:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9d9dd-120">Hallo-abonnement dat u wilt dat een ExpressRoute-circuit voor toocreate selecteren:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="9d9dd-121">2. Hallo-lijst met ondersteunde providers, locaties en bandbreedten</span><span class="sxs-lookup"><span data-stu-id="9d9dd-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="9d9dd-122">Voordat u een ExpressRoute-circuit maken, moet u Hallo lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="9d9dd-123">PowerShell-cmdlet Hallo **Get-AzureRmExpressRouteServiceProvider** retourneert deze informatie, die u in latere stappen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="9d9dd-124">Controleer de toosee als uw connectiviteitsprovider daar wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="9d9dd-125">Noteer Hallo informatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-125">Make a note of hello following information.</span></span> <span data-ttu-id="9d9dd-126">U hebt deze later nodig bij het maken van een circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="9d9dd-127">Naam</span><span class="sxs-lookup"><span data-stu-id="9d9dd-127">Name</span></span>
* <span data-ttu-id="9d9dd-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="9d9dd-128">PeeringLocations</span></span>
* <span data-ttu-id="9d9dd-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="9d9dd-129">BandwidthsOffered</span></span>

<span data-ttu-id="9d9dd-130">U bent nu klaar toocreate een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="9d9dd-131">3. Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="9d9dd-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="9d9dd-132">Als u nog een resourcegroep hebt, moet u een maken voordat u uw ExpressRoute-circuit maken.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="9d9dd-133">U kunt dit doen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="9d9dd-134">Hallo volgende voorbeeld ziet u hoe toocreate een 200 Mbps-ExpressRoute-circuit via Equinix in Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="9d9dd-135">Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="9d9dd-136">Hallo Hier volgt een voorbeeld van de aanvraag voor een nieuwe servicesleutel:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="9d9dd-137">Zorg ervoor dat u de juiste SKU-laag Hallo en SKU-serie opgeeft:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="9d9dd-138">SKU-laag bepaalt of een standaard ExpressRoute of een premium-invoegtoepassing voor ExpressRoute is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="9d9dd-139">U kunt opgeven *standaard* tooget Hallo standaard SKU of *Premium* voor Hallo premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="9d9dd-140">SKU-serie, bepaalt Hallo facturering.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="9d9dd-141">U kunt opgeven *Metereddata* voor een plan datalimiet en *Unlimiteddata* voor een onbeperkte gegevens-plan.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="9d9dd-142">U kunt facturering type Hallo van wijzigen *Metereddata* te*Unlimiteddata*, maar niet Hallo type uit *Unlimiteddata* te*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="9d9dd-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d9dd-143">Uw ExpressRoute-circuit worden gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="9d9dd-144">Zorg ervoor dat u deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="9d9dd-145">Hallo-antwoord bevat de servicesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-145">hello response contains hello service key.</span></span> <span data-ttu-id="9d9dd-146">U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="9d9dd-147">4. Lijst van alle ExpressRoute-circuits</span><span class="sxs-lookup"><span data-stu-id="9d9dd-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="9d9dd-148">een lijst met alle Hallo ExpressRoute-circuits die u hebt gemaakt, tooget uitvoeren Hallo **Get-AzureRmExpressRouteCircuit** opdracht:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="9d9dd-149">Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-149">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="9d9dd-150">U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo `Get-AzureRmExpressRouteCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="9d9dd-151">Hallo aanroepen zonder parameters maken een lijst met alle Hallo-circuits.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="9d9dd-152">De sleutel van uw service wordt weergegeven in Hallo *ServiceKey* veld:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="9d9dd-153">Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-153">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="9d9dd-154">U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="9d9dd-155">5. Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden</span><span class="sxs-lookup"><span data-stu-id="9d9dd-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="9d9dd-156">*ServiceProviderProvisioningState* bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="9d9dd-157">Status biedt Hallo status op Hallo Microsoft aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="9d9dd-158">Zie voor meer informatie over het circuit inrichtingstatuswaarden hello [werkstromen](expressroute-workflows.md#expressroute-circuit-provisioning-states) artikel.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="9d9dd-159">Bij het maken van nieuwe ExpressRoute-circuit liggen Hallo circuit Hallo status te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="9d9dd-160">Hallo circuit verandert toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="9d9dd-161">Voor u toobe kunnen toouse een ExpressRoute-circuit, moet het Hallo status volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="9d9dd-162">6. Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren</span><span class="sxs-lookup"><span data-stu-id="9d9dd-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="9d9dd-163">Controle op Hallo status en status van Hallo circuit sleutel hello, laat u weten wanneer uw provider uw circuit is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="9d9dd-164">Nadat het Hallo-circuit is geconfigureerd, *ServiceProviderProvisioningState* wordt weergegeven als *ingericht*, zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="9d9dd-165">Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-165">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="9d9dd-166">7. Maken van uw configuratie van de routering</span><span class="sxs-lookup"><span data-stu-id="9d9dd-166">7. Create your routing configuration</span></span>
<span data-ttu-id="9d9dd-167">Zie voor stapsgewijze instructies Hallo [ExpressRoute-circuit routeringsconfiguratie](expressroute-howto-routing-arm.md) toocreate artikel en circuit peerings wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d9dd-168">Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="9d9dd-169">Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="9d9dd-170">8. Koppelen van een virtueel netwerk tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9d9dd-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="9d9dd-171">Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="9d9dd-172">Gebruik Hallo [tooExpressRoute circuits koppelt virtuele netwerken](expressroute-howto-linkvnet-arm.md) artikel als u met Hallo Resource Manager-implementatiemodel werkt.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="9d9dd-173">Hallo-status van een ExpressRoute-circuit ophalen</span><span class="sxs-lookup"><span data-stu-id="9d9dd-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="9d9dd-174">U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo **Get-AzureRmExpressRouteCircuit** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="9d9dd-175">Hallo aanroepen zonder parameters maken een lijst met alle Hallo-circuits.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="9d9dd-176">antwoord Hallo zijn vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-176">hello response will be similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="9d9dd-177">U kunt informatie over een specifieke ExpressRoute-circuit krijgen door Hallo Resourcegroepnaam en de naam van het circuit wordt doorgegeven als een aanroep van de parameter toohello:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="9d9dd-178">Hallo antwoord ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-178">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="9d9dd-179">U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="9d9dd-180"><a name="modify"></a>Wijzigen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9d9dd-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="9d9dd-181">U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="9d9dd-182">U kunt doen Hallo zonder uitvaltijd te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="9d9dd-183">In- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="9d9dd-184">Hallo-bandbreedte verhoging van uw ExpressRoute-circuit mits capaciteit beschikbaar op Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="9d9dd-185">Hallo bandbreedte van een circuit downgraden wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="9d9dd-186">Hallo softwarelicentiecontrole plan van gegevens Datalimiet tooUnlimited gegevens wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="9d9dd-187">Het wijzigen van Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="9d9dd-188">U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="9d9dd-189">Raadpleeg voor meer informatie over limieten en beperkingen toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9d9dd-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="9d9dd-190">tooenable hello ExpressRoute premium-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="9d9dd-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="9d9dd-191">U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit inschakelen met behulp van de volgende PowerShell-codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="9d9dd-192">Hallo circuit hebt nu Hallo ExpressRoute premium-invoegtoepassing voor functies die worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="9d9dd-193">We begint facturering voor Hallo premium-invoegtoepassing mogelijkheid zodra Hallo-opdracht met succes is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="9d9dd-194">toodisable hello ExpressRoute premium-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="9d9dd-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9d9dd-195">Deze bewerking kan mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="9d9dd-196">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-196">Note hello following:</span></span>

* <span data-ttu-id="9d9dd-197">Voordat u van premium toostandard downgraden, moet u ervoor zorgen dat virtuele netwerken die zijn gekoppeld, aantal Hallo toohello circuit is minder dan 10.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="9d9dd-198">Als u dit doet, uw aanvraag bijwerken mislukt en er worden kosten in rekening brengen volgens de premietarieven voor.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="9d9dd-199">U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="9d9dd-200">Als u dit doet, uw aanvraag bijwerken mislukt en er worden kosten in rekening brengen volgens de premietarieven voor.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="9d9dd-201">De routetabel moet minder dan 4000 routes voor persoonlijke peering.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="9d9dd-202">Uw tabel route is groter dan 4000 routes, Hallo BGP-sessie wordt neergezet als totdat Hallo aantal geadverteerde voorvoegsels daaronder 4.000 won't worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="9d9dd-203">U kunt Hallo-invoegtoepassing voor ExpressRoute premium voor een bestaand circuit Hallo uitschakelen met behulp van de volgende PowerShell-cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="9d9dd-204">bandbreedte tooupdate hello ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9d9dd-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="9d9dd-205">Controleer voor ondersteunde bandbreedte-opties voor uw provider Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9d9dd-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="9d9dd-206">U kunt de grootte die groter zijn dan de grootte van uw bestaande circuit Hallo verzamelen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d9dd-207">Mogelijk hebt u toorecreate hello ExpressRoute-circuit als er onvoldoende capaciteit op de bestaande poort Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="9d9dd-208">U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="9d9dd-209">U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="9d9dd-210">Downgraden bandbreedte, moet u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="9d9dd-211">Nadat u welke grootte die u nodig hebt besluiten, uw circuit Hallo opdracht tooresize volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="9d9dd-212">Uw circuit, wordt in de Microsoft-zijde Hallo worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="9d9dd-213">U moet contact opnemen uw connectiviteit provider tooupdate-configuraties van hun kant toomatch deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="9d9dd-214">Nadat u deze melding, beginnen wij u facturering voor Hallo bijgewerkt bandbreedte optie.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="9d9dd-215">toomove hello SKU van gecontroleerde toounlimited</span><span class="sxs-lookup"><span data-stu-id="9d9dd-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="9d9dd-216">U kunt Hallo SKU van een ExpressRoute-circuit wijzigen met behulp van de volgende PowerShell-codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="9d9dd-217">toocontrol toegang toohello klassieke en Resource Manager-omgevingen</span><span class="sxs-lookup"><span data-stu-id="9d9dd-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="9d9dd-218">Lees de instructies Hallo in [verplaatsen ExpressRoute-circuits vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9d9dd-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="9d9dd-219">Opheffen van inrichting en een ExpressRoute-circuit verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d9dd-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="9d9dd-220">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-220">Note hello following:</span></span>

* <span data-ttu-id="9d9dd-221">U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="9d9dd-222">Als deze bewerking is mislukt, controleert u toosee als er geen virtuele netwerken zijn gekoppeld toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="9d9dd-223">Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht** moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="9d9dd-224">We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="9d9dd-225">Als serviceprovider Hallo heeft gemaakt Hallo circuit (Hallo serviceprovider Inrichtingsstatus te is ingesteld**niet ingericht**) kunt u Hallo circuit verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d9dd-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="9d9dd-226">Hiermee stopt u facturering voor Hallo circuit</span><span class="sxs-lookup"><span data-stu-id="9d9dd-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="9d9dd-227">U kunt uw ExpressRoute-circuit verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="9d9dd-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d9dd-228">Next steps</span></span>

<span data-ttu-id="9d9dd-229">Nadat u het circuit hebt gemaakt, moet u Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d9dd-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="9d9dd-230">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9d9dd-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="9d9dd-231">Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9d9dd-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
