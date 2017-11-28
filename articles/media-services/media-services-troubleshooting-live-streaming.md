---
title: handleiding voor live streamen aaaTroubleshooting | Microsoft Docs
description: In dit onderwerp biedt informatie over hoe tootroubleshoot live streaming problemen.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="e5aa8-103">Handleiding voor het oplossen van problemen met live streaming</span><span class="sxs-lookup"><span data-stu-id="e5aa8-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="e5aa8-104">Dit onderwerp bevat suggesties voor het tootroubleshoot sommige live streaming-problemen.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="e5aa8-105">Problemen tooon-premises coderingsprogramma 's</span><span class="sxs-lookup"><span data-stu-id="e5aa8-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="e5aa8-106">In deze sectie biedt informatie over hoe tootroubleshoot problemen gerelateerde tooon-premises coderingsprogramma's die zijn geconfigureerd voor toosend een single-bitrate stream tooAMS kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="e5aa8-107">Probleem: Wilt toosee Logboeken</span><span class="sxs-lookup"><span data-stu-id="e5aa8-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="e5aa8-108">**Potentiële probleem**: kan niet zoeken encoder logboeken die kan helpen bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="e5aa8-109">**Telestream Wirecast**: meestal vindt u Logboeken onder C:\Users\{username} \AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="e5aa8-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="e5aa8-110">**Elementaire Live**: vindt u koppelingen toologs heeft op Hallo-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="e5aa8-111">Klik op **statistieken**, klikt u vervolgens **logboeken**.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="e5aa8-112">Op Hallo **logboekbestanden** pagina ziet u een lijst van Logboeken voor alle items LiveEvent Hallo; Selecteer Hallo een die overeenkomt met de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="e5aa8-113">**Flash Live Mediacoderingsprogramma**: U kunt vinden Hallo **logboekmap...**  door te navigeren toohello **codering logboek** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="e5aa8-114">Probleem: Er is geen optie voor het uitvoeren van een progressieve stream</span><span class="sxs-lookup"><span data-stu-id="e5aa8-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="e5aa8-115">**Potentiële probleem**: Hallo codering wordt gebruikt niet automatisch interliniëring ongedaan maken.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="e5aa8-116">**Stappen voor probleemoplossing**: zoek naar een ongedaan ineengestrengeld optie binnen Hallo encoder interface.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="e5aa8-117">Zodra de-interlacing is ingeschakeld, Controleer of opnieuw progressief uitvoerinstellingen.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="e5aa8-118">Probleem: Probeert verschillende instellingen voor codering uitvoer en nog steeds niet tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="e5aa8-119">**Potentiële probleem**: Azure codering kanaal is niet juist opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="e5aa8-120">**Stappen voor probleemoplossing**: Zorg ervoor dat Hallo encoder niet meer tooAMS pusht, stoppen en opnieuw instellen van Hallo-kanaal.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="e5aa8-121">Als opnieuw uit te voeren, probeert u het coderingsprogramma verbinding te maken met de nieuwe instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="e5aa8-122">Als dit nog niet is opgelost probleem hello, maak een nieuw kanaal volledig, soms kanalen beschadigd kunnen raken na een aantal mislukte pogingen.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="e5aa8-123">**Potentiële probleem**: Hallo GOP grootte of Sleutelframe instellingen zijn niet optimaal.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="e5aa8-124">**Stappen voor probleemoplossing**: GOP aanbevolen grootte of keyframe interval is 2 seconden.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="e5aa8-125">Sommige coderingsprogramma's berekenen deze instelling in het aantal frames, terwijl andere seconden.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="e5aa8-126">Bijvoorbeeld: bij het uitvoeren van 30fps Hallo GOP grootte is 60 frames die gelijkwaardige too2 seconden is.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="e5aa8-127">**Potentiële probleem**: gesloten poorten blokkeren het Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="e5aa8-128">**Stappen voor probleemoplossing**: Controleer bij de streaming via RTMP, firewall en/of de proxy-instellingen tooconfirm uitgaande poorten 1935 en 1936 zijn geopend.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="e5aa8-129">Wanneer u RTP streaming, moet u bevestigen dat de uitgaande poort 2010 open is.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="e5aa8-130">Probleem: Bij het configureren van Hallo encoder toostream Hello RTP-protocol, er is geen locatie tooenter een hostnaam.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="e5aa8-131">**Potentiële probleem**: veel RTP coderingsprogramma's niet toegestaan voor hostnamen en een IP-adres moet toobe verkregen.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="e5aa8-132">**Stappen voor probleemoplossing**: toofind Hallo IP-adres, open een opdrachtprompt op elke computer.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="e5aa8-133">toodo open dit in Windows hello uitvoeren starten (WIN + R) en typ 'cmd' tooopen.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="e5aa8-134">Zodra het Hallo-opdrachtprompt is geopend, typt u 'Ping [AMS-hostnaam]'.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="e5aa8-135">Hallo-hostnaam kan worden afgeleid door Hallo poortnummer tussen hello Azure-URL voor opnemen, zoals gemarkeerd in het volgende voorbeeld Hallo weg te laten:</span><span class="sxs-lookup"><span data-stu-id="e5aa8-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="e5aa8-136">RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 /</span><span class="sxs-lookup"><span data-stu-id="e5aa8-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="e5aa8-138">Als na het volgen van Hallo stappen die u nog steeds niet met succes streamen indienen een ondersteuningsticket met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e5aa8-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="e5aa8-139">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="e5aa8-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e5aa8-140">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="e5aa8-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

