---
title: aaaHow werkt Hyper-V-replicatie tooAzure in Azure Site Recovery? | Microsoft Docs
description: Dit artikel bevat een overzicht van onderdelen en -architectuur gebruikt bij het repliceren van lokale Hyper-V-machines tooAzure met hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 3b64156307f37764a8315dec68cf297acf279530
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work-in-site-recovery"></a>Hoe werkt tooAzure voor Hyper-V-replicatie in Site Recovery?


Dit artikel wordt beschreven Hallo-onderdelen en processen die betrokken zijn bij het repliceren van on-premises Hyper-V virtuele machines, met behulp van Hallo tooAzure [Azure Site Recovery](site-recovery-overview.md) service.

Met Site Recovery kunt u Hyper-V-VM's repliceren op Hyper-V-clusters en zelfstandige hosts die worden beheerd met of zonder System Center Virtual Machine Manager (VMM).

Eventuele opmerkingen posten onderin Hallo van dit artikel of in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Architectuuronderdelen

Er zijn een aantal onderdelen betrokken bij het repliceren van Hyper-V-machines tooAzure.

**Onderdeel** | **Locatie** | **Details**
--- | --- | ---
**Azure** | U hebt in Azure een Microsoft Azure-account, een Azure-opslagaccount en een Azure-netwerk nodig. | Gerepliceerde gegevens worden opgeslagen in Hallo storage-account en Azure VM's zijn gemaakt met Hallo gerepliceerde gegevens bij een storing van uw on-premises site.<br/><br/> Hallo virtuele Azure-machines verbinding toohello virtuele Azure-netwerk maken wanneer ze worden gemaakt.
**VMM-server** | Hyper-V-hosts bevinden zich in VMM-clouds | Als Hyper-V-hosts in VMM-clouds worden beheerd, kunt u Hallo VMM-server registreren in Hallo die Recovery Services-kluis.<br/><br/> Installeer op Hallo VMM-server Hallo Site Recovery Provider tooorchestrate replicatie met Azure.<br/><br/> U moet logische en VM-netwerken tooconfigure netwerktoewijzing instellen. Een VM-netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan het Hallo-cloud.
**Hyper-V-host** | Hyper-V-hosts en -clusters kunnen worden geïmplementeerd met of zonder de VMM-server. | Als er geen VMM-server, Hallo Hallo Site Recovery Provider is geïnstalleerd op Hallo host tooorchestrate replicatie met Site Recovery via internet. Als er een VMM-server, worden Hallo Provider is geïnstalleerd op deze en niet op Hallo host.<br/><br/> Hallo Recovery Services-agent is geïnstalleerd op Hallo host toohandle gegevensreplicatie.<br/><br/> Communicatie van zowel Hallo Provider en Hallo-agent is beveiligd en versleuteld. De gerepliceerde gegevens in de Azure-opslag zijn eveneens versleuteld.
**Virtuele Hyper-V-machines** | U hebt een of meer VM's nodig die worden uitgevoerd op een Hyper-V-hostserver. | Er is niets moet tooexplicitly geïnstalleerd op virtuele machines.

Meer informatie over de implementatievereisten Hallo en vereisten voor elk van deze onderdelen in Hallo [ondersteuningsmatrix](site-recovery-support-matrix-to-azure.md).

**Afbeelding 1: Hyper-V-sitereplicatie tooAzure**

