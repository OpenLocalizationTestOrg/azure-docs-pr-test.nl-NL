---
title: aaaHow toofail door Azure tooVMware | Microsoft Docs
description: "U kunt een failback toobring virtuele machines back tooon-on-premises starten na een failover van virtuele machines tooAzure. Meer informatie over stappen voor hoe toofail reservekopieën Hallo."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Failback van Azure tooan lokale site

Dit artikel wordt beschreven hoe toofail back-virtuele machines van Azure Virtual Machines toohello lokale site. Hallo Volg de instructies in dit artikel toofail back uw virtuele VMware-machines of fysieke Windows of Linux-servers nadat ze van Hallo lokale site tooAzure hebt failover met behulp van Hallo [repliceren VMware virtuele machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) zelfstudie.

> [!WARNING]
> Als u hebt [migratie voltooid](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), Hallo verplaatste virtuele machine tooanother resource groep of verwijderde virtuele machine van Azure Hallo, u kunt geen failback daarna.

> [!NOTE]
> Als u virtuele VMware-machines failover vervolgens kunt u niet failback tooa Hyper-v-host.

## <a name="overview-of-failback"></a>Overzicht van failback
Hier volgt de werking van failback. Nadat u hebt tooAzure failover, kunt u back tooyour lokale site niet in een aantal fasen:

