---
title: Voorbeeldconfiguratie - Cisco ASA apparaat verbinding te maken met Azure VPN-gateways | Microsoft Docs
description: Dit artikel bevat een voorbeeldconfiguratie voor Cisco ASA apparaat verbinding te maken met Azure VPN-gateways.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="c13dc-103">Voorbeeldconfiguratie: Cisco ASA apparaat (BGP IKEv2/Nee)</span><span class="sxs-lookup"><span data-stu-id="c13dc-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="c13dc-104">Dit artikel vindt voorbeelden van configuraties voor Cisco ASA-apparaten die verbinding maken met Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="c13dc-104">This article provides sample configurations for Cisco ASA devices connecting to Azure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="c13dc-105">Apparaat in een oogopslag</span><span class="sxs-lookup"><span data-stu-id="c13dc-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="c13dc-106">De leverancier van apparaat</span><span class="sxs-lookup"><span data-stu-id="c13dc-106">Device vendor</span></span>          | <span data-ttu-id="c13dc-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="c13dc-107">Cisco</span></span>                             |
| <span data-ttu-id="c13dc-108">Apparaatmodel</span><span class="sxs-lookup"><span data-stu-id="c13dc-108">Device model</span></span>           | <span data-ttu-id="c13dc-109">ASA (adaptieve beveiliging toestel)</span><span class="sxs-lookup"><span data-stu-id="c13dc-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="c13dc-110">Doelversie</span><span class="sxs-lookup"><span data-stu-id="c13dc-110">Target version</span></span>         | <span data-ttu-id="c13dc-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="c13dc-111">8.4+</span></span>                              |
| <span data-ttu-id="c13dc-112">Geteste model</span><span class="sxs-lookup"><span data-stu-id="c13dc-112">Tested model</span></span>           | <span data-ttu-id="c13dc-113">5505 ASA</span><span class="sxs-lookup"><span data-stu-id="c13dc-113">ASA 5505</span></span>                          |
| <span data-ttu-id="c13dc-114">Geteste versie</span><span class="sxs-lookup"><span data-stu-id="c13dc-114">Tested version</span></span>         | <span data-ttu-id="c13dc-115">9.2</span><span class="sxs-lookup"><span data-stu-id="c13dc-115">9.2</span></span>                               |
| <span data-ttu-id="c13dc-116">IKE-versie</span><span class="sxs-lookup"><span data-stu-id="c13dc-116">IKE version</span></span>            | <span data-ttu-id="c13dc-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="c13dc-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="c13dc-118">BGP</span><span class="sxs-lookup"><span data-stu-id="c13dc-118">BGP</span></span>                    | <span data-ttu-id="c13dc-119">**Nee**</span><span class="sxs-lookup"><span data-stu-id="c13dc-119">**No**</span></span>                            |
| <span data-ttu-id="c13dc-120">Azure VPN-gateway-type</span><span class="sxs-lookup"><span data-stu-id="c13dc-120">Azure VPN gateway type</span></span> | <span data-ttu-id="c13dc-121">**Op route gebaseerde** VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="c13dc-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="c13dc-122">De onderstaande configuratie een Cisco ASA-apparaat verbindt met een Azure **op route gebaseerde** VPN-gateway met behulp van aangepaste IPsec/IKE-beleid met de optie 'UserPolicyBasedTrafficSelectors', zoals beschreven in [in dit artikel](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c13dc-122">The configuration below connects a Cisco ASA device to an Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="c13dc-123">Hiervoor ASA-apparaten **IKEv2** met configuraties toegang lijst is gebaseerd op VTI basis niet.</span><span class="sxs-lookup"><span data-stu-id="c13dc-123">It requires ASA devices to use **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="c13dc-124">Neem contact op met de VPN-leverancier apparaatspecificaties om te controleren of dat het beleid wordt ondersteund op uw on-premises VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="c13dc-124">Please consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="c13dc-125">Vereisten voor VPN-apparaten</span><span class="sxs-lookup"><span data-stu-id="c13dc-125">VPN device requirements</span></span>
<span data-ttu-id="c13dc-126">Azure VPN-gateways gebruiken standaard IPsec/IKE-protocol suites voor S2S-VPN-tunnels tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c13dc-126">Azure VPN gateways use standard IPsec/IKE protocol suites to establish S2S VPN tunnels.</span></span> <span data-ttu-id="c13dc-127">Raadpleeg [over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor de parameters van gedetailleerde IPsec/IKE-protocol en de standaard cryptografische algoritmen voor Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="c13dc-127">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="c13dc-128">U kunt optioneel de exacte combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="c13dc-128">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="c13dc-129">Als u een specifieke combinatie van cryptografische algoritmen en de belangrijkste sterkte selecteert, Controleer of dat u de overeenkomstige specificaties gebruiken op uw VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="c13dc-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use the corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="c13dc-130">Één VPN-tunnel</span><span class="sxs-lookup"><span data-stu-id="c13dc-130">Single VPN tunnel</span></span>
<span data-ttu-id="c13dc-131">Deze topologie bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c13dc-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="c13dc-132">U kunt desgewenst BGP configureren via de VPN-tunnel.</span><span class="sxs-lookup"><span data-stu-id="c13dc-132">You can optionally configure BGP across the VPN tunnel.</span></span>

