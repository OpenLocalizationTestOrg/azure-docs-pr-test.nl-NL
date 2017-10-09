---
title: aaaHow tooperform live streamen met Azure Media Services toocreate multi-bitrate streams Hello Azure-portal | Microsoft Docs
description: Deze zelfstudie helpt u bij het Hallo-stappen voor het maken van een kanaal dat een single-bitrate livestream ontvangt en coderen van deze toomulti-bitrate stream met hello Azure-portal.
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Hoe tooperform live streamen met Azure Media Services toocreate multi-bitrate streams Hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Deze zelfstudie leert u Hallo van het maken van een **kanaal** dat een single-bitrate livestream ontvangt, en coderen van deze toomulti-bitrate stream.

> [!NOTE]
> Zie voor meer conceptuele informatie gerelateerde tooChannels die zijn ingeschakeld voor live codering [Live streamen met Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Algemeen scenario voor live streamen
Hallo hieronder vindt u algemene stappen voor het maken van algemene toepassingen voor live streamen.

> [!NOTE]
> Hallo maximum is aanbevolen duur van een live gebeurtenis op dit moment acht uur. Neem contact op met amslived op Microsoft.com als u toorun een kanaal voor langere tijd nodig.
> 
> 

1. Sluit een videocamera tooa-computer. Start en configureer een on-premises live coderingsprogramma dat een single-bitrate stream in een van de volgende protocollen Hallo kunt uitvoeren: RTMP, Smooth Streaming of RTP (MPEG-TS). Zie [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824) voor meer informatie.
   
    Deze stap kan ook worden uitgevoerd nadat u uw kanaal hebt gemaakt.
2. Maak en start een kanaal. 
3. URL voor opnemen ophalen Hallo kanaal. 
   
    Hallo URL voor opnemen wordt gebruikt door Hallo live coderingsprogramma toosend Hallo stroom toohello kanaal.
4. Hallo kanaal preview URL niet ophalen. 
   
    Gebruik deze URL tooverify dat Hallo livestream goed door het kanaal wordt ontvangen.
5. Maak een gebeurtenis/programma (hierbij wordt ook een asset gemaakt). 
6. Hallo-gebeurtenis (die wordt gemaakt een OnDemand-locator voor de gekoppelde asset Hallo) publiceren.    
7. Start Hallo gebeurtenis wanneer u bent klaar toostart streamen en te archiveren.
8. Hallo live coderingsprogramma kan desgewenst gesignaleerde toostart een advertentie zijn. Hallo advertentie wordt ingevoegd in de uitvoerstroom Hallo.
9. Stop Hallo gebeurtenis gewenst toostop streaming en Hallo-gebeurtenis wilt archiveren.
10. Hallo gebeurtenis verwijderen (en verwijder desgewenst Hallo asset).   

## <a name="in-this-tutorial"></a>In deze zelfstudie
In deze zelfstudie is hello Azure-portal gebruikte tooaccomplish Hallo taken te volgen: 

1. Maken van een kanaal dat ingeschakelde tooperform live codering.
2. Get Hallo URL voor opnemen in de volgorde toosupply het toolive encoder. Hallo live coderingsprogramma gebruikt deze URL tooingest Hallo stroom in Hallo kanaal.
3. Een gebeurtenis/programma (en een asset) maken.
4. Hallo asset publiceren en streaming-URL's ophalen.  
5. Uw inhoud afspelen.
6. Opschonen.

## <a name="prerequisites"></a>Vereisten
Hallo volgen vereist toocomplete Hallo zelfstudie.

* toocomplete in deze zelfstudie, moet u een Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. 
  Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
* Een Media Services-account. een Media Services-account toocreate Zie [-Account maken](media-services-portal-create-account.md).
* Een webcam en een coderingsprogramma dat een single bitrate livestream kan verzenden.

## <a name="create-a-channel"></a>Een kanaal maken
1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u Media Services en klik vervolgens op de naam van uw Media Services-account.
2. Selecteer **Live streamen**.
3. Selecteer **Aangepast maken**. Met deze optie kunt u een kanaal maken dat is ingeschakeld voor real-time codering.
   
    ![Een kanaal maken](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Klik op **Instellingen**.
   
   1. Kies Hallo **Live Encoding** kanaaltype. Dit type geeft aan dat u toocreate een kanaal dat is ingeschakeld voor live codering. Dat betekent Hallo binnenkomende single-bitrate stream toohello kanaal verzonden en gecodeerd naar een multi-bitrate stream met de instellingen van de opgegeven live codering. Zie voor meer informatie [Live streamen met Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md). Klik op OK.
   2. Geef een naam op voor het kanaal.
   3. Klik op OK Hallo onder welkomstscherm aan.
5. Selecteer Hallo **opnemen** tabblad.
   
   1. Op deze pagina kunt u een streaming-protocol selecteren. Voor Hallo **Live Encoding** kanaaltype, geldig protocolopties zijn:
      
      * Single-bitrate Fragmented MP4 (Smooth Streaming);
      * Single-bitrate RTMP;
      * RTP (MPEG-TS): MPEG-2-transportstroom via RTP.
        
        Zie voor gedetailleerde uitleg over elk protocol [Live streamen met Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).
        
        U Hallo protocoloptie tijdens het Hallo kanaal niet wijzigen of de bijbehorende gebeurtenissen/programma's worden uitgevoerd. Als u verschillende protocollen nodig hebt, maakt u afzonderlijke kanalen voor elk streaming-protocol.  
   2. U kunt IP-beperkingen toepassen op Hallo opnemen. 
      
       U kunt definiëren Hallo IP-adressen die zijn toegestaan tooingest een video toothis-kanaal. Toegestane IP-adressen kunnen worden opgegeven als een enkel IP-adres (bijvoorbeeld 10.0.0.1), een IP-adresbereik met een IP-adres en een CIDR-subnetmasker (bijvoorbeeld 10.0.0.1/22) of een IP-adresbereik met een IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld '10.0.0.1(255.255.252.0)').
      
       Als geen IP-adressen zijn opgegeven en er geen regeldefinitie bestaat, zijn er geen IP-adressen toegestaan. tooallow elk IP-adres, maakt u een regel en stelt u 0.0.0.0/0.
6. Op Hallo **Preview** tabblad, IP-beperking is van toepassing op Hallo preview.
7. Op Hallo **codering** tabblad, Hallo codering voorinstelling opgeven. 
   
    Op dit moment Hallo alleen systeem kunt u Systeemwaarde **Default 720p**. toospecify een aangepaste voorinstelling, opent u een ondersteuningsticket van Microsoft. Voer vervolgens de naam Hallo Hallo voorinstelling voor u gemaakt. 

> [!NOTE]
> Hallo kanaal wordt gestart kan op dit moment too30 minuten duren. Opnieuw instellen van kanaal kan too5 minuten duren.
> 
> 

Als u Hallo kanaal hebt gemaakt, kunt u Hallo-kanaal op en selecteer **instellingen** waar u de configuraties van de kanalen kunt bekijken. 

Zie voor meer informatie [Live streamen met Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>URL’s voor opnemen ophalen
Wanneer het Hallo-kanaal is gemaakt, kunt u URL's die u toohello live codering voor opnemen. Hallo coderingsprogramma gebruikt deze URL's tooinput een live stream.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Gebeurtenissen maken en beheren
### <a name="overview"></a>Overzicht
Een kanaal is gekoppeld aan gebeurtenissen/programma's waarmee u toocontrol Hallo publiceren en opslaan van segmenten in een live stream. Kanalen beheren gebeurtenissen/programma’s. Hallo is kanaal- en programma-relatie heel vergelijkbaar tootraditional media waarbij een kanaal een constante stream met inhoud heeft en een programma bereik toosome getimede gebeurtenis op dat kanaal.

U kunt opgeven dat Hallo aantal uren dat u wilt dat tooretain Hallo opgenomen inhoud voor Hallo gebeurtenis door Hallo instellen **archiefvenster** lengte. Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur. Lengte van een archiefvenster bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo. Gebeurtenissen in de opgegeven tijdsduur Hallo kunnen uitvoeren, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd. De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.

Elke gebeurtenis is gekoppeld aan een asset. toopublish hello gebeurtenis moet u een OnDemand-locator voor Hallo gekoppelde asset. Met deze locator kunt u een streaming-URL die u kunt tooyour clients leveren toobuild.

Een kanaal biedt ondersteuning voor maximaal toothree gebeurtenissen gelijktijdig uitvoeren zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream. Hiermee kunt u toopublish en te archiveren verschillende onderdelen van een gebeurtenis naar behoefte. De vereiste van uw bedrijf is bijvoorbeeld tooarchive zes uur van een gebeurtenis, maar toobroadcast alleen de laatste tien minuten. tooaccomplish, moet u toocreate twee gelijktijdig uitgevoerd gebeurtenis. Een gebeurtenis is ingesteld tooarchive zes uur van de gebeurtenis Hallo maar Hallo programma wordt niet gepubliceerd. Hallo andere gebeurtenis is set tooarchive voor 10 minuten en dit programma is gepubliceerd.

Gebruik bestaande programma's niet voor nieuwe gebeurtenissen. In plaats daarvan maakt en start u een nieuw programma voor elke gebeurtenis.

Start een gebeurtenis/het programma wanneer u bent klaar toostart streamen en te archiveren. Stop Hallo gebeurtenis gewenst toostop streaming en Hallo-gebeurtenis wilt archiveren. 

toodelete gearchiveerde inhoud, stoppen en Hallo gebeurtenis verwijderen en verwijder vervolgens de gekoppelde asset Hallo. Een asset kan niet worden verwijderd als deze wordt gebruikt door de gebeurtenis Hallo; Hallo-gebeurtenis moet eerst worden verwijderd. 

Zelfs na het stoppen en verwijderen van de gebeurtenis Hallo Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd.

Als u tooretain Hallo gearchiveerde inhoud wilt, maar niet langer voor streaming beschikbaar, verwijdert u Hallo streaming-locator.

### <a name="createstartstop-events"></a>Gebeurtenissen maken/starten/stoppen
Zodra u Hallo stroom hebt kunt Hallo kanaal binnenkomt u beginnen Hallo gebeurtenis streaming door een Asset, programma en Streaming-Locator te maken. Dit wordt Hallo stream gearchiveerd en beschikbaar tooviewers via Hallo Streaming-eindpunt. 

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

Er zijn twee manieren toostart gebeurtenis: 

1. Van Hallo **kanaal** pagina, drukt u op **Live gebeurtenis** tooadd een nieuwe gebeurtenis.
   
    Geef het volgende op: gebeurtenisnaam, assetnaam, archiefvenster en versleutelingsoptie.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Als u **deze live gebeurtenis nu publiceren** dit selectievakje inschakelt, Hallo gebeurtenis Hallo publicatie-URL's gemaakt.
   
    U kunt ook op **Start**, wanneer u klaar toostream Hallo gebeurtenis bent.
   
    Wanneer u begint met Hallo gebeurtenis, kunt u ook op **controle** toostart Hallo inhoud afspelen.
2. U kunt ook kunt u een snelkoppeling en druk op **Go Live** knop op Hallo **kanaal** pagina. Hiermee wordt een standaardasset, -programma en -streaming-locator gemaakt.
   
    Hallo gebeurtenis heet **standaard** en Hallo archiefvenster is ingesteld too8 uur.

U kunt bekijken Hallo gepubliceerde gebeurtenisgegevens van Hallo **Live gebeurtenis** pagina. 

Als u op **Uit lucht** klikt, worden alle live evenementen gestopt. 

## <a name="watch-hello-event"></a>Hallo controlegebeurtenis
toowatch hello gebeurtenis, klikt u op **controle** in hello Azure portal of een kopie van Hallo streaming-URL en gebruikt u een speler van uw keuze. 

![Gemaakt](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Live gebeurtenis converteert automatisch gebeurtenissen tooon aanvraag inhoud wanneer deze is gestopt.

## <a name="clean-up"></a>Opruimen
Als u klaar bent met het streamen van gebeurtenissen en tooclean Hallo-resources die eerder zijn ingericht, volgt u de Hallo procedure te volgen.

* Stop het pushen van Hallo stroom van Hallo coderingsprogramma.
* Hallo-kanaal stoppen. Zodra het Hallo-kanaal is gestopt, worden hiervoor kosten. Wanneer u toostart moet deze opnieuw, is er hello dezelfde URL voor opnemen zodat u geen tooreconfigure het coderingsprogramma hoeft.
* U kunt uw Streaming-eindpunt stoppen, tenzij u toocontinue tooprovide Hallo archief van uw live gebeurtenis als een stream op aanvraag wilt. Als het Hallo-kanaal is gestopt, worden hiervoor kosten.

## <a name="view-archived-content"></a>Gearchiveerde inhoud weergeven
Zelfs na het stoppen en verwijderen van de gebeurtenis Hallo Hallo gebruikers kunnen toostream uw gearchiveerde inhoud als video op aanvraag voor niet zolang u Hallo asset niet hebt verwijderd. Een asset kan niet worden verwijderd als deze wordt gebruikt door een gebeurtenis; Hallo-gebeurtenis moet eerst worden verwijderd. 

uw assets selecteert u toomanage **instelling** en klik op **activa**.

![Assets](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Overwegingen
* Hallo maximum is aanbevolen duur van een live gebeurtenis op dit moment acht uur. Neem contact op met amslived op Microsoft.com als u toorun een kanaal voor langere tijd nodig.
* Zorg ervoor dat Hallo streaming-eindpunt van waaruit u wilt dat toostream uw inhoud wordt Hallo **met** status.

## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

