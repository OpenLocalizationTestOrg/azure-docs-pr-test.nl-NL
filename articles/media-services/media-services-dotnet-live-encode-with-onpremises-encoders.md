---
title: Live streamen met lokale coderingsprogramma's met .NET | Microsoft Docs
description: Dit onderwerp leest hoe u met .NET live coderen met on-premises coderingsprogramma's.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/18/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 3ef6065f5b9e05e0ea5716548699943a2c877bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="a04b4-103">Live streamen met lokale coderingsprogramma's met .NET</span><span class="sxs-lookup"><span data-stu-id="a04b4-103">How to perform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a04b4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a04b4-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="a04b4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a04b4-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="a04b4-106">REST</span><span class="sxs-lookup"><span data-stu-id="a04b4-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="a04b4-107">Deze zelfstudie leert u de stappen voor het gebruik van Azure Media Services .NET SDK voor het maken van een **kanaal** die is geconfigureerd voor een doorvoerlevering.</span><span class="sxs-lookup"><span data-stu-id="a04b4-107">This tutorial walks you through the steps of using the Azure Media Services .NET SDK to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a04b4-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a04b4-108">Prerequisites</span></span>
<span data-ttu-id="a04b4-109">Hieronder wordt aangegeven wat de vereisten zijn om de zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="a04b4-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="a04b4-110">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a04b4-110">An Azure account.</span></span>
* <span data-ttu-id="a04b4-111">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="a04b4-111">A Media Services account.</span></span>    <span data-ttu-id="a04b4-112">Zie [Een Media Services-account maken](media-services-portal-create-account.md) voor meer informatie over het maken van een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="a04b4-112">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a04b4-113">Instellen van uw Developer-omgeving.</span><span class="sxs-lookup"><span data-stu-id="a04b4-113">Set up your dev environment.</span></span> <span data-ttu-id="a04b4-114">Zie voor meer informatie [instellen van uw omgeving](media-services-set-up-computer.md).</span><span class="sxs-lookup"><span data-stu-id="a04b4-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="a04b4-115">Een webcam.</span><span class="sxs-lookup"><span data-stu-id="a04b4-115">A webcam.</span></span> <span data-ttu-id="a04b4-116">Bijvoorbeeld [Telestream Wirecast-coderingsprogramma](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="a04b4-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="a04b4-117">Aanbevolen om te controleren van de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="a04b4-117">Recommended to review the following articles:</span></span>

* [<span data-ttu-id="a04b4-118">Azure Media Services RTMP-ondersteuning en live coderingsprogramma's</span><span class="sxs-lookup"><span data-stu-id="a04b4-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="a04b4-119">Live streamen met on-premises coderingsprogramma's die multi-bitrate streams maken</span><span class="sxs-lookup"><span data-stu-id="a04b4-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a04b4-120">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="a04b4-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a04b4-121">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a04b4-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="a04b4-122">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a04b4-122">Example</span></span>
<span data-ttu-id="a04b4-123">De volgende voorbeeldcode laat zien hoe bereiken van de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="a04b4-123">The following code example demonstrates how to achieve the following tasks:</span></span>

* <span data-ttu-id="a04b4-124">Verbinding met Media Services maken</span><span class="sxs-lookup"><span data-stu-id="a04b4-124">Connect to Media Services</span></span>
* <span data-ttu-id="a04b4-125">Een kanaal maken</span><span class="sxs-lookup"><span data-stu-id="a04b4-125">Create a channel</span></span>
* <span data-ttu-id="a04b4-126">Bijwerken van het kanaal</span><span class="sxs-lookup"><span data-stu-id="a04b4-126">Update the channel</span></span>
* <span data-ttu-id="a04b4-127">Het kanaal invoereindpunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="a04b4-127">Retrieve the channel’s input endpoint.</span></span> <span data-ttu-id="a04b4-128">Het invoereindpunt wordt opgegeven voor de on-premises live codering.</span><span class="sxs-lookup"><span data-stu-id="a04b4-128">The input endpoint should be provided to the on-premises live encoder.</span></span> <span data-ttu-id="a04b4-129">De live codering converteert signalen van de camera naar stromen die worden verzonden naar het kanaal-invoer opnemen () eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a04b4-129">The live encoder converts signals from the camera to streams that are sent to the channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="a04b4-130">Ophalen van het kanaal preview-eindpunt</span><span class="sxs-lookup"><span data-stu-id="a04b4-130">Retrieve the channel’s preview endpoint</span></span>
* <span data-ttu-id="a04b4-131">Maken en een programma te starten</span><span class="sxs-lookup"><span data-stu-id="a04b4-131">Create and start a program</span></span>
* <span data-ttu-id="a04b4-132">Maak een locator nodig voor toegang tot het programma</span><span class="sxs-lookup"><span data-stu-id="a04b4-132">Create a locator needed to access the program</span></span>
* <span data-ttu-id="a04b4-133">Maak en start een StreamingEndpoint</span><span class="sxs-lookup"><span data-stu-id="a04b4-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="a04b4-134">Bijwerken van het streaming-eindpunt</span><span class="sxs-lookup"><span data-stu-id="a04b4-134">Update the streaming endpoint</span></span>
* <span data-ttu-id="a04b4-135">Resources afsluiten</span><span class="sxs-lookup"><span data-stu-id="a04b4-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="a04b4-136">Controleer of het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** heeft.</span><span class="sxs-lookup"><span data-stu-id="a04b4-136">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="a04b4-137">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a04b4-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a04b4-138">U moet dezelfde beleids-id gebruiken als u altijd dezelfde dagen/toegangsmachtigingen gebruikt, bijvoorbeeld beleidsregels voor locators die zijn bedoeld om gedurende een lange periode gehandhaafd te blijven (niet-upload-beleidsregels).</span><span class="sxs-lookup"><span data-stu-id="a04b4-138">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a04b4-139">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a04b4-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="a04b4-140">Zie voor meer informatie over het configureren van een live coderingsprogramma [Azure Media Services RTMP-ondersteuning en Live coderingsprogramma's](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span><span class="sxs-lookup"><span data-stu-id="a04b4-140">For information on how to configure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSLiveTest
    {
        class Program
        {
        private const string StreamingEndpointName = "streamingendpoint001";
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

            // Set the Live Encoder to point to the channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use the previewEndpoint to preview and verify
            // that the input from the encoder is actually reaching the Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want to change the Smooth fragments to HLS segment ratio, you would set the ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time to execute. To determine the state of operations after calling Start or Stop, query the IChannel.State .

            channel.Start();

            return channel;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTMP,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                    {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access to IP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

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
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access to IP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            channel.Update();
        }

        public static IProgram CreateAndStartProgram(IChannel channel)
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            // Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
            // however each Program must have a unique name within your Media Services account.
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            program.Start();

            return program;
        }

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

        public static IStreamingEndpoint CreateAndStartStreamingEndpoint(bool createNew)
        {
            IStreamingEndpoint streamingEndpoint = null;
            if (createNew)
            {
            var options = new StreamingEndpointCreationOptions
            {
                Name = StreamingEndpointName,
                ScaleUnits = 1,
                AccessControl = GetAccessControl(),
                CacheControl = GetCacheControl()
            };

            streamingEndpoint = _context.StreamingEndpoints.Create(options);
            }
            else
            {
            streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            }


            if (streamingEndpoint.State == StreamingEndpointState.Stopped)
            streamingEndpoint.Start();

            return streamingEndpoint;
        }

        private static StreamingEndpointAccessControl GetAccessControl()
        {
            return new StreamingEndpointAccessControl
            {
            IPAllowList = new List<IPRange>
                {
                new IPRange
                {
                    Name = "Allow all",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                }
                },

            AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                {
                new AkamaiSignatureHeaderAuthenticationKey
                {
                    Identifier = "My key",
                    Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                    Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                }
                }
            };
        }

        private static byte[] GenerateRandomBytes(int length)
        {
            var bytes = new byte[length];
            using (var rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(bytes);
            }

            return bytes;
        }

        private static StreamingEndpointCacheControl GetCacheControl()
        {
            return new StreamingEndpointCacheControl
            {
            MaxAge = TimeSpan.FromSeconds(1000)
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            streamingEndpoint.Update();
        }

        public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                        IChannel channel)
        {
            if (streamingEndpoint != null)
            {
            streamingEndpoint.Stop();
            if(streamingEndpoint.Name != "default")
                streamingEndpoint.Delete();
            }

            IAsset asset;
            if (channel != null)
            {

            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                program.Stop();
                program.Delete();

                if (asset != null)
                {
                foreach (var l in asset.Locators)
                    l.Delete();

                asset.Delete();
                }
            }

            channel.Stop();
            channel.Delete();
            }
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="a04b4-141">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="a04b4-141">Next Step</span></span>
<span data-ttu-id="a04b4-142">Media Services-leertrajecten bekijken</span><span class="sxs-lookup"><span data-stu-id="a04b4-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a04b4-143">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="a04b4-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

