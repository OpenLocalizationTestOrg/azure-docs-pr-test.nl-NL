---
title: een Azure VPN-verbinding voor site-naar-site die geen verbinding kan maken aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot een site-naar-site VPN-verbinding die plotseling werkt niet en kan niet worden hersteld.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="70654-103">Voor probleemoplossing: Een Azure site-naar-site VPN-verbinding kan geen verbinding maken en werkt niet</span><span class="sxs-lookup"><span data-stu-id="70654-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="70654-104">Nadat u een site-naar-site VPN-verbinding tussen een on-premises netwerk en een Azure-netwerk configureert, wordt Hallo VPN-verbinding plotseling werkt niet en kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="70654-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="70654-105">In dit artikel voor probleemoplossing stappen toohelp vindt u dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="70654-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="70654-106">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="70654-106">Troubleshooting steps</span></span>

<span data-ttu-id="70654-107">tooresolve hello probleem, probeer dan eerst te[reset hello Azure VPN-gateway](vpn-gateway-resetgw-classic.md) en Hallo tunnel van Hallo on-premises VPN-apparaat opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="70654-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="70654-108">Als het Hallo-probleem zich blijft voordoen, volgt u deze stappen tooidentify Hallo Hallo probleem veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="70654-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="70654-109">Vereiste stap</span><span class="sxs-lookup"><span data-stu-id="70654-109">Prerequisite step</span></span>

