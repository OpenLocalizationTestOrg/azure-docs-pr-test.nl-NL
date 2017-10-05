---
title: 'Een virtuele netwerkgateway verwijderen: PowerShell: Azure Resource Manager | Microsoft Docs'
description: Verwijder de gateway van een virtueel netwerk met behulp van PowerShell in het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="f8b0f-103">Verwijder de gateway van een virtueel netwerk met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8b0f-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8b0f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f8b0f-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="f8b0f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8b0f-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="f8b0f-106">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="f8b0f-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="f8b0f-107">Er zijn verschillende manieren die kunt u uw als u wilt verwijderen van een virtuele netwerkgateway voor de configuratie van een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="f8b0f-108">Als u wilt Alles verwijderen en opnieuw beginnen, zoals in het geval van een testomgeving kunt u de resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="f8b0f-109">Wanneer u een resourcegroep verwijdert, worden alle resources binnen de groep verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="f8b0f-110">Deze methode is wordt alleen aanbevolen als u niet wilt dat de bronnen in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="f8b0f-111">U kunt alleen een aantal bronnen met deze benadering selectief niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="f8b0f-112">Als u wilt dat een aantal van de resources in de resourcegroep, verwijderen van een virtuele netwerkgateway enigszins iets gecompliceerder.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="f8b0f-113">Voordat u de virtuele netwerkgateway verwijderen kunt, moet u eerst alle bronnen die afhankelijk van de gateway zijn te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="f8b0f-114">De stappen die u volgt, is afhankelijk van het type van de verbindingen die u hebt gemaakt en de afhankelijke resources voor elke verbinding.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="f8b0f-115">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f8b0f-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="f8b0f-116">1. Download de nieuwste Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="f8b0f-117">Download en installeer de nieuwste versie van de Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f8b0f-118">Zie voor meer informatie over het downloaden en installeren van PowerShell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f8b0f-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="f8b0f-119">2. Verbinding maken met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="f8b0f-120">Open de PowerShell-console en maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="f8b0f-121">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="f8b0f-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f8b0f-122">Controleer de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f8b0f-123">Als u meer dan één abonnement hebt, geeft u het abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="f8b0f-124"><a name="S2S"></a>Verwijderen van een Site-naar-Site VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="f8b0f-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="f8b0f-125">Als u wilt verwijderen van een virtuele netwerkgateway voor een S2S-configuratie, moet u eerst elke bron die betrekking op de virtuele netwerkgateway hebben verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="f8b0f-126">Resources moeten worden verwijderd in een bepaalde volgorde vanwege afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="f8b0f-127">Als u werkt met de voorbeelden hieronder enkele van moeten de waarden worden opgegeven, terwijl andere waarden een uitvoerresultaat zijn.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="f8b0f-128">We gebruiken de volgende specifieke waarden in de voorbeelden voor demonstratiedoeleinden:</span><span class="sxs-lookup"><span data-stu-id="f8b0f-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="f8b0f-129">VNet-naam: VNet1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="f8b0f-130">De naam van resourcegroep: RG1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="f8b0f-131">Naam van virtuele-netwerkgateway: GW1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="f8b0f-132">De volgende stappen van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="f8b0f-133">1. Haal de virtuele netwerkgateway die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="f8b0f-134">2. Controleer of de virtuele netwerkgateway geen verbindingen heeft.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="f8b0f-135">3. Verwijder alle verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-135">3. Delete all connections.</span></span>

