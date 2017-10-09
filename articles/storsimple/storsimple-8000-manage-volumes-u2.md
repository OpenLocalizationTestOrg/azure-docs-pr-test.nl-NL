---
title: aaaManage StorSimple-volumes (Update 3) | Microsoft Docs
description: Legt uit hoe tooadd, wijzigen, bewaken en verwijderen van StorSimple-volumes en hoe tootake offline indien nodig.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Gebruik Hallo Apparaatbeheer StorSimple-service toomanage volumes (Update 3 of hoger)

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheren van volumes op Hallo StorSimple 8000 series apparaten met Update 3 en hoger.

Hallo StorSimple-apparaat Manager-service is een uitbreiding in hello Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface. Gebruik hello Azure portal toomanage volumes op al uw apparaten. U kunt ook maken en beheren van StorSimple-services, apparaten, back-upbeleid en back-upcatalogus beheren en waarschuwingen weergeven.

## <a name="volume-types"></a>Volumetypen

StorSimple-volumes kunnen zijn:

* **Lokaal vastgemaakte volumes**: gegevens in deze volumes blijft op de lokale StorSimple-apparaat hello te allen tijde.
* **Gelaagde volumes**: gegevens in deze volumes kunnen toohello cloud worden gelekt.

Een archivering volume is een gelaagd volume. Hallo groter Ontdubbeling chunkgrootte gebruikt voor archivering volumes kunt Hallo apparaat tootransfer groter segmenten van gegevens toohello cloud.

