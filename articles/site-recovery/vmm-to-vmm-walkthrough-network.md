---
title: netwerk voor Hyper-V-replicatie tooa secundaire VMM-site met Azure Site Recovery aaaPlan | Microsoft Docs
description: Dit artikel wordt de planning van het netwerk bij het repliceren van Hyper-V-machines tooa secundaire System Center VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Stap 3: Plannen netwerken voor virtuele machine van Hyper-V-replicatie tooa secundaire VMM-site

Bekijk de vereisten voor implementatie, Lees dit artikel tooplan networking bij het repliceren van Hyper-V virtuele machines (VM's) in System Center Virtual Machine Manager (VMM)-clouds worden beheerd met behulp tooa secundaire site [Azure Site Recovery](site-recovery-overview.md) in hello Azure-portal. 

Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Overzicht van de netwerk-toewijzing

Netwerktoewijzing wordt gebruikt bij het repliceren van Hyper-V-machines (beheerd in VMM) tooa secundair datacenter. Koppelingen van Netwerktoewijzingen tussen VM-netwerken op een bronserver met VMM en VM-netwerken op een VMM-server. Toewijzing Hallo te volgen:

- **Netwerkverbinding**: verbindt VMs tooappropriate netwerken na een failover. Hallo replica-VM zijn doelnetwerk verbonden toohello die is toegewezen toohello Bronnetwerk.
- **Optimale plaatsing**: optimaal plaatsen Hallo replica virtuele machines op Hyper-V-hostservers. Replica-VM's geplaatst op hosts dat de kunnen toegang hello, VM-netwerken toegewezen.
- **Er is geen netwerktoewijzing**— als u geen netwerktoewijzing configureert, replica VMs verbonden tooany VM-netwerken niet na een failover.


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



## <a name="prepare-for-network-mapping"></a>Voorbereiden op netwerktoewijzing

1. Op Hallo bron en doel-VMM-servers, moet u een logisch netwerk is gekoppeld aan de bron en doel clouds Hallo hebben. 
2. In het Hallo-bron- en servers, moet u een logisch netwerk voor VM-netwerk gekoppelde toohello hebben.
3. Virtuele machines op Hyper-V-hosts op de bronlocatie Hallo moet gekoppelde toohello bron-VM-netwerk. Als u slechts één VMM-server gebruikt, kunt u configureren toewijzing tussen VM-netwerken op Hallo dezelfde server.

Dit is wat er gebeurt als u netwerktoewijzing tijdens de implementatie van Site Recovery instellen:

- Als u netwerktoewijzing instellen en selecteer een doel VM-netwerk, wordt Hallo VMM bron clouds die Hallo bron-VM-netwerk weergegeven, samen met de Hallo beschikbare doelservers VM-netwerken op Hallo doel clouds.
- - Als de toewijzing correct is geconfigureerd en replicatie is ingeschakeld, een bron-VM is verbonden tooits bron-VM-netwerk en de replica op de doellocatie Hallo verbonden toegewezen tooits VM-netwerk.
- Als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten dezelfde naam als het subnet op welke Hallo virtuele bronmachine zich bevindt, Hallo vervolgens Hallo Hallo heeft worden replica virtuele machine verbonden toothat Doelsubnet na een failover. Als er geen Doelsubnet met een overeenkomende naam, worden Hallo VM verbonden toohello eerste subnet in het Hallo-netwerk.

## <a name="connect-toovms-after-failover"></a>Verbinding maken met tooVMs na een failover

Bij het plannen van uw replicatie en failoverstrategie is een belangrijke vragen Hallo hoe tooconnect toohello replica na een failover. Er zijn een aantal opties: 

- **Gebruik een ander IP-adres**: U kunt toouse een ander IP-adres voor selecteren Hallo VM gerepliceerd. In dit scenario Hallo VM krijgt een nieuwe IP-adres na een failover en een DNS-update is vereist.
- **Behouden Hallo hetzelfde IP-adres**: U kunt toouse Hallo hetzelfde IP-adres voor Hallo replica-VM. Houden Hallo dezelfde IP-adressen vereenvoudigt Hallo recovery vermindert toegangsproblemen netwerk na een failover. 

## <a name="retain-ip-addresses"></a>IP-adressen behouden

Als u tooretain Hallo IP-adressen wilt van Hallo primaire site na failover toohello secundaire site, kunt u een failover volledige subnet doen en bijwerken van routes tooindicate Hallo nieuwe locatie van Hallo IP-adressen of alternatieve een gespreide subnet tussen Hallo implementeren primaire en Hallo herstellocatie.

### <a name="stretched-subnet"></a>Gespreide subnet

In een gespreide subnet is Hallo subnet beschikbaar tegelijk in beide Hallo primaire en secundaire site. Als u een server en de secundaire site ervan IP (laag 3) configuratie toohello verplaatst, wordt Hallo netwerk Hallo verkeer toohello nieuwe locatie automatisch gerouteerd. 

Vanuit een perspectief Layer 2 (data link-laag) moet u netwerkapparatuur die een gespreide VLAN kunt beheren. Bovendien breidt Hallo potentiële foutdomein door uitrekken Hallo VLAN tooboth sites, wordt in wezen een potentieel risico. Hoewel dit een onwaarschijnlijk, kan het gebeuren dat een broadcast-storm gestart en kan niet geïsoleerd worden. 


### <a name="subnet-failover"></a>Subnet failover

U kunt een subnet failover tooobtain Hallo voordelen van Hallo uitgerekt subnet, uitvoeren zonder het daadwerkelijk uitrekken. In deze oplossing wordt een subnet beschikbaar zijn in de bron- of doelentiteit site hello, maar niet in beide tegelijk. toomaintain hello IP-adresruimte in Hallo gebeurtenis van een failover, kunt u programmatisch rangschikken voor Hallo router infrastructuur toomove Hallo subnetten van één site tooanother. Nadat er bij een storing subnetten zou worden verplaatst met gekoppelde Hallo virtuele machines. het grootste nadeel Hallo is dat in geval van storing Hallo u toomove Hallo hele subnet.

### <a name="example"></a>Voorbeeld

Hier volgt een voorbeeld van een volledige subnet failover. Hallo primaire site heeft toepassingen in een subnet 192.168.1.0/24. Bij een failover alle Hallo virtuele machines in dit subnet wordt een failover uitgevoerd toohello secundaire site en de IP-adressen behouden. Routes moeten toobe gewijzigd tooreflect Hallo feit dat alle Hallo VM virtuele machines die horen toosubnet 192.168.1.0/24 nu toohello secundaire site hebt verplaatst.

Hallo tonen onderstaande afbeeldingen Hallo subnetten vóór en na een failover:

- Vóór de failover is subnet 192.168.0.1/24 actief op de bronsite hello, worden actief op de secundaire site Hallo na een failover.
- Hallo van routes tussen primaire site en de site recovery, derde en primaire site en derde en de site recovery heeft toobe op de juiste wijze zijn gewijzigd.

**Vóór de failover**

![Vóór de Failover](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Na een failover**

![Na een Failover](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Na een failover moet u dit is wat er gebeurt:

- Site Recovery wijst een IP-adres voor elke netwerkinterface op de virtuele machine, Hallo van Hallo statische IP-adresgroep in de relevante netwerk Hallo voor elk exemplaar van VMM.
- Als Hallo IP-adresgroep op de secundaire site Hallo HALLO hallo dezelfde als diegene die op de bronsite hello, Site Recovery wijst hetzelfde IP-adres (van Hallo bron-VM) toohello replica-VM. Hallo IP-adres is gereserveerd in VMM, maar het is niet ingesteld als Hallo failover-IP-adres op Hallo Hyper-V-host. Hallo failover-IP-adres op een Hyper-v-host is ingesteld op net vóór Hallo failover.
- Als hello hetzelfde IP-adres niet beschikbaar is, wijst Site Recovery een ander beschikbaar IP-adres uit groep Hallo.
- Als VMs DHCP gebruikt, beheert de Site Recovery niet Hallo IP-adressen. U moet toocheck die Hallo DHCP-server op Hallo secundaire site-adres uit hetzelfde bereik als bronsite Hallo Hallo kunt toewijzen.

### <a name="validate-hello-ip-address"></a>Hallo IP-adres valideren

Nadat u de beveiliging voor een virtuele machine hebt ingeschakeld, kunt u de volgende sample script tooverify Hallo-adres is toegewezen toohello VM. Hallo hetzelfde IP-adres worden ingesteld als Hallo failover-IP-adres, en toegewezen toohello VM op moment van failover Hallo:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Het wijzigen van IP-adressen

In dit scenario worden Hallo IP-adressen van virtuele machines die een failover gewijzigd. Hallo nadeel van deze oplossing is Hallo onderhoud vereist. Normaal gesproken worden DNS bijgewerkt nadat de replica-VM start. DNS-vermeldingen mogelijk moet u toobe gewijzigd of fluster in thenetwork en vermeldingen in cache bijgewerkt. Dit kan leiden tot uitvaltijd. Uitvaltijd kan worden opgevangen volgt als volgt:

- Lage TTL-waarden voor intranettoepassingen gebruiken.
- Hallo na script in een Site Recovery-herstelplan tooupdate Hallo DNS-server tooensure een tijdige update gebruiken. U hoeft niet Hallo script als u dynamische DNS-registratie.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Voorbeeld 

We bekijken een scenario waarin u van plan bent toouse verschillende IP-adressen op Hallo van primaire en Hallo herstellocatie. In dit voorbeeld hebben we verschillende IP-adressen op primaire en secundaire sites en er; s een externe site uit welke toepassingen die worden gehost op de primaire of herstel site Hallo toegankelijk zijn.

- Voordat u failover apps gehoste subnet 192.168.1.0/24 op Hallo primaire site zijn en zijn geconfigureerde toobe in 172.16.1.0/24 subnet op de secundaire site Hallo na een failover.
- VPN-verbindingen/netwerkroutes zijn op de juiste wijze geconfigureerd zodat alle drie sites toegang elkaar tot hebben.
- Na een failover wordt in Hallo herstel subnet apps worden hersteld. In dit scenario er is geen toofail nodig via Hallo gehele subnet en er zijn geen wijzigingen nodig tooreconfigure VPN- of netwerkbeheerder routes. Zorg ervoor dat toepassingen toegankelijk blijven Hallo failover en een aantal DNS-updates.
- Als DNS geconfigureerde tooallow dynamische updates, vervolgens registreert Hallo VM's zelf Hallo nieuwe IP-adres via wanneer ze na een failover wordt gestart.

**Vóór de failover**

![Verschillende IP - vóór de Failover](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Na een failover**

![Verschillende IP - na een Failover](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Volgende stappen

Ga te[stap 4: VMM voorbereiden en Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


