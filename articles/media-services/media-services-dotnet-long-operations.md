---
title: aaaPolling langlopende bewerkingen | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toopoll langlopende bewerkingen.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="66b51-103">Live streamen met Azure mediaservices leveren</span><span class="sxs-lookup"><span data-stu-id="66b51-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="66b51-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="66b51-104">Overview</span></span>

<span data-ttu-id="66b51-105">Microsoft Azure Media Services biedt API's die aanvragen tooMedia Services toostart bewerkingen verzenden (bijvoorbeeld: maken, starten, stoppen of verwijderen van een kanaal).</span><span class="sxs-lookup"><span data-stu-id="66b51-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="66b51-106">Deze bewerkingen zijn langlopend.</span><span class="sxs-lookup"><span data-stu-id="66b51-106">These operations are long-running.</span></span>

<span data-ttu-id="66b51-107">Hallo Media Services .NET SDK biedt API's die Hallo aanvraag verzenden en te wachten op Hallo bewerking toocomplete (intern hello API's zijn gedelegeerd voor bewerking uitgevoerd met een bepaalde interval).</span><span class="sxs-lookup"><span data-stu-id="66b51-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="66b51-108">Bijvoorbeeld bij het aanroepen van kanaal. Start(), Hallo-methode retourneert nadat Hallo-kanaal is gestart.</span><span class="sxs-lookup"><span data-stu-id="66b51-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="66b51-109">U kunt ook de asynchrone versie hello gebruiken: wachten op een kanaal. StartAsync() (Zie voor meer informatie over de taakgebaseerde asynchrone patroon [tik](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="66b51-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="66b51-110">API's die een aanvraag verzendt en vervolgens poll-frequentie voor Hallo status totdat het Hallo-bewerking is voltooid, worden 'polling methoden' genoemd.</span><span class="sxs-lookup"><span data-stu-id="66b51-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="66b51-111">Deze methoden (met name Hallo asynchrone versie) worden aanbevolen voor interactieve toepassingen en/of stateful services.</span><span class="sxs-lookup"><span data-stu-id="66b51-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="66b51-112">Er zijn scenario's waarbij een toepassing niet kan wachten op een langdurige http-aanvraag en toopoll handmatig wil voor Hallo bewerking uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="66b51-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="66b51-113">Een typisch voorbeeld zou een browser interactie met een stateless webservice: als Hallo browser aanvraagt toocreate een kanaal, Hallo webservice initieert een langdurige bewerking retourneert Hallo bewerking-ID toohello browser.</span><span class="sxs-lookup"><span data-stu-id="66b51-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="66b51-114">Hallo browser kan vervolgens vraagt u Hallo web service tooget Hallo bewerkingsstatus op basis van het Hallo-ID.</span><span class="sxs-lookup"><span data-stu-id="66b51-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="66b51-115">Hallo Media Services .NET SDK biedt API's die handig voor dit scenario zijn.</span><span class="sxs-lookup"><span data-stu-id="66b51-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="66b51-116">Deze API's worden 'niet polling methoden' genoemd.</span><span class="sxs-lookup"><span data-stu-id="66b51-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="66b51-117">Hallo ' niet polling methoden' hebben Hallo volgende naamgevingspatroon: verzenden*OperationName*bewerking (bijvoorbeeld SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="66b51-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="66b51-118">Verzenden*OperationName*bewerking methoden retourneren Hallo **IOperation** object; hello geretourneerde object bevat informatie die gebruikt tootrack Hallo-bewerking worden kan.</span><span class="sxs-lookup"><span data-stu-id="66b51-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="66b51-119">Hallo verzenden*OperationName*OperationAsync methoden retourneren **taak<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="66b51-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="66b51-120">Op dit moment Hallo volgende klassen ondersteuning niet polling methoden: **kanaal**, **StreamingEndpoint**, en **programma**.</span><span class="sxs-lookup"><span data-stu-id="66b51-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="66b51-121">toopoll voor bewerkingsstatus hello, gebruik Hallo **GetOperation** methode op Hallo **OperationBaseCollection** klasse.</span><span class="sxs-lookup"><span data-stu-id="66b51-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="66b51-122">Hallo intervallen toocheck Hallo bewerkingsstatus volgende gebruiken: voor **kanaal** en **StreamingEndpoint** bewerkingen, gebruikt u 30 seconden; voor **programma** bewerkingen, gebruikmaken van 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="66b51-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="66b51-123">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="66b51-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="66b51-124">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="66b51-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="66b51-125">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="66b51-125">Example</span></span>

<span data-ttu-id="66b51-126">Hallo volgende voorbeeld definieert een klasse met de naam **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="66b51-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="66b51-127">De definitie van deze klasse kan een startpunt voor de klassedefinitie van uw web-service zijn.</span><span class="sxs-lookup"><span data-stu-id="66b51-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="66b51-128">Eenvoud gebruik hello volgende voorbeelden voor Hallo niet asynchrone versies van methoden.</span><span class="sxs-lookup"><span data-stu-id="66b51-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="66b51-129">Hallo-voorbeeld ziet u ook hoe deze klasse in Hallo-client kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="66b51-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="66b51-130">De klassendefinitie ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="66b51-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
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
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="66b51-131">Hallo-clientcode</span><span class="sxs-lookup"><span data-stu-id="66b51-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="66b51-132">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="66b51-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="66b51-133">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="66b51-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

