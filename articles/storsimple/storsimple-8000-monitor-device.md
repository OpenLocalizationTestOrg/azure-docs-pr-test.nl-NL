---
title: aaaMonitor uw StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe toouse hello StorSimple Apparaatbeheer service toomonitor gebruik, i/o-prestaties en gebruik van capaciteit.
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>Hallo Apparaatbeheer StorSimple-service toomonitor uw StorSimple-apparaat gebruiken
## <a name="overview"></a>Overzicht
U kunt Hallo Apparaatbeheer StorSimple-service toomonitor specifieke apparaten gebruiken in uw StorSimple-oplossing. U kunt aangepaste grafieken op basis van i/o-prestaties, gebruik van capaciteit, netwerkdoorvoer en maatstaven voor prestaties apparaat maken en deze toohello dashboard vastmaken. Voor meer informatie gaat te[portal dashboard aanpassen](/articles/azure-portal/azure-portal-dashboards.md).

tooview hello controlegegevens voor een bepaald apparaat in hello Azure-portal, selecteer Hallo Apparaatbeheer StorSimple-service. Selecteer uw apparaat in Hallo lijst met apparaten en gaat u verder te**Monitor**. Vervolgens kunt u zien Hallo **capaciteit**, **gebruik**, en **prestaties** grafieken voor het geselecteerde apparaat Hallo.

## <a name="capacity"></a>Capaciteit
**Capaciteit** houdt Hallo Hallo ruimte resterende op Hallo-apparaat en de ingerichte ruimte. Hallo resterende capaciteit wordt vervolgens weergegeven als lokaal vastgemaakt of lagen.

Hallo ingericht en de resterende capaciteit is verder uitgesplitst gelaagde en lokaal vastgemaakte volumes. Voor elk volume Hallo ingericht capaciteit en Hallo resterende capaciteit op Hallo-apparaat wordt weergegeven.

