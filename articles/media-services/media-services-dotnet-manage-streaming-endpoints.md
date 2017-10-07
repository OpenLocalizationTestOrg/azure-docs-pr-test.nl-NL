---
title: aaaManage streaming-eindpunten met .NET SDK. | Microsoft Docs
description: Dit onderwerp leest hoe toomanage streaming-eindpunten met hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="46c86-104">Streaming-eindpunten met .NET SDK beheren</span><span class="sxs-lookup"><span data-stu-id="46c86-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="46c86-105">Zorg ervoor dat tooreview hello [overzicht](media-services-streaming-endpoints-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="46c86-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="46c86-106">Bekijk ook [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="46c86-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="46c86-107">Hallo-code in dit onderwerp wordt getoond hoe toodo Hallo na taken met Azure Media Services .NET SDK Hallo:</span><span class="sxs-lookup"><span data-stu-id="46c86-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="46c86-108">Bekijk Hallo standaardstreaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="46c86-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="46c86-109">Nieuwe streaming-eindpunt maken/toevoegen.</span><span class="sxs-lookup"><span data-stu-id="46c86-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="46c86-110">U kunt toohave meerdere streaming-eindpunten als u van plan toohave bent verschillende CDN of een CDN en directe toegang.</span><span class="sxs-lookup"><span data-stu-id="46c86-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="46c86-111">U wordt alleen gefactureerd als uw Streaming-eindpunt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46c86-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="46c86-112">Hallo streaming-eindpunt worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="46c86-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="46c86-113">Zorg ervoor dat toocall Hallo Update() functie.</span><span class="sxs-lookup"><span data-stu-id="46c86-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="46c86-114">Hallo streaming-eindpunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="46c86-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="46c86-115">Hallo standaardstreaming-eindpunt kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="46c86-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="46c86-116">Zie voor meer informatie over hoe tooscale streaming-eindpunt Hallo [dit](media-services-portal-scale-streaming-endpoints.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="46c86-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="46c86-117">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="46c86-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="46c86-118">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="46c86-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="46c86-119">Code die wordt beheerd streaming-eindpunten toevoegen</span><span class="sxs-lookup"><span data-stu-id="46c86-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="46c86-120">Hallo-code in Program.cs Hallo vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="46c86-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
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

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="46c86-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46c86-121">Next steps</span></span>
<span data-ttu-id="46c86-122">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="46c86-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="46c86-123">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="46c86-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

