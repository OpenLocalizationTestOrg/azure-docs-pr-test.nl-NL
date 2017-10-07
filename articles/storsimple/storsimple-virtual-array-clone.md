---
title: een virtueel StorSimple-matrix back-up aaaClone | Microsoft Docs
description: Meer informatie over hoe tooclone een back-up en herstellen van een bestand van uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Klonen van een back-up van uw virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

In dit artikel wordt stapsgewijs beschreven hoe tooclone een back-upset van uw shares of volumes op uw Microsoft Azure StorSimple virtuele matrix. Hallo gekloonde back-up is gebruikte toorecover een bestand verwijderd of verloren. Hallo artikel bevat tevens gedetailleerde stappen tooperform een herstel op itemniveau op uw virtuele StorSimple-matrix die is geconfigureerd als een bestandsserver.

## <a name="clone-shares-from-a-backup-set"></a>Kloon-shares vanuit een back-upset

**Voordat u tooclone shares probeert, zorg ervoor dat er voldoende ruimte op Hallo apparaat toocomplete deze bewerking.** tooclone vanuit een back-up in Hallo [Azure-portal](https://portal.azure.com/), Hallo volgende stappen uit te voeren.

#### <a name="tooclone-a-share"></a>tooclone een share

1. Te bladeren**apparaten** blade. Selecteer en klik op het apparaat en klik vervolgens op **Shares**. Selecteer Hallo-share die u tooclone, Hallo share tooinvoke Hallo contextmenu wilt. Selecteer **kloon**.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. In Hallo **kloon** blade, klikt u op **back-up > Selecteer** en vervolgens Hallo te volgen: 
   
   a.    Een back-up op dit apparaat op basis van het tijdsbereik Hallo filteren. U kunt kiezen uit **afgelopen 7 dagen**, **afgelopen 30 dagen**, en **afgelopen jaar**.
   
   b.    Selecteer een back-tooclone uit in lijst Hallo van gefilterde back-ups weergegeven.
   
   c.    Klik op **OK**.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. In Hallo **kloon** blade, klikt u op **doel instellingen** en vervolgens Hallo te volgen:
   
   a.    Geef een sharenaam. Hallo sharenaam moet 3-127 tekens bevatten.
   
   b.    Geef optioneel een beschrijving voor de gekloonde share Hallo.
   
   c.    U kunt Hallo Hallo-share die u naar herstellen wilt type niet wijzigen. Een gelaagde share wordt gekloond als een gelaagde en een lokaal vastgemaakt share als lokaal vastgemaakt.
   
   d.    Hallo capaciteit is ingesteld als gelijk toohello grootte van Hallo share die u klonen uit.
   
   e.    Hallo-beheerders voor deze share toewijzen. U zijn kunt toomodify Hallo-eigenschappen voor bestandsdeling via Verkenner nadat de Hallo kloon is voltooid.
   
   f.    Klik op **OK**.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Klik op **kloon** toostart een taak voor de kloon. Nadat het Hallo-taak is voltooid, Hallo kopieerbewerking wordt gestart en u wordt gewaarschuwd. toomonitor hello voortgang van de kloon Ga toohello **taken** blade en klik op Hallo tooview taak taakdetails.
5. Nadat het Hallo kloon is gemaakt, gaat u terug toohello **Shares** blade op uw apparaat.
6. U kunt nu Hallo nieuwe gekloonde share weergeven in de lijst met shares Hallo op uw apparaat. Een gelaagde share is gekloond omdat lagen en een lokaal vastgemaakt share als een lokaal vastgemaakt share.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Volumes klonen van een back-upset

tooclone vanuit een back-up in hello Azure-portal hebt tooperform stappen vergelijkbaar toohello die bij het klonen van een share. Hallo kopieerbewerking kloont Hallo back-tooa nieuw volume op Hallo hetzelfde virtuele apparaat; tooa ander apparaat kan niet worden gekloond.

#### <a name="tooclone-a-volume"></a>een volume tooclone

1. Te bladeren**apparaten** blade. Selecteer en klik op het apparaat en klik vervolgens op **Volumes**. Gewenste tooclone, Hallo volume tooinvoke Hallo contextmenu selec Hallo-volume. Selecteer **kloon**.
   
   ![Een volume klonen](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. In Hallo **kloon** blade, klikt u op **back-up** en vervolgens Hallo te volgen: 
   
   a.    Een back-up op dit apparaat op basis van het tijdsbereik Hallo filteren. U kunt kiezen uit **afgelopen 7 dagen**, **afgelopen 30 dagen**, en **afgelopen jaar**. 
   
   b.    Selecteer een back-tooclone uit in lijst Hallo van gefilterde back-ups weergegeven.
   
   c.    Klik op **OK**.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. In Hallo **kloon** blade, klikt u op **volume-instellingen als doel** en vervolgens Hallo na::
   
   a. Hallo apparaatnaam wordt automatisch gevuld.
   
   b. Geef de naam van een volume voor Hallo **gekloond volume**. Hallo volumenaam moet 3 too127 tekens bevatten.
   
   c. Hallo-volumetype wordt het oorspronkelijke volume toohello automatisch ingesteld. Een gelaagd volume is gekloond omdat lagen en een lokaal vastgemaakt volume als lokaal vastgemaakt.
   
   d. Voor Hallo **verbonden hosts**, klikt u op **Selecteer**.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. In Hallo **verbonden hosts** blade uit een bestaande ACR selecteren of een nieuwe ACR toevoegen. een nieuwe ACR tooadd, moet u tooprovide ACR-naam en Hallo host IQN. Klik op **Selecteren**.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Klik op **kloon** toolaunch een taak voor de kloon.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Nadat het Hallo-kloon-taak is gemaakt, wordt klonen gestart. Zodra Hallo kloon is gemaakt, wordt deze weergegeven op Hallo Volumes blade op uw apparaat. Houd er rekening mee dat een gelaagd volume is gekloond omdat lagen en een lokaal vastgemaakt volume als een lokaal vastgemaakt volume wordt gekloond.
   
   ![Klonen van een back-up](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Zodra het Hallo-volume wordt weergegeven online op Hallo-lijst van volumes, is Hallo volume beschikbaar voor gebruik. Op Hallo iSCSI-initiator host Hallo-lijst met doelen in het eigenschappenvenster van iSCSI-initiator te vernieuwen. Een nieuw doel met de naam van de gekloonde volume Hallo moet worden weergegeven als 'inactive' onder de kolom status Hallo.
8. Hallo doel selecteren en op **Connect**. Nadat de Hallo initiator is verbonden toohello doel, Hallo moet statuswijziging te**verbonden**.
9. In Hallo **Schijfbeheer** venster hello gekoppelde volumes weergegeven zoals in Hallo volgende afbeelding. Met de rechtermuisknop op Hallo gedetecteerde volume (Klik op de naam van de schijf Hallo), en klik vervolgens op **Online**.

> [!IMPORTANT]
> Wanneer tooclone probeert een volume of een share van een back-upset als Hallo kloon taak mislukt, een doelvolume of share mogelijk nog steeds worden in Hallo portal gemaakt. Het is belangrijk dat u dit doelvolume verwijderen of delen in de portal toominimize Hallo toekomstige problemen die voortkomen uit dit element.
> 
> 

## <a name="item-level-recovery-ilr"></a>Herstel op itemniveau (ILR)

Deze release bevat Hallo van het herstel van itemniveau (ILR) op een virtueel StorSimple-matrix geconfigureerd als een bestandsserver. Hallo-functie kunt u toodo gedetailleerde bestanden en mappen herstellen uit een cloud back-up van alle Hallo shares op Hallo StorSimple-apparaat. U kunt verwijderde bestanden ophalen van recente back-ups met behulp van een selfservice-model.

Elke share heeft een *.backups* map met de meest recente back-ups Hallo. U kunt navigeren toohello gewenste back-up-, kopieer relevante bestanden en mappen van Hallo back-up en herstel deze. Deze functie wordt voorkomen dat tooadministrators aanroepen voor het herstellen van bestanden vanuit back-ups.

1. Bij het uitvoeren van Hallo ILR, kunt u Hallo back-ups via Verkenner kunt weergeven. Klik op specifieke Hallo-share die u wilt dat toolook op Hallo back-up voor. U ziet een *.backups* map gemaakt onder het Hallo-share die alle Hallo back-ups worden opgeslagen. Vouw Hallo *.backups* map tooview Hallo back-ups. Hallo-map bevat Hallo geëxplodeerde weergave van Hallo volledige back-hiërarchie. Deze weergave wordt gemaakt op aanvraag en gewoonlijk duurt slechts enkele seconden toocreate.
   
   Hallo laatste vijf back-ups op deze manier worden weergegeven en gebruikte tooperform een itemniveau herstel kunnen worden. Hallo vijf recente back-ups zijn beide Hallo standaard een geplande en Hallo handmatige back-ups.
   
   * **Geplande back-ups** met de naam als &lt;apparaatnaam&gt;DailySchedule JJJJMMDD-UUMMSS UTC.
   * **Handmatige back-ups** met de naam als Ad-hoc-JJJJMMDD-UUMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Identificeer Hallo back-up die Hallo meest recente versie van bestand Hallo verwijderd. Hoewel Hallo mapnaam een UTC-timestamp in elk van de voorgaande gevallen hello bevat, is Hallo welke Hallo map is gemaakt Hallo daadwerkelijk apparaattijd waarop hello back-up is gestart. Gebruik Hallo map tijdstempel toolocate en Hallo back-ups te identificeren.

3. Hallo-map of het Hallo-bestand dat u wilt toorestore in Hallo back-up die u hebt geïdentificeerd in de vorige stap Hallo niet vinden. Houd er rekening mee dat kunt u alleen Hallo bestanden of mappen die u machtigingen hebt voor bekijken. Als u geen toegang bepaalde bestanden of mappen tot, moet u contact op met de beheerder van een share. Hallo beheerder kunt Verkenner tooedit Hallo sharemachtigingen gebruiken en bieden u toegang tot toohello specifiek bestand of map. Het is aanbevolen dat Hallo beheerder van de share is een gebruikersgroep in plaats van een enkele gebruiker.

4. Hallo-bestand of Hallo map toohello juiste share op de bestandsserver StorSimple kopiëren.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het te[beheren van uw virtuele StorSimple-matrix met Hallo lokale webgebruikersinterface](storsimple-ova-web-ui-admin.md).

