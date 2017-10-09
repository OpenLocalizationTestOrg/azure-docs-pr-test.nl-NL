---
title: overzicht van de virtuele Azure StorSimple-matrix aaaMicrosoft | Microsoft Docs
description: "Hierin wordt beschreven Hallo StorSimple virtuele matrix, een geïntegreerde opslagoplossing die opslagtaken tussen een lokale virtuele-matrix en Microsoft Azure cloud-opslag beheert."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Inleiding toohello virtuele StorSimple-matrix
## <a name="overview"></a>Overzicht
Hallo Microsoft Azure StorSimple virtuele matrix is een geïntegreerde opslagoplossing die beheert opslagtaken tussen een lokale virtuele-matrix uitgevoerd in een hypervisor en Microsoft Azure cloud-opslag. Hallo virtuele matrix is een efficiënte, rendabele en eenvoudig beheerde bestandsserver of iSCSI-serveroplossing die veel Hallo problemen en kosten in verband met enterprise-opslag en gegevensbeveiliging. Hallo virtuele matrix is met name geschikt voor externe office/filiaalscenario's.

In dit onderwerp biedt een overzicht van de virtuele matrix Hallo - er zijn andere bronnen:

* Zie voor aanbevolen procedures [aanbevolen procedures voor virtuele StorSimple-matrix](storsimple-ova-best-practices.md).
* Voor een overzicht van apparaten Hallo StorSimple 8000-serie gaat te[StorSimple 8000-serie: een oplossing voor hybride cloud](storsimple-overview.md). 
* Voor informatie over apparaten Hallo StorSimple 5000/7000-serie gaat te[Online-Help voor StorSimple](http://onlinehelp.storsimple.com/).

Hallo virtuele matrix ondersteunt Hallo iSCSI-protocol Server Message Block (SMB). Het wordt uitgevoerd op uw bestaande infrastructuur van de hypervisor en biedt lagen toohello cloud, cloud back-up, herstel op itemniveau, snel terugzetten en disaster recovery functies.

Hallo volgende tabel geeft een overzicht van belangrijke functies Hallo Hallo virtuele StorSimple-matrix.

| Functie | StorSimple Virtual Array |
| --- | --- |
| Vereisten voor installatie |Maakt gebruik van virtualisatie-infrastructuur (Hyper-V- of VMware) |
| Beschikbaarheid |Eén knooppunt |
| Totale capaciteit (met inbegrip van de cloud) |Too64 TB bruikbare capaciteit per virtuele matrix |
| Lokale capaciteit |390 GB too6.4 TB bruikbare capaciteit per virtuele matrix (nodig tooprovision 500 GB too8 TB aan schijfruimte) |
| Systeemeigen protocollen |iSCSI- of SMB |
| Beoogde hersteltijd (RTO) |iSCSI: ongeacht de grootte van minder dan twee minuten |
| Recovery Point Objective (RPO) |Dagelijkse back-ups en back-ups op aanvraag |
| Opslaglagen |Maakt gebruik van Breng toewijzing toodetermine welke gegevens moeten tiers worden verdeeld, in- of |
| Ondersteuning |Ondersteund door de leverancier Hallo virtualisatie-infrastructuur |
| Prestaties |Varieert afhankelijk van de onderliggende infrastructuur |
| Gegevensmobiliteit |Toohello kunt herstellen hetzelfde apparaat of itemniveau herstel (bestandsserver) |
| Opslaglagen |Opslag van de lokale hypervisor en cloud |
| Grootte van de bestandsshare |Gelaagde: van too20 TB; lokaal vastgemaakt: too2 TB omhoog |
| De grootte van volume |Gelaagde: 500 GB too5 TB; lokaal vastgemaakt: 50 GB too500 GB |
| De grootte van volume |Gelaagde: van too5 TB; lokaal vastgemaakt: too500 GB omhoog |
| Momentopnamen |Crashconsistent |
| Herstel op itemniveau |Ja; gebruikers kunnen herstellen van shares |

## <a name="why-use-storsimple"></a>Waarom StorSimple gebruiken?
StorSimple verbindt tooAzure opslag voor gebruikers en -servers in minuten, er zijn geen wijzigingen in de toepassing.

Hallo volgende tabel worden enkele van de belangrijkste voordelen van Hallo die Hallo virtuele StorSimple-matrix oplossing biedt.

| Functie | Voordeel |
| --- | --- |
| Transparante-integratie |Hallo virtuele matrix ondersteunt Hallo iSCSI- of Hallo SMB-protocol. Hallo gegevensverplaatsing tussen lokale laag Hallo of Hallo cloud is naadloze en transparante toohello gebruiker. |
| Lagere opslagkosten |Met StorSimple, moet u voldoende lokale opslag toomeet huidige aanvragen voor de meest gebruikte Hallo hot gegevens inrichten. Wanneer opslag groeien behoeften, cloud StorSimple lagen koude gegevens in rendabele opslag. Hallo-gegevens worden ontdubbeld en gecomprimeerd voordat toohello cloud verzonden toofurther opslagvereisten en kosten verminderen. |
| Vereenvoudigd opslagbeheer |StorSimple biedt gecentraliseerd beheer in Hallo cloud met behulp van Apparaatbeheer StorSimple toomanage meerdere apparaten. |
| Verbeterde noodherstel en naleving |Noodherstel sneller vergemakkelijkt StorSimple door Hallo metagegevens onmiddellijk herstellen en Hallo gegevens terugzetten naar behoefte. Dit betekent dat met het normale bewerkingen kunnen doorgaan met minimale onderbrekingen. |
| Gegevensmobiliteit |Gelaagde toohello cloud toegankelijk is vanaf andere sites voor herstel en migratie van gegevens. Houd er rekening mee dat u de gegevens alleen toohello oorspronkelijke virtuele matrix kunt herstellen. Echter, u disaster recovery functies toorestore Hallo volledige virtuele matrix tooanother virtuele matrix. |

## <a name="storsimple-workload-summary"></a>StorSimple workloadoverzicht

Hieronder wordt een overzicht van ondersteunde StorSimple werkbelastingen in een tabel.

|Scenario     |Workload     |Ondersteund      |Beperkingen               |
|-------------|-------------|---------------|---------------------------|
|ROBO samenwerking |Delen van bestanden     |Ja      |Zie [maximaal limieten voor bestandsserver](storsimple-ova-limits.md).<br></br>Zie [systeemvereisten voor ondersteunde versies van SMB-](storsimple-ova-system-requirements.md).| Alle versies     |

## <a name="workflows"></a>Werkstromen
Hallo virtuele StorSimple-matrix is bijzonder geschikt voor Hallo werkstromen te volgen:

* [Cloud-gebaseerd opslagbeheer](#cloud-based-storage-management)
* [Locatie-onafhankelijke back-up](#location-independent-backup)
* [Data protection en herstel na noodgevallen](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>cloud-gebaseerd opslagbeheer
U kunt Hallo Apparaatbeheer StorSimple-service die wordt uitgevoerd in Azure portal toomanage gegevens die zijn opgeslagen op meerdere apparaten Hallo en op meerdere locaties. Dit is vooral nuttig in scenario's voor gedistribueerde vertakking. Houd er rekening mee dat u afzonderlijke exemplaren van Hallo Apparaatbeheer StorSimple-service toomanage virtuele matrices en fysieke StorSimple-apparaten moet maken. Let ook op dat Hallo van de nieuwe Azure portal dat virtuele matrix Hallo nu gebruikt in plaats van Hallo klassieke Azure-portal.

![cloud-gebaseerd opslagbeheer](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Locatie-onafhankelijke back-up
Met virtuele Hallo-matrix bieden cloudmomentopnamen een locatie-onafhankelijke, punt in tijd kopie van een volume of share. Cloudmomentopnamen zijn standaard ingeschakeld en kunnen niet worden uitgeschakeld. Alle volumes en shares zijn back-up op Hallo dezelfde tijdstip via een enkel dagelijkse back-upbeleid en u extra ad-hoc back-ups zo nodig kunt nemen.

### <a name="data-protection-and-disaster-recovery"></a>Data protection en herstel na noodgevallen
Hallo virtuele matrix ondersteunt Hallo data protection en noodherstel herstelscenario's te volgen:

* **Volume of share terugzetten** : Hallo terugzetten gebruiken als nieuwe werkstroom toorecover een volume of share. Gebruik deze benadering toorecover Hallo hele volume of share.
* **Item-level recovery** – Shares vereenvoudigde toegang toestaan toorecent back-ups. U kunt gemakkelijk een afzonderlijk bestand herstellen vanaf een speciale *.backup* map die beschikbaar zijn in Hallo cloud. Deze mogelijkheid terugzetten is door gebruikers geïnitieerde en hoeft u geen beheerdersrechten ondernemen.
* **Herstel na noodgevallen** – gebruik Hallo failover mogelijkheid toorecover alle volumes of shares tooa nieuwe virtuele matrix. U nieuwe virtuele matrix Hallo maken en bij Hallo StorSimple-apparaat Manager-service registreren en vervolgens failover van de oorspronkelijke virtuele matrix Hallo. nieuwe virtuele matrix Hallo krijgt vervolgens Hallo ingericht resources. 

## <a name="storsimple-virtual-array-components"></a>Virtuele StorSimple-matrix-onderdelen
Hallo virtuele matrix bevat Hallo volgende onderdelen:

* [Virtuele matrix](#virtual-array) – een hybride cloud-opslagapparaat op basis van een virtuele machine ingericht in uw gevirtualiseerde omgeving of de hypervisor.  
* [StorSimple-apparaat Manager-service](#storsimple-device-manager-service) – een uitbreiding van hello Azure-portal waarmee u een of meer StorSimple-apparaten beheren via een enkel webinterface die u vanuit verschillende geografische locaties openen kunt. U kunt Hallo Apparaatbeheer StorSimple-service toocreate gebruiken en services beheren, weergeven en beheren van apparaten en waarschuwingen en beheren van volumes, shares en bestaande momentopnamen.
* [Lokale online gebruikersinterface](#local-web-user-interface) – een webgebaseerde gebruikersinterface die gebruikte tooconfigure Hallo apparaat zodat het verbinding maken met het lokale netwerk toohello en registreer Hallo-apparaat met Hallo Apparaatbeheer StorSimple-service. 
* [Opdrachtregelinterface](#command-line-interface) – een Windows PowerShell-interface waarmee u toostart een ondersteuningssessie op de virtuele Hallo-matrix kunt.
  Hallo volgende secties beschrijven elk van deze onderdelen in meer detail en wordt uitgelegd hoe Hallo oplossing rangschikt gegevens, wijst opslag en vereenvoudigt het beheer van opslag en gegevensbeveiliging.

### <a name="virtual-array"></a>Virtuele matrix
Hallo virtuele matrix is een enkel knooppunt opslagoplossing die primaire opslag biedt, beheert de communicatie met de cloudopslag en helpt tooensure Hallo beveiligings- en vertrouwelijkheid van alle gegevens die zijn opgeslagen op Hallo-apparaat.

Hallo virtuele matrix is beschikbaar in één model dat is gedownload. Hallo virtuele matrix heeft een maximale capaciteit van 6.4 TB op Hallo-apparaat (met een onderliggende eisen aan opslag van 8 TB) en met inbegrip van 64 TB cloudopslag. 

Hallo virtuele matrix heeft Hallo volgende kenmerken:

* Betaalbaar is. Deze maken gebruik van uw bestaande virtualisatie-infrastructuur en kunnen worden geïmplementeerd op uw bestaande Hyper-V- of VMware-hypervisor.
* Deze bevindt zich in Hallo datacenter en kan worden geconfigureerd als een server met iSCSI- of een bestandsserver. 
* Het is geïntegreerd met Hallo cloud.
* Back-ups worden opgeslagen in de cloud hello, die u kunt herstel na noodgevallen vergemakkelijken en herstel op itemniveau (ILR) vereenvoudigen. 
* Net zoals u ze, kunt u tooa fysieke apparaat toepassen wilt, kunt u updates toohello virtuele matrix, toepassen.

> [!NOTE]
> Een virtuele-matrix kan niet worden uitgebreid. Daarom is het belangrijk tooprovision voldoende opslagruimte bij het maken van virtuele Hallo-matrix. 
> 
> 

### <a name="storsimple-device-manager-service"></a>StorSimple-apparaat Manager-service
Microsoft Azure StorSimple biedt een webgebaseerde gebruikersinterface Hallo Apparaatbeheer StorSimple-service, waarmee u toocentrally StorSimple opslag te beheren. U kunt Hallo Apparaatbeheer StorSimple-service tooperform Hallo taken te volgen:

* Meerdere virtuele StorSimple-matrices van een service beheren. 
* Configureren en beheren van de beveiligingsinstellingen voor het virtuele StorSimple-matrices. (Hallo cloud-versleuteling is afhankelijk van de Microsoft Azure-API's.)
* Storage-accountreferenties en -eigenschappen configureren.
* Configureren en beheren van volumes of shares.
* Back-up en herstel van gegevens op volumes of shares.
* Prestaties controleren.
* Systeeminstellingen bekijken en mogelijke problemen te identificeren.

U Hallo Apparaatbeheer StorSimple-service tooperform dagelijks beheer van uw virtuele matrix.

Voor meer informatie gaat te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Lokale online gebruikersinterface
Hallo virtuele matrix bevat een webgebaseerde gebruikersinterface die wordt gebruikt voor eenmalige configuratie en de registratie van apparaat Hallo Hello StorSimple-apparaat Manager-service. U kunt tooshut omlaag gebruiken en opnieuw opstarten van virtuele Hallo-matrix, diagnostische tests uitvoeren, software bijwerken, Hallo apparaat beheerderswachtwoord wijzigen, het systeemlogboek in logboeken bekijken en neem contact op met Microsoft Support toofile een serviceaanvraag. 

Voor informatie over het gebruik van Hallo webgebaseerde gebruikersinterface, gaat u te[gebruik Hallo webgebaseerde gebruikersinterface tooadminister uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Opdrachtregelinterface
Hallo opgenomen Windows PowerShell-interface kunt u tooinitiate een ondersteuningssessie met Microsoft Support, zodat ze kunt u problemen op te lossen die op uw virtuele matrix optreden kunnen.

## <a name="storage-management-technologies"></a>Beheer van opslagtechnologieën
Bovendien Hallo toohello virtuele matrix en andere onderdelen, StorSimple-oplossing gebruikt Hallo volgt software technologieën tooprovide snelle toegang tooimportant gegevens, opslagverbruik te verlagen en beveiligen van gegevens die zijn opgeslagen op uw virtuele matrix:

* [Automatische opslaglagen](#automatic-storage-tiering) 
* [Lokaal vastgemaakt shares en -volumes](#locally-pinned-shares-and-volumes)
* [Compressie van gegevens voor Ontdubbeling en lagen of een back-up toohello cloud](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Geplande en on-demand back-ups](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Automatische opslaglagen
Hallo virtuele matrix gebruikt een nieuwe lagen mechanisme toomanage opgeslagen gegevens op Hallo virtuele matrix en Hallo cloud. Er zijn slechts twee lagen: Hallo lokale virtuele-matrix en Azure-cloudopslag. Hallo virtuele StorSimple-matrix worden gegevens automatisch in Hallo-lagen op basis van een heatmap die actuele informatie over het gebruik, leeftijd en relaties tooother gegevens bijhoudt geplaatst. Gegevens die de meeste actief (gegevensbeheer) lokaal is opgeslagen, terwijl minder actieve en inactieve gegevens automatisch wordt gemigreerd toohello cloud. (Alle back-ups worden opgeslagen in de cloud Hallo.) StorSimple aanpast en gegevens opnieuw worden ingedeeld en toewijzingen van de opslag als gebruikspatronen wijzigen. Sommige gegevens kan bijvoorbeeld worden minder actief gedurende een bepaalde periode. Als deze actief geleidelijk minder, is deze lagen uit toohello cloud. Als dat dezelfde gegevens opnieuw geactiveerd wordt, is deze lagen in toohello opslagmatrix.

Gegevens voor een bepaalde gelaagde bestandsshare of het volume is een eigen lokale laag ruimte gegarandeerd. (ongeveer 10% van de totale Hallo ingerichte ruimte voor deze share of het volume). Terwijl dit wordt beperkt door de beschikbare opslagruimte Hallo op Hallo virtuele matrix voor die share of het volume, zorgt u ervoor dat lagen voor één share of het volume niet worden beïnvloed door Hallo lagen behoeften van andere shares of volumes. Een bezet werkbelasting op een share of het volume kan niet alle cloud van andere werkbelastingen toohello dus niet afdwingen. 

![Automatische opslaglagen](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> U kunt een als lokaal vastgemaakt volume opgeven, in welk geval Hallo gegevens op de virtuele matrix Hallo blijft en nooit is gelaagd toohello cloud. Voor meer informatie gaat te[lokaal vastgemaakt-shares en -volumes](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Lokaal vastgemaakt shares en -volumes
U kunt de juiste shares en -volumes als lokaal vastgemaakt maken. Deze mogelijkheid zorgt ervoor dat gegevens die nodig zijn voor kritieke toepassingen in Hallo virtuele matrix blijft en nooit is gelaagd toohello cloud. Lokaal vastgemaakt bestandsshares en volumes hebben Hallo volgende kenmerken: 

* Ze zijn geen onderwerp toocloud latenties of problemen met de netwerkverbinding.
* Ze blijven profiteren van de StorSimple-cloud back-up en noodherstel herstelfuncties.

U kunt een lokaal vastgemaakt share of volume als lagen of een gelaagde share herstellen of volume als lokaal vastgemaakt. 

Voor meer informatie over lokaal vastgemaakte volumes gaat te[hello StorSimple Apparaatbeheer service toomanage volumes gebruiken](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>Compressie van gegevens voor Ontdubbeling en lagen of een back-up toohello cloud
StorSimple maakt gebruik van Ontdubbeling en gegevens compressie toofurther verminderen de opslagvereisten in Hallo cloud. Ontdubbeling vermindert Hallo totale hoeveelheid gegevens die zijn opgeslagen doordat redundantie in de gegevensset Hallo opgeslagen. Omdat informatie wordt gewijzigd, StorSimple Hallo ongewijzigd gegevens negeert en opnamen Hallo alleen wijzigingen. StorSimple vermindert bovendien Hallo en de hoeveelheid opgeslagen gegevens door het identificeren en verwijderen van dubbele gegevens. 

> [!NOTE]
> Gegevens die zijn opgeslagen op de virtuele Hallo-matrix is geen ontdubbeld of gecomprimeerd. Alle Ontdubbeling en compressie vindt plaats voordat Hallo gegevens toohello cloud worden verzonden.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Geplande en on-demand back-ups
Functies voor gegevensbeveiliging StorSimple kunnen u back-ups van toocreate op aanvraag. Een back-upschema standaard Bovendien zorgt ervoor dat de back-up dagelijks. Back-ups zijn gemaakt in de vorm Hallo van incrementele momentopnamen die zijn opgeslagen in de cloud Hallo. Momentopnamen die alleen Hallo wijzigingen sinds de laatste back-up Hallo vastlegt, worden gemaakt en snel worden hersteld. Deze momentopnamen is zeer belangrijk in herstel na noodgevallen, omdat ze secundaire opslagsystemen (zoals tapeback-up vervangen) en kunnen u toorestore gegevens tooyour datacenter of tooalternate sites indien nodig.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe te[voorbereiden Hallo virtuele matrix portal](storsimple-virtual-array-deploy1-portal-prep.md).

