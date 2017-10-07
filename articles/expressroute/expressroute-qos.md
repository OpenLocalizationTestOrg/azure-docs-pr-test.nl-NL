---
title: aaaQoS vereisten voor ExpressRoute | Microsoft Docs
description: Deze pagina bevat gedetailleerde vereisten voor het configureren en beheren van de QoS voor ExpressRoute-circuits.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>QoS-vereisten voor ExpressRoute
Skype voor Bedrijven heeft verschillende workloads die allemaal een andere QoS-behandeling vereisen. Als u van plan tooconsume voice-services via ExpressRoute bent, moet u voldoen toohello vereisten die hieronder worden beschreven.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> QoS-vereisten toohello Microsoft-peering alleen van toepassing. Hallo DSCP-waarden in het netwerkverkeer dat is ontvangen op openbare Azure-peering en persoonlijke Azure-peering worden too0 opnieuw instellen. 
> 
> 

Hallo bevat volgende tabel een lijst van DSCP-markeringen gebruikt door Skype voor bedrijven. Raadpleeg te[QoS voor Skype voor bedrijven beheren](https://technet.microsoft.com/library/gg405409.aspx) voor meer informatie.

| **Verkeersklasse** | **Behandeling (DSCP-markering)** | **Workloads voor Skype voor Bedrijven** |
| --- | --- | --- |
| **Spraak** |EF (46) |Skype / Lync voice |
| **Interactief** |AF41 (34) |Video, VBSS |
| AF21 (18) |Apps delen | |
| **Standaard** |AF11 (10) |Bestandsoverdracht |
| CS0 (0) |Overige | |

* U moet Hallo workloads classificeren en Hallo juiste DSCP-waarden markeren. Volg de richtlijnen voor Hallo [hier](https://technet.microsoft.com/library/gg405409.aspx) over het tooset DSCP-markeringen in uw netwerk.
* U moet meerdere QoS-wachtrijen in uw netwerk configureren en ondersteunen. Voice moet een zelfstandige klasse en krijg Hallo EF-behandeling opgegeven in RFC 3246. 
* U kunt Hallo queuing mechanisme, congestiedetectiebeleid en de bandbreedtetoewijzing per verkeersklasse bepalen. Maar hello DSCP-markering voor Skype voor bedrijven-werkbelastingen moet worden bewaard. Als u DSCP-markeringen die niet wordt weergegeven, bijvoorbeeld AF31 (26), moet u deze DSCP-waarde too0 herschrijven voordat Hallo pakket tooMicrosoft worden verzonden. Microsoft verzendt alleen pakketten die zijn gemarkeerd met Hallo DSCP-waarde wordt weergegeven in Hallo bovenstaande tabel. 

## <a name="next-steps"></a>Volgende stappen
* Raadpleeg de vereisten voor toohello [routering](expressroute-routing.md) en [NAT](expressroute-nat.md).
* Zie de volgende Hallo koppelingen tooconfigure uw ExpressRoute-verbinding.
  
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-classic.md)
  * [Routering configureren](expressroute-howto-routing-classic.md)
  * [Koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md)

