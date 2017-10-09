---
title: aaaUse StorSimple 8000 series apparaatoverzicht | Microsoft Docs
description: Hallo Apparaatbeheer StorSimple-apparaat overzicht beschrijft en hoe toouse deze metrische gegevens tooview storage en verbonden initiators en zoeken Hallo serienummer en de IQN.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Hallo apparaatoverzicht in service Manager voor StorSimple-apparaat gebruiken

## <a name="overview"></a>Overzicht
Hallo StorSimple-apparaat samenvatting blade geeft een overzicht van gegevens voor een specifieke StorSimple-apparaat, in tegenstelling toohello service samenvatting blade waarmee u informatie over alle Hallo apparaten opgenomen in de Microsoft Azure StorSimple-oplossing.

Hallo apparaat samenvatting blade geeft een overzicht van een StorSimple 8000 serie-apparaat dat is geregistreerd bij een gegeven StorSimple apparaat Manager markeren die apparaat-problemen die aandacht vereisen een systeembeheerder. Deze zelfstudie Hallo apparaat samenvatting blade introduceert, wordt uitgelegd Hallo inhoud en de functie en Hallo worden taken beschreven die u vanuit deze blade uitvoeren kunt.

Hallo apparaat samenvatting blade geeft Hallo volgende informatie weer:

![Samenvatting blade apparaat](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Opdrachtbalk Management

In de blade voor Hallo StorSimple-apparaat ziet u Hallo opties voor het beheren van uw StorSimple-apparaat. Opdrachten voor het beheer van Hallo ziet u aan de bovenkant Hallo van Hallo blade en aan de linkerkant Hallo. Gebruikmaken van deze opties tooadd shares of volumes, bijwerken of failover van uw apparaat.

![Opdrachtbalk Management](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Essentials

Hallo essentials gebied vastgelegd Hallo belangrijke eigenschappen zoals, Hallo status, model, doel IQN en Hallo softwareversie. 

![Apparaat essentials](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>Bewaking

* Hallo **waarschuwingen** tegel biedt een momentopname van alle Hallo actieve waarschuwingen voor uw apparaat, gegroepeerd op de ernst van waarschuwing.

    ![Waarschuwing tegel](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Klik op Hallo tegel tooopen hello **waarschuwingen** blade en klik vervolgens op een afzonderlijke een waarschuwing tooview aanvullende details over deze waarschuwing, inclusief alle aanbevolen acties. U kunt ook een waarschuwing Hallo wissen als Hallo probleem is opgelost.

    ![Klik op de tegel waarschuwingen](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Hallo **Status en gezondheid** tegel biedt inzicht in de status van Hallo hardware-onderdeel voor een apparaat, inclusief het Hallo-Apparaatstatus. de apparaatstatus Hallo mogelijk offline, online, gedeactiveerd of gereed tooset up.

    ![Tegel status en gezondheid](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Hallo **Volumes** tegel bevat een samenvatting van Hallo aantal volumes in uw apparaat op status gegroepeerd.

    ![Tegel volumes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Klik op Hallo tegel tooopen hello **Volumes** blade lijst en klikt u op een afzonderlijke volume tooview of de eigenschappen wijzigen.
    
    ![Klik op de tegel volumes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Voor meer informatie Zie hoe te[volumes beheren](storsimple-8000-manage-volumes-u2.md).

* In Hallo **gebruik** grafiek, kunt u Hallo primaire opslag gebruikt via het apparaat en de Hallo cloud-opslag verbruikt Hallo afgelopen 7 dagen, Hallo standaard periode bekijken.

     ![Tegel gebruik](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     een andere tijdschaal toochoose hello gebruiken **bewerken** optie in de rechterbovenhoek Hallo van Hallo grafiek.

     ![Gebruiksgrafiek bewerken](./media/storsimple-8000-device-dashboard/device-summary12.png)

     In deze grafiek, u kunt metrische gegevens voor Hallo totale primaire opslag (Hallo hoeveelheid gegevens die zijn geschreven door hosts tooyour apparaat) weergeven en totale Hallo cloudopslag verbruikt door uw apparaat gedurende een periode.
  
     In deze context *primaire opslag* toohello totale hoeveelheid gegevens die zijn geschreven door Hallo host verwijst, en door volumetype kunnen worden onderverdeeld: *primaire gelaagde opslag* bevat zowel lokaal opgeslagen gegevens en gegevens gelaagde toohello cloud. *Primaire lokaal vastgemaakt opslag* bevat alleen gegevens die lokaal zijn opgeslagen. *Cloudopslag*, op Hallo daarentegen, is een meting van de totale hoeveelheid gegevens die zijn opgeslagen in de cloud Hallo Hallo. Deze opslag bevat gelaagde gegevens en back-ups. Hallo-gegevens die zijn opgeslagen in de cloud Hallo is ontdubbeld en gecomprimeerd, terwijl primaire opslag Hallo en de hoeveelheid opslagruimte gebruikt geeft voordat het Hallo-gegevens worden ontdubbeld en gecomprimeerd. (U kunt deze twee getallen tooget een idee van Hallo compressie tarief vergelijken.) Voor zowel de primaire en cloudopslag, Hallo bedragen die zijn gebaseerd op Hallo bijhouden frequentie die u configureert. Als u een frequentie van één week kiest, klikt u vervolgens ziet Hallo grafiek u bijvoorbeeld gegevens voor elke dag in Hallo vorige week.

     toosee hello hoeveelheid cloud-opslag verbruikt tijd, selecteer Hallo **CLOUD-opslag gebruikt** optie. toosee hello totale opslag die is geschreven door Hallo host, selecteer Hallo **primaire GELAAGDE opslag gebruikt** en **primaire lokaal VASTGEMAAKT opslag gebruikt** opties. 
     Zie voor meer informatie [gebruik Hallo StorSimple Apparaatbeheer service toomonitor uw StorSimple-apparaat](storsimple-monitor-device.md).


* Hallo **capaciteit** tegel geeft Hallo primaire opslag die is ingericht en de resterende over Hallo apparaat relatieve toohello totale opslag beschikbaar voor dezelfde Hallo. **Ingericht** toohello en de hoeveelheid opslagruimte die is voorbereid en toegewezen voor gebruik, verwijst **resterend** verwijst toohello resterende capaciteit die kan worden ingericht op dit apparaat. 

    ![Tegel gebruik](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Klik op deze tegel tooview hoe Hallo capaciteit is ingericht op de gelaagde en lokaal vastgemaakte volumes. Hallo **resterende gelaagde** capaciteit is Hallo beschikbare capaciteit die kan worden ingericht met inbegrip van de cloud, tijdens het Hallo **resterende lokale** is Hallo resterende capaciteit op Hallo schijven toothis apparaat is gekoppeld.

    ![Klik op de gebruiksgrafiek](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo [StorSimple-service samenvatting blade](storsimple-8000-service-dashboard.md).
* Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

