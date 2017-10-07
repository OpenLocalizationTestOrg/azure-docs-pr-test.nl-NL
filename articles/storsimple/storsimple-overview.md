---
title: overzicht van de oplossing aaaStorSimple 8000 series | Microsoft Docs
description: Beschrijft StorSimple lagen, Hallo apparaat virtueel apparaat, services en opslagbeheer en introduceert belangrijke termen die in StorSimple gebruikt.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>StorSimple 8000-serie: een hybride cloud-opslagoplossing
## <a name="overview"></a>Overzicht
Welkom tooMicrosoft Azure StorSimple, een geïntegreerde opslagoplossing die opslagtaken tussen on-premises apparaten en Microsoft Azure cloud-opslag beheert. StorSimple is een efficiënte, rendabele en eenvoudig beheerbare storage area network (SAN) oplossing die veel Hallo problemen en kosten in verband met enterprise-opslag en gegevensbeveiliging. Het Hallo bedrijfseigen StorSimple 8000 series apparaat gebruikt, kan worden geïntegreerd met cloudservices en biedt een set van beheerhulpprogramma's voor een naadloze weergave van alle Ondernemingsopslag, met inbegrip van cloud-opslag. (StorSimple-implementatiegegevens Hallo gepubliceerd op Hallo Microsoft Azure-website van de toepassing tooStorSimple 8000 series alleen apparaten. Als u van een apparaat StorSimple 5000/7000-serie gebruikmaakt, gaat u verder te[StorSimple Help](http://onlinehelp.storsimple.com/).)

