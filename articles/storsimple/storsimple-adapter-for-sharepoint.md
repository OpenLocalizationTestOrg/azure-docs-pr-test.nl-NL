---
title: aaaInstall StorSimple-Adapter voor SharePoint | Microsoft Docs
description: Hierin wordt beschreven hoe tooinstall en configureren of te verwijderen van Hallo StorSimple Adapter voor SharePoint in een SharePoint-serverfarm.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Installeren en configureren van Hallo StorSimple Adapter voor SharePoint
## <a name="overview"></a>Overzicht
Hallo StorSimple-Adapter voor SharePoint is een onderdeel waarmee u Microsoft Azure StorSimple flexibele opslag en data protection tooSharePoint serverfarms bieden. U kunt Hallo adapter toomove binaire grote Object (BLOB) inhoud op Hallo SQL Server inhoudsdatabases toohello Microsoft Azure StorSimple hybride cloud opslagapparaat.

Hallo StorSimple-Adapter voor SharePoint fungeert als een externe BLOB Storage planning provider en maakt gebruik van SQL Server externe BLOB Storage functie toostore Hallo ongestructureerde SharePoint-inhoud (in de vorm van de Hallo van BLOB's) op een bestandsserver die wordt ondersteund door een StorSimple-apparaat.

> [!NOTE]
> Hallo StorSimple-Adapter voor SharePoint biedt ondersteuning voor SharePoint Server 2010 afstand BLOB Storage planning. Geen biedt ondersteuning voor SharePoint Server 2010 externe BLOB Storage (EBS).


* toodownload hello StorSimple-Adapter voor SharePoint, gaat u te[StorSimple-Adapter voor SharePoint] [ 1] in Hallo Microsoft Download Center.
* Voor informatie over de planning voor Resourcestructuur en Resourcestructuur beperkingen gaat te[beslist toouse Resourcestructuur in SharePoint 2013] [ 2] of [plannen voor Resourcestructuur (SharePoint Server 2010)] [3].

Hallo rest van dit overzicht wordt kort beschreven Hallo rol Hallo StorSimple-Adapter voor SharePoint en Hallo capaciteit van SharePoint en prestatielimieten die u weten moet voordat u installeert en Hallo-adapter configureert. Nadat u deze gegevens bekijken, gaat u te[StorSimple-Adapter voor SharePoint-installatie](#storsimple-adapter-for-sharepoint-installation) toobegin Hallo adapter instellen.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>StorSimple-Adapter voor SharePoint voordelen
Inhoud wordt opgeslagen in een SharePoint-site als niet-gestructureerde BLOB-gegevens in een of meer inhoudsdatabases. Standaard worden deze databases worden gehost op computers waarop SQL Server uitvoert en bevinden zich in Hallo SharePoint-serverfarm. BLOBs kunnen snel worden verhoogd met grootte, verbruiken grote hoeveelheden lokale opslag. Daarom kunt u toofind oplossing voor een andere, minder dure opslag. SQL Server biedt een technologie die externe Blob Storage planning die u kunt BLOB-inhoud opslaan in de bestandssysteem Hallo buiten SQL Server-database Hallo genoemd. BLOBs kunnen zich bevinden in het bestandssysteem Hallo op Hallo-computer waarop SQL Server wordt uitgevoerd met Resourcestructuur, of ze kunnen worden opgeslagen in het bestandssysteem Hallo op een andere servercomputer.

Resourcestructuur vereist dat u een provider Resourcestructuur zoals Hallo StorSimple-Adapter voor SharePoint, tooenable Resourcestructuur in SharePoint. Hallo StorSimple-Adapter voor SharePoint werkt met Resourcestructuur, zodat u BLOBs tooa server back-up door Microsoft Azure StorSimple-systeem Hallo gemaakt verplaatsen. Microsoft Azure StorSimple slaat vervolgens de blobgegevens Hallo lokaal of in de cloud hello, op basis van gebruik. BLOBs die zeer actief zijn (meestal waarnaar wordt verwezen tooas Tier 1 of gegevens hot) lokaal staan. Minder actieve gegevens en archivering van gegevens zich bevinden in de cloud Hallo. Nadat u op een inhoudsdatabase Resourcestructuur hebt ingeschakeld, worden alle nieuwe BLOB-inhoud in SharePoint gemaakt wordt opgeslagen op Hallo StorSimple-apparaat en niet in de inhoudsdatabase Hallo.

Hallo Microsoft Azure StorSimple-implementatie van Resourcestructuur biedt Hallo volgende voordelen:

* Zwevend BLOB inhoud tooa afzonderlijke server, kunt u beperken Hallo querybelasting van SQL Server, betere reactiesnelheid van SQL Server. 
* Azure StorSimple maakt gebruik van gegevensontdubbeling en compressie tooreduce gegevensgrootte.
* Azure StorSimple biedt bescherming van gegevens in het formulier Hallo van lokale en cloudmomentopnamen. Ook als u Hallo-database zelf op Hallo StorSimple-apparaat plaatst, kunt u back-up Hallo inhoudsdatabase en BLOBs samen in een crashconsistent manier. (Verplaatsen Hallo inhoudsdatabase toohello apparaat wordt alleen ondersteund voor Hallo StorSimple 8000 series apparaat. Deze functie wordt niet ondersteund voor Hallo 5000 of 7000-serie.)
* Azure StorSimple bevat disaster recovery functies zoals failover, bestands- en volume herstel (inclusief test recovery) en snel herstel van gegevens.
* U kunt data recovery software, zoals Kroll Ontrack PowerControls, met StorSimple momentopnamen van herstel van BLOB-gegevens tooperform itemniveau van SharePoint-inhoud. (Deze software voor het herstel van gegevens is een afzonderlijke aankoop.)
* Hallo StorSimple-Adapter voor SharePoint kunt aansluiten op Hallo SharePoint Centraal beheer-portal, zodat u toomanage uw hele SharePoint-oplossing van een centrale locatie.

Het verplaatsen van BLOB-inhoud toohello bestandssysteem bieden andere kostenbesparingen en voordelen. Bijvoorbeeld met behulp van Resourcestructuur inkorten Hallo behoefte aan dure opslag van het niveau van Tier 1 en omdat deze de inhoudsdatabase Hallo kleiner, Resourcestructuur Hallo aantal databases dat is vereist in de SharePoint-serverfarm Hallo kan verminderen. Andere factoren, zoals de maximale grootte database en Hallo hoeveelheid niet-Resourcestructuur inhoud, kunnen echter ook opslagvereisten beïnvloeden. Zie voor meer informatie over Hallo kosten en voordelen van het gebruik van Resourcestructuur [plannen voor Resourcestructuur (SharePoint Foundation 2010)] [ 4] en [beslist toouse Resourcestructuur in SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Limieten voor capaciteit en prestaties
Voordat u Resourcestructuur in de SharePoint-oplossing overwegen, moet u rekening houden met Hallo getest prestaties en beperkingen van de capaciteit van SharePoint Server 2010 en SharePoint Server 2013 en hoe deze limieten tooacceptable prestaties gerelateerd zijn. Zie voor meer informatie [Software grenzen en beperkingen voor SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Lees Hallo volgende voordat u Resourcestructuur configureren:

* Zorg ervoor dat de totale grootte van die Hallo Hallo inhoud (grootte van een inhoudsdatabase Hallo) plus Hallo grootte van alle gekoppelde externalized BLOBs Hallo groottelimiet voor Resourcestructuur ondersteund door SharePoint niet overschrijden. Deze limiet is 200 GB. 
  
    **toomeasure inhoud van de database en de BLOB-grootte**
  
  1. Deze query uitvoeren op Hallo Centraal beheer WFE. Start Hallo SharePoint Management Shell en voer vervolgens de volgende Windows PowerShell-opdracht tooget Hallo grootte van de inhoudsdatabases Hallo Hallo:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Deze stap ontvangt Hallo de grootte van de inhoudsdatabase Hallo op Hallo schijf.
  2. Voer een van de volgende SQL-query's in SQL Management Studio op Hallo-vak SQL server op elke inhoudsdatabase Hallo en Hallo resultaat toohello nummer verkregen in stap 1 toevoegen.
     
     Voer op de inhoudsdatabases van SharePoint 2013:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     Voer op de inhoudsdatabases van SharePoint 2010:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Deze stap ontvangt Hallo grootte Hallo BLOBs die hebben is externalized.
* U wordt aangeraden dat u alle BLOBS en database inhoud lokaal opslaan op Hallo StorSimple-apparaat. Hallo StorSimple-apparaat is een cluster met twee knooppunten voor hoge beschikbaarheid. Hallo-inhoudsdatabases en BLOBs plaatsen op Hallo StorSimple-apparaat biedt hoge beschikbaarheid.
  
    Traditionele SQL Server migratie best practices toomove Hallo inhoudsdatabase toohello StorSimple-apparaat gebruiken. Hallo-database verplaatsen pas nadat alle BLOB-inhoud uit Hallo-database verplaatst toohello bestandsshare via de Resourcestructuur is. Als u ervoor toomove Hallo inhoudsdatabase toohello StorSimple-apparaat kiest, raden wij u Hallo inhoudsdatabase opslag configureren op Hallo-apparaat als primaire volume.
* In Microsoft Azure StorSimple, als gelaagde volumes gebruikt, is er geen enkele manier tooguarantee die inhoud lokaal wordt opgeslagen op Hallo StorSimple-apparaat niet meer worden gelaagde tooMicrosoft Azure cloud-opslag. Daarom wordt u aangeraden lokaal vastgemaakt StorSimple-volumes in combinatie met SharePoint RBS. Dit zorgt ervoor dat alle BLOB-inhoud lokaal op Hallo StorSimple-apparaat blijft, en niet verplaatst tooMicrosoft Azure is.
* Als u niet de inhoudsdatabases Hallo op Hallo StorSimple-apparaat opslaat, gebruik traditionele SQL Server hoge beschikbaarheid best practices die ondersteuning bieden voor Resourcestructuur. SQL Server clustering ondersteunt Resourcestructuur, terwijl SQL Server spiegelen niet. 

> [!WARNING]
> Als u Resourcestructuur niet hebt ingeschakeld, raden we niet verplaatsen Hallo inhoudsdatabase toohello StorSimple-apparaat. Dit is een niet-geteste configuratie.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>StorSimple-Adapter voor SharePoint-installatie
Voordat u Hallo StorSimple Adapter voor SharePoint installeren kunt, moet u Hallo StorSimple-apparaat configureren en zorg ervoor dat Hallo SharePoint-serverfarm en instantiëring van SQL Server aan alle vereisten voldoen. Deze zelfstudie wordt beschreven configuratievereisten, evenals de procedures voor het installeren en upgraden Hallo StorSimple Adapter voor SharePoint.

## <a name="configure-prerequisites"></a>Vereisten configureren
Zorg voordat u Hallo StorSimple Adapter voor SharePoint installeren kunt, Hallo StorSimple-apparaat, SharePoint-serverfarm en instantiëring van SQL Server voldoen aan vereisten volgen Hallo.

### <a name="system-requirements"></a>Systeemvereisten
Hallo StorSimple-Adapter voor SharePoint werkt met Hallo hardware en software te volgen:

* Ondersteund besturingssysteem: Windows Server 2008 R2 SP1, Windows Server 2012 of Windows Server 2012 R2
* Ondersteunde SharePoint versies – SharePoint Server 2010 of SharePoint Server 2013
* Ondersteunde versies van SQL Server: SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition of SQL Server 2012 Enterprise Edition
* StorSimple-apparaten ondersteund StorSimple 8000-serie, StorSimple 7000-serie of StorSimple 5000-reeks.

### <a name="storsimple-device-configuration-prerequisites"></a>Configuratievereisten voor StorSimple-apparaat
Hallo StorSimple-apparaat is een blok-apparaat, en als zodanig vereist een bestandsserver waarop Hallo gegevens kan worden gehost. Het is raadzaam dat u een afzonderlijke server in plaats van een bestaande server van Hallo SharePoint-farm gebruiken. Deze bestandsserver moet worden op Hallo hetzelfde local area network (LAN) als de SQL Server-computer Hallo die hosts Hallo-inhoudsdatabases.

> [!TIP]
> * Als u uw SharePoint-farm voor maximale beschikbaarheid configureert, moet u ook de bestandsserver Hallo voor hoge beschikbaarheid implementeren.
> * Als u niet de inhoudsdatabase Hallo op Hallo StorSimple-apparaat opslaat, gebruikt u traditionele hoge beschikbaarheid aanbevolen procedures die ondersteuning bieden voor Resourcestructuur. SQL Server clustering ondersteunt Resourcestructuur, terwijl SQL Server spiegelen niet. 


Zorg ervoor dat uw StorSimple-apparaat correct is geconfigureerd en dat toosupport relevante volumes uw SharePoint-implementatie worden geconfigureerd en toegankelijk is vanaf uw SQL Server-computer. Ga te[uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md) als u nog niet hebt geïmplementeerd en geconfigureerd uw StorSimple-apparaat. Houd er rekening mee Hallo IP-adres van de StorSimple-apparaat Hallo; u hebt deze tijdens de StorSimple-Adapter voor SharePoint-installatie.

Zorg daarnaast dat Hallo volume toobe gebruikt voor BLOB externalization Hallo volgens de vereisten voldoet aan:

* Hallo volume moet zijn geformatteerd met een clustergrootte van 64 KB.
* Uw web-front-end (WFE) en toepassingsservers moeten kunnen tooaccess Hallo volume via een pad (Universal Naming Convention) bevinden.
* Hallo SharePoint-serverfarm moet geconfigureerde toowrite toohello volume.

> [!NOTE]
> Na het installeren en configureren van de adapter Hallo alle BLOB externalization hello StorSimple-apparaat moet doorlopen (Hallo-apparaat wordt Hallo volumes tooSQL Server aanwezig en beheren van opslaglagen Hallo). U kunt andere doelen niet gebruiken voor BLOB externalization.


Als u van plan toouse StorSimple Snapshot Manager tootake momentopnamen van Hallo BLOB bent en databasegegevens worden verwijderd, worden ervoor tooinstall StorSimple Snapshot Manager op de databaseserver Hallo zodat het Hallo tooimplement SQL Writer-Service kan gebruiken Hallo Windows Volume Shadow Copy -Service (VSS).

> [!IMPORTANT]
> StorSimple Snapshot Manager biedt geen ondersteuning voor Hallo SharePoint VSS Writer en toepassingsconsistente momentopnamen kan niet van de SharePoint-gegevens. In een SharePoint-scenario biedt StorSimple Snapshot Manager alleen crashconsistente back-ups.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Configuratievereisten voor SharePoint-farm
Zorg ervoor dat uw SharePoint-serverfarm correct is geconfigureerd, als volgt:

* Controleer of uw SharePoint-serverfarm in orde is en controleer Hallo volgende:
* Alle SharePoint WFE en geregistreerd in de farm Hallo toepassingsservers worden uitgevoerd en kunnen worden gepingd van Hallo-server waarop u Hallo StorSimple Adapter voor SharePoint installeert.
* Hallo SharePoint Timer-service (SPTimerV3 of SPTimerV4) wordt uitgevoerd op elke WFE-server en de toepassingsserver.
* Beheerdersbevoegdheden hebben zowel Hallo SharePoint Timer-service en Hallo IIS-toepassingsgroep waaronder Hallo SharePoint Centraal beheer site wordt uitgevoerd.
* Zorg ervoor dat Internet Explorer Verbeterde beveiligingscontext (IE ESC) is uitgeschakeld. Volg deze stappen toodisable IE ESC:
  
  1. Sluit alle exemplaren van Internet Explorer.
  2. Hallo Serverbeheer starten.
  3. Klik in het linkerdeelvenster Hallo **lokale Server**.
  4. Op Hallo rechtermuisknop deelvenster naast te**verbeterde beveiliging van Internet Explorer**, klikt u op **op**.
  5. Onder **beheerders**, klikt u op **uit**.
  6. Klik op **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Externe vereisten voor BLOB Storage planning
Zorg ervoor dat u van een ondersteunde versie van SQL Server gebruikmaakt. Alleen hello volgende versies worden ondersteund en kunnen toouse Resourcestructuur:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

BLOBs kunnen worden externalized op alleen volumes die StorSimple-apparaat Hallo geeft tooSQL Server. Er zijn geen andere doelen voor BLOB externalization worden ondersteund.

Wanneer u alle vereiste configuratiestappen hebt voltooid, gaat u te[installeren Hallo StorSimple-Adapter voor SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Hallo StorSimple-Adapter installeren voor SharePoint
Hallo volgende stappen tooinstall hello StorSimple Adapter voor SharePoint gebruiken. Als u opnieuw Hallo software installeert, raadpleegt u [bijwerken of opnieuw Hallo StorSimple-Adapter installeren voor SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). Hallo-tijd die nodig is voor de installatie van Hallo is afhankelijk van totaal aantal Hallo van de SharePoint-databases op uw SharePoint-serverfarm.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Resourcestructuur configureren
Nadat u Hallo StorSimple Adapter voor SharePoint installeert, configureert u Resourcestructuur zoals beschreven in Hallo procedure te volgen.

> [!TIP]
> Hallo StorSimple-Adapter voor SharePoint in Hallo SharePoint Centraal beheer pagina Resourcestructuur toobe ingeschakeld of uitgeschakeld op elke inhoudsdatabase in Hallo SharePoint-farm wordt geplaatst. Echter, in- of uitschakelen van Resourcestructuur op Hallo inhoudsdatabase zorgt ervoor dat een IIS opnieuw instellen, die, afhankelijk van uw farmconfiguratie kan tijdelijk worden verstoren Hallo beschikbaarheid van Hallo SharePoint-webfront-end (WFE). (Factoren zoals Hallo gebruik van een front-end load balancer, de huidige server-werkbelasting hello, enzovoort, kunnen beperken of deze onderbreking elimineren.) tooprotect gebruikers van een onderbreking van, het is raadzaam dat u in- of uitschakelen van Resourcestructuur alleen tijdens een geplande onderhoudsvenster.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Garbagecollection configureren
Wanneer u objecten uit een SharePoint-site worden verwijderd, worden ze niet automatisch uit Hallo Resourcestructuur store volume verwijderd. In plaats daarvan een asynchrone, onderhoudsprogramma achtergrond verwijderen van zwevende BLOBs van Hallo bestandsarchief. Systeembeheerders periodiek dit proces toorun kunnen plannen of ze deze indien nodig kunnen starten.

Dit onderhoudsprogramma (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) wordt automatisch geïnstalleerd op alle SharePoint WFE-servers en toepassingsservers, wanneer u Resourcestructuur inschakelt. Hallo-programma wordt geïnstalleerd in Hallo volgende locatie: *opstartschijf*: \Program Files\Microsoft externe SQL-blobopslag 10.50\Maintainer\

Zie voor meer informatie over het configureren en gebruiken van Hallo onderhoudsprogramma [Resourcestructuur onderhouden in SharePoint Server 2013][8].

> [!IMPORTANT]
> Hallo Resourcestructuur maintainer programma wordt zo bronintensief. U moet deze toorun, plannen alleen tijdens perioden van lichte activiteiten op Hallo SharePoint-farm.


### <a name="delete-orphaned-blobs-immediately"></a>Zwevende BLOBs onmiddellijk verwijderen
Als u zwevende toodelete BLOBs onmiddellijk moet, kunt u Hallo instructies te volgen. Houd er rekening mee dat deze instructies een voorbeeld zijn van hoe dit kunt doen in een SharePoint 2013-omgeving met Hallo volgende onderdelen:

* naam van de inhoud van de database Hallo is WSS_Content.
* Hallo SQL-servernaam is SHRPT13 SQL12\SHRPT13.
* Hallo webtoepassingsnaam is SharePoint: 80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Bijwerken of opnieuw Hallo StorSimple-Adapter installeren voor SharePoint
Hallo te volgen procedure tooupgrade SharePoint-server gebruiken en StorSimple-Adapter installeren voor SharePoint- of toosimply upgrade of Hallo adapter in een bestaande SharePoint-serverfarm opnieuw installeren.

> [!IMPORTANT]
> Hallo volgende informatie voordat u de tooupgrade bekijken uw SharePoint-software en/of de upgrade of Hallo StorSimple-Adapter installeren voor SharePoint:
> 
> * Alle bestanden die eerder zijn verplaatst tooexternal opslag via de Resourcestructuur worden pas beschikbaar Hallo-installatie is voltooid en Hallo Resourcestructuur functie is weer ingeschakeld. toolimit gebruiker invloed, voert u een upgrade of herinstallatie tijdens een geplande onderhoudsvenster.
> * Hallo-tijd die nodig is voor upgrade Hallo/opnieuw installeren kan variëren, afhankelijk van het totale aantal SharePoint-databases in SharePoint-serverfarm Hallo Hallo.
> * Nadat de upgrade Hallo/installatie is voltooid, moet u tooenable Resourcestructuur voor inhoudsdatabases Hallo. Zie [Resourcestructuur configureren](#configure-rbs) voor meer informatie.
> * Als u Resourcestructuur configureert voor een SharePoint-farm met een zeer groot aantal databases (groter dan 200), Hallo **SharePoint Centraal beheer** pagina mogelijk time-out. Als dit het geval is, moet u Hallo pagina vernieuwen. Dit heeft geen invloed op Hallo-configuratieproces.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>StorSimple-Adapter voor SharePoint verwijderen
Hallo volgen procedures beschrijven hoe toomove Hallo BLOBs back-inhoud toohello SQL Server-databases en verwijder StorSimple Adapter Hallo voor SharePoint. 

> [!IMPORTANT]
> U hebt toomove Hallo BLOBs back toohello inhoudsdatabases voordat u Hallo adaptersoftware verwijderen.


### <a name="before-you-begin"></a>Voordat u begint
Hallo volgende informatie voordat u verdergaat Hallo gegevens back-inhoud toohello SQL Server-databases en beginnen met Hallo adapter verwijderen verzamelen:

* Hallo-namen van alle Hallo databases waarvoor Resourcestructuur is ingeschakeld
* Hallo UNC-pad van Hallo bloblarchief geconfigureerd

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Hallo BLOBs back toohello inhoudsdatabases verplaatsen
Voordat u Hallo StorSimple Adapter voor SharePoint-software verwijdert, moet u alle BLOBs die inhoud externalized back toohello SQL Server-databases zijn Hallo migreren. Als u toouninstall hello StorSimple Adapter voor SharePoint probeert voordat u alle Hallo BLOBs back toohello inhoudsdatabases verplaatst, ziet u Hallo waarschuwingsbericht te volgen.

![Waarschuwingsbericht](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello BLOBs back toohello inhoudsdatabases
1. Elk van de objecten Hallo externalized downloaden.
2. Open Hallo **SharePoint Centraal beheer** pagina en te bladeren**systeeminstellingen**.
3. Onder **Azure StorSimple**, klikt u op **StorSimple-Adapter configureren**.
4. Op Hallo **StorSimple-Adapter configureren** pagina, klikt u op Hallo **uitschakelen** knop onder elke Hallo inhoudsdatabases die u wilt dat tooremove van externe BLOB-opslag. 
5. Hallo-objecten verwijderen uit SharePoint en vervolgens opnieuw uploaden.

U kunt ook Microsoft hello gebruiken` RBS Migrate()` PowerShell-cmdlet die deel uitmaakt van SharePoint. Zie voor meer informatie [inhoud migreert van of naar Resourcestructuur](https://technet.microsoft.com/library/ff628255.aspx).

Nadat u Hallo BLOBs back toohello inhoud van de database verplaatst, gaat u de volgende stap toohello: [verwijderen Hallo adapter](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Hallo-adapter verwijderen
Nadat u Hallo BLOBs back toohello SQL Server inhoudsdatabases verplaatst, gebruikt u een Hallo opties toouninstall hello StorSimple Adapter voor SharePoint te volgen.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>toouse hello installatie programma toouninstall Hallo adapter
1. Gebruik een account met administrator-bevoegdheden toolog op toohello (WFE)-webserver.
2. Dubbelklik op Hallo StorSimple Adapter voor SharePoint-installatieprogramma. Hallo-installatiewizard wordt gestart.
   
    ![Wizard Setup](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Klik op **Volgende**. Hallo na pagina wordt weergegeven.
   
    ![Setup-wizardpagina verwijderen](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Klik op **verwijderen** tooselect Hallo verwijderingsproces. Hallo na pagina wordt weergegeven.
   
    ![Bevestigingspagina voor Setup-wizard](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Klik op **verwijderen** tooconfirm Hallo verwijderen. Hallo volgende op de voortgangspagina wordt weergegeven.
   
    ![Voortgangspagina van Setup-wizard](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Als het Hallo-verwijdering is voltooid, weergegeven Hallo voltooiingspagina. Klik op **voltooien** tooclose Hallo installatiewizard.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>toouse hello Configuratiescherm toouninstall Hallo adapter
1. Hallo Configuratiescherm openen en klik vervolgens op **programma's en onderdelen**.
2. Selecteer **StorSimple-Adapter voor SharePoint**, en klik vervolgens op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
