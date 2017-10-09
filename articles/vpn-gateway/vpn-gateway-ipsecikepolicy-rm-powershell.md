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
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="02cc9-103">Beleid voor IPsec/IKE voor S2S-VPN- of VNet-naar-VNet-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="02cc9-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="02cc9-104">Dit artikel begeleidt u bij Hallo stappen tooconfigure IPsec/IKE-beleid voor Site-naar-Site VPN- of VNet-naar-VNet-verbindingen met Hallo Resource Manager-implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02cc9-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="02cc9-105"><a name="about"></a>Informatie over IPsec en IKE beleidsparameters voor Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="02cc9-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="02cc9-106">IPsec en IKE-protocol standaard ondersteunt een groot aantal cryptografische algoritmen in verschillende combinaties.</span><span class="sxs-lookup"><span data-stu-id="02cc9-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="02cc9-107">Raadpleeg te[over cryptografische vereisten en Azure VPN-gateways](vpn-gateway-about-compliance-crypto.md) toosee hoe dit kan helpen waarborgen cross-premises en VNet-naar-VNet-connectiviteit voldoen aan uw vereisten voor naleving of beveiliging.</span><span class="sxs-lookup"><span data-stu-id="02cc9-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="02cc9-108">In dit artikel biedt instructies toocreate en een IPsec/IKE-beleid configureren en toepassen van de nieuwe of bestaande verbinding tooa:</span><span class="sxs-lookup"><span data-stu-id="02cc9-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="02cc9-109">Deel 1 - werkstroom toocreate en IPsec/IKE-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="02cc9-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="02cc9-110">Deel 2 - ondersteund cryptografische algoritmen en de belangrijkste voordelen</span><span class="sxs-lookup"><span data-stu-id="02cc9-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="02cc9-111">Deel 3: een nieuwe S2S VPN-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="02cc9-112">Deel 4: een nieuwe VNet-naar-VNet-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="02cc9-113">Deel 5 - beheren (maken, toevoegen, verwijderen) IPsec/IKE-beleid voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="02cc9-114">Houd er rekening mee dat IPsec/IKE-beleid alleen werkt op Hallo gateway-SKU's te volgen:</span><span class="sxs-lookup"><span data-stu-id="02cc9-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="02cc9-115">***VpnGw1, VpnGw2, VpnGw3*** (op route gebaseerd)</span><span class="sxs-lookup"><span data-stu-id="02cc9-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="02cc9-116">***Standaard*** en ***HighPerformance*** (op route gebaseerd)</span><span class="sxs-lookup"><span data-stu-id="02cc9-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="02cc9-117">U kunt maar ***één*** beleidscombinatie opgeven voor een bepaalde verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="02cc9-118">U moet alle algoritmen en parameters opgeven voor zowel IKE (hoofdmodus) en IPsec (snelle modus).</span><span class="sxs-lookup"><span data-stu-id="02cc9-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="02cc9-119">Gedeeltelijke beleidsspecificatie is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="02cc9-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="02cc9-120">Neem contact op met uw VPN-apparaat Leverancierspecificaties tooensure Hallo beleid op uw on-premises VPN-apparaten wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="02cc9-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="02cc9-121">S2S of VNet-naar-VNet-verbindingen kunnen niet tot stand brengen als Hallo beleid niet compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="02cc9-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="02cc9-122"><a name ="workflow"></a>Deel 1 - werkstroom toocreate en IPsec/IKE-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="02cc9-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="02cc9-123">Deze sectie geeft een overzicht van Hallo werkstroom toocreate en update IPsec/IKE-beleid op een S2S VPN- of VNet-naar-VNet-verbinding:</span><span class="sxs-lookup"><span data-stu-id="02cc9-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="02cc9-124">Een virtueel netwerk en een VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="02cc9-125">Maak een lokale netwerkgateway voor cross-premises-verbinding of een ander virtueel netwerk en de gateway voor VNet-naar-VNet-verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="02cc9-126">Een beleid voor IPsec/IKE maken met geselecteerde algoritmen en parameters</span><span class="sxs-lookup"><span data-stu-id="02cc9-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="02cc9-127">Maak een verbinding (IPSec- of VNet2VNet) met Hallo IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="02cc9-128">Toevoegen/bijwerken/verwijderen uit een IPsec/IKE-beleid voor een bestaande verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="02cc9-129">Hallo-instructies in dit artikel helpt u bij het instellen en configureren van beleid voor IPsec/IKE zoals u in Hallo diagram:</span><span class="sxs-lookup"><span data-stu-id="02cc9-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ike-IPSec-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="02cc9-131"><a name ="params"></a>Deel 2 - ondersteund cryptografische algoritmen en kracht van</span><span class="sxs-lookup"><span data-stu-id="02cc9-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="02cc9-132">Hallo volgende tabel bevat Hallo ondersteund cryptografische algoritmen en kracht kunnen worden geconfigureerd door Hallo-klanten:</span><span class="sxs-lookup"><span data-stu-id="02cc9-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="02cc9-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="02cc9-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="02cc9-134">**Opties**</span><span class="sxs-lookup"><span data-stu-id="02cc9-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="02cc9-135">IKEv2-versleuteling</span><span class="sxs-lookup"><span data-stu-id="02cc9-135">IKEv2 Encryption</span></span> | <span data-ttu-id="02cc9-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="02cc9-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="02cc9-137">IKEv2-integriteit</span><span class="sxs-lookup"><span data-stu-id="02cc9-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="02cc9-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="02cc9-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="02cc9-139">DH-groep</span><span class="sxs-lookup"><span data-stu-id="02cc9-139">DH Group</span></span>         | <span data-ttu-id="02cc9-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, geen</span><span class="sxs-lookup"><span data-stu-id="02cc9-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="02cc9-141">IPsec-versleuteling</span><span class="sxs-lookup"><span data-stu-id="02cc9-141">IPsec Encryption</span></span> | <span data-ttu-id="02cc9-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, geen</span><span class="sxs-lookup"><span data-stu-id="02cc9-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="02cc9-143">IPsec-integriteit</span><span class="sxs-lookup"><span data-stu-id="02cc9-143">IPsec Integrity</span></span>  | <span data-ttu-id="02cc9-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="02cc9-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="02cc9-145">PFS-groep</span><span class="sxs-lookup"><span data-stu-id="02cc9-145">PFS Group</span></span>        | <span data-ttu-id="02cc9-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, geen</span><span class="sxs-lookup"><span data-stu-id="02cc9-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="02cc9-147">QM SA-levensduur</span><span class="sxs-lookup"><span data-stu-id="02cc9-147">QM SA Lifetime</span></span>   | <span data-ttu-id="02cc9-148">(**Optioneel**: standaardwaarden worden gebruikt als dat niet het opgegeven)</span><span class="sxs-lookup"><span data-stu-id="02cc9-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="02cc9-149">Seconden (geheel getal; **min. 300** /standaard 27000 seconden)</span><span class="sxs-lookup"><span data-stu-id="02cc9-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="02cc9-150">KB (geheel getal; **min. 1024**/standaard 102400000 KB)</span><span class="sxs-lookup"><span data-stu-id="02cc9-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="02cc9-151">Verkeersselector</span><span class="sxs-lookup"><span data-stu-id="02cc9-151">Traffic Selector</span></span> | <span data-ttu-id="02cc9-152">UsePolicyBasedTrafficSelectors ** ($True/$False; **Optioneel**, standaard $False als u niets opgeeft)</span><span class="sxs-lookup"><span data-stu-id="02cc9-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="02cc9-153">**Als GCMAES als voor IPsec-versleutelingsalgoritme wordt gebruikt, moet u dezelfde GCMAES algoritme en de sleutellengte Hallo voor IPSec-integriteit; bijvoorbeeld, met behulp van GCMAES128 voor beide**</span><span class="sxs-lookup"><span data-stu-id="02cc9-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="02cc9-154">Levensduur voor de Hoofdmodus IKEv2 wordt vastgesteld op 28.800 seconden op Hallo Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="02cc9-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="02cc9-155">Instelling 'UsePolicyBasedTrafficSelectors' te$ True voor een verbinding configureert hello Azure VPN-gateway tooconnect toopolicy gebaseerde VPN-firewall on-premises.</span><span class="sxs-lookup"><span data-stu-id="02cc9-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="02cc9-156">Als u PolicyBasedTrafficSelectors inschakelt, moet u uw VPN-apparaat Hallo overeenkomende verkeer selectoren gedefinieerd met behulp van alle combinaties van uw lokale netwerk (lokale netwerkgateway) voorvoegsels van voorvoegsels Hallo virtuele Azure-netwerk heeft, tooensure in plaats van any-to-any.</span><span class="sxs-lookup"><span data-stu-id="02cc9-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="02cc9-157">Als uw lokale netwerkvoorvoegsels 10.1.0.0/16 en 10.2.0.0/16 zijn, en de voorvoegsels van uw virtuele netwerk 192.168.0.0/16 en 172.16.0.0/16 zijn, moet u bijvoorbeeld toospecify Hallo verkeer selectoren te volgen:</span><span class="sxs-lookup"><span data-stu-id="02cc9-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="02cc9-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="02cc9-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="02cc9-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="02cc9-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="02cc9-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="02cc9-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="02cc9-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="02cc9-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="02cc9-162">Zie voor meer informatie over op beleid gebaseerde verkeer selectoren [verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="02cc9-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="02cc9-163">Hallo volgende Tabellijsten Hallo bijbehorende Diffie-Hellman-groepen die worden ondersteund door het aangepaste beleid Hallo:</span><span class="sxs-lookup"><span data-stu-id="02cc9-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="02cc9-164">**Diffie-Hellman-groep**</span><span class="sxs-lookup"><span data-stu-id="02cc9-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="02cc9-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="02cc9-165">**DHGroup**</span></span>              | <span data-ttu-id="02cc9-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="02cc9-166">**PFSGroup**</span></span> | <span data-ttu-id="02cc9-167">**Sleutellengte**</span><span class="sxs-lookup"><span data-stu-id="02cc9-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="02cc9-168">1</span><span class="sxs-lookup"><span data-stu-id="02cc9-168">1</span></span>                         | <span data-ttu-id="02cc9-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="02cc9-169">DHGroup1</span></span>                 | <span data-ttu-id="02cc9-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="02cc9-170">PFS1</span></span>         | <span data-ttu-id="02cc9-171">768-bits MODP</span><span class="sxs-lookup"><span data-stu-id="02cc9-171">768-bit MODP</span></span>   |
| <span data-ttu-id="02cc9-172">2</span><span class="sxs-lookup"><span data-stu-id="02cc9-172">2</span></span>                         | <span data-ttu-id="02cc9-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="02cc9-173">DHGroup2</span></span>                 | <span data-ttu-id="02cc9-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="02cc9-174">PFS2</span></span>         | <span data-ttu-id="02cc9-175">1024-bits MODP</span><span class="sxs-lookup"><span data-stu-id="02cc9-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="02cc9-176">14</span><span class="sxs-lookup"><span data-stu-id="02cc9-176">14</span></span>                        | <span data-ttu-id="02cc9-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="02cc9-177">DHGroup14</span></span><br><span data-ttu-id="02cc9-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="02cc9-178">DHGroup2048</span></span> | <span data-ttu-id="02cc9-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="02cc9-179">PFS2048</span></span>      | <span data-ttu-id="02cc9-180">2048-bits MODP</span><span class="sxs-lookup"><span data-stu-id="02cc9-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="02cc9-181">19</span><span class="sxs-lookup"><span data-stu-id="02cc9-181">19</span></span>                        | <span data-ttu-id="02cc9-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="02cc9-182">ECP256</span></span>                   | <span data-ttu-id="02cc9-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="02cc9-183">ECP256</span></span>       | <span data-ttu-id="02cc9-184">256-bits ECP</span><span class="sxs-lookup"><span data-stu-id="02cc9-184">256-bit ECP</span></span>    |
| <span data-ttu-id="02cc9-185">20</span><span class="sxs-lookup"><span data-stu-id="02cc9-185">20</span></span>                        | <span data-ttu-id="02cc9-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="02cc9-186">ECP384</span></span>                   | <span data-ttu-id="02cc9-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="02cc9-187">ECP284</span></span>       | <span data-ttu-id="02cc9-188">384-bits ECP</span><span class="sxs-lookup"><span data-stu-id="02cc9-188">384-bit ECP</span></span>    |
| <span data-ttu-id="02cc9-189">24</span><span class="sxs-lookup"><span data-stu-id="02cc9-189">24</span></span>                        | <span data-ttu-id="02cc9-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="02cc9-190">DHGroup24</span></span>                | <span data-ttu-id="02cc9-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="02cc9-191">PFS24</span></span>        | <span data-ttu-id="02cc9-192">2048-bits MODP</span><span class="sxs-lookup"><span data-stu-id="02cc9-192">2048-bit MODP</span></span>  |

