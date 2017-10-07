---
title: netwerk voor Hyper-V (zonder de System Center VMM) tooAzure replicatie met Azure Site Recovery aaaPlan | Microsoft Docs
description: Dit artikel wordt beschreven netwerkplanning vereist wanneer tooAzure Hyper-V-machines (zonder VMM) repliceren
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a>Stap 4: De netwerken voor Hyper-V tooAzure replicatie plannen

In dit artikel bevat een overzicht van netwerk planningsoverwegingen bij het repliceren van lokale Hyper-V-machines (zonder de System Center VMM) tooAzure met Hallo [Azure Site Recovery](site-recovery-overview.md) service.

Eventuele opmerkingen onder Hallo van dit artikel plaatsen of vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connecting-tooreplica-vms-after-failover"></a>Verbinding maken met virtuele machines tooreplica na een failover

Bij het plannen van uw replicatie en failoverstrategie is een belangrijke vragen Hallo hoe tooconnect toohello virtuele Azure-machine na een failover. Er zijn een aantal opties bij het ontwerpen van uw netwerk-strategie voor de replica virtuele Azure-machines:

- **Ander IP-adres**: U kunt toouse een ander IP-adresbereik voor selecteren Hallo gerepliceerd Azure VM-netwerk. In dit scenario Hallo VM krijgt een nieuwe IP-adres na een failover en een DNS-update is vereist. [Meer informatie](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- **Hetzelfde IP-adres**: U kunt toouse Hallo hetzelfde IP-adresbereik als die op uw primaire on-premises netwerk, voor hello Azure-netwerk na een failover.  Houden Hallo dezelfde IP-adressen vereenvoudigt Hallo recovery vermindert toegangsproblemen netwerk na een failover. Echter, wanneer u tooAzure repliceert, moet u tooupdate routes met de nieuwe locatie Hallo Hallo IP-adressen na een failover.


## <a name="retain-ip-addresses"></a>IP-adressen behouden

Site Recovery biedt Hallo mogelijkheid tooretain vaste IP-adressen wanneer failover tooAzure met de failover van een subnet.

Met subnet-failover is een specifiek subnet aanwezig op de Site 1 of 2, maar niet op beide sites tegelijkertijd. In volgorde toomaintain Hallo IP-adresruimte in Hallo gebeurtenis van een failover rangschikt u programmatisch voor Hallo router infrastructuur toomove Hallo subnetten van één site tooanother. Tijdens de failover gekoppelde Hallo subnetten verplaatsen Hello beveiligde virtuele machines. het grootste nadeel Hallo is dat in geval van storing Hallo u toomove Hallo hele subnet.


### <a name="failover-example"></a>Failover-voorbeeld

Bekijk een voorbeeld van failover-tooAzure.

- Een ficticious bedrijf Woodgrove Bank, heeft een on-premises infrastructuur die als host fungeert voor de business-apps. Hun mobiele toepassingen worden gehost op Azure.
- Connectiviteit tussen de Woodgrove Bank virtuele machines in Azure en on-premises servers wordt verstrekt door een site-naar-site (VPN)-verbinding tussen Hallo on-premises rand netwerk en Hallo virtuele Azure-netwerk.
- Dit VPN-betekent dat het virtuele netwerk van bedrijf in Azure Hallo wordt weergegeven als een uitbreiding van hun on-premises netwerk.
- Woodgrove wil toouse siteherstel tooreplicate lokale werkbelastingen tooAzure.
 - Woodgrove heeft toodeal met toepassingen en configuraties die afhankelijk zijn van vastgelegde IP-adressen en dus tooretain IP-adressen voor hun toepassingen na failover tooAzure nodig.
 - Woodgrove heeft IP-adressen worden toegewezen uit het bereik 172.16.1.0/24, 172.16.2.0/24 tooits resources in Azure wordt uitgevoerd.


Woodgrove toobe kunnen tooreplicate de tooAzure VMs terwijl behouden Hallo IP-adressen, is dit wat Hallo bedrijf behoefte heeft aan toodo:

1. Maak een Azure-netwerk. Deze moet een extensie van Hallo lokale netwerk, zodat toepassingen naadloos kunnen failover.
2. Azure kunt u tooadd site-naar-site VPN-verbindingen naast toopoint-naar-site-connectiviteit toohello virtuele netwerken in Azure gemaakt.
3. Wanneer u site-naar-site-verbinding Hallo instelt, in hello Azure-netwerk, kunt u verkeer toohello on-premises locatie (LAN) routeren alleen als Hallo IP-adresbereik verschilt van Hallo lokale IP-adresbereik.
    - Dit is omdat Azure biedt geen ondersteuning voor gespreide subnetten. Als u beschikt over subnet 192.168.1.0/24 on-premises, kan u dus een lokaal netwerk 192.168.1.0/24 toevoegen aan hello Azure-netwerk.
    - Dit is normaal omdat Azure niet weet dat er geen actieve VM's in Hallo subnet zijn en dat Hallo-subnet wordt gemaakt voor alleen herstel na noodgevallen.
    - toobe kunnen toocorrectly netwerkverkeer buiten een Azure-netwerk Hallo subnetten in Hallo netwerk- en LAN Hallo mag niet in conflict.

![Vóór de subnet-failover](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Vóór de failover

1. Maak een extra netwerk (bijvoorbeeld herstel netwerk). Dit is Hallo-netwerk op die failover van virtuele machines worden gemaakt.
2. tooensure die hello IP-adres voor een virtuele machine wordt bewaard na een failover, in de eigenschappen van de VM Hallo > **configureren**, geef dezelfde IP-adres dat Hallo VM een on-premises en klikt u op Hallo **opslaan**.
3. Wanneer Hallo VM failover wordt uitgevoerd, wordt de Azure Site Recovery Hallo opgegeven IP-adres tooit toewijzen.

    ![Eigenschappen van het netwerk](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. Nadat de failover is de trigger wordt geactiveerd en Hallo VM's zijn gemaakt in Azure met Hallo vereist IP-adres, u kunt verbinden toohello netwerk via een [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Deze actie kan scripts worden gebruikt.
5. Routes moeten op de juiste wijze zijn gewijzigd, toobe tooreflect die 192.168.1.0/24 is nu tooAzure verplaatst.

    ![Na een failover van subnet](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Na een failover

Als u niet een Azure-netwerk hebt, zoals wordt geïllustreerd hierboven, kunt u een site-naar-site VPN-verbinding tussen de primaire site en Azure na failvoer maken.

## <a name="change-ip-addresses"></a>IP-adressen wijzigen

Dit [blogbericht](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) wordt uitgelegd hoe tooset up hello Azure netwerkinfrastructuur wanneer u niet tooretain IP hoeft-adressen na een failover. Deze begint met een toepassingsbeschrijving, lijkt op hoe tooset netwerkinstellingen lokaal en in Azure en wordt afgesloten met informatie over het uitvoeren van failovers.  

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 5: Azure voorbereiden](hyper-v-site-walkthrough-prepare-azure.md)
