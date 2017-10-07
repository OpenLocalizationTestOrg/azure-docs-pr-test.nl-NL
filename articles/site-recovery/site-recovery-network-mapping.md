---
title: de netwerktoewijzing aaaPlan voor virtuele machine van Hyper-V-replicatie met Site Recovery | Microsoft Docs
description: Stel netwerktoewijzing voor replicatie van Hyper-V-virtuele machine van een lokaal datacenter tooAzure of tooa secundaire site.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Plan de netwerktoewijzing voor virtuele machine van Hyper-V-replicatie met Site Recovery



Dit artikel helpt u toounderstand en plannen voor netwerk toewijzen tijdens de replicatie van Hyper-V-machines tooAzure of tooa secundaire site, met behulp van Hallo [Azure Site Recovery-service](site-recovery-overview.md).

Na het lezen van dit artikel na de eventuele opmerkingen onder Hallo van dit artikel of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Netwerktoewijzing voor replicatie tooAzure

Netwerktoewijzing wordt gebruikt bij het repliceren van Hyper-V-machines (beheerd in VMM) tooAzure. Toewijzing toewijzingen tussen VM-netwerken op een bronserver met VMM-netwerk en Azure-netwerken zijn gericht. Toewijzing Hallo te volgen:

- **Netwerkverbinding**: zorgt ervoor dat de gerepliceerde Azure Virtual machines toegewezen netwerk verbonden toohello zijn. Alle machines die een failover op Hallo dezelfde netwerk verbinding maken met tooeach andere, zelfs als ze zich in verschillende herstelplannen failover.
- **Netwerkgateway**— als een netwerkgateway is ingesteld op Hallo Azure-doelnetwerk, virtuele machines tooother on-premises virtuele machines verbinding kunnen maken.

Opmerking:

- Een bron-VMM VM-netwerk tooan virtuele Azure-netwerk worden toegewezen.
- Na een failover Azure VM's in Hallo worden Bronnetwerk verbonden toohello toegewezen doel virtueel netwerk.
- Nieuwe virtuele machines toegevoegd toohello bron-VM-netwerk zijn verbonden toohello toegewezen Azure-netwerk wanneer er replicatie plaatsvindt.
- Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtuele machine zich bevindt en vervolgens Hallo replica virtuele machine verbindt toothat Doelsubnet na een failover.
- Als er geen Doelsubnet met een overeenkomende naam, verbindt Hallo virtuele machine toohello eerste subnet in het Hallo-netwerk.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Netwerktoewijzing voor replicatie tooa secundair datacenter

Netwerktoewijzing wordt gebruikt bij het repliceren van Hyper-V-machines (beheerd in System Center Virtual Machine Manager (VMM)) tooa secundair datacenter. Koppelingen van Netwerktoewijzingen tussen VM-netwerken op een bronserver met VMM en VM-netwerken op een VMM-server. Toewijzing Hallo te volgen:

- **Netwerkverbinding**: verbindt VMs tooappropriate netwerken na een failover. Hallo replica-VM zijn doelnetwerk verbonden toohello die is toegewezen toohello Bronnetwerk.
- **Optimale plaatsing**: optimaal plaatsen Hallo replica virtuele machines op Hyper-V-hostservers. Replica-VM's geplaatst op hosts dat de kunnen toegang hello, VM-netwerken toegewezen.
- **Er is geen netwerktoewijzing**— als u geen netwerktoewijzing configureert, replica VMs verbonden tooany VM-netwerken niet na een failover.

Opmerking:

- Netwerktoewijzing kunnen worden geconfigureerd tussen VM-netwerken op twee VMM-servers of op één VMM-server als de twee sites worden beheerd door dezelfde Hallo server.
- Als de toewijzing correct is geconfigureerd en replicatie is ingeschakeld, worden een virtuele machine op de primaire locatie Hallo tooa verbonden netwerk en de replica op de doellocatie Hallo worden aangesloten toegewezen tooits netwerk.
-
- Als netwerken hebt wanneer u een VM-netwerk van het doel bij netwerktoewijzing selecteert in VMM correct is ingesteld, wordt Hallo VMM bron clouds die Hallo bron-VM-netwerk weergegeven, samen met de Hallo beschikbare doelservers VM-netwerken op Hallo doel clouds die worden gebruikt voor beveiliging.
- Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten dezelfde naam als het subnet op welke Hallo virtuele bronmachine zich bevindt, Hallo vervolgens Hallo Hallo heeft worden replica virtuele machine verbonden toothat Doelsubnet na een failover. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.



