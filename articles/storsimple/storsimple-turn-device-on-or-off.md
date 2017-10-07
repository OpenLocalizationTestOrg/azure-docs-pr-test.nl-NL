---
title: aaaTurn uw StorSimple 8000 series apparaat in- of uitschakelen | Microsoft Docs
description: Legt uit hoe tooturn op een nieuwe StorSimple-apparaat inschakelen op een apparaat dat is afgesloten of stroomvoorziening en een actieve apparaat uitschakelen.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Op of het apparaat van de serie StorSimple 8000 uitschakelen
## <a name="overview"></a>Overzicht
Afsluiten van een Microsoft Azure StorSimple-apparaat is niet vereist als onderdeel van de werking van het normale systeem. U moet echter tooturn van een nieuw apparaat of een apparaat waarop toobe afgesloten. In het algemeen is afsluiten vereist in gevallen waarin u moet mislukte hardware vervangen, fysiek verplaatsen een eenheid of een apparaat buiten dienst te nemen. Deze zelfstudie wordt beschreven Hallo vereist voor het in- en afsluiten van het StorSimple-apparaat in verschillende scenario's.

## <a name="turn-on-a-new-device"></a>Een nieuw apparaat inschakelen
Hallo zijn stappen voor het inschakelen van een StorSimple-apparaat voor Hallo eerst afhankelijk van of Hallo-apparaat een 8100 is of een 8600-model. Hallo 8100 heeft één primaire behuizing, terwijl Hallo 8600 een dubbele behuizing-apparaat met een primaire-behuizing en een EBOD behuizing is. Hallo worden gedetailleerde stappen voor beide modellen behandeld in Hallo uit te voeren.

