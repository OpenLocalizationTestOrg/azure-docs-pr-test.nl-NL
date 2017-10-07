---
title: aaaClone uw StorSimple-volume | Microsoft Docs
description: Beschrijving van Hallo kloon van de verschillende typen en wanneer toouse, en wordt uitgelegd hoe u een back-upset tooclone afzonderlijk volume kunt gebruiken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a>Hallo StorSimple Manager-service tooclone een volume gebruiken
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Overzicht
Hallo StorSimple Manager-service **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt. U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.

![Back-upcatalogus pagina](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

Deze zelfstudie wordt beschreven hoe u een back-upset tooclone afzonderlijk volume kunt gebruiken. Ook wordt uitgelegd hoe Hallo verschil tussen *tijdelijke* en *permanente* klonen. 

## <a name="create-a-clone-of-a-volume"></a>Maak een kloon van een volume
U kunt een kloon maken op Hallo hetzelfde apparaat, een ander apparaat of zelfs een virtuele machine met behulp van een lokale of een cloudmomentopname van de.

#### <a name="tooclone-a-volume"></a>een volume tooclone
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad en selecteert u een back-upset.
2. Vouw Hallo back-upset tooview Hallo gekoppeld volumes. Klik op een volume te selecteren vanuit Hallo back-upset.
   
     ![Een volume klonen](./media/storsimple-clone-volume/HCS_Clone.png) 
3. Klik op **kloon** toobegin Hallo geselecteerd volume klonen.
4. In de wizard voor het Volume van de kloon van Hallo onder **naam en locatie opgeven**:
   
   1. Identificeer een doelapparaat. Dit is Hallo-locatie waar Hallo kloon wordt gemaakt. U kunt Hallo hetzelfde apparaat of geef een ander apparaat. Als u een volume dat is gekoppeld aan andere cloudserviceproviders (geen Azure) Hallo vervolgkeuze-lijst voor het doelapparaat hello alleen voor fysieke apparaten weergegeven wordt. Een volume dat is gekoppeld aan andere cloudserviceproviders op een virtueel apparaat kan niet worden gekloond.
      
      > [!NOTE]
      > Zorg ervoor dat Hallo capaciteit is vereist voor de kloon Hallo lager dan Hallo capaciteit die beschikbaar is op het doelapparaat Hallo is.
      > 
      > 
   2. Geef een unieke volumenaam voor de kloon. Hallo-naam moet tussen 3 en 127 tekens bevatten.
   3. Klik op het pijlpictogram Hallo ![pijltje](./media/storsimple-clone-volume/HCS_ArrowIcon.png) tooproceed toohello volgende pagina.
5. Onder **Geef hosts die dit volume kunnen gebruiken**:
   
   1. Geef een record voor toegangscontrole (ACR) voor Hallo kloon. U kunt een nieuwe ACR toevoegen of kiezen uit bestaande Hallo-lijst.
   2. Klik op het vinkje Hallo ![vinkje](./media/storsimple-clone-volume/HCS_CheckIcon.png)toocomplete Hallo-bewerking.
6. Een taak klonen wordt gestart en u wordt gewaarschuwd als Hallo kloon is gemaakt. Klik op **taak weergeven** toomonitor Hallo kloon taak op Hallo **taken** pagina.
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
Tijdelijke en permanente klonen worden alleen gemaakt wanneer u op tooa ander apparaat klonen. U kunt een specifiek volume vanaf een ander apparaat voor back-upset tooa klonen. Een kloon gemaakt op deze manier is een *tijdelijke* kloon. Hallo tijdelijke kloon verwijzingen toohello oorspronkelijke volume zijn en die tooread volume wordt gebruikt tijdens het schrijven van lokaal. 

Nadat u een cloud momentopname van een kloon van tijdelijke, Hallo resulterende kloon is een *permanente* kloon. Hallo permanente kloon is onafhankelijk en hoeft niet elk verwijzingen toohello oorspronkelijke volume dat deze is gekloond uit.  

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenario's voor tijdelijke en permanente klonen
Hallo volgende secties beschrijven voorbeeld situaties waarin tijdelijke en permanente klonen kunnen worden gebruikt.

### <a name="item-level-recovery-with-a-transient-clone"></a>Herstel op itemniveau met een tijdelijke kloon
U moet toorecover één jaar oude Microsoft PowerPoint-presentatie-bestand. Uw IT-beheerder identificeert Hallo specifieke back-up van die periode wordt voltooid en vervolgens filters Hallo volume. Hallo beheerder en vervolgens Hallo volume klonen, zoekt de Hallo-bestand dat u zoekt, en stelt deze tooyou. In dit scenario wordt wordt een tijdelijke kloon gebruikt. 

![Video beschikbaar](./media/storsimple-clone-volume/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe gebruikt u de Hallo klonen en herstellen van functies in StorSimple toorecover verwijderde bestanden, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>In de productieomgeving Hallo met een permanente kloon testen
U moet een bug testen in productieomgeving Hallo tooverify. U maakt een kloon van Hallo volume in de productieomgeving Hallo maken van een cloudmomentopname van de kloon. Hallo is gekloonde volume nu onafhankelijk. In dit scenario wordt wordt een permanente kloon gebruikt.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[een StorSimple-volume herstelt vanuit een back-upset](storsimple-restore-from-backup-set.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

