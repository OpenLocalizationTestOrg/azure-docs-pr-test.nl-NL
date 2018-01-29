---
title: Het beheer van bedrijfsmiddelen en gerelateerde entiteiten met mediaservices .NET SDK
description: Informatie over het beheren van activa en gerelateerde entiteiten met het Media Services SDK voor .NET.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 5efe16a09808267d0797521f9e1df2b60aec9cbb
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/21/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Het beheer van bedrijfsmiddelen en gerelateerde entiteiten met mediaservices .NET SDK
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

Dit onderwerp leest hoe voor het beheren van Azure Media Services-entiteiten met .NET. 

>[!NOTE]
> Vanaf 1 april 2017 wordt elke taakrecord in uw account die ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende onderliggende taakrecords, zelfs als het totale aantal records lager is dan het maximale quotum. Bijvoorbeeld: op 1 April 2017 elke record taak in uw account die ouder zijn dan 31 December 2016, worden automatisch verwijderd. Als u nodig hebt bij de archivering van gegevens van de taak/taak, kunt u de code in dit onderwerp beschreven.

## <a name="prerequisites"></a>Vereisten

Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Een verwijzing naar een activum ophalen
Een taak die vaak is een verwijzing naar een bestaand activum ophalen in Media Services. De volgende voorbeeldcode laat zien hoe u krijgt een verwijzing naar een asset uit de verzameling activa op de server context-object op basis van een asset-id. Het volgende codevoorbeeld maakt gebruik van een Linq-query verwijst naar een bestaand IAsset-object.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query to get an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference the asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Lijst van alle activa
Wanneer het aantal activa dat u in de opslag hebt groeit, is het handig zijn voor een lijst met uw assets. De volgende voorbeeldcode laat zien hoe u doorloopt de verzameling activa op de server-context-object. Aan elke asset schrijft in het voorbeeld ook sommige van de eigenschapswaarden in de console. Elk activum kan bijvoorbeeld veel mediabestanden bevatten. Alle bestanden die zijn gekoppeld aan elke asset schrijft het codevoorbeeld.

    static void ListAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display the collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display the files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a>De taakverwijzing van een ophalen

Wanneer u met het verwerken van de taken in Media Services-code werkt, moet u vaak geen verwijzing ophalen naar een bestaande taak op basis van een id. De volgende voorbeeldcode laat zien hoe een verwijzing naar een object IJob uit de verzameling taken ophalen.

Mogelijk moet u de taakverwijzing van een ophalen bij het starten van de coderingstaak van een langlopende en moet de status van de taak op een thread controleren. Wanneer de methode vanuit een thread retourneert in gevallen als volgt moet u een vernieuwd verwijzing naar een taak ophalen.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query to get an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return the job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Lijst met taken en activa
Een belangrijke taak gerelateerd is aan de lijst met activa met de bijbehorende taken in Media Services. Het volgende codevoorbeeld ziet u hoe u elk object IJob en vervolgens voor elke taak eigenschappen van de taak wordt weergegeven, alle gerelateerde taken, alle invoer-activa en alle uitvoer activa. De code in dit voorbeeld kan handig zijn voor tal van andere opdrachten. Als u weergeven van de activa van de uitvoer van een of meer codering taken die u eerder hebt uitgevoerd wilt, ziet deze code u bijvoorbeeld toegang tot de activa uitvoer. Wanneer u een verwijzing naar een uitvoerasset hebt, kunt u vervolgens de inhoud leveren aan andere gebruikers of toepassingen door downloaden of URL's bieden. 

Zie voor meer informatie over opties voor het leveren van assets [activa leveren met de Media Services SDK voor .NET](media-services-deliver-streaming-content.md).

    // List all jobs on the server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display the collection of jobs on the server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display the associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display the list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display the list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a>Lijst van alle beleidsregels voor toegang
U kunt een toegangsbeleid definiëren op een actief of de bestanden in Media Services. Een toegangsbeleid definieert de machtigingen voor een bestand of een asset (welk type toegang en de duur van). In uw code Media Services u doorgaans een toegangsbeleid definiëren door het maken van een object IAccessPolicy en vervolgens te koppelen aan een bestaande asset. Vervolgens maakt u een object ILocator, waarmee u voorzien in directe toegang tot de activa in een Media Services. De Visual Studio-project die wordt meegestuurd met deze reeks documentatie bevat enkele codevoorbeelden die het maken en toegangsbeleid en locators toewijzen aan activa weergeven.

