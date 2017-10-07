---
title: aaaWhat is StorSimple Snapshot Manager? | Microsoft Docs
description: Hierin wordt beschreven Hallo StorSimple Snapshot Manager, de architectuur en bijbehorende functies.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Een inleiding tooStorSimple Snapshot Manager

## <a name="overview"></a>Overzicht
StorSimple Snapshot Manager is een module Microsoft Management Console (MMC) die vereenvoudigt de bescherming van gegevens en back-beheer in een Microsoft Azure StorSimple-omgeving. Met StorSimple Snapshot Manager beheren Microsoft Azure StorSimple-gegevens in het datacenter hello en in Hallo cloud als een oplossing voor één geïntegreerde opslag, dus back-processen te vereenvoudigen en de kosten te verlagen.

Dit overzicht Hallo StorSimple Snapshot Manager introduceert, worden de functies beschreven en wordt uitgelegd de rol in Microsoft Azure StorSimple. 

Zie voor een overzicht van Hallo gehele Microsoft Azure StorSimple-systeem, inclusief Hallo StorSimple-apparaat, StorSimple Manager-service, StorSimple Snapshot Manager en StorSimple-Adapter voor SharePoint, [StorSimple 8000-serie: een hybride cloud opslagoplossing](storsimple-overview.md). 

> [!NOTE]
> * U kunt StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple virtuele matrices (ook wel bekend als StorSimple on-premises virtuele apparaten) niet gebruiken.
> * Als u van plan tooinstall StorSimple Update 2 op uw StorSimple-apparaat bent, toodownload Hallo meest recente versie ervoor van StorSimple Snapshot Manager en het installeren **voordat u het StorSimple Update 2 installeert**. Hallo meest recente versie van StorSimple Snapshot Manager is achterwaarts compatibel en werkt met alle uitgebrachte versies van Microsoft Azure StorSimple. Als u Hallo eerdere versie van StorSimple Snapshot Manager gebruikt, moet u tooupdate it (u hoeft niet toouninstall Hallo vorige versie voordat u de nieuwe versie Hallo installeren).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>StorSimple Snapshot Manager doel en architectuur
StorSimple Snapshot Manager biedt een centrale beheerconsole waarmee u toocreate consistent kunt, back-ups van de punt in tijd van lokale en cloud gegevens. U kunt bijvoorbeeld Hallo-console om te gebruiken:

* Configureer back-up en volumes verwijderen.
* Volume configureert tooensure groepen waarvan een back-up van gegevens is toepassingsconsistente.
* Back-upbeleid beheren zodat de back-up op een vooraf vastgestelde planning.
* Maken van lokale en cloud worden opgeslagen die kunnen worden opgeslagen in de cloud Hallo en gebruikt voor herstel na noodgevallen.

Hallo StorSimple Snapshot Manager haalt Hallo lijst met toepassingen die zijn geregistreerd bij Hallo VSS-provider op Hallo host. Vervolgens toocreate toepassingsconsistente back-ups, controleert deze Hallo volumes die worden gebruikt door een toepassing en volume groepen tooconfigure wordt voorgesteld. StorSimple Snapshot Manager gebruikt deze volume groepen toogenerate back-ups die toepassing consistent zijn. (Consistentie van de toepassing bestaat als alle bestanden bijbehorende en de databases zijn gesynchroniseerd en Hallo true status van de toepassing hello op een bepaald punt in de tijd weer.) 

