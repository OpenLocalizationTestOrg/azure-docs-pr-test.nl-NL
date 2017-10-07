---
title: aaaMicrosoft virtuele StorSimple-matrix Azure back-zelfstudie | Microsoft Docs
description: Hierin wordt beschreven hoe tooback up virtuele StorSimple-matrix deelt en volumes.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Back-up shares of volumes op uw virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

Hallo virtuele StorSimple-matrix is een hybride cloud-opslag on-premises virtuele apparaat die kan worden geconfigureerd als een bestandsserver of een iSCSI-server. Hallo virtuele matrix kunt Hallo gebruiker toocreate geplande en handmatige back-ups van alle Hallo shares of volumes op Hallo-apparaat. Wanneer geconfigureerd als een bestandsserver, kunt u ook herstel op itemniveau. Deze zelfstudie wordt beschreven hoe toocreate gepland en handmatige back-ups en herstel op itemniveau toorestore een verwijderd bestand op uw virtuele matrix uitvoeren.

Deze zelfstudie geldt toohello StorSimple virtuele matrices alleen. Voor informatie over 8000-serie gaat te[een back-up voor 8000 series apparaat maken](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Back-up-shares en -volumes

Back-ups punt in tijd beveiliging bieden, verbeteren de herstelmogelijkheden en hersteltijden voor shares en -volumes te minimaliseren. U kunt back-up een share of het volume op uw StorSimple-apparaat op twee manieren: **geplande** of **handmatige**. Elk van de methoden hello wordt besproken in Hallo uit te voeren.

## <a name="change-hello-backup-start-time"></a>De back-begintijd Hallo wijzigen

> [!NOTE]
> In deze release worden geplande back-ups gemaakt door een standaardbeleid dat wordt dagelijks wordt uitgevoerd op een opgegeven periode zijn uitgevoerd en een back-up alle Hallo shares of volumes op Hallo-apparaat. Het is niet mogelijk toocreate aangepaste beleidsregels voor geplande back-ups op dit moment.


Uw virtuele StorSimple-matrix heeft een standaard back-upbeleid dat begint op een bepaald tijdstip van de dag (22.30) en een back-up alle Hallo shares of volumes op Hallo apparaat eenmaal per dag. U kunt wijzigen Hallo tijd op welke Hallo back-up wordt gestart, maar de Hallo frequentie en het Hallo bewaren (die geeft het aantal back-ups tooretain Hallo) kan niet worden gewijzigd. Tijdens deze back-ups, Hallo gehele virtuele apparaat back-up. Dit kan mogelijk invloed hebben op prestaties Hallo Hallo-apparaat en van invloed zijn op Hallo werkbelastingen die zijn geïmplementeerd op Hallo-apparaat. Daarom raden we u aan deze back-ups te plannen voor daluren.

 toochange hello standaardback-up begintijd, voert u stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>toochange hello begintijd voor back-upbeleid voor Hallo-standaard

1. Ga te**apparaten**. Hallo-lijst met apparaten die zijn geregistreerd bij uw StorSimple-apparaat Manager-service wordt weergegeven. 
   
    ![Navigeer toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Selecteer en klikt u op uw apparaat. Hallo **instellingen** blade wordt weergegeven. Ga te**beheren > back-upbeleid**.
   
    ![Selecteer het apparaat](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. In Hallo **back-upbeleid** blade Hallo standaardbegintijd is 22:30. In de tijdzone apparaat kunt u nieuwe begintijd Hallo voor Hallo dagelijks schema.
   
    ![Navigeer toobackup beleid](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Klik op **Opslaan**.

### <a name="take-a-manual-backup"></a>Maak een handmatige back-up

Bovendien tooscheduled back-ups, u kunt nemen handmatige (op aanvraag) reservekopie van apparaatgegevens op elk gewenst moment.

#### <a name="toocreate-a-manual-backup"></a>toocreate een handmatige back-up

1. Ga te**apparaten**. Selecteer uw apparaat en met de rechtermuisknop op **...**  op Hallo uiterst rechts in de geselecteerde rij Hallo. Selecteer in het contextmenu hello, **back-up maken**.
   
    ![Navigeer tootake back-up](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. In Hallo **back-up maken** blade, klikt u op **back-up maken**. Dit wordt back-up alle Hallo shares op de bestandsserver Hallo of alle Hallo-volumes op de iSCSI-server. 
   
    ![back-up wordt gestart](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Een op aanvraag back-up wordt gestart en u ziet dat er een back-uptaak is gestart.
   
    ![back-up wordt gestart](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Zodra het Hallo-taak is voltooid, wordt u nogmaals gewaarschuwd. back-upproces Hallo vervolgens wordt gestart.
   
    ![back-uptaak gemaakt](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. tootrack hello voortgang van de back-ups Hallo en bekijk de taakdetails hello, klik op Hallo-melding. Hiermee gaat u verder te **taakgegevens**.
   
     ![details van de back-uptaak](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Nadat het Hallo back-up is voltooid, gaat u te**Management > back-upcatalogus**. U ziet een cloudmomentopname van alle shares hello (of volumes) op uw apparaat.
   
    ![Voltooide back-up](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Bestaande back-ups weergeven
tooview hello bestaande back-ups uitvoeren Hallo stappen te volgen in hello Azure-portal.

#### <a name="tooview-existing-backups"></a>tooview bestaande back-ups

1. Ga te**apparaten** blade. Selecteer en klikt u op uw apparaat. In Hallo **instellingen** blade te gaan**Management > back-upcatalogus**.
   
    ![Navigeer toobackup catalogus](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Geef Hallo criteria toobe gebruikt voor het filteren te volgen:
   
    - **Tijdsbereik** – kan **afgelopen 1 uur**, **afgelopen 24 uur**, **afgelopen 7 dagen**, **afgelopen 30 dagen**, **afgelopen jaar**, en **aangepaste datum**.
    
    - **Apparaten** – Selecteer in de lijst Hallo van bestandsservers of iSCSI-servers geregistreerd bij uw StorSimple-apparaat Manager-service.
   
    - **Geïnitieerd** – automatisch kunnen worden **geplande** (door een back-upbeleid) of **handmatig** gestart (door u).
   
    ![Back-ups filteren](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Klik op **Toepassen**. Hallo gefilterde lijst van back-ups wordt weergegeven in Hallo **back-upcatalogus** blade. Opmerking alleen 100 back-elementen kunnen worden weergegeven op een bepaald moment.
   
    ![Bijgewerkte back-upcatalogus](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

