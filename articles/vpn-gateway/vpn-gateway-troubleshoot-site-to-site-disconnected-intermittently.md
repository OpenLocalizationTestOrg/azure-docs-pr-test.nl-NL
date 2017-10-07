---
title: Azure Site-naar-Site VPN-verbinding wordt verbroken afwisselend aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Hallo probleem in welke Hallo Site-naar-Site VPN-verbinding regelmatig wordt verbroken.
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
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="dc0c7-103">Voor probleemoplossing: Azure Site-naar-Site VPN-verbinding verbreekt met tussenpozen</span><span class="sxs-lookup"><span data-stu-id="dc0c7-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="dc0c7-104">U kunt problemen Hallo dat een nieuwe of bestaande Microsoft Azure punt-naar-Site VPN-verbinding niet stabiel is of regelmatig wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="dc0c7-105">Dit artikel vindt u stappen toohelp u identificeren en oplossen van Hallo oorzaak van Hallo probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="dc0c7-106">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="dc0c7-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="dc0c7-107">Vereiste stap</span><span class="sxs-lookup"><span data-stu-id="dc0c7-107">Prerequisite step</span></span>

<span data-ttu-id="dc0c7-108">Controleer Hallo type gateway voor virtuele Azure-netwerk:</span><span class="sxs-lookup"><span data-stu-id="dc0c7-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="dc0c7-109">Ga te[Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc0c7-110">Controleer de Hallo **overzicht** pagina van de virtuele netwerkgateway Hallo voor Hallo type informatie.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Hallo-overzicht van Hallo-gateway](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="dc0c7-112">Stap 1 Controleer of Hallo lokale VPN-apparaat wordt gevalideerd</span><span class="sxs-lookup"><span data-stu-id="dc0c7-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="dc0c7-113">Controleer of u een [gevalideerde VPN-apparaat en de versie van besturingssysteem](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="dc0c7-114">Als Hallo VPN-apparaat is niet gevalideerd, kunt u toocontact Hallo apparaat fabrikant toosee mogelijk als er een compatibiliteitsprobleem.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="dc0c7-115">Zorg ervoor dat het Hallo-VPN-apparaat correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="dc0c7-116">Zie voor meer informatie [bewerken van apparaatconfiguraties](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="dc0c7-117">Stap 2 selectievakje Hallo beveiligingskoppeling instellingen (voor gateways voor virtuele Azure-netwerk op basis van beleid)</span><span class="sxs-lookup"><span data-stu-id="dc0c7-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="dc0c7-118">Zorg ervoor dat dit Hallo virtuele netwerk, subnetten en bereiken in Hallo **lokale netwerkgateway** definitie in Microsoft Azure zijn hetzelfde als het Hallo-configuratie op Hallo on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="dc0c7-119">Controleer of overeenkomen met de instellingen van die Hallo beveiligingskoppeling.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="dc0c7-120">Stap 3-controle voor de gebruiker gedefinieerde Routes of Netwerkbeveiligingsgroepen van Gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="dc0c7-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="dc0c7-121">Een gebruiker gedefinieerde route op Hallo gatewaysubnet kan beperken sommige verkeer en andere verkeer toestaat.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="dc0c7-122">Op deze manier worden weergegeven dat Hallo VPN-verbinding voor verkeer onbetrouwbaar en geschikt is voor anderen.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="dc0c7-123">Stap 4 selectievakje 'een VPN-Tunnel per Subnet paar' Hallo instellen (voor gateways voor virtueel netwerk op basis van beleid)</span><span class="sxs-lookup"><span data-stu-id="dc0c7-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="dc0c7-124">Zorg ervoor dat Hallo lokale VPN-apparaat is ingesteld toohave **een VPN-tunnel per subnet paar** voor virtuele netwerkgateways op basis van beleid.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="dc0c7-125">Stap 5-controle voor beveiliging koppeling beperking (voor gateways voor virtueel netwerk op basis van beleid)</span><span class="sxs-lookup"><span data-stu-id="dc0c7-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="dc0c7-126">Hallo op beleid gebaseerde virtuele netwerkgateway heeft de limiet van 200 subnet beveiligingskoppeling paren.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="dc0c7-127">Als het aantal virtuele Azure-netwerksubnetten Hallo keren vermenigvuldigd door Hallo lokale subnetten aantal is groter dan 200, er sporadisch subnetten verbinding wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="dc0c7-128">Stap 6 Controleer on-premises VPN-apparaat externe Interfaceadres</span><span class="sxs-lookup"><span data-stu-id="dc0c7-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="dc0c7-129">Als hello Internetgericht IP-adres van Hallo VPN-apparaat is opgenomen in Hallo **lokale netwerkgateway** definitie in Azure, treden sporadisch worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="dc0c7-130">Hallo moet externe interface van het apparaat rechtstreeks op Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="dc0c7-131">Er zijn geen NAT (Network Address Translation) of firewall tussen Hallo Internet en het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="dc0c7-132">Als u op een virtueel IP-adres toohave Clustering Firewall configureert, moet u opsplitsen Hallo cluster en het Hallo-VPN-apparaat beschikbaar rechtstreeks tooa openbare interface die Hallo gateway kan verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="dc0c7-133">Stap 7 controle of Hallo lokale VPN-apparaat is Perfect Forward Secrecy ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="dc0c7-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="dc0c7-134">Hallo **Perfect Forward Secrecy** functie Hallo verbreken problemen kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="dc0c7-135">Als Hallo VPN-apparaat heeft **Perfect forward Secrecy** Hallo-functie ingeschakeld, uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="dc0c7-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="dc0c7-136">Vervolgens [Hallo virtueel netwerk gateway IPSec-beleid bijwerken](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="dc0c7-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc0c7-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc0c7-137">Next steps</span></span>

- [<span data-ttu-id="dc0c7-138">Een virtueel netwerk voor Site-naar-Site-verbinding tooa configureren</span><span class="sxs-lookup"><span data-stu-id="dc0c7-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="dc0c7-139">Beleid voor IPsec/IKE voor Site-naar-Site VPN-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="dc0c7-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

