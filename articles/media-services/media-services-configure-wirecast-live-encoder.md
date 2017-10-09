---
title: aaaConfigure hello Telestream Wirecast-coderingsprogramma toosend een single-bitrate live stream | Microsoft Docs
description: 'Dit onderwerp leest hoe tooconfigure hello Wirecast live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering. '
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Hallo Wirecast-coderingsprogramma toosend een single-bitrate live stream gebruiken
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Live elemental](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Dit onderwerp wordt beschreven hoe tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.  Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma. Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC. Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Vereisten
* [Een Azure Media Services-account maken](media-services-portal-create-account.md)
* Zorg dat er een Streaming-eindpunt is uitgevoerd. Zie voor meer informatie [Streaming-eindpunten beheren in een Media Services-Account](media-services-portal-manage-streaming-endpoints.md)
* Installeer de meest recente versie Hallo Hallo [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) hulpprogramma.
* Hallo hulpprogramma start en tooyour AMS-account koppelen.

## <a name="tips"></a>Tips
* Gebruik indien mogelijk een internetverbinding ' hardwired '.
* Een goede vuistregel bij het bepalen van de vereiste bandbreedte is toodouble Hallo bitsnelheden streaming. Hoewel dit niet verplicht is, wordt deze verminderen Hallo impact van opstoppingen in het netwerk.
* Wanneer met behulp van software gebaseerd coderingsprogramma's, sluit u alle onnodige programma's.

## <a name="create-a-channel"></a>Een kanaal maken
1. Navigeer in Hallo AMSE-hulpprogramma, toohello **Live** tabblad en klik met de rechtermuisknop in Hallo kanaal gebied. Selecteer **kanaal maken...** Hallo upmenu.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Geef een kanaalnaam Hallo beschrijvingsveld is optioneel. Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTMP**. U kunt alle andere instellingen zoals is laten.

    Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.

3. Klik op **kanaal maken**.

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> Hallo kanaal kan 20 minuten toostart zo lang duren.
>
>

Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed. Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Hallo Telestream Wirecast-coderingsprogramma configureren
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

### <a name="configuration-steps"></a>Configuratiestappen
1. Open Hallo Telestream Wirecast-toepassing op het Hallo-machine wordt gebruikt, en voor het streamen van RTMP ingesteld.
2. Hallo-uitvoer configureren door te navigeren toohello **uitvoer** tabblad en het selecteren van **uitvoerinstellingen...** .

    Zorg ervoor dat Hallo **bestemming voor de uitvoer** te is ingesteld,**RTMP Server**.
3. Klik op **OK**.
4. Ingesteld op de instellingenpagina Hallo Hallo **bestemming** veld toobe **Azure Media Services**.

    Hallo codering profiel is vooraf ingeschakeld te**Azure H.264 720 p 16:9 (1280 x 720)**. toocustomize deze instellingen, selecteer Hallo tandwielpictogram pictogram toohello rechts van Hallo vervolgkeuzelijst en kies vervolgens **nieuwe voorinstelling**.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Standaardinstellingen voor codering configureren.

    Naam Hallo voorinstelling en te controleren op Hallo volgende aanbevolen instellingen:

    **Video**

   * Codering: MainConcept H.264
   * Frames per seconde: 30
   * Gemiddelde bitsnelheid: 5000 kbits per seconde (kan worden aangepast op basis van de beperkingen op het netwerk)
   * Profiel: Main
   * Sleutelframe elke: 60 frames

    **Audio**

   * Doelbitsnelheid: 192 kbits per seconde
   * Samplefrequentie: 44,100 kHz

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Druk op **opslaan**.

    het veld Encoding Hallo is nu Hallo nieuw gemaakt profiel beschikbaar voor selectie.

    Zorg ervoor dat nieuwe Hallo-profiel is geselecteerd.
7. Hallo-kanaal invoer-URL ophalen in volgorde tooassign het toohello Wirecast **RTMP eindpunt**.

    Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer. Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.

    Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. In Hallo Wirecast **uitvoerinstellingen** venster plakt u deze informatie in Hallo **adres** veld sectie Hallo-uitvoer, en wijst u de naam van een gegevensstroom.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Selecteer **OK**.
2. Op de belangrijkste Hallo **Wirecast** scherm, invoerbronnen bevestigen voor video en audio gereed zijn en klik vervolgens op **stroom** in Hallo bovenste linkerkant hoek.

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Voordat u op **stroom**, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.
> Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een bijdrage invoer feed langer dan 15 minuten >.
>
>

## <a name="test-playback"></a>Test afspelen

Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op. Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.

Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast. Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.  

## <a name="create-a-program"></a>Een programma maken
1. Nadat het kanaal afspelen is bevestigd, maak een programma. Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. Hallo-programma een naam en wijzig indien nodig, Hallo **lengte van een archiefvenster** (welke standaardwaarden too4 uur). U kunt ook opgeven van een opslaglocatie of laat als Hallo standaard.  
3. Controleer de Hallo **Start Hallo programma nu** vak.
4. Klik op **programma maken**.  

   >[!NOTE]
   >Maken van het programma kost minder tijd dan het maken van kanaal.
       
5. Zodra het Hallo-programma wordt uitgevoerd, bevestigt u afspelen met de rechtermuisknop te klikken op het Hallo-programma en te navigeren**afspelen Hallo-programma's** en selecteren **met Azure Media Player**.  
6. Zodra bevestigd, klik met de rechtermuisknop Hallo programma opnieuw en selecteer **kopiëren Hallo uitvoer URL tooClipboard** (of deze informatie ophalen van Hallo **programma gegevens en instellingen** optie uit Hallo menu).

Hallo-stroom is nu gereed toobe ingesloten in een speler of gedistribueerde tooan doelgroep voor live weergeven.  

## <a name="troubleshooting"></a>Problemen oplossen
Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
