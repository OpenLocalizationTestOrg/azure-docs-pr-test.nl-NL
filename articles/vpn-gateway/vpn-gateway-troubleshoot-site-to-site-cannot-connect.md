---
title: Problemen met een Azure VPN-verbinding voor site-naar-site die kan geen verbinding maken | Microsoft Docs
description: Informatie over het oplossen van problemen met een site-naar-site VPN-verbinding die plotseling werkt niet en kan niet worden hersteld.
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
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="8263e-103">Voor probleemoplossing: Een Azure site-naar-site VPN-verbinding kan geen verbinding maken en werkt niet</span><span class="sxs-lookup"><span data-stu-id="8263e-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="8263e-104">Nadat u een site-naar-site VPN-verbinding tussen een on-premises netwerk en een Azure-netwerk configureert, wordt de VPN-verbinding plotseling werkt niet en kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8263e-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="8263e-105">Dit artikel bevat de stappen voor probleemoplossing waarmee u kunt dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="8263e-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="8263e-106">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="8263e-106">Troubleshooting steps</span></span>

<span data-ttu-id="8263e-107">U lost het probleem door eerst [opnieuw instellen van de Azure VPN-gateway](vpn-gateway-resetgw-classic.md) en de tunnel van de on-premises VPN-apparaat opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="8263e-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="8263e-108">Als het probleem zich blijft voordoen, volg deze stappen om de oorzaak van het probleem te identificeren.</span><span class="sxs-lookup"><span data-stu-id="8263e-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="8263e-109">Vereiste stap</span><span class="sxs-lookup"><span data-stu-id="8263e-109">Prerequisite step</span></span>

