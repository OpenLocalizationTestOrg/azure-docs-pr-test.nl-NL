---
title: aaaClone StorSimple 8000 series volume | Microsoft Docs
description: Beschrijving van Hallo kloon van de verschillende typen en wanneer toouse, en wordt uitgelegd hoe u een back-upset tooclone afzonderlijk volume kunt gebruiken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Hallo StorSimple Manager-service tooclone een volume (Update 2) gebruiken
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Overzicht
Hallo StorSimple Manager-service **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt. U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.

![Back-upcatalogus pagina](./media/storsimple-clone-volume-u2/backupCatalog.png)  

Deze zelfstudie wordt beschreven hoe u een back-upset tooclone afzonderlijk volume kunt gebruiken. Ook wordt uitgelegd hoe Hallo verschil tussen *tijdelijke* en *permanente* klonen.

> [!NOTE]
> Een lokaal vastgemaakt volume wordt als een gelaagd volume worden gekloond. Als u moet de gekloonde volume toobe lokaal vastgemaakt hello, kunt u Hallo kloon tooa lokaal vastgemaakt volume converteren nadat Hallo kloonbewerking is voltooid. Ga voor informatie over het converteren van een gelaagd volume tooa lokaal volume vastgemaakt, te[Hallo volumetype wijzigen](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Als u een gekloonde volume van gelaagde toolocally vastgemaakt onmiddellijk na het klonen probeert (wanneer deze nog steeds een tijdelijke kloon wordt) tooconvert, mislukt Hallo conversie met de Hallo volgende foutbericht weergegeven:
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Deze fout wordt alleen als u op een ander apparaat tooa klonen ontvangen. U kunt met succes Hallo volume toolocally vastgemaakt als u eerst Hallo tijdelijke kloon tooa permanente kloon converteren converteren. Hallo tijdelijke kloon tooa tooconvert permanente klonen, een momentopname van de cloud ervan.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Maak een kloon van een volume
U kunt een kloon maken op hetzelfde apparaat, een ander apparaat of zelfs een virtuele machine met behulp van een lokale hello of een momentopname cloud.

#### <a name="tooclone-a-volume"></a>een volume tooclone
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad en selecteert u een back-upset.
2. Vouw Hallo back-upset tooview Hallo gekoppeld volumes. Klik op een volume te selecteren vanuit Hallo back-upset.
   
     ![Een volume klonen](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Klik op **kloon** toobegin Hallo geselecteerd volume klonen.
4. In de wizard voor het Volume van de kloon van Hallo onder **naam en locatie opgeven**:
   
   1. Identificeer een doelapparaat. Dit is Hallo-locatie waar Hallo kloon wordt gemaakt. U kunt Hallo hetzelfde apparaat of geef een ander apparaat. Als u een volume dat is gekoppeld aan andere cloudserviceproviders (geen Azure) Hallo vervolgkeuze-lijst voor het doelapparaat hello alleen voor fysieke apparaten weergegeven wordt. Een volume dat is gekoppeld aan andere cloudserviceproviders op een virtueel apparaat kan niet worden gekloond.
      
      > [!NOTE]
      > Zorg ervoor dat Hallo capaciteit is vereist voor de kloon Hallo lager dan Hallo capaciteit die beschikbaar is op het doelapparaat Hallo is.
      > 
      > 
   2. Geef een unieke volumenaam voor de kloon. Hallo-naam moet tussen 3 en 127 tekens bevatten. 
      
      > [!NOTE]
      > Hallo **kloon Volume als** veld **tiers verdeelde** zelfs als u bij het klonen van een lokaal vastgemaakt volume. U kunt deze instelling; niet wijzigen echter, als u moet de gekloonde volume toobe lokaal vastgemaakt ook hello, kunt u converteren Hallo kloon tooa lokaal vastgemaakt volume nadat u Hallo kloon is gemaakt. Ga voor informatie over het converteren van een gelaagd volume tooa lokaal volume vastgemaakt, te[Hallo volumetype wijzigen](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Kloon wizard 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Klik op het pijlpictogram Hallo ![pijltje](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello volgende pagina.
5. Onder **Geef hosts die dit volume kunnen gebruiken**:
   
   1. Geef een record voor toegangscontrole (ACR) voor Hallo kloon. U kunt een nieuwe ACR toevoegen of kiezen uit bestaande Hallo-lijst.
      
        ![Kloon wizard 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Klik op het vinkje Hallo ![vinkje](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)toocomplete Hallo-bewerking.
6. Een taak klonen wordt gestart en u wordt gewaarschuwd als Hallo kloon is gemaakt. Klik op **taak weergeven** toomonitor Hallo kloon taak op Hallo **taken** pagina. Hier ziet u Hallo volgende bericht wanneer Hallo kloon taak is voltooid:
   
    ![Kloon-bericht](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Na het Hallo is kloon taak voltooid:
   
   1. Ga toohello **apparaten** pagina en selecteer Hallo **Volumecontainers** tabblad. 
   2. Hallo-volumecontainer die is gekoppeld aan Hallo bronvolume die u selecteert. U ziet in de lijst Hallo van volumes, Hallo klonen die is gemaakt.

> [!NOTE]
> Bewaking en het standaard back-up worden automatisch uitgeschakeld op een gekloonde volume.
> 
> 

Een kloon dat is gemaakt op deze manier is een tijdelijke kloon. Zie voor meer informatie over de typen kloon [tijdelijke versus permanente klonen](#transient-vs-permanent-clones).

De kloon is nu een gewone volume en bewerking die mogelijk is op een volume, zijn beschikbaar voor Hallo kloon. U moet tooconfigure dit volume voor een back-ups.

## <a name="transient-vs-permanent-clones"></a>Tijdelijke versus permanente klonen
Tijdelijke klonen worden alleen gemaakt wanneer u bij het klonen van tooa ander apparaat. U kunt een specifiek volume vanaf een back-upset tooa ander apparaat beheerd door Hallo StorSimple Manager klonen. Hallo tijdelijke kloon wordt verwijzingen toohello gegevens bevatten in de oorspronkelijke volume Hallo en gebruikt die gegevens tooread en schrijven lokaal op Hallo doelapparaat. 

Nadat u een cloud momentopname van een kloon van tijdelijke, Hallo resulterende kloon is een *permanente* kloon. Tijdens dit proces wordt een kopie van Hallo gegevens op Hallo cloud is gemaakt en Hallo tijd toocopy die deze gegevens wordt bepaald door de grootte Hallo Hallo gegevens en hello Azure latenties (dit is een exemplaar van Azure naar Azure). Dit kan tooweeks dagen duren. Hallo tijdelijke kloon wordt een permanente klonen op deze manier en geen verwijzingen toohello oorspronkelijke volumegegevens dat deze is gekloond uit. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenario's voor tijdelijke en permanente klonen
Hallo volgende secties beschrijven voorbeeld situaties waarin tijdelijke en permanente klonen kunnen worden gebruikt.

### <a name="item-level-recovery-with-a-transient-clone"></a>Herstel op itemniveau met een tijdelijke kloon
U moet toorecover één jaar oude Microsoft PowerPoint-presentatie-bestand. Uw IT-beheerder identificeert Hallo specifieke back-up van die periode wordt voltooid en vervolgens filters Hallo volume. Hallo beheerder en vervolgens Hallo volume klonen, zoekt de Hallo-bestand dat u zoekt, en stelt deze tooyou. In dit scenario wordt wordt een tijdelijke kloon gebruikt. 

![Video beschikbaar](./media/storsimple-clone-volume-u2/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe gebruikt u de Hallo klonen en herstellen van functies in StorSimple toorecover verwijderde bestanden, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>In de productieomgeving Hallo met een permanente kloon testen
U moet een bug testen in productieomgeving Hallo tooverify. U maakt een kloon van Hallo volume in de productieomgeving Hallo en vervolgens een momentopname cloud van dit toocreate kloon een onafhankelijke gekloonde volume. In dit scenario wordt wordt een permanente kloon gebruikt.  

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[een StorSimple-volume herstelt vanuit een back-upset](storsimple-restore-from-backup-set-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

