---
title: Een Azure VPN-gateway als u wilt herstellen IPsec-tunnels opnieuw instellen | Microsoft Docs
description: Dit artikel begeleidt u bij het opnieuw instellen van uw Azure VPN-Gateway als u wilt herstellen IPsec-tunnels. Het artikel is van toepassing op VPN-gateways in het klassieke en het Resource Manager-implementatiemodel.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="fef4b-104">Een VPN Gateway opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="fef4b-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="fef4b-105">Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels.</span><span class="sxs-lookup"><span data-stu-id="fef4b-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="fef4b-106">In een dergelijke situatie functioneren al uw on-premises VPN-apparaten naar behoren, maar kunnen ze geen IPSec-tunnels tot stand brengen met de Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="fef4b-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="fef4b-107">In dit artikel helpt u bij uw VPN-gateway opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="fef4b-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="fef4b-108">Wat er gebeurt tijdens het opnieuw instellen?</span><span class="sxs-lookup"><span data-stu-id="fef4b-108">What happens during a reset?</span></span>

<span data-ttu-id="fef4b-109">Een VPN-gateway bestaat uit twee VM-instanties uitgevoerd in een actief/stand-byconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="fef4b-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="fef4b-110">Wanneer u de gateway opnieuw instelt, wordt de gateway opnieuw opgestart en vervolgens wordt de cross-premises configuraties opnieuw toegepast.</span><span class="sxs-lookup"><span data-stu-id="fef4b-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="fef4b-111">De gateway behoudt hetzelfde openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="fef4b-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="fef4b-112">Dat betekent dat u de VPN-routerconfiguratie niet hoeft bij te werken met een nieuw openbaar IP-adres voor de Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="fef4b-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="fef4b-113">Wanneer u de opdracht opnieuw in te stellen van de gateway, de huidige instantie van de Azure VPN-gateway wordt onmiddellijk opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="fef4b-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="fef4b-114">Er is een korte onderbreking tijdens de failover van de actieve instantie (opnieuw wordt opgestart), naar de stand-by-instantie.</span><span class="sxs-lookup"><span data-stu-id="fef4b-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="fef4b-115">Deze onderbreking zou niet langer dan een minuut moeten duren.</span><span class="sxs-lookup"><span data-stu-id="fef4b-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="fef4b-116">Als de verbinding na de eerste keer opnieuw opstarten niet is hersteld, voert u deze opdracht opnieuw uit om de tweede VM-instantie (de nieuwe actieve gateway) opnieuw op te starten.</span><span class="sxs-lookup"><span data-stu-id="fef4b-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="fef4b-117">Als de twee keer opnieuw opstarten direct na elkaar wordt aangevraagd, duurt het iets langer omdat beide VM-exemplaren (actief en stand-by) opnieuw worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="fef4b-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="fef4b-118">Dit veroorzaakt een langere onderbreking van de VPN-verbinding, die twee tot vier minuten kan duren, voordat de virtuele machines opnieuw zijn opgestart.</span><span class="sxs-lookup"><span data-stu-id="fef4b-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="fef4b-119">Na twee keer opnieuw opstarten als u steeds cross-premises connectiviteitsproblemen ondervindt nog, opent u een verzoek om ondersteuning van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fef4b-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="fef4b-120"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fef4b-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="fef4b-121">Controleer voordat u de gateway opnieuw instelt de hieronder vermelde belangrijke zaken voor elke S2S-VPN-tunnel (site-naar-site) met IPsec.</span><span class="sxs-lookup"><span data-stu-id="fef4b-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="fef4b-122">Als items niet overeenkomen, wordt de verbinding met S2SVPN-tunnels verbroken.</span><span class="sxs-lookup"><span data-stu-id="fef4b-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="fef4b-123">Controleren en te corrigeren van de configuraties voor uw on-premises en Azure VPN-gateways slaat u onnodig opnieuw moet opstarten en dat de andere werkende verbindingen op de gateways.</span><span class="sxs-lookup"><span data-stu-id="fef4b-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="fef4b-124">Controleer of u de volgende items voordat het opnieuw instellen van uw gateway:</span><span class="sxs-lookup"><span data-stu-id="fef4b-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="fef4b-125">Controleer of de internet-IP-adressen (VIP's) voor zowel de Azure VPN-gateway als de on-premises VPN-gateway correct zijn geconfigureerd in zowel het Azure- als het lokale VPN-beleid.</span><span class="sxs-lookup"><span data-stu-id="fef4b-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="fef4b-126">De vooraf gedeelde sleutel moet hetzelfde zijn in de Azure- en de on-premises VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="fef4b-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="fef4b-127">Als u een specifieke IPsec/IKE-configuratie, zoals versleuteling, hash-algoritmen en PFS (Perfect Forward Secrecy) toepast, moet u controleren of de Azure- en on-premises VPN-gateway dezelfde configuratie hebben.</span><span class="sxs-lookup"><span data-stu-id="fef4b-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="fef4b-128"><a name="portal"></a>Azure-portal</span><span class="sxs-lookup"><span data-stu-id="fef4b-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="fef4b-129">U kunt een Resource Manager-VPN-gateway met behulp van de Azure-portal opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="fef4b-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="fef4b-130">Als u een klassieke gateway opnieuw instellen wilt, raadpleegt u de [PowerShell](#resetclassic) stappen.</span><span class="sxs-lookup"><span data-stu-id="fef4b-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="fef4b-131">Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="fef4b-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="fef4b-132">Open de [Azure-portal](https://portal.azure.com) en navigeer naar de virtuele netwerkgateway van Resource Manager die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="fef4b-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="fef4b-133">Klik op 'Herstellen' op de blade voor de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="fef4b-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![Opnieuw instellen van VPN-Gateway-blade](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="fef4b-135">Klik op de blade opnieuw instellen op de **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="fef4b-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="fef4b-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef4b-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="fef4b-137">Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="fef4b-137">Resource Manager deployment model</span></span>

<span data-ttu-id="fef4b-138">De cmdlet voor het opnieuw instellen van een gateway is **Reset AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="fef4b-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="fef4b-139">Voordat u een reset uitvoert, zorg ervoor dat de nieuwste versie van de [Resource Manager PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="fef4b-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="fef4b-140">Het volgende voorbeeld wordt een virtuele netwerkgateway VNet1GW met de naam in de resourcegroep TestRG1:</span><span class="sxs-lookup"><span data-stu-id="fef4b-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="fef4b-141">Resultaat:</span><span class="sxs-lookup"><span data-stu-id="fef4b-141">Result:</span></span>

<span data-ttu-id="fef4b-142">Wanneer u een resultaat geretourneerd ontvangt, kunt u aannemen opnieuw instellen van de gateway is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="fef4b-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="fef4b-143">Maar is er niets in de geretourneerde resultatenset die expliciet aangeeft dat het opnieuw instellen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="fef4b-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="fef4b-144">Als u kijken nauw de geschiedenis om te zien precies wanneer het opnieuw instellen van de gateway is opgetreden wilt, kunt u bekijken die informatie in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fef4b-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fef4b-145">Navigeer in de portal naar **'GatewayName' -> resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="fef4b-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="fef4b-146"><a name="resetclassic"></a>Klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="fef4b-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="fef4b-147">De cmdlet voor het opnieuw instellen van een gateway is **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="fef4b-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="fef4b-148">Voordat u een reset uitvoert, zorg ervoor dat de nieuwste versie van de [Service Management (SM) PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="fef4b-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="fef4b-149">Het volgende voorbeeld wordt de gateway voor een virtueel netwerk met de naam 'ContosoVNet':</span><span class="sxs-lookup"><span data-stu-id="fef4b-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="fef4b-150">Resultaat:</span><span class="sxs-lookup"><span data-stu-id="fef4b-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="fef4b-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fef4b-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="fef4b-152">Om de gateway opnieuw instellen, gebruikt u de [az vnet-netwerkgateway opnieuw](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) opdracht.</span><span class="sxs-lookup"><span data-stu-id="fef4b-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="fef4b-153">Het volgende voorbeeld wordt een virtuele netwerkgateway VNet5GW met de naam in de resourcegroep TestRG5:</span><span class="sxs-lookup"><span data-stu-id="fef4b-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="fef4b-154">Resultaat:</span><span class="sxs-lookup"><span data-stu-id="fef4b-154">Result:</span></span>

<span data-ttu-id="fef4b-155">Wanneer u een resultaat geretourneerd ontvangt, kunt u aannemen opnieuw instellen van de gateway is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="fef4b-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="fef4b-156">Maar is er niets in de geretourneerde resultatenset die expliciet aangeeft dat het opnieuw instellen voltooid is.</span><span class="sxs-lookup"><span data-stu-id="fef4b-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="fef4b-157">Als u kijken nauw de geschiedenis om te zien precies wanneer het opnieuw instellen van de gateway is opgetreden wilt, kunt u bekijken die informatie in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fef4b-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fef4b-158">Navigeer in de portal naar **'GatewayName' -> resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="fef4b-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>