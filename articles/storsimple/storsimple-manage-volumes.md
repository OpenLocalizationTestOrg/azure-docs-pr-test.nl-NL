---
title: aaaManage uw StorSimple-volumes | Microsoft Docs
description: Legt uit hoe tooadd, wijzigen, bewaken en verwijderen van StorSimple-volumes en hoe tootake offline indien nodig.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Hallo StorSimple Manager-service toomanage volumes gebruiken
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Manager service toocreate Hallo en beheren van volumes op Hallo StorSimple-apparaat en virtuele StorSimple-apparaat.

Hallo StorSimple Manager-service is een uitbreiding van Hallo klassieke Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface. In toevoeging toomanaging volumes, kunt u Hallo StorSimple Manager-service toocreate gebruiken en StorSimple-services beheren, weergeven en beheren van apparaten, waarschuwingen, weergeven en weergeven en beheren back-upbeleid en back-upcatalogus Hallo.

> [!NOTE]
> Azure StorSimple kunt alleen thin ingerichte volumes maken. U kunt geen maken volledig of gedeeltelijk ingerichte volumes op een Azure StorSimple-systeem.
> 
> Thin provisioning is een virtualisatietechnologie voor het waarin beschikbare opslag tooexceed fysieke resources weergegeven. In plaats van voldoende opslagruimte van tevoren reserveren, Azure StorSimple maakt gebruik van thin provisioning tooallocate net voldoende ruimte toomeet actuele vereisten. Hallo elastische aard van cloud-opslag vergemakkelijkt deze benadering omdat Azure StorSimple kunt vergroten of verkleinen van veranderende verzoeken voor toomeet cloud-opslag.
> 
> 