<span data-ttu-id="02cc9-193">Raadpleeg te[RFC3526](https://tools.ietf.org/html/rfc3526) en [RFC5114](https://tools.ietf.org/html/rfc5114) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02cc9-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="02cc9-194"><a name ="crossprem"></a>Deel 3: een nieuwe S2S VPN-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-195">In deze sectie leert u Hallo van een S2S VPN-verbinding maken met een IPsec/IKE-beleid.</span><span class="sxs-lookup"><span data-stu-id="02cc9-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="02cc9-196">Hallo volgt Hallo verbinding maken zoals u in Hallo diagram:</span><span class="sxs-lookup"><span data-stu-id="02cc9-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="02cc9-198">Zie [een S2S VPN-verbinding](vpn-gateway-create-site-to-site-rm-powershell.md) voor stapsgewijze instructies gedetailleerde voor het maken van een S2S VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="02cc9-199"><a name="before"></a>Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="02cc9-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="02cc9-200">Controleer of u een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="02cc9-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="02cc9-201">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02cc9-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="02cc9-202">Hello Azure Resource Manager PowerShell-cmdlets installeren.</span><span class="sxs-lookup"><span data-stu-id="02cc9-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="02cc9-203">Zie [overzicht van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="02cc9-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="02cc9-204"><a name="createvnet1"></a>Stap 1: Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="02cc9-205">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="02cc9-205">1. Declare your variables</span></span>

<span data-ttu-id="02cc9-206">Voor deze oefening eerst we onze variabelen declareren.</span><span class="sxs-lookup"><span data-stu-id="02cc9-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="02cc9-207">Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie.</span><span class="sxs-lookup"><span data-stu-id="02cc9-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="02cc9-208">2. Verbinding maken met tooyour abonnement en een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="02cc9-209">Zorg ervoor dat u overschakelt tooPowerShell modus toouse Hallo Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="02cc9-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="02cc9-210">Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02cc9-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="02cc9-211">Open de PowerShell-console en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="02cc9-212">Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:</span><span class="sxs-lookup"><span data-stu-id="02cc9-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="02cc9-213">3. Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="02cc9-214">Hallo volgende voorbeeld maakt Hallo virtueel netwerk TestVNet1, met drie subnetten en Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="02cc9-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="02cc9-215">Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="02cc9-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="02cc9-216">Als u een andere naam kiest, mislukt het maken van de gateway.</span><span class="sxs-lookup"><span data-stu-id="02cc9-216">If you name it something else, your gateway creation fails.</span></span>

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

### <span data-ttu-id="02cc9-217"><a name="s2sconnection"></a>Stap 2: een S2S VPN-verbinding maken met een IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="02cc9-218">1. Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-219">Hallo volgende voorbeeldscript maakt u een beleid voor IPsec/IKE met Hallo algoritmen en parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="02cc9-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="02cc9-220">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="02cc9-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="02cc9-221">IPsec: AES256, SHA256, PFS24, SA levensduur 7200 seconden & 2048KB</span><span class="sxs-lookup"><span data-stu-id="02cc9-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="02cc9-222">Als u GCMAES voor IPSec-authenticatie gebruikt, moet u dezelfde GCMAES algoritme en de sleutellengte voor IPSec-codering en integriteit, bijvoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="02cc9-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="02cc9-223">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="02cc9-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="02cc9-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA levensduur 7200 seconden & 2048 KB</span><span class="sxs-lookup"><span data-stu-id="02cc9-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="02cc9-225">2. Hallo S2S VPN-verbinding maken met Hallo IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-226">Een S2S VPN-verbinding maken en toepassen van beleid voor IPsec/IKE Hallo eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="02cc9-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="02cc9-227">U kunt optioneel toevoegen '-UsePolicyBasedTrafficSelectors $True ' toohello verbinding maken cmdlet tooenable Azure VPN-gateway tooconnect toopolicy gebaseerde VPN-apparaten on-premises, zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="02cc9-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02cc9-228">Als een beleid voor IPsec/IKE op een verbinding is opgegeven, wordt alleen hello Azure VPN-gateway verzenden of Hallo IPsec/IKE voorstel met opgegeven cryptografische algoritmen en de belangrijkste sterkte op die bepaalde verbinding accepteren.</span><span class="sxs-lookup"><span data-stu-id="02cc9-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="02cc9-229">Controleer of uw on-premises VPN-apparaat voor verbinding Hallo gebruikt of accepteert Hallo exacte beleid combinatie, anders Hallo S2S VPN-tunnel niet tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="02cc9-230"><a name ="vnet2vnet"></a>Deel 4: een nieuwe VNet-naar-VNet-verbinding maken met IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-231">Hallo-stappen voor het maken van een VNet-naar-VNet-verbinding met een beleid voor IPsec/IKE zijn vergelijkbaar toothat van een S2S VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="02cc9-232">Hallo volgende voorbeeldscripts Hallo verbinding maken zoals u in Hallo diagram:</span><span class="sxs-lookup"><span data-stu-id="02cc9-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![V2V-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="02cc9-234">Zie [Maak een VNet-naar-VNet-verbinding](vpn-gateway-vnet-vnet-rm-ps.md) voor stappen gedetailleerde voor het maken van een VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="02cc9-235">U moet voltooien [deel 3](#crossprem) toocreate en configureer TestVNet1 en Hallo VPN-Gateway.</span><span class="sxs-lookup"><span data-stu-id="02cc9-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="02cc9-236"><a name="createvnet2"></a>Stap 1: Hallo tweede virtuele netwerk- en VPN-gateway maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="02cc9-237">1. De variabelen declareren</span><span class="sxs-lookup"><span data-stu-id="02cc9-237">1. Declare your variables</span></span>

<span data-ttu-id="02cc9-238">Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="02cc9-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="02cc9-239">2. Hallo tweede virtuele netwerk- en VPN-gateway in Hallo nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

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

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="02cc9-240">Stap 2: een VNet-toVNet verbinding maken met Hallo IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-241">Vergelijkbare toohello S2S VPN-verbinding een IPsec/IKE-beleid maken en toepassen van toopolicy toohello nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="02cc9-242">1. Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="02cc9-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-243">Hallo volgende voorbeeldscript maakt u een ander IPsec/IKE-beleid met Hallo algoritmen en parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="02cc9-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="02cc9-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="02cc9-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="02cc9-245">IPsec: GCMAES128, GCMAES128, PFS14, SA levensduur 7200 seconden en 4096KB</span><span class="sxs-lookup"><span data-stu-id="02cc9-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="02cc9-246">2. VNet-naar-VNet-verbindingen maken met de Hallo IPsec/IKE-beleid</span><span class="sxs-lookup"><span data-stu-id="02cc9-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="02cc9-247">Een VNet-naar-VNet-verbinding maken en toepassen van Hallo IPsec/IKE-beleid die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="02cc9-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="02cc9-248">In dit voorbeeld beide gateways zijn in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="02cc9-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="02cc9-249">Zodat het is mogelijk toocreate en configureren van beide verbindingen met dezelfde IPsec/IKE-beleid in Hallo Hallo dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="02cc9-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="02cc9-250">Als een beleid voor IPsec/IKE op een verbinding is opgegeven, wordt alleen hello Azure VPN-gateway verzenden of Hallo IPsec/IKE voorstel met opgegeven cryptografische algoritmen en de belangrijkste sterkte op die bepaalde verbinding accepteren.</span><span class="sxs-lookup"><span data-stu-id="02cc9-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="02cc9-251">Zorg ervoor dat Hallo IPSec-beleid voor beide verbindingen zijn Hallo dezelfde, anders de VNet-naar-VNet-verbinding niet tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="02cc9-252">Hallo-verbinding is gemaakt in een paar minuten na het voltooien van deze stappen en hebt u Hallo netwerktopologie te volgen, zoals wordt weergegeven in Hallo vanaf:</span><span class="sxs-lookup"><span data-stu-id="02cc9-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ike-IPSec-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="02cc9-254"><a name ="managepolicy"></a>Deel 5 - Update IPsec/IKE-beleid voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="02cc9-255">de laatste sectie Hallo ziet u hoe toomanage IPsec/IKE-beleid voor een bestaande S2S of VNet-naar-VNet-verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="02cc9-256">Hallo oefening hieronder wordt u begeleid bij Hallo bewerkingen op een verbinding te volgen:</span><span class="sxs-lookup"><span data-stu-id="02cc9-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="02cc9-257">Hallo IPsec/IKE-beleid van een verbinding weergeven</span><span class="sxs-lookup"><span data-stu-id="02cc9-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="02cc9-258">Toevoegen of bijwerken van Hallo IPsec/IKE-beleid tooa verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="02cc9-259">Hallo IPsec/IKE-beleid verwijderen uit een verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="02cc9-260">Hallo dezelfde stappen van toepassing tooboth S2S- en VNet-naar-VNet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02cc9-261">IPsec/IKE-beleid wordt ondersteund op *standaard* en *HighPerformance* op route gebaseerde VPN-gateways alleen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="02cc9-262">Deze werkt niet op Hallo Basic gateway-SKU of Hallo op beleid gebaseerde VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="02cc9-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="02cc9-263">1. Hallo IPsec/IKE-beleid van een verbinding weergeven</span><span class="sxs-lookup"><span data-stu-id="02cc9-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="02cc9-264">Hallo volgende voorbeeld ziet u hoe tooget Hallo IPsec/IKE-beleid op een verbinding is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="02cc9-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="02cc9-265">Hallo scripts blijven ook uit Hallo oefeningen hierboven.</span><span class="sxs-lookup"><span data-stu-id="02cc9-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="02cc9-266">de laatste opdracht Hallo bevat Hallo huidige IPsec/IKE-beleid geconfigureerd op Hallo verbinding, indien deze aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="02cc9-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="02cc9-267">Hallo volgende voorbeelduitvoer wordt voor Hallo verbinding:</span><span class="sxs-lookup"><span data-stu-id="02cc9-267">hello following sample output is for hello connection:</span></span>

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

<span data-ttu-id="02cc9-268">Als er geen IPsec/IKE-beleid dat is geconfigureerd, Hallo opdracht (PS > $connection6.policy) een leeg retourtype opgehaald.</span><span class="sxs-lookup"><span data-stu-id="02cc9-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="02cc9-269">Dit betekent niet dat IPsec/IKE is niet geconfigureerd op Hallo verbinding, maar er is geen aangepaste IPsec/IKE-beleid.</span><span class="sxs-lookup"><span data-stu-id="02cc9-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="02cc9-270">de huidige verbinding Hallo maakt gebruik van Hallo standaardbeleid onderhandeld tussen uw on-premises VPN-apparaat en hello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="02cc9-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="02cc9-271">2. Toevoegen of bijwerken van een beleid voor IPsec/IKE voor een verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="02cc9-272">een nieuw beleid voor stappen tooadd Hallo of update zijn van een bestaand beleid op een verbinding Hallo dezelfde: een nieuw beleid maken en toepassen van Hallo nieuwe beleid toohello verbinding.</span><span class="sxs-lookup"><span data-stu-id="02cc9-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="02cc9-273">tooenable 'UsePolicyBasedTrafficSelectors' wanneer tooan verbinding maken met on-premises op beleid gebaseerde VPN-apparaat toevoegen Hallo '-UsePolicyBaseTrafficSelectors ' parameter toohello cmdlet, of stel deze in te$ False toodisable Hallo optie:</span><span class="sxs-lookup"><span data-stu-id="02cc9-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="02cc9-274">U krijgt Hallo verbinding opnieuw toocheck als Hallo beleid wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="02cc9-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="02cc9-275">U ziet Hallo-uitvoer van de laatste regel hello, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="02cc9-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

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

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="02cc9-276">3. Een beleid voor IPsec/IKE verwijderen uit een verbinding</span><span class="sxs-lookup"><span data-stu-id="02cc9-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="02cc9-277">Wanneer u een aangepast beleid Hallo van een verbinding verwijdert, hello Azure VPN-gateway wordt teruggezet back toohello [standaardlijst met IPsec/IKE voorstellen](vpn-gateway-about-vpn-devices.md) en start een opnieuw nieuwe onderhandeling met uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="02cc9-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="02cc9-278">U kunt hetzelfde script toocheck Hallo als Hallo beleid uit Hallo-verbinding is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="02cc9-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02cc9-279">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02cc9-279">Next steps</span></span>

<span data-ttu-id="02cc9-280">Zie [verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](vpn-gateway-connect-multiple-policybased-rm-ps.md) voor meer informatie over op beleid gebaseerde verkeer selectoren.</span><span class="sxs-lookup"><span data-stu-id="02cc9-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="02cc9-281">Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="02cc9-282">Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.</span><span class="sxs-lookup"><span data-stu-id="02cc9-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
