---
title: aaaLive stream met lokale coderingsprogramma's met behulp van hello Azure-portal | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het maken van een kanaal dat is geconfigureerd voor een doorvoerlevering.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Hoe live streamen van tooperform met lokale coderingsprogramma's via hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Deze zelfstudie leert u Hallo van het gebruik van Azure portal toocreate Hallo een **kanaal** die is geconfigureerd voor een doorvoerlevering. 

## <a name="prerequisites"></a>Vereisten
Hallo volgen vereist toocomplete Hallo-zelfstudie:

* Een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
* Een Media Services-account. een Media Services-account toocreate Zie [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).
* Een webcam. Bijvoorbeeld [Telestream Wirecast-coderingsprogramma](http://www.telestream.net/wirecast/overview.htm).

Het is raadzaam tooreview Hallo artikelen te volgen:

* [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Overzicht van live streamen met Azure Media Services](media-services-manage-channels-overview.md)
* [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Algemeen scenario voor live streamen
Hallo beschrijven volgende stappen taken voor het maken van algemene toepassingen voor live streamen die kanalen gebruiken die zijn geconfigureerd voor doorvoerlevering. Deze zelfstudie laat zien hoe toocreate een doorvoerkanaal en live gebeurtenissen en beheren.

>[!NOTE]
>Zorg ervoor dat Hallo streaming-eindpunt van waaruit u wilt dat toostream inhoud wordt Hallo **met** status. 
    
1. Sluit een videocamera tooa-computer. Start en configureer een on-premises live coderingsprogramma waarmee een multi-bitrate RTMP- of Fragmented MP4-stream wordt uitgevoerd. Zie [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824) voor meer informatie.
   
    Deze stap kan ook worden uitgevoerd nadat u uw kanaal hebt gemaakt.
2. Maak en start een doorvoerkanaal.
3. URL voor opnemen ophalen Hallo kanaal. 
   
    Hallo URL voor opnemen wordt gebruikt door Hallo live coderingsprogramma toosend Hallo stroom toohello kanaal.
4. Hallo kanaal preview URL niet ophalen. 
   
    Gebruik deze URL tooverify dat Hallo livestream goed door het kanaal wordt ontvangen.
5. Maak een live gebeurtenis/programma. 
   
    Wanneer met behulp van hello Azure-portal, het maken van een live gebeurtenis ook een asset gemaakt. 

6. Start Hallo gebeurtenis/het programma wanneer u bent klaar toostart streamen en te archiveren.
7. Hallo live coderingsprogramma kan desgewenst gesignaleerde toostart een advertentie zijn. Hallo advertentie wordt ingevoegd in de uitvoerstroom Hallo.
8. Stop Hallo gebeurtenis/het programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren.
9. Verwijder Hallo gebeurtenis/het programma (en verwijder desgewenst Hallo asset).     

> [!IMPORTANT]
> Raadpleeg [Live streamen met on-premises-coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) toolearn over de concepten en overwegingen gerelateerde toolive streamen met on-premises coderingsprogramma's en doorvoerkanalen.
> 
> 

## <a name="tooview-notifications-and-errors"></a>tooview meldingen en fouten
Als u wilt dat tooview meldingen en fouten die wordt geproduceerd door hello Azure-portal, klik op het pictogram in systeemvak Hallo.

![Meldingen](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Doorvoerkanalen en gebeurtenissen maken en starten
Een kanaal is gekoppeld aan gebeurtenissen/programma's waarmee u toocontrol Hallo publiceren en opslaan van segmenten in een live stream. Kanalen beheren gebeurtenissen. 

Kunt u het aantal uren waarop u tooretain Hallo opgenomen inhoud voor Hallo programma door de instelling Hallo Hallo **archiefvenster** lengte. Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur. Lengte van een archiefvenster bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo. Gebeurtenissen in de opgegeven tijdsduur Hallo kunnen uitvoeren, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd. De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.

Elke gebeurtenis is gekoppeld aan een asset. toopublish hello gebeurtenis, moet u een OnDemand-locator voor Hallo gekoppeld asset maken. Met deze locator kunt u een streaming-URL die u kunt tooyour clients leveren toobuild.

Een kanaal biedt ondersteuning voor maximaal toothree gebeurtenissen gelijktijdig uitvoeren zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream. Hiermee kunt u toopublish en te archiveren verschillende onderdelen van een gebeurtenis naar behoefte. De vereiste van uw bedrijf is bijvoorbeeld tooarchive zes uur van een programma, maar toobroadcast alleen de laatste tien minuten. tooaccomplish, moet u twee gelijktijdig actieve programma's toocreate. Een programma wordt ingesteld tooarchive zes uur van de gebeurtenis Hallo maar Hallo programma wordt niet gepubliceerd. Hallo andere programma is set tooarchive voor 10 minuten en dit programma is gepubliceerd.

Gebruik de bestaande live gebeurtenissen niet opnieuw. In plaats daarvan maakt en start u een nieuwe gebeurtenis voor elke gebeurtenis.

Start Hallo gebeurtenis wanneer u bent klaar toostart streamen en te archiveren. Stop Hallo programma als u wilt dat toostop streaming en Hallo-gebeurtenis wilt archiveren. 

toodelete gearchiveerde inhoud, stoppen en Hallo gebeurtenis verwijderen en verwijder vervolgens de gekoppelde asset Hallo. Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis; Hallo-gebeurtenis moet eerst worden verwijderd. 

Zelfs na het stoppen en verwijderen van de gebeurtenis Hallo Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd.

Als u tooretain Hallo gearchiveerde inhoud wilt, maar niet langer voor streaming beschikbaar, verwijdert u Hallo streaming-locator.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello portal toocreate een kanaal
Deze sectie wordt beschreven hoe toouse hello **snelle invoer** optie toocreate een doorvoerkanaal.

Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over doorvoerkanalen.

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. In Hallo **instellingen** venster, klikt u op **Live streamen**. 
   
    ![Aan de slag](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Hallo **Live streamen** venster wordt weergegeven.
3. Klik op **snelle invoer** toocreate een doorvoerkanaal Hello RTMP-opnameprotocol.
   
    Hallo **een nieuw kanaal maken** venster wordt weergegeven.
4. Hallo nieuw kanaal een naam geven en klik op **maken**. 
   
    Hiermee maakt u een doorvoerkanaal Hello RTMP-opnameprotocol.

## <a name="create-events"></a>Gebeurtenissen maken
1. Selecteer een kanaal toowhich gewenste tooadd een gebeurtenis.
2. Klik op de knop **Live gebeurtenis**.

![Gebeurtenis](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>URL’s voor opnemen ophalen
Wanneer het Hallo-kanaal is gemaakt, kunt u URL's die u toohello live codering voor opnemen. Hallo coderingsprogramma gebruikt deze URL's tooinput een live stream.

![Gemaakt](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Hallo controlegebeurtenis
toowatch hello gebeurtenis, klikt u op **controle** in hello Azure portal of een kopie van Hallo streaming-URL en gebruikt u een speler van uw keuze. 

![Gemaakt](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Live gebeurtenis ophalen automatisch inhoud geconverteerde tooon aanvraag wanneer gestopt.

## <a name="clean-up"></a>Opruimen
Zie [Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken](media-services-live-streaming-with-onprem-encoders.md) voor meer informatie over doorvoerkanalen.

* Een kanaal kan worden gestopt, alleen wanneer alle gebeurtenissen/programma's op Hallo kanaal zijn gestopt.  Zodra het Hallo-kanaal is gestopt, wordt deze niet worden geen kosten berekend. Wanneer u toostart moet deze opnieuw, is er hello dezelfde URL voor opnemen zodat u geen tooreconfigure het coderingsprogramma hoeft.
* Een kanaal kan alleen worden verwijderd als alle live gebeurtenissen op Hallo kanaal zijn verwijderd.

## <a name="view-archived-content"></a>Gearchiveerde inhoud weergeven
Zelfs na het stoppen en verwijderen van de gebeurtenis Hallo Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd. Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis; Hallo-gebeurtenis moet eerst worden verwijderd. 

uw assets selecteert u toomanage **instelling** en klik op **activa**.

![Assets](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

