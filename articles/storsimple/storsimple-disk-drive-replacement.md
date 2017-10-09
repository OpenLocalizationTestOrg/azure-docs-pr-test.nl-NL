---
title: aaaReplace een harde schijf op een StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooreplace een schijf station op een primaire behuizing StorSimple of een EBOD behuizing.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a>Vervangen van een harde schijf op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe u kunt verwijderen en vervangen door een slecht werkende of mislukte harde schijf op een Microsoft Azure StorSimple-apparaat. tooreplace een harde schijf, moet u:

* Werking stellen Hallo antitamper vergrendelen
* Hallo-schijfstation verwijderen
* Hallo vervangende schijf installeren

> [!IMPORTANT]
> Voordat verwijderen en een schijf vervangen Lees Hallo veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="disengage-hello-antitamper-lock"></a>Werking stellen Hallo antitamper vergrendelen
Deze procedure wordt uitgelegd hoe Hallo antitamper vergrendelingen voor uw StorSimple-apparaat kunnen worden in- of uitgeschakeld wanneer u de schijfstations Hallo vervangt. Hallo antitamper vergrendelingen zijn aangebracht in Hallo station carrier verwerkt en ze toegankelijk zijn via een kleine opening in Hallo vergrendeling sectie van Hallo-ingang. Schijven worden geleverd met Hallo vergrendelingen set toohello vergrendeld positie.

#### <a name="toounlock-hello-antitamper-lock"></a>toounlock hello antitamper vergrendelen
1. Hallo lock-toets (een 'tamperproof' T10 draai die Microsoft opgegeven) zorgvuldig invoegen in Hallo opening in ingang hello en in een socket. 
   
   > [!NOTE]
   > Als Hallo antitamper lock is geactiveerd, is Hallo rode indicator zichtbaar in Hallo opening.
   > 
   > 
   
    ![Vergrendelde schijfstation](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Afbeelding 1** antivirusprogramma draagbare vergrendeling is ingeschakeld
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |Indicator opening |
   | 2 |Antitamper vergrendelen |
2. Hallo-sleutel in een Linksomdraaiend richting draaien totdat Hallo rode indicator niet zichtbaar in Hallo opening hierboven Hallo-sleutel is.
3. Hallo sleutel verwijderen.
   
    ![Niet-vergrendelde schijfstation](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Afbeelding 2** ontgrendeld harde schijf
4. Hallo-schijfstation kunnen nu worden verwijderd.

Volg de stappen Hallo in omgekeerde tooengage Hallo vergrendelen.

## <a name="remove-hello-disk-drive"></a>Hallo-schijfstation verwijderen
Uw StorSimple-apparaat ondersteunt een RAID 10-achtige spaties opslagconfiguratie. Dit betekent dat het normaal gesproken met een mislukte schijf SSD-schijf (SSD werken kan) of harde schijf drive (HDD). 

> [!IMPORTANT]
> * Als uw systeem meer dan één niet-werkende schijf heeft, verwijder niet meer dan één SSD of harde schijf van Hallo systeem op elk gewenst moment in de tijd. Dit kan leiden tot verlies van gegevens.
> * Zorg ervoor dat u een vervangende SSD plaatsen in een sleuf dat eerder een SSD bevatte. Plaats een vervangende harde schijf op dezelfde manier in een sleuf dat eerder een harde schijf bevatte.
> * Sleuven zijn in de klassieke Azure-portal hello, genummerd van 0 – 11. Daarom als Hallo portal ziet u een schijf in de sleuf 2 is mislukt, op Hallo apparaat zoekt Hallo defecte schijf in de derde sleuf Hallo van Hallo boven links.
> 
> 

Schijven worden verwijderd en vervangen tijdens het Hallo-systeem werkt.

#### <a name="tooremove-a-drive"></a>een station tooremove
1. tooidentify Hallo van niet-werkende schijf, in Hallo klassieke Azure-portal, gaat u te**apparaten** > **onderhoud** > **hardwarestatus**. Omdat een schijf kan niet in de primaire behuizing Hallo en/of in een behuizing EBOD (als u van een model 8600 gebruikmaakt), Hallo status van schijven Hallo onder bekijken **gedeelde onderdelen** en klikt u onder **EBOD behuizing gedeelde onderdelen**. Een niet-werkende schijf in de behuizing worden weergegeven met een rode status.
2. Hallo-stations vinden in Hallo voorzijde van primaire behuizing Hallo of Hallo EBOD behuizing. 
3. Als het Hallo-schijf is ontgrendeld, gaat u verder toohello volgende stap. Als het Hallo-schijf is vergrendeld, deze ontgrendelen met na Hallo-procedure in [werking stellen Hallo antitamper vergrendeling](#disengage-the-antitamper-lock).
4. Druk op Hallo zwart vergrendelingen op Hallo station carrier module en pull-hallo station carrier ingang af en opslag van Hallo voor van Hallo chassis. 
   
    ![Schijfstation ingang vrijgeven](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Afbeelding 3** vrijgeven Hallo station ingang
5. Wanneer Hallo station carrier ingang volledig is uitgebreid, schuift u Hallo station carrier buiten het Hallo-chassis. 
   
    ![Schijf buiten het schijfstation Verschuivend](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Afbeelding 4** Verschuivend Hallo schijfstation buiten het Hallo-provider

## <a name="install-hello-replacement-disk-drive"></a>Hallo vervangende schijf installeren
Nadat een station in uw StorSimple-apparaat is mislukt en u deze hebt verwijderd, voert u deze procedure tooreplace deze met een nieuwe schijf.

#### <a name="tooinsert-a-drive"></a>een station tooinsert
1. Zorg ervoor dat Hallo station carrier ingang volledig is uitgebreid, zoals wordt weergegeven in Hallo installatiekopie te volgen.
   
    ![Harde schijf met de ingang uitgebreid](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Afbeelding 5** station met de ingang uitgebreid
2. Schuif Hallo station carrier alle Hallo manier in Hallo chassis. 
   
    ![Schijf naar schijf carrier Verschuivend](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Afbeelding 6** schuifregelaar Hallo station carrier in Hallo-chassis
3. Met de Hallo station carrier aanwezig is, sluit Hallo station carrier ingang tijdens de bewerking wordt voortgezet toopush Hallo station carrier in Hallo chassis, tot Hallo station carrier ingang in een vergrendelde positie is uitgelijnd.
4. Hallo vergrendeling sleutel gebruiken die werd geleverd door Microsoft (tamperproof Torx draai) toosecure Hallo carrier ingang naar de juiste plaats door in te schakelen Hallo vergrendeling installatie inschakelen van een kwartaal rechtsom.
5. Controleer of Hallo vervanging is geslaagd en Hallo station op Hallo klassieke Azure-portal te openen en te navigeren operationele is**onderhoud** > **hardwarestatus**. Onder **gedeelde onderdelen** of **EBOD behuizing gedeelde onderdelen**, moet de Hallo stationsstatus groen is, die aangeeft of dit in orde is.
   
   > [!NOTE]
   > Het kan enkele uren duren voordat Hallo schijf status tooturn groen na Hallo vervanging.
   > 
   > 

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).

