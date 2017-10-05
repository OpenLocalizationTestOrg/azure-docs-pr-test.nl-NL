---
title: Problemen met Azure Site-naar-Site VPN-verbinding wordt verbroken afwisselend | Microsoft Docs
description: Informatie over het oplossen van het probleem waarin de Site-naar-Site VPN-verbinding regelmatig verbroken.
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="8bcbc-103">Voor probleemoplossing: Azure Site-naar-Site VPN-verbinding verbreekt met tussenpozen</span><span class="sxs-lookup"><span data-stu-id="8bcbc-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="8bcbc-104">U kunt het probleem dat in een nieuwe of bestaande Microsoft Azure punt-naar-Site VPN-verbinding niet stabiel is of de verbinding regelmatig verbreekt ondervinden.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="8bcbc-105">Dit artikel bevat stappen om te identificeren en oplossen van de oorzaak van het probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="8bcbc-106">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="8bcbc-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="8bcbc-107">Vereiste stap</span><span class="sxs-lookup"><span data-stu-id="8bcbc-107">Prerequisite step</span></span>

<span data-ttu-id="8bcbc-108">Controleer het type van de gateway virtuele Azure-netwerk:</span><span class="sxs-lookup"><span data-stu-id="8bcbc-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="8bcbc-109">Ga naar [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bcbc-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8bcbc-110">Controleer de **overzicht** pagina van de virtuele netwerkgateway voor de type-informatie.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![Het overzicht van de gateway](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="8bcbc-112">Stap 1 Controleer of de on-premises VPN-apparaat wordt gevalideerd</span><span class="sxs-lookup"><span data-stu-id="8bcbc-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="8bcbc-113">Controleer of u een [gevalideerde VPN-apparaat en de versie van besturingssysteem](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="8bcbc-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="8bcbc-114">Als het VPN-apparaat is niet gevalideerd, moet u wellicht contact op met de fabrikant van het apparaat om te zien of er een compatibiliteitsprobleem.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="8bcbc-115">Zorg ervoor dat het VPN-apparaat correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="8bcbc-116">Zie voor meer informatie [bewerken van apparaatconfiguraties](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="8bcbc-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="8bcbc-117">Stap 2 Controleer de instellingen van de beveiligingskoppeling (voor gateways voor virtuele Azure-netwerk op basis van beleid)</span><span class="sxs-lookup"><span data-stu-id="8bcbc-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="8bcbc-118">Zorg ervoor dat het virtuele netwerk, subnetten en bereiken in de **lokale netwerkgateway** definitie in Microsoft Azure zijn hetzelfde als de configuratie op de on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="8bcbc-119">Controleer of de instellingen van de beveiligingskoppeling die overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="8bcbc-120">Stap 3-controle voor de gebruiker gedefinieerde Routes of Netwerkbeveiligingsgroepen van Gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="8bcbc-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="8bcbc-121">Een gebruiker gedefinieerde route op het gatewaysubnet kan beperken sommige verkeer en andere verkeer toestaat.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="8bcbc-122">Op deze manier worden weergegeven dat de VPN-verbinding voor verkeer onbetrouwbaar en geschikt is voor anderen.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="8bcbc-123">Stap 4 controleren de 'een VPN-Tunnel per Subnet paar' (voor gateways voor virtueel netwerk op basis van beleid)</span><span class="sxs-lookup"><span data-stu-id="8bcbc-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="8bcbc-124">Zorg ervoor dat de on-premises VPN-apparaat is ingesteld om **een VPN-tunnel per subnet paar** voor virtuele netwerkgateways op basis van beleid.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="8bcbc-125">Stap 5-controle voor beveiliging koppeling beperking (voor gateways voor virtueel netwerk op basis van beleid)</span><span class="sxs-lookup"><span data-stu-id="8bcbc-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="8bcbc-126">De op beleid gebaseerde virtuele netwerkgateway heeft de limiet van 200 subnet beveiligingskoppeling paren.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="8bcbc-127">Als het aantal virtuele Azure-netwerksubnetten vermenigvuldigd tijden door het nummer van lokale subnetten is groter dan 200, er sporadisch subnetten verbinding wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="8bcbc-128">Stap 6 Controleer on-premises VPN-apparaat externe Interfaceadres</span><span class="sxs-lookup"><span data-stu-id="8bcbc-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="8bcbc-129">Als de IP-adres van het VPN-apparaat voor Internetgericht is opgenomen in de **lokale netwerkgateway** definitie in Azure, treden sporadisch worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="8bcbc-130">De externe interface van het apparaat moet rechtstreeks op het Internet.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="8bcbc-131">Er zijn geen NAT (Network Address Translation) of de firewall tussen het Internet en het apparaat.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="8bcbc-132">Als u Firewall Clustering als u wilt dat een virtueel IP-adres configureert, moet u het cluster opsplitsen en weergeven van de VPN-apparaat rechtstreeks naar een openbare interface die de gateway kan verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="8bcbc-133">Stap 7 Controleer of de on-premises VPN-apparaat Perfect Forward Secrecy ingeschakeld is</span><span class="sxs-lookup"><span data-stu-id="8bcbc-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="8bcbc-134">De **Perfect Forward Secrecy** functie kan leiden tot problemen met de verbinding wordt verbroken.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="8bcbc-135">Als het VPN-apparaat heeft **Perfect forward Secrecy** ingeschakeld, schakelt u de functie.</span><span class="sxs-lookup"><span data-stu-id="8bcbc-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="8bcbc-136">Vervolgens [bijwerken van de virtuele netwerkgateway IPSec-beleid](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="8bcbc-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bcbc-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bcbc-137">Next steps</span></span>

- [<span data-ttu-id="8bcbc-138">Een Site-naar-Site-verbinding met een virtueel netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="8bcbc-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="8bcbc-139">Beleid voor IPsec/IKE voor Site-naar-Site VPN-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="8bcbc-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

