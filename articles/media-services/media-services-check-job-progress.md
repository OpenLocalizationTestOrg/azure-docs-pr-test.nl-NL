---
title: De voortgang van de taak bewaken met .NET
description: Informatie over het gebruik van gebeurtenis-handlercode te taak voortgang volgen en statusupdates. Het codevoorbeeld is geschreven in C# en maakt gebruik van de Media Services SDK voor .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee720ed6-8ce5-4434-b6d6-4df71fca224e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 851981b291115ba31dc40535f8bcc71cdb475717
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="8794f-104">De voortgang van de taak bewaken met .NET</span><span class="sxs-lookup"><span data-stu-id="8794f-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8794f-105">Portal</span><span class="sxs-lookup"><span data-stu-id="8794f-105">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="8794f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="8794f-106">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="8794f-107">REST</span><span class="sxs-lookup"><span data-stu-id="8794f-107">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="8794f-108">Wanneer u taken uitvoert, moet u vaak een manier om de voortgang van de taak volgen.</span><span class="sxs-lookup"><span data-stu-id="8794f-108">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="8794f-109">U kunt de voortgang controleren door het definiëren van een gebeurtenis-handler StateChanged (zoals beschreven in dit onderwerp) of Azure Queue storage gebruiken om te controleren van Media Services taak meldingen (zoals beschreven in [dit](media-services-dotnet-check-job-progress-with-queues.md) onderwerp).</span><span class="sxs-lookup"><span data-stu-id="8794f-109">You can check the progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage to monitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-to-monitor-job-progress"></a><span data-ttu-id="8794f-110">Gebeurtenis-handler om de voortgang taak StateChanged definiëren</span><span class="sxs-lookup"><span data-stu-id="8794f-110">Define StateChanged event handler to monitor job progress</span></span>
<span data-ttu-id="8794f-111">Het volgende voorbeeld definieert de StateChanged gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="8794f-111">The following code example defines the StateChanged event handler.</span></span> <span data-ttu-id="8794f-112">Deze gebeurtenis-handler houdt de voortgang van de taak en bevat informatie over bijgewerkte status, afhankelijk van de status.</span><span class="sxs-lookup"><span data-stu-id="8794f-112">This event handler tracks job progress and provides updated status, depending on the state.</span></span> <span data-ttu-id="8794f-113">De code definieert ook de methode LogJobStop.</span><span class="sxs-lookup"><span data-stu-id="8794f-113">The code also defines the LogJobStop method.</span></span> <span data-ttu-id="8794f-114">Deze Help-methode logboeken foutgegevens.</span><span class="sxs-lookup"><span data-stu-id="8794f-114">This helper method logs error details.</span></span>

    private static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);

        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("********************");
                Console.WriteLine("Job is finished.");
                Console.WriteLine("Please wait while local tasks or downloads complete...");
                Console.WriteLine("********************");
                Console.WriteLine();
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                LogJobStop(job.Id);
                break;
            default:
                break;
        }
    }

    private static void LogJobStop(string jobId)
    {
        StringBuilder builder = new StringBuilder();
        IJob job = GetJob(jobId);

        builder.AppendLine("\nThe job stopped due to cancellation or an error.");
        builder.AppendLine("***************************");
        builder.AppendLine("Job ID: " + job.Id);
        builder.AppendLine("Job Name: " + job.Name);
        builder.AppendLine("Job State: " + job.State.ToString());
        builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
        builder.AppendLine("Media Services account name: " + _accountName);
        builder.AppendLine("Media Services account location: " + _accountLocation);
        // Log job errors if they exist.  
        if (job.State == JobState.Error)
        {
            builder.Append("Error Details: \n");
            foreach (ITask task in job.Tasks)
            {
                foreach (ErrorDetail detail in task.ErrorDetails)
                {
                    builder.AppendLine("  Task Id: " + task.Id);
                    builder.AppendLine("    Error Code: " + detail.Code);
                    builder.AppendLine("    Error Message: " + detail.Message + "\n");
                }
            }
        }
        builder.AppendLine("***************************\n");
        // Write the output to a local file and to the console. The template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="8794f-115">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="8794f-115">Next step</span></span>
<span data-ttu-id="8794f-116">Media Services-leertrajecten bekijken.</span><span class="sxs-lookup"><span data-stu-id="8794f-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8794f-117">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="8794f-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