![één tunnel](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="c13dc-134">Raadpleeg [één tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) voor gedetailleerde, stapsgewijze instructies voor het bouwen van de Azure-configuraties.</span><span class="sxs-lookup"><span data-stu-id="c13dc-134">Refer to [Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions to build the Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="c13dc-135">Gegevens voor netwerk- en VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="c13dc-135">Network and VPN gateway information</span></span>
<span data-ttu-id="c13dc-136">Deze sectie lijst met de parameters voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c13dc-136">This section list the parameters for the this sample.</span></span>

| <span data-ttu-id="c13dc-137">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="c13dc-137">**Parameter**</span></span>                | <span data-ttu-id="c13dc-138">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="c13dc-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="c13dc-139">VNet-adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="c13dc-139">VNet address prefixes</span></span>        | <span data-ttu-id="c13dc-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c13dc-140">10.11.0.0/16</span></span><br><span data-ttu-id="c13dc-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c13dc-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="c13dc-142">Azure VPN-gateway-IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="c13dc-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="c13dc-144">Lokale adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="c13dc-144">On-premises address prefixes</span></span> | <span data-ttu-id="c13dc-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c13dc-145">10.51.0.0/16</span></span><br><span data-ttu-id="c13dc-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c13dc-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="c13dc-147">Lokale VPN-apparaat IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="c13dc-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="c13dc-149">* VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="c13dc-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="c13dc-150">65010</span><span class="sxs-lookup"><span data-stu-id="c13dc-150">65010</span></span>                        |
| <span data-ttu-id="c13dc-151">* Azure BGP-peer-IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="c13dc-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="c13dc-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="c13dc-153">* On-premises BGP ASN</span><span class="sxs-lookup"><span data-stu-id="c13dc-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="c13dc-154">65050</span><span class="sxs-lookup"><span data-stu-id="c13dc-154">65050</span></span>                        |
| <span data-ttu-id="c13dc-155">* On-premises BGP-peer-IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="c13dc-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="c13dc-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="c13dc-157">(*) Optionele parameters voor BGP alleen.</span><span class="sxs-lookup"><span data-stu-id="c13dc-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="c13dc-158">Beleid voor IPsec/IKE & parameters</span><span class="sxs-lookup"><span data-stu-id="c13dc-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="c13dc-159">De volgende tabel bevat de IPsec/IKE-algoritmen en parameters die worden gebruikt in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c13dc-159">The table below lists the IPsec/IKE algorithms and parameters used in the sample.</span></span> <span data-ttu-id="c13dc-160">Neem contact op met uw VPN-apparaatspecificaties om ervoor te zorgen dat alle hierboven vermelde-algoritmen worden ondersteund door uw VPN-apparaatmodellen en firmware-versies.</span><span class="sxs-lookup"><span data-stu-id="c13dc-160">Please consult your VPN device specifications to make sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="c13dc-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="c13dc-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="c13dc-162">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="c13dc-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="c13dc-163">IKEv2-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c13dc-163">IKEv2 Encryption</span></span> | <span data-ttu-id="c13dc-164">AES256</span><span class="sxs-lookup"><span data-stu-id="c13dc-164">AES256</span></span>                               |
| <span data-ttu-id="c13dc-165">IKEv2-integriteit</span><span class="sxs-lookup"><span data-stu-id="c13dc-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="c13dc-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="c13dc-166">SHA384</span></span>                               |
| <span data-ttu-id="c13dc-167">DH-groep</span><span class="sxs-lookup"><span data-stu-id="c13dc-167">DH Group</span></span>         | <span data-ttu-id="c13dc-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="c13dc-168">DHGroup24</span></span>                            |
| <span data-ttu-id="c13dc-169">IPsec-versleuteling</span><span class="sxs-lookup"><span data-stu-id="c13dc-169">IPsec Encryption</span></span> | <span data-ttu-id="c13dc-170">AES256</span><span class="sxs-lookup"><span data-stu-id="c13dc-170">AES256</span></span>                               |
| <span data-ttu-id="c13dc-171">IPsec-integriteit</span><span class="sxs-lookup"><span data-stu-id="c13dc-171">IPsec Integrity</span></span>  | <span data-ttu-id="c13dc-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="c13dc-172">SHA1</span></span>                                 |
| <span data-ttu-id="c13dc-173">PFS-groep</span><span class="sxs-lookup"><span data-stu-id="c13dc-173">PFS Group</span></span>        | <span data-ttu-id="c13dc-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="c13dc-174">PFS24</span></span>                                |
| <span data-ttu-id="c13dc-175">QM SA-levensduur</span><span class="sxs-lookup"><span data-stu-id="c13dc-175">QM SA Lifetime</span></span>   | <span data-ttu-id="c13dc-176">7200 seconden</span><span class="sxs-lookup"><span data-stu-id="c13dc-176">7200 seconds</span></span>                         |
| <span data-ttu-id="c13dc-177">Verkeersselector</span><span class="sxs-lookup"><span data-stu-id="c13dc-177">Traffic Selector</span></span> | <span data-ttu-id="c13dc-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="c13dc-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="c13dc-179">Vooraf gedeelde sleutel</span><span class="sxs-lookup"><span data-stu-id="c13dc-179">Pre-Shared Key</span></span>   | <span data-ttu-id="c13dc-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="c13dc-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="c13dc-181">(*) Op sommige apparaten moet IPSec-integriteit 'null' als GCM-AES wordt gebruikt als de IPsec-versleutelingsalgoritme.</span><span class="sxs-lookup"><span data-stu-id="c13dc-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="c13dc-182">Opmerkingen bij de apparaten</span><span class="sxs-lookup"><span data-stu-id="c13dc-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="c13dc-183">IKEv2-ondersteuning vereist ASA versie 8.4 en hoger.</span><span class="sxs-lookup"><span data-stu-id="c13dc-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="c13dc-184">Ondersteuning voor hogere DH en PFS (anders dan de groep 5) is de ASA-versie vereist 9.x.</span><span class="sxs-lookup"><span data-stu-id="c13dc-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="c13dc-185">IPSec-codering met AES-GCM en IPSec-integriteit met SHA-256, SHA-384 en SHA-512 ondersteuning vereist ASA versie 9.x op nieuwere ASA hardware; 5505 ASA, 5510, 5520, 5540, 5550, 5580 zijn **niet** ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c13dc-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="c13dc-186">(Controleer of de Leverancierspecificaties om te bevestigen.)</span><span class="sxs-lookup"><span data-stu-id="c13dc-186">(Please check the vendor specifications to confirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="c13dc-187">Voorbeeld apparaatconfiguraties</span><span class="sxs-lookup"><span data-stu-id="c13dc-187">Sample device configurations</span></span>
<span data-ttu-id="c13dc-188">Het onderstaande script geeft een voorbeeldconfiguratie op basis van de topologie en de hierboven vermelde parameters.</span><span class="sxs-lookup"><span data-stu-id="c13dc-188">The script below provides a sample configuration based on the topology and parameters listed above.</span></span> <span data-ttu-id="c13dc-189">De configuratie van de S2S VPN-tunnel bestaat uit de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="c13dc-189">The S2S VPN tunnel configuration consists of the following parts:</span></span>

1. <span data-ttu-id="c13dc-190">Interfaces & routes</span><span class="sxs-lookup"><span data-stu-id="c13dc-190">Interfaces & routes</span></span>
2. <span data-ttu-id="c13dc-191">Een lijst met toegang</span><span class="sxs-lookup"><span data-stu-id="c13dc-191">Access lists</span></span>
3. <span data-ttu-id="c13dc-192">IKE-beleid en de parameters (fase 1 of hoofdmodus)</span><span class="sxs-lookup"><span data-stu-id="c13dc-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="c13dc-193">IPSec-beleid en de parameters (fase 2 of snelle modus)</span><span class="sxs-lookup"><span data-stu-id="c13dc-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="c13dc-194">Andere parameters (TCP MSS clamping, enz.)</span><span class="sxs-lookup"><span data-stu-id="c13dc-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c13dc-195">Controleer of u de aanvullende configuratie hieronder vermelde voltooien en vervang de tijdelijke aanduidingen door de werkelijke waarden:</span><span class="sxs-lookup"><span data-stu-id="c13dc-195">Please make sure you complete the additional configuration listed below and replace the placeholders with the actual values:</span></span>
> 
> - <span data-ttu-id="c13dc-196">Configuratie voor zowel binnen als buiten interfaces interface</span><span class="sxs-lookup"><span data-stu-id="c13dc-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="c13dc-197">Routes voor uw binnen en persoonlijke en buiten/openbare netwerken</span><span class="sxs-lookup"><span data-stu-id="c13dc-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="c13dc-198">Zorg ervoor dat alle namen en getallen beleid zijn uniek op het apparaat</span><span class="sxs-lookup"><span data-stu-id="c13dc-198">Ensure all names and policy numbers are unique on the device</span></span>
> - <span data-ttu-id="c13dc-199">Zorg ervoor dat de cryptografische algoritmen worden ondersteund op uw apparaat</span><span class="sxs-lookup"><span data-stu-id="c13dc-199">Ensure the cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="c13dc-200">De volgende plaats houders vervangen door de werkelijke waarden</span><span class="sxs-lookup"><span data-stu-id="c13dc-200">Replace the following place holders with the actual values</span></span>
>   - <span data-ttu-id="c13dc-201">Buiten Interfacenaam: 'externe'</span><span class="sxs-lookup"><span data-stu-id="c13dc-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="c13dc-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="c13dc-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c13dc-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="c13dc-204">IKE-Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="c13dc-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="c13dc-205">VNet en lokale gateway netwerknamen (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="c13dc-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="c13dc-206">VNet- en on-premises netwerk adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="c13dc-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="c13dc-207">Juiste netmaskers</span><span class="sxs-lookup"><span data-stu-id="c13dc-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="c13dc-208">Voorbeeldconfiguratie</span><span class="sxs-lookup"><span data-stu-id="c13dc-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="c13dc-209">Eenvoudige foutopsporing opdrachten</span><span class="sxs-lookup"><span data-stu-id="c13dc-209">Simple debugging commands</span></span>

<span data-ttu-id="c13dc-210">Hier volgen enkele ASA-opdrachten voor foutopsporing:</span><span class="sxs-lookup"><span data-stu-id="c13dc-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="c13dc-211">IPsec en IKE-SA weergeven</span><span class="sxs-lookup"><span data-stu-id="c13dc-211">Show the IPsec and IKE SA's</span></span>
    - <span data-ttu-id="c13dc-212">' weergeven crypto ipsec sa '</span><span class="sxs-lookup"><span data-stu-id="c13dc-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="c13dc-213">' weergeven crypto ikev2 sa '</span><span class="sxs-lookup"><span data-stu-id="c13dc-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="c13dc-214">Invoeren foutopsporingsmodus - dit zeer veel ruis veroorzaken kunt krijgen op de console</span><span class="sxs-lookup"><span data-stu-id="c13dc-214">Entering debug mode - this can get very noisy on the console</span></span>
    - <span data-ttu-id="c13dc-215">' debug crypto ikev2 platform <level>'</span><span class="sxs-lookup"><span data-stu-id="c13dc-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="c13dc-216">' debug crypto ikev2 protocol <level>'</span><span class="sxs-lookup"><span data-stu-id="c13dc-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="c13dc-217">Lijst met huidige configuraties</span><span class="sxs-lookup"><span data-stu-id="c13dc-217">List current configurations</span></span>
    - <span data-ttu-id="c13dc-218">'show uitvoeren' - ziet u de huidige configuraties op het apparaat. u kunt de verschillende onderliggende opdrachten voor het specifieke onderdelen van de lijst van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="c13dc-218">"show run" - shows the current configurations on the device; you can use the various sub-commands to list specific parts of the configuration.</span></span> <span data-ttu-id="c13dc-219">Bijvoorbeeld 'crypto-presentatie', 'weergeven die worden uitgevoerd toegang-list', 'uitvoeren tunnel-groep weergeven', enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c13dc-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c13dc-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c13dc-220">Next steps</span></span>
<span data-ttu-id="c13dc-221">Zie [Actief/actief VPN-gateways configureren voor cross-premises en VNet-naar-VNet-verbindingen](vpn-gateway-activeactive-rm-powershell.md) voor de stappen om actief/actief on-premises en VNet-naar-VNet-verbindingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="c13dc-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

