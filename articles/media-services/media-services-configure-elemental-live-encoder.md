---
title: aaaConfigure Hallo elementair Live coderingsprogramma toosend een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe tooconfigure Hallo elementair Live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Hallo elementair Live coderingsprogramma toosend een single-bitrate live stream gebruiken
> [!div class="op_single_selector"]
> * [Live elemental](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Dit onderwerp wordt beschreven hoe tooconfigure hello [elementair Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.  Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma. Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC. Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Vereisten
* Moet een praktische kennis van het gebruik van elementaire Live web interface toocreate live gebeurtenissen hebben.
* [Een Azure Media Services-account maken](media-services-portal-create-account.md)
* Zorg dat er een Streaming-eindpunt is uitgevoerd. Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md).
* Installeer de meest recente versie Hallo Hallo [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.
* Hallo hulpprogramma start en tooyour AMS-account koppelen.

## <a name="tips"></a>Tips
* Gebruik indien mogelijk een internetverbinding ' hardwired '.
* Een goede vuistregel bij het bepalen van de vereiste bandbreedte is toodouble Hallo bitsnelheden streaming. Hoewel dit niet verplicht is, wordt deze verminderen Hallo impact van opstoppingen in het netwerk.
* Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.

## <a name="elemental-live-with-rtp-ingest"></a>Elementaire Live met RTP opnemen
Deze sectie wordt beschreven hoe tooconfigure Hallo elementair Live coderingsprogramma dat verzendt een single bitrate livestream via RTP.  Zie voor meer informatie [MPEG-TS-stream via RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Een kanaal maken

1. Navigeer in Hallo AMSE-hulpprogramma, toohello **Live** tabblad en klik met de rechtermuisknop in Hallo kanaal gebied. Selecteer **kanaal maken...** Hallo upmenu.

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Geef een kanaalnaam Hallo beschrijvingsveld is optioneel. Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTP (MPEG-TS)**. U kunt alle andere instellingen zoals is laten.

    Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.

3. Klik op **kanaal maken**.

   ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> Hallo kanaal kan 20 minuten toostart zo lang duren.
>
>

Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed. Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Hallo elementair Live coderingsprogramma configureren
In deze zelfstudie Hallo volgende uitvoerinstellingen gebruikt. Hallo rest van deze sectie beschrijft de configuratiestappen in meer detail.

**Video**:

* Codec: H.264
* Profiel: Hoge (niveau 4.0)
* Bitrate: 5000 kbps
* Sleutelframe: 2 seconden (60 seconden)
* Frequentie frame: 30

**Audio**:

* Codec: AAC (LC)
* Bitrate: 192 kbps
* Samplefrequentie: 44,1 kHz

#### <a name="configuration-steps"></a>Configuratiestappen
1. Navigeer toohello **elementair Live** webinterface en stellen Hallo-codering voor **UDP/TS** streaming.
2. Zodra een nieuwe gebeurtenis is gemaakt, schuif naar beneden toohello uitvoer groepen en Hallo toevoegen **UDP/TS** uitvoer groep.
3. De uitvoer van een nieuwe maken door te selecteren **nieuwe Stream** en vervolgens te klikken op **uitvoer toevoegen**.  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > Het verdient aanbeveling dat Hallo elementair gebeurtenis heeft Hallo tijdcode instellen te 'Systeemklok' toohelp Hallo encoder opnieuw verbinding maken in geval van een stroom fout Hallo.
   >
   >
4. Nu hello uitvoer is gemaakt, klikt u op **stroom toevoegen**. Hallo uitvoerinstellingen kunnen nu worden geconfigureerd.
5. Schuif naar beneden toohello 'Stream 1' die is gemaakt, klikt u op Hallo **Video** tabblad op Hallo links en vouw Hallo **Geavanceerd** gedeelte instellingen.

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Terwijl elementair Live een breed scala heeft aan beschikbare aanpassen, worden hello volgende instellingen aanbevolen voor aan de slag met tooAMS streaming.

   * Oplossing: 1280 x 720
   * Framesnelheid: 30
   * GOP grootte: 60 frames
   * Modus interliniëren: progressief
   * Bitrate: 5000000 bits/s (dit kan worden aangepast op basis van de beperkingen op het netwerk)

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Hallo-kanaal invoer-URL ophalen.

    Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer. Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.

    Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Deze informatie plakken in Hallo **primaire doel** veld Hallo Elemental. Alle andere instellingen kunnen Hallo standaard blijven.

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Herhaal deze stappen Hello secundaire invoer-URL voor het maken van een afzonderlijke tabblad 'Uitvoer' voor het UDP/TS Streaming voor extra redundantie.
3. Klik op **maken** (als een nieuwe gebeurtenis is gemaakt) of **Update** (als een bestaande gebeurtenis bewerken) en ga vervolgens verder toostart Hallo encoder.

> [!IMPORTANT]
> Voordat u op **Start** op Hallo elementair Live webinterface, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.
> Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een gebeurtenis voor langer dan 15 minuten >.
>
>

Nadat het Hallo stroom actief is geweest gedurende 30 seconden, gaat u terug toohello AMSE hulpprogramma's en test afspelen.  

### <a name="test-playback"></a>Test afspelen

Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op. Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.

Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast. Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.   

### <a name="create-a-program"></a>Een programma maken
1. Nadat het kanaal afspelen is bevestigd, maak een programma. Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.  

    ![Elementaire](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Hallo-programma een naam en wijzig indien nodig, Hallo **lengte van een archiefvenster** (welke standaardwaarden too4 uur). U kunt ook opgeven van een opslaglocatie of laat als Hallo standaard.  
3. Controleer de Hallo **Start Hallo programma nu** vak.
4. Klik op **programma maken**.  

    >[!NOTE]
    > Maken van het programma kost minder tijd dan het maken van kanaal.   
      
5. Zodra het Hallo-programma wordt uitgevoerd, bevestigt u afspelen met de rechtermuisknop te klikken op het Hallo-programma en te navigeren**afspelen Hallo-programma's** en selecteren **met Azure Media Player**.  
6. Zodra bevestigd, klik met de rechtermuisknop Hallo programma opnieuw en selecteer **kopiëren Hallo uitvoer URL tooClipboard** (of deze informatie ophalen van Hallo **programma gegevens en instellingen** optie uit Hallo menu).

Hallo-stroom is nu gereed toobe ingesloten in een speler of gedistribueerde tooan doelgroep voor live weergeven.  

## <a name="troubleshooting"></a>Problemen oplossen
Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
