---
title: Live streamen met Azure Media Services om multi-bitrate streams te maken met .NET | Microsoft Docs
description: In deze zelfstudie wordt u begeleid bij de stappen voor het maken van een kanaal dat een single-bitrate livestream ontvangt, en het coderen van deze stream naar een multi-bitrate stream met .NET SDK.
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22d63ff5e9fd33db8711b0c5125ab0882b9f6a74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-using-azure-media-services-to-create-multi-bitrate-streams-with-net"></a><span data-ttu-id="5bebb-103">Live streamen met Azure Media Services om multi-bitrate streams te maken met .NET</span><span class="sxs-lookup"><span data-stu-id="5bebb-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bebb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5bebb-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="5bebb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5bebb-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="5bebb-106">REST API</span><span class="sxs-lookup"><span data-stu-id="5bebb-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="5bebb-107">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="5bebb-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5bebb-108">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bebb-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="5bebb-109">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5bebb-109">Overview</span></span>
<span data-ttu-id="5bebb-110">In deze zelfstudie wordt u begeleid bij de stappen voor het maken van een **kanaal** dat een single-bitrate livestream ontvangt, en het coderen van deze stream naar een multi-bitrate stream.</span><span class="sxs-lookup"><span data-stu-id="5bebb-110">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span></span>

<span data-ttu-id="5bebb-111">Zie [Live streamen met Azure Media Services om multi-bitrate streams te maken](media-services-manage-live-encoder-enabled-channels.md) voor meer conceptuele informatie over kanalen die zijn ingeschakeld voor live codering.</span><span class="sxs-lookup"><span data-stu-id="5bebb-111">For more conceptual information related to Channels that are enabled for live encoding, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="5bebb-112">Algemeen scenario voor live streamen</span><span class="sxs-lookup"><span data-stu-id="5bebb-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="5bebb-113">In de onderstaande stappen worden de taken beschreven voor het maken van algemene toepassingen voor het maken van livestreams.</span><span class="sxs-lookup"><span data-stu-id="5bebb-113">The following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="5bebb-114">De maximum aanbevolen duur van een live gebeurtenis is momenteel acht uur.</span><span class="sxs-lookup"><span data-stu-id="5bebb-114">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="5bebb-115">Neem contact op met amslived op Microsoft.com als u een kanaal voor langere tijd wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5bebb-115">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="5bebb-116">Sluit een videocamera aan op een computer.</span><span class="sxs-lookup"><span data-stu-id="5bebb-116">Connect a video camera to a computer.</span></span> <span data-ttu-id="5bebb-117">Start en configureer een on-premises livecoderingsprogramma dat een single-bitrate stream in een van de volgende protocollen kan uitvoeren: RTMP, Smooth Streaming of RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="5bebb-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="5bebb-118">Zie [Azure Media Services RTMP-ondersteuning en live coderingsprogramma's](http://go.microsoft.com/fwlink/?LinkId=532824) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bebb-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="5bebb-119">Deze stap kan ook worden uitgevoerd nadat u uw kanaal hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5bebb-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="5bebb-120">Maak en start een kanaal.</span><span class="sxs-lookup"><span data-stu-id="5bebb-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="5bebb-121">Haal de URL voor opnemen voor het kanaal op.</span><span class="sxs-lookup"><span data-stu-id="5bebb-121">Retrieve the Channel ingest URL.</span></span>

    <span data-ttu-id="5bebb-122">De URL voor opnemen wordt gebruikt door het live coderingsprogramma om de stream naar het kanaal te verzenden.</span><span class="sxs-lookup"><span data-stu-id="5bebb-122">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>

4. <span data-ttu-id="5bebb-123">Haal de voorbeeld-URL voor het kanaal op.</span><span class="sxs-lookup"><span data-stu-id="5bebb-123">Retrieve the Channel preview URL.</span></span>

    <span data-ttu-id="5bebb-124">Gebruik deze URL om te controleren of de livestream goed door het kanaal wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="5bebb-124">Use this URL to verify that your channel is properly receiving the live stream.</span></span>

