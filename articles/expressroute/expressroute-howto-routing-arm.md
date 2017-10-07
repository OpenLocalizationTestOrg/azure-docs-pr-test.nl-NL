---
title: 'Hoe tooconfigure routering (peering) voor een ExpressRoute-circuit: Resource Manager: PowerShell: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="02c6a-104">Maken en wijzigen van de peering voor een ExpressRoute-circuit met PowerShell</span><span class="sxs-lookup"><span data-stu-id="02c6a-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="02c6a-105">In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in Hallo Resource Manager-implementatiemodel met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02c6a-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="02c6a-106">U kunt ook controleren Hallo status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="02c6a-107">Als u wilt dat een andere methode toowork toouse met uw circuit, selecteert u een artikel in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="02c6a-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02c6a-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="02c6a-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="02c6a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02c6a-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="02c6a-110">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="02c6a-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="02c6a-111">Video - persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="02c6a-112">Video - openbare peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="02c6a-113">Video - Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="02c6a-114">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="02c6a-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="02c6a-115">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="02c6a-115">Configuration prerequisites</span></span>

* <span data-ttu-id="02c6a-116">U moet de meest recente versie Hallo van hello Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="02c6a-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="02c6a-117">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="02c6a-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="02c6a-118">Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) pagina hello [routeringsvereisten](expressroute-routing.md) pagina en Hallo [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="02c6a-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="02c6a-119">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="02c6a-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="02c6a-120">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="02c6a-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="02c6a-121">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo cmdlets in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="02c6a-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="02c6a-122">Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="02c6a-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="02c6a-123">Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.</span><span class="sxs-lookup"><span data-stu-id="02c6a-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02c6a-124">We momenteel doen nog geen peerings geconfigureerd door serviceproviders via Hallo service management portal.</span><span class="sxs-lookup"><span data-stu-id="02c6a-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="02c6a-125">Deze mogelijkheid zal binnenkort worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="02c6a-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="02c6a-126">Neem contact op met uw serviceprovider voordat u BGP-peerings configureert.</span><span class="sxs-lookup"><span data-stu-id="02c6a-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="02c6a-127">U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="02c6a-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="02c6a-128">U kunt peerings configureren in elke gewenste volgorde.</span><span class="sxs-lookup"><span data-stu-id="02c6a-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="02c6a-129">Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.</span><span class="sxs-lookup"><span data-stu-id="02c6a-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="02c6a-130">Persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-130">Azure private peering</span></span>

<span data-ttu-id="02c6a-131">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="02c6a-132">toocreate persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="02c6a-133">Importeer Hallo PowerShell-module voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="02c6a-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="02c6a-134">Moet u het meest recente PowerShell installer Hallo van installeren [PowerShell Gallery](http://www.powershellgallery.com/) en hello Azure Resource Manager-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="02c6a-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="02c6a-135">U moet toorun PowerShell als beheerder.</span><span class="sxs-lookup"><span data-stu-id="02c6a-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="02c6a-136">Importeer alle AzureRM.*-modules Hallo binnen Hallo bekende semantische versiebereik.</span><span class="sxs-lookup"><span data-stu-id="02c6a-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="02c6a-137">U kunt ook gewoon een bepaalde module binnen Hallo bekend bereik semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="02c6a-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="02c6a-138">Meld u aan tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="02c6a-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="02c6a-139">Selecteer Hallo abonnement u wilt dat toocreate ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="02c6a-140">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="02c6a-141">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="02c6a-142">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="02c6a-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="02c6a-143">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="02c6a-144">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="02c6a-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="02c6a-145">Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="02c6a-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="02c6a-146">Gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="02c6a-147">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-147">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="02c6a-148">Configureer persoonlijke Azure-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="02c6a-149">Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="02c6a-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="02c6a-150">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="02c6a-151">Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="02c6a-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="02c6a-152">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="02c6a-153">Hallo-subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="02c6a-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="02c6a-154">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="02c6a-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="02c6a-155">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="02c6a-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="02c6a-156">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="02c6a-156">AS number for peering.</span></span> <span data-ttu-id="02c6a-157">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="02c6a-158">U kunt een persoonlijk AS-nummer voor deze peering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="02c6a-159">Zorg dat u niet 65515 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="02c6a-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="02c6a-160">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="02c6a-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="02c6a-161">Gebruik Hallo voorbeeld tooconfigure Azure persoonlijke peering voor uw circuit te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="02c6a-162">Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="02c6a-163">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="02c6a-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="02c6a-164">tooview Azure persoonlijke peering details</span><span class="sxs-lookup"><span data-stu-id="02c6a-164">tooview Azure private peering details</span></span>

<span data-ttu-id="02c6a-165">U kunt configuratie-informatie krijgen met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="02c6a-166">tooupdate Azure configuratie van persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="02c6a-167">U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="02c6a-168">In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 100 too500 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="02c6a-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="02c6a-169">toodelete persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-169">toodelete Azure private peering</span></span>

<span data-ttu-id="02c6a-170">U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="02c6a-171">U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van Hallo ExpressRoute-circuit zijn voordat u dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="02c6a-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="02c6a-172">Openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-172">Azure public peering</span></span>

<span data-ttu-id="02c6a-173">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="02c6a-174">toocreate openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="02c6a-175">Importeer Hallo PowerShell-module voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="02c6a-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="02c6a-176">Moet u het meest recente PowerShell installer Hallo van installeren [PowerShell Gallery](http://www.powershellgallery.com/) en hello Azure Resource Manager-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="02c6a-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="02c6a-177">U moet toorun PowerShell als beheerder.</span><span class="sxs-lookup"><span data-stu-id="02c6a-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="02c6a-178">Importeer alle AzureRM.*-modules Hallo binnen Hallo bekende semantische versiebereik.</span><span class="sxs-lookup"><span data-stu-id="02c6a-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="02c6a-179">U kunt ook gewoon een bepaalde module binnen Hallo bekend bereik semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="02c6a-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="02c6a-180">Meld u aan tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="02c6a-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="02c6a-181">Selecteer Hallo abonnement u wilt dat toocreate ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="02c6a-182">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="02c6a-183">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="02c6a-184">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="02c6a-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="02c6a-185">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="02c6a-186">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="02c6a-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="02c6a-187">Controleer Hallo ExpressRoute-circuit tooensure is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="02c6a-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="02c6a-188">Gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="02c6a-189">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-189">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="02c6a-190">Configureer openbare Azure-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="02c6a-191">Zorg ervoor dat u de volgende informatie voordat u verder Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="02c6a-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="02c6a-192">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="02c6a-193">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="02c6a-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="02c6a-194">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="02c6a-195">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="02c6a-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="02c6a-196">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="02c6a-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="02c6a-197">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="02c6a-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="02c6a-198">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="02c6a-198">AS number for peering.</span></span> <span data-ttu-id="02c6a-199">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="02c6a-200">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="02c6a-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="02c6a-201">Hallo na voorbeeld tooconfigure openbare peering voor uw circuit Azure uitvoeren</span><span class="sxs-lookup"><span data-stu-id="02c6a-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="02c6a-202">Als u een MD5-hash toouse kiest, gebruikt u Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="02c6a-203">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="02c6a-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="02c6a-204">tooview Azure openbare peering details</span><span class="sxs-lookup"><span data-stu-id="02c6a-204">tooview Azure public peering details</span></span>

<span data-ttu-id="02c6a-205">U kunt met behulp van de volgende cmdlet Hallo configuratiedetails krijgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="02c6a-206">configuratie van openbare peering Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="02c6a-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="02c6a-207">U kunt elk deel van Hallo-configuratie met behulp van de volgende voorbeeld Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="02c6a-208">In dit voorbeeld wordt Hallo VLAN-ID van het circuit Hallo van 200 too600 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="02c6a-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="02c6a-209">toodelete openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-209">toodelete Azure public peering</span></span>

<span data-ttu-id="02c6a-210">U kunt de peeringconfiguratie verwijderen door het uitvoeren van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="02c6a-211">Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-211">Microsoft peering</span></span>

<span data-ttu-id="02c6a-212">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02c6a-213">Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Hallo Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="02c6a-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="02c6a-214">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="02c6a-215">Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="02c6a-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="02c6a-216">toocreate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="02c6a-217">Importeer Hallo PowerShell-module voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="02c6a-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="02c6a-218">Moet u het meest recente PowerShell installer Hallo van installeren [PowerShell Gallery](http://www.powershellgallery.com/) en hello Azure Resource Manager-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="02c6a-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="02c6a-219">U moet toorun PowerShell als beheerder.</span><span class="sxs-lookup"><span data-stu-id="02c6a-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="02c6a-220">Importeer alle AzureRM.*-modules Hallo binnen Hallo bekende semantische versiebereik.</span><span class="sxs-lookup"><span data-stu-id="02c6a-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="02c6a-221">U kunt ook gewoon een bepaalde module binnen Hallo bekend bereik semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="02c6a-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="02c6a-222">Meld u aan tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="02c6a-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="02c6a-223">Selecteer Hallo abonnement u wilt dat toocreate ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="02c6a-224">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="02c6a-225">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="02c6a-226">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="02c6a-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="02c6a-227">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="02c6a-228">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert, maar de configuratie met behulp van de volgende stappen Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="02c6a-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="02c6a-229">Controleer de ExpressRoute-circuit toomake Hallo is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="02c6a-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="02c6a-230">Gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="02c6a-231">Hallo-antwoord is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-231">hello response is similar toohello following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="02c6a-232">Configureer Microsoft-peering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="02c6a-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="02c6a-233">Zorg ervoor dat er Hallo volgende informatie voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="02c6a-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="02c6a-234">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="02c6a-235">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="02c6a-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="02c6a-236">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02c6a-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="02c6a-237">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="02c6a-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="02c6a-238">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="02c6a-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="02c6a-239">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="02c6a-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="02c6a-240">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="02c6a-240">AS number for peering.</span></span> <span data-ttu-id="02c6a-241">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="02c6a-242">Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie.</span><span class="sxs-lookup"><span data-stu-id="02c6a-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="02c6a-243">Alleen openbare IP-adresvoorvoegsels worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="02c6a-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="02c6a-244">Als u een reeks voorvoegsels toosend plant, kunt u een door komma's gescheiden lijst verzenden.</span><span class="sxs-lookup"><span data-stu-id="02c6a-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="02c6a-245">Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="02c6a-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="02c6a-246">**Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn ingeschreven toohello peering als getal, kunt u Hallo opgeven als getal toowhich ze zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="02c6a-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="02c6a-247">Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="02c6a-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="02c6a-248">**Optionele -** een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="02c6a-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="02c6a-249">Gebruik Hallo voorbeeld tooconfigure Microsoft-peering voor uw circuit te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="02c6a-250">details van tooget Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="02c6a-251">U kunt krijgen configuratiegegevens wilt weergeven Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02c6a-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="02c6a-252">configuratie van tooupdate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="02c6a-253">U kunt elk deel van Hallo-configuratie met Hallo volgt bijwerken:</span><span class="sxs-lookup"><span data-stu-id="02c6a-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="02c6a-254">toodelete Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="02c6a-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="02c6a-255">U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="02c6a-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="02c6a-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02c6a-256">Next steps</span></span>

<span data-ttu-id="02c6a-257">Volgende stap, [koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="02c6a-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="02c6a-258">Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).</span><span class="sxs-lookup"><span data-stu-id="02c6a-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="02c6a-259">Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).</span><span class="sxs-lookup"><span data-stu-id="02c6a-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="02c6a-260">Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="02c6a-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
