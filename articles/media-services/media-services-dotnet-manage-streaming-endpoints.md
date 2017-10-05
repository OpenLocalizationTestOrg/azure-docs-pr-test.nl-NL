---
title: Streaming-eindpunten met .NET SDK beheren. | Microsoft Docs
description: Dit onderwerp leest hoe voor het beheren van streaming-eindpunten met de Azure-portal.
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
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="15ff9-104">Streaming-eindpunten met .NET SDK beheren</span><span class="sxs-lookup"><span data-stu-id="15ff9-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="15ff9-105">Leest de [overzicht](media-services-streaming-endpoints-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="15ff9-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="15ff9-106">Bekijk ook [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="15ff9-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="15ff9-107">De code in dit onderwerp toont hoe u de volgende taken uitvoeren met Azure Media Services .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="15ff9-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="15ff9-108">Bekijk het standaard streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="15ff9-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="15ff9-109">Nieuwe streaming-eindpunt maken/toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15ff9-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="15ff9-110">U kunt meerdere streaming-eindpunten hebben als u van plan bent een andere CDN of een CDN en directe toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="15ff9-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15ff9-111">U wordt alleen gefactureerd als uw Streaming-eindpunt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="15ff9-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="15ff9-112">Werk het streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="15ff9-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="15ff9-113">Zorg ervoor dat de functie Update() aanroepen.</span><span class="sxs-lookup"><span data-stu-id="15ff9-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="15ff9-114">Verwijder het streaming-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="15ff9-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="15ff9-115">Het standaard streaming-eindpunt kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="15ff9-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="15ff9-116">Zie voor meer informatie over het schalen van het streaming-eindpunt [dit](media-services-portal-scale-streaming-endpoints.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="15ff9-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="15ff9-117">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="15ff9-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="15ff9-118">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="15ff9-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="15ff9-119">Code die wordt beheerd streaming-eindpunten toevoegen</span><span class="sxs-lookup"><span data-stu-id="15ff9-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="15ff9-120">Vervang de code in de Program.cs met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="15ff9-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
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


## <a name="next-steps"></a><span data-ttu-id="15ff9-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15ff9-121">Next steps</span></span>
<span data-ttu-id="15ff9-122">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="15ff9-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="15ff9-123">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="15ff9-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