5. <span data-ttu-id="5bebb-125">Maak een asset.</span><span class="sxs-lookup"><span data-stu-id="5bebb-125">Create an asset.</span></span>
6. <span data-ttu-id="5bebb-126">Als u wilt dat de asset dynamisch worden versleuteld tijdens het afspelen, gaat u als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5bebb-126">If you want for the asset to be dynamically encrypted during playback, do the following:</span></span>
7. <span data-ttu-id="5bebb-127">Maak een inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="5bebb-127">Create a content key.</span></span>
8. <span data-ttu-id="5bebb-128">Configureer het autorisatiebeleid voor de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="5bebb-128">Configure the content key's authorization policy.</span></span>
9. <span data-ttu-id="5bebb-129">Configureer het beleid voor de levering van assets (gebruikt door dynamische pakketten en dynamische versleuteling).</span><span class="sxs-lookup"><span data-stu-id="5bebb-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="5bebb-130">Maak een programma en geef op dat de asset die u hebt gemaakt, moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5bebb-130">Create a program and specify to use the asset that you created.</span></span>
11. <span data-ttu-id="5bebb-131">Publiceer de asset die aan het programma is gekoppeld door een OnDemand-locator te maken.</span><span class="sxs-lookup"><span data-stu-id="5bebb-131">Publish the asset associated with the program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5bebb-132">Wanneer uw AMS-account is gemaakt, wordt er een **standaardstreaming-eindpunt** met de status **Gestopt** toegevoegd aan uw account.</span><span class="sxs-lookup"><span data-stu-id="5bebb-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="5bebb-133">Het streaming-eindpunt van waar u inhoud wilt streamen, moet de status **Wordt uitgevoerd** hebben.</span><span class="sxs-lookup"><span data-stu-id="5bebb-133">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

