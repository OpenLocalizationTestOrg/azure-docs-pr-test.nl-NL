---
title: aaaConfigure Hallo NewTek TriCaster encoder toosend een single-bitrate live stream | Microsoft Docs
description: Dit onderwerp leest hoe tooconfigure hello Tricaster live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Hallo NewTek TriCaster encoder toosend een single-bitrate live stream gebruiken
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Live elemental](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Dit onderwerp wordt beschreven hoe tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live coderingsprogramma toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering. Zie voor meer informatie [werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Deze zelfstudie laat zien hoe toomanage Azure Media Services (AMS) met Azure Media Services Explorer (AMSE)-hulpprogramma. Dit hulpprogramma wordt alleen uitgevoerd op Windows-PC. Als u op Mac- of Linux, gebruikt u Azure portal toocreate hello [kanalen](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) en [programma's](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> Wanneer met Tricaster voor het verzenden van een bijdrage feed tooAMS kanalen die zijn ingeschakeld voor live codering, kunnen er video en audio haperingen in uw live gebeurtenis als u bepaalde functies van Tricaster, zoals snelle knippen tussen feeds of overschakelen van Smartphones gebruiken . Hallo AMS-team werkt op deze problemen tot die tijd is hersteld, is niet raadzaam toouse deze functies.
>
>

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

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Geef een kanaalnaam Hallo beschrijvingsveld is optioneel. Selecteer onder instellingen voor kanaal **standaard** voor Hallo optie Live Encoding, hello invoer Protocol ingesteld te**RTMP**. U kunt alle andere instellingen zoals is laten.

    Zorg ervoor dat Hallo **Start Hallo nieuw kanaal nu** is geselecteerd.

3. Klik op **kanaal maken**.

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> Hallo kanaal kan 20 minuten toostart zo lang duren.
>
>

Tijdens het Hallo-kanaal wordt gestart. u kunt [Hallo-codering configureren](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Houd er rekening mee dat omdat facturering begint zodra kanaal probeert het gereed. Zie voor meer informatie [van kanaal statussen](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Hallo NewTek TriCaster-codering configureren
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
1. Maak een nieuwe **NewTek TriCaster** project, afhankelijk van welke video-invoerbron wordt gebruikt.
2. Eenmaal in dat project Hallo zoeken **stroom** en klik op Hallo tandwielpictogram pictogram volgende tooit tooaccess Hallo configuratie menu stream.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Zodra het Hallo-menu heeft geopend, klikt u op **nieuw** onder Hallo verbinding kop. Als u wordt gevraagd voor het verbindingstype hello, selecteer **Adobe Flash**.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. Klik op **OK**.
5. Een profiel FMLE kan nu worden geïmporteerd door te klikken op Hallo vervolgkeuzepijl onder **Streaming profiel** en te navigeren**Bladeren**.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Navigeer toowhere Hallo geconfigureerd FMLE profiel is opgeslagen.
7. Selecteer deze en druk op **OK**.

    Zodra het Hallo-profiel is geüpload, gaat u verder toohello volgende stap.
8. Hallo-kanaal invoer-URL ophalen in volgorde tooassign het toohello Tricaster **RTMP eindpunt**.

    Navigeer terug toohello AMSE-hulpprogramma, en controleren op Hallo kanaal voltooiingsstatus weer. Zodra het Hallo-status is gewijzigd van **starten** te**met**, krijgt u Hallo invoer-URL.

    Wanneer Hallo kanaal wordt uitgevoerd, klik met de rechtermuisknop op Hallo kanaalnaam, omlaag toohover gaan via **invoer-URL kopiëren tooclipboard** en selecteer vervolgens **primaire invoer-URL**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Deze informatie plakken in Hallo **locatie** veld onder **Flash Server** binnen Hallo Tricaster-project. Ook de Stroomnaam van een in Hallo toewijzen **stroom-ID** veld.

    Als stream informatie is toegevoegd toohello FMLE profiel, het kan ook worden geïmporteerd toothis sectie door te klikken op **importinstellingen**, toohello opgeslagen FMLE profiel navigeren en op **OK**. Hallo relevante Flash Server velden moeten gevuld met Hallo gegevens van FMLE.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. Wanneer u klaar bent, klikt u op **OK** Hallo onder welkomstscherm aan. Wanneer de video en audio-ingangen in Hallo Tricaster klaar bent, moet u beginnen tooAMS streaming door te klikken op Hallo **stroom** knop.

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Voordat u op **stroom**, u **moet** ervoor te zorgen dat het Hallo-kanaal klaar is.
> Zorg er ook geen tooleave Hallo kanaal in een status gereed zonder een bijdrage invoer feed langer dan 15 minuten >.
>
>

## <a name="test-playback"></a>Test afspelen
Navigeer toohello AMSE-hulpprogramma en Hallo kanaal toobe getest met de rechtermuisknop op. Hallo menu Beweeg de muisaanwijzer over **afspelen Hallo Preview** en selecteer **met Azure Media Player**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Als Hallo stroom wordt weergegeven in Hallo-speler, heeft Hallo encoder correct geconfigureerde tooconnect tooAMS zijn.

Als een fout wordt ontvangen, moet Hallo kanaal toobe opnieuw instellen en coderingsprogramma instellingen aangepast. Zie Hallo [probleemoplossing](media-services-troubleshooting-live-streaming.md) onderwerp voor hulp.  

## <a name="create-a-program"></a>Een programma maken
1. Nadat het kanaal afspelen is bevestigd, maak een programma. Onder Hallo **Live** tabblad Hallo AMSE-hulpprogramma, klik met de rechtermuisknop in Hallo programma gebied en selecteer **nieuw programma maken**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
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

## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