<span data-ttu-id="70654-110">Controleer Hallo type hello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="70654-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="70654-111">Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70654-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="70654-112">Controleer Hallo **overzicht** pagina Hallo VPN-gateway voor Hallo type informatie.</span><span class="sxs-lookup"><span data-stu-id="70654-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Overzicht van Hallo-gateway](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="70654-114">Step 1.</span><span class="sxs-lookup"><span data-stu-id="70654-114">Step 1.</span></span> <span data-ttu-id="70654-115">Controleer of de Hallo on-premises VPN-apparaat wordt gevalideerd</span><span class="sxs-lookup"><span data-stu-id="70654-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="70654-116">Controleer of u een [gevalideerde VPN-apparaat en de versie van besturingssysteem](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="70654-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="70654-117">Als het Hallo-apparaat is niet gevalideerde VPN-apparaat, kunt u toocontact Hallo apparaat fabrikant toosee wellicht als er een compatibiliteitsprobleem.</span><span class="sxs-lookup"><span data-stu-id="70654-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="70654-118">Zorg ervoor dat het Hallo-VPN-apparaat correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="70654-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="70654-119">Zie voor meer informatie [bewerken van apparaatconfiguraties](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="70654-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="70654-120">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="70654-120">Step 2.</span></span> <span data-ttu-id="70654-121">Controleer of de gedeelde sleutel Hallo</span><span class="sxs-lookup"><span data-stu-id="70654-121">Verify hello shared key</span></span>

<span data-ttu-id="70654-122">Hallo gedeelde sleutel voor Hallo lokale VPN-apparaat toohello Azure Virtual Network VPN toomake Hallo sleutels overeenkomen met vergelijken.</span><span class="sxs-lookup"><span data-stu-id="70654-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="70654-123">tooview hello gedeelde sleutel voor hello Azure VPN-verbinding, een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="70654-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="70654-124">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="70654-124">**Azure portal**</span></span>

1. <span data-ttu-id="70654-125">Ga toohello VPN-gateway site-naar-site-verbinding die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70654-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="70654-126">In Hallo **instellingen** sectie, klikt u op **gedeelde sleutel**.</span><span class="sxs-lookup"><span data-stu-id="70654-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Gedeelde sleutel](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="70654-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="70654-128">**Azure PowerShell**</span></span>

<span data-ttu-id="70654-129">Hello Azure Resource Manager-implementatiemodel:</span><span class="sxs-lookup"><span data-stu-id="70654-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="70654-130">Voor het klassieke implementatiemodel Hallo:</span><span class="sxs-lookup"><span data-stu-id="70654-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="70654-131">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="70654-131">Step 3.</span></span> <span data-ttu-id="70654-132">Controleer of Hallo VPN-peer IP-adressen</span><span class="sxs-lookup"><span data-stu-id="70654-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="70654-133">IP-definitie in Hallo Hallo **Local Network Gateway** -object in Azure moet overeenkomen met de Hallo lokale apparaat IP.</span><span class="sxs-lookup"><span data-stu-id="70654-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="70654-134">Hello Azure-gateway IP-definitie die is ingesteld op Hallo lokale apparaat moet overeenkomen met hello Azure-gateway IP.</span><span class="sxs-lookup"><span data-stu-id="70654-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="70654-135">Stap 4.</span><span class="sxs-lookup"><span data-stu-id="70654-135">Step 4.</span></span> <span data-ttu-id="70654-136">Controleer UDR en nsg's op Hallo gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="70654-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="70654-137">Controleren op en verwijderen van de gebruiker gedefinieerde Routering of Netwerkbeveiligingsgroepen (nsg's) op Hallo gatewaysubnet en test u Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="70654-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="70654-138">Als het Hallo-probleem is opgelost, controleert u Hallo-instellingen die UDR of NSG toegepast.</span><span class="sxs-lookup"><span data-stu-id="70654-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="70654-139">Stap 5.</span><span class="sxs-lookup"><span data-stu-id="70654-139">Step 5.</span></span> <span data-ttu-id="70654-140">Hallo lokale VPN-apparaat externe Interfaceadres controleren</span><span class="sxs-lookup"><span data-stu-id="70654-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="70654-141">Als Hallo internetgerichte IP-adres van Hallo VPN-apparaat is opgenomen in Hallo **lokale netwerk** definitie in Azure, kunt u tegenkomen sporadisch worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="70654-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="70654-142">Hallo moet externe interface van het apparaat rechtstreeks op Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="70654-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="70654-143">Er zijn geen netwerkadresomzetting of de firewall tussen Hallo Internet en het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="70654-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="70654-144">tooconfigure firewall clustering toohave een virtueel IP-adres, moet u Hallo cluster opsplitsen en Hallo-VPN-apparaat beschikbaar rechtstreeks tooa openbare interface die Hallo-gateway kan verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="70654-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="70654-145">Stap 6.</span><span class="sxs-lookup"><span data-stu-id="70654-145">Step 6.</span></span> <span data-ttu-id="70654-146">Controleren of subnetten Hallo exact overeenkomen (Azure op beleid gebaseerde gateways)</span><span class="sxs-lookup"><span data-stu-id="70654-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="70654-147">Controleer of dat Hallo subnetten exact hello virtuele Azure-netwerk- en lokale definities voor Hallo virtuele Azure-netwerk overeen.</span><span class="sxs-lookup"><span data-stu-id="70654-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="70654-148">Controleer of dat Hallo subnetten tussen Hallo exact overeenkomen met **Local Network Gateway** en on-premises definities voor Hallo on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="70654-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="70654-149">Stap 7.</span><span class="sxs-lookup"><span data-stu-id="70654-149">Step 7.</span></span> <span data-ttu-id="70654-150">Controleer of de statuscontrole van hello Azure-gateway</span><span class="sxs-lookup"><span data-stu-id="70654-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="70654-151">Ga toohello [health test](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="70654-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="70654-152">Klik in het Hallo-certificaatwaarschuwing.</span><span class="sxs-lookup"><span data-stu-id="70654-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="70654-153">Als u een antwoord ontvangt, Hallo VPN-gateway wordt beschouwd als in orde.</span><span class="sxs-lookup"><span data-stu-id="70654-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="70654-154">Als u niet een antwoord ontvangt, Hallo gateway mogelijk niet in orde of Hallo probleem wordt veroorzaakt door een NSG op Hallo gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="70654-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="70654-155">na de tekst Hello is een voorbeeldantwoord:</span><span class="sxs-lookup"><span data-stu-id="70654-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="70654-156">&lt;? XML-versie = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">primaire exemplaar: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / tekenreeks&gt;</span><span class="sxs-lookup"><span data-stu-id="70654-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="70654-157">Stap 8.</span><span class="sxs-lookup"><span data-stu-id="70654-157">Step 8.</span></span> <span data-ttu-id="70654-158">Controleer of Hallo lokale VPN-apparaat heeft Hallo perfect forward secrecy functie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="70654-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="70654-159">Hallo perfect forward secrecy functie veroorzaken verbreken problemen.</span><span class="sxs-lookup"><span data-stu-id="70654-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="70654-160">Als Hallo VPN-apparaat perfect forward secrecy is ingeschakeld heeft, Hallo functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="70654-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="70654-161">Werk vervolgens Hallo VPN-gateway IPSec-beleid.</span><span class="sxs-lookup"><span data-stu-id="70654-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70654-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70654-162">Next steps</span></span>

-   [<span data-ttu-id="70654-163">Een site-naar-site-verbinding tooa virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="70654-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="70654-164">Beleid voor IPsec/IKE voor site-naar-site VPN-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="70654-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
