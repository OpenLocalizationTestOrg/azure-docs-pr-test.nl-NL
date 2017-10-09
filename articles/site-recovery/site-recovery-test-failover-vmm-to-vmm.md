---
title: aaaTest failover (VMM tooVMM) in Azure Site Recovery | Microsoft Docs
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
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Testfailover (VMM tooVMM) in Site Recovery


In dit artikel bevat informatie en instructies voor het uitvoeren van een testfailover of een detailanalyse disaster recovery (DR) van virtuele machines (VM's) en fysieke servers die zijn beveiligd met Azure Site Recovery. Als de herstelsite Hallo gebruikt u een System Center Virtual Machine Manager VMM beheerde on-premises site.

U uw replicatiestrategie voor van een failover-test toovalidate uitvoeren of een details voor Dr zonder verlies van gegevens of uitvaltijd. Een testfailover heeft geen invloed op Hallo lopende replicatie of op uw productieomgeving. U kunt uitvoeren op een virtuele machine of een [herstelplan](site-recovery-create-recovery-plans.md). Wanneer u een testfailover activeren wilt, moet u toospecify Hallo netwerk dat Hallo test-virtuele machines verbinding maken. U kunt de voortgang van de testfailover Hallo Hallo bijhouden op Hallo **taken** pagina.  

Als u eventuele opmerkingen of vragen hebt, plaatst u deze op Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Hallo-infrastructuur voorbereiden voor testfailover
Als u een testfailover toorun wilt met behulp van een bestaand netwerk, bereid u Active Directory, DHCP en DNS-in dit netwerk.

Als u toorun een testfailover wilt automatisch via Hallo optie toocreate VM-netwerken, voegt u een handmatige stap voordat de groep 1 in Hallo herstelplan dat u toouse voor testfailover Hallo gaat. Vervolgens voegt u Hallo infrastructuur resources toohello automatisch gemaakt netwerk voordat u Hallo testfailover uitvoeren.

### <a name="things-toonote"></a>Dingen toonote
Wanneer u bent bezig met repliceren tooa secundaire site, Hallo type netwerk dat Hallo replica-machine gebruikt toomatch Hallo type logische netwerk dat wordt gebruikt voor een testfailover niet nodig, maar sommige combinaties niet werkt mogelijk. Als Hallo replica maakt gebruik van DHCP- en isolatie op basis van een VLAN, hoeft Hallo VM-netwerk voor Hallo replica niet een statische IP-adresgroep. Met behulp van Windows-Netwerkvirtualisatie voor de testfailover Hallo werkt niet omdat geen-adresgroepen beschikbaar zijn. 

Bovendien werkt Hallo testfailover niet als Hallo replica netwerk zonder isolatie en Hallo testnetwerk Windows-Netwerkvirtualisatie gebruikt. Dit komt doordat de netwerk zonder isolatie Hallo Hallo subnetten vereist toocreate beschikt niet over een Windows-Netwerkvirtualisatie-netwerk.

Hoe gerepliceerde virtuele machines verbonden toomapped VM-netwerken zijn nadat de failover is afhankelijk van hoe Hallo VM-netwerk is geconfigureerd in Hallo VMM-console.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>VM-netwerk is geconfigureerd met geen isolatie- of VLAN-isolatie
Als DHCP voor Hallo VM-netwerk is gedefinieerd, is het Hallo replica virtuele machine verbonden toohello VLAN-ID via Hallo-instellingen die zijn opgegeven voor de netwerksite Hallo in Hallo gekoppeld logisch netwerk. Hallo virtuele machine ontvangt het IP-adres van Hallo beschikbare DHCP-server. 

U hoeft niet toodefine een statische IP-adresgroep voor Hallo doel VM-netwerk. Als een statische IP-adresgroep voor Hallo VM-netwerk wordt gebruikt, is Hallo replica virtuele machine verbonden toohello VLAN-ID via Hallo-instellingen die zijn opgegeven voor de netwerksite Hallo in Hallo gekoppeld logisch netwerk.

Hallo virtuele machine ontvangt het IP-adres van Hallo-adresgroep die gedefinieerd voor Hallo VM-netwerk. Als een statische IP-adresgroep is niet gedefinieerd op Hallo doel VM-netwerk, mislukt de toewijzing van IP-adres. Hallo IP-adresgroep maken op beide Hallo bron en doel-VMM-servers die u voor beveiliging als herstel gebruiken wilt.

#### <a name="vm-network-with-windows-network-virtualization"></a>VM-netwerk met Windows-Netwerkvirtualisatie
Als een VM-netwerk is geconfigureerd met Windows-Netwerkvirtualisatie, moet u een statische adresgroep voor Hallo doel VM-netwerk, ongeacht of Hallo bron-VM-netwerk geconfigureerd toouse DHCP is of een statisch IP-adresgroep definiëren. 

Als u DHCP definieert, worden de Hallo doel-VMM-server fungeert als een DHCP-server en biedt een IP-adres uit groep Hallo die gedefinieerd voor Hallo doel VM-netwerk. Als het gebruik van een statische IP-adresgroep is gedefinieerd voor de bronserver hello, wijst Hallo doel-VMM-server een IP-adres uit groep Hallo. In beide gevallen mislukt toewijzing van IP-adres als een statische IP-adresgroep is niet gedefinieerd.


### <a name="prepare-dhcp"></a>DHCP voorbereiden
Als Hallo virtuele machines die zijn betrokken bij de wordt testfailover gebruik van DHCP, maakt u een DHCP-server van de test binnen Hallo geïsoleerd netwerk voor Hallo doel van de testfailover.

### <a name="prepare-active-directory"></a>Active Directory voorbereiden
toorun een testfailover voor de toepassing testen, moet u een kopie van de Active Directory productieomgeving Hallo in uw testomgeving. Raadpleeg voor meer informatie, Hallo [testfailover-overwegingen voor Active Directory](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>DNS voorbereiden
Een DNS-server voor de testfailover Hallo als volgt voorbereiden:

* **DHCP**: als virtuele machines DHCP, Hallo IP-adres van de test Hallo DNS op Hallo test DHCP-server moet worden bijgewerkt. Als u een met het netwerktype Windows-Netwerkvirtualisatie, wordt de Hallo VMM-server fungeert als Hallo DHCP-server. Hallo IP-adres van DNS-moet daarom worden bijgewerkt in Hallo testfailovernetwerk. In dit geval registreren Hallo virtuele machines zichzelf toohello relevante DNS-server.
* **Statisch adres**: als virtuele machines met een statisch IP-adres, IP-adres van DNS-server moet worden bijgewerkt in het testfailovernetwerk Hallo-test Hallo. Mogelijk moet u tooupdate DNS met IP-adres Hallo Hallo test-virtuele machines. U kunt Hallo voorbeeldscript voor dit doel te volgen:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Een testfailover uitvoeren
Deze procedure wordt beschreven hoe toorun een testfailover voor een herstel van plan bent. U kunt ook Hallo failover voor een enkele virtuele machine uitvoeren op Hallo **virtuele Machines** tabblad.

![Failover-blade test](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Selecteer **herstelplannen** > *recoveryplan_name*. Klik op **Failover** > **Testfailover**.
1. Op Hallo **Testfailover** blade opgeven hoe virtuele machines worden verbonden toonetworks na Hallo testfailover. Zie voor meer informatie, Hallo [netwerkopties](#network-options-in-site-recovery).
1. Voortgang van de failover volgen op Hallo **taken** tabblad.
1. Nadat de failover is voltooid, controleert u of Hallo virtuele machines zijn gestart.
1. Wanneer u bent klaar, klikt u op **testfailover opschonen** op Hallo herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo. Deze stap verwijdert Hallo virtuele machines en netwerken die zijn gemaakt tijdens de testfailover.


## <a name="network-options-in-site-recovery"></a>Netwerkopties in Site Recovery

Wanneer u een failovertest uitvoert, wordt u gevraagd tooselect netwerkinstellingen voor test-replica-machines. U hebt meerdere mogelijkheden.  

| **Testen van failover-optie** | **Beschrijving** | **Controle van failover** | **Details** |
| --- | --- | --- | --- |
| **Failover tooa secundaire VMM-site--zonder netwerk** |Selecteer een VM-netwerk niet. |Failover wordt gecontroleerd dat de test-machines worden gemaakt.<br/><br/>Hallo test-virtuele machine wordt gemaakt op Hallo host waar Hallo replica virtuele machine bestaat. Deze is niet toohello cloud waar Hallo replica virtuele machine zich bevindt toegevoegd. |<p>Hallo failover machine is niet verbonden tooany netwerk.<br/><br/>Hallo machine mag verbonden tooa VM-netwerk nadat deze is gemaakt. |
| **Failover tooa secundaire VMM-site--met het netwerk** |Selecteer een bestaand VM-netwerk. |Failover wordt gecontroleerd of de virtuele machines worden gemaakt. |Hallo test-virtuele machine wordt gemaakt op Hallo host waar Hallo replica virtuele machine bestaat. Deze is niet toohello cloud waar Hallo replica virtuele machine zich bevindt toegevoegd.<br/><br/>Maak een VM-netwerk dat is geïsoleerd van uw productienetwerk.<br/><br/>Als u een VLAN-netwerk gebruikt, raden wij u een afzonderlijke logische netwerk (niet gebruikt in productie) maken in VMM voor dit doel. Dit logische netwerk is gebruikte toocreate VM-netwerken voor testfailovers.<br/><br/>Hallo logisch netwerk moet worden gekoppeld aan ten minste één van de netwerkadapters Hallo van alle Hallo Hyper-V-servers die als van virtuele machines host.<br/><br/>Hallo voor VLAN logische netwerken, netwerksites dat u toevoegt, toohello logisch netwerk worden geïsoleerd.<br/><br/>Als u een logisch netwerk voor op basis van Windows-Netwerkvirtualisatie, maakt Azure Site Recovery automatisch geïsoleerde VM-netwerken. |
| **Mislukken via tooa secundaire VMM-site, een netwerk maken** |Een tijdelijke testnetwerk is gemaakt op basis van het Hallo-instelling die u opgeeft in automatisch **logisch netwerk** en de bijbehorende netwerksites. |Failover wordt gecontroleerd of de virtuele machines worden gemaakt. |Gebruik deze optie als het herstelplan Hallo maakt gebruik van meer dan één VM-netwerk. Als u Windows-Netwerkvirtualisatie-netwerken, maken deze optie automatisch VM-netwerken met Hallo dezelfde instellingen (subnetten en IP-adresgroepen) in Hallo-netwerk van Hallo replica virtuele machine. Deze VM-netwerken zijn automatisch opgeschoond nadat Hallo testfailover voltooid is.</p><p>Hallo test-virtuele machine wordt gemaakt op Hallo host waar Hallo replica virtuele machine bestaat. Deze is niet toohello cloud waar Hallo replica virtuele machine zich bevindt toegevoegd. |

> [!TIP]
> Hallo IP-adres opgegeven tooa virtuele machine tijdens de testfailover is Hallo hetzelfde IP-adres die virtuele machine Hallo zou ontvangen voor een geplande of niet-geplande failover (ervan uitgaande dat Hallo IP-adres beschikbaar in het testfailovernetwerk Hallo is). Als hello hetzelfde IP-adres is niet beschikbaar in het testfailovernetwerk hello, ontvangt Hallo virtuele machine een ander IP-adres dat beschikbaar is in het testfailovernetwerk Hallo.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Testen van failover tooa productienetwerk op een site recovery
Het is raadzaam dat als u een failovertest uitvoert, u een netwerk dat verschilt van het herstel site productienetwerk die u hebt opgegeven in [netwerktoewijzing](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Maar als u toch toovalidate end-to-end-netwerkverbinding in een failover-virtuele machine, houd er rekening mee Hallo volgende punten:

* Zorg ervoor dat Hallo de primaire virtuele machine wordt afgesloten wanneer u Hallo testfailover uitvoert. Als u niet twee virtuele machines met dezelfde identiteit wordt uitgevoerd in het netwerk op Hallo HALLO hallo dezelfde tijd. Deze situatie kan tooundesired gevolgen leiden.
* Toohello testen van failover-virtuele machines te maken wijzigingen gaan verloren wanneer u opschonen Hallo failover virtuele machines test. Deze wijzigingen zijn niet-gerepliceerde back toohello primaire virtuele machine.
* Deze werkwijze testen leidt toodowntime voor uw productietoepassing. Vraag gebruikers van de toepassing hello niet toouse toepassing hello wanneer Hallo DR inzoomen wordt uitgevoerd.  


## <a name="next-steps"></a>Volgende stappen
Nadat u een testfailover met succes hebt uitgevoerd, kunt u proberen een [failover](site-recovery-failover.md).
