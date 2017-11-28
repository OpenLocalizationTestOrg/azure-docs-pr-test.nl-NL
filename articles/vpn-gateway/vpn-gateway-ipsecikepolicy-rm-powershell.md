---
title: 'IPsec/IKE-beleid voor S2S-VPN- of VNet-naar-VNet-verbindingen te configureren: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van beleid voor IPsec/IKE voor S2S of VNet-naar-VNet-verbindingen met Azure VPN-Gateways met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: 798014b6e8d4495db99ef2e2d2ea487ae7d02fd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="67911-103">Beleid voor IPsec/IKE voor S2S-VPN- of VNet-naar-VNet-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="67911-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="67911-104">Dit artikel begeleidt u bij de stappen voor het configureren van beleid voor IPsec/IKE voor Site-naar-Site VPN- of VNet-naar-VNet-verbindingen met het Resource Manager-implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67911-104">This article walks you through the steps to configure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="67911-105"><a name="about"></a>Informatie over IPsec en IKE beleidsparameters voor Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="67911-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="67911-106">IPsec en IKE-protocol standaard ondersteunt een groot aantal cryptografische algoritmen in verschillende combinaties.</span><span class="sxs-lookup"><span data-stu-id="67911-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="67911-107">Raadpleeg [over cryptografische vereisten en Azure VPN-gateways](vpn-gateway-about-compliance-crypto.md) om te zien hoe dit kan helpen waarborgen cross-premises en VNet-naar-VNet-connectiviteit voldoen aan uw vereisten voor naleving of beveiliging.</span><span class="sxs-lookup"><span data-stu-id="67911-107">Refer to [About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) to see how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="67911-108">Dit artikel bevat instructies voor het maken en een IPsec/IKE-beleid configureren en toepassen op een nieuwe of bestaande verbinding:</span><span class="sxs-lookup"><span data-stu-id="67911-108">This article provides instructions to create and configure an IPsec/IKE policy and apply to a new or existing connection:</span></span>

