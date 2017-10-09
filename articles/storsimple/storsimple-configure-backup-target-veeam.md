---
title: aaaStorSimple 8000 series als back-updoel met Veeam | Microsoft Docs
description: Hallo StorSimple back-updoel configuratie met Veeam beschreven.
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a>StorSimple als een back-updoel met Veeam

## <a name="overview"></a>Overzicht

Azure StorSimple is een hybride cloud-opslag-oplossing van Microsoft. Hallo complexiteit van de exponentiële Gegevensgroei adressen StorSimple met behulp van een Azure Storage-account als een uitbreiding van Hallo on-premises oplossing en automatisch lagen gegevens voor lokale opslag en cloud-opslag.

In dit artikel wordt besproken StorSimple-integratie met Veeam en aanbevolen procedures voor het integreren van beide oplossingen. We ook maken aanbevelingen voor hoe tooset up Veeam toobest integreren met StorSimple. Aanbevolen procedures voor tooVeeam, back-architecten en administrators voor de beste manier tooset hello Veeam toomeet afzonderlijke back-upvereisten en service level agreements (Sla's) uit te stellen.

Hoewel we configuratiestappen en belangrijkste concepten illustreren, is in dit artikel geen stapsgewijze handleiding voor een configuratie of de installatie. We gaan ervan uit dat Hallo basic onderdelen en infrastructuur zijn en op gereed toosupport Hallo-concepten die worden beschreven.

### <a name="who-should-read-this"></a>Wie is dit?

Hallo-informatie in dit artikel is het nuttigst toobackup beheerders, opslagbeheerders en storage-architecten die kennis van opslag, Windows Server 2012 R2, Ethernet, cloudservices en Veeam hebben.

### <a name="supported-versions"></a>Ondersteunde versies

-   Veeam 9 en latere versies
-   [StorSimple Update 3 en hoger](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Waarom StorSimple als een back-updoel?

StorSimple is een goede keuze voor een back-updoel omdat:

-   Biedt standaard, lokale opslag voor back-uptoepassingen toouse als een snelle back-up bestemming, zonder deze te wijzigen. U kunt ook StorSimple gebruiken voor een snel herstel van recente back-ups.
-   De cloud tiering is volledig geïntegreerd met een Azure-cloud-opslag account toouse rendabele opslag voor Azure.
-   Het biedt automatisch offsite-opslag voor herstel na noodgevallen.


## <a name="key-concepts"></a>Belangrijkste concepten

Frequentie van wijziging en groei capaciteitsbehoeften is net als bij een opslagoplossing, een zorgvuldige evaluatie van opslagprestaties Hallo-oplossing, sla's, kritieke toosuccess. Hallo hoofdonderwerp is dat door de introductie van een cloudlaag, uw toohello toegangstijden en doorvoercapaciteit cloud fundamentele rol spelen in Hallo mogelijkheid van StorSimple toodo de taak.

StorSimple is ontworpen tooprovide opslag tooapplications die worden uitgevoerd op een goed gedefinieerde werkset van gegevens (hot gegevens). In dit model Hallo werkset van gegevens wordt opgeslagen op de lokale lagen Hallo en hello resterende vrije, koude/gearchiveerd gegevensset is gelaagde toohello cloud. Dit model wordt weergegeven in de volgende afbeelding Hallo. Hallo bijna platte groen regel staat Hallo-gegevens die zijn opgeslagen op de lokale lagen Hallo van Hallo StorSimple-apparaat. Hallo vertegenwoordigt rode lijn Hallo totale hoeveelheid gegevens die zijn opgeslagen op Hallo StorSimple-oplossing in alle lagen. Hallo ruimte tussen Hallo platte groen lijn- en Hallo exponentiële rode vertegenwoordigt totale hoeveelheid gegevens die zijn opgeslagen in de cloud Hallo Hallo.

**StorSimple tiering**
![lagen StorSimple-diagram](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)

Met deze architectuur rekening zult u merken dat StorSimple ideaal toooperate als een back-doel is. U kunt StorSimple om te gebruiken:

-   De meest voorkomende herstelacties uitvoeren vanaf de lokale werkset Hallo van gegevens.
-   Gebruik Hallo cloud voor noodherstel offsite en oudere gegevens waar herstelacties minder frequente zijn.

## <a name="storsimple-benefits"></a>Voordelen van StorSimple

StorSimple biedt een on-premises-oplossing is volledig geïntegreerd met Microsoft Azure, door gebruik te maken van naadloze toegang tot tooon-premises en cloudopslag.

StorSimple maakt gebruik van automatische lagen tussen Hallo on-premises apparaat met SSD-apparaat (SSD) en serial attached SCSI (SAS)-opslag en Azure Storage. Automatische lagen houdt wordt vaak gebruikte gegevens die lokaal op Hallo SSD- en SAS-lagen. Deze verplaatst minder vaak gebruikte gegevens tooAzure opslag.

StorSimple biedt deze voordelen:

-   Unieke gegevensontdubbeling en compressie-algoritmen die gebruikmaken van Hallo cloud tooachieve ongekende Ontdubbeling niveaus
-   Hoge beschikbaarheid
-   Geo-replicatie met behulp van Azure geo-replicatie
-   Integratie van Azure
-   Hallo cloud gegevensversleuteling
-   Verbeterde noodherstel en naleving

Hoewel StorSimple fundamenteel geeft de twee belangrijkste implementatiescenario's (back-updoel primaire en secundaire back-updoel), is het een gewone, apparaat met blokopslag. StorSimple alle Hallo compressie en Ontdubbeling. Naadloos verzendt en haalt gegevens tussen Hallo cloud en de toepassing hello en bestandssysteem.

Zie voor meer informatie over StorSimple [StorSimple 8000-serie: hybride cloud opslagoplossing](storsimple-overview.md). Bovendien kunt u bekijken Hallo [technische specificaties van StorSimple 8000 serie](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> Met behulp van een StorSimple wordt apparaat als een back-updoel alleen ondersteund voor StorSimple 8000 Update 3 en hoger.

## <a name="architecture-overview"></a>Overzicht van de architectuur

Hallo bevatten volgende tabellen Hallo apparaat model-naar-initiële architectuurrichtlijnen.

**StorSimple-capaciteit voor lokale en cloud-opslag**

| Opslagcapaciteit | 8100 | 8600 |
|---|---|---|
| Capaciteit van de lokale opslag | &lt;10 TiB\*  | &lt;20 TiB\*  |
| Cloudopslagcapaciteit | &gt;200 TiB\* | &gt;500 TiB\* |

\*Grootte van de opslagruimte wordt ervan uitgegaan dat er geen gegevensontdubbeling of compressie.

**StorSimple capaciteitswaarden voor de primaire en secundaire back-ups**

| Back-scenario  | Capaciteit van de lokale opslag  | Cloudopslagcapaciteit  |
|---|---|---|
| Primaire back-up  | Recente back-ups die zijn opgeslagen op lokale opslag voor snel herstel toomeet beoogd herstelpunt (RPO) | Back-upgeschiedenis (RPO) past in cloudcapaciteit |
| Secundaire back-up | Secundaire kopie van de back-upgegevens kan worden opgeslagen in de cloudcapaciteit  | N.v.t.  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple als primaire back-doel

In dit scenario vindt StorSimple-volumes toohello back-uptoepassing als enige Hallo-opslagplaats voor back-ups. Hallo volgende afbeelding toont de oplossingsarchitectuur van een waarin alle back-ups gebruik StorSimple volumes voor back-ups en herstelbewerkingen gelaagde.

![StorSimple als een primaire back-updoel logisch diagram](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Primaire doel van de back-up logische stappen

1.  Hallo back-upserver contactpersonen Hallo doel back-upagent en Hallo backup-agent verzendt gegevens toohello back-upserver.
2.  back-upserver Hallo schrijft gegevens toohello StorSimple gelaagde volumes.
3.  back-upserver Hallo werkt Hallo catalogusdatabase en vervolgens heeft voltooid Hallo back-uptaak.
4.  Een script momentopname activeert Hallo StorSimple cloud snapshot manager (start of verwijderen).
5.  Hallo back-upserver worden verlopen back-ups op basis van een bewaarbeleid verwijderd.

### <a name="primary-target-restore-logical-steps"></a>Primaire doel terugzetten logische stappen

1.  back-upserver Hallo start Hallo relevante gegevens terugzetten vanuit Hallo-opslagplaats.
2.  back-upagent Hallo ontvangt gegevens van Hallo van Hallo back-upserver.
3.  back-upserver Hallo voltooit Hallo hersteltaak.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple als secundaire back-doel

In dit scenario worden StorSimple-volumes voornamelijk gebruikt voor lange bewaartermijn en archiveren.

Hallo volgende afbeelding toont een architectuur in welke eerste back-ups en hersteld doelvolume hoge prestaties. Deze back-ups worden gekopieerd en gearchiveerde tooa StorSimple gelaagd volume op een vast schema.

Het is belangrijk toosize het volume met hoge prestaties, zodat uw bewaren capaciteit en prestaties beleidsvereisten kan verwerken.

![StorSimple als een secundaire back-updoel logisch diagram](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Back-up logische stappen secundaire doel

1.  Hallo back-upserver contactpersonen Hallo doel back-upagent en Hallo backup-agent verzendt gegevens toohello back-upserver.
2.  back-upserver Hallo schrijft toohigh prestaties gegevensopslag.
3.  back-upserver Hallo werkt Hallo catalogusdatabase en vervolgens heeft voltooid Hallo back-uptaak.
4.  back-upserver Hallo tooStorSimple van back-ups op basis van een bewaarbeleid opgehaald.
5.  Een script momentopname activeert Hallo StorSimple cloud snapshot manager (start of verwijderen).
6.  Hallo back-upserver worden verlopen back-ups op basis van een bewaarbeleid verwijderd.

### <a name="secondary-target-restore-logical-steps"></a>Secundaire doel terugzetten logische stappen

1.  back-upserver Hallo start Hallo relevante gegevens terugzetten vanuit Hallo-opslagplaats.
2.  back-upagent Hallo ontvangt gegevens van Hallo van Hallo back-upserver.
3.  back-upserver Hallo voltooit Hallo hersteltaak.

## <a name="deploy-hello-solution"></a>Hallo-oplossing implementeren

Hallo-oplossing implementeren, moet drie stappen:

1. Bereid Hallo-netwerkinfrastructuur.
2. Uw StorSimple-apparaat implementeren als een back-doel.
3. Veeam implementeren.

Elke stap wordt uitgebreid beschreven in Hallo uit te voeren.

### <a name="set-up-hello-network"></a>Hallo-netwerk instellen

Omdat StorSimple een oplossing die is geïntegreerd met hello Azure-cloud is, moet StorSimple een actieve en functioneel verbinding toohello Azure-cloud. Deze verbinding wordt gebruikt voor bewerkingen, zoals cloudmomentopnamen, beheren, en metagegevens overbrengen en tootier oudere, minder gebruikte gegevens tooAzure cloud-opslag.

Voor Hallo oplossing tooperform optimaal, raden we aan dat u deze netwerken aanbevolen procedures volgt:

-   Hallo-koppeling die verbinding maakt van uw StorSimple-lagen tooAzure moet voldoen aan de bandbreedtevereisten van uw. Dit bereiken door toe te passen Hallo nodig Quality of Service (QoS) niveau tooyour infrastructuur switches toomatch RPO- en herstelinstellingen tijd objective (RTO) Sla's.
-   Maximale toegangslatentie van Azure Blob-opslag moet ongeveer 80 ms.

### <a name="deploy-storsimple"></a>StorSimple implementeren

Zie voor stapsgewijze instructies voor StorSimple-implementatie, [uw on-premises StorSimple-apparaat implementeren](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-veeam"></a>Veeam implementeren

Zie voor aanbevolen procedures voor de Veeam-installatie, [Veeam back-up- en aanbevolen procedures voor replicatie](https://bp.veeam.expert/), en lees de gebruikershandleiding Hallo op [Veeam Help en ondersteuning (technische documentatie)](https://www.veeam.com/documentation-guides-datasheets.html).

## <a name="set-up-hello-solution"></a>Hallo-oplossing instellen

In deze sectie ziet u configuratievoorbeelden. Hallo illustreren volgende voorbeelden en aanbevelingen Hallo meest elementaire en fundamentele implementatie. Deze implementatie kan niet van toepassing rechtstreeks tooyour specifieke back-vereisten.

### <a name="set-up-storsimple"></a>StorSimple instellen

| Implementatietaken StorSimple  | Aanvullende opmerkingen |
|---|---|
| Uw on-premises StorSimple-apparaat implementeren. | Ondersteunde versies: Update 3 en latere versies. |
| Back-updoel Hallo inschakelen. | Deze opdrachten tooturn op gebruiken of back-updoel modus en de status van de tooget uitschakelen. Zie voor meer informatie [tooa StorSimple-apparaat op afstand verbinding maken](storsimple-remote-connect.md).</br> tooturn op back-upmodus: `Set-HCSBackupApplianceMode -enable`. </br> tooturn uit back-upmodus: `Set-HCSBackupApplianceMode -disable`. </br> tooget hello huidige status van de instellingen van de back-upmodus: `Get-HCSBackupApplianceMode`. |
| Maak een algemene volumecontainer voor het volume waarop Hallo back-gegevens worden opgeslagen. Alle gegevens in een volumecontainer is ontdubbeld. | StorSimple volumecontainers definiëren Ontdubbeling domeinen.  |
| StorSimple-volumes maken. | Volumes met grootten maken als sluiten toohello verwacht gebruik zo mogelijk, omdat de grootte van volume is van invloed op een momentopname van de opgegeven tijdsduur cloud. Voor informatie over het toosize een volume meer informatie over [bewaarbeleidsregels](#retention-policies).</br> </br> Gebruik StorSimple gelaagde volumes en selecteer Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje. </br> Gebruik alleen lokaal vastgemaakte volumes wordt niet ondersteund. |
| Een unieke StorSimple-back-upbeleid voor alle Hallo back-updoel volumes maken. | Een StorSimple-back-upbeleid definieert Hallo volume consistentie groep. |
| Hallo schema uitschakelen wanneer Hallo momentopnamen verlopen. | Momentopnamen worden geactiveerd als een na verwerking bewerking. |

### <a name="set-up-hello-host-backup-server-storage"></a>Hallo host back-upserver opslag instellen

Hallo host back-upserver van opslag op basis van toothese richtlijnen instellen:  

- Gebruik geen spanned volumes (gemaakt door Windows Schijfbeheer). Spanned volumes worden niet ondersteund.
- De volumes formatteren met NTFS met clustergrootte van 64 KB.
- Hallo StorSimple-volumes toewijzen rechtstreeks toohello Veeam server.
    - ISCSI-gebruiken voor fysieke servers.


## <a name="best-practices-for-storsimple-and-veeam"></a>Aanbevolen procedures voor StorSimple en Veeam

Instellen van uw oplossing op basis van toohello richtlijnen in Hallo na enkele secties.

### <a name="operating-system-best-practices"></a>Aanbevolen procedures van besturingssysteem

-   Windows Server-versleuteling en Ontdubbeling voor Hallo NTFS-bestandssysteem uitgeschakeld.
-   Schakel defragmentatie van Windows Server op Hallo StorSimple-volumes.
-   Windows Server op Hallo StorSimple-volumes te indexeren uitschakelen.
-   Een antivirusprogramma scan uitvoeren op de bronhost hello (niet tegen Hallo StorSimple-volumes).
-   Hallo standaard uitschakelen [onderhoud van Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Taakbeheer. Dit in een van de volgende manieren Hallo doen:
    - Hallo onderhoud configurator in Windows Taakplanner uitschakelen.
    - Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) van Windows Sysinternals. Na het downloaden van PsExec Voer Windows PowerShell als beheerder en typ:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Aanbevolen procedures voor StorSimple

-   Zorg dat Hallo StorSimple-apparaat is bijgewerkt[Update 3 of hoger](storsimple-install-update-3.md).
-   Isoleren iSCSI- en cloud-verkeer. Speciale iSCSI-verbindingen voor verkeer tussen de back-upserver van StorSimple en hello gebruiken.
-   Zorg ervoor dat uw StorSimple-apparaat een toegewezen back-doel is. Gemengde werkbelastingen worden niet ondersteund omdat ze invloed heeft op uw RTO en RPO.

### <a name="veeam-best-practices"></a>Aanbevolen procedures voor Veeam

-   Hallo Veeam database moet lokale toohello server en bevindt zich niet op een StorSimple-volume.
-   Voor herstel na noodgevallen, back-up Hallo Veeam database op een StorSimple-volume.
-   Wij ondersteunen Veeam volledige en incrementele back-ups voor deze oplossing. Het is raadzaam dat u geen synthetische en differentiële back-ups gebruikt.
-   Back-upgegevensbestanden moeten alleen Hallo gegevens voor een specifieke taak bevatten. Bijvoorbeeld geen media worden toegevoegd via verschillende taken zijn toegestaan.
-   Taak verificatie uitschakelen. Indien nodig, moet verificatie na de meest recente back-uptaak Hallo worden gepland. Het is belangrijk toounderstand dat deze taak is van invloed op uw back-upvenster.
-   Schakel voorafgaande mediatoewijzing.
-   Zorg ervoor dat de parallelle verwerking is ingeschakeld.
-   Compressie uitschakelt.
-   Schakel Ontdubbeling op Hallo back-uptaak.
-   Instellen van optimalisatie te**LAN doel**.
-   Schakel **maken active volledige back-up** (elke 2 weken).
-   Instellen op Hallo back-opslagplaats, **gebruik per VM-back-upbestanden**.
-   Stel **gebruik van meerdere uploaden streams per taak** te**8** (maximaal 16 is toegestaan). Wijzig dit aantal omhoog of omlaag op basis van CPU-gebruik op Hallo StorSimple-apparaat.

## <a name="retention-policies"></a>Bewaarbeleid

Een van de meest voorkomende bewaren van back-up Hallo-beleidstypen is een beleid opa vader en zoon (algemene). Een incrementele back-up dagelijks wordt uitgevoerd in een algemene-beleid en volledige back-ups wekelijkse en maandelijkse klaar bent. Dit beleid resulteert in zes StorSimple gelaagde volumes: één volume bevat Hallo wekelijkse, maandelijkse en jaarlijkse volledige back-ups; Hallo opslaan andere vijf volumes dagelijkse incrementele back-ups.

In Hallo voorbeeld te volgen, gebruiken we een algemene worden gedraaid. Hallo-voorbeeld wordt ervan uitgegaan dat Hallo volgende:

-   Niet-ontdubbelde of gecomprimeerde gegevens worden gebruikt.
-   Volledige back-ups zijn 1 TiB.
-   Dagelijkse incrementele back-ups zijn 500 GiB.
-   Vier wekelijkse back-ups worden gedurende een maand bewaard.
-   Twaalf maandelijkse back-ups worden van een jaar bewaard.
-   Een jaarlijkse back-up is 10 jaar bewaard.

Op basis van Hallo vóór het uitgangspunten, maak een 26-TiB StorSimple gelaagd volume voor Hallo maandelijkse en jaarlijkse volledige back-ups. Maken van een 5-TiB StorSimple gelaagd volume voor elk Hallo incrementele dagelijkse back-ups.

| Back-uptype bewaren | Grootte (TiB) | Algemene vermenigvuldiger\* | Totale capaciteit (TiB)  |
|---|---|---|---|
| Wekelijkse volledige | 1 | 4  | 4 |
| Dagelijkse incrementele | 0.5 | 20 (cycli gelijk aantal weken per maand) | 12 (2 voor extra quotum) |
| Maandelijks volledige | 1 | 12 | 12 |
| Jaarlijks volledige | 1  | 10 | 10 |
| Algemene vereisten |   | 38 |   |
| Extra quota  | 4  |   | 42 totale algemene vereisten  |
\*Hallo algemene vermenigvuldiger is Hallo aantal exemplaren van de u nodig tooprotect hebt en de vereisten van uw back-upbeleid voor toomeet behouden.

## <a name="set-up-veeam-storage"></a>Veeam opslag instellen

### <a name="tooset-up-veeam-storage"></a>tooset Veeam opslag configureren

1.  In hello Veeam back-up- en replicatie-console in **opslagplaats extra**, gaat u te**back-upinfrastructuur**. Met de rechtermuisknop op **back-up-opslagplaatsen**, en selecteer vervolgens **back-up-opslagplaats toevoegen**.

    ![Beheerconsole Veeam, back-opslagplaats pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  In Hallo **nieuwe back-up-opslagplaats** dialoogvenster Voer een naam en beschrijving voor Hallo-opslagplaats. Selecteer **volgende**.

    ![Veeam management console, naam en beschrijving pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  Selecteer Hallo type **Microsoft Windows server**. Hallo Veeam server selecteren. Selecteer **volgende**.

    ![Veeam-beheerconsole, Selecteer type back-opslagplaats](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  toospecify **locatie**, bladeren en Hallo volume te selecteren. Selecteer Hallo **maximum aantal gelijktijdige taken te beperken:** selectievakje en set Hallo waarde te**4**. Dit zorgt ervoor dat slechts vier virtuele schijven worden verwerkt gelijktijdig terwijl elke virtuele machine (VM) wordt verwerkt. Selecteer Hallo **Geavanceerd** knop.

    ![Veeam-beheerconsole, selecteer volume](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  In Hallo **opslag compatibiliteitsinstellingen** dialoogvenster, selecteer Hallo **gebruik per VM-back-upbestanden** selectievakje.

    ![Veeam management console compatibiliteitsinstellingen voor opslag](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  In Hallo **nieuwe back-up-opslagplaats** dialoogvenster, selecteer Hallo **vPower NFS-service op Hallo mount-server (aanbevolen) inschakelen** selectievakje. Selecteer **volgende**.

    ![Beheerconsole Veeam, back-opslagplaats pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  Hallo-instellingen bekijken en selecteer vervolgens **volgende**.

    ![Beheerconsole Veeam, back-opslagplaats pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    Een opslagplaats is toohello Veeam server toegevoegd.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>StorSimple instellen als primaire back-doel

> [!IMPORTANT]
> Gegevens terugzetten vanuit een back-up die gelaagde toohello cloud is vindt plaats met een snelheid van de cloud.

Hallo toont volgende afbeelding Hallo toewijzing van een typische volume tooa back-uptaak. In dit geval alle Hallo wekelijkse back-ups toohello zaterdag volledige schijf toewijzen en incrementele back-ups Hallo tooMonday vrijdag incrementele schijven worden toegewezen. Alle Hallo back-ups en herstelbewerkingen zijn van een StorSimple gelaagd volume.

![Primaire back-updoel configuratie logisch diagram](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>StorSimple als primaire back-updoel algemene voorbeeld plannen

Hier volgt een voorbeeld van een algemene rotatieschema vier weken, maandelijkse en jaarlijkse:

| Type frequentie/back-up | Volledig | Incrementele (dagen 1-5)  |   
|---|---|---|
| Wekelijks (weken 1-4) | Zaterdag | Maandag tot vrijdag |
| Maandelijks  | Zaterdag  |   |
| Jaarlijks | Zaterdag  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a>StorSimple-volumes tooa Veeam back-uptaak toewijzen

Primaire back-updoel scenario voor een dagelijkse taak te maken met uw primaire Veeam StorSimple-volume. Voor een scenario secundaire back-updoel een dagelijkse taak te maken met Direct gekoppelde opslag (DAS), Network Attached Storage (NAS) of net een Bunch van schijven (JBOD)-opslag.

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a>tooassign StorSimple-volumes tooa Veeam back-uptaak

1.  Selecteer in de hello Veeam back-up- en replicatie console **back-up- en replicatie**. Met de rechtermuisknop op **back-up**, en selecteer vervolgens **VMware** of **Hyper-V**, afhankelijk van uw omgeving.

    ![Beheerconsole Veeam, nieuwe back-uptaak](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  In Hallo **nieuwe back-uptaak** dialoogvenster Voer een naam en beschrijving voor dagelijkse back-uptaak Hallo.

    ![Beheerconsole Veeam, nieuwe back-uptaak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  Selecteer een virtuele machine tooback tot.

    ![Beheerconsole Veeam, nieuwe back-uptaak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  Selecteer Hallo gewenste waarden voor **back-up proxy** en **back-up opslagplaats**. Selecteer een waarde voor **terugzetten tookeep beheerpunten op schijf** opslag op basis van toohello RPO en RTO definities voor uw omgeving op lokaal verbonden. Selecteer **geavanceerde**.

    ![Beheerconsole Veeam, nieuwe back-uptaak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. In Hallo **geavanceerde instellingen** op Hallo van het dialoogvenster **back-up** tabblad **incrementele**. Zorg dat Hallo **periodiek synthetische volledige back-ups maken** selectievakje is uitgeschakeld. Selecteer Hallo **periodiek active volledige back-ups maken** selectievakje. Onder **Active volledige back-up**, selecteer Hallo **wekelijks op geselecteerde dagen** selectievakje voor zaterdag.

    ![Beheerconsole voor Veeam nieuwe back-uptaak geavanceerde instellingenpagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. Op Hallo **opslag** tabblad, zorg ervoor dat Hallo **inline-gegevensontdubbeling inschakelen** selectievakje is uitgeschakeld. Selecteer Hallo **uitsluiten wisselen bestandsblokken** selectievakje in en selecteer Hallo **uitsluiten verwijderd bestandsblokken** selectievakje. Stel **compressieniveau** te**geen**. Voor taakverdeling prestaties en Ontdubbeling ingesteld **opslagoptimalisatie** te**LAN doel**. Selecteer **OK**.

    ![Beheerconsole voor Veeam nieuwe back-uptaak geavanceerde instellingenpagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    Zie voor meer informatie over instellingen voor gegevensontdubbeling en compressie van Veeam [gegevenscompressie en Ontdubbeling](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).

7.  In Hallo **bewerken back-uptaak** in het dialoogvenster kunt u Hallo **toepassingsgevoelige-verwerking inschakelen** selectievakje (optioneel).

    ![Beheerconsole Veeam, nieuwe back-uptaak Gast verwerking pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  Hallo planning toorun eenmaal per dag, die kunt u tegelijkertijd ingesteld.

    ![Beheerconsole Veeam, nieuwe pagina van de back-uptaak plannen](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>StorSimple instellen als een secundaire back-doel

> [!NOTE]
> Gegevens terugzetten vanuit een back-up die gelaagde toohello cloud is optreden met een snelheid van de cloud.

In dit model, moet u een media (met uitzondering van StorSimple) opslag tooserve hebben als een tijdelijke cache. U kunt bijvoorbeeld een redundante matrix van onafhankelijke schijven (RAID) ruimte op volume tooaccommodate, input/output (I/O) en bandbreedte. U wordt aangeraden met behulp van RAID-5, 50 en 10.

Hallo volgende afbeelding toont een typische op korte termijn bewaren lokale (toohello server)-volumes en langdurige bewaarperiode archief volumes. In dit scenario alle back-ups uitgevoerd op Hallo lokale (toohello server) RAID-volume. Deze back-ups regelmatig worden gedupliceerd en gearchiveerd tooan archief volume. Het is belangrijk toosize (toohello server) van uw lokale RAID-volume dat de korte termijn capaciteit en prestaties vereisten voor de bewaarperiode kan verwerken.

![StorSimple als secundaire back-updoel logisch diagram](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple als een voorbeeld van een secundaire back-updoel algemene

Hallo volgende tabel toont hoe tooset up toorun back-ups op Hallo lokale en StorSimple-schijven. Bevat capaciteitsvereisten voor afzonderlijke en de totale.

| Type back-up en retentie | Geconfigureerde opslag | Grootte (TiB) | Algemene vermenigvuldiger | Totale capaciteit\* (TiB) |
|---|---|---|---|---|
| Week 1 (volledige en incrementele) |Lokale schijf (korte)| 1 | 1 | 1 |
| StorSimple weken 2-4 |StorSimple schijf (op lange termijn) | 1 | 4 | 4 |
| Maandelijks volledige |StorSimple schijf (op lange termijn) | 1 | 12 | 12 |
| Jaarlijks volledige |StorSimple schijf (op lange termijn) | 1 | 1 | 1 |
|Vereiste grootte van algemene volumes |  |  |  | 18*|
\*Totale capaciteit omvat 17 TiB van StorSimple-schijven en 1 TiB van lokale RAID-volume.


### <a name="gfs-example-schedule"></a>Algemene voorbeeld planning

Algemene rotatie wekelijkse, maandelijkse en jaarlijkse planning

| Week | Volledig | Incrementele dag 1 | Incrementele dag 2 | Incrementele dag 3 | Incrementele dag 4 | Incrementele dag 5 |
|---|---|---|---|---|---|---|
| 1 week | Lokale RAID-volume  | Lokale RAID-volume | Lokale RAID-volume | Lokale RAID-volume | Lokale RAID-volume | Lokale RAID-volume |
| Week 2 | StorSimple weken 2-4 |   |   |   |   |   |
| Week 3 | StorSimple weken 2-4 |   |   |   |   |   |
| Week 4 | StorSimple weken 2-4 |   |   |   |   |   |
| Maandelijks | Maandelijks StorSimple |   |   |   |   |   |
| Jaarlijks | Jaarlijks StorSimple  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a>Taak voor het kopiëren tooa Veeam in StorSimple-volumes toewijzen

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a>tooassign StorSimple-volumes tooa Veeam taak kopiëren

1.  Selecteer in de hello Veeam back-up- en replicatie console **back-up- en replicatie**. Met de rechtermuisknop op **back-up**, en selecteer vervolgens **VMware** of **Hyper-V**, afhankelijk van uw omgeving.

    ![Beheerconsole Veeam, nieuwe back-up taak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  In Hallo **kopiëren met nieuwe back-uptaak** dialoogvenster Voer een naam en beschrijving voor Hallo-taak.

    ![Beheerconsole Veeam, nieuwe back-up taak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  Hallo-virtuele machines die u wilt dat tooprocess selecteren. Selecteer in de back-ups en selecteer vervolgens Hallo dagelijkse back-up die u eerder hebt gemaakt.

    ![Beheerconsole Veeam, nieuwe back-up taak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  Objecten uitsluiten van Hallo back-up taak, indien nodig.

5.  Selecteer uw back-opslagplaats en een waarde instellen voor **terugzetten verwijst tookeep**. Ervoor tooselect Hallo worden **behouden Hallo volgende herstelpunten voor archiveren** selectievakje. Back-upfrequentie Hallo definiëren en selecteer vervolgens **Geavanceerd**.

    ![Beheerconsole Veeam, nieuwe back-up taak pagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  Geef de volgende Hallo geavanceerde instellingen:

    * Op Hallo **onderhoud** tabblad, opslag niveau beschadiging guard uitschakelen.

    ![Beheerconsole voor Veeam nieuwe back-up taak geavanceerde instellingenpagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * Op Hallo **opslag** tabblad, moet u gegevensontdubbeling en compressie zijn uitgeschakeld.

    ![Beheerconsole voor Veeam nieuwe back-up taak geavanceerde instellingenpagina](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  Opgeven dat de gegevensoverdracht Hallo direct is.

8.  Hallo venster-schema voor back-up op basis van behoeften tooyour definiëren en vervolgens Hallo wizard is voltooid.

Zie voor meer informatie [maken van back-up taken](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).

## <a name="storsimple-cloud-snapshots"></a>De cloudmomentopnamen StorSimple

De cloudmomentopnamen StorSimple Hallo gegevens beveiligen die zich in uw StorSimple-apparaat. Maken van een cloudmomentopname is gelijkwaardig tooshipping lokale back-uptapes tooan offsite faciliteit. Als u Azure geografisch redundante opslag gebruikt, wordt het maken van een cloudmomentopname van een gelijkwaardige tooshipping back-uptapes toomultiple sites. Als u een apparaat toorestore na een noodgeval moet, kunt u mogelijk een andere StorSimple-apparaat online brengen en voer een failover. Na een failover hello, zou u kunnen tooaccess Hallo gegevens (snelheden cloud) van de meest recente cloudmomentopname Hallo zijn.

Hallo volgende sectie wordt beschreven hoe een korte script toostart toocreate en delete StorSimple cloud worden opgeslagen tijdens de back-up naverwerking.

> [!NOTE]
> Momentopnamen die handmatig of programmatisch gemaakt Voer Hallo StorSimple snapshot verloopbeleid niet. Deze momentopnamen moeten handmatig of via een programma verwijderen.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Start en cloudmomentopnamen verwijderen met behulp van een script

> [!NOTE]
> Evalueer zorgvuldig Hallo naleving en gegevens bewaren weerslag voordat u een momentopname van een StorSimple verwijderen. Voor meer informatie over het toorun post-back-uptaken script Hallo Veeam te zien.


### <a name="backup-lifecycle"></a>De levenscyclus van de back-up

![De levenscyclus van de back-diagram](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a>Vereisten

-   Hallo-server waarop Hallo script wordt uitgevoerd moet toegang tot tooAzure cloudbronnen hebben.
-   Hallo-gebruikersaccount moet Hallo noodzakelijke machtigingen hebben.
-   Een StorSimple-back-upbeleid Hello gekoppelde StorSimple volumes moeten worden ingesteld, maar niet is ingeschakeld.
-   U moet Hallo StorSimple resourcenaam, registratiesleutel, apparaatnaam en back-upbeleid-ID.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart of een cloudmomentopname verwijderen

1. [Installeer Azure PowerShell](/powershell/azure/overview).
2. [Downloaden en importeren van instellingen en abonnementsgegevens publiceren](https://msdn.microsoft.com/library/dn385850.aspx).
3. In klassieke Azure-portal hello, kunt u Hallo resourcenaam en [registratiecode voor uw StorSimple Manager-service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4. Voer op de server Hallo die Hallo-script wordt uitgevoerd, PowerShell als beheerder. Typ de volgende opdracht:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Opmerking Hallo back-upbeleid-ID.
5. Maak een nieuwe PowerShell-script met behulp van de volgende code Hallo in Kladblok.

    Kopieer en plak dit codefragment:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
6. tooadd hello script tooyour back-up taak, het bewerken van uw Veeam taak geavanceerde opties.

    ![Tabblad Veeam geavanceerde instellingen voor back-up-scripts](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

Het is raadzaam dat u uw back-upbeleid voor StorSimple cloud momentopname als een script dat na verwerking aan Hallo einde van de dagelijkse back-uptaak uitvoert. Voor meer informatie over hoe tooback up en herstel de back-uptoepassing omgeving toohelp u voldoet aan uw RPO en RTO, neem contact op met uw back-architect.

## <a name="storsimple-as-a-restore-source"></a>StorSimple als een bron terugzetten

Herstelt vanuit een StorSimple-apparaat werk zoals herstelt vanaf elk apparaat met blokopslag. Gelaagde toohello cloud gegevens te herstellen vindt plaats met een snelheid van de cloud. Voor lokale gegevens optreden herstelacties op Hallo lokale schijfsnelheid van Hallo-apparaat.

Met Veeam krijgt u snel gedetailleerde, op bestandsniveau herstel via StorSimple via Hallo ingebouwde explorer weergaven in Hallo Veeam-console. Gebruik de Veeam Explorers toorecover afzonderlijke objecten, zoals e-mailberichten, Active Directory-objecten en de SharePoint-items uit de back-ups. Hallo-herstel kan worden uitgevoerd zonder onderbreking van de lokale virtuele machine. U kunt ook punt in tijd herstel voor Azure SQL Database en Oracle-databases doen. Veeam en StorSimple zorg Hallo proces van herstel op itemniveau uit Azure snel en eenvoudig. Voor informatie over hoe u een terugzetbewerking tooperform hello Veeam te zien:

- Voor [Exchange-Server](https://www.veeam.com/microsoft-exchange-recovery.html)
- Voor [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)
- Voor [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)
- Voor [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)
- Voor [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)


## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple failover en herstel na noodgevallen

> [!NOTE]
> Voor scenario's met back-updoel wordt StorSimple Cloud toestel niet ondersteund als een doel voor herstel.

Een noodgeval kan zijn veroorzaakt door een verscheidenheid aan factoren. Hallo volgende tabel geeft een lijst met algemene herstel na noodgevallen.

| Scenario | Impact | Hoe toorecover | Opmerkingen |
|---|---|---|---|
| Fout met StorSimple | Back-up en herstelbewerkingen zijn onderbroken. | Hallo mislukte apparaat vervangen en uit te voeren [StorSimple failover en herstel na noodgevallen](storsimple-device-failover-disaster-recovery.md). | Als u een terugzetbewerking na het herstel van apparaat tooperform moet, worden de volledige gegevens wordt opgehaald uit Hallo cloud toohello nieuw apparaat. Alle bewerkingen zijn met een snelheid van de cloud. Hallo-index en de catalogus opnieuw scannen proces mogelijk alle back-upsets toobe gescand en opgehaald uit de Hallo cloud laag toohello lokale apparaat laag, dit kan een tijdrovend proces zijn. |
| Veeam-serverfout | Back-up en herstelbewerkingen zijn onderbroken. | Back-upserver Hallo bouwen en uitvoeren van het terugzetten van de database zoals beschreven in [Veeam Help en ondersteuning (technische documentatie)](https://www.veeam.com/documentation-guides-datasheets.html).  | U moet opnieuw samenstellen of herstellen Hallo Veeam server op Hallo disaster recovery site. Herstelpunt Hallo database toohello meest recente. Als hello herstelde Veeam database niet synchroon met de meest recente back-uptaken is, is indexeren en catalogiseren vereist. Deze index en de catalogus opnieuw scannen proces mogelijk alle back-upsets toobe gescand en opgehaald uit de Hallo laag toohello lokale apparaat cloudlaag. Dit maakt het verdere tijdrovende. |
| De mislukking van de site die tot verlies van zowel back-upserver Hallo StorSimple Hallo leidt | Back-up en herstelbewerkingen zijn onderbroken. | StorSimple eerst herstellen en herstel vervolgens Veeam. | StorSimple eerst herstellen en herstel vervolgens Veeam. Als u een terugzetbewerking na het herstel van apparaat tooperform nodig, worden Hallo volledige gegevens wordt opgehaald uit Hallo cloud toohello nieuw apparaat. Alle bewerkingen zijn met een snelheid van de cloud. |


## <a name="references"></a>Verwijzingen

Hallo documenten te volgen zijn waarnaar wordt verwezen voor dit artikel:

- [StorSimple multipath i/o-installatie](storsimple-configure-mpio-windows-server.md)
- [Scenario's voor opslag: Thin provisioning](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Met behulp van GPT-schijven](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Schaduwkopieën van gedeelde mappen instellen](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het te[terugzetten vanuit een back-upset](storsimple-restore-from-backup-set-u2.md).
- Meer informatie over het tooperform [apparaat failover en herstel na noodgevallen](storsimple-device-failover-disaster-recovery.md).