De volgende voorbeeldcode laat zien hoe u een lijst van alle beleidsregels voor toegang op de server en geeft het type van de machtigingen die zijn gekoppeld aan elk. Een andere handige manier om weer te geven toegangsbeleid is voor een lijst met alle ILocator objecten op de server en vervolgens voor elke locator u kunt een lijst voor de bijbehorende toegangsbeleid met behulp van de eigenschap AccessPolicy.

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a>Limiet-beleid 

>[!NOTE]
> Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). U moet dezelfde beleids-id gebruiken als u altijd dezelfde dagen/toegangsmachtigingen gebruikt, bijvoorbeeld beleidsregels voor locators die zijn bedoeld om gedurende een lange periode gehandhaafd te blijven (niet-upload-beleidsregels). 

U kunt bijvoorbeeld een algemene reeks beleidsregels maken met de volgende code die één keer kan alleen worden uitgevoerd in uw toepassing. U kunt de id's in een logboekbestand voor later gebruik vastleggen:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Vervolgens gebruikt u de bestaande id's in uw code als volgt:

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get the standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get the existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("The locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Lijst van alle Locators
Een locator is een URL die een directe pad voor toegang tot een asset, samen met machtigingen voor de activa zoals gedefinieerd door de locator gekoppeld toegangsbeleid. Elke asset kan een verzameling ILocator objecten gekoppeld in de eigenschap Locators hebben. De servercontext heeft ook een Locators-verzameling die alle locators bevat.

Het volgende codevoorbeeld geeft een lijst van alle locators op de server. Voor elke locator wordt de Id voor de beleidsregel asset en toegang. Het type van machtigingen, de vervaldatum en het volledige pad wordt weergegeven voor de activa.

Houd er rekening mee dat een locator-pad naar een asset alleen een basis-URL voor de activa is. Voor het maken van een pad naar de afzonderlijke bestanden die een gebruiker of toepassing u naar bladert kan moet uw code het specifieke bestandspad toevoegen aan het locator-pad. Zie het onderwerp voor meer informatie over hoe u dit doet, [activa leveren met de Media Services SDK voor .NET](media-services-deliver-streaming-content.md).

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // The locator path is the base or parent path (with included permissions) to access  
            // the media content of an asset. To create a full URL to a specific media file, take 
            // the locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Door grote verzamelingen van entiteiten opsommen
Tijdens het opvragen van entiteiten, is er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten tot 1000 resultaten beperkt. U moet gebruiken overslaan en nemen bij het opsommen van via grote verzamelingen van entiteiten. 

De volgende functie doorlopen van de taken in de opgegeven Media Services-Account. Media Services retourneert 1000 taken in de verzameling taken. De functie maakt gebruik van overslaan en nemen om ervoor te zorgen dat alle taken die worden geïnventariseerd (als u meer dan 1000 taken in uw account hebt).

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in the Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a>Een activum verwijderen
Het volgende voorbeeld wordt een asset.

    static void DeleteAsset( IAsset asset)
    {
        // delete the asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted the Asset");

    }

## <a name="delete-a-job"></a>Een taak verwijderen
Als u wilt verwijderen van een taak, moet u de status van de taak controleren, zoals aangegeven in de eigenschap State. Taken die zijn voltooid of geannuleerd kunnen worden verwijderd terwijl de taken die zich in een bepaalde status, zoals in de wachtrij, geplande of verwerking, moeten eerst worden geannuleerd, en vervolgens kunnen worden verwijderd.

Het volgende codevoorbeeld toont een methode voor het verwijderen van een taak met taakstatussen controleren en vervolgens te verwijderen wanneer de status is voltooid of geannuleerd. Deze code is afhankelijk van de vorige sectie in dit onderwerp voor het ophalen van een verwijzing naar een taak: de taakverwijzing van een ophalen.

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync to do async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a>Verwijderen van toegangsbeleid instellen
De volgende voorbeeldcode laat zien hoe een verwijzing naar een toegangsbeleid op basis van een beleid voor Id, en vervolgens verwijdert u het beleid.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // To delete a specific access policy, get a reference to the policy.  
        // based on the policy Id passed to the method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

