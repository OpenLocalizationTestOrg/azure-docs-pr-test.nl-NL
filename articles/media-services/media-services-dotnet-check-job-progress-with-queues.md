---
title: Azure Queue storage gebruiken voor het bewaken van Media Services taak meldingen met .NET | Microsoft Docs
description: Informatie over het Azure Queue storage gebruiken voor het bewaken van meldingen voor Media Services-taak. Het codevoorbeeld is geschreven in C# en maakt gebruik van de Media Services SDK voor .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="9b1d3-104">Azure Queue storage gebruiken voor het bewaken van Media Services taak meldingen met .NET</span><span class="sxs-lookup"><span data-stu-id="9b1d3-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="9b1d3-105">Wanneer u een codering taken uitvoert, moet u vaak een manier om de voortgang van de taak volgen.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-105">When you run encoding jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="9b1d3-106">U kunt Media Services voor het leveren van meldingen configureren [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-106">You can configure Media Services to deliver notifications to [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="9b1d3-107">U kunt de voortgang taak bewaken door meldingen ophalen uit de wachtrij-opslag.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-107">You can monitor job progress by getting notifications from the Queue storage.</span></span> 

<span data-ttu-id="9b1d3-108">Berichten in wachtrij opslag toegankelijk zijn vanuit overal ter wereld.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-108">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="9b1d3-109">De messaging opslagarchitectuur van de wachtrij is betrouwbaar en zeer schaalbaar.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-109">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="9b1d3-110">Queue storage voor berichten polling wordt aanbevolen ten opzichte van andere methoden.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="9b1d3-111">Een gebruikelijk scenario om te luisteren op Media Services-meldingen is dat als u ontwikkelt een inhoudsbeheersysteem die nodig zijn voor een aantal extra taak na een codeertaak is voltooid (bijvoorbeeld voor het activeren van de volgende stap in een werkstroom of voor het publiceren van inhoud).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-111">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

<span data-ttu-id="9b1d3-112">Dit onderwerp leest hoe u meldingen van Queue storage.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-112">This topic shows how to get notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="9b1d3-113">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="9b1d3-113">Considerations</span></span>
<span data-ttu-id="9b1d3-114">Overweeg het volgende bij het ontwikkelen van Media Services-toepassingen die gebruikmaken van Queue storage:</span><span class="sxs-lookup"><span data-stu-id="9b1d3-114">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="9b1d3-115">Queue storage biedt geen garantie van first in first out (FIFO) besteld levering.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="9b1d3-116">Zie voor meer informatie [wachtrijen in Azure en Azure Service Bus-wachtrijen vergeleken en Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="9b1d3-117">Wachtrij-opslag is niet een pushservice.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-117">Queue storage is not a push service.</span></span> <span data-ttu-id="9b1d3-118">U hebt voor het pollen van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-118">You have to poll the queue.</span></span>
* <span data-ttu-id="9b1d3-119">U kunt een onbeperkt aantal wachtrijen hebben.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-119">You can have any number of queues.</span></span> <span data-ttu-id="9b1d3-120">Zie voor meer informatie [REST-API van wachtrij](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="9b1d3-121">Queue storage heeft enkele beperkingen en foutopsporingsgegevens moet houden.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-121">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="9b1d3-122">Deze worden beschreven in [wachtrijen in Azure en Azure Service Bus-wachtrijen vergeleken en Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="9b1d3-123">.NET-codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="9b1d3-123">.NET code example</span></span>

<span data-ttu-id="9b1d3-124">Het voorbeeld in deze sectie doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="9b1d3-124">The code example in this section does the following:</span></span>

1. <span data-ttu-id="9b1d3-125">Definieert de **EncodingJobMessage** klasse die is toegewezen aan de berichtindeling melding.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-125">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="9b1d3-126">De code deserializes berichten ontvangen uit de wachtrij in objecten van de **EncodingJobMessage** type.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-126">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="9b1d3-127">Laadt de accountgegevens Media Services en opslag van het bestand app.config.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-127">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="9b1d3-128">In het voorbeeld gebruikt deze informatie voor het maken van de **CloudMediaContext** en **CloudQueue** objecten.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-128">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="9b1d3-129">Hiermee maakt u de wachtrij die meldingen over de coderingstaak ontvangt.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-129">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="9b1d3-130">Het eindpunt van de melding die is toegewezen aan de wachtrij maakt.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-130">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="9b1d3-131">Het eindpunt van de melding is gekoppeld aan de taak en de coderingstaak worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-131">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="9b1d3-132">U kunt meerdere melding eindpunten die zijn gekoppeld aan een taak hebben.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-132">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="9b1d3-133">Geeft **NotificationJobState.FinalStatesOnly** naar de **AddNew** methode.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-133">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="9b1d3-134">(In dit voorbeeld wordt alleen geïnteresseerd bent in laatste status van de verwerking van een taak.)</span><span class="sxs-lookup"><span data-stu-id="9b1d3-134">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="9b1d3-135">Als u doorgeeft **NotificationJobState.All**, krijgt u de volgende status wijzigingsmeldingen: in de wachtrij, geplande, verwerken en is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-135">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="9b1d3-136">Echter, zoals eerder opgemerkt, Queue storage biedt geen garantie levering.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="9b1d3-137">Op volgorde van berichten, gebruikt u de **tijdstempel** eigenschap (gedefinieerd op de **EncodingJobMessage** type in het onderstaande voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-137">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="9b1d3-138">Dubbele berichten zijn mogelijk.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-138">Duplicate messages are possible.</span></span> <span data-ttu-id="9b1d3-139">Gebruiken om te controleren voor duplicaten, de **ETag-eigenschap** (gedefinieerd op de **EncodingJobMessage** type).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-139">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="9b1d3-140">Het is ook mogelijk dat sommige wijzigingsmeldingen status ophalen overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="9b1d3-141">Wacht totdat de taak de status voltooid ophalen door het controleren van de wachtrij elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-141">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="9b1d3-142">Hiermee verwijdert u berichten nadat ze zijn verwerkt.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="9b1d3-143">Hiermee verwijdert u de wachtrij en het eindpunt van de melding.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-143">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1d3-144">De aanbevolen manier om het bewaken van een taak is door te luisteren naar meldingsberichten, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-144">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="9b1d3-145">U kunt ook u op de status van een taak kan controleren met behulp van de **IJob.State** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-145">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="9b1d3-146">Op een melding over een taak is voltooid voordat de status kan binnenkomen **IJob** is ingesteld op **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-146">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="9b1d3-147">De **IJob.State** eigenschap weerspiegelt de status van de nauwkeurige met een kleine vertraging.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-147">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9b1d3-148">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="9b1d3-149">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9b1d3-149">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="9b1d3-150">Maak een nieuwe map (deze kan overal op uw lokaal station zijn opgeslagen) en kopieer een MP4-bestand dat u wilt coderen en streamen of progressief wilt downloaden.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="9b1d3-151">In dit voorbeeld wordt het pad 'C:\Media' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-151">In this example, the "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="9b1d3-152">Code</span><span class="sxs-lookup"><span data-stu-id="9b1d3-152">Code</span></span>

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want to get messages from the queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display the message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete the message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
<span data-ttu-id="9b1d3-153">Het vorige voorbeeld is de volgende uitvoer geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-153">The preceding example produced the following output.</span></span> <span data-ttu-id="9b1d3-154">De waarden variëren.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-154">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="9b1d3-155">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="9b1d3-155">Next step</span></span>
<span data-ttu-id="9b1d3-156">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="9b1d3-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b1d3-157">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="9b1d3-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