<span data-ttu-id="f8b0f-136">U wordt mogelijk gevraagd de verwijdering van elk van de verbindingen te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="f8b0f-137">4. Verwijder de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="f8b0f-138">U wordt mogelijk gevraagd de verwijdering van de gateway te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="f8b0f-139">Als u een P2S-configuratie in dit VNet naast de S2S-configuratie hebt, wordt er bij het verwijderen van de virtuele netwerkgateway automatisch alle P2S-clients zonder waarschuwing verbreekt.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="f8b0f-140">Op dit moment is uw virtuele netwerkgateway verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="f8b0f-141">De volgende stappen kunt u alle resources verwijderen die niet langer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="f8b0f-142">5 verwijderen uit de lokale netwerkgateways.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="f8b0f-143">De lijst van de bijbehorende lokale netwerkgateways ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="f8b0f-144">Verwijderen van de lokale netwerkgateways.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-144">Delete the local network gateways.</span></span> <span data-ttu-id="f8b0f-145">U wordt mogelijk gevraagd de verwijdering van elk van de lokale netwerkgateway te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="f8b0f-146">6. Verwijder het openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="f8b0f-147">De IP-configuraties van de virtuele netwerkgateway ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="f8b0f-148">De lijst met openbare IP-adresbronnen gebruikt voor deze virtuele netwerkgateway ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="f8b0f-149">Als de virtuele netwerkgateway actief-actief is, ziet u twee openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="f8b0f-150">Het openbare IP-resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="f8b0f-151">7. Het gatewaysubnet verwijderen en de configuratie ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="f8b0f-152"><a name="v2v"></a>Verwijderen van een VNet-naar-VNet-VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="f8b0f-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="f8b0f-153">Als u wilt verwijderen van een virtuele netwerkgateway voor een V2V-configuratie, moet u eerst elke bron die betrekking op de virtuele netwerkgateway hebben verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="f8b0f-154">Resources moeten worden verwijderd in een bepaalde volgorde vanwege afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="f8b0f-155">Als u werkt met de voorbeelden hieronder enkele van moeten de waarden worden opgegeven, terwijl andere waarden een uitvoerresultaat zijn.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="f8b0f-156">We gebruiken de volgende specifieke waarden in de voorbeelden voor demonstratiedoeleinden:</span><span class="sxs-lookup"><span data-stu-id="f8b0f-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="f8b0f-157">VNet-naam: VNet1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="f8b0f-158">De naam van resourcegroep: RG1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="f8b0f-159">Naam van virtuele-netwerkgateway: GW1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="f8b0f-160">De volgende stappen van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="f8b0f-161">1. Haal de virtuele netwerkgateway die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="f8b0f-162">2. Controleer of de virtuele netwerkgateway geen verbindingen heeft.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="f8b0f-163">Mogelijk zijn er andere verbindingen met de virtuele netwerkgateway die deel van een andere resourcegroep uitmaken.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="f8b0f-164">Controleren op aanvullende verbindingen in elke extra resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="f8b0f-165">In dit voorbeeld zijn er voor de verbindingen van RG2 gezocht.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="f8b0f-166">Deze uitvoeren voor elke resourcegroep dat u hebt die een verbinding met de virtuele netwerkgateway kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="f8b0f-167">3. De lijst met verbindingen opgehaald in beide richtingen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="f8b0f-168">Omdat dit een VNet-naar-VNet-configuratie, moet u de lijst met verbindingen in beide richtingen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="f8b0f-169">In dit voorbeeld zijn er voor de verbindingen van RG2 gezocht.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="f8b0f-170">Deze uitvoeren voor elke resourcegroep dat u hebt die een verbinding met de virtuele netwerkgateway kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="f8b0f-171">4. Verwijder alle verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-171">4. Delete all connections.</span></span>

