---
title: aaaPrerequisites voor Azure ExpressRoute-acceptatie | Microsoft Docs
description: Deze pagina bevat een lijst met vereisten toobe voldaan voordat u een Azure ExpressRoute-circuit kunt bestellen.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Vereisten en controlelijst voor ExpressRoute
tooconnect tooMicrosoft cloud services met behulp van ExpressRoute, moet u tooverify die volgens de vereisten die worden vermeld in de volgende secties Hallo Hallo is voldaan.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Azure-account
* Een geldig en actief Microsoft Azure-account. Dit account is vereist tooset up Hallo ExpressRoute-circuit. ExpressRoute-circuits zijn resources in Azure-abonnementen. Een Azure-abonnement is vereist, zelfs als connectiviteit beperkt toonon Azure Microsoft cloudservices, zoals Office 365-services en is Dynamics 365.
* Een actief Office 365-abonnement (als u Office 365-services gebruikt). Zie voor meer informatie, Hallo [specifieke vereisten voor Office 365](#office-365-specific-requirements) sectie van dit artikel.

## <a name="connectivity-provider"></a>Connectiveitsprovider

* U kunt werken met een [ExpressRoute-connectiviteitspartner](expressroute-locations.md#partners) tooconnect toohello Microsoft cloud. U kunt op [drie manieren](expressroute-introduction.md) een verbinding instellen tussen uw on-premises netwerk en Microsoft.
* Als uw provider geen ExpressRoute-connectiviteitspartner is, kunt u nog steeds verbinding maken toohello Microsoft cloud via een [cloudexchange-provider](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Netwerkvereisten
* **Redundante connectiviteit**: er is geen redundantievereiste voor fysieke connectiviteit tussen u en uw provider. Microsoft vereist dat redundante BGP-sessies toobe ingesteld tussen Microsoft routers en Hallo peeringrouters, zelfs als u net hebt [één fysieke verbinding tooa cloudexchange](expressroute-faqs.md#onep2plink).
* **Routering**: afhankelijk van hoe u verbinding maakt met Microsoft Cloud toohello, u of uw provider tooset nodig en beheren van Hallo BGP-sessies voor [Routeringsdomeinen](expressroute-circuit-peerings.md). Sommige Ethernet-connectiviteitsproviders of cloudexchange-providers bieden BGP-beheer aan als extra service.
* **NAT**: Microsoft accepteert alleen openbare IP-adressen via Microsoft-peering. Als u privé IP-adressen in uw on-premises netwerk gebruikt, u of uw provider moeten tootranslate Hallo persoonlijke IP-adressen toohello openbare IP-adressen [met behulp van NAT Hallo](expressroute-nat.md).
* **QoS**: Skype voor Bedrijven heeft verschillende services (zoals spraak, video, tekst) die allemaal een andere QoS-behandeling vereisen. U en uw provider moeten volgen Hallo [QoS-vereisten](expressroute-qos.md).
* **Netwerkbeveiliging**: overweeg [netwerkbeveiliging](../best-practices-network-security.md) bij het verbinden van toohello Microsoft Cloud via ExpressRoute.

## <a name="office-365"></a>Office 365
Als u van plan tooenable Office 365 op ExpressRoute bent, raadpleegt u Hallo volgende documenten voor meer informatie over de vereisten voor Office 365.

* [Overview of ExpressRoute for Office 365 (Overzicht van ExpressRoute voor Office 365)](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Routing with ExpressRoute for Office 365 (Routering met ExpressRoute voor Office 365)](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Office 365 URLs and IP address ranges (URL's en IP-adresbereiken voor Office 365)](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Network planning and performance tuning for Office 365 (Netwerkplanning en prestatieafstemming voor Office 365)](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Network bandwidth calculators and tools (Calculators en hulpmiddelen voor het berekenen van de netwerkbandbreedte)](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Office 365 integration with on-premises environments (Office 365-integratie met on-premises omgevingen)](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Geavanceerde trainingsvideo's voor ExpressRoute in Office 365](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Als u van plan tooenable Dynamics 365 op ExpressRoute bent, bekijkt u Hallo volgende documenten voor meer informatie over Dynamics 365

* [Dynamics 365 and ExpressRoute whitepaper](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [Dynamics 365 URLs](https://support.microsoft.com/kb/2655102) en [IP address ranges](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
* Zoek een ExpressRoute-connectiviteitsprovider. Zie [ExpressRoute partners and peering locations](expressroute-locations.md) (ExpressRoute-partners en -peeringlocaties).
* Raadpleeg toorequirements voor [routering](expressroute-routing.md), [NAT](expressroute-nat.md), en [QoS](expressroute-qos.md).
* Configureer uw ExpressRoute-verbinding.
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-classic.md)
  * [Routering configureren](expressroute-howto-routing-classic.md)
  * [Koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md)
