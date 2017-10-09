---
title: aaaManage uw StorSimple-volumes (U2) | Microsoft Docs
description: Legt uit hoe tooadd, wijzigen, bewaken en verwijderen van StorSimple-volumes en hoe tootake offline indien nodig.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Gebruik Hallo StorSimple Manager-service toomanage volumes (Update 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Manager service toocreate Hallo en beheren van volumes op Hallo StorSimple-apparaat en virtuele StorSimple-apparaat met Update 2 is geïnstalleerd.

Hallo StorSimple Manager-service is een uitbreiding in de klassieke Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface Hallo. In toevoeging toomanaging volumes, kunt u Hallo StorSimple Manager-service toocreate gebruiken en StorSimple-services beheren, weergeven en beheren van apparaten, waarschuwingen, weergeven en weergeven en beheren back-upbeleid en back-upcatalogus Hallo.

## <a name="volume-types"></a>Volumetypen
StorSimple-volumes kunnen zijn:

* **Lokaal vastgemaakte volumes**: gegevens in deze volumes blijft op de lokale StorSimple-apparaat hello te allen tijde.
* **Gelaagde volumes**: gegevens in deze volumes kunnen toohello cloud worden gelekt.

Een archivering volume is een gelaagd volume. Hallo groter Ontdubbeling chunkgrootte gebruikt voor archivering volumes kunt Hallo apparaat tootransfer groter segmenten van gegevens toohello cloud. 

Indien nodig, kunt u het volumetype Hallo van lokale tootiered of van gelaagde toolocal is ingesteld. Voor meer informatie gaat te[Hallo volumetype wijzigen](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Lokaal vastgemaakte volumes
Lokaal vastgemaakte volumes zijn volledig ingerichte volumes die gegevens toohello cloud niet laag, garanties waardoor lokale voor primaire gegevens, onafhankelijk van de verbinding van de cloud. Gegevens op lokaal vastgemaakte volumes is niet ontdubbeld en gecomprimeerd. momentopnamen van lokaal vastgemaakte volumes zijn echter ontdubbeld. 

Lokaal vastgemaakte volumes zijn volledig is ingericht; Daarom moet u voldoende ruimte hebben op uw apparaat wanneer u deze maakt. U kunt lokaal vastgemaakte volumes tooa maximale grootte van 8 TB op Hallo StorSimple 8100-apparaat en 20 TB op Hallo 8600-apparaat inrichten. StorSimple reserveert Hallo resterende lokale ruimte op het Hallo-apparaat voor momentopnamen, metagegevens en verwerken van gegevens. Kunt u vergroten Hallo van een lokaal vastgemaakt volume toohello maximaal beschikbaar, maar u kunt geen Hallo verkleining van een volume eenmaal is gemaakt.

Wanneer u een lokaal vastgemaakt volume maakt, wordt de Hallo beschikbare ruimte voor het maken van gelaagde volumes verminderd. Hallo omgekeerde geldt ook: als er bestaande gelaagde volumes, Hallo ruimte beschikbaar voor het maken van lokaal vastgemaakte volumes wordt niet lager zijn dan Hallo maximale bovenstaande grenzen. Raadpleeg voor meer informatie op lokale volumes toohello [Veelgestelde vragen op lokaal vastgemaakte volumes](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Gelaagde volumes
Gelaagde volumes zijn dun ingerichte volumes in welke Hallo vaak gebruikte gegevens lokaal op Hallo apparaat blijft en minder vaak gebruikte gegevens wordt automatisch toohello cloud gelaagde. Thin provisioning is een virtualisatietechnologie voor het waarin beschikbare opslag tooexceed fysieke resources weergegeven. In plaats van voldoende opslagruimte van tevoren reserveren, StorSimple maakt gebruik van thin provisioning tooallocate net voldoende ruimte toomeet actuele vereisten. Hallo elastische aard van cloud-opslag vergemakkelijkt deze benadering omdat StorSimple kunt vergroten of verkleinen van veranderende verzoeken voor toomeet cloud-opslag.

Als u gebruikmaakt van gelaagde volume voor de archivering van gegevens, selecteren Hallo Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje verandert Hallo Ontdubbeling chunkgrootte voor het volume too512 KB. Als u deze optie niet selecteert, wordt de Hallo overeenkomstige gelaagde volume een chunkgrootte van 64 KB gebruikt. Een grotere chunkgrootte voor Ontdubbeling kunt Hallo apparaat tooexpedite Hallo overdracht van grote hoeveelheden gegevens voor archivering toohello cloud.

> [!NOTE]
> Archivering volumes die zijn gemaakt met een vooraf Update 2-versie van StorSimple worden geïmporteerd omdat er gelaagde met Hallo archivering selectievakje ingeschakeld.
> 
> 

### <a name="provisioned-capacity"></a>Ingerichte capaciteit
Raadpleeg de volgende tabel voor maximale ingerichte capaciteit voor elk type apparaat- en volumegegevens toohello. (Houd er rekening mee dat lokaal vastgemaakte volumes niet beschikbaar op een virtueel apparaat zijn.)

|  | De grootte van maximaal gelaagde volume | Maximale lokaal vastgemaakt volumegrootte |
| --- | --- | --- |
| **Fysieke apparaten** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Virtuele apparaten** | | |
| 8010 |30 TB |N.v.t. |
| 8020 |64 TB |N.v.t. |

## <a name="hello-volumes-page"></a>de pagina Volumes Hallo
Hallo **Volumes** pagina kunt u toomanage Hallo opslagvolumes die zijn ingericht op Hallo Microsoft Azure StorSimple-apparaat voor uw initiators (servers). Hallo-lijst van volumes wordt weergegeven op uw StorSimple-apparaat.

 ![Pagina volumes](./media/storsimple-manage-volumes-u2/VolumePage.png)

Een volume bestaat uit een reeks van kenmerken:

* **Volumenaam** – een beschrijvende naam moet uniek zijn en kan Hallo volume geïdentificeerd. Deze naam wordt ook gebruikt in de bewaking van rapporten, wanneer u op een bepaald volume filtert.
* **Status** – online of offline kan zijn. Als een volume offline is, maar het is niet zichtbaar tooinitiators (servers) die toegang toouse Hallo volume zijn toegestaan.
* **Capaciteit** – Hallo totale hoeveelheid gegevens die kunnen worden opgeslagen door Hallo initiator (server). Lokaal vastgemaakte volumes volledig is ingericht en zich bevinden op Hallo StorSimple-apparaat. Gelaagde volumes zijn dun ingericht en Hallo gegevens is ontdubbeld. Met thin provisioning volumes uw apparaat niet vooraf fysieke opslagcapaciteit intern of toewijzen op Hallo-cloud op basis van de volumecapaciteit tooconfigured. Hallo volumecapaciteit is toegewezen en op verzoek gebruikt.
* **Type** – Hiermee wordt aangegeven of Hallo volume **tiers verdeelde** (Hallo standaard) of **lokaal vastgemaakt**.
* **Back-** – Hiermee wordt aangegeven of een back-standaardbeleid voor Hallo volume bestaat.
* **Toegang** – Hiermee geeft u op Hallo initiators (servers) die toegang toothis volume zijn toegestaan. Initiators die geen deel uitmaken van record voor toegangscontrole (ACR) die is gekoppeld aan het volume Hallo zichtbaar Hallo volume niet.
* **Bewaking** – Hiermee wordt aangegeven of een volume wordt bewaakt. Een volume hebt bewaking standaard ingeschakeld wanneer deze wordt gemaakt. Wordt echter bewaking wordt uitgeschakeld voor de kloon van een volume. tooenable bewaking voor een volume instructies Hallo in [bewaken van een volume](#monitor-a-volume). 

Gebruik Hallo-instructies in deze zelfstudie tooperform Hallo taken te volgen:

* Een volume toevoegen 
* Een volume wijzigen 
* Hallo-volumetype wijzigen
* Een volume verwijderen 
* Een volume offline zetten 
* Een volume bewaken 

## <a name="add-a-volume"></a>Een volume toevoegen
U [gemaakt van een volume](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) tijdens de implementatie van uw StorSimple-oplossing. Toevoegen van een volume is een vergelijkbare procedure.

#### <a name="tooadd-a-volume"></a>een volume tooadd
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer een volumecontainer in Hallo lijst en dubbelklik erop tooaccess Hallo volumes die zijn gekoppeld aan het Hallo-container.
3. Klik op **toevoegen** Hallo Hallo pagina onderaan in. Hallo wizard volume toevoegen wordt gestart.
   
     ![Wizard volume basisinstellingen toevoegen](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. In Hallo onder een wizard volume toevoegen **basisinstellingen**, Hallo te volgen:
   
   1. Geef een **naam** op voor het volume.
   2. Selecteer een **gebruikstype** uit de vervolgkeuzelijst Hallo. Selecteer voor werkbelastingen waarvoor gegevens toobe lokaal beschikbaar op Hallo apparaat te allen tijde, **lokaal vastgemaakt**. Selecteer voor alle andere typen gegevens, **tiers verdeelde**. (**Tiers verdeelde** is standaard Hallo.)
   3. Als u hebt geselecteerd **tiers verdeelde** in stap 2, kunt u Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje tooconfigure een archivering volume.
   4. Voer Hallo **ingerichte capaciteit** voor het volume in GB of TB. Zie [ingerichte capaciteit](#provisioned-capacity) voor de maximale grootte voor elk type apparaat en het volume. Bekijkt hello **beschikbare capaciteit** toodetermine hoeveel opslagruimte op het apparaat daadwerkelijk beschikbaar is.
5. Klik op het pijlpictogram Hallo![Pictogram pijl](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Als u een lokaal vastgemaakt volume configureert, ziet u Hallo-bericht te volgen.
   
    ![Tekstbericht Volume wijzigen](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Klik op het pijlpictogram Hallo ![pijlpictogram](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)opnieuw toogo toohello **extra instellingen** pagina.
   
    ![Extra instellingen van de wizard Volume toevoegen](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. Onder **extra instellingen**, Voeg een nieuwe record voor toegangscontrole (ACR):
   
   1. Selecteer een record voor toegangscontrole (ACR) in de vervolgkeuzelijst Hallo. U kunt ook een nieuwe ACR toevoegen. ACRs bepalen welke hosts hebben toegang tot de volumes met overeenkomende Hallo IQN host met die in het Hallo-record genoemd. Als u een ACR niet opgeeft, ziet u Hallo-bericht te volgen.
      
        ![ACR opgeven](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Het is raadzaam dat u Hallo selecteert **een standaardback-up voor dit volume inschakelen** selectievakje.
   3. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) toocreate hello volume Hello opgegeven instellingen.

Het nieuwe volume is nu gereed toouse.

> [!NOTE]
> Als u een lokaal vastgemaakt volume maakt en vervolgens maakt een ander lokaal vastgemaakt volume onmiddellijk daarna Hallo-taken voor het maken van volume worden opeenvolgend uitgevoerd. Hallo-taak voor het maken van eerste volume moet worden voltooid voordat het Hallo-taak voor het maken van volgende volume kan beginnen.
> 
> 

## <a name="modify-a-volume"></a>Een volume wijzigen
Een volume wijzigen wanneer u deze of wijziging hosts die toegang tot het volume Hallo Hallo tooexpand nodig.

> [!IMPORTANT]
> * Als u de volumegrootte Hallo op Hallo apparaat wijzigt, moet de volumegrootte Hallo toobe op Hallo host ook gewijzigd. 
> * hier beschreven stappen Hallo hostzijde zijn voor Windows Server 2012 (2012R2). Procedures voor het Linux- of andere hostbesturingssystemen zullen afwijken. Raadpleeg tooyour host besturingssysteem instructies bij het wijzigen van Hallo volume op een host waarop een ander besturingssysteem. 
> 
> 

#### <a name="toomodify-a-volume"></a>een volume toomodify
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer een volumecontainer in Hallo lijst en dubbelklik erop tooview Hallo volumes die zijn gekoppeld aan het Hallo-container.
3. Selecteer een volume en klik onder aan de pagina Hallo Hallo op **wijzigen**. Hallo wijzigen volume wizard wordt gestart.
4. Wijzig in Hallo wizard volume onder **basisinstellingen**, kunt u doen Hallo volgende:
   
   * Hallo bewerken **naam**.
   * Hallo converteren **gebruikstype** van lokaal vastgemaakte tootiered of van gelaagde toolocally vastgemaakt (Zie [Hallo volumetype wijzigen](#change-the-volume-type) voor meer informatie).
   * Hallo verhogen **ingerichte capaciteit**. Hallo **ingerichte capaciteit** kan alleen worden verhoogd. Nadat deze is gemaakt, kunt u een volume niet verkleinen.
5. Onder **extra instellingen**, kunt u Hallo ACR, mits Hallo volume offline is. Als Hallo volume online is, moet u tootake deze offline eerste. Raadpleeg toohello stappen in [offline zetten van een volume](#take-a-volume-offline) voorafgaande toomodifying hello ACR.
   
   > [!NOTE]
   > U kunt Hallo niet wijzigen **een standaardback-up inschakelen** optie voor het Hallo-volume.
   > 
   > 
6. Sla de wijzigingen door te klikken op het vinkje Hallo ![vinkje](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Hallo klassieke Azure-portal weergegeven een bijwerken volume bericht. Een bericht wordt weergegeven wanneer het Hallo-volume is bijgewerkt.
7. Als u een volume uitbreidt, voltooit u de volgende stappen uit op de hostcomputer Windows hello:
   
   1. Ga te**Computerbeheer** ->**Schijfbeheer**.
   2. Met de rechtermuisknop op **Schijfbeheer** en selecteer **schijven**.
   3. Selecteer in de lijst van de Hallo van schijven, Hallo volume dat u hebt bijgewerkt, klik met de rechtermuisknop en selecteer vervolgens **Volume uitbreiden**. Hallo Volume uitbreiden wizard wordt gestart. Klik op **Volgende**.
   4. Voltooi de wizard hello, accepteer de standaardwaarden Hallo. Nadat het Hallo-wizard is voltooid, moet Hallo verhoogd grootte Hallo volume worden weergegeven.
      
      > [!NOTE]
      > Als u een lokaal vastgemaakt volume uitvouwen en vouwt u vastgemaakt een ander lokaal volume onmiddellijk daarna Hallo volume uitbreiding taken worden opeenvolgend uitgevoerd. Hallo eerste volume Uitbreidingstaak moet zijn voltooid voordat Hallo volgende volume Uitbreidingstaak kan beginnen.
      > 
      > 

![Video beschikbaar](./media/storsimple-manage-volumes-u2/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe tooexpand een volume, klik op [hier](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Hallo-volumetype wijzigen
U kunt het volumetype Hallo wijzigen van gelaagde toolocally vastgemaakt of van lokaal vastgemaakte tootiered. Deze conversie mag echter geen een frequente exemplaar. Enkele redenen voor het converteren van een volume van gelaagde toolocally vastgemaakt zijn:

* Lokale garanties met betrekking tot de beschikbaarheid van gegevens en prestaties
* Afschaffing van de cloud latenties en problemen met de netwerkverbinding van de cloud.

Dit zijn meestal kleine bestaande volumes dat u wilt dat tooaccess vaak. Een lokaal vastgemaakt volume volledig is ingericht wanneer deze wordt gemaakt. Als u een gelaagd volume tooa lokaal vastgemaakt volume converteert, controleert StorSimple of dat er voldoende ruimte is op uw apparaat voordat het Hallo-conversie wordt gestart. Als er onvoldoende ruimte, ontvangt u een fout en Hallo-bewerking wordt geannuleerd. 

> [!NOTE]
> Voordat u begint met de conversie van een gelaagde toolocally vastgemaakt, ervoor zorgen dat u rekening houden met Hallo schijfruimte van andere werkbelastingen. 
> 
> 

U kunt een lokaal vastgemaakt volume tooa toochange gelaagde volume als u extra schijfruimte tooprovision nodig andere volumes. Wanneer u Hallo lokaal vastgemaakt volume tootiered converteert, verhoogt de beschikbare capaciteit op Hallo apparaat Hallo door Hallo grootte van de capaciteit Hallo uitgebracht. Als problemen met de netwerkverbinding te voorkomen dat Hallo conversie van een volume van Hallo lokale type toohello gelaagde type, hello lokaal volume zou vertonen eigenschappen van een gelaagd volume totdat Hallo conversie is voltooid. Dit komt omdat sommige gegevens toohello cloud terechtgekomen mogelijk. Deze gemorst gegevens blijven toooccupy lokale ruimte op Hallo-apparaat dat niet kan worden vrijgemaakt totdat het Hallo-bewerking wordt opnieuw gestart en voltooid.

> [!NOTE]
> Converteren van een volume kan enige tijd duren en u een conversie niet annuleren nadat deze is gestart. Hallo volume online blijft tijdens de conversie van hello, en u kunt back-ups uitvoeren, maar u niet kunt uitbreiden of Hallo volume herstelt tijdens conversie Hallo.  
> 
> 

Conversie van een gelaagde tooa lokaal vastgemaakt volume, kan een nadelige invloed heeft op de prestaties van een apparaat. Hallo volgende factoren kan bovendien Hallo duurt toocomplete Hallo conversie verhogen:

* Er is onvoldoende bandbreedte.
* Er is geen huidige back-up.

toominimize hello effecten die deze factoren kunnen hebben:

* Bekijk uw beleid voor bandbreedteregeling en zorg ervoor dat er geen speciale 40 Mbps bandbreedte beschikbaar is.
* Hallo-conversie voor daluren plannen.
* Een cloud momentopname voordat u begint met Hallo conversie.

Als u meerdere volumes (ondersteunen verschillende werkbelastingen) converteert, moet u Hallo volumeconversie prioriteren zodat volumes met hogere prioriteit eerst worden geconverteerd. Bijvoorbeeld, moet u volumes die virtuele machines (VM's) hosten of volumes met SQL-werkbelastingen converteren voordat u de volumes met file share werkbelastingen converteert.

#### <a name="toochange-hello-volume-type"></a>Hallo-volumetype toochange
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer een volumecontainer in Hallo lijst en dubbelklik erop tooview Hallo volumes die zijn gekoppeld aan het Hallo-container.
3. Selecteer een volume en klik onder aan de pagina Hallo Hallo op **wijzigen**. Hallo wijzigen volume wizard wordt gestart.
4. Op Hallo **basisinstellingen** pagina, Hallo gebruikstype wijzigen door het selecteren van de nieuwe type Hallo van Hallo **gebruikstype** vervolgkeuzelijst.
   
   * Als u Hallo type te wijzigen**lokaal vastgemaakt**, StorSimple toosee wordt gecontroleerd of er onvoldoende capaciteit is.
   * Als u Hallo type te wijzigen**tiers verdeelde** en dit volume wordt gebruikt voor archivering van gegevens, selecteer Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje.
     
       ![Archief selectievakje](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Klik op het pijlpictogram Hallo ![pijlpictogram](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **extra instellingen** pagina. Als u een lokaal vastgemaakt volume configureert, hello volgende bericht wordt weergegeven.
   
    ![Tekstbericht Volume wijzigen](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Klik op het pijlpictogram Hallo ![pijlpictogram](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) opnieuw toocontinue.
7. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) toostart hello conversieproces. een bijwerken volume bericht weergegeven met Hello Azure-portal. Een bericht wordt weergegeven wanneer het Hallo-volume is bijgewerkt.

## <a name="take-a-volume-offline"></a>Een volume offline zetten
Mogelijk moet u een volume offline tootake wanneer u van plan bent toomodify of verwijderen deze. Als een volume offline is, is het niet beschikbaar voor lees-/ schrijftoegang. U moet tootake Hallo volume offline op host hello, evenals op Hallo-apparaat. 

#### <a name="tootake-a-volume-offline"></a>een volume offline tootake
1. Zorg ervoor dat de betreffende Hallo volume is niet in gebruik voordat deze offline wordt gezet.
2. Hallo volume offline op host Hallo eerste duren. Hierdoor wordt een potentieel risico van gegevensbeschadiging op Hallo volume. Raadpleeg voor specifieke stappen toohello instructies voor het besturingssysteem van de host.
3. Nadat de host Hallo offline is, ondernemen Hallo volume Hallo apparaat offline door Hallo volgende stappen uit te voeren:
   
   1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad Hallo **Volumecontainers** lijsten in tabelvorm alle tabblad Hallo volumecontainers die gekoppeld aan het Hallo-apparaat zijn.
   2. Selecteer een volumecontainer en klik erop toodisplay Hallo lijst met alle Hallo volumes in Hallo-container.
   3. Selecteer een volume en klik op **offline zetten**.
   4. Klik op **Ja** als u om bevestiging wordt gevraagd. Hallo volume worden nu offline.
      
      Nadat een volume offline is, Hallo **Online brengen** optie beschikbaar.

> [!NOTE]
> Hallo **Offline nemen** opdracht verzendt een aanvraag toohello apparaat tootake Hallo volume offline. Als hosts nog steeds Hallo volume, resulteert dit in verbroken verbindingen maar Hallo volume offline halen niet mislukken. 
> 
> 

## <a name="delete-a-volume"></a>Een volume verwijderen
> [!IMPORTANT]
> U kunt een volume alleen verwijderen als deze offline is.
> 
> 

Volgende stappen toodelete een volume Hallo voltooien.

#### <a name="toodelete-a-volume"></a>een volume toodelete
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer Hallo volumecontainer met de gewenste toodelete Hallo-volume. Klik op Hallo volume container tooaccess hello **Volumes** pagina.
3. Alle Hallo volumes die zijn gekoppeld aan deze container worden weergegeven in tabelvorm. Controleer de status van Hallo Hallo volume dat u wilt dat toodelete. Als de gewenste toodelete Hallo-volume niet offline is, het Hallo voor offline eerste, de volgende stappen uitvoeren [offline zetten van een volume](#take-a-volume-offline).
4. Nadat het Hallo volume offline is, klikt u op **verwijderen** Hallo Hallo pagina onderaan in.
5. Klik op **Ja** als u om bevestiging wordt gevraagd. Hallo-volume wordt nu verwijderd en Hallo **Volumes** pagina ziet lijst van volumes in de container Hallo Hallo bijgewerkt.
   
   > [!NOTE]
   > Als u een lokaal vastgemaakt volume verwijdert, worden Hallo beschikbare schijfruimte voor het nieuwe volumes mogelijk niet meteen bijgewerkt. Hallo StorSimple Manager-Service-updates worden periodiek Hallo lokale ruimte beschikbaar. We raden dat u wacht enkele minuten duren voordat u toocreate Hallo nieuw volume probeert.<br> Bovendien, als u een lokaal vastgemaakt volume verwijdert en verwijdert u vervolgens een ander lokaal vastgemaakt volume onmiddellijk daarna Hallo volume verwijdering taken worden opeenvolgend uitgevoerd. Hallo-taak voor het verwijderen van eerste volume moet worden voltooid voordat Hallo volgende volume verwijderen van een taak kan beginnen.
   > 
   > 

## <a name="monitor-a-volume"></a>Een volume bewaken
Bewaking van volume, kunt u toocollect I/O-gerelateerde statistieken voor een volume. Bewaking is standaard ingeschakeld voor Hallo eerste 32 volumes die u maakt. Bewaking van extra volumes is standaard uitgeschakeld. Bewaking van de gekloonde volumes wordt ook standaard uitgeschakeld.

Volgende stappen tooenable Hallo uitvoeren of schakel bewaking voor een volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable- of uitschakelen volume bewaking
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer Hallo volumecontainer in welke Hallo volume zich bevindt en klik vervolgens op Hallo volume container tooaccess hello **Volumes** pagina.
3. Alle Hallo volumes die zijn gekoppeld aan deze container worden vermeld in Hallo in tabelvorm weergegeven. Klik op en selecteer Hallo volume of volume klonen.
4. Klik onder aan de pagina Hallo Hallo op **wijzigen**.
5. In de wizard Volume wijzigen Hallo onder **basisinstellingen**, selecteer **inschakelen** of **uitschakelen** van Hallo **bewaking** vervolgkeuzelijst.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[klonen van een StorSimple-volume](storsimple-clone-volume.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

