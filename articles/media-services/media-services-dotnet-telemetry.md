---
title: aaaConfiguring telemetrie van Azure Media Services met .NET | Microsoft Docs
description: Dit artikel laat zien hoe toouse Hallo telemetrie van Azure Media Services met .NET SDK.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 4019fa7d080ca3f8a8709bd1e666f7062b883954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="73bc6-103">Configureren van telemetrie van Azure Media Services met .NET</span><span class="sxs-lookup"><span data-stu-id="73bc6-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="73bc6-104">Dit onderwerp beschrijft de algemene stappen die u bij het configureren van hello Azure Media Services (AMS) telemetrie met .NET SDK kan duren.</span><span class="sxs-lookup"><span data-stu-id="73bc6-104">This topic describes general steps that you might take when configuring hello Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="73bc6-105">Voor hello gedetailleerde uitleg van wat AMS telemetrie is en hoe tooconsume, Zie Hallo [overzicht](media-services-telemetry-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="73bc6-105">For hello detailed explanation of what is AMS telemetry and how tooconsume it, see hello [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="73bc6-106">U kunt telemetrische gegevens in een van de volgende manieren hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="73bc6-106">You can consume telemetry data in one of hello following ways:</span></span>

- <span data-ttu-id="73bc6-107">Gegevens lezen rechtstreeks vanuit Azure Table Storage (bijvoorbeeld via Hallo opslag-SDK).</span><span class="sxs-lookup"><span data-stu-id="73bc6-107">Read data directly from Azure Table Storage (e.g. using hello Storage SDK).</span></span> <span data-ttu-id="73bc6-108">Hallo beschrijving van telemetrie storage-tabellen, Zie Hallo **verbruikt telemetrie informatie** in [dit](https://msdn.microsoft.com/library/mt742089.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="73bc6-108">For hello description of telemetry storage tables, see hello **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="73bc6-109">of</span><span class="sxs-lookup"><span data-stu-id="73bc6-109">Or</span></span>

- <span data-ttu-id="73bc6-110">Hallo-ondersteuning voor gebruik in Hallo Media Services .NET SDK voor het lezen van gegevens in de opslag.</span><span class="sxs-lookup"><span data-stu-id="73bc6-110">Use hello support in hello Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="73bc6-111">Dit onderwerp wordt beschreven hoe tooenable telemetrie voor Hallo AMS-account opgegeven en hoe tooquery Hallo metrische gegevens met Azure Media Services .NET SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="73bc6-111">This topic shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="73bc6-112">Telemetrie voor een Media Services-account configureren</span><span class="sxs-lookup"><span data-stu-id="73bc6-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="73bc6-113">Hallo zijn volgende stappen nodig tooenable telemetrie:</span><span class="sxs-lookup"><span data-stu-id="73bc6-113">hello following steps are needed tooenable telemetry:</span></span>

- <span data-ttu-id="73bc6-114">Hallo-referenties van Hallo storage-account gekoppeld toohello Media Services-account ophalen.</span><span class="sxs-lookup"><span data-stu-id="73bc6-114">Get hello credentials of hello storage account attached toohello Media Services account.</span></span> 
- <span data-ttu-id="73bc6-115">Maak een Meldingseindpunt met **EndPointType** instellen te**AzureTable** en endPointAddress toohello opslag tabel verwijst.</span><span class="sxs-lookup"><span data-stu-id="73bc6-115">Create a Notification Endpoint with **EndPointType** set too**AzureTable** and endPointAddress pointing toohello storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="73bc6-116">Een controleconfiguratie instellingen maken voor Hallo services u wilt dat toomonitor.</span><span class="sxs-lookup"><span data-stu-id="73bc6-116">Create a monitoring configuration settings for hello services you want toomonitor.</span></span> <span data-ttu-id="73bc6-117">Niet meer dan één configuratie-instellingen voor bewaking is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="73bc6-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="73bc6-118">Telemetrie-informatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="73bc6-118">Consuming telemetry information</span></span>

<span data-ttu-id="73bc6-119">Zie voor informatie over consumerende telemetrie [dit](media-services-telemetry-overview.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="73bc6-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="73bc6-120">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="73bc6-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="73bc6-121">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="73bc6-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="73bc6-122">Hallo element te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:</span><span class="sxs-lookup"><span data-stu-id="73bc6-122">Add hello following element too**appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="73bc6-123">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="73bc6-123">Example</span></span>  
    
<span data-ttu-id="73bc6-124">Hallo volgende voorbeeld ziet u hoe tooenable telemetrie voor Hallo AMS-account opgegeven en hoe tooquery Hallo metrische gegevens met Azure Media Services .NET SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="73bc6-124">hello following example shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print hello channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="73bc6-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73bc6-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="73bc6-126">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="73bc6-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
