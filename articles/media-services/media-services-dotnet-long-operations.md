---
title: Polling langlopende bewerkingen | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe pollen langlopende bewerkingen.
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
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="2f3b4-103">Live streamen met Azure mediaservices leveren</span><span class="sxs-lookup"><span data-stu-id="2f3b4-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="2f3b4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2f3b4-104">Overview</span></span>

<span data-ttu-id="2f3b4-105">Microsoft Azure Media Services biedt API's die aanvragen verzenden naar de Media Services activiteiten te starten (bijvoorbeeld: maken, starten, stoppen of verwijderen van een kanaal).</span><span class="sxs-lookup"><span data-stu-id="2f3b4-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="2f3b4-106">Deze bewerkingen zijn langlopend.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-106">These operations are long-running.</span></span>

<span data-ttu-id="2f3b4-107">Media Services .NET SDK biedt API's die de aanvraag verzendt en wacht totdat de bewerking is voltooid (intern maakt de API's zijn gedelegeerd voor het bewerkingsvoortgang op bepaalde tijden).</span><span class="sxs-lookup"><span data-stu-id="2f3b4-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="2f3b4-108">Bijvoorbeeld bij het aanroepen van kanaal. Start(), de methode retourneert nadat het kanaal is gestart.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="2f3b4-109">U kunt ook de asynchrone versie: wachten op een kanaal. StartAsync() (Zie voor meer informatie over de taakgebaseerde asynchrone patroon [tik](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="2f3b4-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="2f3b4-110">API's die een aanvraag verzendt en vervolgens poll-frequentie voor de status totdat de bewerking voltooid is, worden 'polling methoden' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="2f3b4-111">Deze methoden (met name de Async-versie) worden aanbevolen voor interactieve toepassingen en/of stateful services.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="2f3b4-112">Er zijn scenario's waarbij een toepassing niet kan wachten op een langdurige HTTP-verzoek en wil poll-frequentie voor de voortgang van de bewerking handmatig.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="2f3b4-113">Een typisch voorbeeld zou een browser interactie met een stateless webservice: als de browser aanvraagt een kanaal te maken, de webservice initieert een langdurige bewerking en retourneert de bewerkings-ID in de browser.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="2f3b4-114">De browser kan vervolgens vraagt u de web-service om op te halen van de status van de bewerking op basis van de-ID.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="2f3b4-115">Media Services .NET SDK biedt API's die handig voor dit scenario zijn.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="2f3b4-116">Deze API's worden 'niet polling methoden' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="2f3b4-117">'Niet polling methoden' hebben de volgende naamgevingspatroon: verzenden*OperationName*bewerking (bijvoorbeeld SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="2f3b4-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="2f3b4-118">Verzenden*OperationName*bewerking methoden retourneren de **IOperation** object; het geretourneerde object bevat informatie die kan worden gebruikt voor het bijhouden van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="2f3b4-119">De verzenden*OperationName*OperationAsync methoden retourneren **taak<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="2f3b4-120">Op dit moment wordt de volgende klassen ondersteuning voor methoden niet polling: **kanaal**, **StreamingEndpoint**, en **programma**.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="2f3b4-121">Om te controleren voor de status van de bewerking, gebruiken de **GetOperation** methode op de **OperationBaseCollection** klasse.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="2f3b4-122">Gebruik de volgende intervallen om te controleren van de bewerkingsstatus: voor **kanaal** en **StreamingEndpoint** bewerkingen, gebruikt u 30 seconden; voor **programma** bewerkingen, gebruik van 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2f3b4-123">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2f3b4-124">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2f3b4-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="2f3b4-125">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2f3b4-125">Example</span></span>

<span data-ttu-id="2f3b4-126">Het volgende voorbeeld definieert een klasse met de naam **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="2f3b4-127">De definitie van deze klasse kan een startpunt voor de klassedefinitie van uw web-service zijn.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="2f3b4-128">Voor eenvoud gebruik de volgende voorbeelden de versies niet asynchrone methoden.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="2f3b4-129">Het voorbeeld ziet ook hoe de client deze klasse zou kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f3b4-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="2f3b4-130">De klassendefinitie ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="2f3b4-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
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
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
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
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
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

### <a name="the-client-code"></a><span data-ttu-id="2f3b4-131">De clientcode</span><span class="sxs-lookup"><span data-stu-id="2f3b4-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="2f3b4-132">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="2f3b4-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2f3b4-133">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="2f3b4-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

