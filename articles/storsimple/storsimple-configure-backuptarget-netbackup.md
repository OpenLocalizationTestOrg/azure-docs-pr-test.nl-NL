---
title: aaaStorSimple 8000 series als back-updoel met NetBackup | Microsoft Docs
description: Hallo StorSimple back-updoel configuratie met Veritas NetBackup beschreven.
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
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>StorSimple als een back-updoel met NetBackup

## <a name="overview"></a>Overzicht

Azure StorSimple is een hybride cloud-opslag-oplossing van Microsoft. Hallo complexiteit van de exponentiële Gegevensgroei adressen StorSimple met behulp van een Azure storage-account als een uitbreiding van Hallo on-premises oplossing en automatisch lagen gegevens voor lokale opslag en cloud-opslag.

In dit artikel wordt besproken StorSimple-integratie met Veritas NetBackup en aanbevolen procedures voor het integreren van beide oplossingen. We ook maken aanbevelingen voor hoe tooset up Veritas NetBackup toobest integreren met StorSimple. Aanbevolen procedures voor tooVeritas, back-architecten en administrators voor de beste manier tooset Hallo Veritas NetBackup toomeet afzonderlijke back-upvereisten en service level agreements (Sla's) uit te stellen.

Hoewel we configuratiestappen en belangrijkste concepten illustreren, is in dit artikel geen stapsgewijze handleiding voor een configuratie of de installatie. We gaan ervan uit dat Hallo basic onderdelen en infrastructuur zijn en op gereed toosupport Hallo-concepten die worden beschreven.

### <a name="who-should-read-this"></a>Wie is dit?

Hallo-informatie in dit artikel is het nuttigst toobackup beheerders, opslagbeheerders en storage-architecten die kennis van opslag, Windows Server 2012 R2, Ethernet, cloudservices en Veritas NetBackup hebben.

### <a name="supported-versions"></a>Ondersteunde versies

-   NetBackup 7.7.x en latere versies
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
![lagen StorSimple-diagram](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

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

| Opslagcapaciteit       | 8100          | 8600            |
|------------------------|---------------|-----------------|
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

![StorSimple als een primaire back-updoel logisch diagram](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Primaire doel van de back-up logische stappen

1.  Hallo back-upserver contactpersonen Hallo doel back-upagent en Hallo backup-agent verzendt gegevens toohello back-upserver.
2.  back-upserver Hallo schrijft gegevens toohello StorSimple gelaagde volumes.
3.  back-upserver Hallo werkt Hallo catalogusdatabase en vervolgens heeft voltooid Hallo back-uptaak.
4.  Een script momentopname activeert Hallo StorSimple snapshot manager (start of verwijderen).
5.  Hallo back-upserver worden verlopen back-ups op basis van een bewaarbeleid verwijderd.

### <a name="primary-target-restore-logical-steps"></a>Primaire doel terugzetten logische stappen

1.  back-upserver Hallo start Hallo relevante gegevens terugzetten vanuit Hallo-opslagplaats.
2.  back-upagent Hallo ontvangt gegevens van Hallo van Hallo back-upserver.
3.  back-upserver Hallo voltooit Hallo hersteltaak.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple als secundaire back-doel

In dit scenario worden StorSimple-volumes voornamelijk gebruikt voor lange bewaartermijn en archiveren.

Hallo volgende afbeelding toont een architectuur in welke eerste back-ups en hersteld doelvolume hoge prestaties. Deze back-ups worden gekopieerd en gearchiveerde tooa StorSimple gelaagd volume op een vast schema.

Het is belangrijk toosize het volume met hoge prestaties zodat deze uw vereisten bewaren beleid capaciteit en prestaties verwerken kan.

![StorSimple als een secundaire back-updoel logisch diagram](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Back-up logische stappen secundaire doel

1.  Hallo back-upserver contactpersonen Hallo doel back-upagent en Hallo backup-agent verzendt gegevens toohello back-upserver.
2.  back-upserver Hallo schrijft toohigh prestaties gegevensopslag.
3.  back-upserver Hallo werkt Hallo catalogusdatabase en vervolgens heeft voltooid Hallo back-uptaak.
4.  back-upserver Hallo tooStorSimple van back-ups op basis van een bewaarbeleid opgehaald.
5.  Een script momentopname activeert Hallo StorSimple snapshot manager (start of verwijderen).
6.  Hallo back-upserver verwijderingen Hallo verlopen back-ups op basis van een bewaarbeleid.

### <a name="secondary-target-restore-logical-steps"></a>Secundaire doel terugzetten logische stappen

1.  back-upserver Hallo start Hallo relevante gegevens terugzetten vanuit Hallo-opslagplaats.
2.  back-upagent Hallo ontvangt gegevens van Hallo van Hallo back-upserver.
3.  back-upserver Hallo voltooit Hallo hersteltaak.

## <a name="deploy-hello-solution"></a>Hallo-oplossing implementeren

Implementatie van deze oplossing vereist drie stappen:
1. Bereid Hallo-netwerkinfrastructuur.
2. Uw StorSimple-apparaat implementeren als een back-doel.
3. Veritas NetBackup implementeren.

Elke stap wordt uitgebreid beschreven in Hallo uit te voeren.

### <a name="set-up-hello-network"></a>Hallo-netwerk instellen

Omdat StorSimple een oplossing die geïntegreerd met hello Azure-cloud is, moet StorSimple een actieve en functioneel verbinding toohello Azure-cloud. Deze verbinding wordt gebruikt voor bewerkingen, zoals cloudmomentopnamen, beheren, en metagegevens overbrengen en tootier oudere, minder gebruikte gegevens tooAzure cloud-opslag.

Voor Hallo oplossing tooperform optimaal, raden we aan dat u deze netwerken aanbevolen procedures volgt:

-   Hallo-koppeling die verbinding Hallo StorSimple lagen tooAzure maakt moet voldoen aan de bandbreedtevereisten van uw. tooachieve dit toepassing hello juiste Quality of Service (QoS) niveau tooyour infrastructuur switches toomatch RPO- en herstelinstellingen tijd objective (RTO) Sla's.

-   Maximale toegangslatentie van Azure Blob-opslag moet ongeveer 80 ms.

### <a name="deploy-storsimple"></a>StorSimple implementeren

Zie voor stapsgewijze instructies voor StorSimple-implementatie, [uw on-premises StorSimple-apparaat implementeren](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>NetBackup implementeren

Zie voor stapsgewijze instructies NetBackup 7.7.x voor implementatie, Hallo [NetBackup 7.7.x documentatie](http://www.veritas.com/docs/000094423).

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

- Gebruik geen spanned volumes (gemaakt door Windows Schijfbeheer;) spanned volumes worden niet ondersteund.
- De volumes formatteren met NTFS met een toewijzingsgrootte van 64 KB.
- Hallo StorSimple-volumes toewijzen rechtstreeks toohello NetBackup server.
    - ISCSI-gebruiken voor fysieke servers.
    - Passthrough-schijven voor virtuele servers gebruiken.


## <a name="best-practices-for-storsimple-and-netbackup"></a>Aanbevolen procedures voor StorSimple en NetBackup

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

### <a name="netbackup-best-practices"></a>Aanbevolen procedures NetBackup

-   Hallo NetBackup database moet lokale toohello server en bevindt zich niet op een StorSimple-volume.
-   Voor herstel na noodgevallen, back-up Hallo NetBackup database op een StorSimple-volume.
-   We NetBackup volledige en incrementele back-ups ondersteunen (ook waarnaar wordt verwezen tooas differentiële incrementele back-ups in NetBackup) voor deze oplossing. Het is raadzaam dat u geen synthetische cumulatieve incrementele back-ups en gebruikt.
-   Back-upgegevensbestanden moeten alleen Hallo gegevens voor een specifieke taak bevatten. Bijvoorbeeld geen media worden toegevoegd via verschillende taken zijn toegestaan.

Voor Hallo recente NetBackup-instellingen en aanbevolen procedures voor het implementeren van deze vereisten, Zie de documentatie bij de Hallo NetBackup op [www.veritas.com](https://www.veritas.com).


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

## <a name="set-up-netbackup-storage"></a>NetBackup opslag instellen

### <a name="tooset-up-netbackup-storage"></a>tooset NetBackup opslag configureren

1.  Selecteer in de Hallo NetBackup-beheerconsole, **Media- en Apparaatbeheer** > **apparaten** > **schijfgroepen**. Selecteer in de Hallo schijf Pool-configuratiewizard, Hallo server opslagtype **AdvancedDisk**, en selecteer vervolgens **volgende**.

    ![NetBackup-beheerconsole schijf Pool-configuratiewizard](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Selecteer uw server en selecteer vervolgens **volgende**.

    ![NetBackup-beheerconsole, selecteer Hallo-server](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  Selecteer uw StorSimple-volume.

    ![NetBackup-beheerconsole, selecteer Hallo StorSimple-volume schijf](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Voer een naam voor de back-updoel Hallo en selecteer vervolgens **volgende** > **volgende** toofinish Hallo-wizard.

5.  Hallo-instellingen bekijken en selecteer vervolgens **voltooien**.

6.  Wijzig bij Hallo einde van elke toewijzing volume, Hallo opslag apparaat instellingen toomatch die worden aanbevolen in [aanbevolen procedures voor StorSimple en NetBackup](#best-practices-for-storsimple-and-netbackup).

7. Herhaal stap 1-6 totdat u bent klaar voor het toewijzen van uw StorSimple-volumes.

    ![NetBackup-beheerconsole schijfconfiguratie](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>StorSimple instellen als primaire back-doel

> [!NOTE]
> Gegevens terugzetten vanuit een back-up die gelaagde toohello cloud is optreden met een snelheid van de cloud.

Hallo toont volgende afbeelding Hallo toewijzing van een typische volume tooa back-uptaak. In dit geval alle Hallo wekelijkse back-ups toohello zaterdag volledige schijf toewijzen en incrementele back-ups Hallo tooMonday vrijdag incrementele schijven worden toegewezen. Alle Hallo back-ups en herstelbewerkingen zijn van een StorSimple gelaagd volume.

![Primaire back-updoel configuratie logisch diagram ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>StorSimple als primaire back-updoel algemene voorbeeld plannen

Hier volgt een voorbeeld van een algemene rotatieschema vier weken, maandelijkse en jaarlijkse:

| Type frequentie/back-up | Volledig | Incrementele (dagen 1-5)  |   
|---|---|---|
| Wekelijks (weken 1-4) | Zaterdag | Maandag tot vrijdag |
| Maandelijks  | Zaterdag  |   |
| Jaarlijks | Zaterdag  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>StorSimple-volumes tooa NetBackup back-uptaak toewijzen

Hallo volgende reeks wordt ervan uitgegaan dat doelhost NetBackup en Hallo zijn geconfigureerd in overeenstemming met de Hallo NetBackup agent richtlijnen.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>tooassign StorSimple-volumes tooa NetBackup back-uptaak

1.  Selecteer in de Hallo NetBackup-beheerconsole, **NetBackup Management**, met de rechtermuisknop op **beleid**, en selecteer vervolgens **nieuw beleid**.

    ![NetBackup Administration Console, een nieuw beleid maken](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  In Hallo **toevoegen van een nieuw beleid** in het dialoogvenster een naam voor het Hallo-beleid en selecteer vervolgens Hallo **gebruik beleid configuratiewizard** selectievakje. Selecteer **OK**.

    ![NetBackup-beheerconsole een dialoogvenster voor nieuw beleid toevoegen](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  In de Wizard beleid op back-up hello, electeer back-uptype die u wilt en selecteer vervolgens Hallo **volgende**.

    ![NetBackup-beheerconsole, Selecteer type back-up](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tooset hello beleidstype, selecteer **standaard**, en selecteer vervolgens **volgende**.

    ![NetBackup-beheerconsole, selecteer beleidstype](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Selecteer de host, selecteer Hallo **client-besturingssysteem detecteren** selectievakje en selecteer vervolgens **toevoegen**. Selecteer **volgende**.

    ![NetBackup-beheerconsole, lijst met clients in een nieuw beleid](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Selecteer Hallo stations tooback up gewenste.

    ![NetBackup-beheerconsole, back-up van de selecties voor een nieuw beleid](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Hallo-frequentie en retentie-waarden die voldoen aan de vereisten van uw back-selecteren.

    ![NetBackup-beheerconsole, back-upfrequentie en de rotatie voor een nieuw beleid](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Selecteer **volgende** > **volgende** > **voltooien**.  U kunt Hallo planning aanpassen nadat Hallo beleid is gemaakt.

9.  Selecteer tooexpand Hallo beleid die u zojuist hebt gemaakt, en selecteer vervolgens **planningen**.

    ![NetBackup-beheerconsole, schema's voor een nieuw beleid](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Met de rechtermuisknop op **differentiële Inc**, selecteer **kopiëren toonew**, en selecteer vervolgens **OK**.

    ![NetBackup-beheerconsole kopie planning tooa nieuw beleid](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Met de rechtermuisknop op Hallo van een nieuw gemaakt planning en selecteer vervolgens **wijziging**.

12.  Op Hallo **kenmerken** tabblad, selecteer Hallo **beleid Opslagselectie overschrijven** selectievakje in en selecteer vervolgens Hallo volume waar maandag incrementele back-ups gaat.

    ![NetBackup-beheerconsole, schema wijzigen](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  Op Hallo **venster Start** tabblad, selecteer Hallo tijdvenster voor uw back-ups.

    ![NetBackup-beheerconsole start wijzigingsvenster](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  Selecteer **OK**.

15.  Herhaal stap 10-14 voor elke incrementele back-up. Selecteer Hallo relevante volume en plannen voor elke back-up die u maakt.

16.  Klik met de rechtermuisknop Hallo **differentiële Inc** plannen en vervolgens te verwijderen.

17.  Uw volledige schema toomeet die uw back-up moet wijzigen.

    ![NetBackup-beheerconsole, volledige schema wijzigen](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Hallo startvenster wijzigen.

    ![NetBackup-beheerconsole wijzigingsvenster Hallo starten](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  laatste planning Hallo ziet er als volgt:

    ![NetBackup-beheerconsole, laatste planning](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>StorSimple instellen als een secundaire back-doel

> [!NOTE]
>Gegevens terugzetten vanuit een back-up die gelaagde toohello cloud is optreden met een snelheid van de cloud.

In dit model, moet u een media (met uitzondering van StorSimple) opslag tooserve hebben als een tijdelijke cache. U kunt bijvoorbeeld een redundante matrix van onafhankelijke schijven (RAID) ruimte op volume tooaccommodate, input/output (I/O) en bandbreedte. U wordt aangeraden met behulp van RAID-5, 50 en 10.

Hallo volgende afbeelding toont typisch kortetermijnback bewaren lokale (toohello server) volumes en lange bewaartermijn archiveert volumes. In dit scenario alle back-ups uitgevoerd op Hallo lokale (toohello server) RAID-volume. Deze back-ups regelmatig worden gedupliceerd en gearchiveerde tooan archiveert volume. Het is belangrijk toosize (toohello server) van uw lokale RAID-volume dat de korte termijn capaciteit en prestaties vereisten voor de bewaarperiode kan verwerken.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple als een voorbeeld van een secundaire back-updoel algemene

![StorSimple als een secundaire back-updoel logisch diagram](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

Hallo volgende tabel toont hoe tooset up toorun back-ups op Hallo lokale en StorSimple-schijven. Bevat capaciteitsvereisten voor afzonderlijke en de totale.

### <a name="backup-configuration-and-capacity-requirements"></a>Back-upconfiguratie en capaciteitsvereisten van opslaggroepen

| Type back-up en retentie | Geconfigureerde opslag | Grootte (TiB) | Algemene vermenigvuldiger | Totale capaciteit\* (TiB) |
|---|---|---|---|---|
| Week 1 (volledige en incrementele) |Lokale schijf (korte)| 1 | 1 | 1 |
| StorSimple weken 2-4 |StorSimple schijf (op lange termijn) | 1 | 4 | 4 |
| Maandelijks volledige |StorSimple schijf (op lange termijn) | 1 | 12 | 12 |
| Jaarlijks volledige |StorSimple schijf (op lange termijn) | 1 | 1 | 1 |
|Vereiste grootte van algemene volumes |  |  |  | 18*|
\*Totale capaciteit omvat 17 TiB van StorSimple-schijven en 1 TiB van lokale RAID-volume.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Algemene voorbeeld planning: algemene rotatie wekelijkse, maandelijkse en jaarlijkse planning

| Week | Volledig | Incrementele dag 1 | Incrementele dag 2 | Incrementele dag 3 | Incrementele dag 4 | Incrementele dag 5 |
|---|---|---|---|---|---|---|
| 1 week | Lokale RAID-volume  | Lokale RAID-volume | Lokale RAID-volume | Lokale RAID-volume | Lokale RAID-volume | Lokale RAID-volume |
| Week 2 | StorSimple weken 2-4 |   |   |   |   |   |
| Week 3 | StorSimple weken 2-4 |   |   |   |   |   |
| Week 4 | StorSimple weken 2-4 |   |   |   |   |   |
| Maandelijks | Maandelijks StorSimple |   |   |   |   |   |
| Jaarlijks | Jaarlijks StorSimple  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>StorSimple-volumes tooa NetBackup archief en duplicatie taak toewijzen

Omdat NetBackup tal van opties voor opslag en media management biedt, wordt u aangeraden dat u contact met Veritas opneemt of uw NetBackup architect tooproperly beoordelen uw opslagvereisten lifecycle-beleid (SLP).

Nadat de initiële schijfgroepen Hallo die u hebt gedefinieerd, moet u toodefine drie extra opslagruimte lifecycle-beleid, voor een totaal van vier beleidsregels:
* LocalRAIDVolume
* StorSimpleWeek2 4
* StorSimpleMonthlyFulls
* StorSimpleYearlyFulls

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>tooassign StorSimple-volumes tooa NetBackup archief en duplicatie taak

1.  Selecteer in de Hallo NetBackup-beheerconsole, **opslag** > **Lifecycle-beleid voor opslag** > **Lifecycle-beleid voor nieuwe opslag**.

    ![NetBackup-beheerconsole, nieuwe opslag lifecycle-beleid](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Voer een naam voor het Hallo-momentopname en selecteer vervolgens **toevoegen**.

3.  In Hallo **nieuwe bewerking** op Hallo van het dialoogvenster **eigenschappen** tabblad voor **bewerking**, selecteer **back-up**. Selecteer Hallo gewenste waarden voor **doelopslagaccount**, **bewaren type**, en **bewaarperiode**. Selecteer **OK**.

    ![NetBackup Administration Console, in het dialoogvenster voor nieuwe bewerking](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Hiermee definieert u de eerste back-upbewerking Hallo en opslagplaats.

4.  Selecteer toohighlight Hallo vorige bewerking en selecteer vervolgens **toevoegen**. In Hallo **wijziging opslagbewerking** dialoogvenster, selecteer Hallo gewenste waarden voor **doelopslagaccount**, **bewaren type**, en **bewaarperiode** .

    ![NetBackup Administration Console, in het dialoogvenster van de opslagbewerking wijzigen](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Selecteer toohighlight Hallo vorige bewerking en selecteer vervolgens **toevoegen**. In Hallo **Lifecycle-beleid voor nieuwe opslag** dialoogvenster Voeg maandelijkse back-ups van een jaar.

    ![NetBackup Administration Console, in het dialoogvenster voor nieuw beleid voor opslag levenscyclus](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Herhaal stap 4 en 5 totdat u bewaarbeleid van de uitgebreide SLP Hallo die u nodig hebt gemaakt.

    ![NetBackup-beheerconsole, beleid in het dialoogvenster Hallo-Lifecycle-beleid voor nieuwe opslag toevoegen](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Als u hebt onder uw bewaarbeleid SLP definiëren **beleid**, een back-upbeleid definiëren Hallo stappen uiteengezet in [toewijzen StorSimple-volumes tooa NetBackup back-uptaak](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  Onder **planningen**, in Hallo **schema wijzigen** in het dialoogvenster met de rechtermuisknop op **volledige**, en selecteer vervolgens **wijziging**.

    ![NetBackup-beheerconsole, het dialoogvenster schema wijzigen](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Selecteer Hallo **beleid Opslagselectie overschrijven** selectievakje in en selecteer vervolgens Hallo SLP bewaarbeleid die u hebt gemaakt in stap 1-6.

    ![NetBackup-beheerconsole overschrijven beleid Opslagselectie](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Selecteer **OK**, en Herhaal voor Hallo incrementele back-upschema.

    ![NetBackup Administration Console, in het dialoogvenster schema wijzigen voor incrementele back-ups](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Back-uptype bewaren | Grootte (TiB) | Algemene vermenigvuldiger\* | Totale capaciteit (TiB)  |
|---|---|---|---|
| Wekelijkse volledige |  1  |  4 | 4  |
| Dagelijkse incrementele  | 0.5  | 20 (cycli zijn gelijk toohello aantal weken per maand) | 12 (2 voor extra quotum) |
| Maandelijks volledige  | 1 | 12 | 12 |
| Jaarlijks volledige | 1  | 10 | 10 |
| Algemene vereisten  |     |     | 38 |
| Extra quota  | 4  |    | 42 totale algemene vereisten |
\*Hallo algemene vermenigvuldiger is Hallo aantal exemplaren van de u nodig tooprotect hebt en de vereisten van uw back-upbeleid voor toomeet behouden.

## <a name="storsimple-cloud-snapshots"></a>De cloudmomentopnamen StorSimple

De cloudmomentopnamen StorSimple Hallo gegevens beveiligen die zich in uw StorSimple-apparaat. Maken van een cloudmomentopname is gelijkwaardig tooshipping lokale back-uptapes tooan offsite faciliteit. Als u Azure geografisch redundante opslag gebruikt, wordt het maken van een cloudmomentopname van een gelijkwaardige tooshipping back-uptapes toomultiple sites. Als u een apparaat toorestore na een noodgeval moet, kunt u mogelijk een andere StorSimple-apparaat online brengen en voer een failover. Na een failover hello, zou u kunnen tooaccess Hallo gegevens (snelheden cloud) van de meest recente cloudmomentopname Hallo zijn.

Hallo volgende sectie wordt beschreven hoe een korte script toostart toocreate en delete StorSimple cloud worden opgeslagen tijdens de back-up naverwerking.

> [!NOTE]
> Momentopnamen die handmatig of programmatisch gemaakt Voer Hallo StorSimple snapshot verloopbeleid niet. Deze momentopnamen moeten handmatig of via een programma verwijderen.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Start en cloudmomentopnamen verwijderen met behulp van een script

> [!NOTE]
> Evalueer zorgvuldig Hallo naleving en gegevens bewaren weerslag voordat u een momentopname van een StorSimple verwijderen. Voor meer informatie over het toorun een script post-back-uptaken, Zie Hallo [NetBackup documentatie](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>De levenscyclus van de back-up

![Back-Lifecycle-diagram](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a>Vereisten

-   Hallo-server waarop Hallo script wordt uitgevoerd moet toegang tot tooAzure cloudbronnen hebben.
-   Hallo-gebruikersaccount moet Hallo noodzakelijke machtigingen hebben.
-   Een StorSimple-back-upbeleid Hello gekoppelde StorSimple volumes moeten worden ingesteld, maar niet is ingeschakeld.
-   U moet Hallo StorSimple resourcenaam, registratiesleutel, apparaatnaam en back-upbeleid-ID.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart of een cloudmomentopname verwijderen

1.  [Installeer Azure PowerShell](/powershell/azure/overview).
2.  [Downloaden en importeren van instellingen en abonnementsgegevens publiceren](https://msdn.microsoft.com/library/dn385850.aspx).
3.  In klassieke Azure-portal hello, kunt u Hallo resourcenaam en [registratiecode voor uw StorSimple Manager-service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  Voer op de server Hallo die Hallo-script wordt uitgevoerd, PowerShell als beheerder. Typ de volgende opdracht:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Opmerking Hallo back-upbeleid-ID.
5.  Maak een nieuwe PowerShell-script met behulp van de volgende code Hallo in Kladblok.

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
      Sla Hallo PowerShell script toohello dezelfde locatie waar u uw Azure opgeslagen publicatie-instellingen. Bijvoorbeeld, opslaan als C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Hallo script tooyour back-uptaak in NetBackup toevoegen. toodo deze, uw NetBackup taak options vooraf verwerken en na verwerking van opdrachten voor bewerken.

> [!NOTE]
> Het is raadzaam dat u uw back-upbeleid voor StorSimple cloud momentopname als een script dat na verwerking aan Hallo einde van de dagelijkse back-uptaak uitvoert. Voor meer informatie over hoe tooback up en herstel de back-uptoepassing omgeving toohelp u voldoet aan uw RPO en RTO, neem contact op met uw back-architect.

## <a name="storsimple-as-a-restore-source"></a>StorSimple als een bron terugzetten

Herstelt vanuit een StorSimple-apparaat werk zoals herstelt vanaf elk apparaat met blokopslag. Gelaagde toohello cloud gegevens te herstellen vindt plaats met een snelheid van de cloud. Voor lokale gegevens optreden herstelacties op Hallo lokale schijfsnelheid van Hallo-apparaat. Voor informatie over hoe u een terugzetbewerking tooperform Zie Hallo [NetBackup documentatie](http://www.veritas.com/docs/000094423). Het is raadzaam dat u aanbevolen procedures voor tooNetBackup terugzetten in overeenstemming zijn.

## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple failover en herstel na noodgevallen

> [!NOTE]
> Voor scenario's met back-updoel wordt StorSimple Cloud toestel niet ondersteund als een doel voor herstel.

Een noodgeval kan zijn veroorzaakt door een verscheidenheid aan factoren. Hallo volgende tabel geeft een lijst met algemene herstel na noodgevallen.

| Scenario | Impact | Hoe toorecover | Opmerkingen |
|---|---|---|---|
| Fout met StorSimple | Back-up en herstelbewerkingen zijn onderbroken. | Hallo mislukte apparaat vervangen en uit te voeren [StorSimple failover en herstel na noodgevallen](storsimple-device-failover-disaster-recovery.md). | Als u een terugzetbewerking na het herstel van apparaat tooperform moet, worden de volledige gegevens wordt opgehaald uit Hallo cloud toohello nieuw apparaat. Alle bewerkingen zijn met een snelheid van de cloud. Hallo-index en de catalogus opnieuw scannen proces mogelijk alle back-upsets toobe gescand en opgehaald uit de Hallo cloud laag toohello lokale apparaat laag, dit kan een tijdrovend proces zijn. |
| Serverfout NetBackup | Back-up en herstelbewerkingen zijn onderbroken. | Back-upserver Hallo bouwen en uitvoeren van de database terugzetten. | U moet opnieuw samenstellen of herstellen Hallo NetBackup server op Hallo disaster recovery site. Herstelpunt Hallo database toohello meest recente. Als hello herstelde NetBackup-database niet synchroon met de meest recente back-uptaken is, is indexeren en catalogiseren vereist. Deze index en de catalogus opnieuw scannen proces mogelijk alle back-upsets toobe gescand en opgehaald uit de Hallo laag toohello lokale apparaat cloudlaag. Dit maakt het verdere tijdrovende. |
| De mislukking van de site die tot verlies van zowel back-upserver Hallo StorSimple Hallo leidt | Back-up en herstelbewerkingen zijn onderbroken. | StorSimple eerst herstellen en herstel vervolgens NetBackup. | StorSimple eerst herstellen en herstel vervolgens NetBackup. Als u een terugzetbewerking na het herstel van apparaat tooperform nodig, worden Hallo volledige gegevens wordt opgehaald uit Hallo cloud toohello nieuw apparaat. Alle bewerkingen zijn met een snelheid van de cloud. |

## <a name="references"></a>Verwijzingen

Hallo documenten te volgen zijn waarnaar wordt verwezen voor dit artikel:

- [StorSimple multipath i/o-installatie](storsimple-configure-mpio-windows-server.md)
- [Scenario's voor opslag: Thin provisioning](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Met behulp van GPT-schijven](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Schaduwkopieën van gedeelde mappen instellen](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het te[terugzetten vanuit een back-upset](storsimple-restore-from-backup-set-u2.md).
- Meer informatie over het tooperform [apparaat failover en herstel na noodgevallen](storsimple-device-failover-disaster-recovery.md).
