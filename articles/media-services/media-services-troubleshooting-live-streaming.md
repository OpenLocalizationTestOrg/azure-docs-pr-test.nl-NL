---
title: Gids voor probleemoplossing voor live streamen | Microsoft Docs
description: Dit onderwerp bevat suggesties over het oplossen van problemen met live streaming.
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
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="cba0b-103">Handleiding voor het oplossen van problemen met live streaming</span><span class="sxs-lookup"><span data-stu-id="cba0b-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="cba0b-104">Dit onderwerp bevat suggesties over het oplossen van enkele live streaming problemen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="cba0b-105">Problemen met on-premises coderingsprogramma 's</span><span class="sxs-lookup"><span data-stu-id="cba0b-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="cba0b-106">Deze sectie vindt u suggesties over het oplossen van problemen met betrekking tot on-premises-coderingsprogramma's die zijn geconfigureerd voor het verzenden van een single-bitrate stream AMS-kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="cba0b-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="cba0b-107">Probleem: Zou willen zien Logboeken</span><span class="sxs-lookup"><span data-stu-id="cba0b-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="cba0b-108">**Potentiële probleem**: kan niet zoeken encoder logboeken die kan helpen bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="cba0b-109">**Telestream Wirecast**: meestal vindt u Logboeken onder C:\Users\{username} \AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="cba0b-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="cba0b-110">**Elementaire Live**: vindt u koppelingen naar Logboeken op de beheerportal heeft.</span><span class="sxs-lookup"><span data-stu-id="cba0b-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="cba0b-111">Klik op **statistieken**, klikt u vervolgens **logboeken**.</span><span class="sxs-lookup"><span data-stu-id="cba0b-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="cba0b-112">Op de **logboekbestanden** pagina ziet u een lijst van Logboeken voor alle items in de LiveEvent; de optie die overeenkomt met de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="cba0b-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="cba0b-113">**Flash Live Mediacoderingsprogramma**: vindt u de **logboekmap...**  door te navigeren naar de **codering logboek** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cba0b-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="cba0b-114">Probleem: Er is geen optie voor het uitvoeren van een progressieve stream</span><span class="sxs-lookup"><span data-stu-id="cba0b-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="cba0b-115">**Potentiële probleem**: de codering wordt gebruikt niet automatisch interliniëring ongedaan maken.</span><span class="sxs-lookup"><span data-stu-id="cba0b-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="cba0b-116">**Stappen voor probleemoplossing**: zoek naar een ongedaan ineengestrengeld optie binnen de interface van het coderingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="cba0b-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="cba0b-117">Zodra de-interlacing is ingeschakeld, Controleer of opnieuw progressief uitvoerinstellingen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="cba0b-118">Probleem: Er is geprobeerd verschillende instellingen voor codering uitvoer en kan nog steeds geen verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="cba0b-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="cba0b-119">**Potentiële probleem**: Azure codering kanaal is niet juist opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cba0b-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="cba0b-120">**Stappen voor probleemoplossing**: Zorg ervoor dat de codering wordt niet langer te worden gepusht AMS, stoppen en opnieuw instellen van het kanaal.</span><span class="sxs-lookup"><span data-stu-id="cba0b-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="cba0b-121">Als opnieuw uit te voeren, probeert u het coderingsprogramma verbinding te maken met de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="cba0b-122">Als dit nog niet het probleem wordt opgelost, probeert u een nieuw kanaal volledig te maken, soms kanalen beschadigd kunnen raken na een aantal mislukte pogingen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="cba0b-123">**Potentiële probleem**: de GOP grootte of Sleutelframe instellingen zijn niet optimaal.</span><span class="sxs-lookup"><span data-stu-id="cba0b-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="cba0b-124">**Stappen voor probleemoplossing**: GOP aanbevolen grootte of keyframe interval is 2 seconden.</span><span class="sxs-lookup"><span data-stu-id="cba0b-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="cba0b-125">Sommige coderingsprogramma's berekenen deze instelling in het aantal frames, terwijl andere seconden.</span><span class="sxs-lookup"><span data-stu-id="cba0b-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="cba0b-126">Bijvoorbeeld: bij het uitvoeren van 30fps, de grootte van de GOP zou worden 60 frames die gelijk is aan twee seconden.</span><span class="sxs-lookup"><span data-stu-id="cba0b-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="cba0b-127">**Potentiële probleem**: de stroom gesloten poorten blokkeren.</span><span class="sxs-lookup"><span data-stu-id="cba0b-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="cba0b-128">**Stappen voor probleemoplossing**: bij het streamen via RTMP, Controleer de firewall en proxy-instellingen om te bevestigen dat de uitgaande poorten 1935 en 1936 geopend zijn.</span><span class="sxs-lookup"><span data-stu-id="cba0b-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="cba0b-129">Wanneer u RTP streaming, moet u bevestigen dat de uitgaande poort 2010 open is.</span><span class="sxs-lookup"><span data-stu-id="cba0b-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="cba0b-130">Probleem: Bij het configureren van het coderingsprogramma naar een stream met het protocol RTP, er is geen geschikt voor een hostnaam opgeeft.</span><span class="sxs-lookup"><span data-stu-id="cba0b-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="cba0b-131">**Potentiële probleem**: veel RTP coderingsprogramma's niet toegestaan voor hostnamen en een IP-adres moet worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="cba0b-132">**Stappen voor probleemoplossing**: als u het IP-adres zoekt, open een opdrachtprompt op elke computer.</span><span class="sxs-lookup"><span data-stu-id="cba0b-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="cba0b-133">U doet dit in Windows, opent u het venster uitvoeren starten (WIN + R) en typ 'cmd' te openen.</span><span class="sxs-lookup"><span data-stu-id="cba0b-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="cba0b-134">Zodra de opdrachtprompt geopend is, typt u 'Ping [AMS-hostnaam]'.</span><span class="sxs-lookup"><span data-stu-id="cba0b-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="cba0b-135">De hostnaam kan worden afgeleid door het poortnummer van de Azure URL voor opnemen, zoals gemarkeerd in het volgende voorbeeld weg te laten:</span><span class="sxs-lookup"><span data-stu-id="cba0b-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="cba0b-136">RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 /</span><span class="sxs-lookup"><span data-stu-id="cba0b-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="cba0b-138">Verzenden als nadat u de stappen die u nog steeds niet met succes streamen, een ondersteuningsticket met de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cba0b-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="cba0b-139">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="cba0b-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cba0b-140">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="cba0b-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