![I/o-capaciteit](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Gebruik
**Gebruik** houdt metrische gegevens gerelateerde toohello hoeveelheid opslagruimte die wordt gebruikt door het Hallo-volumes, volumecontainers of apparaat. U kunt rapporten op basis van het gebruik van het Hallo-capaciteit van uw primaire opslag, uw cloud-opslag of uw opslagruimte van het apparaat kunt maken. Capaciteitsverbruik kan op een bepaald volume, een specifieke volumecontainer of alle volumecontainers worden gemeten.
Standaard wordt Hallo-gebruik gedurende de afgelopen 24 uur gerapporteerd. U kunt Hallo grafiek toochange Hallo duur via welke Hallo gebruik is gemeld door het selecteren van bewerken:
* Afgelopen 24 uur
* Afgelopen 7 dagen
* Afgelopen 30 dagen
* Aantal voorbije 90 dagen
* Afgelopen jaar


Hallo primaire cloud en lokale opslag gebruikt kunnen als volgt worden beschreven:

### <a name="primary-storage-usage"></a>Primaire opslaggebruik
Deze grafieken weergegeven Hallo en de hoeveelheid gegevens geschreven tooStorSimple volumes voordat Hallo gegevens worden ontdubbeld en gecomprimeerd. Hallo primaire opslag van alle volumes in een volumecontainer of voor één volume, kunt u weergeven. Hallo primaire opslag gebruikt, is verder opgedeeld per primaire gelaagde opslag gebruikt en primaire lokaal vastgemaakt opslag gebruikt.

Hallo weergegeven volgende grafieken Hallo primaire gebruikt als opslag voor een StorSimple-apparaat voordat en nadat een cloudmomentopname is gemaakt. Als dit alleen de gegevens van het volume is, moet een cloudmomentopname Hallo primaire opslag niet wijzigen. Zoals u ziet, bevat Hallo grafiek geen verschil in Hallo primaire gelaagde of lokaal vastgemaakt opslag gebruikt als gevolg van een momentopname van de cloud. Hallo cloudmomentopname gestart op ongeveer 23:50:00 uur op het apparaat.

![Gebruik van de primaire capaciteit na cloudmomentopname](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

Als u nu i/o op Hallo host verbonden tooyour StorSimple-apparaat, u een toename van de primaire gelaagde opslag ziet of primaire lokaal opslag gebruikt, afhankelijk vastgemaakt van welke volumes (gelaagd of lokaal vastgemaakt) u Hallo gegevens schrijven naar. Hier volgen Hallo primaire opslag gebruik grafieken voor een StorSimple-apparaat. Op dit apparaat schrijft Hallo StorSimple host gestart voor de op een gelaagd volume op apparaat Hallo om ongeveer 2:30 uur. Hallo piek in Hallo schrijven bytes/s toohello i/o wordt uitgevoerd op host Hallo hoort, kunt u zien.

![Prestaties bij i/o waarop volumes gelaagde](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Als u hello primaire gelaagde opslag gebruikt bekijkt, die is geworden van terwijl Hallo primaire lokaal vastgemaakt gebruik ongewijzigd, blijft omdat er geen schrijfbewerkingen toohello lokaal vastgemaakte volumes geleverd op Hallo-apparaat.

![Gebruik van primaire capaciteit wanneer i/o op gelaagde volumes worden uitgevoerd](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Als u werkt met Update 3 of hoger, u kunt uitsplitsen naar primaire opslaggebruik capaciteit Hallo afzonderlijk volume, alle volumes, alle gelaagde volumes en alle lokaal vastgemaakte volumes zoals hieronder wordt weergegeven. De te analyseren door alle lokaal vastgemaakte volumes kunt u de tooquickly gaan hoeveel van de lokale laag Hallo van wordt gebruikt.

![Gebruik van de primaire capaciteit voor alle gelaagde volumes](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Gebruik van de primaire capaciteit voor alle lokaal vastgemaakte volumes](./media/storsimple-8000-monitor-device/monitor-usage4.png)

U kunt verder klikt u op elk van de volumes in de lijst Hallo Hallo en Zie Hallo overeenkomstige gebruik.

![Gebruik van de primaire capaciteit voor alle lokaal vastgemaakte volumes](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Gebruik van cloud-opslag
Deze grafieken weergegeven Hallo hoeveelheid cloudopslag die wordt gebruikt. Deze gegevens worden ontdubbeld en gecomprimeerd. Dit bedrag bevat cloudmomentopnamen die mogelijk gegevens bevatten die niet wordt weergegeven in de primaire volumes en bijgehouden voor verouderde of vereist bewaren doeleinden. U kunt vergelijken Hallo primaire cloud-opslag-verbruik cijfers tooget een idee van vermindering van Hallo gegevens classificeren, maar Hallo nummer is niet exact.

Hallo weergegeven volgende grafieken Hallo cloud gebruik van de opslag van een StorSimple-apparaat wanneer een cloudmomentopname is gemaakt.

* Hallo cloudmomentopname gestart op ongeveer 11:50 uur op het apparaat en kunt u zien dat voordat cloudmomentopname hello, er is geen cloud-opslag gebruikt. 
* Eenmaal Hallo cloudmomentopname is voltooid, Hallo cloud opslaggebruik geschoten up 0.89 GB. 
* Hallo cloudmomentopname werd uitgevoerd, is er ook een bijbehorende piek in Hallo i/o van het apparaat toocloud.

    ![Gebruik van de cloud-opslag voordat cloudmomentopname](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Gebruik van de cloud-opslag nadat de cloudmomentopname](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![I/o van het apparaat toocloud tijdens een cloudmomentopname](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Gebruik van lokale opslag
Deze grafieken weergegeven Hallo totale gebruik voor Hallo-apparaat, wordt er meer dan gebruik van primaire opslag omdat het lineaire SSD-laag Hallo omvat. Deze laag bevat een hoeveelheid gegevens die ook op Hallo andere lagen van het apparaat bestaat. Hallo capaciteit in lineaire Hallo SSD-laag is tijdens het bladeren uitlijnen dat als er nieuwe gegevens binnenkomt, oude gegevens Hallo verplaatste toohello HDD-laag (op dat moment is ontdubbeld en gecomprimeerd) en vervolgens toohello cloud.

Na verloop van tijd gelaagde primaire opslag gebruikt en lokale opslag gebruikt, wordt waarschijnlijk samen verhoogd totdat het Hallo-gegevens begint toobe toohello cloud. Op dat moment Hallo lokale opslag gebruikt waarschijnlijk tooplateau begint, maar Hallo primaire opslag gebruikt naarmate er meer gegevens worden geschreven.

Hallo weergegeven volgende grafieken Hallo primaire opslag gebruikt voor een StorSimple-apparaat wanneer een cloudmomentopname is gemaakt. Hallo cloudmomentopname begonnen om 11:50 am en Hallo lokale opslag op dat moment verlagen. Hallo lokale opslag gebruikt is gegaan omlaag van 1.445 GB too1.09 GB. Dit geeft aan dat waarschijnlijk hello niet-gecomprimeerde gegevens in Hallo lineaire SSD-laag is ontdubbeld, gecomprimeerd en naar het Hallo HDD-laag verplaatst. Houd er rekening mee dat als Hallo apparaat al een grote hoeveelheid gegevens in zowel Hallo SSD en HDD-opslaglagen heeft, u geen deze daling ziet mogelijk. In dit voorbeeld heeft Hallo-apparaat een kleine hoeveelheid gegevens.

![Gebruik van de lokale opslag nadat de cloudmomentopname](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Prestaties
**Prestaties** houdt metrische gegevens gerelateerd toohello aantal gelezen- en schrijfbewerkingen tussen beide Hallo iSCSI initiator-interfaces op Hallo-hostserver en Hallo-apparaat of Hallo-apparaat en Hallo cloud. De prestaties kan worden gemeten voor een specifiek volume, een specifieke volumecontainer of alle volumecontainers. Prestaties tevens CPU-gebruik en de netwerkdoorvoer voor Hallo verschillende netwerkinterfaces op uw apparaat.

### <a name="io-performance-for-initiator-toodevice"></a>I/o-prestaties voor initiator toodevice
Hallo diagram hieronder toont Hallo i/o voor Hallo initiator tooyour apparaat voor alle Hallo volumes voor een productie-apparaat. Hallo metrische gegevens uitgezet worden gelezen en geschreven bytes per seconde. U kunt ook grafiek lezen, schrijven en openstaande i/o, of lezen en schrijven latenties.

![I/o-prestaties voor initiator toodevice](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>I/o-prestaties voor apparaat toocloud
Voor Hallo hetzelfde apparaat Hallo i/o-bewerkingen worden getekend voor Hallo gegevens van Hallo apparaat toohello cloud voor alle volumecontainers Hallo. Op dit apparaat Hallo gegevens alleen in lineaire Hallo-laag en niets zich toohello cloud is verspreid. Er zijn geen lees-/ schrijfbewerkingen die voortkomen uit apparaat toohello cloud. Hallo pieken in de grafiek Hallo zijn daarom met een interval van 5 minuten dat overeenkomt met toohello frequentie waarmee Hallo heartbeat tussen Hallo-apparaat en Hallo-service wordt gecontroleerd.

Voor hello hetzelfde apparaat, een cloudmomentopname is gemaakt voor volumegegevens om 11:50 am wordt gestart. Dit resulteert in gegevens van Hallo apparaat toohello cloud. Schrijfbewerkingen zijn toohello cloud geleverd in deze duur. Hallo i/o-diagram toont een piek in de Hallo schrijven Bytes/sec. bijbehorende toohello tijd wanneer Hallo momentopname werd gemaakt.

![I/o van het apparaat toocloud tijdens een cloudmomentopname](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Netwerkdoorvoer voor netwerkinterfaces van apparaat
**Netwerkdoorvoer** houdt metrische gegevens gerelateerde toohello hoeveelheid gegevens overgedragen van Hallo iSCSI-initiator netwerkinterfaces op de hostserver Hallo en Hallo-apparaat en tussen Hallo-apparaat en Hallo cloud. U kunt met deze metriek voor elk van de iSCSI-netwerkinterfaces Hallo bewaken op uw apparaat.

Hallo volgende grafieken weergeven Hallo netwerkdoorvoer voor Hallo Data 0, 1-1 GbE-netwerk op uw apparaat, die beide cloud ingeschakeld (standaard) en iSCSI-functionaliteit. Gegevens is op dit apparaat op 14 juni middags ongeveer 9 lagen in Hallo-cloud (Er is geen cloud momentopnamen zijn gemaakt op die tijd welke punten tootiering wordt Hallo mechanisme toomove Hallo gegevens in de cloud Hallo) wat leidde tot i/o toohello cloud wordt geleverd. Er is een overeenkomstige piek in Hallo netwerk doorvoer grafiek voor hello hetzelfde moment en de meeste Hallo netwerkverkeer is uitgaande toohello cloud.

![Netwerkdoorvoer voor Data 0](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Als we Hallo Data 1 interface doorvoer grafiek bekijkt, een andere 1 GbE netwerkinterface die alleen was ingeschakeld voor iSCSI, wordt er vrijwel geen netwerkverkeer is in deze duur.

![Netwerkdoorvoer voor gegevens-1](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>CPU-gebruik voor apparaat
**CPU-gebruik** houdt metrische gegevens gerelateerd toohello CPU gebruikt op uw apparaat. Hallo volgende diagram toont Hallo CPU-gebruik statistieken voor een apparaat in productie.

![CPU-gebruik voor apparaat](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[hello StorSimple Apparaatbeheer service apparaat dashboard gebruiken](storsimple-device-dashboard.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

