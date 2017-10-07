---
title: aaaProtect Active Directory en DNS met Azure Site Recovery | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooimplement een oplossing voor het herstel na noodgevallen voor Active Directory met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Active Directory en DNS met Azure Site Recovery beveiligen
Enterprise-toepassingen zoals SharePoint, Dynamics AX en SAP afhankelijk van Active Directory en een DNS-infrastructuur toofunction correct. Wanneer u een oplossing voor het herstel na noodgevallen voor toepassingen maakt, is belangrijk tooremember die u tooprotect moet en herstellen van Active Directory en DNS voordat Hallo andere toepassingsonderdelen, tooensure die dingen naar behoren functioneren als een noodsituatie voordoet.

Site Recovery is een Azure-service waarmee herstel na noodgevallen door te organiseren replicatie, failovers en herstel van virtuele machines. Site Recovery biedt ondersteuning voor een aantal scenario's met replicatie tooconsistently beveiligen en naadloos failover virtuele machines en toepassingen tooprivate of openbare hoster clouds.

Site Recovery kunt u een herstelplan volledig geautomatiseerd noodherstel maken voor Active Directory. Wanneer er storingen optreden, kunt u initieer een failover binnen enkele seconden vanaf elke locatie en ophalen van Active Directory actief en werkend in enkele minuten duren. Als u Active Directory voor meerdere toepassingen zoals SharePoint en SAP in uw primaire site hebt geïmplementeerd en u wilt dat toofail via Hallo volledige site, kunt u een failover Active Directory eerste met behulp van Site Recovery en vervolgens een failover Hallo andere toepassingen met behulp van toepassingsspecifieke herstelplannen.

Dit artikel wordt uitgelegd hoe toocreate een oplossing voor het herstel na noodgevallen voor Active Directory, hoe tooperform geplande, niet-geplande en testfailovers met behulp van een herstelplan met één klik Hallo ondersteunde configuraties en vereisten.  U moet bekend bent met Active Directory en Azure Site Recovery voordat u begint.

## <a name="replicating-domain-controller"></a>Bezig met het repliceren van domeincontroller