<span data-ttu-id="8263e-110">Controleer het type van de Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="8263e-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="8263e-111">Ga naar de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8263e-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8263e-112">Controleer de **overzicht** pagina van de VPN-gateway voor de type-informatie.</span><span class="sxs-lookup"><span data-stu-id="8263e-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![Overzicht van de gateway](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="8263e-114">Step 1.</span><span class="sxs-lookup"><span data-stu-id="8263e-114">Step 1.</span></span> <span data-ttu-id="8263e-115">Controleer of de on-premises VPN-apparaat wordt gevalideerd</span><span class="sxs-lookup"><span data-stu-id="8263e-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="8263e-116">Controleer of u een [gevalideerde VPN-apparaat en de versie van besturingssysteem](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="8263e-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="8263e-117">Als het apparaat niet gevalideerde VPN-apparaat, moet u wellicht contact op met de fabrikant van het apparaat om te zien of er een compatibiliteitsprobleem.</span><span class="sxs-lookup"><span data-stu-id="8263e-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="8263e-118">Zorg ervoor dat het VPN-apparaat correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8263e-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="8263e-119">Zie voor meer informatie [bewerken van apparaatconfiguraties](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="8263e-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="8263e-120">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="8263e-120">Step 2.</span></span> <span data-ttu-id="8263e-121">Controleer of de gedeelde sleutel</span><span class="sxs-lookup"><span data-stu-id="8263e-121">Verify the shared key</span></span>

<span data-ttu-id="8263e-122">Vergelijk de gedeelde sleutel voor de on-premises VPN-apparaat met het virtuele netwerk voor Azure VPN om ervoor te zorgen dat de sleutels overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="8263e-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="8263e-123">Als u wilt weergeven van de gedeelde sleutel voor de Azure VPN-verbinding, moet u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8263e-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="8263e-124">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="8263e-124">**Azure portal**</span></span>

1. <span data-ttu-id="8263e-125">Ga naar de VPN-gateway site-naar-site-verbinding die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8263e-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="8263e-126">In de **instellingen** sectie, klikt u op **gedeelde sleutel**.</span><span class="sxs-lookup"><span data-stu-id="8263e-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![Gedeelde sleutel](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="8263e-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="8263e-128">**Azure PowerShell**</span></span>

<span data-ttu-id="8263e-129">Voor het Azure Resource Manager-implementatiemodel:</span><span class="sxs-lookup"><span data-stu-id="8263e-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="8263e-130">Voor het klassieke implementatiemodel:</span><span class="sxs-lookup"><span data-stu-id="8263e-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="8263e-131">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="8263e-131">Step 3.</span></span> <span data-ttu-id="8263e-132">Controleer of de VPN-peer-IP-adressen</span><span class="sxs-lookup"><span data-stu-id="8263e-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="8263e-133">De IP-definitie in de **Local Network Gateway** -object in Azure, moet overeenkomen met het lokale apparaat IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8263e-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="8263e-134">De Azure-gateway IP-definitie die is ingesteld op de on-premises-apparaat moet overeenkomen met het Azure-gateway IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8263e-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="8263e-135">Stap 4.</span><span class="sxs-lookup"><span data-stu-id="8263e-135">Step 4.</span></span> <span data-ttu-id="8263e-136">Controleer UDR en nsg's op het gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="8263e-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="8263e-137">Controleren op en verwijderen van de gebruiker gedefinieerde Routering of Netwerkbeveiligingsgroepen (nsg's) op het gatewaysubnet en vervolgens het resultaat te testen.</span><span class="sxs-lookup"><span data-stu-id="8263e-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="8263e-138">Als het probleem opgelost is, controleert u de instellingen die UDR of NSG toegepast.</span><span class="sxs-lookup"><span data-stu-id="8263e-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="8263e-139">Stap 5.</span><span class="sxs-lookup"><span data-stu-id="8263e-139">Step 5.</span></span> <span data-ttu-id="8263e-140">Controleer het adres van de lokale VPN-apparaat externe interface</span><span class="sxs-lookup"><span data-stu-id="8263e-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="8263e-141">Als het internetgerichte IP-adres van de VPN-apparaat is opgenomen in de **lokale netwerk** definitie in Azure, kunt u tegenkomen sporadisch worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="8263e-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="8263e-142">De externe interface van het apparaat moet rechtstreeks op het Internet.</span><span class="sxs-lookup"><span data-stu-id="8263e-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="8263e-143">Er zijn geen netwerkadresomzetting of de firewall tussen het Internet en het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8263e-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="8263e-144">Firewall clustering als u een virtueel IP-adres wilt configureren, moet u opsplitsen van het cluster en de VPN-apparaat rechtstreeks naar een openbare interface die de gateway kan verbinding maken met weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8263e-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="8263e-145">Stap 6.</span><span class="sxs-lookup"><span data-stu-id="8263e-145">Step 6.</span></span> <span data-ttu-id="8263e-146">Controleer of de subnetten exact overeenkomen (Azure op beleid gebaseerde gateways)</span><span class="sxs-lookup"><span data-stu-id="8263e-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="8263e-147">Controleer of de subnetten die overeenkomen met exact tussen de virtuele Azure-netwerk en lokale definities voor de virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="8263e-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="8263e-148">Controleer of de subnetten tussen exact overeenkomen met de **Local Network Gateway** en on-premises definities voor de on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="8263e-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="8263e-149">Stap 7.</span><span class="sxs-lookup"><span data-stu-id="8263e-149">Step 7.</span></span> <span data-ttu-id="8263e-150">Controleer of de statuscontrole van de Azure-gateway</span><span class="sxs-lookup"><span data-stu-id="8263e-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="8263e-151">Ga naar de [health test](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="8263e-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="8263e-152">Klik in de certificaatwaarschuwing.</span><span class="sxs-lookup"><span data-stu-id="8263e-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="8263e-153">Als u een antwoord ontvangt, wordt de VPN-gateway als in orde beschouwd.</span><span class="sxs-lookup"><span data-stu-id="8263e-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="8263e-154">Als u niet een antwoord ontvangt, de gateway mogelijk niet in orde of het probleem wordt veroorzaakt door een NSG op het gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="8263e-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="8263e-155">De volgende tekst is een voorbeeldantwoord:</span><span class="sxs-lookup"><span data-stu-id="8263e-155">The following text is a sample response:</span></span>

    <span data-ttu-id="8263e-156">&lt;? XML-versie = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">primaire exemplaar: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / tekenreeks&gt;</span><span class="sxs-lookup"><span data-stu-id="8263e-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="8263e-157">Stap 8.</span><span class="sxs-lookup"><span data-stu-id="8263e-157">Step 8.</span></span> <span data-ttu-id="8263e-158">Controleer of de on-premises VPN-apparaat de functie perfect forward secrecy is ingeschakeld heeft</span><span class="sxs-lookup"><span data-stu-id="8263e-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="8263e-159">De functie perfect forward secrecy kunt verbreken problemen veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="8263e-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="8263e-160">Als het VPN-apparaat perfect forward secrecy is ingeschakeld heeft, moet u de functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="8263e-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="8263e-161">Werk vervolgens de VPN-gateway IPSec-beleid.</span><span class="sxs-lookup"><span data-stu-id="8263e-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8263e-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8263e-162">Next steps</span></span>

-   [<span data-ttu-id="8263e-163">Een site-naar-site-verbinding met een virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="8263e-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="8263e-164">Beleid voor IPsec/IKE voor site-naar-site VPN-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="8263e-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