![Onderdelen](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Afbeelding 2: Hyper-V in de VMM-clouds tooAzure replicatie**

![Onderdelen](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Replicatieproces

**Afbeelding 3: Replicatie up en herstel voor Hyper-V-replicatie tooAzure**

![werkstroom](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Beveiliging inschakelen

1. Nadat u de beveiliging voor een virtuele Hyper-V-machine hebt ingeschakeld in hello Azure-portal of on-premises, Hallo **beveiliging inschakelen** wordt gestart.
2. Hallo taak controleert die machine Hallo voldoet aan de vereisten, voordat Functieselectie wordt aangeroepen Hallo [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset van de replicatie met Hallo-instellingen die u hebt geconfigureerd.
3. Hallo taak initiële replicatie start met het aanroepen van Hallo [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) methode tooinitialize een volledige replicatie en verzenden Hallo van de virtuele machine virtuele schijven tooAzure.
4. U kunt bewaken Hallo taak in Hallo **taken** tabblad.      ![Takenlijst](media/site-recovery-hyper-v-azure-architecture/image1.png)![Inzoomen op beveiliging inschakelen](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Hallo initiële gegevens repliceren

1. Er wordt een [Hyper-V VM-momentopname](https://technet.microsoft.com/library/dd560637.aspx) gemaakt wanneer de initiële replicatie wordt geactiveerd.
2. Virtuele harde schijven zijn een voor een gerepliceerd tot ze alle gekopieerde tooAzure zijn. Het kan even duren, afhankelijk van Hallo VM-grootte en de netwerkbandbreedte. toooptimize uw netwerkgebruik Zie [hoe toomanage lokale tooAzure beveiliging netwerkbandbreedtegebruik](https://support.microsoft.com/kb/3056159).
3. Als er schijfwijzigingen optreden terwijl de eerste replicatie uitgevoerd wordt, Hallo Hyper-V Replica Replication Tracker deze wijzigingen worden bijgehouden als Hyper-V-Replicatielogboeken (.hrl). Deze bestanden bevinden zich in Hallo dezelfde map als het Hallo-schijven. Elke schijf heeft een hrl-bestand dat wordt verzonden toosecondary opslag.
4. Hallo schijfbronnnen momentopname- en logboekbestanden terwijl de eerste replicatie uitgevoerd wordt.
5. Wanneer Hallo initiële replicatie is voltooid, wordt de VM-momentopname Hallo verwijderd. Verschillen in logboek Hallo zijn gesynchroniseerd en samengevoegd toohello bovenliggende schijf.


### <a name="finalize-protection"></a>Beveiliging voltooien

1. Nadat de initiële replicatie Hallo is voltooid, hello **beveiliging op Hallo virtuele machine voltooien** taak configureert u netwerk- en andere instellingen na de replicatie zodat Hallo virtuele machine is beveiligd.
    ![Taak Beveiliging voltooien](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Als u tooAzure repliceert, moet u mogelijk tootweak Hallo-instellingen voor Hallo virtuele machine zodat deze gereed voor failover. U kunt een test failover toocheck die alles werkt zoals verwacht op dit moment kunt uitvoeren.

### <a name="replicate-hello-delta"></a>Hallo delta repliceren

1. Na de initiële replicatie hello Start de Deltasynchronisatie in overeenstemming met de replicatie-instellingen.
2. Hallo Hyper-V Replica Replication Tracker bijgehouden Hallo wijzigingen tooa virtuele hardeschijf als .hrl-bestanden. Elke schijf die voor replicatie is geconfigureerd, heeft een bijbehorend .hrl-bestand. Dit logboek wordt storage-account van de klant toohello verzonden nadat de initiële replicatie is voltooid. Wanneer een logboek in transit tooAzure, in een ander logboekbestand in Hallo Hallo wijzigingen in de primaire schijf Hallo worden bijgehouden dezelfde directory.
3. Tijdens de eerste en delta-replicatie, kunt u Hallo VM in Hallo VM weergave bewaken. [Meer informatie](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Replicatie synchroniseren

1. Als de replicatie van verschillen mislukt en een volledige replicatie veel bandbreedte of tijd zou kosten, wordt de virtuele machine gemarkeerd voor hersynchronisatie. Bijvoorbeeld, als Hallo .hrl bestanden 50% van de schijfgrootte hello bereiken, vervolgens hello VM gemarkeerd voor hersynchronisatie.
2.  Hersynchronisatie wordt geminimaliseerd Hallo en de hoeveelheid gegevens die zijn verzonden door controlesommen van Hallo bron- en virtuele machines en alleen Hallo delta-gegevens te verzenden. Hersynchronisatie maakt gebruik van een vaste-blokalgoritme voor verdelen in segmenten, waarbij bron- en doelbestanden in vaste segmenten worden verdeeld. Controlesommen voor elk segment worden gegenereerd en worden vervolgens vergeleken toodetermine die vanaf het Hallo-bron moet toobe toegepaste toohello doel wordt geblokkeerd.
3. Na hersynchronisatie moet de normale replicatie van verschillen worden hervat. Hersynchronisatie is standaard geplande toorun automatisch buiten kantooruren, maar u kunt een virtuele machine handmatig synchroniseren. U kunt de hersynchronisatie bijvoorbeeld hervatten als er een netwerkstoring of een andere storing optreedt. toodo deze, selecteer Hallo VM in de portal Hallo > **opnieuw synchroniseren**.

    ![Handmatig opnieuw synchroniseren](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retry-logic"></a>Logica voor opnieuw proberen

Als er een replicatiefout optreedt, wordt de replicatie automatisch opnieuw geprobeerd. Deze logica kan in twee categorieën worden ingedeeld:

**Categorie** | **Details**
--- | ---
**Niet-herstelbare fouten** | Er wordt geen nieuwe poging gedaan. De status van de virtuele machine is **Kritiek** en tussenkomst van de beheerder is vereist. Voorbeelden van deze fouten zijn: verbroken VHD keten; Ongeldige status voor Hallo replica-VM; Netwerk verificatiefouten: fouten autorisatie; Virtuele machine geen fouten gevonden (voor zelfstandige Hyper-V-servers)
**Herstelbare fouten** | Nieuwe pogingen uitgevoerd elke replicatie-interval, met behulp van een exponentiële back-uit die Hallo-interval voor opnieuw proberen van Hallo begin van de eerste poging Hallo door 1, 2, 4, 8 en 10 minuten verhoogt. Als een fout zich blijft voordoen, probeert u het om de 30 minuten opnieuw. Voorbeelden zijn onder meer: netwerkfouten; fouten in verband met weinig schijfruimte; weinig geheugenruimte |



## <a name="failover-and-failback-process"></a>Failover- en failbackproces

1. U kunt uitvoeren als een geplande of niet-geplande [failover](site-recovery-failover.md) van lokale Hyper-V-machines tooAzure. Als u een geplande failover uitvoert, wordt de Bronmachines tooensure worden afgesloten zonder verlies van gegevens.
2. U kunt één machine failover of maken [herstelplannen](site-recovery-create-recovery-plans.md) tooorchestrate failover van meerdere machines.
4. Nadat u Hallo failover uitvoert, moet u kunnen toosee Hallo replica virtuele machines in Azure gemaakt. U kunt een openbare IP-adres toohello VM indien nodig.
5. U doorvoert vervolgens Hallo failover toostart Hallo werkbelasting vanuit Hallo replica virtuele machine van Azure te openen.
6. Als uw primaire on-premises site weer beschikbaar is, kunt u een [failback](site-recovery-failback-from-azure-to-hyper-v.md) uitvoeren. U ere van een geplande failover van Azure toohello primaire site. Voor een geplande failover, u kunt wijzigingen selecteren toofailback toohello dezelfde virtuele machine of tooan alternatieve locatie en synchroniseren tussen Azure en lokale, tooensure zonder verlies van gegevens. Wanneer virtuele machines worden gemaakt van lokale, doorvoeren Hallo failover.




## <a name="next-steps"></a>Volgende stappen

Bekijk Hallo [ondersteuningsmatrix](site-recovery-support-matrix-to-azure.md)
