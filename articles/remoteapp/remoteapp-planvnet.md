---
title: aaaHow tooplan het virtuele netwerk voor een Azure RemoteApp-verzameling | Microsoft Docs
description: Meer informatie over hoe tooplan het virtuele netwerk voor een Azure RemoteApp-verzameling.
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
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Hoe tooplan het virtuele netwerk voor Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Dit document wordt beschreven hoe tooset van uw Azure-netwerk (VNET) en het Hallo-subnet voor Azure RemoteApp. Als u niet bekend met virtuele Azure-netwerken bent, is dit een functie waarmee u toovirtualize uw netwerk infrastructuur toohello cloud en toocreate hybride oplossingen met Azure en uw lokale bronnen. [Hier](../virtual-network/virtual-networks-overview.md) vindt u meer informatie.

Als u toodefine beveiligingsbeleid voor verkeer (binnenkomend en uitgaand) in uw virtuele netwerk waar u Azure RemoteApp implementeert wilt, wordt aangeraden een apart subnet maken voor Azure RemoteApp van Hallo rest van uw implementaties in hello Azure virtueel netwerk. Lees voor meer informatie over hoe toodefine beveiligingsbeleid op uw virtuele Azure-netwerk subnet, [wat is er een Netwerkbeveiligingsgroep (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Typen Azure RemoteApp-collecties met virtuele netwerken in Azure
Hallo onderstaande afbeeldingen Hallo twee andere verzameling opties weergeven als u wilt dat toouse een virtueel netwerk.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Azure RemoteApp-cloudverzameling met VNET
 ![Azure RemoteApp - cloudverzameling met een VNET](./media/remoteapp-planvpn/ra-cloudvpn.png)

Hiermee wordt een Azure RemoteApp-collectie waarbij alle Hallo resources dat Hallo RemoteApp-sessie hosts tooaccess moeten zijn geïmplementeerd in Azure. Ze kunnen zich op Hallo hetzelfde VNET als Hallo RemoteApp VNET of een andere VNET in Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Azure RemoteApp hybride verzameling met VNET
![Azure RemoteApp - hybride verzameling met een VNET](./media/remoteapp-planvpn/ra-hybridvpn.png)

Hiermee wordt een Azure RemoteApp-collectie waarbij een aantal van Hallo resources dat Hallo RemoteApp-sessie hosts tooaccess moeten zich geïmplementeerde on-premises. Hallo RemoteApp VNET is gekoppelde toohello on-premises netwerk met behulp van Azure hybride technologieën zoals site-naar-site VPN- of Express Route.

## <a name="how-hello-system-works"></a>De werking van Hallo-systeem
Azure RemoteApp implementeert onder Hallo dekt Azure virtuele machines (met uw geüploade afbeelding) toohello virtueel netwerksubnet die u hebt gekozen tijdens het inrichten. Als u voor een hybride verzameling hebt gekozen, proberen we tooresolve Hallo FQDN-naam van het Hallo-domeincontroller die u hebt ingevoerd in de inrichting van de werkstroom met Hallo DNS-server is opgegeven in het virtuele netwerk Hallo Hallo.  
Als u een bestaand virtueel netwerk tooan verbinding, moet u ervoor dat tooexpose Hallo nodig poorten maken in uw netwerkbeveiligingsgroepen in uw Azure RemoteApp-subnet. 

We raden u aan een [groot genoeg subnet voor Azure RemoteApp](remoteapp-vnetsizing.md). Hallo grootste ondersteund door Azure Virtual network/8 die is (met behulp van de CIDR-subnetdefinities). Uw subnet moet groot genoeg tooaccommodate alle hello Azure RemoteApp-VM's tijdens de scale-up wanneer meer gebruikers Hallo apps gebruiken. 

Hieronder vindt u Hallo dingen die u moet tooenable op het subnet van uw virtuele netwerk: 

1. Uitgaand verkeer van Hallo subnet moet worden toegestaan op poort bereik 10101 10175 toocommunicate met een Hallo interne Azure RemoteApp-services.
2. Uitgaand verkeer moet worden toegestaan vanaf uw subnet tooconnect tooAzure opslag op poort 443
3. Als u Active Directory die worden gehost in Azure hebt, zorg er dan voor dat elke virtuele machine binnen virtueel netwerksubnet Hallo voor Azure RemoteApp kunnen tooconnect toothat domeincontroller is. Hallo DNS in het virtuele netwerk Hallo moet kunnen tooresolve Hallo FQDN-naam van deze domeincontroller.

## <a name="virtual-network-with-forced-tunneling"></a>Virtueel netwerk met geforceerde tunneling
[Geforceerde tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) wordt nu ondersteund voor alle nieuwe Azure RemoteApp-collecties. Wordt momenteel niet ondersteund Hallo migratie van een bestaande verzameling toosupport geforceerde tunneling.  U moet uw bestaande verzamelingen Hallo VNET tooAzure RemoteApp een koppeling te klikken en een nieuwe één tooget geforceerde tunneling is ingeschakeld op uw verzamelingen maken met toodelete. 