1. [Beveiligt](site-recovery-how-to-reprotect.md) Hallo van virtuele machines in Azure, zodat ze tooreplicate tooVMware virtuele machines in uw on-premises site starten. Als onderdeel van dit proces moet u ook:
    1. Het hoofddoel van een lokale instellen: Windows hoofddoel voor virtuele machines van Windows en [Linux-hoofddoel](site-recovery-how-to-install-linux-master-target.md) voor virtuele Linux-machines.
    2. Instellen van een [processerver](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Initiëren [beveiligt](site-recovery-how-to-reprotect.md). Hiermee wordt het Hallo on-premises virtuele machine uitschakelen en hello Azure synchroniseren de gegevens van virtuele machine met Hallo lokale schijven.
5. Nadat u uw virtuele machines in Azure zijn tooyour lokale site repliceren, start u een mislukken via van Azure toohello lokale site.

Nadat uw gegevens terug is mislukt, beveiligt u Hallo on-premises virtuele machines die u niet terug naar zodat deze tooreplicate tooAzure beginnen.

Bekijk voor een snel overzicht Hallo video over hoe toofail via uit Azure tooan lokale site te volgen.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>De oorspronkelijke of alternatieve locatie back toohello mislukt

Als de failover van een virtuele VMware-machine kunt u back toohello dezelfde bron op de lokale virtuele machine als deze nog wordt uitgevoerd bestaat niet. In dit scenario worden alleen Hallo wijzigingen terug gerepliceerd. Dit scenario wordt ook wel herstel oorspronkelijke locatie. Als Hallo on-premises virtuele machine niet bestaat, is het Hallo-scenario herstel van een alternatieve locatie.

> [!NOTE]
> U kunt alleen de failback toohello oorspronkelijke vCenter en de configuratieserver. U kunt een nieuwe configuratieserver en gebruik van failback niet implementeren. U toevoegen niet ook een nieuwe vCenter toohello afgesloten configuratieserver en de failback naar de nieuwe vCenter Hallo.

#### <a name="original-location-recovery"></a>Herstel oorspronkelijke locatie

Als u niet de oorspronkelijke virtuele machine back toohello, zijn Hallo volgende voorwaarden zijn vereist:
* Als Hallo virtuele machine wordt beheerd door een vCenter-server, klikt u vervolgens hebt hello hoofddoel van ESX-host datastore toegang toohello van virtuele machine.
* Als Hallo virtuele machine zich op een ESX-host, maar wordt niet beheerd door de vCenter, moet het Hallo harde schijf van Hallo virtuele machine in een gegevensopslag die Hallo master-doelhost toegang tot.
* Als uw virtuele machine zich op een ESX-host en maakt geen gebruik van vCenter, moet u detectie van Hallo ESX-host van het hoofddoel Hallo uitvoeren voordat u opnieuw beveiligen. Dit geldt als u bent terug fysieke servers te mislukken.
* U kunt back tooa virtuele storage area network (vSAN) of een schijf die op basis van niet-gecodeerd apparaat (RDM) toewijzen als Hallo schijven bestaan al en verbonden toohello on-premises virtuele machine zijn mislukt.

#### <a name="alternate-location-recovery"></a>Herstel van alternatieve locatie
Als Hallo on-premises virtuele machine niet bestaat voordat Hallo virtuele machine opnieuw te beveiligen, heet Hallo scenario herstel van een alternatieve locatie. Hallo beveiligt werkstroom maakt Hallo on-premises virtuele machine opnieuw. Ook wordt hierdoor het downloaden van een volledige gegevens.

* Wanneer u een alternatieve locatie back tooan failover, Hallo virtuele machine herstelde toohello is niet dezelfde ESX-host op welke Hallo hoofddoelserver wordt geïmplementeerd. Hallo gegevensopslag die is gebruikt toocreate Hallo schijf worden Hallo hetzelfde gegevensarchief die is geselecteerd toen Hallo virtuele machine opnieuw te beveiligen.
* U kunt terug alleen tooa virtuele machine file system (VMFS) datastore mislukken. Als u een virtueel SAN of RDM hebt, werkt beveiligt en failback niet.
* Beveiligt, moet u een grote eerste gegevensoverdracht die wordt gevolgd door Hallo wijzigingen. Dit proces bestaat omdat Hallo virtuele machine niet on-premises bestaat. Hallo volledige gegevens moeten toobe terug gerepliceerd. Deze opnieuw beveiligen duurt ook langer dan een herstel van de oorspronkelijke locatie.
* U kunt terug toovSAN of RDM gebaseerde schijven niet afkeuren. Nieuwe virtuele machine-schijven (VMDKs) kunnen alleen worden gemaakt op een gegevensopslag VMFS.

Een fysieke computer wanneer failover tooAzure, failover back alleen als een virtuele VMware-machine (ook waarnaar wordt verwezen tooas P2A2V). Deze stroom valt onder Hallo herstellen op alternatieve locaties.

* Een fysieke server van Windows Server 2008 R2 SP1, kan niet als beveiligd en tooAzure, failover worden uitgevoerd voor terug.
* Zorg ervoor dat u ten minste één hoofddoel server en Hallo nodig ESX/ESXi-hosts toowhich u toofail terug moet detecteren.

## <a name="have-you-completed-reprotection"></a>Hebt u beveiligingspoging voltooid?
Voordat u doorgaat, beveiligt voltooid Hallo stappen zodat Hallo virtuele machines zich in een gerepliceerde status en u kunt een failover back tooan lokale site starten. Zie voor meer informatie [hoe tooreprotect vanuit Azure tooon lokale](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Vereisten

* Een configuratieserver is on-premises vereist als u een failback doet. Tijdens de failback, Hallo virtuele machine moet aanwezig zijn in de configuratiedatabase server Hallo of failback won't slagen. Dus zorgen ervoor dat u regelmatig geplande back-ups van uw server. Als er een ramp is, moet u toorestore Hallo server Hello hetzelfde IP-adres voor failback toowork.
* de hoofddoelserver Hallo mag geen eventuele momentopnamen voordat failback.

## <a name="steps-toofail-back"></a>Stappen toofail terug

> [!IMPORTANT]
> Voordat u een failback-bewerking starten, zorg ervoor dat u waarvoor Hallo virtuele machines hebt voltooid. Hallo virtuele machines moet in een beveiligde staat en hun status moet **OK**. tooreprotect hello virtuele machines gelezen [hoe tooreprotect](site-recovery-how-to-reprotect.md).

1. In Hallo gerepliceerde items pagina Hallo virtuele machine en selecteer met de rechtermuisknop op het tooselect **niet-geplande Failover**.
2. In **bevestigen Failover**, Controleer of de failoverrichting hello (van Azure) en selecteer Hallo herstelpunt (laatste of Hallo nieuwste app consistent) wilt u toouse voor Hallo failover. Hallo app consistent punt achter het laatste herstelpunt Hallo is in de tijd en zorgt ervoor dat er gegevens verloren gaan.
3. Site Recovery afgesloten Hallo virtuele machines in Azure tijdens failover. Nadat u hebt gecontroleerd dat failback is voltooid zoals verwacht, kunt u controleren dat Hallo virtuele machines in Azure is afgesloten.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>het herstelpunt toowhat kan ik mislukken back Hallo virtuele machines?

Tijdens de failback hebt u twee opties toofail back Hallo/herstel van virtuele machine plannen.

Als u Hallo meest recente verwerkte punt in tijd selecteert, worden alle virtuele machines in de tijd via tootheir meest recente beschikbare herstelpunt mislukt. Er is een replicatiegroep in het herstelplan hello, mislukken elke virtuele machine van de replicatiegroep Hallo via tooits onafhankelijke laatste herstelpunt in de tijd.

U kan geen failback uit op een virtuele machine totdat er ten minste één herstelpunt. U kan niet een failback uit op een herstelplan totdat alle virtuele machines ten minste één herstelpunt.

> [!NOTE]
> Meest recente herstelpunt is een crashconsistent herstelpunt.

Als u Hallo toepassing consistent herstelpunt hebt geselecteerd, wordt een enkele virtuele machine failback tooits meest recente beschikbare toepassingsconsistente herstelpunt herstellen. Elke replicatiegroep herstelt in geval van een herstelplan met een replicatiegroep Hallo tooits algemene beschikbaar herstelpunt vermeld.
Houd er rekening mee dat toepassingsconsistente herstelpunten kunnen zich niet achter in de tijd en er wordt mogelijk verlies van gegevens.

### <a name="what-happens-toovmware-tools-post-failback"></a>Wat gebeurt er tooVMware hulpprogramma's na de failback?

Tijdens de failover-tooAzure kunnen niet Hallo VMware tools op Hallo virtuele machine van Azure worden uitgevoerd. In geval van een virtuele Windows-computer ASR Hallo VMware tools uitgeschakeld tijdens de failover. In geval van een virtuele Linux-machine verwijdert ASR Hallo VMware tools tijdens failover.

Hallo VMware tools zijn tijdens de failback van virtuele machine met Windows hello opnieuw bij de failback is ingeschakeld. Op deze manier voor een virtuele linux-machine, Hallo VMware tools opnieuw geïnstalleerd op machine Hallo tijdens de failback.

## <a name="next-steps"></a>Volgende stappen

Nadat de failback is voltooid, moet u toocommit Hallo virtuele machine tooensure die virtuele machines in Azure wordt hersteld, worden verwijderd.

### <a name="commit"></a>Doorvoeren
Doorvoeren is vereist tooremove Hallo failover van virtuele machine van Azure.
Met de rechtermuisknop op Hallo beveiligde item en klik vervolgens op **doorvoeren**. Een taak verwijdert Hallo failover van virtuele machines in Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Beveiligt van lokale tooAzure

Nadat het vastleggen is voltooid, de virtuele machine terug op Hallo lokale site is, maar won't worden beveiligd. toostart tooreplicate tooAzure opnieuw Hallo te volgen:

1. In **kluis** > **instelling** > **gerepliceerde items**, selecteer de virtuele machines die zijn mislukt terug en klik vervolgens op Hallo  **Beveilig de farm opnieuw**.
2. Hallo-waarde van de processerver Hallo dat toobe gebruikt toosend gegevens back tooAzure moet geven.
3. Klik op **OK** toobegin Hallo beveiligt taak.

> [!NOTE]
> Nadat een on-premises virtuele machine wordt opgestart, duurt het enige tijd voor de agent Hallo tooregister back toohello configuratieserver (omhoog too15 minuten). Gedurende deze tijd beveiligt mislukt en retourneert een foutmelding die Hallo-agent is niet geïnstalleerd. Wacht een paar minuten en probeer het vervolgens opnieuw beveiligt.

Nadat het Hallo beveiligt de taak is voltooid, Hallo virtuele machine repliceert back tooAzure en kunt u een failover uitvoeren.

## <a name="common-issues"></a>Algemene problemen
Zorg ervoor dat vCenter Hallo een verbonden status heeft in voordat u een failback. Virtuele machine wordt anders mislukken schijven verbreken en het back-toohello koppelen.