U moet toosetup [replicatie van Site Recovery](#enable-protection-using-site-recovery) op ten minste één virtuele machine-domeincontroller en DNS-te hosten. Als u hebt [meerdere domeincontrollers](#environment-with-multiple-domain-controllers) in uw omgeving, Hallo tooreplicating bovendien domain controller virtuele machine met Site Recovery u ook tooset van hebt een [extra domeincontroller](#protect-active-directory-with-active-directory-replication) op de doelsite hello (Azure of een secundaire on-premises datacenter). 

### <a name="single-domain-controller-environment"></a>Één domeincontroller-omgeving
Als u een aantal toepassingen en slechts één domeincontroller hebt, en toofail gedurende de gehele site Hallo samen gewenste, dan wordt u aangeraden Site Recovery tooreplicate Hallo domeincontroller toohello secundaire site (of u bent failover wordt uitgevoerd tooAzure of tooa secundaire site). Hallo dezelfde gerepliceerd domain controller en DNS-virtuele machine kan worden gebruikt voor [failover testen](#test-failover-considerations) ook.

### <a name="environment-with-multiple-domain-controllers"></a>Omgeving met meerdere domeincontrollers
Als u veel toepassingen hebt en er is meer dan één domeincontroller in de omgeving Hallo of als u van plan toofail via enkele toepassingen op een tijdstip bent, raden wij aan dat bovendien tooreplicating Hallo-domeincontroller van een virtuele machine met Site Recovery u ook instellen van een [extra domeincontroller](#protect-active-directory-with-active-directory-replication) op de doelsite hello (Azure of een secundaire on-premises datacenter). Voor [testfailover](#test-failover-considerations), u gerepliceerd door Site Recovery en voor failover, Hallo extra domeincontroller op de doelsite Hallo domeincontroller gebruiken. 


Hallo volgende secties wordt uitgelegd hoe tooenable beveiliging voor een domeincontroller in de Site is hersteld, en hoe tooset van een domeincontroller in Azure.

## <a name="prerequisites"></a>Vereisten
* Een on-premises implementatie van Active Directory en DNS-server.
* Een Azure Site Recovery Services-kluis in een Microsoft Azure-abonnement.
* Als u tooAzure repliceert, hello Azure virtuele Machine Readiness Assessment tool uitvoeren op virtuele machines tooensure zijn ze compatibel met virtuele Azure-machines en Azure Site Recovery-Services.

## <a name="enable-protection-using-site-recovery"></a>Schakel de beveiliging met Site Recovery
### <a name="protect-hello-virtual-machine"></a>Hallo virtuele machine te beveiligen
Schakel de beveiliging van Hallo domain controller en DNS-virtuele machine in Site Recovery. Site Recovery-instellingen op basis van Hallo virtuele machinetype (Hyper-V- of VMware) configureren. Hallo-domeincontroller die is gerepliceerd met Site Recovery wordt gebruikt voor [testfailover](#test-failover-considerations). Zorg ervoor dat het voldoet aan Hallo volgens de vereisten:

1. Hallo-domeincontroller is een globale catalogusserver
2. Hallo-domeincontroller moet Hallo FSMO-roleigenaar voor functies die nodig tijdens een testfailover zijn (deze rollen moet anders toobe [overgenomen](http://aka.ms/ad_seize_fsmo) na een failover Hallo)

### <a name="configure-virtual-machine-network-settings"></a>Netwerkinstellingen van de virtuele machine configureren
Voor Hallo domain controller en DNS-virtuele machine netwerkinstellingen configureren in Site Recovery zodat Hallo virtuele machine de juiste netwerk aangesloten toohello na een failover. 

![VM-netwerkinstellingen](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Beveiligen van Active Directory met Active Directory-replicatie
### <a name="site-to-site-protection"></a>Site-naar-site-beveiliging
Maak een domeincontroller op Hallo secundaire site. Als u Hallo server tooa rol domeincontroller promoveert, Hallo naam opgeven van Hallo hetzelfde domein bevinden dat wordt gebruikt op Hallo primaire site. U kunt Hallo **Active Directory: Sites en Services** module tooconfigure instellingen op de sitekoppeling Hallo object toowhich Hallo sites worden toegevoegd. Instellingen configureren op een site-koppeling, kunt u bepalen wanneer replicatie plaatsvindt tussen twee of meer sites, en hoe vaak. Zie voor meer informatie [replicatie tussen Sites plannen](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Beveiliging van de site naar Azure
Hallo-instructies te volgen[maken van een domeincontroller in een Azure-netwerk](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Wanneer u Hallo server tooa rol domeincontroller promoveert, geef Hallo dezelfde domeinnaam die wordt gebruikt op Hallo primaire site.

Vervolgens [Hallo DNS-server voor het virtuele netwerk Hallo opnieuw configureren](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), toouse Hallo DNS-server in Azure.

![Azure-netwerk](./media/site-recovery-active-directory/azure-network.png)

**DNS-server in Azure productienetwerk**

## <a name="test-failover-considerations"></a>Testfailover-overwegingen
Testfailover treedt op in een netwerk dat is geïsoleerd van productienetwerk, zodat er geen gevolgen voor de productie-workloads zijn.

De meeste toepassingen moet ook Hallo aanwezigheid van een domeincontroller en een DNS-server toofunction. Daarom voordat de toepassing hello failover wordt uitgevoerd, moet een domeincontroller toobe in Hallo geïsoleerd netwerk toobe gebruikt voor de testfailover hebt gemaakt. Hallo gemakkelijkste manier toodo dit tooreplicate een domain controller en DNS-virtuele machine met Site Recovery is. Voer een testfailover van Hallo domain controller virtuele machine voordat u een testfailover van het herstelplan Hallo voor Hallo toepassing uitvoert. Hier ziet u hoe u dat doen:

1. [Repliceren](site-recovery-replicate-vmware-to-azure.md) Hallo domain controller en DNS-virtuele machine met Site Recovery.
1. Maak een geïsoleerd netwerk. Een virtueel netwerk in Azure gemaakt standaard is geïsoleerd van andere netwerken. Het is raadzaam dat Hallo IP-adresbereik voor dit netwerk hetzelfde als die van uw productienetwerk is. Geen site-naar-site-connectiviteit op dit netwerk inschakelen.
1. Geef een DNS IP-adres in Hallo netwerk gemaakt als Hallo IP-adres dat u Hallo DNS-virtuele machine tooget verwacht. Als u tooAzure repliceert, voor de virtuele machine die wordt gebruikt op failover in Hallo Hallo IP-adres geeft **IP-adres doel** instellen in **berekening en netwerk** instellingen. 

    ![Doel-IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **doel-IP**

    ![Azure testnetwerk](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS-server in Azure testnetwerk**

> [!TIP]
> Site Recovery probeert toocreate test-virtuele machines in een subnet met dezelfde naam en hetzelfde IP als die beschikbaar is in gebruik Hallo **berekening en netwerk** instellingen van Hallo virtuele machine. Als het subnet van dezelfde naam is niet beschikbaar in Hallo opgegeven voor de testfailover, virtuele Azure-netwerk en vervolgens de virtuele testmachine wordt gemaakt in het eerste subnet Hallo alfabetische volgorde. Als IP-adres Hallo doel deel van Hallo gekozen subnet uitmaakt, probeert Site Recovery toocreate Hallo test failover-virtuele machine met behulp van IP-adres Hallo-doel. Als het IP-adres Hallo-doel is geen onderdeel van de gekozen subnet hello, opgehaald vervolgens failover van de virtuele machine gemaakt met een beschikbare IP in Hallo gekozen subnet. 
>
>


1. Als u tooanother lokale site repliceert en u DHCP gebruikt, volgt u Hallo instructies te[DNS en DHCP instellen voor testfailover](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Een testfailover van Hallo domain controller virtuele machine worden uitgevoerd in een geïsoleerd netwerk Hallo doen. Gebruik meest recente beschikbare **toepassing consistente** herstelpunt van Hallo domain controller toodo Hallo testfailover van virtuele machine. 
1. Een testfailover voor Hallo herstelplan met virtuele machines van de toepassing hello uitvoeren. 
1. Nadat het testen is voltooid, **testfailover opschonen** op Hallo domain controller virtuele machine. Deze stap verwijdert Hallo-domeincontroller die is gemaakt voor de testfailover.


### <a name="removing-reference-tooother-domain-controllers"></a>Verwijderen van verwijzing tooother-domeincontrollers
Wanneer u een failovertest uitvoert, kunt u niet alle Hallo-domeincontrollers in Hallo testnetwerk brengt. Hallo-verwijzing tooremove van andere domeincontrollers die zijn opgenomen in uw productieomgeving, moet u mogelijk te[overnemen van FSMO-Active Directory-functies](http://aka.ms/ad_seize_fsmo) en [metagegevens opruimen](https://technet.microsoft.com/library/cc816907.aspx) voor domein ontbreekt domeincontrollers. 



> [!IMPORTANT]
> Enkele van Hallo configuraties beschreven in de volgende sectie Hallo zijn niet Hallo standard/domain controller standaardconfiguraties. Als u niet toomake wilt deze wijzigingen tooa productie-domeincontroller, dan hebt u maakt een domain controller toegewezen toobe gebruikt voor de Site Recovery-testfailover en deze toothat wijzigingen aanbrengen.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problemen vanwege veiligheidsmaatregelen voor virtualisatie 

Vanaf Windows Server 2012 [extra garanties al ingebouwd in Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Met deze beveiligingen te helpen beveiligen van gevirtualiseerde domeincontrollers tegen USN-terugdraaiacties door, zolang het onderliggende hypervisorplatform Hallo VM-GenerationID ondersteunt. Azure ondersteunt VM-GenerationID, wat betekent dat domeincontrollers met Windows Server 2012 of later op Azure virtual machines Hallo extra beveiliging. 


Wanneer Hallo generatie-id opnieuw wordt ingesteld, Hallo invocationID van Hallo AD DS-database ook opnieuw ingesteld, Hallo RID-groep is verwijderd en SYSVOL is gemarkeerd als niet-bindende. Zie voor meer informatie [inleiding tooActive virtualisatie Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) en [Safely Virtualizing DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Mislukte via tooAzure kan leiden tot het opnieuw instellen van de generatie-id en die weer bij Hallo extra beveiliging wanneer Hallo domain controller virtuele machine wordt opgestart in Azure. Dit kan leiden tot een **aanzienlijke vertraging** in gebruiker wordt kunnen toologin toohello domain controller virtuele machine. Aangezien deze domeincontroller kan alleen worden gebruikt in een testfailover, zijn er geen veiligheidsmaatregelen voor virtualisatie nodig. tooensure die de generatie-id voor Hallo domain controller virtuele machine niet wijzigen, wijzigt u Hallo-waarde van de volgende DWORD-too4 in Hallo lokale domeincontroller.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Symptomen van veiligheidsmaatregelen voor virtualisatie
 
Als de veiligheidsmaatregelen voor virtualisatie hebben gestart na een failovertest uitvoert, ziet u mogelijk een of meer van de volgende symptomen:  

Wijziging van generatie-ID

![Wijziging van generatie-ID](./media/site-recovery-active-directory/Event2170.png)

Wijziging van de aanroep-ID

![Wijziging van de aanroep-ID](./media/site-recovery-active-directory/Event1109.png)

SYSVOL en de Netlogon-shares zijn niet beschikbaar

![Sysvol-Share](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

Geen DFSR-databases zijn verwijderd

![DFSR-database verwijderen](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Enkele van Hallo configuraties beschreven in de volgende sectie Hallo zijn niet Hallo standard/domain controller standaardconfiguraties. Als u niet toomake wilt deze wijzigingen tooa productie-domeincontroller, dan hebt u maakt een domain controller toegewezen toobe gebruikt voor de Site Recovery-testfailover en deze toothat wijzigingen aanbrengen.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Domain controller problemen tijdens de testfailover


Voer Hallo opdracht toocheck te volgen of SYSVOL en NETLOGON mappen worden gedeeld op vanaf de opdrachtprompt:

    NET SHARE

Voer op Hallo opdrachtprompt Hallo na de opdracht tooensure die Hallo domeincontroller correct werkt.

    dcdiag /v > dcdiag.txt

In het logboek hello werkt zoeken naar de volgende tekst tooconfirm die domeincontroller Hallo goed. 

* 'doorgegeven test connectiviteit'
* 'doorgegeven test reclame'
* 'doorgegeven test MachineAccount'

Indien hello bovenstaande voorwaarden is voldaan, is het waarschijnlijk dat Hallo-domeincontroller goed werkt. Als dat niet het geval is, voer de volgende stappen.


* Een bindend terugzetten van de domeincontroller Hallo doen.
    * Hoewel het [niet aanbevolen toouse FRS-replicatie](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), maar als u nog steeds wordt gebruikt en Hallo stappen volgt [hier](https://support.microsoft.com/kb/290762) toodo bindend terugzetten. U vindt meer informatie over Burflags besproken in de vorige koppeling Hallo [hier](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Als u van DFSR replicatie gebruikmaakt, stappen Hallo beschikbaar [hier](https://support.microsoft.com/kb/2218556) toodo bindend terugzetten. U kunt ook Powershell-functies die beschikbaar zijn op deze [koppeling](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) voor dit doel. 
    
* Vereiste voor initiële synchronisatie omzeilen door in te stellen na Register sleutel too0 in Hallo lokale domeincontroller. Als deze DWORD niet bestaat, kunt klikt u vervolgens u dit maken onder het knooppunt 'Parameters'. U kunt meer lezen over deze [hier](https://support.microsoft.com/kb/2001093)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Hallo vereiste dat een globale catalogusserver beschikbaar toovalidate gebruikersaanmelding door in te stellen na Register sleutel too1 in Hallo lokale domeincontroller is uitgeschakeld. Als deze DWORD niet bestaat, kunt klikt u vervolgens u dit maken onder het knooppunt 'Lsa'. U kunt meer lezen over deze [hier](http://support.microsoft.com/kb/241789)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS- en de domeincontroller op verschillende computers
Als DNS niet op Hallo dezelfde virtuele machine als Hallo domeincontroller, moet u toocreate een VM DNS voor een testfailover Hallo. Als ze op Hallo van dezelfde virtuele machine, kunt u deze sectie overslaan.

U kunt een nieuwe DNS-server gebruiken en alle vereiste Hallo zones maken. Als uw Active Directory-domein contoso.com is, kunt u bijvoorbeeld een DNS-zone maken met de Hallo naam contoso.com. Hallo vermeldingen overeenkomt tooActive Directory moeten worden bijgewerkt in DNS, als volgt:

1. Zorg ervoor dat deze instellingen zijn voldaan voordat een andere virtuele machine in het herstelplan hello weergegeven wordt:
   
   * Hallo-zone moet de naam na hoofdnaam Hallo-forest.
   * Hallo-zone moet bestandsondersteuning.
   * Hallo-zone moet zijn ingeschakeld voor veilige en niet-beveiligde updates.
   * Hallo-omzetter van Hallo domain controller virtuele machine moet toohello IP-adres van Hallo DNS-virtuele machine te verwijzen.
2. Voer Hallo opdracht op domain controller virtuele machine te volgen:
   
    `nltest /dsregdns`
3. Een zone op Hallo DNS-server toevoegen en voeg een vermelding voor tooDNS niet-beveiligde updates toestaan:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Volgende stappen
Lees [welke workloads kan ik beveiligen?](site-recovery-workload.md) toolearn meer over het beveiligen van enterprise-werkbelastingen met Azure Site Recovery.