StorSimple Snapshot Manager back-ups worden Hallo vorm van incrementele momentopnamen die alleen Hallo wijzigingen sinds de laatste back-up Hallo vast te leggen. Als gevolg hiervan worden back-ups vereisen minder opslagruimte en gemaakt en snel worden hersteld. StorSimple Snapshot Manager maakt gebruik van Hallo Windows Volume Shadow Copy Service (VSS) tooensure dat momentopnamen van toepassingsconsistente gegevens vastleggen. (Ga toohello integratie met Windows Volume Shadow Copy Service sectie voor meer informatie.) Met StorSimple Snapshot Manager kunt u back-upschema's maken of directe back-ups uitvoeren indien nodig. Als u nodig hebt toorestore gegevens uit een back-up, StorSimple Snapshot Manager kunt u vanuit een catalogus van de lokale of cloudmomentopnamen. Azure StorSimple herstelt alleen Hallo gegevens die nodig is deze nodig is, waardoor vertragingen in de beschikbaarheid van gegevens tijdens de herstelbewerkingen.)

![StorSimple Snapshot Manager-architectuur](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**StorSimple Snapshot Manager-architectuur** 

## <a name="support-for-multiple-volume-types"></a>Ondersteuning voor meerdere volumetypen
U kunt gebruiken Hallo StorSimple Snapshot Manager tooconfigure en back-up Hallo typen volumes te volgen: 

* **Basisvolumes** – een standaardvolume wordt één partitie op een standaardschijf zijn. 
* **Eenvoudige volumes** – een eenvoudig volume is een dynamisch volume met de schijfruimte van één dynamische schijf. Een eenvoudig volume bestaat uit één regio op een schijf of meerdere regio's die zijn gekoppeld op Hallo dezelfde schijf. (U kunt eenvoudige volumes maken alleen op dynamische schijven.) Eenvoudige volumes zijn niet fouttolerant.
* **Dynamische volumes** – een dynamisch volume is een volume dat is gemaakt op een dynamische schijf. Dynamische schijven gebruiken een database tootrack informatie over de volumes die zijn opgenomen op de dynamische schijven op een computer. 
* **Dynamische volumes met mirroring** – dynamische volumes met mirroring zijn gebouwd op Hallo RAID 1-architectuur. Met RAID 1 identieke gegevens op twee of meer schijf, het opstellen van een gespiegelde set geschreven. Een leesaanvraag kan vervolgens worden verwerkt door een schijf die Hallo bevat gegevens.
* **Gedeelde clustervolumes** – met gedeelde clustervolumes (CSV's), meerdere knooppunten in een failovercluster kunnen tegelijkertijd gelezen of geschreven toohello dezelfde schijf. Failover van één knooppunt tooanother knooppunt kunt snel plaatsvinden zonder een wijziging in eigendom van het station of koppelen, ontkoppelen en verwijderen van een volume. 

> [!IMPORTANT]
> Niet door elkaar op CSV's en niet-CSV in Hallo dezelfde momentopname. De combinatie van CSV's en niet-CSV in een momentopname wordt niet ondersteund. 
> 
> 

U kunt het StorSimple Snapshot Manager toorestore hele volume groepen gebruiken of afzonderlijke volumes klonen en afzonderlijke bestanden te herstellen.

* [Volumes en volume-groepen](#volumes-and-volume-groups) 
* [Back-uptypen en back-upbeleid](#backup-types-and-backup-policies) 

Voor meer informatie over StorSimple Snapshot Manager-functies en hoe toouse die ze zien [StorSimple Snapshot Manager-gebruikersinterface](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Volumes en volume-groepen
Met StorSimple Snapshot Manager volumes maken en deze vervolgens in volume groepen te configureren. 

StorSimple Snapshot Manager maakt gebruik van volume groepen toocreate back-ups die toepassing consistent zijn. Consistentie van de toepassing bestaat als alle bestanden bijbehorende en de databases zijn gesynchroniseerd en Hallo true status van een toepassing op een bepaald punt in tijd weer. Volume-groepen (die ook wel bekend als zijn *consistentie groepen*) Hallo basis vormen van een back-up of herstellen van de taak.

Volume-groepen zijn niet hetzelfde als volumecontainers Hallo. Een volumecontainer bevat een of meer volumes die delen van een cloud-opslagaccount en andere kenmerken, zoals versleuteling en bandbreedte. Een container voor één volume kan van de StorSimple-volumes too256 thin provisioning bevatten. Voor meer informatie over volumecontainers gaat te[beheren van uw volumecontainers](storsimple-manage-volume-containers.md). Volume-groepen zijn verzamelingen van volumes die u de back-upbewerkingen toofacilitate configureert. Als u twee volumes die eigendom zijn toodifferent volumecontainers, plaats deze in een groep één volume en maak vervolgens een back-upbeleid voor de groep volume selecteert, elk volume wordt een back-up in Hallo relevante volumecontainer, met behulp van de juiste opslag Hallo account.

> [!NOTE]
> Alle volumes in een groep volume moeten afkomstig zijn van een serviceprovider één cloud.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integratie met Windows Volume Shadow Copy-Service
StorSimple Snapshot Manager maakt gebruik van Hallo Windows Volume Shadow Copy Service (VSS) toocapture toepassingsconsistente gegevens. VSS zorgt voor een toepassing consistente door te communiceren met de VSS-bewuste toepassingen toocoordinate Hallo maken van incrementele momentopnamen. VSS zorgt ervoor dat toepassingen Hallo tijdelijk niet actief of quiescent, wanneer momentopnamen worden gemaakt. 

Hallo StorSimple Snapshot Manager-implementatie van VSS werkt met SQL Server- en algemene NTFS-volumes. Hallo-proces is als volgt: 

1. Een aanvrager die normaal gesproken een gegevensbeheer en de oplossing voor gegevensbeveiliging (zoals StorSimple Snapshot Manager) of een back-uptoepassing, roept VSS en vraagt de toogather informatie uit Hallo writer software in de doeltoepassing Hallo.
2. Contactpersonen VSS Hallo writer onderdeel tooretrieve een beschrijving van de gegevens Hallo. Hallo writer retourneert Hallo beschrijving van Hallo gegevens toobe back-up gemaakt. 
3. VSS signalen Hallo tooprepare hello schrijftoepassing uit voor back-up. Hallo writer Hallo worden gegevens voorbereid voor back-up door te voeren van geopende transacties voor het bijwerken van transactielogboeken, enzovoort, en wordt vervolgens VSS.
4. VSS geïnstrueerd Hallo writer tootemporarily stop Hallo toepassingsgegevens worden opgeslagen en zorg ervoor dat er geen gegevens toohello volume wordt geschreven terwijl Hallo schaduwkopie is gemaakt. Deze stap zorgt ervoor dat de consistentie van de gegevens, en wordt niet meer dan 60 seconden.
5. VSS geïnstrueerd Hallo provider toocreate Hallo-schaduwkopie. Providers, wat kunnen software of hardware-gebaseerde, beheren Hallo volumes die momenteel worden uitgevoerd en maken van schaduwkopieën van deze op aanvraag. Hallo provider Hallo schaduwkopie maakt en VSS waarschuwt wanneer dit is voltooid.
6. VSS contactpersonen Hallo writer toonotify Hallo toepassing die i/o kunt hervatten en ook tooconfirm i/o met succes is onderbroken tijdens shadow kopiëren maken. 
7. Als Hallo kopie voltooid is, VSS Hallo kopie van locatie toohello aanvrager retourneert. 
8. Als de gegevens zijn geschreven terwijl Hallo schaduwkopie is gemaakt, worden back-up Hallo inconsistent worden. VSS Hallo schaduwkopie wordt verwijderd en ontvangt een melding Hallo aanvrager. Hallo aanvrager kunt Hallo back-upproces automatisch te herhalen of Hallo beheerder tooretry melden op een later tijdstip.

Zie Hallo volgende afbeelding.

![VSS-proces](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Windows Volume Shadow Copy-Service verwerken** 

## <a name="backup-types-and-backup-policies"></a>Back-uptypen en back-upbeleid
Met StorSimple Snapshot Manager kunt u back-up van gegevens en lokaal en in de cloud Hallo opslaan. U kunt onmiddellijk StorSimple Snapshot Manager tooback upgegevens gebruiken of kunt u een back-upbeleid toocreate een planning voor het automatisch maken van back-ups. Back-upbeleid kunnen u ook toospecify hoeveel momentopnamen behouden blijft. 

### <a name="backup-types"></a>Back-uptypen
U kunt StorSimple Snapshot Manager toocreate Hallo typen back-ups te volgen:

* **Lokale momentopnamen** : lokale momentopnamen zijn punt in tijd kopieën van volumegegevens die zijn opgeslagen op Hallo StorSimple-apparaat. Normaal gesproken worden deze type back-up gemaakt en snel worden hersteld. Net als een lokale back-up, kunt u een lokale momentopname gebruiken.
* **Momentopnamen cloud** – cloudmomentopnamen punt in tijd kopieën van volumegegevens die zijn opgeslagen in de cloud Hallo zijn. Een cloudmomentopname is gelijk tooa momentopname op een andere, externe opslagsysteem gerepliceerd. Cloudmomentopnamen zijn bijzonder nuttig voor herstel na noodgevallen.

### <a name="on-demand-and-scheduled-backups"></a>Op aanvraag en geplande back-ups
Met StorSimple Snapshot Manager kunt u een eenmalige back-toobe onmiddellijk gemaakt start, of kunt u een back-upbeleid tooschedule periodiek back-upbewerkingen.

Een back-upbeleid is een set van geautomatiseerde regels die u regelmatig back-ups tooschedule kunt gebruiken. Een back-upbeleid kunt u toodefine Hallo frequentie en parameters voor het maken van momentopnamen van een groep specifieke volume. U kunt beleidsregels toospecify begin- en verloopdatum datums, tijden, frequentie en vereisten voor de bewaarperiode van lokale en cloud worden opgeslagen. Een beleid wordt toegepast onmiddellijk nadat u deze variabele definiëren. 

U kunt StorSimple Snapshot Manager tooconfigure gebruiken of back-upbeleid op elk gewenst moment opnieuw configureren. 

U de volgende informatie voor elke back-upbeleid die u maakt Hallo configureren:

* **Naam** – Hallo unieke naam van Hallo back-upbeleid geselecteerd.
* **Type** – Hallo type back-upbeleid; lokale momentopname of cloudmomentopname.
* **Volume groep** – Hallo volume groep toowhich Hallo geselecteerd back-upbeleid is toegewezen.
* **Bewaartermijn** : het aantal back-ups tooretain Hallo. Als u het selectievakje Hallo **alle** vak alle back-ups worden bewaard totdat Hallo kunt u het maximum aantal back-ups per volume is bereikt, op welk punt Hallo beleid mislukken en er een foutbericht weergegeven. U kunt ook opgeven dat een aantal back-ups tooretain (tussen 1 en 64).
* **Datum** – Hallo datum waarop de back-upbeleid Hallo is gemaakt.

Voor informatie over het configureren van de back-upbeleid gaat te[gebruik StorSimple Snapshot Manager toocreate en beheren van back-upbeleid](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Back-uptaak bewaking en beheer
U kunt gebruiken Hallo StorSimple Snapshot Manager toomonitor en toekomstige geplande en voltooide back-uptaken beheren. Daarnaast biedt StorSimple Snapshot Manager een catalogus van back-ups too64 voltooid. U kunt gebruiken Hallo catalogus toofind en volumes of afzonderlijke bestanden te herstellen. 

Voor informatie over het controleren van de back-uptaken gaat te[gebruik StorSimple Snapshot Manager tooview en beheren van back-uptaken](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple Snapshot Manager tooadminister met uw StorSimple-oplossing](storsimple-snapshot-manager-admin.md).
* Download [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220).

