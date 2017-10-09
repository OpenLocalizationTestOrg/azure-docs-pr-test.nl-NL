---
title: aaaTest failover tooAzure in Site Recovery | Microsoft Docs
description: Informatie over het uitvoeren van een testfailover van lokale tooAzure
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
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Testen van failover-tooAzure in Site Recovery



In dit artikel bevat informatie en instructies voor het uitvoeren van een testfailover of een details voor Dr van virtuele machines en fysieke servers die zijn beveiligd met Site Recovery met behulp van Azure als Hallo herstelsite.

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Testfailover wordt uw replicatiestrategie voor van toovalidate uitvoeren of een detailanalyse van het herstel na noodgevallen zonder verlies van gegevens of uitvaltijd. Tijdens het doorzoeken van een testfailover heeft geen invloed op Hallo lopende replicatie of op uw productieomgeving. Testfailover kan worden gedaan op een virtuele machine of een [herstelplan](site-recovery-create-recovery-plans.md). Bij activering van een failovertest uitvoert, moet u toospecify hello toowhich Netwerktest virtuele machines verbinding wordt gemaakt. Zodra een testfailover wordt geactiveerd, kunt u de voortgang in Hallo bijhouden **taken** pagina.  


## <a name="supported-scenarios"></a>Ondersteunde scenario 's
Testfailover wordt ondersteund in alle implementatiescenario's anders dan [verouderde VMware site tooAzure](site-recovery-vmware-to-azure-classic-legacy.md). Testfailover wordt ook niet ondersteund wanneer de failover van virtuele machine uitgevoerd tooAzure.  


## <a name="run-a-test-failover"></a>Een testfailover uitvoeren
Deze procedure wordt beschreven hoe toorun een testfailover voor een herstel van plan bent. U kunt ook testfailover voor één machine ook uitvoeren met behulp van de juiste optie Hallo erop.

