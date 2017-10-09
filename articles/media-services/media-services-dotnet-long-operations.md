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
# <a name="delivering-live-streaming-with-azure-media-services"></a>Live streamen met Azure mediaservices leveren

## <a name="overview"></a>Overzicht

Microsoft Azure Media Services biedt API's die aanvragen tooMedia Services toostart bewerkingen verzenden (bijvoorbeeld: maken, starten, stoppen of verwijderen van een kanaal). Deze bewerkingen zijn langlopend.

Hallo Media Services .NET SDK biedt API's die Hallo aanvraag verzenden en te wachten op Hallo bewerking toocomplete (intern hello API's zijn gedelegeerd voor bewerking uitgevoerd met een bepaalde interval). Bijvoorbeeld bij het aanroepen van kanaal. Start(), Hallo-methode retourneert nadat Hallo-kanaal is gestart. U kunt ook de asynchrone versie hello gebruiken: wachten op een kanaal. StartAsync() (Zie voor meer informatie over de taakgebaseerde asynchrone patroon [tik](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). API's die een aanvraag verzendt en vervolgens poll-frequentie voor Hallo status totdat het Hallo-bewerking is voltooid, worden 'polling methoden' genoemd. Deze methoden (met name Hallo asynchrone versie) worden aanbevolen voor interactieve toepassingen en/of stateful services.

Er zijn scenario's waarbij een toepassing niet kan wachten op een langdurige http-aanvraag en toopoll handmatig wil voor Hallo bewerking uitgevoerd. Een typisch voorbeeld zou een browser interactie met een stateless webservice: als Hallo browser aanvraagt toocreate een kanaal, Hallo webservice initieert een langdurige bewerking retourneert Hallo bewerking-ID toohello browser. Hallo browser kan vervolgens vraagt u Hallo web service tooget Hallo bewerkingsstatus op basis van het Hallo-ID. Hallo Media Services .NET SDK biedt API's die handig voor dit scenario zijn. Deze API's worden 'niet polling methoden' genoemd.
Hallo ' niet polling methoden' hebben Hallo volgende naamgevingspatroon: verzenden*OperationName*bewerking (bijvoorbeeld SendCreateOperation). Verzenden*OperationName*bewerking methoden retourneren Hallo **IOperation** object; hello geretourneerde object bevat informatie die gebruikt tootrack Hallo-bewerking worden kan. Hallo verzenden*OperationName*OperationAsync methoden retourneren **taak<IOperation>**.

Op dit moment Hallo volgende klassen ondersteuning niet polling methoden: **kanaal**, **StreamingEndpoint**, en **programma**.

toopoll voor bewerkingsstatus hello, gebruik Hallo **GetOperation** methode op Hallo **OperationBaseCollection** klasse. Hallo intervallen toocheck Hallo bewerkingsstatus volgende gebruiken: voor **kanaal** en **StreamingEndpoint** bewerkingen, gebruikt u 30 seconden; voor **programma** bewerkingen, gebruikmaken van 10 seconden.

## <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.

Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld definieert een klasse met de naam **ChannelOperations**. De definitie van deze klasse kan een startpunt voor de klassedefinitie van uw web-service zijn. Eenvoud gebruik hello volgende voorbeelden voor Hallo niet asynchrone versies van methoden.

Hallo-voorbeeld ziet u ook hoe deze klasse in Hallo-client kunnen worden gebruikt.

### <a name="channeloperations-class-definition"></a>De klassendefinitie ChannelOperations

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

### <a name="hello-client-code"></a>Hallo-clientcode
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



## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

