---
title: 'Het configureren van routering (peering) voor een ExpressRoute-circuit: Resource Manager: PowerShell: Azure | Microsoft Docs'
description: Dit artikel begeleidt u stapsgewijs door de procedure voor het maken en inrichten van de persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. In dit artikel leest u hoe u de status controleert en peerings voor uw circuit bijwerkt of verwijdert.
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
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="aa402-104">Maken en wijzigen van de peering voor een ExpressRoute-circuit met PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa402-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="aa402-105">In dit artikel helpt u bij het maken en beheren van routeringsconfiguratie voor een ExpressRoute-circuit in het Resource Manager-implementatiemodel met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa402-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="aa402-106">U kunt ook controleren van de status, update of delete en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="aa402-107">Als u een andere methode gebruiken om te werken met uw circuit wilt, selecteert u een artikel uit de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="aa402-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa402-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aa402-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="aa402-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa402-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="aa402-110">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="aa402-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="aa402-111">Video - persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="aa402-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aa402-112">Video - openbare peering</span><span class="sxs-lookup"><span data-stu-id="aa402-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aa402-113">Video - Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="aa402-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aa402-114">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="aa402-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="aa402-115">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="aa402-115">Configuration prerequisites</span></span>

* <span data-ttu-id="aa402-116">U moet de meest recente versie van de Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="aa402-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="aa402-117">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aa402-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="aa402-118">Zorg dat u de pagina met [vereisten](expressroute-prerequisites.md), de pagina over [routeringsvereisten](expressroute-routing.md) en de pagina over [werkstromen](expressroute-workflows.md) hebt gelezen voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="aa402-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="aa402-119">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="aa402-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="aa402-120">Volg de instructies voor het [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="aa402-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="aa402-121">Het ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld om te kunnen uitvoeren van de cmdlets in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="aa402-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="aa402-122">Deze instructies zijn alleen van toepassing op circuits die zijn gemaakt met serviceproviders die services met Laag-2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="aa402-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="aa402-123">Als u gebruikmaakt van een serviceprovider die beheerde laag-3-services (meestal een IPVPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.</span><span class="sxs-lookup"><span data-stu-id="aa402-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa402-124">Op dit moment bieden we nog geen peerings aan die door serviceproviders worden geconfigureerd via de beheerportal van de service.</span><span class="sxs-lookup"><span data-stu-id="aa402-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="aa402-125">Deze mogelijkheid zal binnenkort worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aa402-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="aa402-126">Neem contact op met uw serviceprovider voordat u BGP-peerings configureert.</span><span class="sxs-lookup"><span data-stu-id="aa402-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="aa402-127">U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="aa402-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="aa402-128">U kunt peerings configureren in elke gewenste volgorde.</span><span class="sxs-lookup"><span data-stu-id="aa402-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="aa402-129">U moet er echter wel voor zorgen dat u de configuratie van elke peering een voor een voltooit.</span><span class="sxs-lookup"><span data-stu-id="aa402-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="aa402-130">Persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="aa402-130">Azure private peering</span></span>

<span data-ttu-id="aa402-131">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van de Azure persoonlijke peering configuratie voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="aa402-132">Persoonlijke Azure-peering maken</span><span class="sxs-lookup"><span data-stu-id="aa402-132">To create Azure private peering</span></span>

1. <span data-ttu-id="aa402-133">Importeer de PowerShell-module voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aa402-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="aa402-134">U moet het meest recente installatieprogramma installeren vanuit de [PowerShell Gallery](http://www.powershellgallery.com/) en de Azure Resource Manager-modules importeren in de PowerShell-sessie om de ExpressRoute-cmdlets te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="aa402-135">U moet PowerShell tevens uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aa402-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="aa402-136">Alle AzureRM.*-modules binnen het bereik van de bekende semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="aa402-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="aa402-137">U kunt ook gewoon een bepaalde module binnen het bereik van de bekende semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="aa402-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="aa402-138">Aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="aa402-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="aa402-139">Selecteer het abonnement dat u wilt maken van ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="aa402-140">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="aa402-141">Volg de instructies voor het [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het circuit inrichten door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="aa402-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="aa402-142">Als uw connectiviteitsprovider beheerde Laag-3-services biedt, kunt u de connectiviteitsprovider vragen om persoonlijke Azure-peering voor u in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="aa402-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aa402-143">In dat geval hoeft u de instructies in de volgende secties niet te volgen.</span><span class="sxs-lookup"><span data-stu-id="aa402-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aa402-144">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert blijven echter uw configuratie met behulp van de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="aa402-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="aa402-145">Controleer het ExpressRoute-circuit is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aa402-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="aa402-146">Gebruik het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="aa402-147">Het antwoord is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-147">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="aa402-148">Configureer persoonlijke Azure-peering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="aa402-149">Zorg ervoor dat u de volgende items hebt voordat u verdergaat met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="aa402-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="aa402-150">Een /30-subnet voor de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="aa402-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aa402-151">Het subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="aa402-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="aa402-152">Een /30-subnet voor de secundaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="aa402-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aa402-153">Het subnet moet deel uitmaken van een adresruimte gereserveerd voor virtuele netwerken niet.</span><span class="sxs-lookup"><span data-stu-id="aa402-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="aa402-154">Een geldige VLAN-id waarop u deze peering wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="aa402-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aa402-155">Controleer of er geen andere peering in het circuit is die dezelfde VLAN-id gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa402-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="aa402-156">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="aa402-156">AS number for peering.</span></span> <span data-ttu-id="aa402-157">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="aa402-158">U kunt een persoonlijk AS-nummer voor deze peering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="aa402-159">Zorg dat u niet 65515 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa402-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="aa402-160">**Optionele -** een MD5-hash, als u ervoor kiest een te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="aa402-161">Gebruik het volgende voorbeeld voor het configureren van persoonlijke Azure-peering voor uw circuit:</span><span class="sxs-lookup"><span data-stu-id="aa402-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="aa402-162">Als u gebruiken een MD5-hash wilt, gebruikt u het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="aa402-163">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="aa402-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="aa402-164">De details van persoonlijke Azure-peering weergeven</span><span class="sxs-lookup"><span data-stu-id="aa402-164">To view Azure private peering details</span></span>

<span data-ttu-id="aa402-165">U kunt configuratie-informatie krijgen met behulp van het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="aa402-166">De configuratie van persoonlijke Azure-peering bijwerken</span><span class="sxs-lookup"><span data-stu-id="aa402-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="aa402-167">U kunt elk deel van de configuratie in het volgende voorbeeld bijwerken.</span><span class="sxs-lookup"><span data-stu-id="aa402-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="aa402-168">In dit voorbeeld wordt de VLAN-ID van het circuit wordt bijgewerkt van 100 tot 500.</span><span class="sxs-lookup"><span data-stu-id="aa402-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="aa402-169">Persoonlijke Azure-peering verwijderen</span><span class="sxs-lookup"><span data-stu-id="aa402-169">To delete Azure private peering</span></span>

<span data-ttu-id="aa402-170">U kunt de peeringconfiguratie verwijderen door het uitvoeren van het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="aa402-171">U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van het ExpressRoute-circuit zijn voordat u dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="aa402-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="aa402-172">Openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="aa402-172">Azure public peering</span></span>

<span data-ttu-id="aa402-173">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van de Azure openbare peering configuratie voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="aa402-174">Openbare Azure-peering maken</span><span class="sxs-lookup"><span data-stu-id="aa402-174">To create Azure public peering</span></span>

1. <span data-ttu-id="aa402-175">Importeer de PowerShell-module voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aa402-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="aa402-176">U moet het meest recente installatieprogramma installeren vanuit de [PowerShell Gallery](http://www.powershellgallery.com/) en de Azure Resource Manager-modules importeren in de PowerShell-sessie om de ExpressRoute-cmdlets te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="aa402-177">U moet PowerShell tevens uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aa402-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="aa402-178">Alle AzureRM.*-modules binnen het bereik van de bekende semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="aa402-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="aa402-179">U kunt ook gewoon een bepaalde module binnen het bereik van de bekende semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="aa402-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="aa402-180">Aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="aa402-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="aa402-181">Selecteer het abonnement dat u wilt maken van ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="aa402-182">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="aa402-183">Volg de instructies voor het [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het circuit inrichten door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="aa402-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="aa402-184">Als uw connectiviteitsprovider beheerde Laag-3-services biedt, kunt u de connectiviteitsprovider vragen om persoonlijke Azure-peering voor u in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="aa402-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aa402-185">In dat geval hoeft u de instructies in de volgende secties niet te volgen.</span><span class="sxs-lookup"><span data-stu-id="aa402-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aa402-186">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert blijven echter uw configuratie met behulp van de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="aa402-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="aa402-187">Controleer of de ExpressRoute circuit is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aa402-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="aa402-188">Gebruik het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="aa402-189">Het antwoord is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-189">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="aa402-190">Configureer openbare Azure-peering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="aa402-191">Zorg ervoor dat u hebt de volgende informatie beschikt voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="aa402-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="aa402-192">Een /30-subnet voor de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="aa402-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aa402-193">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="aa402-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="aa402-194">Een /30-subnet voor de secundaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="aa402-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aa402-195">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="aa402-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="aa402-196">Een geldige VLAN-id waarop u deze peering wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="aa402-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aa402-197">Controleer of er geen andere peering in het circuit is die dezelfde VLAN-id gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa402-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="aa402-198">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="aa402-198">AS number for peering.</span></span> <span data-ttu-id="aa402-199">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="aa402-200">**Optionele -** een MD5-hash, als u ervoor kiest een te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="aa402-201">Het volgende voorbeeld voor het configureren van openbare Azure-peering voor uw circuit uitvoert</span><span class="sxs-lookup"><span data-stu-id="aa402-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="aa402-202">Als u gebruiken een MD5-hash wilt, gebruikt u het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="aa402-203">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="aa402-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="aa402-204">De details van openbare Azure-peering weergeven</span><span class="sxs-lookup"><span data-stu-id="aa402-204">To view Azure public peering details</span></span>

<span data-ttu-id="aa402-205">U kunt met de volgende cmdlet configuratiedetails krijgen:</span><span class="sxs-lookup"><span data-stu-id="aa402-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="aa402-206">De configuratie van openbare Azure-peering bijwerken</span><span class="sxs-lookup"><span data-stu-id="aa402-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="aa402-207">U kunt elk deel van de configuratie in het volgende voorbeeld bijwerken.</span><span class="sxs-lookup"><span data-stu-id="aa402-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="aa402-208">In dit voorbeeld wordt wordt de VLAN-ID van het circuit van 200 bijgewerkt op 600.</span><span class="sxs-lookup"><span data-stu-id="aa402-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="aa402-209">Openbare Azure-peering verwijderen</span><span class="sxs-lookup"><span data-stu-id="aa402-209">To delete Azure public peering</span></span>

<span data-ttu-id="aa402-210">U kunt de peeringconfiguratie verwijderen door het uitvoeren van het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="aa402-211">Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="aa402-211">Microsoft peering</span></span>

<span data-ttu-id="aa402-212">Deze sectie helpt u bij het maken, verkrijgen, bijwerken en verwijderen van de configuratie voor de Microsoft-peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa402-213">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, voordat u 1 augustus 2017 hebben alle service voorvoegsels die worden geadverteerd via de Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="aa402-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="aa402-214">Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter is gekoppeld aan het circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="aa402-215">Zie voor meer informatie [configureren van een routefilter voor Microsoft-peering](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aa402-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="aa402-216">Microsoft-peering maken</span><span class="sxs-lookup"><span data-stu-id="aa402-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="aa402-217">Importeer de PowerShell-module voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aa402-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="aa402-218">U moet het meest recente installatieprogramma installeren vanuit de [PowerShell Gallery](http://www.powershellgallery.com/) en de Azure Resource Manager-modules importeren in de PowerShell-sessie om de ExpressRoute-cmdlets te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="aa402-219">U moet PowerShell tevens uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aa402-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="aa402-220">Alle AzureRM.*-modules binnen het bereik van de bekende semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="aa402-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="aa402-221">U kunt ook gewoon een bepaalde module binnen het bereik van de bekende semantische versie importeren.</span><span class="sxs-lookup"><span data-stu-id="aa402-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="aa402-222">Aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="aa402-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="aa402-223">Selecteer het abonnement dat u wilt maken van ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="aa402-224">Maak een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="aa402-225">Volg de instructies voor het [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat het circuit inrichten door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="aa402-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="aa402-226">Als uw connectiviteitsprovider beheerde Laag-3-services biedt, kunt u de connectiviteitsprovider vragen om persoonlijke Azure-peering voor u in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="aa402-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aa402-227">In dat geval hoeft u de instructies in de volgende secties niet te volgen.</span><span class="sxs-lookup"><span data-stu-id="aa402-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aa402-228">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert blijven echter uw configuratie met behulp van de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="aa402-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="aa402-229">Controleer het ExpressRoute-circuit is ingericht en ook ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aa402-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="aa402-230">Gebruik het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="aa402-231">Het antwoord is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-231">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="aa402-232">Configureer Microsoft-peering voor het circuit.</span><span class="sxs-lookup"><span data-stu-id="aa402-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="aa402-233">Zorg ervoor dat u over de volgende informatie beschikt voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="aa402-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="aa402-234">Een /30-subnet voor de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="aa402-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aa402-235">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="aa402-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="aa402-236">Een /30-subnet voor de secundaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="aa402-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aa402-237">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="aa402-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="aa402-238">Een geldige VLAN-id waarop u deze peering wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="aa402-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aa402-239">Controleer of er geen andere peering in het circuit is die dezelfde VLAN-id gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa402-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="aa402-240">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="aa402-240">AS number for peering.</span></span> <span data-ttu-id="aa402-241">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="aa402-242">Geadverteerde voorvoegsels: u moet een lijst verstrekken van alle voorvoegsels die u via de BGP-sessie wilt adverteren.</span><span class="sxs-lookup"><span data-stu-id="aa402-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="aa402-243">Alleen openbare IP-adresvoorvoegsels worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="aa402-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="aa402-244">Als u van plan bent een reeks voorvoegsels verzenden, kunt u een door komma's gescheiden lijst verzenden.</span><span class="sxs-lookup"><span data-stu-id="aa402-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="aa402-245">Deze voorvoegsels moeten voor u zijn geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="aa402-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="aa402-246">**Optionele -** klant-ASN: als u voorvoegsels adverteert die niet zijn geregistreerd op de AS-nummer peering, kunt u het AS-nummer waaraan ze zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="aa402-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="aa402-247">Naam van routeringsregister: u kunt het RIR/IRR opgeven waarbij het AS-nummer en de voorvoegsels zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="aa402-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="aa402-248">**Optionele -** een MD5-hash, als u ervoor kiest een te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa402-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="aa402-249">Gebruik het volgende voorbeeld voor het Microsoft-peering voor uw circuit te configureren:</span><span class="sxs-lookup"><span data-stu-id="aa402-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="aa402-250">De details van Microsoft-peering ophalen</span><span class="sxs-lookup"><span data-stu-id="aa402-250">To get Microsoft peering details</span></span>

<span data-ttu-id="aa402-251">U kunt krijgen configuratiegegevens wilt weergeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aa402-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="aa402-252">Configuratie van Microsoft-peering bijwerken</span><span class="sxs-lookup"><span data-stu-id="aa402-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="aa402-253">U kunt elk deel van de configuratie in het volgende voorbeeld bijwerken:</span><span class="sxs-lookup"><span data-stu-id="aa402-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="aa402-254">Microsoft-peering verwijderen</span><span class="sxs-lookup"><span data-stu-id="aa402-254">To delete Microsoft peering</span></span>

<span data-ttu-id="aa402-255">U kunt de peeringconfiguratie verwijderen door de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aa402-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="aa402-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa402-256">Next steps</span></span>

<span data-ttu-id="aa402-257">Volgende stap, [Een VNet koppelen aan een ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="aa402-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="aa402-258">Voor meer informatie over ExpressRoute-werkstromen raadpleegt u [ExpressRoute workflows](expressroute-workflows.md) (ExpressRoute-werkstromen).</span><span class="sxs-lookup"><span data-stu-id="aa402-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="aa402-259">Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).</span><span class="sxs-lookup"><span data-stu-id="aa402-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="aa402-260">Bekijk het [Virtual network overview](../virtual-network/virtual-networks-overview.md) (Virtual Network-overzicht) voor meer informatie over het gebruik van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="aa402-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
