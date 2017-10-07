---
title: aaaAbout cryptografische vereisten en Azure VPN-gateways | Microsoft Docs
description: Dit artikel wordt beschreven cryptografische vereisten en Azure VPN-gateways
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
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="5188d-103">Over de cryptografische vereisten en Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="5188d-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="5188d-104">Dit artikel wordt beschreven hoe u kunt configureren Azure VPN-gateways toosatisfy de vereisten van uw cryptografische voor cross-premises S2S VPN-tunnels en VNet-naar-VNet-verbindingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="5188d-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="5188d-105">Informatie over IPsec en IKE beleidsparameters voor Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="5188d-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="5188d-106">IPsec en IKE-protocol standaard ondersteunt een groot aantal cryptografische algoritmen in verschillende combinaties.</span><span class="sxs-lookup"><span data-stu-id="5188d-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="5188d-107">Als een specifieke combinatie van cryptografische algoritmen en parameters klanten geen aanvragen, gebruikt u Azure VPN-gateways een reeks standaard voorstellen.</span><span class="sxs-lookup"><span data-stu-id="5188d-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="5188d-108">Hallo standaard beleid sets zijn gekozen toomaximize interoperabiliteit met een breed scala aan VPN-apparaten van derden standaardconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="5188d-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="5188d-109">Als gevolg hiervan dekken Hallo beleid en het aantal voorstellen Hallo niet alle mogelijke combinaties van beschikbare cryptografische algoritmen en de belangrijkste sterkte.</span><span class="sxs-lookup"><span data-stu-id="5188d-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="5188d-110">Hallo standaardbeleid instellen voor Azure VPN-gateway wordt vermeld in het Hallo-document: [over VPN-apparaten en IPsec/IKE-parameters voor de Site-naar-Site-VPN-gatewayverbindingen](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="5188d-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="5188d-111">Cryptografische vereisten</span><span class="sxs-lookup"><span data-stu-id="5188d-111">Cryptographic requirements</span></span>
<span data-ttu-id="5188d-112">Voor communicatie waarvoor specifieke cryptografische algoritmen of parameters die kunnen doorgaans vanwege toocompliance of beveiliging vereisten, klanten nu configureren hun Azure VPN-gateways toouse een aangepast beleid voor IPsec/IKE met specifieke cryptografische algoritmen en kracht van de plaats van hello Azure standaard beleid sets.</span><span class="sxs-lookup"><span data-stu-id="5188d-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="5188d-113">Hallo IKEv2 hoofdmodusbeleidsregels voor Azure VPN-gateways gebruiken bijvoorbeeld alleen Diffie-Hellman-groep 2 (1024 bits), terwijl klanten toospecify sterkere groepen toobe gebruikt in IKE, zoals groep 14 (2048-bits), groep 24 (2048-bits MODP groep) of ECP (elliptic wellicht curve groepen) 256 of 384 bits (een groep 19 en 20 groep, respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="5188d-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="5188d-114">Vergelijkbare vereisten tooIPsec snelle modus beleid ook van toepassing.</span><span class="sxs-lookup"><span data-stu-id="5188d-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="5188d-115">Aangepaste IPsec/IKE-beleid met Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="5188d-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="5188d-116">Nu ondersteuning voor Azure VPN-gateways per verbinding, aangepaste IPsec/IKE-beleid.</span><span class="sxs-lookup"><span data-stu-id="5188d-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="5188d-117">Voor een Site-naar-Site of een VNet-naar-VNet-verbinding kunt u een specifieke combinatie van cryptografische algoritmen voor IPsec en IKE met Hallo gewenst sleutelsterkte, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="5188d-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ike-IPSec-beleid](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="5188d-119">U kunt een IPsec/IKE-beleid maken en toepassen van tooa nieuwe of bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="5188d-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="5188d-120">Werkstroom</span><span class="sxs-lookup"><span data-stu-id="5188d-120">Workflow</span></span>

1. <span data-ttu-id="5188d-121">Hallo virtuele netwerken, VPN-gateways of lokale netwerkgateways voor uw topologie connectiviteit maken, zoals beschreven in andere hoe-toodocuments</span><span class="sxs-lookup"><span data-stu-id="5188d-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="5188d-122">Een IPsec/IKE-beleid maken</span><span class="sxs-lookup"><span data-stu-id="5188d-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="5188d-123">U kunt Hallo beleid toepassen wanneer u een S2S of VNet-naar-VNet-verbinding maken</span><span class="sxs-lookup"><span data-stu-id="5188d-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="5188d-124">Als al Hallo verbinding is gemaakt, kunt u toepassen of Hallo beleid tooan bestaande verbinding bijwerken</span><span class="sxs-lookup"><span data-stu-id="5188d-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="5188d-125">Beleid voor IPsec/IKE Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="5188d-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="5188d-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5188d-126">Next steps</span></span>
<span data-ttu-id="5188d-127">Zie [configureren IPsec/IKE-beleid](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor stapsgewijze instructies over het configureren van aangepaste IPsec/IKE-beleid op een verbinding.</span><span class="sxs-lookup"><span data-stu-id="5188d-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="5188d-128">Zie ook [meerdere op beleid gebaseerde VPN-apparaten aansluiten](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn meer over Hallo UsePolicyBasedTrafficSelectors optie.</span><span class="sxs-lookup"><span data-stu-id="5188d-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