![Failover testen](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Selecteer **herstelplannen** > *recoveryplan_name*. Klik op **Testfailover**.
1. Selecteer een **herstelpunt** toofailover aan. U kunt een Hallo volgende opties gebruiken:
    1.  **Meest recente verwerkte**: deze optie is overgenomen van alle virtuele machines van Hallo recovery plan toohello meest recente herstelpunt dat al is verwerkt door Site Recovery-service. Wanneer u een testfailover uitgevoerd van een virtuele machine uitvoert, wordt ook de tijdstempel van Hallo meest recente verwerkte-herstelpunt weergegeven. Als u failover van een herstelplan doet, kunt u Ga tooindividual virtuele machine en bekijk **herstelpunten van de meest recente** tegel tooget deze informatie. Als u geen tijd is besteed tooprocess Hallo onbewerkte gegevens, deze optie biedt een laag RTO (beoogde hersteltijd) failover-optie.
    1.  **Meest recente app-consistente**: deze optie is overgenomen van alle virtuele machines van Hallo recovery plan toohello nieuwste toepassing consistente herstelpunten die al is verwerkt door Site Recovery-service. Wanneer u een testfailover uitgevoerd van een virtuele machine uitvoert, wordt ook de tijdstempel van Hallo laatste app-consistente-herstelpunt weergegeven. Als u failover van een herstelplan doet, kunt u Ga tooindividual virtuele machine en bekijk **herstelpunten van de meest recente** tegel tooget deze informatie.
    1.  **Meest recente**: deze optie eerst alle Hallo-gegevens dat verzonden tooSite Recovery service toocreate een herstelpunt voor elke virtuele machine is voordat de failover tooit verwerkt. Deze optie biedt Hallo laagste RPO (beoogd herstelpunt) als Hallo virtuele machine gemaakt nadat de failover alle Hallo gegevens hebt die is gerepliceerd tooSite herstelservice Hallo failover is geactiveerd.
    1.  **Meest recente multi-VM verwerkt**: deze optie is alleen beschikbaar voor herstelplannen die ten minste één virtuele machine met de consistentie tussen meerdere VM's op. Virtuele machines die deel van een replicatie groep failover toohello laatste algemene multi-VM consistent herstelpunt uitmaken verwijzen. Andere virtuele machines failover tootheir meest recente verwerkte herstelpunt.  
    1.  **Meest recente multi-VM-app-consistente**: deze optie is alleen beschikbaar voor herstelplannen die ten minste één virtuele machine met meerdere VM consistentie ON hebben. Virtuele machines die deel van een replicatie uitmaken groeperen failover toohello meest recente algemene multi-VM toepassingsconsistente herstelpunt. Andere virtuele machines failover tootheir nieuwste toepassingsconsistente herstelpunt. 
    1.  **Aangepaste**: als u een testfailover uitgevoerd van een virtuele machine uitvoert, dan kunt u deze optie toofailover tooa bepaald herstelpunt.
1. Selecteer een **virtuele Azure-netwerk**: Geef een Azure-netwerk waar Hallo test-virtuele machines moet worden gemaakt. Site Recovery probeert toocreate test-virtuele machines in een subnet met dezelfde naam en hetzelfde IP als die beschikbaar is in gebruik Hallo **berekening en netwerk** instellingen van Hallo virtuele machine. Als het subnet van dezelfde naam is niet beschikbaar in Hallo opgegeven voor de testfailover, virtuele Azure-netwerk en vervolgens de virtuele testmachine wordt gemaakt in het eerste subnet Hallo alfabetische volgorde. Als u dezelfde IP is niet beschikbaar op subnet hello, haalt virtuele machine een ander IP-adres beschikbaar op Hallo subnet. Lees dit gedeelte voor [meer informatie](#creating-a-network-for-test-failover)
1. Als u bent tooAzure failover en gegevensversleuteling is ingeschakeld, in **versleutelingssleutel** Selecteer Hallo-certificaat dat was uitgegeven wanneer u de versleuteling van gegevens tijdens de installatie van de Provider is ingeschakeld. Als u versleuteling op Hallo virtuele machine niet hebt ingeschakeld, kunt u deze stap overslaan.
1. Voortgang van de failover volgen op Hallo **taken** tabblad. U moet kunnen toosee Hallo test replica-machine in hello Azure-portal.
1. tooinitiate een RDP-verbinding op Hallo virtuele machine, moet u te[toevoegen van een openbaar IP-adres](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) op Hallo netwerkinterface Hallo via de virtuele machine is mislukt. Als u tooa klassieke virtuele machine mislukken, moet u te[een eindpunt toevoegen](../virtual-machines/windows/classic/setup-endpoints.md) op poort 3389
1. Wanneer u bent klaar, klikt u op **testfailover opschonen** op Hallo herstelplan. In **notities** opnemen en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo opslaan. Hiermee verwijdert u Hallo virtuele machines die zijn gemaakt tijdens de testfailover.


> [!TIP]
> Site Recovery probeert toocreate test-virtuele machines in een subnet met dezelfde naam en hetzelfde IP als die beschikbaar is in gebruik Hallo **berekening en netwerk** instellingen van Hallo virtuele machine. Als het subnet van dezelfde naam is niet beschikbaar in Hallo opgegeven voor de testfailover, virtuele Azure-netwerk en vervolgens de virtuele testmachine wordt gemaakt in het eerste subnet Hallo alfabetische volgorde. Als IP-adres Hallo doel deel van Hallo gekozen subnet uitmaakt, probeert siteherstel toocreate Hallo test failover-virtuele machine met behulp van IP-adres Hallo-doel. Als het IP-adres Hallo-doel is geen onderdeel van subnet gekozen Hallo opgehaald vervolgens failover van de virtuele machine gemaakt met een beschikbare IP in Hallo gekozen subnet.
>
>

## <a name="test-failover-job"></a>Een testtaak voor failover

![Failover testen](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Wanneer een testfailover wordt geactiveerd, omvat het volgende stappen uit:

1. Controle van vereisten: deze stap zorgt ervoor dat alle voorwaarden die vereist is voor failover wordt voldaan
1. Failover: Deze stap Hallo gegevens verwerkt en maakt het klaar is zodat Azure een virtuele machine buiten deze kunnen worden gemaakt. Als u hebt gekozen **nieuwste** herstelpunt, deze stap maakt een herstelpunt van Hallo-gegevens die toohello-service is verzonden.
1. Start: Deze stap maakt u een virtuele machine van Azure met behulp van Hallo-gegevens in de vorige stap Hallo verwerkt.

## <a name="time-taken-for-failover"></a>Gebruikte tijd voor failover

Failover van virtuele machines vereist in bepaalde gevallen, een extra tussenstap die duurt normaal ongeveer 8 too10 minuten toocomplete gesproken. Deze gevallen zijn als volgende:

* Met een versie van de Mobility-service die ouder zijn dan 9,8 Hallo virtuele VMware-machines
* Fysieke servers
* Virtuele VMware-Linux-machines
* Hyper-V virtuele machines die beveiligd als de fysieke servers
* Waar volgende stuurprogramma's niet aanwezig als opstartstuurprogramma zijn virtuele VMware-machines
    * storvsc
    * VMBus
    * storflt
    * Intelide
    * ATAPI
* Virtuele VMware-machines waarvoor geen DHCP-service is ingeschakeld ongeacht of ze zijn geïnstalleerd via DHCP of statische IP-adressen

In alle Hallo andere gevallen deze tussenstap is niet vereist en Hallo tijd voor het Hallo-failover zijn aanzienlijk minder.


## <a name="creating-a-network-for-test-failover"></a>Maken van een netwerk voor testfailover
Het verdient aanbeveling dat als u een testfailover doet u een netwerk dat is geïsoleerd van het herstel site productienetwerk die u hebt opgegeven in **berekening en netwerk** instellingen voor Hallo virtuele machine. Standaard bij het maken van een Azure-netwerk is geïsoleerd van andere netwerken. Dit netwerk moet uw productienetwerk nabootsen:

1. Testnetwerk moet hetzelfde aantal subnetten als die in uw productienetwerk en met dezelfde naam als die van Hallo subnetten in het productienetwerk Hallo hebben.
1. Gebruik testnetwerk Hallo hetzelfde IP-adresbereik als die van uw productienetwerk.
1. Update Hallo DNS Hallo testnetwerk zoals Hallo IP die u hebt opgegeven als doel-IP voor Hallo DNS-virtuele machine onder **berekening en netwerk** instellingen. Doorloop [testfailover-overwegingen voor active directory](site-recovery-active-directory.md#test-failover-considerations) sectie voor meer informatie.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Testen van failover tooa productienetwerk op de site recovery
Het verdient aanbeveling dat als u een testfailover doet u een netwerk dat verschilt van het herstel site productienetwerk die u hebt opgegeven in **berekening en netwerk** instellingen voor Hallo virtuele machine. Maar als u toch toovalidate end tooend netwerkverbinding een failover via de virtuele machine, houd er rekening mee Hallo volgende punten:

1. Zorg ervoor dat Hallo de primaire virtuele machine wordt afgesloten wanneer u Hallo testfailover uitvoert. Als u doet dit, zullen er twee virtuele machines met Hallo dezelfde identiteit uitgevoerd in de Hallo netwerk op Hallo hetzelfde moment en die tooundesired gevolgen kan leiden.
1. Alle wijzigingen die u in Hallo test failover virtuele machines aanbrengt zou gaat verloren wanneer u opschonen Hallo test failover-virtuele machines. Deze wijzigingen worden niet-gerepliceerde back toohello primaire virtuele machine.
1. Deze werkwijze testen leidt tooa uitvaltijd van uw productietoepassing. Gebruikers van de toepassing hello moeten worden gevraagd toonot gebruik Hallo toepassing hello DR inzoomen wordt uitgevoerd.  



## <a name="prepare-active-directory-and-dns"></a>Active Directory en DNS voorbereiden
toorun een testfailover voor de toepassing testen, moet u een kopie van de Active Directory productieomgeving Hallo in uw testomgeving. Doorloop [testfailover-overwegingen voor active directory](site-recovery-active-directory.md#test-failover-considerations) sectie voor meer informatie.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Het voorbereiden van de tooconnect tooAzure VM's na een failover

Als u wilt dat tooconnect tooAzure virtuele machines met RDP na een failover, Controleer of u acties samengevat in de tabel Hallo Hallo.

**Failover** | **Locatie** | **Acties**
--- | --- | ---
**Azure VM waarop Windows wordt uitgevoerd** | Op on-premises machine vóór de failover | tooaccess hello Azure VM via internet hello, schakelt u RDP in, zorg ervoor dat TCP en UDP-regels worden toegevoegd voor Hallo **openbare**, en dat is toegestaan RDP **Windows Firewall** > **toegestaan Apps**, voor alle profielen.<br/><br/> tooaccess via een site-naar-site-verbinding, schakelt u RDP in op de machine Hallo en zorg ervoor dat RDP in Hallo is toegestaan **Windows Firewall** -> **toegestane apps en functies** voor  **Domein- en persoonlijke** netwerken.<br/><br/>  Zorg dat SAN-beleid Hallo van het besturingssysteem is ingesteld, te**OnlineAll**. [Meer informatie](https://support.microsoft.com/kb/3031135).<br/><br/> Zorg ervoor dat er zijn geen Windows-updates in behandeling op Hallo virtuele machine wanneer u een failover activeren. Windows update kan worden gestart wanneer u failover en u zich niet kunnen toologin toohello virtuele machine totdat het Hallo-update is voltooid. <br/><br/>
**Azure VM waarop Windows wordt uitgevoerd** | Op de virtuele machine na een failover van Azure | Voor een klassieke virtuele machine, [toevoegen van een openbaar eindpunt](../virtual-machines/windows/classic/setup-endpoints.md) voor Hallo RDP-protocol (poort 3389)<br/><br/>  Voor een virtuele machine van het Resource Manager [toevoegen van een openbaar IP-adres](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) erop.<br/><br/> netwerkbeveiligingsgroepen op VM failover Hallo Hallo en hello Azure-subnet toowhich is verbonden, moet tooallow binnenkomende verbindingen toohello RDP-poort.<br/><br/> Voor een virtuele machine van het Resource Manager kunt u controleren **opstarten diagnostics** toolook op een schermopname van Hallo virtuele machine<br/><br/> Als u geen verbinding kunt maken die Hallo VM wordt uitgevoerd, controleren en zoek vervolgens naar deze [tips voor probleemoplossing](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**Azure VM waarop Linux wordt uitgevoerd** | Op on-premises machine vóór de failover | Zorg ervoor dat Hallo Secure Shell-service op Azure VM Hallo toostart automatisch ingesteld op opstarten van het systeem.<br/><br/> Controleer dat de firewallregels voor een SSH-verbinding tooit toestaan.
**Azure VM waarop Linux wordt uitgevoerd** | Azure virtuele machine na een failover | netwerkbeveiligingsgroepen op VM failover Hallo Hallo en hello Azure-subnet toowhich is verbonden, moet tooallow binnenkomende verbindingen toohello SSH-poort.<br/><br/> Voor een klassieke virtuele machine, [toevoegen van een openbaar eindpunt](../virtual-machines/windows/classic/setup-endpoints.md) moeten worden gemaakt, tooallow binnenkomende verbindingen op Hallo SSH-poort (standaard TCP-poort 22).<br/><br/> Voor een virtuele machine van het Resource Manager [toevoegen van een openbaar IP-adres](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) erop.<br/><br/> Voor een virtuele machine van het Resource Manager kunt u controleren **opstarten diagnostics** toolook op een schermopname van Hallo virtuele machine<br/><br/>



## <a name="next-steps"></a>Volgende stappen
Zodra u een testfailover met succes hebt geprobeerd kunt u doen proberen een [failover](site-recovery-failover.md).
