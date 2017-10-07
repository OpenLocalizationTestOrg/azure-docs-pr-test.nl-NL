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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Over de cryptografische vereisten en Azure VPN-gateways

Dit artikel wordt beschreven hoe u kunt configureren Azure VPN-gateways toosatisfy de vereisten van uw cryptografische voor cross-premises S2S VPN-tunnels en VNet-naar-VNet-verbindingen in Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Informatie over IPsec en IKE beleidsparameters voor Azure VPN-gateways
IPsec en IKE-protocol standaard ondersteunt een groot aantal cryptografische algoritmen in verschillende combinaties. Als een specifieke combinatie van cryptografische algoritmen en parameters klanten geen aanvragen, gebruikt u Azure VPN-gateways een reeks standaard voorstellen. Hallo standaard beleid sets zijn gekozen toomaximize interoperabiliteit met een breed scala aan VPN-apparaten van derden standaardconfiguraties. Als gevolg hiervan dekken Hallo beleid en het aantal voorstellen Hallo niet alle mogelijke combinaties van beschikbare cryptografische algoritmen en de belangrijkste sterkte.

Hallo standaardbeleid instellen voor Azure VPN-gateway wordt vermeld in het Hallo-document: [over VPN-apparaten en IPsec/IKE-parameters voor de Site-naar-Site-VPN-gatewayverbindingen](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Cryptografische vereisten
Voor communicatie waarvoor specifieke cryptografische algoritmen of parameters die kunnen doorgaans vanwege toocompliance of beveiliging vereisten, klanten nu configureren hun Azure VPN-gateways toouse een aangepast beleid voor IPsec/IKE met specifieke cryptografische algoritmen en kracht van de plaats van hello Azure standaard beleid sets.

Hallo IKEv2 hoofdmodusbeleidsregels voor Azure VPN-gateways gebruiken bijvoorbeeld alleen Diffie-Hellman-groep 2 (1024 bits), terwijl klanten toospecify sterkere groepen toobe gebruikt in IKE, zoals groep 14 (2048-bits), groep 24 (2048-bits MODP groep) of ECP (elliptic wellicht curve groepen) 256 of 384 bits (een groep 19 en 20 groep, respectievelijk). Vergelijkbare vereisten tooIPsec snelle modus beleid ook van toepassing.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Aangepaste IPsec/IKE-beleid met Azure VPN-gateways
Nu ondersteuning voor Azure VPN-gateways per verbinding, aangepaste IPsec/IKE-beleid. Voor een Site-naar-Site of een VNet-naar-VNet-verbinding kunt u een specifieke combinatie van cryptografische algoritmen voor IPsec en IKE met Hallo gewenst sleutelsterkte, zoals wordt weergegeven in het volgende voorbeeld Hallo:

![ike-IPSec-beleid](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

U kunt een IPsec/IKE-beleid maken en toepassen van tooa nieuwe of bestaande verbinding. 

### <a name="workflow"></a>Werkstroom

1. Hallo virtuele netwerken, VPN-gateways of lokale netwerkgateways voor uw topologie connectiviteit maken, zoals beschreven in andere hoe-toodocuments
2. Een IPsec/IKE-beleid maken
3. U kunt Hallo beleid toepassen wanneer u een S2S of VNet-naar-VNet-verbinding maken
4. Als al Hallo verbinding is gemaakt, kunt u toepassen of Hallo beleid tooan bestaande verbinding bijwerken


## <a name="ipsecike-policy-faq"></a>Beleid voor IPsec/IKE Veelgestelde vragen

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Volgende stappen
Zie [configureren IPsec/IKE-beleid](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor stapsgewijze instructies over het configureren van aangepaste IPsec/IKE-beleid op een verbinding.

Zie ook [meerdere op beleid gebaseerde VPN-apparaten aansluiten](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn meer over Hallo UsePolicyBasedTrafficSelectors optie.
