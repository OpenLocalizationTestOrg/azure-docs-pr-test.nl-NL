---
title: aaaFailover in Site Recovery | Microsoft Docs
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
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Failover in Site Recovery
Dit artikel wordt beschreven hoe toofailover virtuele machines en fysieke servers beveiligd door Site Recovery.

## <a name="prerequisites"></a>Vereisten
1. Voordat u een failover doet, voert u een [testfailover](site-recovery-test-failover-to-azure.md) tooensure dat alles werkt zoals verwacht.
1. [Bereid Hallo netwerk](site-recovery-network-design.md) op doellocatie voordat u een failover.  


## <a name="run-a-failover"></a>Een failover uitvoeren
Deze procedure wordt beschreven hoe toorun een failover voor een [herstelplan](site-recovery-create-recovery-plans.md). U kunt ook Hallo failover voor een enkele virtuele machine of fysieke server uitvoeren van Hallo **gerepliceerde items** pagina


![Failover](./media/site-recovery-failover/Failover.png)

1. Selecteer **herstelplannen** > *recoveryplan_name*. Klik op **Failover**
2. Op Hallo **Failover** Schakel in het scherm een **herstelpunt** toofailover aan. U kunt een Hallo volgende opties gebruiken:
    1.  **Meest recente** (standaard): deze optie eerst alle Hallo-gegevens dat verzonden tooSite Recovery service toocreate een herstelpunt voor elke virtuele machine is voordat de failover tooit verwerkt. Deze optie biedt Hallo laagste RPO (beoogd herstelpunt) als Hallo virtuele machine gemaakt nadat de failover alle Hallo gegevens heeft die is gerepliceerd tooSite herstelservice Hallo failover is geactiveerd.
    1.  **Meest recente verwerkte**: deze optie is overgenomen van alle virtuele machines van Hallo recovery plan toohello meest recente herstelpunt dat al is verwerkt door Site Recovery-service. Wanneer u een testfailover uitgevoerd van een virtuele machine uitvoert, wordt ook de tijdstempel van Hallo meest recente verwerkte-herstelpunt weergegeven. Als u failover van een herstelplan doet, kunt u Ga tooindividual virtuele machine en bekijk **herstelpunten van de meest recente** tegel tooget deze informatie. Als u geen tijd is besteed tooprocess Hallo onbewerkte gegevens, deze optie biedt een laag RTO (beoogde hersteltijd) failover-optie.
    1.  **Meest recente app-consistente**: deze optie is overgenomen van alle virtuele machines van Hallo recovery plan toohello nieuwste toepassing consistente herstelpunten die al is verwerkt door Site Recovery-service. Wanneer u een testfailover uitgevoerd van een virtuele machine uitvoert, wordt ook de tijdstempel van Hallo laatste app-consistente-herstelpunt weergegeven. Als u failover van een herstelplan doet, kunt u Ga tooindividual virtuele machine en bekijk **herstelpunten van de meest recente** tegel tooget deze informatie.
    1.  **Meest recente multi-VM verwerkt**: deze optie is alleen beschikbaar voor herstelplannen die ten minste één virtuele machine met de consistentie tussen meerdere VM's op. Virtuele machines die deel van een replicatie groep failover toohello laatste algemene multi-VM consistent herstelpunt uitmaken verwijzen. Andere virtuele machines failover tootheir meest recente verwerkte herstelpunt.  
    1.  **Meest recente multi-VM-app-consistente**: deze optie is alleen beschikbaar voor herstelplannen die ten minste één virtuele machine met meerdere VM consistentie ON hebben. Virtuele machines die deel van een replicatie uitmaken groeperen failover toohello meest recente algemene multi-VM toepassingsconsistente herstelpunt. Andere virtuele machines failover tootheir nieuwste toepassingsconsistente herstelpunt.
    1.  **Aangepaste**: als u een testfailover uitgevoerd van een virtuele machine uitvoert, dan kunt u deze optie toofailover tooa bepaald herstelpunt.

    > [!NOTE]
    > Hallo optie toochoose een herstelpunt is alleen beschikbaar wanneer u via tooAzure mislukken.
    >
    >


1. Als sommige Hallo virtuele machines in het herstelplan Hallo zijn failover in een eerder uitgevoerde en nu Hallo virtuele machines actief op de locatie van de bron- en doelserver zijn, kunt u **richting wijzigen** optie toodecide Hallo richting in welke Hallo failover moet gebeuren.
1. Als u bent tooAzure failover en gegevensversleuteling is ingeschakeld voor Hallo cloud (geldt alleen wanneer u Hyper-v virtuele machines van een VMM-Server hebt beveiligd), in **versleutelingssleutel** Selecteer Hallo-certificaat dat was uitgegeven wanneer u versleuteling van gegevens tijdens de installatie op Hallo VMM-server ingeschakeld.
1. Selecteer **machine afsluiten voordat u begint met failover** als u wilt dat Site Recovery tooattempt toodo afsluiten van de virtuele bronmachines voordat Hallo failover. Failover wordt voortgezet zelfs als afsluiten is mislukt.  

    > [!NOTE]
    > In geval van een Hyper-v virtuele machines probeert deze optie ook toosynchronize Hallo on-premises gegevens is nog niet is verzonden toohello service voordat Hallo failover.
    >
    >

