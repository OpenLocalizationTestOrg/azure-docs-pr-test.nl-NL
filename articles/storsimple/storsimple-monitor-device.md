---
title: aaaMonitor uw StorSimple-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo StorSimple Manager service toomonitor i/o-prestaties, gebruik van capaciteit, netwerkdoorvoer en prestaties van een apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Hallo StorSimple Manager-service toomonitor uw StorSimple-apparaat gebruiken
## <a name="overview"></a>Overzicht
U kunt Hallo StorSimple Manager-service toomonitor specifieke apparaten gebruiken in uw StorSimple-oplossing. U kunt aangepaste grafieken op basis van i/o-prestaties, gebruik van capaciteit, netwerkdoorvoer en maatstaven voor prestaties apparaat maken. 

tooview hello controlegegevens voor een specifiek apparaat, in Hallo klassieke Azure-portal, selecteer Hallo StorSimple Manager-service. Klik op Hallo **Monitor** tabblad en selecteer vervolgens in Hallo lijst met apparaten. Hallo **Monitor** pagina Hallo volgende informatie bevat.

## <a name="io-performance"></a>I/o-prestaties
**I/o-prestaties** houdt metrische gegevens gerelateerd toohello aantal gelezen- en schrijfbewerkingen tussen beide Hallo iSCSI initiator-interfaces op Hallo-hostserver en Hallo-apparaat of Hallo-apparaat en Hallo cloud. De prestaties kan worden gemeten voor een specifiek volume, een specifieke volumecontainer of alle volumecontainers.

Hallo diagram hieronder toont Hallo i/o voor Hallo initiator tooyour apparaat voor alle Hallo volumes voor een productie-apparaat. Hallo metrische gegevens uitgezet worden gelezen en geschreven bytes per seconde, lezen en schrijven van i/o-bewerkingen per seconde, en lezen en schrijven latenties.

