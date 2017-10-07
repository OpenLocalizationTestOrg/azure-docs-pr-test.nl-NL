---
title: een volume op StorSimple 8000-serie aaaClone | Microsoft Docs
description: Beschrijft Hallo kloon van de verschillende typen en het gebruik en wordt uitgelegd hoe u een back-upset tooclone afzonderlijk volume op een StorSimple 8000 series apparaat kunt gebruiken.
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
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Hallo Apparaatbeheer StorSimple-service van Azure portal tooclone een volume gebruikt

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt beschreven hoe u kunt een back-upset tooclone afzonderlijk volume via Hallo **back-upcatalogus** blade. Ook wordt uitgelegd hoe Hallo verschil tussen *tijdelijke* en *permanente* klonen. Hallo richtlijnen in deze zelfstudie geldt tooall hello StorSimple 8000 series apparaat met Update 3 of hoger.

Hallo StorSimple-apparaat Manager-service **back-upcatalogus** blade geeft alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt. Vervolgens kunt u een volume selecteren in een tooclone back-upset.

 ![Back-upset lijst](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Overwegingen voor het klonen van een volume

Houd rekening met Hallo informatie te volgen bij het klonen van een volume.

- Een kloon gedraagt zich op Hallo dezelfde manier als een reguliere volume. Een bewerking die mogelijk is op een volume is beschikbaar voor Hallo kloon.

- Bewaking en het standaard back-up worden automatisch uitgeschakeld op een gekloonde volume. U moet een gekloonde volume tooconfigure voor elke back-ups.

- Een lokaal vastgemaakt volume is als een gelaagd volume gekloond. Als u moet de gekloonde volume toobe lokaal vastgemaakt hello, kunt u Hallo kloon tooa lokaal vastgemaakt volume converteren nadat Hallo kloonbewerking is voltooid. Ga voor informatie over het converteren van een gelaagd volume tooa lokaal volume vastgemaakt, te[Hallo volumetype wijzigen](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Als u een gekloonde volume van gelaagde toolocally vastgemaakt onmiddellijk na het klonen probeert (wanneer deze nog steeds een tijdelijke kloon wordt) tooconvert, Hallo conversie is mislukt met de Hallo volgende foutbericht weergegeven:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Deze fout wordt alleen als u op een ander apparaat tooa klonen ontvangen. U kunt met succes Hallo volume toolocally vastgemaakt als u eerst Hallo tijdelijke kloon tooa permanente kloon converteren converteren. Een momentopname van de cloud van Hallo tijdelijke kloon tooconvert het tooa permanente kloon.

## <a name="create-a-clone-of-a-volume"></a>Maak een kloon van een volume

U kunt een kloon maken op hetzelfde apparaat, een ander apparaat of zelfs een cloud-toestel Hallo met behulp van een lokale of een momentopname cloud.

Hallo onderstaande procedure beschrijft hoe een kloon van Hallo toocreate back-up catalogus.  De kloon van een alternatieve methode tooinitiate is toogo te**Volumes**, een volume te selecteren en vervolgens met de rechtermuisknop op tooinvoke Hallo contextmenu en selecteert u **kloon**.

Volgende stappen toocreate een kloon van het volume uit de back-upcatalogus Hallo Hallo uitvoeren.

#### <a name="tooclone-a-volume"></a>een volume tooclone

1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **back-upcatalogus**.

2. Selecteer een back-up als volgt instellen:
   
   1. Selecteer het juiste apparaat Hallo.
   2. Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.
   3. Hallo tijdsperiode opgeven.
   4. Klik op **toepassen** tooexecute deze query.

    Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.
   
    ![Back-upset lijst](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Vouw Hallo back-upset tooview Hallo gekoppeld volumes. Deze volumes moeten op Hallo host en het apparaat offline worden genomen voordat u ze kunt herstellen. Toegang tot Hallo volumes op Hallo **Volumes** blade van uw apparaat en Hallo Volg de stappen in [offline zetten van een volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake ze offline.
   
   > [!IMPORTANT]
   > Zorg ervoor dat u hebt ondernomen Hallo volumes offline op Hallo host eerst voordat u Hallo volumes offline op Hallo-apparaat nemen. Als u niet Hallo volumes offline op Hallo host nemen, kan deze toodata beschadiging leiden.
   
4. Navigeer terug toohello **back-upcatalogus** een volume te selecteren in een back-upset. Met de rechtermuisknop en selecteer vervolgens in het contextmenu hello, **kloon**.

   ![Back-upset lijst](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. In Hallo **kloon** blade Hallo volgende stappen:
   
    1. Identificeer een doelapparaat. Dit is Hallo-locatie waar Hallo kloon wordt gemaakt. U kunt Hallo hetzelfde apparaat of geef een ander apparaat.

      > [!NOTE]
      > Zorg ervoor dat Hallo capaciteit is vereist voor de kloon Hallo lager dan Hallo capaciteit die beschikbaar is op het doelapparaat Hallo is.
       
    2. Geef een unieke volumenaam voor de kloon. Hallo-naam moet tussen 3 en 127 tekens bevatten.
      
        > [!NOTE]
        > Hallo **kloon Volume als** veld **tiers verdeelde** zelfs als u bij het klonen van een lokaal vastgemaakt volume. U kunt deze instelling; niet wijzigen echter, als u moet de gekloonde volume toobe lokaal vastgemaakt ook hello, kunt u converteren Hallo kloon tooa lokaal vastgemaakt volume nadat u Hallo kloon is gemaakt. Ga voor informatie over het converteren van een gelaagd volume tooa lokaal volume vastgemaakt, te[Hallo volumetype wijzigen](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. Onder **verbonden hosts**, een record voor toegangscontrole (ACR) voor de kloon Hallo opgeven. U kunt een nieuwe ACR toevoegen of kiezen uit bestaande Hallo-lijst. Hallo ACR wordt bepaald welke hosts hebben toegang tot de kloon.
      
        ![Back-upset lijst](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Klik op **kloon** toocomplete Hallo-bewerking.

4. Een taak klonen wordt gestart en u wordt gewaarschuwd wanneer het Hallo-kloon is gemaakt. Klik op Hallo taakmeldingen of te gaan**taken** blade toomonitor Hallo kloon taak.

    ![Back-upset lijst](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Wanneer Hallo kloon voltooid is, gaat u tooyour apparaat en klik vervolgens op **Volumes**. In de lijst Hallo van volumes, ziet u Hallo klonen die is gemaakt in Hallo dezelfde volumecontainer met Hallo bronvolume.

    ![Back-upset lijst](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Een kloon dat is gemaakt op deze manier is een tijdelijke kloon. Zie voor meer informatie over de typen kloon [tijdelijke versus permanente klonen](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Tijdelijke versus permanente klonen
Tijdelijke klonen worden alleen gemaakt wanneer u tooanother apparaat klonen. U kunt een specifiek volume vanaf een back-upset tooa ander apparaat beheerd door Hallo StorSimple Apparaatbeheer klonen. Hallo tijdelijke kloon verwijzingen toohello gegevens in het oorspronkelijke volume Hallo gebruikt, en die gegevens tooread en write lokaal op Hallo doelapparaat.

Nadat u een cloud momentopname van een kloon van tijdelijke, Hallo resulterende kloon is een *permanente* kloon. Tijdens dit proces wordt een kopie van Hallo gegevens op Hallo cloud is gemaakt en Hallo tijd toocopy die deze gegevens wordt bepaald door de grootte Hallo Hallo gegevens en hello Azure latenties (dit is een exemplaar van Azure naar Azure). Dit kan tooweeks dagen duren. Hallo tijdelijke kloon wordt een permanente kloon en geen verwijzingen toohello oorspronkelijke volumegegevens dat deze is gekloond uit.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenario's voor tijdelijke en permanente klonen
Hallo volgende secties beschrijven voorbeeld situaties waarin tijdelijke en permanente klonen kunnen worden gebruikt.

### <a name="item-level-recovery-with-a-transient-clone"></a>Herstel op itemniveau met een tijdelijke kloon
U moet toorecover één jaar oude Microsoft PowerPoint-presentatie-bestand. Uw IT-beheerder identificeert Hallo specifieke back-up vanaf dat moment en vervolgens filters Hallo volume. Hallo beheerder en vervolgens Hallo volume klonen, zoekt de Hallo-bestand dat u zoekt, en stelt deze tooyou. In dit scenario wordt wordt een tijdelijke kloon gebruikt.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>In de productieomgeving Hallo met een permanente kloon testen
U moet een bug testen in productieomgeving Hallo tooverify. U maakt een kloon van Hallo volume in de productieomgeving Hallo en vervolgens een momentopname cloud van dit toocreate kloon een onafhankelijke gekloonde volume. In dit scenario wordt wordt een permanente kloon gebruikt.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[een StorSimple-volume herstelt vanuit een back-upset](storsimple-8000-restore-from-backup-set-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