## <a name="hello-volumes-page"></a>de pagina Volumes Hallo
Hallo **Volumes** pagina kunt u toomanage Hallo opslagvolumes die zijn ingericht op Hallo Microsoft Azure StorSimple-apparaat voor uw initiators (servers). Hallo-lijst van volumes wordt weergegeven op uw StorSimple-apparaat.

 ![Pagina volumes](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Een volume bestaat uit een reeks van kenmerken:

* **Naam** – een beschrijvende naam moet uniek zijn en kan Hallo volume geïdentificeerd. Deze naam wordt ook gebruikt in de bewaking van rapporten, wanneer u op een bepaald volume filtert.
* **Status** – online of offline kan zijn. Als een volume als offline, maar het is niet zichtbaar tooinitiators (servers) die toegang toouse Hallo volume zijn toegestaan.
* **Capaciteit** – Hiermee geeft u op hoe groot Hallo volume is, zoals waargenomen door Hallo initiator (server). Capaciteit geeft Hallo totale hoeveelheid gegevens die kunnen worden opgeslagen door Hallo initiator (server). Volumes zijn dun ingericht en gegevens is ontdubbeld. Dit betekent dat het apparaat niet vooraf fysieke opslagcapaciteit intern of toewijzen op Hallo-cloud op basis van de volumecapaciteit tooconfigured. Hallo volumecapaciteit is toegewezen en op verzoek gebruikt.
* **Type** – Hallo volumetype mag gelaagde of archivering (een subtype van gelaagd)
* **Toegang** – Hiermee geeft u op Hallo initiators (servers) die toegang toothis volume zijn toegestaan. Initiators die geen deel uitmaken van record voor toegangscontrole (ACR) die is gekoppeld aan het volume Hallo zichtbaar Hallo volume niet.
* **Bewaking** – Hiermee wordt aangegeven of een volume wordt bewaakt. Een volume hebt bewaking standaard ingeschakeld wanneer deze wordt gemaakt. Wordt echter bewaking wordt uitgeschakeld voor de kloon van een volume. bewaking voor een volume tooenable instructies Hallo in de Monitor een volume.

Hallo meest algemene taken die zijn gekoppeld aan een volume zijn:

* Een volume toevoegen
* Een volume wijzigen
* Een volume verwijderen
* Een volume offline zetten
* Een volume bewaken

## <a name="add-a-volume"></a>Een volume toevoegen
U [gemaakt van een volume](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) tijdens de implementatie van uw StorSimple-oplossing. Toevoegen van een volume is een vergelijkbare procedure.

### <a name="tooadd-a-volume"></a>een volume tooadd
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer een volumecontainer en op de pijl Hallo in Hallo overeenkomstige rij tooaccess Hallo volumes die zijn gekoppeld aan het Hallo-container.
3. Klik op **toevoegen** Hallo Hallo pagina onderaan in. Hallo wizard volume toevoegen wordt gestart.
   
     ![Wizard volume basisinstellingen toevoegen](./media/storsimple-manage-volumes/AddVolume1.png)
4. In Hallo onder een wizard volume toevoegen **basisinstellingen**, Hallo te volgen:
   
   1. Geef een **naam** op voor het volume.
   2. Geef Hallo **ingerichte capaciteit** voor het volume in GB of TB. Hallo capaciteit moet tussen 1 GB en 64 TB voor een fysiek apparaat. Hallo maximale capaciteit die kan worden ingericht voor een volume op een virtueel StorSimple-apparaat is 30 TB.
   3. Selecteer Hallo **gebruikstype** voor het volume. Als u gebruikmaakt van gelaagde volume voor de archivering van gegevens, selecteren Hallo Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje verandert Hallo Ontdubbeling chunkgrootte voor het volume too512 KB. Als u deze optie niet selecteert, wordt de Hallo overeenkomstige gelaagde volume een chunkgrootte van 64 KB gebruikt. Een grotere chunkgrootte voor Ontdubbeling kunt Hallo apparaat tooexpedite Hallo overdracht van grote hoeveelheden gegevens voor archivering toohello cloud. (Gelaagde volumes werden voorheen primaire volumes genoemd.)
   4. Klik op het pijlpictogram Hallo ![pijlpictogram](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **extra instellingen** pagina.
      
        ![Extra instellingen van de wizard Volume toevoegen](./media/storsimple-manage-volumes/AddVolume2.png)
5. Onder **extra instellingen**, Voeg een nieuwe record voor toegangscontrole (ACR):
   
   1. Selecteer een record voor toegangscontrole (ACR) in de vervolgkeuzelijst Hallo. U kunt ook een nieuwe ACR toevoegen. ACRs bepalen welke hosts hebben toegang tot de volumes met overeenkomende Hallo IQN host met die in het Hallo-record genoemd.
   2. Het is raadzaam dat u een standaardback-up inschakelen door het selecteren van Hallo **een standaardback-up voor dit volume inschakelen** selectievakje.
   3. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-volumes/HCS_CheckIcon.png) toocreate hello volume Hello opgegeven instellingen.

Het nieuwe volume is nu gereed toouse.

## <a name="modify-a-volume"></a>Een volume wijzigen
Een volume wijzigen wanneer u deze of wijziging hosts die toegang tot het volume Hallo Hallo tooexpand nodig.

> [!IMPORTANT]
> * Als u de volumegrootte Hallo op Hallo apparaat wijzigt, moet de volumegrootte Hallo toobe op Hallo host ook gewijzigd.
> * hier beschreven stappen Hallo hostzijde zijn voor Windows Server 2012 (2012R2). Procedures voor het Linux- of andere hostbesturingssystemen zullen afwijken. Raadpleeg tooyour host besturingssysteem instructies bij het wijzigen van Hallo volume op een host waarop een ander besturingssysteem.
> 
> 

### <a name="toomodify-a-volume"></a>een volume toomodify
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainer** tabblad. Deze pagina geeft een lijst in tabelvorm alle Hallo volumecontainers die gekoppeld aan het Hallo-apparaat zijn.
2. Selecteer een volumecontainer en klik erop toodisplay Hallo lijst met alle Hallo volumes in Hallo-container.
3. Op Hallo **Volumes** pagina, selecteert u een volume en klik op **wijzigen**.
4. Wijzig in Hallo wizard volume onder **basisinstellingen**, kunt u doen Hallo volgende:
   
   * Hallo bewerken **naam** en **Type** desgewenst toomodify een gelaagd volume tooan archivering volume door het selecteren van Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje toochange Hallo Ontdubbeling chunkgrootte voor het volume too512 KB.
   * Hallo verhogen **ingerichte capaciteit**. Hallo **ingerichte capaciteit** kan alleen worden verhoogd. Nadat deze is gemaakt, kunt u een volume niet verkleinen.
     
     > [!NOTE]
     > U kunt Hallo volumecontainer niet wijzigen nadat deze tooa volume is toegewezen.
     > 
     > 
5. Onder **extra instellingen**, kunt u doen Hallo volgende:
   
   * Wijzig Hallo ACRs, mits Hallo volume offline is. Als Hallo volume online is, moet u tootake deze offline eerste. Raadpleeg toohello stappen in [offline zetten van een volume](#take-a-volume-offline) voorafgaande toomodifying hello ACR.
   * Hallo-lijst met ACRs wijzigen nadat Hallo volume offline is.
     
     > [!NOTE]
     > U kunt Hallo niet wijzigen **een standaardback-up voor dit volume inschakelen** optie voor het Hallo-volume.
     > 
     > 
6. Sla de wijzigingen door te klikken op het vinkje Hallo ![vinkje](./media/storsimple-manage-volumes/HCS_CheckIcon.png). Hallo klassieke Azure-portal weergegeven een bijwerken volume bericht. Een bericht wordt weergegeven wanneer het Hallo-volume is bijgewerkt.
7. Als u een volume uitbreidt, voltooit u de volgende stappen uit op de hostcomputer Windows hello:
   
   1. Ga te**Computerbeheer** ->**Schijfbeheer**.
   2. Met de rechtermuisknop op **Schijfbeheer** en selecteer **schijven**.
   3. Selecteer in de lijst van de Hallo van schijven, Hallo volume dat u hebt bijgewerkt, klik met de rechtermuisknop en selecteer vervolgens **Volume uitbreiden**. Hallo Volume uitbreiden wizard wordt gestart. Klik op **Volgende**.
   4. Voltooi de wizard hello, accepteer de standaardwaarden Hallo. Nadat het Hallo-wizard is voltooid, moet Hallo verhoogd grootte Hallo volume worden weergegeven.

![Video beschikbaar](./media/storsimple-manage-volumes/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe tooexpand een volume, klik op [hier](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Een volume offline zetten
Mogelijk moet u een volume offline tootake wanneer u van plan bent toomodify of verwijderen deze. Als een volume offline is, is het niet beschikbaar voor lees-/ schrijftoegang. U moet tootake Hallo volume offline op host hello, evenals op Hallo-apparaat. Hallo te volgen stappen tootake offline een volume uitvoeren.

### <a name="tootake-a-volume-offline"></a>een volume offline tootake
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

### <a name="toodelete-a-volume"></a>een volume toodelete
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer Hallo volumecontainer met de gewenste toodelete Hallo-volume. Klik op Hallo volume container tooaccess hello **Volumes** pagina.
3. Alle Hallo volumes die zijn gekoppeld aan deze container worden weergegeven in tabelvorm. Controleer de status van Hallo Hallo volume dat u wilt dat toodelete. Als de gewenste toodelete Hallo-volume niet offline is, het Hallo voor offline eerste, de volgende stappen uitvoeren [offline zetten van een volume](#take-a-volume-offline).
4. Nadat het Hallo volume offline is, klikt u op **verwijderen** Hallo Hallo pagina onderaan in.
5. Klik op **Ja** als u om bevestiging wordt gevraagd. Hallo-volume wordt nu verwijderd en Hallo **Volumes** pagina ziet lijst van volumes in de container Hallo Hallo bijgewerkt.

## <a name="monitor-a-volume"></a>Een volume bewaken
Bewaking van volume, kunt u toocollect I/O-gerelateerde statistieken voor een volume. Bewaking is standaard ingeschakeld voor Hallo eerste 32 volumes die u maakt. Bewaking van extra volumes is standaard uitgeschakeld. Bewaking van de gekloonde volumes wordt ook standaard uitgeschakeld.

Volgende stappen tooenable Hallo uitvoeren of schakel bewaking voor een volume.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable- of uitschakelen volume bewaking
1. Op Hallo **apparaten** pagina, Hallo apparaat selecteert, dubbelklikt u op en klik vervolgens op Hallo **Volumecontainers** tabblad.
2. Selecteer Hallo volumecontainer in welke Hallo volume zich bevindt en klik vervolgens op Hallo volume container tooaccess hello **Volumes** pagina.
3. Alle Hallo volumes die zijn gekoppeld aan deze container worden vermeld in Hallo in tabelvorm weergegeven. Klik op en selecteer Hallo volume of volume klonen.
4. Klik onder aan de pagina Hallo Hallo op **wijzigen**.
5. In de wizard Volume wijzigen Hallo onder **basisinstellingen**, selecteer **inschakelen** of **uitschakelen** van Hallo **bewaking** vervolgkeuzelijst.
   
    ![Een volume basisinstellingen wijzigen](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[klonen van een StorSimple-volume](storsimple-clone-volume.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

