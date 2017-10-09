---
title: aaaHow werkt Hyper-V-replicatie tooAzure in Site Recovery? | Microsoft Docs
description: Dit artikel geeft een overzicht van de werking van Hyper-V-replicatie in Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Hoe werkt de Hyper-V-replicatie tooAzure?

Lees dit artikel toounderstand Hallo architectuur en werkstromen voor Hyper-V-replicatie tooAzure Hallo met [Azure Site Recovery](site-recovery-overview.md) service.

Eventuele opmerkingen posten onderin Hallo van dit artikel of in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

U kunt repliceren Hallo tooAzure te volgen:
- **Hyper-V met VMM**: VM's op on-premises Hyper-V-hosts die in System Center Virtual Machine Manager-clouds (VMM) worden beheerd. Hosts kunnen worden uitgevoerd op elk [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). U kunt virtuele Hyper-V-machines repliceren waarop gastbesturingssystemen worden uitgevoerd die [worden ondersteund door Hyper-V en Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).
- **Hyper-V zonder VMM**: on-premises VM's op Hyper-V-hosts die niet worden beheerd in VMM-clouds. Hosts kunnen uitvoeren op een van de Hallo [ondersteunde besturingssystemen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). U kunt virtuele Hyper-V-machines repliceren waarop gastbesturingssystemen worden uitgevoerd die [worden ondersteund door Hyper-V en Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="architectural-components"></a>Architectuuronderdelen

**Onderwerp** | **Onderdeel** | **Details**
--- | --- | ---
**Azure** | U hebt in Azure een Microsoft Azure-account, een Azure-opslagaccount en een Azure-netwerk nodig. | Opslag en netwerk kunnen Resource Manager-gebaseerd of klassieke accounts zijn.<br/><br/> Gerepliceerde gegevens worden opgeslagen in Hallo storage-account en Azure VM's zijn gemaakt met Hallo gerepliceerde gegevens bij een storing van uw on-premises site.<br/><br/> Hallo virtuele Azure-machines verbinding toohello virtuele Azure-netwerk maken wanneer ze worden gemaakt.
**VMM-server** | Hyper-V-hosts die zich in VMM-clouds bevinden | Als Hyper-V-hosts in VMM-clouds worden beheerd, kunt u Hallo VMM-server registreren in Hallo die Recovery Services-kluis.<br/><br/> Installeer op Hallo VMM-server Hallo Site Recovery Provider tooorchestrate replicatie met Azure.<br/><br/> U moet logische en VM-netwerken tooconfigure netwerktoewijzing instellen. Een VM-netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan het Hallo-cloud.
**Hyper-V-host** | Hyper-V-servers kunnen worden geïmplementeerd met of zonder de VMM-server. | Als er geen VMM-server, Hallo Hallo Site Recovery Provider is geïnstalleerd op Hallo host tooorchestrate replicatie met Site Recovery via internet. Als er een VMM-server, worden Hallo Provider is geïnstalleerd op deze en niet op Hallo host.<br/><br/> Hallo Recovery Services-agent is geïnstalleerd op Hallo host toohandle gegevensreplicatie.<br/><br/> Communicatie van zowel Hallo Provider en Hallo-agent is beveiligd en versleuteld. De gerepliceerde gegevens in de Azure-opslag zijn eveneens versleuteld.
**Virtuele Hyper-V-machines** | U moet een of meer virtuele machines op Hallo Hyper-V-hostserver. | Hoeft u niets tooexplicitly geïnstalleerd op virtuele machines

## <a name="deployment-steps"></a>Implementatiestappen