Indien nodig, kunt u het volumetype Hallo van lokale tootiered of van gelaagde toolocal is ingesteld. Voor meer informatie gaat te[Hallo volumetype wijzigen](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Lokaal vastgemaakte volumes

Lokaal vastgemaakte volumes zijn volledig ingerichte volumes die gegevens toohello cloud niet laag, garanties waardoor lokale voor primaire gegevens, onafhankelijk van de verbinding van de cloud. Gegevens op lokaal vastgemaakte volumes is niet ontdubbeld en gecomprimeerd. momentopnamen van lokaal vastgemaakte volumes zijn echter ontdubbeld. 

Lokaal vastgemaakte volumes zijn volledig is ingericht; Daarom moet u voldoende ruimte hebben op uw apparaat wanneer u deze maakt. U kunt lokaal vastgemaakte volumes tooa maximale grootte van 8 TB op Hallo StorSimple 8100-apparaat en 20 TB op Hallo 8600-apparaat inrichten. StorSimple reserveert Hallo resterende lokale ruimte op het Hallo-apparaat voor momentopnamen, metagegevens en verwerken van gegevens. Kunt u vergroten Hallo van een lokaal vastgemaakt volume toohello maximaal beschikbaar, maar u kunt geen Hallo verkleining van een volume eenmaal is gemaakt.

Wanneer u een lokaal vastgemaakt volume maakt, wordt de Hallo beschikbare ruimte voor het maken van gelaagde volumes verminderd. Hallo omgekeerde geldt ook: als er bestaande gelaagde volumes, Hallo ruimte beschikbaar voor het maken van lokaal vastgemaakte volumes wordt niet lager zijn dan Hallo maximale bovenstaande grenzen. Raadpleeg voor meer informatie op lokale volumes toohello [Veelgestelde vragen op lokaal vastgemaakte volumes](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Gelaagde volumes

Gelaagde volumes zijn dun ingerichte volumes in welke Hallo vaak gebruikte gegevens lokaal op Hallo apparaat blijft en minder vaak gebruikte gegevens wordt automatisch toohello cloud gelaagde. Thin provisioning is een virtualisatietechnologie voor het waarin beschikbare opslag tooexceed fysieke resources weergegeven. In plaats van voldoende opslagruimte van tevoren reserveren, StorSimple maakt gebruik van thin provisioning tooallocate net voldoende ruimte toomeet actuele vereisten. Hallo elastische aard van cloud-opslag vergemakkelijkt deze benadering omdat StorSimple kunt vergroten of verkleinen van veranderende verzoeken voor toomeet cloud-opslag.

Als u gebruikmaakt van gelaagde volume voor de archivering van gegevens, selecteer Hallo Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje toochange Hallo Ontdubbeling chunkgrootte voor het volume too512 KB. Als u deze optie niet selecteert, wordt de Hallo overeenkomstige gelaagde volume een chunkgrootte van 64 KB gebruikt. Een grotere chunkgrootte voor Ontdubbeling kunt Hallo apparaat tooexpedite Hallo overdracht van grote hoeveelheden gegevens voor archivering toohello cloud.


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

## <a name="hello-volumes-blade"></a>Hallo volumes blade

Hallo **Volumes** blade kunt u toomanage Hallo opslagvolumes die zijn ingericht op Hallo Microsoft Azure StorSimple-apparaat voor uw initiators (servers). Hallo-lijst van volumes wordt weergegeven op Hallo StorSimple-apparaten verbonden tooyour-service.

 ![Pagina volumes](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Een volume bestaat uit een reeks van kenmerken:

* **Volumenaam** – een beschrijvende naam moet uniek zijn en kan Hallo volume geïdentificeerd. Deze naam wordt ook gebruikt in de bewaking van rapporten, wanneer u op een bepaald volume filtert. Zodra Hallo volume is gemaakt, kan niet worden gewijzigd.
* **Status** – online of offline kan zijn. Als een volume offline is, maar het is niet zichtbaar tooinitiators (servers) die toegang toouse Hallo volume zijn toegestaan.
* **Capaciteit** – Hallo totale hoeveelheid gegevens die kunnen worden opgeslagen door Hallo initiator (server). Lokaal vastgemaakte volumes volledig is ingericht en zich bevinden op Hallo StorSimple-apparaat. Gelaagde volumes zijn dun ingericht en Hallo gegevens is ontdubbeld. Met thin provisioning volumes uw apparaat niet vooraf fysieke opslagcapaciteit intern of toewijzen op Hallo-cloud op basis van de volumecapaciteit tooconfigured. Hallo volumecapaciteit is toegewezen en op verzoek gebruikt.
* **Type** – Hiermee wordt aangegeven of Hallo volume **tiers verdeelde** (Hallo standaard) of **lokaal vastgemaakt**.

Gebruik Hallo-instructies in deze zelfstudie tooperform Hallo taken te volgen:

* Een volume toevoegen 
* Een volume wijzigen 
* Hallo-volumetype wijzigen
* Een volume verwijderen 
* Een volume offline zetten 
* Een volume bewaken 

## <a name="add-a-volume"></a>Een volume toevoegen

U [gemaakt van een volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) tijdens de implementatie van uw StorSimple 8000 serie-apparaat. Toevoegen van een volume is een vergelijkbare procedure.

#### <a name="tooadd-a-volume"></a>een volume tooadd

1. Uit in tabelvorm aanbieding van apparaten in Hallo HALLO hallo **apparaten** blade, selecteer uw apparaat. Klik op **Volume toevoegen**.

    ![Een nieuw volume toevoegen](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. In Hallo **toevoegen van een volume** blade:
   
    1. Hallo **Selecteer welk apparaat** veld wordt automatisch gevuld met uw huidige apparaat.

    2. Selecteer in de vervolgkeuzelijst hello, Hallo volumecontainer wanneer u een volume tooadd nodig.

    3.  een **naam** voor het volume. Zodra Hallo volume is gemaakt, kunt u Hallo volume niet hernoemen.

    4. Selecteer op de vervolgkeuzelijst hello, Hallo **Type** voor het volume. Voor workloads waarvoor lokale garanties, lage latenties en betere prestaties vereist zijn, selecteert u een **lokaal vastgemaakt** volume. Voor alle overige gegevens selecteert u een **gelaagd** volume. Als u dit volume gebruikt voor de archivering van gegevens, schakelt u **Dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** in.
      
       Een gelaagd volume is dun ingericht (thin provisioning) en kan zeer snel worden gemaakt. Selecteren **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** voor gelaagde volume gericht voor archivering van gegevens wijzigingen Hallo Ontdubbeling chunkgrootte voor het volume too512 KB. Als dit veld niet is ingeschakeld, gebruikt Hallo overeenkomstige gelaagde volume een chunkgrootte van 64 KB. Een grotere chunkgrootte voor Ontdubbeling kunt Hallo apparaat tooexpedite Hallo overdracht van grote hoeveelheden gegevens voor archivering toohello cloud.
       
       Een lokaal vastgemaakt volume is compact ingericht en zorgt ervoor dat de primaire gegevens op Hallo volume Hallo lokale toohello apparaat blijft en komt niet toohello cloud worden gelekt.  Als u een lokaal vastgemaakt volume maakt, Hallo-apparaat controleert op beschikbare ruimte op de lokale lagen Hallo tooprovision Hallo volume Hallo aangevraagde grootte. Hallo-bewerking voor het maken van een lokaal vastgemaakt volume heeft als risico dat bestaande gegevens uit Hallo apparaat toohello cloud kan inhouden en Hallo tijd toocreate Hallo volume mogelijk lang. Hallo totale tijd is afhankelijk van Hallo grootte van het volume Hallo ingericht, beschikbare netwerkbandbreedte en Hallo gegevens op uw apparaat.

    5. Geef Hallo **ingerichte capaciteit** voor het volume. Noteer Hallo capaciteit die beschikbaar is op basis van Hallo volume dat is geselecteerd. Hallo opgegeven volumegrootte mag niet groter zijn dan Hallo beschikbare ruimte.
      
       U kunt lokaal vastgemaakte volumes tot too8.5 TB en gelaagde volumes van too200 TB op Hallo 8100-apparaat inrichten. U kunt lokaal vastgemaakte volumes tot too22.5 TB en gelaagde volumes van too500 TB inrichten op Hallo groter 8600-apparaat. Aangezien lokale ruimte op Hallo apparaat vereist toohost Hallo werkset van gelaagde volumes, het maken van lokaal vastgemaakte volumes invloed is op Hallo beschikbare schijfruimte voor het inrichten van gelaagde volumes. Als u dus een lokaal vastgemaakt volume maakt, wordt de beschikbare schijfruimte voor het maken van gelaagde volumes verminderd. Als een gelaagd volume is gemaakt, wordt op dezelfde manier Hallo beschikbare ruimte voor het maken van lokaal vastgemaakte volumes verminderd.
      
       Als u een lokaal vastgemaakt volume van 8.5 TB (maximaal toegestane grootte) op uw 8100-apparaat inricht, hebt u alle Hallo lokale ruimte beschikbaar is op Hallo apparaat uitgeput. U kunt geen gelaagd volume kan niet maken vanaf dat moment of hoger als er geen lokale ruimte op Hallo apparaat toohost Hallo-werkset Hallo is gelaagd volume. Bestaande gelaagde volumes zijn ook van invloed op Hallo ruimte beschikbaar. Als u bijvoorbeeld een 8100-apparaat hebt met reeds gelaagde volumes van circa 106 TB, is er nog maar 4 TB ruimte beschikbaar voor lokaal vastgemaakte volumes.

    6. In Hallo **verbonden hosts** en klik op de pijl Hallo veld. 

        ![Verbonden hosts](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. In Hallo **verbonden hosts** blade, kiest u een bestaande ACR of Voeg een nieuwe ACR. Als u een nieuwe ACR kiest, geeft vervolgens een **naam** bieden voor uw ACR hello **iSCSI Qualified Name** (IQN) van uw Windows-host. Als u Hallo IQN niet hebt, gaat u verder te[Get Hallo IQN van een Windows Server-host](#get-the-iqn-of-a-windows-server-host). Klik op **Create**. Een volume wordt gemaakt met de Hallo opgegeven instellingen.

        ![Klik op Maken](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

Het nieuwe volume is nu gereed toouse.

> [!NOTE]
> Als u een lokaal vastgemaakt volume maakt en vervolgens maakt een ander lokaal vastgemaakt volume onmiddellijk daarna Hallo-taken voor het maken van volume worden opeenvolgend uitgevoerd. Hallo-taak voor het maken van eerste volume moet worden voltooid voordat het Hallo-taak voor het maken van volgende volume kan beginnen.

## <a name="modify-a-volume"></a>Een volume wijzigen

Een volume wijzigen wanneer u deze of wijziging hosts die toegang tot het volume Hallo Hallo tooexpand nodig.

> [!IMPORTANT]
> * Als u de volumegrootte Hallo op Hallo apparaat wijzigt, moet de volumegrootte Hallo toobe op Hallo host ook gewijzigd.
> * hier beschreven stappen Hallo hostzijde zijn voor Windows Server 2012 (2012R2). Procedures voor het Linux- of andere hostbesturingssystemen zullen afwijken. Raadpleeg tooyour host besturingssysteem instructies bij het wijzigen van Hallo volume op een host waarop een ander besturingssysteem.

#### <a name="toomodify-a-volume"></a>een volume toomodify

1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **apparaten**. Selecteer in de Hallo in tabelvorm aanbieding Hallo apparaten, Hallo apparaat Hallo volume dat u van plan toomodify bent heeft. Klik op **instellingen > Volumes**.

    ![Ga tooVolumes-blade](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. Hallo in tabelvorm lijst van volumes, Hallo volume te selecteren en met de rechtermuisknop op tooinvoke Hallo contextmenu. Selecteer **offline zetten** tootake Hallo volume u offline wijzigt.

    ![Selecteer en volume offline zetten](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. In Hallo **offline zetten** blade Hallo gevolgen van het volume Hallo offline halen bekijken en het bijbehorende selectievakje Hallo selecteert. Zorg ervoor dat Hallo bijbehorende volume op Hallo host eerst offline is. Raadpleeg voor informatie over hoe tootake offline een volume op de hostserver tooStorSimple aangesloten toooperating system specifieke instructies. Klik op **offline zetten**.

    ![Gevolgen van het volume offline halen controleren](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Nadat de Hallo volume is offline (zoals weergegeven door de status van Hallo volume), Hallo volume te selecteren en met de rechtermuisknop op tooinvoke Hallo contextmenu. Selecteer **volume wijzigen**.

    ![Selecteer wijzigen volume](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. In Hallo **volume wijzigen** blade kunt u Hallo volgende wijzigingen aanbrengen:
   
   1. Hallo volume **naam** kan niet worden bewerkt.
   2. Hallo converteren **Type** van lokaal vastgemaakte tootiered of van gelaagde toolocally vastgemaakt (Zie [Hallo volumetype wijzigen](#change-the-volume-type) voor meer informatie).
   3. Hallo verhogen **ingerichte capaciteit**. Hallo **ingerichte capaciteit** kan alleen worden verhoogd. Nadat deze is gemaakt, kunt u een volume niet verkleinen.
   4. Onder **verbonden hosts**, kunt u Hallo ACR wijzigen. een ACR toomodify, Hallo volume moet offline zijn.

       ![Gevolgen van het volume offline halen controleren](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Klik op **opslaan** toosave uw wijzigingen. Klik op **Ja** als u om bevestiging wordt gevraagd. een bijwerken volume bericht weergegeven met Hello Azure-portal. Een bericht wordt weergegeven wanneer het Hallo-volume is bijgewerkt.

    ![Gevolgen van het volume offline halen controleren](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Als u een volume uitbreidt, voltooit u de volgende stappen uit op de hostcomputer Windows hello:
   
   1. Ga te**Computerbeheer** ->**Schijfbeheer**.
   2. Met de rechtermuisknop op **Schijfbeheer** en selecteer **schijven**.
   3. Selecteer in de lijst van de Hallo van schijven, Hallo volume dat u hebt bijgewerkt, klik met de rechtermuisknop en selecteer vervolgens **Volume uitbreiden**. Hallo Volume uitbreiden wizard wordt gestart. Klik op **Volgende**.
   4. Voltooi de wizard hello, accepteer de standaardwaarden Hallo. Nadat het Hallo-wizard is voltooid, moet Hallo verhoogd grootte Hallo volume worden weergegeven.
      
      > [!NOTE]
      > Als u een lokaal vastgemaakt volume uitvouwen en vouwt u vastgemaakt een ander lokaal volume onmiddellijk daarna Hallo volume uitbreiding taken worden opeenvolgend uitgevoerd. Hallo eerste volume Uitbreidingstaak moet zijn voltooid voordat Hallo volgende volume Uitbreidingstaak kan beginnen.
      

## <a name="change-hello-volume-type"></a>Hallo-volumetype wijzigen

U kunt het volumetype Hallo wijzigen van gelaagde toolocally vastgemaakt of van lokaal vastgemaakte tootiered. Deze conversie mag echter geen een frequente exemplaar.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Aandachtspunten bij de conversie van de toolocal gelaagde volume

Enkele redenen voor het converteren van een volume van gelaagde toolocally vastgemaakt zijn:

* Lokale garanties met betrekking tot de beschikbaarheid van gegevens en prestaties
* Afschaffing van de cloud latenties en problemen met de netwerkverbinding van de cloud.

Dit zijn meestal kleine bestaande volumes dat u wilt dat tooaccess vaak. Een lokaal vastgemaakt volume volledig is ingericht wanneer deze wordt gemaakt. 

Als u een gelaagd volume tooa lokaal vastgemaakt volume converteert, controleert StorSimple of dat er voldoende ruimte is op uw apparaat voordat het Hallo-conversie wordt gestart. Als er onvoldoende ruimte, ontvangt u een fout en Hallo-bewerking wordt geannuleerd. 

> [!NOTE]
> Voordat u begint met de conversie van een gelaagde toolocally vastgemaakt, ervoor zorgen dat u rekening houden met Hallo schijfruimte van andere werkbelastingen. 

Conversie van een gelaagde tooa lokaal vastgemaakt volume, kan een nadelige invloed heeft op de prestaties van een apparaat. Hallo volgende factoren kan bovendien Hallo duurt toocomplete Hallo conversie verhogen:

* Er is onvoldoende bandbreedte.
* Er is geen huidige back-up.

toominimize hello effecten die deze factoren kunnen hebben:

* Bekijk uw beleid voor bandbreedteregeling en zorg ervoor dat er geen speciale 40 Mbps bandbreedte beschikbaar is.
* Hallo-conversie voor daluren plannen.
* Een cloud momentopname voordat u begint met Hallo conversie.

Als u meerdere volumes (ondersteunen verschillende werkbelastingen) converteert, moet u Hallo volumeconversie prioriteren zodat volumes met hogere prioriteit eerst worden geconverteerd. Bijvoorbeeld, moet u volumes die virtuele machines (VM's) hosten of volumes met SQL-werkbelastingen converteren voordat u de volumes met file share werkbelastingen converteert.

### <a name="local-tootiered-volume-conversion-considerations"></a>Aandachtspunten bij de conversie van de lokale tootiered volume

U kunt een lokaal vastgemaakt volume tooa toochange gelaagde volume als u extra schijfruimte tooprovision nodig andere volumes. Wanneer u Hallo lokaal vastgemaakt volume tootiered converteert, verhoogt de beschikbare capaciteit op Hallo apparaat Hallo door Hallo grootte van de capaciteit Hallo uitgebracht. Als problemen met de netwerkverbinding te voorkomen dat Hallo conversie van een volume van Hallo lokale type toohello gelaagde type, hello lokaal volume zou vertonen eigenschappen van een gelaagd volume totdat Hallo conversie is voltooid. Dit komt omdat sommige gegevens toohello cloud terechtgekomen mogelijk. Deze gemorst gegevens blijft toooccupy lokale ruimte op Hallo-apparaat dat niet kan worden vrijgemaakt totdat het Hallo-bewerking wordt opnieuw gestart en voltooid.

> [!NOTE]
> Converteren van een volume kan enige tijd duren en u een conversie niet annuleren nadat deze is gestart. Hallo volume online blijft tijdens de conversie van hello, en u kunt back-ups uitvoeren, maar u niet kunt uitbreiden of Hallo volume herstelt tijdens conversie Hallo.


#### <a name="toochange-hello-volume-type"></a>Hallo-volumetype toochange

1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **apparaten**. Selecteer in de Hallo in tabelvorm aanbieding Hallo apparaten, Hallo apparaat Hallo volume dat u van plan toomodify bent heeft. Klik op **instellingen > Volumes**.

    ![Ga tooVolumes-blade](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Hallo in tabelvorm lijst van volumes, Hallo volume te selecteren en met de rechtermuisknop op tooinvoke Hallo contextmenu. Selecteer **wijzigen**.

    ![Selecteer wijzigen in contextmenu](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. Op Hallo **volume wijzigen** blade Hallo volumetype wijzigen door het selecteren van de nieuwe type Hallo van Hallo **Type** vervolgkeuzelijst.
   
   * Als u Hallo type te wijzigen**lokaal vastgemaakt**, StorSimple toosee wordt gecontroleerd of er onvoldoende capaciteit is.
   * Als u Hallo type te wijzigen**tiers verdeelde** en dit volume wordt gebruikt voor archivering van gegevens, selecteer Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje.
   * Als u een lokaal vastgemaakt volume configureert zoals lagen of _omgekeerd_, hello volgende bericht wordt weergegeven.
   
    ![Wijziging volume tekstbericht](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Klik op **opslaan** toosave Hallo wijzigingen. Wanneer u om bevestiging gevraagd, klikt u op **Ja** toostart Hallo-conversieproces. 

    ![Opslaan en bevestigen](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Hello Azure-portal geeft een melding voor het Hallo-taak maken die Hallo volume wordt bijgewerkt. Klik op Hallo toomonitor Hallo meldingenstatus van Hallo volume conversietaak.

    ![Taak voor volumeconversie](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Een volume offline zetten

Mogelijk moet u een volume offline tootake wanneer u van plan bent toomodify of Hallo volume verwijderen. Als een volume offline is, is het niet beschikbaar voor lees-/ schrijftoegang. U moet nemen Hallo volume offline op Hallo host en Hallo-apparaat.

#### <a name="tootake-a-volume-offline"></a>een volume offline tootake

1. Zorg ervoor dat de betreffende Hallo volume is niet in gebruik voordat deze offline wordt gezet.
2. Hallo volume offline op host Hallo eerste duren. Hierdoor wordt een potentieel risico van gegevensbeschadiging op Hallo volume. Raadpleeg voor specifieke stappen toohello instructies voor het besturingssysteem van de host.
3. Nadat de host Hallo offline is, ondernemen Hallo volume Hallo apparaat offline door Hallo volgende stappen uit te voeren:
   
    1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **apparaten**. Selecteer in de Hallo in tabelvorm aanbieding Hallo apparaten, Hallo apparaat Hallo volume dat u van plan toomodify bent heeft. Klik op **instellingen > Volumes**.

        ![Ga tooVolumes-blade](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. Hallo in tabelvorm lijst van volumes, Hallo volume te selecteren en met de rechtermuisknop op tooinvoke Hallo contextmenu. Selecteer **offline zetten** tootake Hallo volume u offline wijzigt.

        ![Selecteer en volume offline zetten](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. In Hallo **offline zetten** blade Hallo gevolgen van het volume Hallo offline halen bekijken en het bijbehorende selectievakje Hallo selecteert. Klik op **offline zetten**. 

    ![Gevolgen van het volume offline halen controleren](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      U wordt gewaarschuwd wanneer Hallo volume offline is. Hallo volumestatus ook tooOffline bijgewerkt.
      
4. Nadat een volume offline is, als u Hallo volume en klik met de rechtermuisknop, selecteer **Online brengen** optie is beschikbaar in het contextmenu Hallo.

> [!NOTE]
> Hallo **Offline nemen** opdracht verzendt een aanvraag toohello apparaat tootake Hallo volume offline. Als hosts nog steeds Hallo volume, resulteert dit in verbroken verbindingen maar Hallo volume offline halen niet mislukken.

## <a name="delete-a-volume"></a>Een volume verwijderen

> [!IMPORTANT]
> U kunt een volume alleen verwijderen als deze offline is.

Volgende stappen toodelete een volume Hallo voltooien.

#### <a name="toodelete-a-volume"></a>een volume toodelete

1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **apparaten**. Selecteer in de Hallo in tabelvorm aanbieding Hallo apparaten, Hallo apparaat Hallo volume dat u van plan toomodify bent heeft. Klik op **instellingen > Volumes**.

    ![Ga tooVolumes-blade](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Controleer de status van Hallo Hallo volume dat u wilt dat toodelete. Hallo volume gewenste toodelete is niet als offline, eerst offline halen. Volg de stappen Hallo in [offline zetten van een volume](#take-a-volume-offline).
4. Nadat Hallo volume offline is, selecteert u volume hello, met de rechtermuisknop op tooinvoke Hallo contextmenu en selecteer vervolgens **verwijderen**.

    ![Selecteer verwijderen in contextmenu](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. In Hallo **verwijderen** blade, controleren en selecteer Hallo selectievakje tegen Hallo gevolgen van het verwijderen van een volume. Wanneer u een volume verwijdert, zijn alle Hallo-gegevens die zich op Hallo volume gaat verloren. 

    ![Opslaan en wijzigingen bevestigen](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Nadat het Hallo-volume wordt verwijderd, Hallo in tabelvorm lijst updates van volumes tooindicate Hallo verwijderen.

    ![Bijgewerkte Volumelijst](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Als u een lokaal vastgemaakt volume verwijdert, worden Hallo beschikbare schijfruimte voor het nieuwe volumes mogelijk niet meteen bijgewerkt. Hallo StorSimple-apparaat Manager-Service-updates worden periodiek Hallo lokale ruimte beschikbaar. We raden dat u wacht enkele minuten duren voordat u toocreate Hallo nieuw volume probeert.
   >
   > Bovendien, als u een lokaal vastgemaakt volume verwijdert en verwijdert u vervolgens een ander lokaal vastgemaakt volume onmiddellijk daarna Hallo volume verwijdering taken worden opeenvolgend uitgevoerd. Hallo-taak voor het verwijderen van eerste volume moet worden voltooid voordat Hallo volgende volume verwijderen van een taak kan beginnen.

## <a name="monitor-a-volume"></a>Een volume bewaken

Bewaking van volume, kunt u toocollect I/O-gerelateerde statistieken voor een volume. Bewaking is standaard ingeschakeld voor Hallo eerste 32 volumes die u maakt. Bewaking van extra volumes is standaard uitgeschakeld. 

> [!NOTE]
> Bewaking van de gekloonde volumes is standaard uitgeschakeld.


Volgende stappen tooenable Hallo uitvoeren of schakel bewaking voor een volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable- of uitschakelen volume bewaking

1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **apparaten**. Selecteer in de Hallo in tabelvorm aanbieding Hallo apparaten, Hallo apparaat Hallo volume dat u van plan toomodify bent heeft. Klik op **instellingen > Volumes**.
2. Hallo in tabelvorm lijst van volumes, Hallo volume te selecteren en met de rechtermuisknop op tooinvoke Hallo contextmenu. Selecteer **wijzigen**.
3. In Hallo **volume wijzigen** blade voor **bewaking** Selecteer **inschakelen** of **uitschakelen** tooenable of schakel bewaking.

    ![Schakel bewaking](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**. Hello Azure-portal geeft een melding voor het bijwerken van Hallo volume en vervolgens een voltooiingsbericht te zien, nadat het Hallo-volume is bijgewerkt.

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over hoe te[klonen van een StorSimple-volume](storsimple-8000-clone-volume-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