![I/o-prestaties van de initiator toodevice](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Voor Hallo hetzelfde apparaat Hallo i/o-bewerkingen worden getekend voor Hallo gegevens van Hallo apparaat toohello cloud voor alle volumecontainers Hallo. Op dit apparaat Hallo gegevens alleen in lineaire Hallo-laag en niets zich toohello cloud is verspreid. Er zijn geen lees-/ schrijfbewerkingen die voortkomen uit apparaat toohello cloud. Hallo pieken in de grafiek Hallo zijn daarom met een interval van 5 minuten dat overeenkomt met toohello frequentie waarmee Hallo heartbeat tussen Hallo-apparaat en Hallo-service wordt gecontroleerd. 

![I/o-prestaties van apparaat toocloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Voor hello hetzelfde apparaat, een cloudmomentopname is gemaakt voor volumegegevens vanaf 14:00 uur. Dit resulteert in gegevens van Hallo apparaat toohello cloud. Lezen / schrijven zijn toohello cloud geleverd in deze duur. Hallo IO diagram toont een piek in Hallo verschillende metrische gegevens overeenkomt toohello tijd wanneer Hallo momentopname werd gemaakt. 

![I/o-prestaties voor apparaat toocloud na cloudmomentopname](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Capaciteitsverbruik
**Capaciteitsverbruik** houdt metrische gegevens gerelateerde toohello hoeveelheid opslagruimte die wordt gebruikt door het Hallo-volumes, volumecontainers of apparaat. U kunt rapporten op basis van het gebruik van het Hallo-capaciteit van uw primaire opslag, uw cloud-opslag of uw opslagruimte van het apparaat kunt maken. Capaciteitsverbruik kan op een bepaald volume, een specifieke volumecontainer of alle volumecontainers worden gemeten.

Hallo primaire cloud en apparaat opslagcapaciteit kunnen als volgt worden beschreven:

### <a name="primary-storage-capacity-utilization"></a>Primaire verbruik van de opslagcapaciteit
Deze grafieken weergegeven Hallo en de hoeveelheid gegevens geschreven tooStorSimple volumes voordat Hallo gegevens worden ontdubbeld en gecomprimeerd. U kunt gebruik van de primaire opslag Hallo weergeven door alle volumes of voor één volume.

Wanneer u hello primaire opslag volume capaciteit gebruik grafieken voor alle volumes ten opzichte van elk van de afzonderlijke volumes Hallo en totaliseren Hallo primaire gegevens in beide gevallen deze bekijkt, kan er een niet-overeenkomend tussen twee getallen Hallo. Hallo totale primaire gegevens op alle volumes kan niet worden toegevoegd van totaal toohello met primaire gegevens van de afzonderlijke volumes Hallo Hallo. Dit kan worden veroorzaakt tooone van Hallo volgende:

* **Momentopnamegegevens opgenomen voor alle volumes**: dit gedrag wordt gezien alleen als u versie ouder is dan Update 3. Hallo primaire gegevens weergegeven voor alle Hallo volumes is Hallo som van Hallo primaire gegevens voor elk volume en Hallo momentopname. Hallo primaire gegevens weergegeven voor een bepaald volume komt overeen tooonly Hallo hoeveelheid gegevens die zijn toegewezen op Hallo volume (en omvat geen bijbehorende volume Hallo-momentopnamegegevens).
  
    Dit kan ook worden verklaard door Hallo vergelijking te volgen:
  
    *Primaire gegevens (alle volumes) = de som van (primaire gegevens (volume i) + grootte van de momentopnamegegevens (volume i))*
  
    *Wanneer primaire gegevens (volume i) = grootte van de primaire gegevens toegewezen toovolume ik*
  
    Als Hallo momentopnamen worden verwijderd via Hallo-service, Hallo verwijdering gebeurt asynchroon op Hallo achtergrond. Het kan even duren voor Hallo volume gegevens grootte toobe bijgewerkt na Hallo momentopname verwijderen. 
  
    Als met Update 3 of hoger, klikt u vervolgens Hallo momentopnamegegevens niet opgenomen in Hallo volumegegevens. En Hallo primaire gebruik is als volgt berekend:
  
    * Primaire gegevens (alle volumes) = de som van (primaire gegevens (volume i)
  
    *Wanneer primaire gegevens (volume i) = grootte van de primaire gegevens toegewezen toovolume ik*
* **Volumes met bewaking uitgeschakeld opgenomen in alle volumes**: als u volumes op het apparaat waarvoor bewaking is uitgeschakeld hebt, het bewaken van gegevens voor deze afzonderlijke volumes Hallo niet meer beschikbaar in Hallo grafieken. Hallo-gegevens voor alle volumes in de grafiek Hallo bevat echter Hallo volumes waarvoor bewaking is uitgeschakeld. 
* **Volumes met een live gekoppelde back-ups opgenomen voor alle volumes verwijderd**: als volumes met momentopnamegegevens worden verwijderd, maar momentopnamen Hallo die zijn gekoppeld, nog bestaan, wordt er een niet-overeenkomend.
* **Volumes die zijn opgenomen voor alle volumes verwijderd**: In sommige gevallen oude volumes mogelijk bestaat, zelfs als deze zijn verwijderd. Hallo effect van verwijdering niet te zien en Hallo apparaat kan tonen lagere beschikbare capaciteit. U moet deze volumes toocontact Microsoft Support tooremove.

Hallo weergegeven volgende grafieken Hallo primaire verbruik van de opslagcapaciteit van een StorSimple-apparaat voordat en nadat een cloudmomentopname is gemaakt. Als dit alleen de gegevens van het volume is, moet een cloudmomentopname Hallo primaire opslag niet wijzigen. Zoals u ziet, bevat Hallo grafiek geen verschil tussen het gebruik van de primaire capaciteit Hallo als gevolg van een momentopname van de cloud. Hallo cloudmomentopname gestart op ongeveer 14:00 uur op het apparaat.

![Gebruik van de primaire capaciteit voordat cloudmomentopname](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Gebruik van de primaire capaciteit na cloudmomentopname](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Als u werkt met Update 2 of hoger, u kunt uitsplitsen naar primaire opslaggebruik capaciteit Hallo afzonderlijk volume, alle volumes, alle gelaagde volumes en alle lokaal vastgemaakte volumes zoals hieronder wordt weergegeven. De te analyseren door alle lokaal vastgemaakte volumes kunt u de tooquickly gaan hoeveel van de lokale laag Hallo van wordt gebruikt.

![Gebruik van de primaire capaciteit voor alle lokaal vastgemaakte volumes](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Gebruik van cloud-opslag-capaciteit
Deze grafieken weergegeven Hallo hoeveelheid cloudopslag die wordt gebruikt. Deze gegevens worden ontdubbeld en gecomprimeerd. Dit bedrag bevat cloudmomentopnamen die mogelijk gegevens bevatten die niet wordt weergegeven in de primaire volumes en bijgehouden voor verouderde of vereist bewaren doeleinden. U kunt vergelijken Hallo primaire cloud-opslag-verbruik cijfers tooget een idee van vermindering van Hallo gegevens classificeren, maar Hallo nummer is niet exact. Hallo weergegeven volgende grafieken Hallo cloud verbruik van de opslagcapaciteit van een StorSimple-apparaat voordat en nadat een cloudmomentopname is gemaakt. Hallo cloudmomentopname gestart op ongeveer 14:00 uur op het apparaat en ziet u Hallo cloud capaciteit gebruik maken van op Hallo dezelfde tijd van 5.73 MB too4.04 GB verhogen.

![Gebruik van cloud-capaciteit voordat cloudmomentopname](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Gebruik van capaciteit cloud nadat de cloudmomentopname](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Verbruik van de opslagcapaciteit apparaat
Deze grafieken weergegeven Hallo totale gebruik voor Hallo-apparaat, wordt er meer dan gebruik van de primaire opslag omdat het lineaire SSD-laag Hallo omvat. Deze laag bevat een hoeveelheid gegevens die ook op Hallo andere lagen van het apparaat bestaat. Hallo capaciteit in lineaire Hallo SSD-laag is tijdens het bladeren uitlijnen dat als er nieuwe gegevens binnenkomt, oude gegevens Hallo verplaatste toohello HDD-laag (op dat moment is ontdubbeld en gecomprimeerd) en vervolgens toohello cloud.

Na verloop van tijd gebruik van primaire capaciteit en gebruik van de capaciteit apparaat waarschijnlijk vergroten samen totdat het Hallo-gegevens begint toobe gelaagde toohello cloud. Op dat moment gebruik van de capaciteit Hallo apparaat waarschijnlijk tooplateau begint, maar het gebruik van de primaire capaciteit Hallo naarmate er meer gegevens worden geschreven.

Hallo weergegeven volgende grafieken Hallo primaire verbruik van de opslagcapaciteit van een StorSimple-apparaat voordat en nadat een cloudmomentopname is gemaakt. Hallo cloudmomentopname begonnen op 14:00 uur en gebruik van de capaciteit Hallo apparaat op dat moment verlagen. Hallo apparaat opslaggebruik capaciteit is gegaan omlaag van 11.58 GB too7.48 GB. Dit geeft aan dat waarschijnlijk hello niet-gecomprimeerde gegevens in Hallo lineaire SSD-laag is ontdubbeld, gecomprimeerd en naar het Hallo HDD-laag verplaatst. Houd er rekening mee dat als Hallo apparaat al een grote hoeveelheid gegevens in zowel Hallo SSD en HDD-opslaglagen heeft, u geen deze daling ziet mogelijk. In dit voorbeeld heeft Hallo-apparaat een kleine hoeveelheid gegevens.

![Gebruik van capaciteit apparaat voordat cloudmomentopname](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Gebruik van capaciteit apparaat na cloudmomentopname](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Netwerkdoorvoer
**Netwerkdoorvoer** houdt metrische gegevens gerelateerde toohello hoeveelheid gegevens overgedragen van Hallo iSCSI-initiator netwerkinterfaces op de hostserver Hallo en Hallo-apparaat en tussen Hallo-apparaat en Hallo cloud. U kunt met deze metriek voor elk van de iSCSI-netwerkinterfaces Hallo bewaken op uw apparaat.

Hallo grafieken weergeven Hallo netwerkdoorvoer voor Hallo Data 0 en 4, gegevens, zowel 1 GbE-netwerkinterfaces op uw apparaat te volgen. In dit exemplaar is Data 0 ingeschakeld voor de cloud terwijl Data 4 iSCSI-functionaliteit. U kunt beide Hallo inkomend en uitgaand verkeer voor uw StorSimple-apparaat Hallo zien. Hallo platte lijn in Hallo grafiek vanaf 3:24 uur is ten gevolge van toohello feit we verzamelen van gegevens alleen om de 5 minuten en dient te worden genegeerd. 

![Netwerkdoorvoer voor Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Netwerkdoorvoer voor Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Prestaties van een apparaat
**Prestaties van een apparaat** houdt metrische gegevens gerelateerd toohello prestaties van uw apparaat. Hallo volgende diagram toont Hallo CPU-gebruik statistieken voor een apparaat in productie.

![CPU-gebruik voor apparaat](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[hello StorSimple Manager service apparaat dashboard gebruiken](storsimple-device-dashboard.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