12. <span data-ttu-id="5bebb-134">Start het programma wanneer u klaar bent om te streamen en te archiveren.</span><span class="sxs-lookup"><span data-stu-id="5bebb-134">Start the program when you are ready to start streaming and archiving.</span></span>
13. <span data-ttu-id="5bebb-135">Het live coderingsprogramma kan desgewenst een signaal ontvangen dat een advertentie moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="5bebb-135">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="5bebb-136">De advertentie wordt ingevoegd in de uitvoerstream.</span><span class="sxs-lookup"><span data-stu-id="5bebb-136">The advertisement is inserted in the output stream.</span></span>
14. <span data-ttu-id="5bebb-137">Stop het programma als u het streamen wilt stoppen en de gebeurtenis wilt archiveren.</span><span class="sxs-lookup"><span data-stu-id="5bebb-137">Stop the program whenever you want to stop streaming and archiving the event.</span></span>
15. <span data-ttu-id="5bebb-138">Verwijder het programma (en verwijder desgewenst de asset).</span><span class="sxs-lookup"><span data-stu-id="5bebb-138">Delete the Program (and optionally delete the asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5bebb-139">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5bebb-139">What you'll learn</span></span>
<span data-ttu-id="5bebb-140">In dit onderwerp wordt beschreven hoe u verschillende bewerkingen op kanalen en programma's met Media Services .NET SDK uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5bebb-140">This topic shows you how to execute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="5bebb-141">Aangezien veel bewerkingen langlopend zijn, worden er .NET API's gebruikt waarmee langlopende bewerkingen worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="5bebb-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="5bebb-142">In het onderwerp wordt beschreven hoe u het volgende doet:</span><span class="sxs-lookup"><span data-stu-id="5bebb-142">The topic shows how to do the following:</span></span>

1. <span data-ttu-id="5bebb-143">Een kanaal maken en starten.</span><span class="sxs-lookup"><span data-stu-id="5bebb-143">Create and start a channel.</span></span> <span data-ttu-id="5bebb-144">Er worden langlopende API's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5bebb-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="5bebb-145">Zorg ervoor dat de kanalen het (invoer)eindpunt opnemen.</span><span class="sxs-lookup"><span data-stu-id="5bebb-145">Get the channels ingest (input) endpoint.</span></span> <span data-ttu-id="5bebb-146">Dit eindpunt wordt opgegeven voor het coderingsprogramma dat een single-bitrate livestream kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="5bebb-146">This endpoint should be provided to the encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="5bebb-147">Haal het preview-eindpunt op.</span><span class="sxs-lookup"><span data-stu-id="5bebb-147">Get the preview endpoint.</span></span> <span data-ttu-id="5bebb-148">Dit eindpunt wordt gebruikt om een voorbeeld van uw stream te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5bebb-148">This endpoint is used to preview your stream.</span></span>
4. <span data-ttu-id="5bebb-149">Maak een asset die wordt gebruikt voor het opslaan van uw inhoud.</span><span class="sxs-lookup"><span data-stu-id="5bebb-149">Create an asset that will be used to store your content.</span></span> <span data-ttu-id="5bebb-150">Het beleid voor de levering van assets moet ook worden geconfigureerd, zoals in dit voorbeeld wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="5bebb-150">The asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="5bebb-151">Maak een programma en geef op dat de eerder gemaakte asset moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5bebb-151">Create a program and specify to use the asset that was created earlier.</span></span> <span data-ttu-id="5bebb-152">Start het programma.</span><span class="sxs-lookup"><span data-stu-id="5bebb-152">Start the program.</span></span> <span data-ttu-id="5bebb-153">Er worden langlopende API's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5bebb-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="5bebb-154">Maak een locator voor de asset zodat de inhoud wordt gepubliceerd en kan worden gestreamd naar uw clients.</span><span class="sxs-lookup"><span data-stu-id="5bebb-154">Create a locator for the asset, so the content gets published and can be streamed to your clients.</span></span>
7. <span data-ttu-id="5bebb-155">Geef slates weer en verberg ze.</span><span class="sxs-lookup"><span data-stu-id="5bebb-155">Show and hide slates.</span></span> <span data-ttu-id="5bebb-156">Start en stop advertenties.</span><span class="sxs-lookup"><span data-stu-id="5bebb-156">Start and stop advertisements.</span></span> <span data-ttu-id="5bebb-157">Er worden langlopende API's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5bebb-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="5bebb-158">Schoon het kanaal en alle bijbehorende resources op.</span><span class="sxs-lookup"><span data-stu-id="5bebb-158">Clean up your channel and all the associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bebb-159">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5bebb-159">Prerequisites</span></span>
<span data-ttu-id="5bebb-160">Hieronder wordt aangegeven wat de vereisten zijn om de zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="5bebb-160">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="5bebb-161">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5bebb-161">An Azure account.</span></span> <span data-ttu-id="5bebb-162">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="5bebb-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5bebb-163">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bebb-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="5bebb-164">U ontvangt tegoed dat kan worden gebruikt om betaalde Azure-services te proberen.</span><span class="sxs-lookup"><span data-stu-id="5bebb-164">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="5bebb-165">Zelfs nadat het tegoed is gebruikt, kunt u het account houden en de gratis Azure-services en -functies gebruiken, zoals de functie Web Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5bebb-165">Even after the credits are used up, you can keep the account and use free Azure services and features, such as the Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="5bebb-166">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="5bebb-166">A Media Services account.</span></span> <span data-ttu-id="5bebb-167">Zie [Account maken](media-services-portal-create-account.md) voor meer informatie over het maken van een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="5bebb-167">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="5bebb-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate of Express) of hoger.</span><span class="sxs-lookup"><span data-stu-id="5bebb-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="5bebb-169">U moet Media Services .NET SDK versie 3.2.0.0 of hoger gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5bebb-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="5bebb-170">Een webcam en een coderingsprogramma dat een single bitrate livestream kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="5bebb-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="5bebb-171">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="5bebb-171">Considerations</span></span>
* <span data-ttu-id="5bebb-172">De maximum aanbevolen duur van een live gebeurtenis is momenteel acht uur.</span><span class="sxs-lookup"><span data-stu-id="5bebb-172">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="5bebb-173">Neem contact op met amslived op Microsoft.com als u een kanaal voor langere tijd wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5bebb-173">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
* <span data-ttu-id="5bebb-174">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="5bebb-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5bebb-175">U moet dezelfde beleids-id gebruiken als u altijd dezelfde dagen/toegangsmachtigingen gebruikt, bijvoorbeeld beleidsregels voor locators die zijn bedoeld om gedurende een lange periode gehandhaafd te blijven (niet-upload-beleidsregels).</span><span class="sxs-lookup"><span data-stu-id="5bebb-175">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5bebb-176">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bebb-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="5bebb-177">Voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="5bebb-177">Download sample</span></span>

<span data-ttu-id="5bebb-178">U kunt [hier](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/) het voorbeeld downloaden dat in dit onderwerp wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="5bebb-178">You can download the sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="5bebb-179">Setup voor de ontwikkeling met Media Services SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="5bebb-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="5bebb-180">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5bebb-180">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="5bebb-181">Voorbeeld van code</span><span class="sxs-lookup"><span data-stu-id="5bebb-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // The channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use the previewEndpoint to preview and verify 
            // that the input from the encoder is actually reaching the Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of the live feed as it reaches the Channel. 
            // This can be a valuable tool to check whether your live feed is actually reaching the Channel. 
            // The thumbnail is exposed via the same end-point as the Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if the channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set to StreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order to be able to publish and stream the video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with the channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting to track ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, the operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created entity Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the entity Id associated with the sucessful operation is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle the failure. 
                // For example, throw an exception. 
                // Use the following information in the exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="5bebb-182">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="5bebb-182">Next step</span></span>
<span data-ttu-id="5bebb-183">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="5bebb-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5bebb-184">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="5bebb-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