* [Nieuw apparaat met alleen primaire behuizing](#new-device-with-primary-enclosure-only)
* [Nieuw apparaat met EBOD behuizing](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Nieuw apparaat met alleen primaire behuizing
Hallo StorSimple 8100-model is een apparaat één behuizing. Uw apparaat bevat redundante stroom en koeling Modules (PCMs). Zowel PCMs moet worden geïnstalleerd en verbonden toodifferent power bronnen tooensure hoge beschikbaarheid.

Volgende stappen toocable Hallo uw apparaat voor power uitvoeren.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Ga te voor apparaat voltooien en instructies bekabeling,[uw StorSimple 8100-apparaat installeert](storsimple-8100-hardware-installation.md). Zorg ervoor dat u instructies Hallo exact.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Nieuw apparaat met EBOD behuizing
Hallo StorSimple 8600 model heeft zowel een primaire-behuizing en een EBOD behuizing. U moet hiervoor Hallo eenheden toobe bekabeld samen voor seriële gekoppelde SCSI (SAS)-verbinding en geen stroom.

Bij het instellen van dit apparaat voor Hallo eerst, Voer u Hallo stappen voor SAS eerst bekabeling en vervolgens voltooit Hallo stappen voor het power bekabeling.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Ga te voor apparaat voltooien en instructies bekabeling,[uw StorSimple 8600-apparaat installeert](storsimple-8600-hardware-installation.md). Zorg ervoor dat u instructies Hallo exact.

## <a name="turn-on-a-device-after-shutdown"></a>Een apparaat inschakelen na afsluiten
Hallo-stappen voor het inschakelen van een StorSimple-apparaat nadat deze is afgesloten zijn verschillend afhankelijk van of Hallo-apparaat een 8100 is of een 8600-model. Hallo 8100 heeft één primaire behuizing, terwijl Hallo 8600 een dubbele behuizing-apparaat met een primaire-behuizing en een EBOD behuizing is.

* [Apparaten met alleen primaire behuizing](#device-with-primary-enclosure-only)
* [Apparaat met EBOD behuizing](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Apparaten met alleen primaire behuizing
Gebruik na een afsluiten Hallo tooturn procedure volgen op een StorSimple-apparaat met een primaire-behuizing en geen EBOD behuizing.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn op een apparaat met een primaire behuizing alleen
1. Zorg ervoor dat Hallo power switches op beide stroom en koeling Modules (PCMs) op Hallo OFF positie zijn. Als Hallo switches zich niet in Hallo OFF positie, spiegelt ze toohello OFF positie en wacht Hallo lichten toogo uitschakelen.
2. Hallo apparaat inschakelen door spiegelen Hallo power switches op beide PCMs toohello op positie. Hallo-apparaat moet inschakelen.
3. Selectievakje Hallo na tooverify die Hallo apparaat is volledig ingeschakeld:
   
   1. Hallo OK LED's op beide PCM-modules zijn groen.
   2. Hallo status LED's op beide domeincontrollers zijn groen.
   3. Hallo die blauw LED op een van de domeincontrollers Hallo knippert, waarmee wordt aangegeven dat Hallo domeincontroller actief is.
      
      Uw apparaat is niet in orde als een van deze voorwaarden niet wordt voldaan. Neem [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Apparaat met EBOD behuizing
Gebruik na een afsluiten Hallo tooturn procedure volgen op een StorSimple-apparaat met een primaire-behuizing en een EBOD behuizing. Elke stap precies zoals beschreven in volgorde uitvoert. Fout toodo kan dus leiden tot verlies van gegevens.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn op een apparaat met een primaire en een behuizing EBOD
1. Zorg ervoor dat Hallo EBOD behuizing is verbonden toohello primaire behuizing. Zie voor meer informatie [uw StorSimple 8600-apparaat installeert](storsimple-8600-hardware-installation.md).
2. Zorg ervoor dat Hallo stroom en koeling Modules (PCMs) op zowel Hallo EBOD en primaire behuizingen in Hallo OFF positie. Als Hallo switches zich niet in Hallo OFF positie, spiegelt ze toohello OFF positie en wacht Hallo lichten toogo uitschakelen.
3. Hallo EBOD behuizing eerst inschakelen door spiegelen Hallo power switches op beide PCMs toohello op positie. Hallo PCM LED's moeten groene. Een groen EBOD controller LED op deze eenheid geeft aan dat Hallo EBOD behuizing op.
4. Schakel primaire behuizing Hallo door spiegelen Hallo power switches op beide PCMs toohello op positie. het hele systeem Hallo worden nu op.
5. Controleer of Hallo SAS LED's zijn groen, waardoor die Hallo-verbinding tussen Hallo EBOD behuizing en Hallo primaire behuizing is goed.

## <a name="turn-on-a-device-after-a-power-loss"></a>Een apparaat na een stroomstoring inschakelen
Een stroomstoring of onderbreking kan een StorSimple-apparaat afsluiten. Hallo stroomstoring kan gebeuren op een van de voedingen Hallo of beide voedingen. Hallo herstelstappen zijn verschillend afhankelijk van of Hallo-apparaat een 8100 is of een 8600-model. Hallo 8100 heeft één primaire behuizing, terwijl Hallo 8600 een dubbele behuizing-apparaat met een primaire-behuizing en een EBOD behuizing is. Deze sectie beschrijft de herstelprocedure Hallo voor elk scenario.

* [Apparaten met alleen primaire behuizing](#8100)
* [Apparaat met EBOD behuizing](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Apparaten met alleen primaire behuizing<a name="8100">
Hallo-systeem kan de normale werking blijven als er power verlies tooone van de stroom wordt voorzien. Echter, hoge beschikbaarheid van Hallo apparaat terugzetten power toohello tooensure voeding zo snel mogelijk.

Als er een stroomstoring of een stroomstoring op beide voedingen, wordt system Hallo zich op een geordende en gecontroleerde manier afgesloten. Hallo-systeem wordt automatisch ingeschakeld wanneer Hallo power wordt hersteld.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Apparaat met EBOD behuizing<a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Stroomstoring op één power supply
Hallo-systeem kan de normale werking blijven als er power verlies tooone van de voedingen op Hallo primaire behuizing of Hallo EBOD behuizing. Echter tooensure hoge beschikbaarheid van Hallo-apparaat, herstel voeding toohello power zo snel mogelijk.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Stroomstoring op beide voedingen op primaire en EBOD behuizingen
Als er een stroomstoring voor onderbreking of power op beide voedingen, Hallo EBOD behuizing wordt onmiddellijk afgesloten en Hallo primaire behuizing op een geordende en gecontroleerde manier wordt afgesloten. Wanneer power wordt hersteld, wordt automatisch Hallo toestel gestart.

Hallo power handmatig wordt uitgeschakeld, los Hallo stappen toorestore power toohello systeem te volgen.

1. Hallo EBOD behuizing inschakelen.
2. Nadat Hallo EBOD behuizing is op, schakel Hallo primaire behuizing.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Stroomstoring op beide voedingen op EBOD behuizing
Bij het instellen van de kabels, moet u ervoor zorgen dat Hallo EBOD nooit is verbonden alleen tooa PDU scheiden. Als Hallo EBOD en primaire behuizing op Hallo uitvallen hetzelfde moment Hallo system wordt hersteld.

Als er slechts Hallo EBOD behuizing op beide voedingen mislukt, Hallo system wordt niet automatisch worden hersteld. Hallo tooturn stappen te volgen op Hallo systeem houden en herstel hem tooa status in orde:

1. Als de primaire behuizing Hallo is ingeschakeld, schakel uit zowel stroom en koeling Modules (PCMs).
2. Wacht een paar minuten voordat Hallo system tooshut omlaag.
3. Hallo EBOD behuizing inschakelen.
4. Nadat Hallo EBOD behuizing is op, schakel Hallo primaire behuizing.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Een apparaat inschakelen na Hallo primaire en EBOD behuizing verbinding wordt verbroken
Als het Hallo-verbinding is verbroken tussen Hallo stand-by-controller en de bijbehorende EBOD-controller hello, blijft Hallo apparaat toowork. Hallo-verbinding tussen Hallo system actieve controller en de bijbehorende EBOD-controller hello wordt verbroken, failover moet worden uitgevoerd als Hallo apparaat toowork als normaal moet blijven.

Wanneer beide kabels seriële gekoppelde SCSI (SAS) zijn verwijderd of Hallo verbinding tussen Hallo EBOD behuizing en Hallo primaire behuizing is verbroken, zal Hallo apparaat niet meer werken. Op dit moment uitvoeren Hallo stappen te volgen.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn op Hallo apparaat nadat de verbinding wordt verbroken
1. Toegang hello achterzijde Hallo-apparaat.
2. Als Hallo SAS-kabelverbinding tussen Hallo EBOD enclosure en Hallo primaire behuizing verbroken is, wordt alle SAS lane LED's op Hallo EBOD behuizing zijn uitgeschakeld.
3. Zowel stroom en koeling Modules (PCMs) afgesloten Hallo EBOD enclosure en Hallo primaire behuizing.
4. Wacht totdat alle Hallo lichten op Hallo achterzijde van beide behuizingen Hallo uitschakelen.
5. Plaats Hallo SAS-kabels en zorg ervoor dat er een goede verbinding tussen Hallo EBOD behuizing en Hallo primaire behuizing.
6. Hallo EBOD behuizing eerst inschakelen door het spiegelen van beide PCM switches toohello op positie.
7. Zorg ervoor dat Hallo EBOD behuizing op door te controleren dat Hallo groen LED is ingesteld op ON.
8. Hallo primaire behuizing inschakelen.
9. Zorg ervoor dat de primaire behuizing hello op door te controleren of Hallo controller groen LED op.
10. Controleer of deze Hallo EBOD behuizing verbinding met de primaire behuizing Hallo goed door te controleren die Hallo SAS lane LED's (vier per EBOD-controller) zijn alle op.

> [!IMPORTANT]
> Als SAS-kabels Hallo defect zijn of Hallo-verbinding tussen Hallo EBOD behuizing en Hallo primaire behuizing niet goed, is wanneer u Hallo system inschakelen, gaat deze in de herstelmodus overgaat. Neem [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) als dit gebeurt.


## <a name="turn-off-a-running-device"></a>Een actief apparaat uitschakelen
Een actieve StorSimple-apparaat moet mogelijk toobe afgesloten als hij wordt verplaatst, buiten de service, of heeft een slecht werkende onderdeel dat toobe vervangen moet. Hallo stappen zijn verschillend, afhankelijk van of Hallo StorSimple-apparaat een 8100 of een 8600-model. Hallo 8100 heeft één primaire behuizing, terwijl Hallo 8600 een dubbele behuizing-apparaat met een primaire-behuizing en een EBOD behuizing is. In deze sectie beschrijft Hallo stappen tooshut een actieve apparaten.

* [Apparaat met primaire behuizing](#8100a)
* [Apparaat met EBOD behuizing](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Apparaat met primaire behuizing<a name="8100a">
tooshut hello apparaten op een geordende en gecontroleerde manier, u kunt dit doen via Hallo klassieke Azure-portal of via Hallo Windows PowerShell voor StorSimple. 

> [!IMPORTANT]
> Niet worden afgesloten een apparaat uitgevoerd met behulp van Hallo / uit-knop op Hallo achterzijde Hallo-apparaat.
> 
> Voordat u afsluit Hallo-apparaat, zorg ervoor dat alle onderdelen van het apparaat Hallo in orde. In klassieke Azure-portal Hallo, te navigeren**apparaten** > **onderhoud** > **hardwarestatus**, en controleer of de status van alle Hallo onderdelen groen is. Dit geldt alleen voor een goede systeem. Als Hallo-systeem wordt afgesloten omlaag tooreplace een onderdeel functioneert niet goed, u ziet een mislukte (rode) of gedegradeerd (geel) status voor de betreffende onderdeel Hallo in Hallo **hardwarestatus**.
> 
> 

Wanneer u Hallo Windows PowerShell voor StorSimple of Hallo klassieke Azure-portal, stappen Hallo in [een StorSimple-apparaat afsluiten](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Apparaat met EBOD behuizing<a name="8600a">
> [!IMPORTANT]
> Voordat u afsluit Hallo primaire enclosure en Hallo EBOD behuizing, zorg ervoor dat alle onderdelen van het apparaat Hallo in orde. In Azure-portal Hallo, te navigeren**apparaten** > **Monitor** > **Hardware health**, en controleer of alle Hallo-onderdelen in orde zijn.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut een actieve apparaten met EBOD behuizing
1. Volg alle Hallo hier vermelde stappen [een StorSimple-apparaat afsluiten](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) voor Hallo primaire behuizing.
2. Na het Hallo wordt primaire behuizing afgesloten, Hallo EBOD afgesloten door spiegelen uit zowel stroom en koeling Module (PCM).
3. tooverify die EBOD Hallo is afgesloten, Controleer of alle licht op Hallo achterzijde Hallo EBOD behuizing zijn uitgeschakeld.

> [!NOTE]
> Hallo SAS-kabels die gebruikt tooconnect hello EBOD behuizing toohello primaire behuizing zijn mogen niet worden verwijderd pas nadat het Hallo-systeem wordt afgesloten.

## <a name="next-steps"></a>Volgende stappen
[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) als u problemen bij het afsluiten een StorSimple-apparaat of inschakelen.