### <a name="example"></a>Voorbeeld

Hier volgt een voorbeeld tooillustrate dit mechanisme. U gaat nu een organisatie met twee locaties in New York en Chicago.

**Locatie** | **VMM-server** | **VM-netwerken** | **Toegewezen aan**
---|---|---|---
New York | VMM-NewYork| VMNetwork1 NewYork | Toegewezen tooVMNetwork1-Chicago
 |  | VMNetwork2 NewYork | Niet toegewezen
Chicago | VMM-Chicago| VMNetwork1 Chicago | Toegewezen tooVMNetwork1-NewYork
 | | VMNetwork1 Chicago | Niet toegewezen

In dit voorbeeld:

- Wanneer een replica virtuele machine wordt gemaakt voor elke virtuele machine die is verbonden tooVMNetwork1-NewYork, zal de tooVMNetwork1-Chicago verbonden zijn.
- Wanneer een replica virtuele machine wordt gemaakt voor VMNetwork2 NewYork of VMNetwork2 Chicago, het is niet verbonden tooany netwerk mogelijk.

Hier volgt hoe VMM-clouds in ons voorbeeldorganisatie en Hallo logische netwerken die zijn gekoppeld aan clouds Hallo zijn ingesteld.

#### <a name="cloud-protection-settings"></a>Instellingen voor cloudbeveiliging

**Beveiligde cloud** | **Beveiligen van de cloud** | **Logisch netwerk (Den Haag)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>N.v.t.</p><p></p> | <p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p>
SilverCloud2 | <p>N.v.t.</p><p></p> | <p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Logische schijf als VM-netwerkinstellingen

**Locatie** | **Logisch netwerk** | **Bijbehorende VM-netwerk**
---|---|---
New York | LogicalNetwork1 NewYork | VMNetwork1 NewYork
Chicago | LogicalNetwork1 Chicago | VMNetwork1 Chicago
 | LogicalNetwork2Chicago | VMNetwork2 Chicago

#### <a name="target-network-settings"></a>Doel-netwerkinstellingen

Op basis van deze instellingen wanneer u Hallo doel VM-netwerk selecteert, worden Hallo tabel Hallo-opties die beschikbaar zijn.

**Selecteren** | **Beveiligde cloud** | **Beveiligen van de cloud** | **Doelnetwerk beschikbaar**
---|---|---|---
VMNetwork1 Chicago | SilverCloud1 | SilverCloud2 | Beschikbaar
 | GoldCloud1 | GoldCloud2 | Beschikbaar
VMNetwork2 Chicago | SilverCloud1 | SilverCloud2 | Niet beschikbaar
 | GoldCloud1 | GoldCloud2 | Beschikbaar


Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten dezelfde naam als het subnet op welke Hallo virtuele bronmachine zich bevindt, Hallo vervolgens Hallo Hallo heeft worden replica virtuele machine verbonden toothat Doelsubnet na een failover. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.


#### <a name="failback-behavior"></a>Failback gedrag

Wat gebeurt er in geval van failback (omgekeerde replicatie) Hallo toosee gaan we ervan uit dat VMNetwork1 NewYork is toegewezen tooVMNetwork1-Chicago, hello instellingen te volgen.


**Virtuele machine** | **TooVM verbonden netwerk**
---|---
VM1 | VMNetwork1-netwerk
VM2 (replica van VM1) | VMNetwork1 Chicago

Met deze instellingen gaan we bekijken wat er gebeurt in een aantal mogelijke scenario's.

**Scenario** | **Resultaat**
---|---
Geen wijziging in hello netwerkgegevens van VM-2 na een failover. | VM-1 blijft verbonden toohello Bronnetwerk.
Netwerkeigenschappen van VM-2 worden gewijzigd na een failover en is verbroken. | VM-1 wordt verbroken.
Netwerkeigenschappen van VM-2 zijn gewijzigd na een failover en is verbonden tooVMNetwork2-Chicago. | Als VMNetwork2 Chicago niet is toegewezen, kunt u VM-1 wordt verbroken.
Netwerktoewijzing van VMNetwork1 Chicago wordt gewijzigd. | VM-1 zijn verbonden toohello netwerk nu toegewezen tooVMNetwork1-Chicago.



## <a name="next-steps"></a>Volgende stappen

Meer informatie over [Hallo netwerkinfrastructuur planning](site-recovery-network-design.md).
