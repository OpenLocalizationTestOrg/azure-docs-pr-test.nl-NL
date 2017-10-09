---
title: aaaUse hello StorSimple Manager apparaat dashboard | Microsoft Docs
description: Hallo StorSimple Manager service apparaat dashboard worden beschreven en hoe toouse deze metrische gegevens tooview storage en verbonden initiators en zoeken Hallo serienummer en de IQN.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Hallo apparaat dashboard in StorSimple Manager-service gebruiken  

## <a name="overview"></a>Overzicht
Hallo StorSimple Manager apparaat dashboard geeft een overzicht van gegevens voor een specifieke StorSimple-apparaat, in tegenstelling toohello service-dashboard waarmee u informatie over alle Hallo-apparaten die zijn opgenomen in de Microsoft Azure StorSimple-oplossing.

![De dashboardpagina van apparaat](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

Hallo dashboard bevat Hallo volgende informatie:

* **Grafiekgebied** – ziet u Hallo relevante opslag metrische gegevens in het grafiekgebied Hallo Hallo boven aan het Hallo-dashboard. In deze grafiek, u kunt metrische gegevens voor Hallo totale primaire opslag (Hallo hoeveelheid gegevens die zijn geschreven door hosts tooyour apparaat) weergeven en totale Hallo cloudopslag verbruikt door uw apparaat gedurende een periode.
  
     In deze context *primaire opslag* toohello totale hoeveelheid gegevens die zijn geschreven door Hallo host verwijst, en door volumetype kunnen worden onderverdeeld: *primaire gelaagde opslag* bevat zowel lokaal opgeslagen gegevens en gegevens gelaagde toohello cloud; *primaire lokaal vastgemaakt opslag* bevat alleen gegevens die lokaal zijn opgeslagen. *Cloudopslag*, op Hallo daarentegen, is een meting van de totale hoeveelheid gegevens die zijn opgeslagen in de cloud Hallo Hallo. Dit omvat gelaagde gegevens en back-ups. Houd er rekening mee dat de gegevens die zijn opgeslagen in de cloud Hallo is ontdubbeld en gecomprimeerd, terwijl primaire opslag Hallo en de hoeveelheid opslagruimte gebruikt geeft voordat het Hallo-gegevens worden ontdubbeld en gecomprimeerd. (U kunt deze twee getallen tooget een idee van Hallo compressie tarief vergelijken.) Voor zowel de primaire en cloudopslag, Hallo bedragen wordt gebaseerd op Hallo bijhouden frequentie die u configureert. Bijvoorbeeld, als u een frequentie van één week kiest, klikt u vervolgens Hallo grafiek toont gegevens voor elke dag in Hallo vorige week.
  
     Hallo-grafiek kunt u als volgt configureren:
  
  * toosee hello hoeveelheid cloud-opslag verbruikt tijd, selecteer Hallo **CLOUD-opslag gebruikt** optie. toosee hello totale opslag die is geschreven door Hallo host, selecteer Hallo **primaire GELAAGDE opslag gebruikt** en **primaire lokaal VASTGEMAAKT opslag gebruikt** opties. In afbeelding Hallo zijn beide opties geselecteerd. Hallo-grafiek bevat daarom opslag bedragen voor zowel cloud als primaire opslag. Alle primaire opslag gebruikt eerdere tooinstalling Update 2 wordt vertegenwoordigd door Hallo **primaire GELAAGDE opslag gebruikt** regel.
  * De vervolgkeuzelijst Hallo in Hallo rechtsboven van Hallo grafiek toospecify een 1 week, 1 maand, 3 maanden of 1 jaar periode gebruiken. Let op het hoogste niveau grafiek Hallo wordt vernieuwd slechts één keer per dag en daarom wordt weergegeven van de vorige dag totalen Hallo.
    
    Zie voor meer informatie [gebruik Hallo StorSimple Manager service toomonitor uw StorSimple-apparaat](storsimple-monitor-device.md).
* **Overzicht gebruik** – In Hallo **overzicht gebruik** gebied kunt u zien Hallo hoeveelheid primaire opslag gebruikt, Hallo hoeveelheid ingerichte opslag en Hallo maximale capaciteit voor uw apparaat. Door het vergelijken van deze informatie over het gebruik cijfers toohello maximale hoeveelheid opslagruimte die beschikbaar is, ziet u in één oogopslag als u extra opslagruimte tooobtain nodig. Noteer dit overzicht wordt elke 15 minuten bijgewerkt en vanwege Hallo verschil in updatefrequentie, kan worden weergegeven verschillende aantallen dan die wordt weergegeven op Hallo grafiekgebied hierboven, dat wordt dagelijks bijgewerkt. Zie voor meer informatie [gebruik Hallo StorSimple Manager service toomonitor uw StorSimple-apparaat](storsimple-monitor-device.md).
* **Waarschuwingen** – hello **waarschuwingen** gebied bevat een overzicht van Hallo waarschuwingen voor uw apparaat. Waarschuwingen worden gegroepeerd op ernst en een telling van het aantal waarschuwingen op elk ernstniveau Hallo is opgegeven. Hallo waarschuwing ernst Hiermee opent u een bereik weergave van hello te klikken op een waarschuwing tabblad tooshow dat u alleen Hallo waarschuwingen van dat ernstniveau worden weergegeven voor dit apparaat.
* **Taken** – hello **taken** gebied toont Hallo van resultaat van recente activiteit van de taak. Dit kunt u zorgen dat Hallo-systeem werkt zoals verwacht, of u weet kunt dat u nodig hebt tootake corrigerende maatregelen. Klik op toosee meer informatie over de laatst voltooide taken **taken is voltooid in Hallo afgelopen 24 uur**.
* Hallo **snelle weergave** gebied op Hallo van Hallo dashboard biedt nuttige informatie zoals Apparaatmodel, serienummer, status, beschrijving en het aantal volumes.

U kunt ook failover configureren en weergeven van verbonden initiators van Hallo apparaat dashboard.

Hallo algemene taken die kunnen worden uitgevoerd op deze pagina zijn:

* Verbonden initiators weergeven
* Hallo apparaatserienummer vindt
* Hallo apparaat doel IQN zoeken

## <a name="view-connected-initiators"></a>Verbonden initiators weergeven
Vindt u Hallo iSCSI-initiators die verbonden tooyour van het apparaat zijn door te klikken op Hallo **weergave verbonden initiators** koppeling in Hallo **snelle weergave** gebied van uw apparaat-dashboard. Deze pagina bevat een in tabelvorm overzicht van Hallo-initiators die verbinding tooyour apparaat hebt gemaakt. Voor elke initiator kunt u het volgende zien:

* Hallo iSCSI Qualified Name (IQN) Hallo verbonden initiator.
* Hallo-naam van Hallo record voor toegangscontrole (ACR) waarmee deze verbonden initiator.
* Hallo IP-adres van Hallo verbonden initiator.
* Hallo netwerkinterfaces die Hallo-initiator is verbonden tooon uw opslagapparaat. Deze kunnen op 0 tooDATA 5 variëren van gegevens.
* Alle Hallo volumes die verbonden initiator Hallo is toegestaan volgens de huidige ACR configuratie toohello tooaccess.

Als u onverwachte initiators in deze lijst wordt weergegeven of ziet geen Hallo verwacht zijn, raadpleegt u uw ACR-configuratie. Maximaal 512 initiators verbinding kan maken tooyour apparaat.

## <a name="find-hello-device-serial-number"></a>Hallo apparaatserienummer vindt
Mogelijk moet u het serienummer Hallo apparaat wanneer u Microsoft Multipath I/O (MPIO) op Hallo apparaat configureert. Volgende stappen toofind hello apparaatserienummer Hallo uitvoeren.

#### <a name="toofind-hello-device-serial-number"></a>serienummer van toofind Hallo apparaat
1. Navigeer te**apparaten** > **Dashboard**.
2. Zoek in het rechterdeelvenster Hallo van dashboard Hallo Hallo **snelle weergave** gebied.
3. Schuif naar beneden en zoek Hallo serienummer.

## <a name="find-hello-device-target-iqn"></a>Hallo apparaat doel IQN zoeken
U moet mogelijk Hallo apparaat doel IQN wanneer u Hallo Challenge Handshake Authentication Protocol (CHAP) op uw StorSimple-apparaat configureren. Volgende stappen toofind Hallo apparaat doel IQN Hallo uitvoeren.

### <a name="toofind-hello-device-target-iqn"></a>toofind hello apparaat doel IQN
1. Navigeer te**apparaten** > **Dashboard**.
2. Zoek in het rechterdeelvenster Hallo van dashboard Hallo Hallo **snelle weergave** gebied.
3. Schuif naar beneden en Hallo doel IQN vinden.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo [StorSimple Manager servicedashboard](storsimple-service-dashboard.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

