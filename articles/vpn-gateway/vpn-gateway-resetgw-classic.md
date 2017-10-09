---
title: Opnieuw instellen van een Azure VPN-gateway tooreestablish IPsec-tunnels | Microsoft Docs
description: Dit artikel begeleidt u bij het opnieuw instellen van uw Azure VPN-Gateway tooreestablish IPsec-tunnels. Hallo-artikel geldt tooVPN gateways in Hallo-classic en Hallo Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="3c766-104">Een VPN Gateway opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3c766-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="3c766-105">Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels.</span><span class="sxs-lookup"><span data-stu-id="3c766-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="3c766-106">In dit geval uw on-premises VPN-apparaten zijn alle naar behoren werkt, maar er kan geen tooestablish IPsec-tunnels met hello Azure VPN-gateways zijn.</span><span class="sxs-lookup"><span data-stu-id="3c766-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="3c766-107">In dit artikel helpt u bij uw VPN-gateway opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3c766-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="3c766-108">Wat er gebeurt tijdens het opnieuw instellen?</span><span class="sxs-lookup"><span data-stu-id="3c766-108">What happens during a reset?</span></span>

<span data-ttu-id="3c766-109">Een VPN-gateway bestaat uit twee VM-instanties uitgevoerd in een actief/stand-byconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="3c766-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="3c766-110">Wanneer u opnieuw Hallo-gateway, Hallo-gateway opnieuw opgestart en vervolgens opnieuw toegepast Hallo cross-premises configuraties tooit.</span><span class="sxs-lookup"><span data-stu-id="3c766-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="3c766-111">Hallo gateway houdt Hallo openbaar IP-adres al heeft.</span><span class="sxs-lookup"><span data-stu-id="3c766-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="3c766-112">Dit betekent dat u hoeft niet tooupdate Hallo VPN-routerconfiguratie met een nieuw openbaar IP-adres voor de Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="3c766-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="3c766-113">Wanneer u Hallo opdracht tooreset Hallo gateway verzendt, Hallo huidige instantie van hello Azure VPN-gateway wordt onmiddellijk opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="3c766-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="3c766-114">Er is een korte onderbreking tijdens de failover van Hallo van Hallo actieve instantie (opnieuw wordt opgestart), toohello stand-by-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3c766-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="3c766-115">Hallo onderbreking moet minder dan een minuut.</span><span class="sxs-lookup"><span data-stu-id="3c766-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="3c766-116">Als het Hallo-verbinding is niet hersteld na de eerste keer opnieuw opstarten hello, probleem Hallo dezelfde opdracht opnieuw tooreboot Hallo tweede VM-instantie (Hallo nieuwe actieve gateway).</span><span class="sxs-lookup"><span data-stu-id="3c766-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="3c766-117">Als twee keer opnieuw opstarten Hallo aangevraagde back tooback, zal er iets langer waar beide VM-instanties (actieve en stand-by) worden opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="3c766-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="3c766-118">Hierdoor wordt een gap langer op Hallo VPN-verbinding van too2 too4 minuten voordat VMs toocomplete Hallo opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="3c766-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="3c766-119">Na twee keer opnieuw opstarten als u steeds cross-premises connectiviteitsproblemen ondervindt nog, opent u een verzoek om ondersteuning van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3c766-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="3c766-120"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="3c766-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="3c766-121">Voordat u de gateway opnieuw instelt, moet u controleren Hallo essentiële items voor elke IPsec-Site-naar-Site (S2S) VPN-tunnel hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="3c766-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="3c766-122">Hallo verbinding verbreken van de S2S VPN-tunnels leidt ertoe dat Hallo items niet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="3c766-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="3c766-123">Controleren en te corrigeren Hallo configuraties voor uw on-premises en Azure VPN-gateways voorkomt dat u onnodig opnieuw moet opstarten en onderbrekingen voor Hallo andere werkende verbindingen op Hallo gateways.</span><span class="sxs-lookup"><span data-stu-id="3c766-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="3c766-124">Controleer of de volgende items voordat het opnieuw instellen van uw gateway Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c766-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="3c766-125">Hallo Internet-IP-adressen (VIP's) voor beide hello Azure VPN-gateway en Hallo on-premises VPN-gateway correct zijn geconfigureerd in beide hello Azure en Hallo lokale VPN-beleid.</span><span class="sxs-lookup"><span data-stu-id="3c766-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="3c766-126">Hallo vooraf gedeelde sleutel moet hetzelfde zijn op zowel Azure en on-premises VPN-gateways Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c766-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="3c766-127">Als u specifieke IPsec/IKE-configuratie toepassen, zoals versleuteling, hash-algoritmen en PFS (Perfect Forward Secrecy), zorg ervoor dat beide hello Azure en lokale VPN-gateways Hallo hebben dezelfde configuraties.</span><span class="sxs-lookup"><span data-stu-id="3c766-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="3c766-128"><a name="portal"></a>Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3c766-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="3c766-129">U kunt een Resource Manager-VPN-gateway met behulp van hello Azure-portal opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3c766-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="3c766-130">Als u tooreset een klassieke gateway wilt, Zie Hallo [PowerShell](#resetclassic) stappen.</span><span class="sxs-lookup"><span data-stu-id="3c766-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="3c766-131">Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="3c766-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="3c766-132">Open Hallo [Azure-portal](https://portal.azure.com) en navigeer toohello Resource Manager virtuele netwerkgateway die u tooreset wilt.</span><span class="sxs-lookup"><span data-stu-id="3c766-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="3c766-133">Klik op 'Herstellen' op de blade voor de virtuele netwerkgateway Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c766-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Opnieuw instellen van VPN-Gateway-blade](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="3c766-135">Op Hallo blade, klikt u op Hallo **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="3c766-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="3c766-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c766-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="3c766-137">Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="3c766-137">Resource Manager deployment model</span></span>

<span data-ttu-id="3c766-138">Hallo cmdlet voor opnieuw instellen van een gateway is **Reset AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="3c766-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="3c766-139">Voordat u een reset uitvoert, zorg ervoor dat u beschikt over de nieuwste versie van de Hallo Hallo [Resource Manager PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="3c766-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="3c766-140">Hallo wordt volgende voorbeeld een virtuele netwerkgateway met de naam VNet1GW in Hallo TestRG1 resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="3c766-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="3c766-141">Resultaat:</span><span class="sxs-lookup"><span data-stu-id="3c766-141">Result:</span></span>

<span data-ttu-id="3c766-142">Wanneer u een resultaat geretourneerd ontvangt, kunt u aannemen Hallo gateway opnieuw instellen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c766-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="3c766-143">Maar is er niets in Hallo return resultaat die expliciet aangeeft dat Hallo opnieuw instellen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c766-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="3c766-144">Als u wilt dat toolook nauw op Hallo geschiedenis toosee precies wanneer Hallo-gateway opnieuw instellen is opgetreden, kunt u die informatie weergeven in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3c766-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3c766-145">Navigeer te in Hallo portal**'GatewayName' -> resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="3c766-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="3c766-146"><a name="resetclassic"></a>Klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="3c766-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="3c766-147">Hallo cmdlet voor opnieuw instellen van een gateway is **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="3c766-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="3c766-148">Voordat u een reset uitvoert, zorg ervoor dat u beschikt over de nieuwste versie van de Hallo Hallo [Service Management (SM) PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="3c766-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="3c766-149">Hallo hersteld volgende voorbeeld Hallo gateway voor een virtueel netwerk met de naam 'ContosoVNet':</span><span class="sxs-lookup"><span data-stu-id="3c766-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="3c766-150">Resultaat:</span><span class="sxs-lookup"><span data-stu-id="3c766-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="3c766-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c766-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="3c766-152">Gebruik Hallo-gateway Hallo tooreset [az vnet-netwerkgateway opnieuw](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c766-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="3c766-153">Hallo wordt volgende voorbeeld een virtuele netwerkgateway met de naam VNet5GW in Hallo TestRG5 resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="3c766-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="3c766-154">Resultaat:</span><span class="sxs-lookup"><span data-stu-id="3c766-154">Result:</span></span>

<span data-ttu-id="3c766-155">Wanneer u een resultaat geretourneerd ontvangt, kunt u aannemen Hallo gateway opnieuw instellen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c766-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="3c766-156">Maar is er niets in Hallo return resultaat die expliciet aangeeft dat Hallo opnieuw instellen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c766-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="3c766-157">Als u wilt dat toolook nauw op Hallo geschiedenis toosee precies wanneer Hallo-gateway opnieuw instellen is opgetreden, kunt u die informatie weergeven in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3c766-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3c766-158">Navigeer te in Hallo portal**'GatewayName' -> resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="3c766-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