1. U kunt Hallo failover voortgang volgen op Hallo **taken** pagina. Zelfs als er fouten optreden tijdens een niet-geplande failover Hallo herstelplan wordt uitgevoerd totdat deze voltooid is.
1. Na een failover Hallo logboekregistratie in tooit valideren Hallo virtuele machine. Als u toogo een ander herstelpunt voor Hallo virtuele machine wilt, dan kunt u **herstelpunt wijzigen** optie.
1. Wanneer u tevreden met de virtuele machine failover hello bent, kunt u **doorvoeren** Hallo failover. Hiermee verwijdert u alle Hallo herstelpunten beschikbaar met Hallo-service en **herstelpunt wijzigen** optie niet langer beschikbaar.

## <a name="planned-failover"></a>Geplande failover
Naast de Failover, Hyper-V virtuele machines die beveiligd met Site Recovery ook ondersteuning **geplande failover**. Dit is een nul gegevens verloren gaan failover-optie. Wanneer een geplande failover wordt geactiveerd, Hallo eerst bron virtuele machines worden afgesloten, Hallo gegevens nog toobe gesynchroniseerd is gesynchroniseerd en vervolgens een failover wordt geactiveerd.

> [!NOTE]
> Wanneer u een failover-Hyper-v virtuele machines van een lokale site tooanother lokale site, toocome back toohello primaire lokale site hebt u toofirst **omgekeerd repliceren** Hallo virtuele machine back tooprimary site en vervolgens activeert u een failover. Hallo primaire virtuele machine is niet beschikbaar als, voordat start het programma te**omgekeerd repliceren** u toorestore Hallo virtuele machine vanaf een back-up hebt.   
>
>

## <a name="failover-job"></a>Failover-taak

![Failover](./media/site-recovery-failover/FailoverJob.png)

Wanneer een failover wordt geactiveerd, omvat het volgende stappen uit:

1. Controle van vereisten: deze stap zorgt ervoor dat alle voorwaarden die vereist is voor failover wordt voldaan
1. Failover: Deze stap Hallo gegevens verwerkt en maakt het klaar is zodat Azure een virtuele machine buiten deze kunnen worden gemaakt. Als u hebt gekozen **nieuwste** herstelpunt, deze stap maakt een herstelpunt van Hallo-gegevens die toohello-service is verzonden.
1. Start: Deze stap maakt u een virtuele machine van Azure met behulp van Hallo-gegevens in de vorige stap Hallo verwerkt.

> [!WARNING]
> **Een onderhanden niet annuleren failover**: voordat failover wordt gestart, replicatie voor Hallo virtuele machine is gestopt. Als u **annuleren** een taak uitgevoerd, stopt de failover, maar Hallo virtuele machine kan niet worden gestart tooreplicate. Replicatie kan niet opnieuw worden gestart.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Gebruikte tijd voor failover-tooAzure

Failover van virtuele machines vereist in bepaalde gevallen, een extra tussenstap die duurt normaal ongeveer 8 too10 minuten toocomplete gesproken. Deze gevallen zijn als volgende:

* Met behulp van de mobility-service van de versie die ouder zijn dan 9,8 virtuele VMware-machines
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





## <a name="using-scripts-in-failover"></a>Met behulp van scripts in Failover
U kunt tooautomate bepaalde acties tijdens het uitvoeren van een failover. U kunt scripts gebruiken of [Azure automation-runbooks](site-recovery-runbook-automation.md) in [herstelplannen](site-recovery-create-recovery-plans.md) toodo die.

## <a name="other-considerations"></a>Andere overwegingen
* **Stationsletter** : tooretain Hallo stationsletter op virtuele machines na een failover kunt u instellen Hallo **SAN-beleid** voor Hallo virtuele machine te**OnlineAll**. [Lees meer](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Volgende stappen
Als u failover uitgevoerd voor virtuele machines en Hallo on-premises Datacenter beschikbaar is, moet u [ **opnieuw beveiligen** ](site-recovery-how-to-reprotect.md) virtuele VMware-machines back toohello on-premises Datacenter.

Gebruik [ **geplande failover** ](site-recovery-failback-from-azure-to-hyper-v.md) te optie**Failback** back tooon-premises-Hyper-v virtuele machines van Azure.

Als u is mislukt via een Hyper-v virtuele machine tooanother on-premises gegevens center worden beheerd door een VMM-server en Hallo primaire Datacenter beschikbaar is, gebruik vervolgens **omgekeerde repliceren** optie toostart Hallo replicatie back toohello primaire Datacenter.
