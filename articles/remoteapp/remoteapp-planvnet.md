---
title: Het plannen van het virtuele netwerk voor een Azure RemoteApp-verzameling | Microsoft Docs
description: Informatie over het plannen van het virtuele netwerk voor een Azure RemoteApp-verzameling.
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 1eb8115b13fb18074b4c4726b69e3d9faf387c32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a>Het plannen van het virtuele netwerk van Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Dit document beschrijft het instellen van uw Azure-netwerk (VNET) en het subnet voor Azure RemoteApp. Als u niet bekend met virtuele Azure-netwerken bent, is dit een functie die u kunt virtualiseren uw netwerkinfrastructuur naar de cloud en hybride oplossingen maken met Azure en uw lokale bronnen. [Hier](../virtual-network/virtual-networks-overview.md) vindt u meer informatie.

Als u wilt definiëren beveiligingsbeleid voor verkeer (binnenkomend en uitgaand) in het virtuele netwerk waar u Azure RemoteApp implementeert, wordt aangeraden een apart subnet maken voor Azure RemoteApp van de rest van uw implementaties in Azure virtueel netwerk. Lees voor meer informatie over het definiëren van beveiligingsbeleid op uw virtuele netwerk van Azure-subnet [wat is er een Netwerkbeveiligingsgroep (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Typen Azure RemoteApp-collecties met virtuele netwerken in Azure
De volgende afbeeldingen tonen de twee andere verzameling opties wanneer u wilt gebruiken een virtueel netwerk.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Azure RemoteApp-cloudverzameling met VNET
 ![Azure RemoteApp - cloudverzameling met een VNET](./media/remoteapp-planvpn/ra-cloudvpn.png)

Hiermee wordt een Azure RemoteApp-verzameling waarin alle resources die de RemoteApp-sessie hosts moeten toegang hebben tot zijn geïmplementeerd in Azure. Ze kunnen zich in hetzelfde VNET als het RemoteApp VNET of een andere VNET in Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Azure RemoteApp hybride verzameling met VNET
![Azure RemoteApp - hybride verzameling met een VNET](./media/remoteapp-planvpn/ra-hybridvpn.png)

Hiermee wordt een Azure RemoteApp-verzameling wanneer zich een aantal van de resources die de RemoteApp-sessie hosts moeten toegang hebben tot geïmplementeerde on-premises. De RemoteApp VNET is gekoppeld aan de on-premises netwerk met behulp van Azure hybride technologieën zoals site-naar-site VPN- of Express Route.

## <a name="how-the-system-works"></a>De werking van het systeem
Achter de implementeert Azure RemoteApp (met uw geüploade afbeelding) virtuele Azure-machines op het subnet van het virtuele netwerk dat u hebt gekozen tijdens het inrichten. Als u voor een hybride verzameling hebt gekozen, proberen we om op te lossen de FQDN-naam van de domeincontroller die u hebt ingevoerd in de inrichting werkstroom met de DNS-server die u in het virtuele netwerk.  
Als u verbinding met een bestaand virtueel netwerk maakt, zorg ervoor dat de vereiste poorten in uw netwerkbeveiligingsgroepen in uw Azure RemoteApp-subnet weer. 

We raden u aan een [groot genoeg subnet voor Azure RemoteApp](remoteapp-vnetsizing.md). Het grootste ondersteund door Azure Virtual network/8 die is (met behulp van de CIDR-subnetdefinities). Uw subnet moet groot genoeg voor alle Azure RemoteApp-VM's tijdens de scale-up wanneer meer gebruikers toegang hebben tot de apps. 

Hieronder volgen de bewerkingen die u wel wilt inschakelen op het subnet van uw virtuele netwerk: 

1. Uitgaand verkeer van het subnet moet worden toegestaan op poortbereik 10101 10175 om te communiceren met een van de interne Azure RemoteApp-services.
2. Uitgaand verkeer moet van uw subnet worden toegestaan verbinding maken met Azure Storage op poort 443
3. Als u Active Directory die worden gehost in Azure hebt, zorg er dan voor dat elke virtuele machine binnen het subnet van het virtuele netwerk voor Azure RemoteApp is geen verbinding maken met die domeincontroller. De DNS-server in het virtuele netwerk moet kunnen omzetten van de FQDN-naam van deze domeincontroller.

## <a name="virtual-network-with-forced-tunneling"></a>Virtueel netwerk met geforceerde tunneling
[Geforceerde tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) wordt nu ondersteund voor alle nieuwe Azure RemoteApp-collecties. Wordt momenteel niet ondersteund de migratie van een bestaande verzameling voor de ondersteuning van geforceerde tunneling.  U moet uw bestaande verzamelingen met behulp van de VNET die u aan Azure RemoteApp koppelen wilt verwijderen en maken van een nieuw token voor het ophalen van geforceerde tunneling is ingeschakeld op uw verzamelingen. 

