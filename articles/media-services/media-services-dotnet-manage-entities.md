---
title: aaaManaging activa en gerelateerde entiteiten met Media Services .NET SDK
description: Meer informatie over hoe toomanage activa en gerelateerde entiteiten met Hallo Media Services SDK voor .NET.
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
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Het beheer van bedrijfsmiddelen en gerelateerde entiteiten met mediaservices .NET SDK
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

Dit onderwerp wordt beschreven hoe toomanage Azure Media Services entiteiten met .NET. 

>[!NOTE]
> Vanaf 1 April 2017 worden elke record taak in uw account ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende records van de taak zelfs als Hallo kunt u het totale aantal records lager dan de maximumquotum Hallo is. Bijvoorbeeld: op 1 April 2017 elke record taak in uw account die ouder zijn dan 31 December 2016, worden automatisch verwijderd. Als u tooarchive Hallo projecttaak/informatie nodig hebt, kunt u Hallo-code in dit onderwerp beschreven.

## <a name="prerequisites"></a>Vereisten

Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Een verwijzing naar een activum ophalen
Een taak die vaak is tooget een verwijzing tooan van bestaande asset in Media Services. Hallo volgende codevoorbeeld ziet u hoe u krijgt een verwijzing naar een asset uit Hallo activa verzameling op Hallo server context-object, op basis van een asset-Id. Hallo volgende code wordt een Linq query tooget tooan bestaande IAsset referentieobject.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Lijst van alle activa
Zoals het aantal activa dat u in de opslag hebt Hallo groeit, is het handig toolist uw assets. Hallo volgende codevoorbeeld toont hoe tooiterate via Hallo activa verzameling op Hallo server context-object. Aan elke asset schrijft Hallo codevoorbeeld ook enkele van de eigenschap waarden toohello-console. Elk activum kan bijvoorbeeld veel mediabestanden bevatten. Hallo-codevoorbeeld schrijft alle bestanden die zijn gekoppeld aan elke asset.

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
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

Wanneer u met het verwerken van de taken in Media Services-code werkt, moet u vaak een verwijzing tooan bestaande taak op basis van een id Hallo volgende codevoorbeeld ziet u hoe een verwijzing tooan IJob tooget object uit de verzameling taken Hallo tooget.

U kunt tooget de verwijzing naar een taak moet bij het starten van de coderingstaak van een langlopende en moet toocheck Hallo taakstatus op een thread. In gevallen als volgt wanneer Hallo-methode vanuit een thread retourneert moet u een vernieuwd verwijzing tooa taak tooretrieve.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Lijst met taken en activa
Een belangrijke taak gerelateerde is toolist activa met de bijbehorende taken in Media Services. Hallo volgende voorbeeldcode laat zien u hoe toolist elk object IJob voor elke taak wordt vervolgens het eigenschappen over Hallo taak, alle gerelateerde taken, alle invoer activa en alle activa uitvoer. Hallo-code in dit voorbeeld kan handig zijn voor tal van andere opdrachten. Bijvoorbeeld, als u toolist Hallo uitvoer elementen uit een of meer codering taken die u eerder hebt uitgevoerd wilt, deze code laat zien hoe tooaccess Hallo activa uitvoer. Wanneer u een verwijzing tooan uitvoerasset hebt, kunt u vervolgens Hallo inhoud tooother gebruikers of toepassingen te downloaden of URL's naar ons leveren. 

Zie voor meer informatie over opties voor het leveren van assets [activa leveren met Media Services SDK voor .NET Hallo](media-services-deliver-streaming-content.md).

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
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

            // For each job, display hello list of input media assets.
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

            // For each job, display hello list of output media assets.
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
U kunt een toegangsbeleid definiëren op een actief of de bestanden in Media Services. Een toegangsbeleid definieert Hallo machtigingen voor een bestand of een asset (welk type toegang en Hallo duur). In uw code Media Services u doorgaans een toegangsbeleid definiëren door het maken van een object IAccessPolicy en vervolgens te koppelen aan een bestaande asset. Vervolgens maakt u een object ILocator, waarmee u directe toegang tooassets in Media Services te leveren. Hallo Visual Studio-project die wordt meegestuurd met deze reeks documentatie bevat enkele codevoorbeelden die laten zien hoe toocreate en toewijzen toegang beleid en locators tooassets tot.