<span data-ttu-id="f8b0f-172">U wordt mogelijk gevraagd de verwijdering van elk van de verbindingen te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="f8b0f-173">5. Verwijder de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="f8b0f-174">U wordt mogelijk gevraagd de verwijdering van de virtuele netwerkgateway te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="f8b0f-175">Als u P2S-configuraties naar uw vnet's naast de V2V-configuratie hebt, wordt er bij het verwijderen van de virtuele netwerkgateways automatisch alle P2S-clients zonder waarschuwing verbroken.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="f8b0f-176">Op dit moment is uw virtuele netwerkgateway verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="f8b0f-177">De volgende stappen kunt u alle resources verwijderen die niet langer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="f8b0f-178">6. De resources van openbare IP-adres verwijderen</span><span class="sxs-lookup"><span data-stu-id="f8b0f-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="f8b0f-179">De IP-configuraties van de virtuele netwerkgateway ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="f8b0f-180">De lijst met openbare IP-adresbronnen gebruikt voor deze virtuele netwerkgateway ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="f8b0f-181">Als de virtuele netwerkgateway actief-actief is, ziet u twee openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="f8b0f-182">Het openbare IP-resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-182">Delete the Public IP resources.</span></span> <span data-ttu-id="f8b0f-183">U wordt mogelijk gevraagd de verwijdering van het openbare IP-adres te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="f8b0f-184">7. Het gatewaysubnet verwijderen en de configuratie ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="f8b0f-185"><a name="deletep2s"></a>Verwijderen van een punt-naar-Site VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="f8b0f-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="f8b0f-186">Als u wilt verwijderen van een virtuele netwerkgateway voor een P2S-configuratie, moet u eerst elke bron die betrekking op de virtuele netwerkgateway hebben verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="f8b0f-187">Resources moeten worden verwijderd in een bepaalde volgorde vanwege afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="f8b0f-188">Als u werkt met de voorbeelden hieronder enkele van moeten de waarden worden opgegeven, terwijl andere waarden een uitvoerresultaat zijn.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="f8b0f-189">We gebruiken de volgende specifieke waarden in de voorbeelden voor demonstratiedoeleinden:</span><span class="sxs-lookup"><span data-stu-id="f8b0f-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="f8b0f-190">VNet-naam: VNet1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="f8b0f-191">De naam van resourcegroep: RG1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="f8b0f-192">Naam van virtuele-netwerkgateway: GW1</span><span class="sxs-lookup"><span data-stu-id="f8b0f-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="f8b0f-193">De volgende stappen van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="f8b0f-194">Wanneer u de VPN-gateway verwijdert, worden alle verbonden clients worden losgekoppeld van het VNet zonder waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="f8b0f-195">1. Haal de virtuele netwerkgateway die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="f8b0f-196">2. Verwijder de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="f8b0f-197">U wordt mogelijk gevraagd de verwijdering van de virtuele netwerkgateway te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="f8b0f-198">Op dit moment is uw virtuele netwerkgateway verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="f8b0f-199">De volgende stappen kunt u alle resources verwijderen die niet langer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="f8b0f-200">3. De resources van openbare IP-adres verwijderen</span><span class="sxs-lookup"><span data-stu-id="f8b0f-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="f8b0f-201">De IP-configuraties van de virtuele netwerkgateway ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="f8b0f-202">De lijst met openbare IP-adressen gebruikt voor deze virtuele netwerkgateway ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="f8b0f-203">Als de virtuele netwerkgateway actief-actief is, ziet u twee openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="f8b0f-204">Verwijder het openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-204">Delete the Public IPs.</span></span> <span data-ttu-id="f8b0f-205">U wordt mogelijk gevraagd de verwijdering van het openbare IP-adres te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="f8b0f-206">4. Het gatewaysubnet verwijderen en de configuratie ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="f8b0f-207"><a name="delete"></a>Een VPN-gateway verwijderen door het verwijderen van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f8b0f-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="f8b0f-208">Als u zich geen zorgen over het houden van uw resources in de resourcegroep en u wilt beginnen, kunt u een hele resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="f8b0f-209">Dit is een snelle manier om alles verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="f8b0f-210">De volgende stappen gelden alleen voor het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="f8b0f-211">1. Een lijst met alle resourcegroepen in uw abonnement ophalen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="f8b0f-212">2. Zoek de resourcegroep die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="f8b0f-213">Zoek de resourcegroep die u wilt verwijderen en de lijst met resources in die resourcegroep weergeven.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="f8b0f-214">In het voorbeeld is de naam van de resourcegroep RG1.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="f8b0f-215">Wijzig in het voorbeeld voor het ophalen van een lijst met alle bronnen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="f8b0f-216">3. Controleer of de bronnen in de lijst.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="f8b0f-217">Als de lijst wordt geretourneerd, bekijken om te controleren dat u wilt verwijderen van alle resources in de resourcegroep, evenals de resourcegroep zelf.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="f8b0f-218">Als u wilt dat sommige van de resources in de resourcegroep, gebruikt u de stappen in de vorige secties van dit artikel uw gateway verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="f8b0f-219">4. Verwijder de resourcegroep en resources.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="f8b0f-220">Als u wilt verwijderen van de resourcegroep en de resource die zijn opgenomen in de resourcegroep, in het voorbeeld wijzigen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="f8b0f-221">5. Controleer de status.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-221">5. Check the status.</span></span>

<span data-ttu-id="f8b0f-222">Het duurt enige tijd Azure alle resources verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="f8b0f-223">U kunt de status van de resourcegroep controleren met behulp van deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="f8b0f-224">Het resultaat dat wordt geretourneerd toont 'Voltooid'.</span><span class="sxs-lookup"><span data-stu-id="f8b0f-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```