Maakt gebruik van StorSimple [opslaglagen](#automatic-storage-tiering) toomanage opgeslagen gegevens op verschillende opslagmedia. de huidige werkset Hello wordt lokaal opgeslagen op Solid-State stations (SSD's), gegevens die minder vaak wordt gebruikt, worden opgeslagen op de harde schijven (HDD's) en archivering van gegevens wordt doorgeschoven, toohello cloud. Bovendien StorSimple maakt gebruik van gegevensontdubbeling en compressie tooreduce Hallo hoeveelheid opslagruimte die gegevens Hallo verbruikt. Voor meer informatie gaat te[Gegevensontdubbeling en compressie](#deduplication-and-compression). Ga te voor definities van andere belangrijkste termen en concepten die worden gebruikt in Hallo StorSimple 8000 series documentatie,[StorSimple terminologie](#storsimple-terminology) aan Hallo einde van dit artikel.

Daarnaast toostorage management, functies voor gegevensbeveiliging StorSimple inschakelen u toocreate op aanvraag en geplande back-ups en deze lokaal of in Hallo cloud opslaan. Back-ups zijn gemaakt in Hallo formulier incrementele momentopnamen, wat betekent dat ze worden gemaakt en snel hersteld. Cloudmomentopnamen is zeer belangrijk in herstel na noodgevallen, omdat ze secundaire opslagsystemen (zoals tapeback-up vervangen) en kunnen u toorestore gegevens tooyour datacenter of tooalternate sites indien nodig.

![video-pictogram](./media/storsimple-overview/video_icon.png) Bekijk de video Hallo voor een korte inleiding tooMicrosoft Azure StorSimple.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>Waarom StorSimple gebruiken?
Hallo volgende tabel beschrijft enkele Hallo belangrijkste voordelen van Microsoft Azure StorSimple biedt.

| Functie | Voordeel |
| --- | --- |
| Transparante-integratie |Hallo iSCSI-protocol tooinvisibly koppeling gegevens met opslagruimten gebruikt. Dit zorgt ervoor dat gegevens die zijn opgeslagen in de cloud Hallo Hallo datacenter, of op externe servers weergegeven toobe opgeslagen op één locatie. |
| Lagere opslagkosten |Voldoende lokale toewijst of cloud opslag toomeet huidige behoeften en breidt cloud-opslag alleen indien nodig. Dit vermindert verder de opslagvereisten en onkosten doordat redundante versies van Hallo dezelfde gegevens (Ontdubbeling) en door het gebruik van compressie. |
| Vereenvoudigd opslagbeheer |Biedt system administration tools tooconfigure en gegevens die zijn opgeslagen op locatie, op een externe server, en in de cloud Hallo beheren. Bovendien kunt u back-up beheren en functies herstellen vanuit een module Microsoft Management Console (MMC).|
| Verbeterde noodherstel en naleving |Vereist geen uitgebreide hersteltijd. In plaats daarvan worden hersteld gegevens nodig is. Dit betekent dat met het normale bewerkingen kunnen doorgaan met minimale onderbrekingen. Bovendien kunt u beleidsregels toospecify back-upschema en bewaren van gegevens. |
| Gegevensmobiliteit |Gegevens geüpload tooMicrosoft Azure cloud services toegankelijk is vanaf andere sites voor herstel- en migratiedoeleinden. Bovendien kunt u StorSimple tooconfigure StorSimple Cloud toestellen op virtuele machines (VM's) in Microsoft Azure wordt uitgevoerd. Hallo VM's kunt virtuele apparaten tooaccess opgeslagen gegevens vervolgens gebruiken voor test- of herstel. |
| Bedrijfscontinuïteit |Kan StorSimple 5000 7000-serie gebruikers toomigrate hun gegevens tooa StorSimple 8000 series apparaat. |
| Beschikbaarheid in hello Azure Government Portal |StorSimple is beschikbaar in hello Azure Government Portal. Zie voor meer informatie [implementeren van uw on-premises StorSimple-apparaat in Hallo Government Portal](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Gegevensbescherming en beschikbaarheid |Hallo StorSimple 8000-serie ondersteunt Zone redundante opslag (ZRS), in aanvulling tooLocally redundante opslag (LRS) en geografisch redundante opslag (GRS). Raadpleeg te[in dit artikel over Azure Storage redundantieopties](https://azure.microsoft.com/documentation/articles/storage-redundancy/) voor ZRS meer informatie. |
| Ondersteuning voor kritieke toepassingen |StorSimple kunt die u relevante volumes identificeren als een lokaal vastgemaakt die op zijn beurt zorgt ervoor dat gegevens die nodig zijn voor kritieke toepassingen niet gelaagde toohello cloud. Lokaal vastgemaakte volumes zijn niet onderwerp toocloud latenties of problemen met de netwerkverbinding. Zie voor meer informatie over lokaal vastgemaakte volumes [hello StorSimple Apparaatbeheer service toomanage volumes gebruiken](storsimple-8000-manage-volumes-u2.md). |
| Lage latentie en hoge prestaties |U kunt de cloud-toepassingen die van Hallo hoge prestaties, lage latentie functies van Azure premium-opslag gebruikmaken maken. Zie voor meer informatie over StorSimple premium cloud toestellen [implementeren en beheren van een StorSimple-Cloud-toestel in Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>StorSimple-onderdelen
Hallo Microsoft Azure StorSimple-oplossing omvat Hallo volgende onderdelen:

* **Microsoft Azure StorSimple-apparaat** – een lokale hybride-opslagmatrix die SSD en HDD's, samen met automatische failover-mogelijkheden en redundante controllers bevat. Hallo-controllers beheren opslag in lagen, het plaatsen van momenteel gebruikte (of hot) gegevens op de lokale opslag (in Hallo apparaat of on-premises servers), tijdens het verplaatsen van minder vaak gebruikte gegevens toohello cloud.
* **StorSimple Cloud toestel** – ook wel bekend als Hallo virtueel StorSimple-apparaat, is dit een softwareversie van Hallo StorSimple-apparaat die Hallo-architectuur repliceert en de meeste mogelijkheden van Hallo fysieke hybride opslagapparaat. Hallo StorSimple Cloud toestel op één knooppunt in Azure een virtuele machine wordt uitgevoerd. Premium virtuele apparaten die van Azure premium-opslag gebruikmaken, zijn beschikbaar in Update 2 en hoger.
* **StorSimple-apparaat Manager-service** – een uitbreiding van hello Azure-portal waarmee u een StorSimple-apparaat of StorSimple Cloud toestel beheren via een enkel webinterface. U kunt Hallo Apparaatbeheer StorSimple-service toocreate gebruiken en services beheren, en apparaten beheren, waarschuwingen weergeven, volumes, beheren en weergeven en weergeven en beheren back-upbeleid Hallo back-upcatalogus.
* **Windows PowerShell voor StorSimple** – een opdrachtregelinterface waarmee u kunt toomanage Hallo StorSimple-apparaat. Windows PowerShell voor StorSimple bevat functies waarmee u tooregister uw StorSimple-apparaat, Hallo netwerkinterface configureren op uw apparaat, bepaalde typen updates installeren, het apparaat oplossen door het Hallo support-sessie openen en Hallo wijzigen status van het apparaat. U kunt Windows PowerShell voor StorSimple openen door de verbindende toohello seriële console of via Windows PowerShell op afstand.
* **Azure PowerShell StorSimple-cmdlets** : een verzameling van Windows PowerShell-cmdlets waarmee u tooautomate serviceniveau en de migratie taken van Hallo vanaf de opdrachtregel. Ga voor meer informatie over hello Azure PowerShell-cmdlets voor StorSimple toohello [cmdlet-verwijzing](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **StorSimple Snapshot Manager** – een MMC-module die gebruikmaakt van volume groepen en Hallo Windows Volume Shadow Copy Service toogenerate toepassingsconsistente back-ups. U kunt bovendien gebruiken StorSimple Snapshot Manager toocreate back-upschema en klonen of herstel van volumes.
* **StorSimple-Adapter voor SharePoint** – een hulpprogramma dat transparant tooSharePoint serverfarms, Microsoft Azure StorSimple-opslag en gegevensbeveiliging breidt tijdens het maken van StorSimple opslag worden bekeken en beheerd via Hallo SharePoint Centraal Beheerportal.

Hallo diagram hieronder biedt een weergave op hoog niveau van Hallo Microsoft Azure StorSimple-architectuur en onderdelen.

![StorSimple-architectuur](./media/storsimple-overview/overview-big-picture.png)

Hallo volgende secties beschrijven elk van deze onderdelen in meer detail en wordt uitgelegd hoe Hallo oplossing rangschikt gegevens, wijst opslag en vereenvoudigt het beheer van opslag en gegevensbeveiliging. de laatste sectie Hallo bevat definities voor een aantal Hallo belangrijke termen en concepten tooStorSimple verwante onderdelen en het beheer ervan.

## <a name="storsimple-device"></a>StorSimple-apparaat
Hallo Microsoft Azure StorSimple-apparaat is een lokale hybride-opslagmatrix die voorziet in primaire opslag- en iSCSI-toegang toodata opgeslagen. Deze communicatie met de cloudopslag wordt beheerd en helpt tooensure Hallo beveiligings- en vertrouwelijkheid van alle gegevens die zijn opgeslagen op Hallo van Microsoft Azure StorSimple-oplossing.

Hallo StorSimple-apparaat bevat SSD en HDD's van harde schijven, evenals ondersteuning voor clustering en automatische failover. Het bevat een gedeelde processor, gedeelde opslag en twee gespiegelde controllers. Elke domeincontroller biedt Hallo volgende:

* Verbinding tooa hostcomputer
* Toosix netwerk poorten tooconnect toohello local area network (LAN)
* Hardwarebewaking
* Niet-vluchtige RAM-geheugen (NVRAM) waarin informatie behouden, zelfs als de stroom wordt onderbroken
* Clusterbewust bijwerken van toomanage software-updates op servers in een failovercluster zodat Hallo updates minimale hebben of niet van invloed op de beschikbaarheid van de service
* Cluster-service, welke functies, zoals een back-end-cluster, bieden hoge beschikbaarheid en voor het minimaliseren van een nadelige effecten die optreden kunnen als een harde schijf of de SSD uitvalt of offline gehaald

Slechts één domeincontroller is actief op elk gewenst moment in de tijd. Als de actieve controller Hallo mislukt, actief de tweede controller Hallo automatisch.

Voor meer informatie gaat te[StorSimple hardwareonderdelen en status](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>StorSimple Cloud Appliance
U kunt StorSimple toocreate een cloud-apparaat die Hallo-architectuur en mogelijkheden van Hallo fysieke hybride opslagapparaat repliceert. Hallo StorSimple Cloud toestel (ook wel bekend als hello virtueel StorSimple-apparaat) wordt uitgevoerd op één knooppunt in Azure een virtuele machine. (Een cloud-apparaat kan alleen worden gemaakt op een virtuele machine van Azure. U kunt geen maken op een StorSimple-apparaat of een on-premises server.)

Hallo cloud toestel heeft Hallo volgende kenmerken:

* Het gedraagt zich als een fysieke apparaat en een iSCSI interface toovirtual machines in de cloud Hallo kunt aanbieden.
* U kunt een onbeperkt aantal cloud toestellen in Hallo cloud maken en deze in en uit te schakelen indien nodig.
* Het kan helpen bij het simuleren van on-premises omgevingen herstel na noodgevallen, ontwikkeling en Testscenario's en kan helpen bij het ophalen van back-ups op itemniveau.

Hallo StorSimple Cloud toestel is beschikbaar in twee modellen: Hallo 8010-apparaat (voorheen bekend als Hallo 1100 model) en Hallo 8020 apparaat. Hallo 8010 apparaat heeft een maximale capaciteit van 30 TB. Hallo 8020-apparaat dat gebruikmaakt van Azure premium-opslag, heeft een maximale capaciteit van 64 TB. (In de lokale lagen Azure premium-opslag gegevens opgeslagen op SSD's dat standaardopslag gegevens op HDD's slaat.) Houd er rekening mee dat u een Azure premium storage-account toouse premium-opslag nodig hebt. Voor meer informatie over de premium-opslag, gaat u te[Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../storage/common/storage-premium-storage.md).

Voor meer informatie over Hallo StorSimple Cloud toestel gaat te[implementeren en beheren van een StorSimple-Cloud-toestel in Azure](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>StorSimple-apparaat Manager-service
Microsoft Azure StorSimple biedt een webgebaseerde gebruikersinterface (hello StorSimple-apparaat Manager-service) waarmee u toocentrally datacenter beheren en cloudopslag. U kunt Hallo Apparaatbeheer StorSimple-service tooperform Hallo taken te volgen:

* Systeeminstellingen voor StorSimple-apparaten configureren.
* Configureren en beheren van de beveiligingsinstellingen voor StorSimple-apparaten.
* Cloud-referenties en eigenschappen configureren.
* Configureren en beheren van volumes op een server.
* Volume groepen configureren.
* Back-up en herstellen van gegevens.
* Prestaties controleren.
* Systeeminstellingen bekijken en mogelijke problemen te identificeren.

U kunt Hallo Apparaatbeheer StorSimple-service tooperform alle beheerderstaken, behalve de waarvoor system uitvaltijd, zoals de eerste configuratie en installatie van updates.

Voor meer informatie gaat te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell voor StorSimple
Windows PowerShell voor StorSimple biedt een opdrachtregelinterface dat u kunt toocreate gebruiken en beheren van Hallo Microsoft Azure StorSimple-service en instellen en StorSimple-apparaten controleren. Het is een Windows PowerShell gebaseerde opdrachtregelinterface die specifieke cmdlets voor het beheren van uw StorSimple-apparaat bevat. Windows PowerShell voor StorSimple bevat functies waarmee u kunt:

* Een apparaat registreren.
* Hallo-netwerkinterface configureren op een apparaat.
* Bepaalde typen updates installeren.
* Los problemen met uw apparaat met het openen van Hallo support-sessie.
* Hallo Apparaatstatus wijzigen.

U kunt Windows PowerShell voor StorSimple openen vanaf een seriële console (op een host computer die rechtstreeks zijn aangesloten apparaat toohello) of op afstand via Windows PowerShell op afstand. Houd er rekening mee dat sommige Windows PowerShell voor StorSimple taken, zoals initiële apparaatregistratie, kan alleen worden uitgevoerd op de seriële console Hallo.

Voor meer informatie gaat te[gebruik Windows PowerShell voor StorSimple tooadminister uw apparaat](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>Azure PowerShell StorSimple-cmdlets
Hallo StorSimple van Azure PowerShell-cmdlets zijn een verzameling van Windows PowerShell-cmdlets waarmee u tooautomate serviceniveau- en migratietaken vanaf de opdrachtregel Hallo. Ga voor meer informatie over hello Azure PowerShell-cmdlets voor StorSimple toohello [cmdlet-verwijzing](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>StorSimple Snapshot Manager
StorSimple Snapshot Manager is een Microsoft Management Console (MMC) module waarmee u toocreate consistente, punt in tijd back-ups van lokale kunt en cloudgegevens. Hallo-module wordt uitgevoerd op een host op basis van Windows Server. U kunt StorSimple Snapshot Manager te gebruiken:

* Configureer back-up en volumes verwijderen.
* Volume configureert tooensure groepen waarvan een back-up van gegevens is toepassingsconsistente.
* Back-upbeleid beheren, zodat gegevens een back-up op een vooraf vastgestelde planning en in een bepaalde locatie opgeslagen (lokaal of in de cloud Hallo).
* Volumes en afzonderlijke bestanden terugzetten.

Back-ups worden vastgelegd als momentopnamen die vastleggen alleen Hallo wijzigingen sinds de laatste momentopname Hallo is gemaakt en veel minder opslagruimte dan volledige back-ups vereisen. U kunt maken van back-upschema's of directe back-ups uitvoeren indien nodig. Bovendien kunt u StorSimple Snapshot Manager tooestablish bewaarbeleid instellen die bepalen hoeveel momentopnamen worden opgeslagen. Als u later nodig hebt toorestore gegevens uit een back-up, StorSimple Snapshot Manager kunt selecteert u uit Hallo catalogus van de lokale of cloudmomentopnamen. 

Als er een ramp optreedt of als u toorestore gegevens nodig om een andere reden, StorSimple Snapshot Manager herstellen incrementeel nodig is. Het herstel van gegevens is niet vereist dat u Hallo volledige systeem afsluiten terwijl u een bestand te herstellen, apparatuur vervangen of operations tooanother site verplaatsen.

Voor meer informatie gaat te[wat is er StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>StorSimple Adapter voor SharePoint
Microsoft Azure StorSimple omvat Hallo StorSimple Adapter voor SharePoint, een optioneel onderdeel dat transparant functies tooSharePoint serverfarms StorSimple opslag en gegevensbeveiliging breidt. Hallo-adapter werkt met een externe Blob Storage planning provider en Hallo Resourcestructuur van SQL Server-functie, waardoor u toomove BLOBs tooa server back-up gemaakt door Hallo Microsoft Azure StorSimple-systeem. Microsoft Azure StorSimple slaat vervolgens de blobgegevens Hallo lokaal of in de cloud hello, op basis van gebruik.

Hallo StorSimple-Adapter voor SharePoint wordt beheerd vanuit Hallo SharePoint Centraal beheer-portal. Als gevolg daarvan kan SharePoint management blijft gecentraliseerd en alle opslag toobe in de SharePoint-farm hello wordt weergegeven.

Voor meer informatie gaat te[StorSimple-Adapter voor SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Beheer van opslagtechnologieën
Bovendien toohello toegewezen StorSimple-apparaat, virtueel apparaat en andere onderdelen, gebruikt de Microsoft Azure StorSimple Hallo software technologieën tooprovide snelle toegang toodata en tooreduce opslagverbruik te volgen:

* [Automatische opslaglagen](#automatic-storage-tiering) 
* [Thin provisioning](#thin-provisioning) 
* [Gegevensontdubbeling en compressie](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Automatische opslaglagen
Microsoft Azure StorSimple rangschikt automatisch gegevens in logische categorieën op basis van het huidige gebruik, leeftijd en tooother relatiegegevens. Gegevens die de meeste active lokaal is opgeslagen, terwijl minder actieve en inactieve gegevens automatisch wordt gemigreerd toohello cloud. Hallo volgende diagram ziet u deze benadering van gegevensopslag.

![Opslaglagen StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

Snelle toegang tooenable, StorSimple slaat zeer actieve gegevens (hot gegevens) op SSD's in Hallo StorSimple-apparaat. Gegevens die wordt gebruikt van tijd tot tijd worden opgeslagen (oefenen gegevens) op HDD's in Hallo-apparaat of op de servers in Hallo datacenter. Inactieve gegevens, back-upgegevens worden verplaatst en blijven gegevens bewaard archivering of naleving doelen toohello cloud. 

> [!NOTE]
> Bij Update 2 of hoger, kunt u een als lokaal vastgemaakt volume opgeven, in welk geval Hallo gegevens op het lokale apparaat Hallo blijft en niet is gelaagde toohello cloud. 


StorSimple aanpast en gegevens opnieuw worden ingedeeld en toewijzingen van de opslag als gebruikspatronen wijzigen. Sommige gegevens kan bijvoorbeeld worden minder actief gedurende een bepaalde periode. Als deze actief geleidelijk minder, wordt deze is gemigreerd van SSD's tooHDDs en vervolgens toohello cloud. Als dat dezelfde gegevens opnieuw geactiveerd wordt, is het gemigreerde back toohello opslagapparaat.

Hallo opslag lagen proces verloopt als volgt:

1. Een systeembeheerder stelt u een opslagaccount van de Microsoft Azure-cloud.
2. Hallo beheerder gebruikt Hallo seriële console en Hallo StorSimple-apparaat Manager service (actief in hello Azure-portal) tooconfigure Hallo apparaat en de bestandsnaam server, volumes en gegevens protection-beleid maken. Lokale machines (zoals bestandsservers) gebruiken Hallo Internet Small Computer System Interface (iSCSI) tooaccess hello StorSimple-apparaat.
3. In eerste instantie opslaat StorSimple-gegevens op Hallo snelle SSD-laag van Hallo-apparaat.
4. Als Hallo capaciteit SSD-laag benaderingen, StorSimple deduplicates Hallo oudste gegevensblokken worden gecomprimeerd en ze toohello HDD-laag verplaatst.
5. Als Hallo benaderingen-capaciteit van HDD-laag, StorSimple codeert Hallo oudste gegevensblokken en stuurt ze veilig toohello Microsoft Azure storage-account via HTTPS.
6. Microsoft Azure maakt meerdere replica's van Hallo gegevens in het datacenter en op een externe datacenter, waarbij u ervoor zorgt dat Hallo gegevens kunnen worden hersteld als een noodsituatie voordoet.
7. Hallo bestandsserver gegevens opgeslagen in de cloud Hallo aanvraagt, StorSimple naadloos retourneert als een kopie opgeslagen op Hallo SSD-laag van Hallo StorSimple-apparaat.

#### <a name="how-storsimple-manages-cloud-data"></a>Hoe StorSimple cloudgegevens beheert

StorSimple deduplicates klantgegevens voor alle Hallo momentopnamen en Hallo primaire gegevens (gegevens geschreven door hosts). Ontdubbeling is ideaal voor de opslagruimte, maakt het Hallo-vraag van 'Wat is in de cloud Hallo' ingewikkeld. Hallo overlappen gelaagde gegevens van de primaire en Hallo momentopname met elkaar. Hoeveelheid gegevens in de cloud Hallo één kan worden gebruikt als gelaagde primaire gegevens, en ook naar worden verwezen door meerdere momentopnamen. Elke cloudmomentopname zorgt ervoor dat een kopie van alle gegevens van Hallo punt in tijd is vergrendeld in de cloud Hallo tot momentopname worden verwijderd.

Gegevens worden alleen van Hallo cloud verwijderd wanneer er geen verwijzingen toothat gegevens. Bijvoorbeeld, als er een cloudmomentopname alle Hallo-gegevens van die Hallo StorSimple-apparaat en verwijder vervolgens de primaire gegevens, zou zien we Hallo _primaire gegevens_ onmiddellijk te verwijderen. Hallo _cloudgegevens_ waaronder Hallo gelaagde gegevens en back-ups hello, blijft dezelfde Hallo. Dit is omdat er een momentopname nog verwijzen naar Hallo cloudgegevens. Na het Hallo cloud momentopname is verwijderd (en andere momentopname waarnaar wordt verwezen Hallo dezelfde gegevens), cloud verbruik verwijdert. Voordat we cloudgegevens verwijdert, wordt er gecontroleerd of er zijn geen momentopnamen nog steeds verwijzen naar die gegevens. Dit proces wordt genoemd _garbagecollection_ en een achtergrondservice wordt uitgevoerd op Hallo-apparaat. Verwijderen van cloudgegevens is niet direct Hallo garbagecollection verzameling service controleert op andere verwijzingen naar toothat gegevens vóór Hallo verwijdering. Hallo snelheid van de garbage collector is afhankelijk van Hallo totale aantal momentopnamen en Hallo totale gegevens. Normaal gesproken Hallo cloudgegevens opgeschoond in minder dan een week.


### <a name="thin-provisioning"></a>Thin provisioning
Thin provisioning is een virtualisatietechnologie voor het waarin beschikbare opslag tooexceed fysieke resources weergegeven. In plaats van voldoende opslagruimte van tevoren reserveren, StorSimple maakt gebruik van thin provisioning tooallocate net voldoende ruimte toomeet actuele vereisten. Hallo elastische aard van cloud-opslag vergemakkelijkt deze benadering omdat StorSimple kunt vergroten of verkleinen van veranderende verzoeken voor toomeet cloud-opslag.

> [!NOTE]
> Lokaal vastgemaakte volumes zijn niet dun ingericht. Opslag die is toegewezen tooa lokale alleen-lezen volume is ingericht in zijn geheel wanneer Hallo volume wordt gemaakt.


### <a name="deduplication-and-compression"></a>Gegevensontdubbeling en compressie
Microsoft Azure StorSimple maakt gebruik van Ontdubbeling en gegevens compressie toofurther verminderen de opslagvereisten.

Ontdubbeling vermindert Hallo totale hoeveelheid gegevens die zijn opgeslagen doordat redundantie in de gegevensset Hallo opgeslagen. Omdat informatie wordt gewijzigd, StorSimple Hallo ongewijzigd gegevens negeert en opnamen Hallo alleen wijzigingen. StorSimple vermindert bovendien Hallo en de hoeveelheid opgeslagen gegevens door het identificeren en onnodige gegevens verwijderen. 

> [!NOTE]
> Gegevens op lokaal vastgemaakte volumes is niet ontdubbeld of gecomprimeerd. Back-ups van lokaal vastgemaakte volumes zijn echter ontdubbeld en gecomprimeerd.


## <a name="storsimple-workload-summary"></a>StorSimple workloadoverzicht
Hieronder wordt een samenvatting van Hallo ondersteund StorSimple werkbelastingen in een tabel.

| Scenario | Workload | Ondersteund | Beperkingen | Versie |
| --- | --- | --- | --- | --- |
| Samenwerking |Delen van bestanden |Ja | |Alle versies |
| Samenwerking |Gedistribueerde bestanden delen |Ja | |Alle versies |
| Samenwerking |SharePoint |Ja* |Alleen ondersteund met lokaal vastgemaakte volumes |Update 2 en hoger |
| Archivering |Eenvoudige bestand archiveren |Ja | |Alle versies |
| Virtualisatie |Virtuele machines |Ja* |Alleen ondersteund met lokaal vastgemaakte volumes |Update 2 en hoger |
| Database |SQL |Ja* |Alleen ondersteund met lokaal vastgemaakte volumes |Update 2 en hoger |
| Videobewaking |Videobewaking |Ja* |Ondersteund wanneer de StorSimple-apparaat is toegewezen alleen toothis werkbelasting |Update 2 en hoger |
| Back-up |Back-up van primaire doel |Ja* |Ondersteund wanneer de StorSimple-apparaat is toegewezen alleen toothis werkbelasting |Update 3 en hoger |
| Back-up |Back-up van secundaire doel |Ja* |Ondersteund wanneer de StorSimple-apparaat is toegewezen alleen toothis werkbelasting |Update 3 en hoger |

*Ja &#42; -Oplossing richtlijnen en beperkingen worden toegepast.*

Hallo volgende van werkbelastingen worden niet ondersteund door apparaten StorSimple 8000-serie. Als op de StorSimple wordt geïmplementeerd, wordt deze werkbelastingen leidt tot een niet-ondersteunde configuratie.

* Medische imaging
* Exchange
* VDI
* Oracle
* SAP
* Big data
* Distributie van inhoud
* Opstarten vanaf een SCSI

Hier volgt een lijst met onderdelen van de infrastructuur Hallo StorSimple ondersteund.

| Scenario | Workload | Ondersteund | Beperkingen | Versie |
| --- | --- | --- | --- | --- |
| Algemeen |ExpressRoute |Ja | |Alle versies |
| Algemeen |DataCore FC |Ja* |Ondersteund met DataCore SANsymphony |Alle versies |
| Algemeen |DFSR |Ja* |Alleen ondersteund met lokaal vastgemaakte volumes |Alle versies |
| Algemeen |Indexeren |Ja* |Voor gelaagde volumes alleen metagegevens indexeren wordt ondersteund (geen gegevens).<br>Voor lokaal vastgemaakte volumes wordt volledige indexering ondersteund. |Alle versies |
| Algemeen |Antivirusprogramma 's |Ja* |Voor gelaagde volumes wordt alleen scan Open en close ondersteund.<br> Voor lokaal vastgemaakte volumes, wordt volledige scan ondersteund. |Alle versies |

*Ja &#42; -Oplossing richtlijnen en beperkingen worden toegepast.*

Hier volgt een lijst met andere software die worden gebruikt met StorSimple toobuild oplossingen.

| Type werkbelasting | Software die worden gebruikt met StorSimple | Ondersteunde versies|Koppeling toosolution handleiding| 
| --- | --- | --- | --- |
| Back-updoel |Veeam |Veeam v 9 en hoger |[StorSimple als een back-updoel met Veaam](storsimple-configure-backup-target-veeam.md)|
| Back-updoel |Veritas Backup Exec |Back-up uitvoeren / 16 en hoger |[StorSimple als een back-updoel met Backup Exec](storsimple-configure-backup-target-using-backup-exec.md)|
| Back-updoel |VERITAS NetBackup |NetBackup 7.7.x en hoger  |[StorSimple als een back-updoel met NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Globale bestanden delen <br></br> Samenwerking |Talon  |[StorSimple met Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>StorSimple-terminologie
Voordat u uw Microsoft Azure StorSimple-oplossing implementeert, wordt aangeraden dat u lees Hallo volgende termen en definities.

### <a name="key-terms-and-definitions"></a>Belangrijkste termen en definities
| Term (acroniem of afkorting) | Beschrijving |
| --- | --- |
| record voor toegangscontrole (ACR) |Een record die is gekoppeld aan een volume op uw Microsoft Azure StorSimple-apparaat waarmee wordt bepaald welke hosts verbinding kunnen maken van tooit. Hallo bepaling is gebaseerd op Hallo iSCSI Qualified Name (IQN) (opgenomen in Hallo ACR) Hallo-hosts die verbinding tooyour StorSimple-apparaat maken. |
| AES-256 |Een Advanced Encryption Standard (AES) 256-bits-algoritme voor het versleutelen van gegevens, zoals het tooand van Hallo cloud wordt verplaatst. |
| grootte van toewijzingseenheid (AUS) |Hallo kleinste hoeveelheid schijfruimte die kan worden toegewezen toohold een bestand in uw Windows-bestandssystemen. Als de bestandsgrootte van een niet een veelvoud van Hallo clustergrootte is, extra ruimte moet gebruikte toohold Hallo-bestand (up toohello volgende veelvoud van Hallo clustergrootte) waardoor verloren ruimte en fragmentatie van Hallo harde schijf. <br>Hallo aanbevolen dat AUS voor Azure StorSimple-volumes is 64 KB omdat deze goed samen met de Hallo Ontdubbeling algoritmen werkt. |
| geautomatiseerde opslaglagen |Minder actieve gegevens automatisch het verplaatsen van SSD's tooHDDs en vervolgens tooa laag in Hallo cloud en het beheer van alle opslag van een centrale gebruikersinterface in te schakelen. |
| Back-upcatalogus |Een verzameling van back-ups, meestal gekoppeld door Hallo toepassingstype dat is gebruikt. Deze verzameling wordt weergegeven in de blade back-upcatalogus Hallo Hallo Apparaatbeheer StorSimple-service UI. |
| back-catalogusbestand |Een bestand met een lijst met beschikbare momentopnamen die momenteel zijn opgeslagen in Hallo back-updatabase van StorSimple Snapshot Manager. |
| back-upbeleid |Een selectie van volumes, type back-up en een tijdschema waarmee u toocreate back-ups op een vooraf gedefinieerd schema. |
| binaire grote objecten (BLOB's) |Een verzameling van binaire gegevens die zijn opgeslagen als één entiteit in een databasebeheersysteem. BLOBs zijn meestal afbeeldingen, audio of andere multimedia objecten, hoewel soms binaire uitvoerbare code wordt opgeslagen als een BLOB. |
| Challenge Handshake Authentication Protocol (CHAP) |Een protocol dat tooauthenticate Hallo peer van een verbinding, op basis van Hallo peer delen van een wachtwoord of geheim. CHAP kan eenzijdige of wederzijdse zijn. Met één richting CHAP, wordt een initiator Hallo doel geverifieerd. Wederzijdse CHAP moet Hallo doel Hallo initiator verifiëren en dat initiator Hallo Hallo doel verifieert. |
| kloon |Een kopie van een volume. |
| Cloud als een laag (CaaT) |Cloudopslag geïntegreerd als een laag binnen Hallo opslagarchitectuur zodat alle opslag toobe deel uitmaken van een onderneming opslagnetwerk wordt weergegeven. |
| cloud serviceprovider (CSP) |Een provider van services voor cloudcomputing. |
| cloudmomentopname |Een punt in tijd kopie van gegevens van het volume dat is opgeslagen in de cloud Hallo. Een cloudmomentopname is gelijk tooa momentopname op een andere, externe opslagsysteem gerepliceerd. Cloudmomentopnamen zijn bijzonder nuttig voor herstel na noodgevallen. |
| coderingssleutel voor cloudopslag |Een wachtwoord of een sleutel die wordt gebruikt door uw StorSimple-apparaat tooaccess Hallo versleutelde gegevens verzonden door uw apparaat toohello cloud. |
| clusterbewust bijwerken |Het beheren van software-updates op servers in een failovercluster zodat Hallo updates minimale hebben of niet van invloed op de beschikbaarheid van de service. |
| gegevenspad |Een verzameling functionele eenheden die onderling verbonden gegevensverwerking bewerkingen uitvoeren. |
| deactiveren |Een permanente actie dat einden verbinding tussen Hallo StorSimple-apparaat en Hallo Hallo gekoppelde service in de cloud. Cloudmomentopnamen van Hallo apparaat kunnen blijven na dit proces en worden gekloond of gebruikt voor herstel na noodgevallen. |
| het spiegelen van de schijf |Replicatie van de logische schijfvolumes op afzonderlijke vaste schijven in realtime tooensure continue beschikbaarheid. |
| dynamische schijf spiegelen |Replicatie van de logische schijfvolumes op dynamische schijven. |
| dynamische schijven |Een volume schijfindeling dat wordt gebruikt Hallo toostore Logical Disk Manager (LDM) en gegevens over meerdere fysieke schijven te beheren. Dynamische schijven vergrote tooprovide meer ruimte vrij kan worden. |
| Uitgebreide Bunch van schijven (EBOD) behuizing |Een secundaire behuizing van uw Microsoft Azure StorSimple-apparaat met extra harde schijf schijven voor extra opslagruimte. |
| FAT-inrichting |Een conventionele opslaginrichting in welke opslag wordt ruimte toegewezen op basis van behoeften verwacht (en meestal valt buiten het huidige behoefte Hallo). Zie ook *thin provisioning,*. |
| harde schijf (HDD) |Een station dat gebruikmaakt van draaiende platen toostore gegevens. |
| hybride-cloudopslag |Een opslagarchitectuur die gebruikmaakt van lokale en externe bronnen, met inbegrip van cloud-opslag. |
| Internet Small Computer System Interface (iSCSI) |Een opslag op basis van Internet Protocol-IP-netwerken standaard voor het koppelen van de gegevens opslagapparatuur of faciliteiten. |
| iSCSI-initiator |Een softwareonderdeel waarmee een hostcomputer waarop Windows tooconnect tooan externe opslag op basis van iSCSI-netwerk wordt uitgevoerd. |
| iSCSI Qualified Name (IQN) |Een unieke naam die een iSCSI-doel of de initiator aangeeft. |
| iSCSI-doel |Een softwareonderdeel dat gecentraliseerd iSCSI schijfsubsystemen in een storage area network biedt. |
| Live archiveren |Een benadering van gegevensopslag waarmee archivering van gegevens toegankelijk alle Hallo-tijd is (deze wordt niet opgeslagen op een externe locatie op tape, bijvoorbeeld). Microsoft Azure StorSimple maakt gebruik van live archiveren. |
| lokaal vastgemaakt volume |een volume dat zich bevindt op Hallo-apparaat en nooit is gelaagd toohello cloud. |
| lokale momentopname |Een kopie van de punt in tijd van de volumegegevens die zijn opgeslagen op Hallo Microsoft Azure StorSimple-apparaat. |
| Microsoft Azure StorSimple |Een krachtige oplossing die bestaan uit een opslagapparaat datacenter- en software waarmee IT-organisaties tooleverage cloudopslag alsof het datacenter-opslag. StorSimple vereenvoudigt de bescherming van gegevens en het beheer van gegevens tijdens de kosten te verlagen. Hallo oplossing consolideert primaire herstel voor opslag, archiveren, back-up en noodherstel (DR) via naadloze integratie met Hallo cloud. StorSimple-apparaten inschakelen door een combinatie van SAN-opslag- en cloud gegevensbeheer op een platform bedrijfsniveau snelheid, eenvoud en betrouwbaarheid voor alle opslag-gerelateerde behoeften. |
| Stroom en koeling van Module (PCM) |Hardware-onderdelen van uw StorSimple-apparaat die bestaan uit Hallo voedingen en koeling ventilator, Hallo Hallo daarom de naam van stroom en koeling module. primaire behuizing Hallo Hallo apparaat heeft twee 764W PCMs terwijl Hallo EBOD behuizing twee 580 w bij PCMs heeft. |
| Primaire behuizing |Belangrijkste behuizing van uw StorSimple-apparaat met Hallo toepassing platform domeincontrollers. |
| Beoogde hersteltijd (RTO) |maximale hoeveelheid tijd die voordat een bedrijfsproces of systeem opgebruikt moet Hallo is volledig hersteld na een noodgeval. |
| seriële gekoppelde SCSI (SAS) |Een type harde schijf (HDD). |
| gegevensversleutelingssleutel van service |Een sleutel gemaakt beschikbaar tooany nieuwe StorSimple-apparaat dat wordt geregistreerd bij Hallo StorSimple-apparaat Manager-service. Hallo configuratiegegevens worden overgedragen tussen Hallo Apparaatbeheer StorSimple-service en Hallo-apparaat is versleuteld met een openbare sleutel en vervolgens alleen op Hallo-apparaat met een persoonlijke sleutel kan worden ontsleuteld. Gegevensversleutelingssleutel van service kunt Hallo service tooobtain deze persoonlijke sleutel voor ontsleuteling. |
| serviceregistratiesleutel |Zodat deze wordt weergegeven in hello Azure-portal voor verdere acties, een sleutel die helpt Hallo StorSimple-apparaat registreren bij Hallo StorSimple-apparaat Manager-service. |
| Small Computer System Interface (SCSI) |Een verzameling standaarden voor fysiek verbinden van computers en het doorgeven van gegevens. |
| Solid state schijf (SSD) |Een schijf die geen bewegende onderdelen bevat; bijvoorbeeld: een flash-station. |
| Storage-account |Een set referenties voor toegang gekoppeld tooyour storage-account voor een bepaalde cloud serviceprovider. |
| StorSimple Adapter voor SharePoint |Een Microsoft Azure StorSimple-component die transparant tooSharePoint serverfarms StorSimple opslag en gegevensbeveiliging breidt. |
| StorSimple-apparaat Manager-service |Een uitbreiding van hello Azure-portal waarmee u toomanage uw Azure StorSimple on-premises en virtuele apparaten. |
| StorSimple Snapshot Manager |Een Microsoft Management Console (MMC)-module voor het beheren van back-up en herstellen van bewerkingen in Microsoft Azure StorSimple. |
| back-up maken |Een functie waarmee Hallo gebruiker tootake een interactieve back-up van een volume. Het is een andere manier een handmatige back-up van een volume maken als tegengestelde tootaking van een automatische back-up via een gedefinieerd beleid. |
| Thin provisioning |Een methode voor het optimaliseren van welke Hello beschikbare opslagruimte wordt gebruikt in opslagsystemen Hallo-efficiëntie. Hallo-opslag is in dunne inrichting wordt toegewezen door meerdere gebruikers op basis van Hallo minimaal vereiste schijfruimte: door elke gebruiker op elk moment. Zie ook *fat inrichting*. |
| lagen |Gegevens in logische groepen op basis van het huidige gebruik, leeftijd en tooother relatiegegevens rangschikken. StorSimple rangschikt automatisch gegevens in categorieën. |
| Volume |Logische opslagplaatsen aangeboden in de vorm Hallo van stations. StorSimple-volumes overeen toohello volumes die zijn gekoppeld met de Hallo host, met inbegrip van die gedetecteerd via Hallo gebruik van iSCSI- en een StorSimple-apparaat. |
| volumecontainer |Een groepering van volumes en het Hallo-instellingen die van toepassing toothem. Alle volumes in uw StorSimple-apparaat zijn gegroepeerd in volumecontainers. Instellingen voor volume-container omvatten storage-accounts, versleutelingsinstellingen voor gegevens toocloud met bijbehorende coderingssleutels en bandbreedte voor bewerkingen met betrekking tot Hallo cloud verzonden. |
| volume-groep |In StorSimple Snapshot Manager een volume-groep is een verzameling van volumes die zijn geconfigureerd toofacilitate back-verwerking. |
| Volume Shadow Copy Service (VSS) |Een service van de Windows Server-besturingssysteem die zorgt voor een toepassing consistente door te communiceren met de VSS-bewuste toepassingen toocoordinate Hallo maken van incrementele momentopnamen. VSS zorgt ervoor dat Hallo toepassingen tijdelijk niet actief zijn wanneer momentopnamen worden gemaakt. |
| Windows PowerShell voor StorSimple |Een Windows PowerShell gebaseerde opdrachtregelinterface toooperate gebruikt en uw StorSimple-apparaat te beheren. Deze interface heeft terwijl sommige Hallo essentiële mogelijkheden van Windows PowerShell andere speciale cmdlets die zijn gericht op het beheren van een StorSimple-apparaat. |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple security](storsimple-8000-security.md).

