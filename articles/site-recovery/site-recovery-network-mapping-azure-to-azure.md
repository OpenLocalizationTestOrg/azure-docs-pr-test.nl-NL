---
title: aaaNetwork toewijzing tussen twee Azure-regio's in Azure Site Recovery | Microsoft Docs
description: "Azure Site Recovery coördineert Hallo replicatie, failovers en herstel van virtuele machines en fysieke servers. Meer informatie over failover tooAzure of een secundair datacenter."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>De netwerkkoppeling tussen twee Azure-regio 's


Dit artikel wordt beschreven hoe toomap Azure virtuele netwerken van twee Azure-regio's met elkaar. Netwerktoewijzing zorgt ervoor dat wanneer gerepliceerde virtuele machine wordt gemaakt in Hallo doel-Azure-regio, wordt gemaakt op Hallo virtueel netwerk dat is toegewezen toovirtual netwerk van de virtuele bronmachine Hallo.  

## <a name="prerequisites"></a>Vereisten
Voordat u toewijzen netwerken zeker dat u hebt gemaakt kunt [virtuele netwerken van Azure](../virtual-network/virtual-networks-overview.md) in zowel bron en doel van de Azure-regio's.

## <a name="map-networks"></a>Netwerken toewijzen

een Azure-netwerk in een Azure-regio tooanother virtueel netwerk in een andere regio, Ga tooSite Recovery-infrastructuur toomap -> netwerktoewijzing (voor Azure Virtual Machines) en maak de netwerktoewijzing van een.

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


In het volgende voorbeeld wordt mijn virtuele machine wordt uitgevoerd in de Oost-Azië regio en wordt gerepliceerd in Hallo tooSoutheast Azië.

Hallo-bron en doel netwerk selecteren en klik op OK toocreate een netwerktoewijzing van Oost-Azië tooSoutheast Azië.

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Hallo dezelfde ding toocreate een netwerktoewijzing van Zuidoost-Azië tooEast Azië.  
![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Netwerkverbinding maken bij het inschakelen van replicatie

Als de netwerktoewijzing is niet uitgevoerd wanneer u een virtuele machine voor Hallo eerste tijd formulier een Azure-regio tooanother repliceert, kunt u doelnetwerk als onderdeel van Hallo hetzelfde proces. Uit bron regio tootarget regio en regio toosource doelregio op basis van deze selectie, maakt site Recovery-netwerkkoppelingen.   

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Site Recovery maakt een netwerk in Hallo doelregio die het Bronnetwerk identieke toohello en door toe te voegen '-asr' als de naam van een achtervoegsel toohello van Hallo Bronnetwerk. U kunt een bestaande netwerk door te klikken op aanpassen.

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Als de netwerktoewijzing Hallo al wordt uitgevoerd, kunt u Hallo doel virtueel netwerk niet wijzigen tijdens het inschakelen van replicatie. toochange, bestaande netwerktoewijzing wijzigt.  

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Netwerktoewijzing](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Als u een netwerktoewijzing vanuit tooregion regio-1-2 wijzigt, zorg er dan voor dat u de netwerktoewijzing Hallo van regio-2-tooregion-ook 1 wijzigen.
>
>


## <a name="subnet-selection"></a>Selectie van subnet
Subnet van de virtuele doelmachine Hallo is geselecteerd op basis van naam van het subnet van de virtuele bronmachine Hallo HALLO hallo. Als er een subnet van Hallo wordt dezelfde naam als die van Hallo virtuele bronmachine beschikbaar zijn in het doelnetwerk hello, en vervolgens die voor de virtuele doelmachine Hallo is gekozen. Als er geen subnet met hello wordt dezelfde naam in het doelnetwerk hello, en vervolgens alfabetisch eerste subnet is gekozen als Hallo Doelsubnet. U kunt dit subnet wijzigen door te gaan tooCompute en de netwerkinstellingen van Hallo virtuele machine.

![Wijzigen van Subnet](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>IP-adres

IP-adres voor elk van de netwerkinterface Hallo van de virtuele doelmachine Hallo gekozen als volgt:

### <a name="dhcp"></a>DHCP
Als het Hallo-netwerkinterface van de virtuele bronmachine hello wordt DHCP gebruikt, vervolgens netwerkinterface van de virtuele doelmachine Hallo ook ingesteld als DHCP.

### <a name="static-ip"></a>Vaste IP-adres
Als Hallo-netwerkinterface van de virtuele bronmachine Hallo van vaste IP-adres gebruikmaakt, wordt klikt u vervolgens netwerkinterface van de virtuele doelmachine hello ook ingesteld toouse vaste IP-adres. Vaste IP-adres is als volgt kiezen:

#### <a name="same-address-space"></a>Dezelfde adresruimte

Als Hallo bron subnet en Doelsubnet Hallo Hallo-dezelfde adresruimte, wordt IP-adres doel hetzelfde als Hallo IP-adres van de netwerkinterface Hallo van de virtuele bronmachine Hallo ingesteld. Als dezelfde IP niet beschikbaar is, is sommige andere beschikbare IP ingesteld als IP-adres Hallo-doel.

#### <a name="different-address-space"></a>Andere adresruimte

Als Hallo bron subnet en Hallo Doelsubnet hebt verschillende adresruimte, is de doel-IP als een beschikbare IP in het doelsubnet Hallo ingesteld.

U kunt Hallo doel-IP-adres op elke netwerkinterface wijzigen door te gaan tooCompute en de netwerkinstellingen van Hallo virtuele machine.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [richtlijnen voor het repliceren van virtuele Azure-machines networking](site-recovery-azure-to-azure-networking-guidance.md).