Hallo van de volgende code voorbeeld ziet u hoe alle beleidsregels voor toegang op Hallo-server en toont Hallo type machtigingen die zijn gekoppeld aan elk toolist. Een andere handige manier tooview-beleid is toolist alle ILocator objecten op Hallo-server en vervolgens voor elke locator u kunt een lijst voor de bijbehorende toegangsbeleid met behulp van de eigenschap AccessPolicy.

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
> Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). 

Bijvoorbeeld, kunt u een algemene reeks beleidsregels Hello code die één keer kan alleen worden uitgevoerd in uw toepassing te volgen. U kunt zich aanmelden id's tooa logboekbestand voor later gebruik:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Vervolgens gebruikt u Hallo bestaande id's in uw code als volgt:

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Lijst van alle Locators
Een locator is een URL die een directe paden tooaccess een asset, samen met machtigingen toohello asset biedt zoals gedefinieerd door de bijbehorende toegangsbeleid Hallo-locator. Elke asset kan een verzameling ILocator objecten gekoppeld in de eigenschap Locators hebben. Hallo servercontext heeft ook een Locators-verzameling die alle locators bevat.

Hallo volgende codevoorbeeld geeft een lijst van alle locators op Hallo-server. Voor elke locator wordt Hallo Id voor Hallo gerelateerde asset en -beleid. Hallo type machtigingen, Hallo vervaldatum en Hallo volledig pad toohello asset worden ook weergegeven.

Houd er rekening mee dat een locator pad tooan actief is alleen een base URL toohello actief. toocreate die een directe paden tooindividual waarin een gebruiker of toepassing naar bladeren kan bestanden, moet uw code Hallo specifieke pad toohello locator bestandspad toevoegen. Voor meer informatie over het toodo deze, Zie Hallo onderwerp [activa leveren met Media Services SDK voor .NET Hallo](media-services-deliver-streaming-content.md).

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
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Door grote verzamelingen van entiteiten opsommen
Tijdens het opvragen van entiteiten, moet u er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten resultaten too1000 beperkt is. U moet de toouse overslaan en nemen bij het opsommen van via grote verzamelingen van entiteiten. 

Hallo functie lussen via alle Hallo taken in Media Services-Account opgegeven hello te volgen. Media Services retourneert 1000 taken in de verzameling taken. Hallo-functie maakt gebruik van overslaan en toomake zeker die alle taken worden geïnventariseerd (als u meer dan 1000 taken in uw account hebt).

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
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
Hallo volgende voorbeeld wordt een asset verwijderd.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Een taak verwijderen
een taak toodelete, moet u Hallo status van taak Hallo zoals aangegeven in de eigenschap State Hallo controleren. Taken die zijn voltooid of geannuleerd kunnen worden verwijderd terwijl de taken die zich in een bepaalde status, zoals in de wachtrij, geplande of verwerking, moeten eerst worden geannuleerd, en vervolgens kunnen worden verwijderd.

Hallo toont volgende codevoorbeeld een methode voor het verwijderen van een taak met taakstatussen controleren en vervolgens te verwijderen wanneer het Hallo-status is voltooid of geannuleerd. Deze code is afhankelijk van de vorige sectie Hallo in dit onderwerp voor het ophalen van een verwijzing tooa taak: de taakverwijzing van een ophalen.

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
                    // You can also call job.DeleteAsync toodo async deletes.
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
Hallo volgende voorbeeldcode laat zien hoe tooget een verwijzing tooan-beleid op basis van een beleids-Id en toodelete Hallo beleid.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
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