* [<span data-ttu-id="67911-109">Deel 1: werkstroom voor het maken en IPsec/IKE-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="67911-109">Part 1 - Workflow to create and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="67911-110">Deel 2 - ondersteund cryptografische algoritmen en de belangrijkste voordelen</span><span class="sxs-lookup"><span data-stu-id="67911-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="67911-111">Deel 3: een nieuwe S2S VPN-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="67911-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="67911-112">Deel 4: een nieuwe VNet-naar-VNet-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="67911-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="67911-113">Deel 5 - beheren (maken, toevoegen, verwijderen) IPsec/IKE-beleid voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="67911-114">Houd er rekening mee dat IPsec/IKE-beleid alleen op de volgende gateway-SKU's werkt:</span><span class="sxs-lookup"><span data-stu-id="67911-114">Note that IPsec/IKE policy only works on the following gateway SKUs:</span></span>
>    * <span data-ttu-id="67911-115">***VpnGw1, VpnGw2, VpnGw3*** (op route gebaseerd)</span><span class="sxs-lookup"><span data-stu-id="67911-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="67911-116">***Standaard*** en ***HighPerformance*** (op route gebaseerd)</span><span class="sxs-lookup"><span data-stu-id="67911-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="67911-117">U kunt maar ***één*** beleidscombinatie opgeven voor een bepaalde verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="67911-118">U moet alle algoritmen en parameters opgeven voor zowel IKE (hoofdmodus) en IPsec (snelle modus).</span><span class="sxs-lookup"><span data-stu-id="67911-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="67911-119">Gedeeltelijke beleidsspecificatie is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="67911-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="67911-120">Neem contact op met de VPN-leverancier apparaatspecificaties om te controleren of dat het beleid wordt ondersteund op uw on-premises VPN-apparaten.</span><span class="sxs-lookup"><span data-stu-id="67911-120">Consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="67911-121">S2S of VNet-naar-VNet-verbindingen kunnen niet tot stand brengen als het beleid niet compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="67911-121">S2S or VNet-to-VNet connections cannot establish if the policies are incompatible.</span></span>

## <span data-ttu-id="67911-122"><a name ="workflow"></a>Deel 1: werkstroom voor het maken en IPsec/IKE-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="67911-122"><a name ="workflow"></a>Part 1 - Workflow to create and set IPsec/IKE policy</span></span>
<span data-ttu-id="67911-123">Deze sectie geeft een overzicht van de werkstroom voor het maken en IPsec/IKE-beleid op een S2S VPN- of VNet-naar-VNet-verbinding bijwerken:</span><span class="sxs-lookup"><span data-stu-id="67911-123">This section outlines the workflow to create and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="67911-124">Een virtueel netwerk en een VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="67911-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="67911-125">Maak een lokale netwerkgateway voor cross-premises-verbinding of een ander virtueel netwerk en de gateway voor VNet-naar-VNet-verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="67911-126">Een beleid voor IPsec/IKE maken met geselecteerde algoritmen en parameters</span><span class="sxs-lookup"><span data-stu-id="67911-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="67911-127">Maak een verbinding (IPSec- of VNet2VNet) met het beleid voor IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="67911-127">Create a connection (IPsec or VNet2VNet) with the IPsec/IKE policy</span></span>
5. <span data-ttu-id="67911-128">Toevoegen/bijwerken/verwijderen uit een IPsec/IKE-beleid voor een bestaande verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="67911-129">De instructies in dit artikel helpt u bij het instellen en configureren van IPsec/IKE-beleid, zoals wordt weergegeven in het diagram:</span><span class="sxs-lookup"><span data-stu-id="67911-129">The instructions in this article helps you set up and configure IPsec/IKE policies as shown in the diagram:</span></span>

![ike-IPSec-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="67911-131"><a name ="params"></a>Deel 2 - ondersteund cryptografische algoritmen en kracht van</span><span class="sxs-lookup"><span data-stu-id="67911-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="67911-132">De volgende tabel bevat de ondersteunde cryptografische algoritmen en kracht kunnen worden geconfigureerd door de klanten:</span><span class="sxs-lookup"><span data-stu-id="67911-132">The following table lists the supported cryptographic algorithms and key strengths configurable by the customers:</span></span>

| <span data-ttu-id="67911-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="67911-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="67911-134">**Opties**</span><span class="sxs-lookup"><span data-stu-id="67911-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="67911-135">IKEv2-versleuteling</span><span class="sxs-lookup"><span data-stu-id="67911-135">IKEv2 Encryption</span></span> | <span data-ttu-id="67911-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="67911-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="67911-137">IKEv2-integriteit</span><span class="sxs-lookup"><span data-stu-id="67911-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="67911-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="67911-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="67911-139">DH-groep</span><span class="sxs-lookup"><span data-stu-id="67911-139">DH Group</span></span>         | <span data-ttu-id="67911-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, geen</span><span class="sxs-lookup"><span data-stu-id="67911-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="67911-141">IPsec-versleuteling</span><span class="sxs-lookup"><span data-stu-id="67911-141">IPsec Encryption</span></span> | <span data-ttu-id="67911-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, geen</span><span class="sxs-lookup"><span data-stu-id="67911-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="67911-143">IPsec-integriteit</span><span class="sxs-lookup"><span data-stu-id="67911-143">IPsec Integrity</span></span>  | <span data-ttu-id="67911-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="67911-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="67911-145">PFS-groep</span><span class="sxs-lookup"><span data-stu-id="67911-145">PFS Group</span></span>        | <span data-ttu-id="67911-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, geen</span><span class="sxs-lookup"><span data-stu-id="67911-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="67911-147">QM SA-levensduur</span><span class="sxs-lookup"><span data-stu-id="67911-147">QM SA Lifetime</span></span>   | <span data-ttu-id="67911-148">(**Optioneel**: standaardwaarden worden gebruikt als dat niet het opgegeven)</span><span class="sxs-lookup"><span data-stu-id="67911-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="67911-149">Seconden (geheel getal; **min. 300** /standaard 27000 seconden)</span><span class="sxs-lookup"><span data-stu-id="67911-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="67911-150">KB (geheel getal; **min. 1024**/standaard 102400000 KB)</span><span class="sxs-lookup"><span data-stu-id="67911-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="67911-151">Verkeersselector</span><span class="sxs-lookup"><span data-stu-id="67911-151">Traffic Selector</span></span> | <span data-ttu-id="67911-152">UsePolicyBasedTrafficSelectors ** ($True/$False; **Optioneel**, standaard $False als u niets opgeeft)</span><span class="sxs-lookup"><span data-stu-id="67911-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="67911-153">**Als GCMAES als voor IPsec-versleutelingsalgoritme wordt gebruikt, moet u de dezelfde GCMAES algoritme en de lengte van de sleutel selecteren voor IPSec-integriteit; bijvoorbeeld, met behulp van GCMAES128 voor beide**</span><span class="sxs-lookup"><span data-stu-id="67911-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select the same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="67911-154">SA-levensduur voor IKEv2 Main Mode staat vastgesteld op 28.800 seconden op de Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="67911-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on the Azure VPN gateways</span></span>
> 3. <span data-ttu-id="67911-155">'UsePolicyBasedTrafficSelectors' op $True instellen op een verbinding, wordt de Azure VPN-gateway verbinding maken met op beleid gebaseerde VPN-firewall on-premises configureren.</span><span class="sxs-lookup"><span data-stu-id="67911-155">Setting "UsePolicyBasedTrafficSelectors" to $True on a connection will configure the Azure VPN gateway to connect to policy-based VPN firewall on premises.</span></span> <span data-ttu-id="67911-156">Als u PolicyBasedTrafficSelectors inschakelt, moet u ervoor zorgen dat uw VPN-apparaat heeft de overeenkomende verkeer selectoren gedefinieerd met behulp van alle combinaties van uw on-premises voorvoegsels (lokale netwerkgateway) van de voorvoegsels virtuele Azure-netwerk in plaats van het netwerk any-to-any.</span><span class="sxs-lookup"><span data-stu-id="67911-156">If you enable PolicyBasedTrafficSelectors, you need to ensure your VPN device has the matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from the Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="67911-157">Als uw lokale netwerkvoorvoegsels bijvoorbeeld 10.1.0.0/16 en 10.2.0.0/16 zijn, en de voorvoegsels van uw virtuele netwerk 192.168.0.0/16 en 172.16.0.0/16, moet u de volgende verkeersselectoren opgeven:</span><span class="sxs-lookup"><span data-stu-id="67911-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need to specify the following traffic selectors:</span></span>
>    * <span data-ttu-id="67911-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="67911-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="67911-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="67911-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="67911-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="67911-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="67911-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="67911-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="67911-162">Zie voor meer informatie over op beleid gebaseerde verkeer selectoren [verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="67911-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="67911-163">De volgende tabel worden de bijbehorende Diffie-Hellman-groepen wordt ondersteund door het aangepaste beleid:</span><span class="sxs-lookup"><span data-stu-id="67911-163">The following table lists the corresponding Diffie-Hellman Groups supported by the custom policy:</span></span>

| <span data-ttu-id="67911-164">**Diffie-Hellman-groep**</span><span class="sxs-lookup"><span data-stu-id="67911-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="67911-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="67911-165">**DHGroup**</span></span>              | <span data-ttu-id="67911-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="67911-166">**PFSGroup**</span></span> | <span data-ttu-id="67911-167">**Sleutellengte**</span><span class="sxs-lookup"><span data-stu-id="67911-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="67911-168">1</span><span class="sxs-lookup"><span data-stu-id="67911-168">1</span></span>                         | <span data-ttu-id="67911-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="67911-169">DHGroup1</span></span>                 | <span data-ttu-id="67911-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="67911-170">PFS1</span></span>         | <span data-ttu-id="67911-171">768-bits MODP</span><span class="sxs-lookup"><span data-stu-id="67911-171">768-bit MODP</span></span>   |
| <span data-ttu-id="67911-172">2</span><span class="sxs-lookup"><span data-stu-id="67911-172">2</span></span>                         | <span data-ttu-id="67911-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="67911-173">DHGroup2</span></span>                 | <span data-ttu-id="67911-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="67911-174">PFS2</span></span>         | <span data-ttu-id="67911-175">1024-bits MODP</span><span class="sxs-lookup"><span data-stu-id="67911-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="67911-176">14</span><span class="sxs-lookup"><span data-stu-id="67911-176">14</span></span>                        | <span data-ttu-id="67911-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="67911-177">DHGroup14</span></span><br><span data-ttu-id="67911-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="67911-178">DHGroup2048</span></span> | <span data-ttu-id="67911-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="67911-179">PFS2048</span></span>      | <span data-ttu-id="67911-180">2048-bits MODP</span><span class="sxs-lookup"><span data-stu-id="67911-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="67911-181">19</span><span class="sxs-lookup"><span data-stu-id="67911-181">19</span></span>                        | <span data-ttu-id="67911-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="67911-182">ECP256</span></span>                   | <span data-ttu-id="67911-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="67911-183">ECP256</span></span>       | <span data-ttu-id="67911-184">256-bits ECP</span><span class="sxs-lookup"><span data-stu-id="67911-184">256-bit ECP</span></span>    |
| <span data-ttu-id="67911-185">20</span><span class="sxs-lookup"><span data-stu-id="67911-185">20</span></span>                        | <span data-ttu-id="67911-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="67911-186">ECP384</span></span>                   | <span data-ttu-id="67911-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="67911-187">ECP284</span></span>       | <span data-ttu-id="67911-188">384-bits ECP</span><span class="sxs-lookup"><span data-stu-id="67911-188">384-bit ECP</span></span>    |
| <span data-ttu-id="67911-189">24</span><span class="sxs-lookup"><span data-stu-id="67911-189">24</span></span>                        | <span data-ttu-id="67911-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="67911-190">DHGroup24</span></span>                | <span data-ttu-id="67911-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="67911-191">PFS24</span></span>        | <span data-ttu-id="67911-192">2048-bits MODP</span><span class="sxs-lookup"><span data-stu-id="67911-192">2048-bit MODP</span></span>  |

<span data-ttu-id="67911-193">Raadpleeg [RFC3526](https://tools.ietf.org/html/rfc3526) en [RFC5114](https://tools.ietf.org/html/rfc5114) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67911-193">Refer to [RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="67911-194"><a name ="crossprem"></a>Deel 3: een nieuwe S2S VPN-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="67911-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="67911-195">In deze sectie leidt u door de stappen voor het maken van een S2S VPN-verbinding met een IPsec/IKE-beleid.</span><span class="sxs-lookup"><span data-stu-id="67911-195">This section walks you through the steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="67911-196">De volgende stappen maakt de verbinding zoals weergegeven in het diagram:</span><span class="sxs-lookup"><span data-stu-id="67911-196">The following steps create the connection as shown in the diagram:</span></span>

![s2s-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="67911-198">Zie [een S2S VPN-verbinding](vpn-gateway-create-site-to-site-rm-powershell.md) voor stapsgewijze instructies gedetailleerde voor het maken van een S2S VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="67911-199"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="67911-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="67911-200">Controleer of u een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="67911-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="67911-201">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67911-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="67911-202">Installeer de Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="67911-202">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="67911-203">Zie [overzicht van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="67911-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <span data-ttu-id="67911-204"><a name="createvnet1"></a>Stap 1: het virtuele netwerk, de VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="67911-204"><a name="createvnet1"></a>Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="67911-205">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="67911-205">1. Declare your variables</span></span>

<span data-ttu-id="67911-206">Voor deze oefening eerst we onze variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="67911-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="67911-207">Zorg dat u de waarden door uw eigen waarden vervangt wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="67911-207">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="67911-208">2. Verbinding maken met uw abonnement en een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="67911-208">2. Connect to your subscription and create a new resource group</span></span>

<span data-ttu-id="67911-209">Zorg ervoor dat u overschakelt naar de PowerShell-modus als u de Resource Manager-cmdlets wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67911-209">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="67911-210">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67911-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="67911-211">Open de PowerShell-console en maak verbinding met uw account.</span><span class="sxs-lookup"><span data-stu-id="67911-211">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="67911-212">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="67911-212">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="67911-213">3. Het virtuele netwerk, de VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="67911-213">3. Create the virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="67911-214">Het volgende voorbeeld maakt het virtuele netwerk, TestVNet1 met drie subnetten en de VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="67911-214">The following sample creates the virtual network, TestVNet1, with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="67911-215">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="67911-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="67911-216">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="67911-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="67911-217"><a name="s2sconnection"></a>Stap 2: een S2S VPN-verbinding maken met een IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="67911-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="67911-218">1. Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="67911-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="67911-219">Het volgende voorbeeldscript wordt een beleid voor IPsec/IKE gemaakt met de volgende algoritmen en parameters:</span><span class="sxs-lookup"><span data-stu-id="67911-219">The following sample script creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>

* <span data-ttu-id="67911-220">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="67911-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="67911-221">IPsec: AES256, SHA256, PFS24, SA levensduur 7200 seconden & 2048KB</span><span class="sxs-lookup"><span data-stu-id="67911-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="67911-222">Als u GCMAES voor IPSec-authenticatie gebruikt, moet u de dezelfde GCMAES algoritme en de lengte van de sleutel voor de IPsec-codering en integriteit, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="67911-222">If you use GCMAES for IPsec, you must use the same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="67911-223">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="67911-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="67911-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA levensduur 7200 seconden & 2048 KB</span><span class="sxs-lookup"><span data-stu-id="67911-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-the-ipsecike-policy"></a><span data-ttu-id="67911-225">2. De S2S VPN-verbinding maken met het beleid voor IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="67911-225">2. Create the S2S VPN connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="67911-226">Maak een S2S VPN-verbinding en het eerder gemaakte IPsec/IKE-beleid toepassen.</span><span class="sxs-lookup"><span data-stu-id="67911-226">Create an S2S VPN connection and apply the IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="67911-227">U kunt optioneel toevoegen '-UsePolicyBasedTrafficSelectors $True ' aan de cmdlet van de verbinding maken inschakelen Azure VPN-gateway verbinding maken met op beleid gebaseerde VPN-apparaten on-premises, zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="67911-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" to the create connection cmdlet to enable Azure VPN gateway to connect to policy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67911-228">Als een beleid voor IPsec/IKE op een verbinding is opgegeven, wordt de Azure VPN-gateway alleen verzenden of de voorstel IPsec/IKE met opgegeven cryptografische algoritmen en de belangrijkste sterkte op die bepaalde verbinding accepteren.</span><span class="sxs-lookup"><span data-stu-id="67911-228">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="67911-229">Controleer of uw on-premises VPN-apparaat voor de verbinding wordt gebruikt of accepteert de combinatie exacte beleid anders de S2S VPN-tunnel niet tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="67911-229">Make sure your on-premises VPN device for the connection uses or accepts the exact policy combination, otherwise the S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="67911-230"><a name ="vnet2vnet"></a>Deel 4: een nieuwe VNet-naar-VNet-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="67911-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="67911-231">De stappen voor het maken van een VNet-naar-VNet-verbinding met een beleid voor IPsec/IKE zijn vergelijkbaar met die van een S2S VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-231">The steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar to that of a S2S VPN connection.</span></span> <span data-ttu-id="67911-232">De volgende voorbeeldscripts maken de verbinding, zoals weergegeven in het diagram:</span><span class="sxs-lookup"><span data-stu-id="67911-232">The following sample scripts create the connection as shown in the diagram:</span></span>

![V2V-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="67911-234">Zie [Maak een VNet-naar-VNet-verbinding](vpn-gateway-vnet-vnet-rm-ps.md) voor stappen gedetailleerde voor het maken van een VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="67911-235">U moet voltooien [deel 3](#crossprem) naar TestVNet1 en de VPN-Gateway maken en configureren.</span><span class="sxs-lookup"><span data-stu-id="67911-235">You must complete [Part 3](#crossprem) to create and configure TestVNet1 and the VPN Gateway.</span></span>

### <span data-ttu-id="67911-236"><a name="createvnet2"></a>Stap 1: het tweede virtuele netwerk en de VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="67911-236"><a name="createvnet2"></a>Step 1 - Create the second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="67911-237">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="67911-237">1. Declare your variables</span></span>

<span data-ttu-id="67911-238">Zorg ervoor dat u de waarden vervangt door de waarden die u voor uw configuratie wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67911-238">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-the-second-virtual-network-and-vpn-gateway-in-the-new-resource-group"></a><span data-ttu-id="67911-239">2. Het tweede virtuele netwerk en de VPN-gateway in de nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="67911-239">2. Create the second virtual network and VPN gateway in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-the-ipsecike-policy"></a><span data-ttu-id="67911-240">Stap 2: een VNet-toVNet verbinding maken met het beleid voor IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="67911-240">Step 2 - Create a VNet-toVNet connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="67911-241">Vergelijkbaar met de S2S VPN-verbinding, een IPsec/IKE-beleid maken en toepassen op beleid naar de nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-241">Similar to the S2S VPN connection, create an IPsec/IKE policy then apply to policy to the new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="67911-242">1. Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="67911-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="67911-243">Het volgende voorbeeldscript wordt een ander beleid voor IPsec/IKE gemaakt met de volgende algoritmen en parameters:</span><span class="sxs-lookup"><span data-stu-id="67911-243">The following sample script creates a different IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="67911-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="67911-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="67911-245">IPsec: GCMAES128, GCMAES128, PFS14, SA levensduur 7200 seconden en 4096KB</span><span class="sxs-lookup"><span data-stu-id="67911-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-the-ipsecike-policy"></a><span data-ttu-id="67911-246">2. VNet-naar-VNet-verbindingen maken met het beleid voor IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="67911-246">2. Create VNet-to-VNet connections with the IPsec/IKE policy</span></span>

<span data-ttu-id="67911-247">Een VNet-naar-VNet-verbinding maken en toepassen van de IPsec/IKE-beleid dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="67911-247">Create a VNet-to-VNet connection and apply the IPsec/IKE policy you created.</span></span> <span data-ttu-id="67911-248">In dit voorbeeld zijn beide gateways in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="67911-248">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="67911-249">Het is daarom mogelijk te maken en configureren van beide verbindingen met hetzelfde IPsec/IKE-beleid in dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="67911-249">So it is possible to create and configure both connections with the same IPsec/IKE policy in the same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="67911-250">Als een beleid voor IPsec/IKE op een verbinding is opgegeven, wordt de Azure VPN-gateway alleen verzenden of de voorstel IPsec/IKE met opgegeven cryptografische algoritmen en de belangrijkste sterkte op die bepaalde verbinding accepteren.</span><span class="sxs-lookup"><span data-stu-id="67911-250">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="67911-251">Zorg ervoor dat de IPSec-beleid voor beide verbindingen zijn hetzelfde, anders de VNet-naar-VNet-verbinding niet tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="67911-251">Make sure the IPsec policies for both connections are the same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="67911-252">De verbinding is gemaakt in een paar minuten en hebt u de volgende netwerktopologie zoals weergegeven in het begin na het voltooien van deze stappen:</span><span class="sxs-lookup"><span data-stu-id="67911-252">After completing these steps, the connection is established in a few minutes, and you will have the following network topology as shown in the beginning:</span></span>

![ike-IPSec-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="67911-254"><a name ="managepolicy"></a>Deel 5 - Update IPsec/IKE-beleid voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="67911-255">De laatste sectie leest u hoe voor het beheren van IPsec/IKE-beleid voor een bestaande S2S of VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-255">The last section shows you how to manage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="67911-256">De oefening hieronder wordt u begeleid bij de volgende bewerkingen uit op een verbinding:</span><span class="sxs-lookup"><span data-stu-id="67911-256">The exercise below walks you through the following operations on a connection:</span></span>

1. <span data-ttu-id="67911-257">Het beleid voor IPsec/IKE van een verbinding weergeven</span><span class="sxs-lookup"><span data-stu-id="67911-257">Show the IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="67911-258">Toevoegen of bijwerken van het beleid voor IPsec/IKE naar een verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-258">Add or update the IPsec/IKE policy to a connection</span></span>
3. <span data-ttu-id="67911-259">Het beleid voor IPsec/IKE verwijderen uit een verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-259">Remove the IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="67911-260">Dezelfde stappen van toepassing op S2S- en VNet-naar-VNet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="67911-260">The same steps apply to both S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67911-261">IPsec/IKE-beleid wordt ondersteund op *standaard* en *HighPerformance* op route gebaseerde VPN-gateways alleen.</span><span class="sxs-lookup"><span data-stu-id="67911-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="67911-262">Deze werkt niet op de standaard gateway-SKU of de op beleid gebaseerde VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="67911-262">It does not work on the Basic gateway SKU or the policy-based VPN gateway.</span></span>

#### <a name="1-show-the-ipsecike-policy-of-a-connection"></a><span data-ttu-id="67911-263">1. Het beleid voor IPsec/IKE van een verbinding weergeven</span><span class="sxs-lookup"><span data-stu-id="67911-263">1. Show the IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="67911-264">Het volgende voorbeeld laat zien hoe om de IPsec/IKE-beleid dat is geconfigureerd op een verbinding te krijgen.</span><span class="sxs-lookup"><span data-stu-id="67911-264">The following example shows how to get the IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="67911-265">De scripts blijven ook uit de bovenstaande oefeningen.</span><span class="sxs-lookup"><span data-stu-id="67911-265">The scripts also continue from the exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="67911-266">De laatste opdracht geeft het huidige IPsec/IKE-beleid dat is geconfigureerd op de verbinding indien deze aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="67911-266">The last command lists the current IPsec/IKE policy configured on the connection, if there is any.</span></span> <span data-ttu-id="67911-267">De volgende voorbeelduitvoer wordt voor de verbinding:</span><span class="sxs-lookup"><span data-stu-id="67911-267">The following sample output is for the connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="67911-268">Als er geen beleid voor IPsec/IKE geconfigureerd, de opdracht (PS > $connection6.policy) een leeg retourtype opgehaald.</span><span class="sxs-lookup"><span data-stu-id="67911-268">If there is no IPsec/IKE policy configured, the command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="67911-269">Dit betekent niet dat IPsec/IKE is niet geconfigureerd op de verbinding, maar er is geen aangepaste IPsec/IKE-beleid.</span><span class="sxs-lookup"><span data-stu-id="67911-269">It does not mean IPsec/IKE is not configured on the connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="67911-270">De huidige verbinding maakt gebruik van het standaardbeleid onderhandeld tussen uw on-premises VPN-apparaat en de Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="67911-270">The actual connection uses the default policy negotiated between your on-premises VPN device and the Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="67911-271">2. Toevoegen of bijwerken van een beleid voor IPsec/IKE voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="67911-272">De stappen voor het toevoegen van een nieuw beleid of een bestaand beleid op een verbinding bijwerken zijn hetzelfde: een nieuw beleid maken en vervolgens het nieuwe beleid toepassen op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="67911-272">The steps to add a new policy or update an existing policy on a connection are the same: create a new policy then apply the new policy to the connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="67911-273">Toevoegen om te schakelen "UsePolicyBasedTrafficSelectors" bij het verbinden met een on-premises op beleid gebaseerde VPN-apparaat, de '-UsePolicyBaseTrafficSelectors ' parameter aan de cmdlet, of stel deze in op $False de optie uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="67911-273">To enable "UsePolicyBasedTrafficSelectors" when connecting to an on-premises policy-based VPN device, add the "-UsePolicyBaseTrafficSelectors" parameter to the cmdlet, or set it to $False to disable the option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="67911-274">U kunt de verbinding opnieuw om te controleren als het beleid wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="67911-274">You can get the connection again to check if the policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="67911-275">U ziet de uitvoer van de laatste regel, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="67911-275">You should see the output from the last line, as shown in the following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="67911-276">3. Een beleid voor IPsec/IKE verwijderen uit een verbinding</span><span class="sxs-lookup"><span data-stu-id="67911-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="67911-277">Wanneer u het aangepaste beleid van een verbinding verwijdert, wordt de Azure VPN-gateway teruggedraaid naar de [standaardlijst met IPsec/IKE voorstellen](vpn-gateway-about-vpn-devices.md) en start een opnieuw nieuwe onderhandeling met uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="67911-277">Once you remove the custom policy from a connection, the Azure VPN gateway reverts back to the [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="67911-278">U kunt hetzelfde script gebruiken om te controleren als het beleid van de verbinding is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="67911-278">You can use the same script to check if the policy has been removed from the connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67911-279">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67911-279">Next steps</span></span>

<span data-ttu-id="67911-280">Zie [verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](vpn-gateway-connect-multiple-policybased-rm-ps.md) voor meer informatie over op beleid gebaseerde verkeer selectoren.</span><span class="sxs-lookup"><span data-stu-id="67911-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="67911-281">Wanneer de verbinding is voltooid, kunt u virtuele machines aan uw virtuele netwerken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="67911-281">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="67911-282">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="67911-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>