1. **Azure**: U hebt ingesteld hello Azure onderdelen. Wij raden u aan om opslag- en netwerkaccounts in te stellen voordat u begint met de Site Recovery-implementatie.
2. **Kluis**: u maakt een Recovery Services-kluis voor Site Recovery en configureert de kluisinstellingen, met inbegrip van het configureren van de bron- en doelinstellingen, het instellen van een replicatiebeleid en het inschakelen van replicatie.
3. **Bron en doel**:
    - **Hyper-V-hosts in VMM-clouds**: als onderdeel van het opgeven van instellingen van de bronserver u downloaden en installeren van hello Azure Site Recovery Provider op Hallo VMM-server en hello Azure Recovery Services-agent op elke Hyper-V-host. Hallo bron wordt Hallo VMM-server zijn. Hallo-doel is Azure.
    - Hyper-V-hosts zonder VMM: wanneer u de instellingen van de bronserver opgeeft, u en downloaden en installeren Hallo Provider-agent op elke Hyper-V-host. Hallo hosts verzamelen in een Hyper-V-site tijdens de implementatie en geef op deze site als Hallo bron. Hallo-doel is Azure.

    ![Replicatie van Hyper-V of VMM tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![Hyper-V-site-replicatie tooAzure](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Beleid voor wachtwoordreplicatie**: maken van een beleid voor wachtwoordreplicatie voor Hallo Hyper-V-site of de VMM-cloud. Hallo-beleid is toegepast tooall virtuele machines op hosts in het Hallo-site of in de cloud bevinden.
5. **Replicatie inschakelen**: u schakelt replicatie voor virtuele Hyper-V-machines in. Initiële replicatie vindt plaats in overeenstemming met beleidsinstellingen Hallo-replicatie. Gegevenswijzigingen worden bijgehouden en replicatie van verschillen wijzigingen tooAzure wordt gestart nadat de Hallo initiële replicatie is voltooid. Bijgehouden wijzigingen voor een item worden opgeslagen in een .hrl-bestand.
6. **Failover testen**: uitvoeren van een test failover toomake, controleren of alles werkt zoals verwacht.

Meer informatie over implementatie:
- [Aan de slag met Hyper-V VM replicatie tooAzure - met VMM](site-recovery-vmm-to-azure.md)
- [Aan de slag met Hyper-V VM replicatie tooAzure - zonder VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Werkstroom van de Hyper-V-replicatie

### <a name="enable-protection"></a>Beveiliging inschakelen

1. Nadat u de beveiliging voor een virtuele Hyper-V-machine hebt ingeschakeld in hello Azure-portal of on-premises, Hallo **beveiliging inschakelen** wordt gestart.
2. Hallo taak controleert die machine Hallo voldoet aan de vereisten, voordat Functieselectie wordt aangeroepen Hallo [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset van de replicatie met Hallo-instellingen die u hebt geconfigureerd.
3. Hallo taak initiële replicatie start met het aanroepen van Hallo [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) methode tooinitialize een volledige replicatie en verzenden Hallo van de virtuele machine virtuele schijven tooAzure.
4. U kunt bewaken Hallo taak in Hallo **taken** tabblad.      ![Takenlijst](media/site-recovery-hyper-v-azure-architecture/image1.png)![Inzoomen op beveiliging inschakelen](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>Initiële replicatie

1. Er wordt een [Hyper-V VM-momentopname](https://technet.microsoft.com/library/dd560637.aspx) gemaakt wanneer de initiële replicatie wordt geactiveerd.
2. Virtuele harde schijven zijn een voor een gerepliceerd tot ze alle gekopieerde tooAzure zijn. Het kan even duren, afhankelijk van Hallo VM-grootte en de netwerkbandbreedte. toooptimize uw netwerkgebruik Zie [hoe toomanage lokale tooAzure beveiliging netwerkbandbreedtegebruik](https://support.microsoft.com/kb/3056159).
3. Als er schijfwijzigingen optreden terwijl de eerste replicatie uitgevoerd wordt, Hallo Hyper-V Replica Replication Tracker deze wijzigingen worden bijgehouden als Hyper-V-Replicatielogboeken (.hrl). Deze bestanden bevinden zich in Hallo dezelfde map als het Hallo-schijven. Elke schijf heeft een hrl-bestand dat wordt verzonden toosecondary opslag.
4. Hallo schijfbronnnen momentopname- en logboekbestanden terwijl de eerste replicatie uitgevoerd wordt.
5. Wanneer Hallo initiële replicatie is voltooid, wordt de VM-momentopname Hallo verwijderd. Verschillen in logboek Hallo zijn gesynchroniseerd en samengevoegd toohello bovenliggende schijf.


### <a name="finalize-protection"></a>Beveiliging voltooien

1. Nadat de initiële replicatie Hallo is voltooid, hello **beveiliging op Hallo virtuele machine voltooien** taak configureert u netwerk- en andere instellingen na de replicatie zodat Hallo virtuele machine is beveiligd.
    ![Taak Beveiliging voltooien](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Als u tooAzure repliceert, moet u mogelijk tootweak Hallo-instellingen voor Hallo virtuele machine zodat deze gereed voor failover. U kunt een test failover toocheck die alles werkt zoals verwacht op dit moment kunt uitvoeren.

### <a name="delta-replication"></a>Replicatie van verschillen

1. Na de initiële replicatie hello Start de Deltasynchronisatie in overeenstemming met de replicatie-instellingen.
2. Hallo Hyper-V Replica Replication Tracker bijgehouden Hallo wijzigingen tooa virtuele hardeschijf als .hrl-bestanden. Elke schijf die voor replicatie is geconfigureerd, heeft een bijbehorend .hrl-bestand. Dit logboek wordt storage-account van de klant toohello verzonden nadat de initiële replicatie is voltooid. Wanneer een logboek in transit tooAzure, in een ander logboekbestand in Hallo Hallo wijzigingen in de primaire schijf Hallo worden bijgehouden dezelfde directory.
3. Tijdens de eerste en delta-replicatie, kunt u Hallo VM in Hallo VM weergave bewaken. [Meer informatie](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>Replicatiesynchronisatie

1. Als de replicatie van verschillen mislukt en een volledige replicatie veel bandbreedte of tijd zou kosten, wordt de virtuele machine gemarkeerd voor hersynchronisatie. Bijvoorbeeld, als Hallo .hrl bestanden 50% van de schijfgrootte hello bereiken, vervolgens hello VM gemarkeerd voor hersynchronisatie.
2.  Hersynchronisatie wordt geminimaliseerd Hallo en de hoeveelheid gegevens die zijn verzonden door controlesommen van Hallo bron- en virtuele machines en alleen Hallo delta-gegevens te verzenden. Hersynchronisatie maakt gebruik van een vaste-blokalgoritme voor verdelen in segmenten, waarbij bron- en doelbestanden in vaste segmenten worden verdeeld. Controlesommen voor elk segment worden gegenereerd en worden vervolgens vergeleken toodetermine die vanaf het Hallo-bron moet toobe toegepaste toohello doel wordt geblokkeerd.
3. Na hersynchronisatie moet de normale replicatie van verschillen worden hervat. Hersynchronisatie is standaard geplande toorun automatisch buiten kantooruren, maar u kunt een virtuele machine handmatig synchroniseren. U kunt de hersynchronisatie bijvoorbeeld hervatten als er een netwerkstoring of een andere storing optreedt. toodo deze, selecteer Hallo VM in de portal Hallo > **opnieuw synchroniseren**.

    ![Handmatig opnieuw synchroniseren](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Nieuwe pogingen

Als er een replicatiefout optreedt, wordt de replicatie automatisch opnieuw geprobeerd. Deze logica kan in twee categorieën worden ingedeeld:

**Categorie** | **Details**
--- | ---
**Niet-herstelbare fouten** | Er wordt geen nieuwe poging gedaan. De status van de virtuele machine is **Kritiek** en tussenkomst van de beheerder is vereist. Voorbeelden van deze fouten zijn: verbroken VHD keten; Ongeldige status voor Hallo replica-VM; Netwerk verificatiefouten: fouten autorisatie; Virtuele machine geen fouten gevonden (voor zelfstandige Hyper-V-servers)
**Herstelbare fouten** | Nieuwe pogingen uitgevoerd elke replicatie-interval, met behulp van een exponentiële back-uit die Hallo-interval voor opnieuw proberen van Hallo begin van de eerste poging Hallo door 1, 2, 4, 8 en 10 minuten verhoogt. Als een fout zich blijft voordoen, probeert u het om de 30 minuten opnieuw. Voorbeelden zijn onder meer: netwerkfouten; fouten in verband met weinig schijfruimte; weinig geheugenruimte |

## <a name="protection-and-recovery-lifecycle"></a>Levenscyclus beveiliging en herstel

![werkstroom](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Volgende stappen

- [Vereisten voor implementatie controleren](site-recovery-prereq.md)
- Problemen oplossen met:
    - [Beveiliging controleren en beveiligingsproblemen oplossen](site-recovery-monitoring-and-troubleshooting.md)
    - [Hulp van Microsoft-ondersteuning](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [Veelvoorkomende fouten en oplossingen](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
