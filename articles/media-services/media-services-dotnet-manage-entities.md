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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="c4e09-103">Het beheer van bedrijfsmiddelen en gerelateerde entiteiten met mediaservices .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c4e09-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4e09-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c4e09-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="c4e09-105">REST</span><span class="sxs-lookup"><span data-stu-id="c4e09-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="c4e09-106">Dit onderwerp wordt beschreven hoe toomanage Azure Media Services entiteiten met .NET.</span><span class="sxs-lookup"><span data-stu-id="c4e09-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="c4e09-107">Vanaf 1 April 2017 worden elke record taak in uw account ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende records van de taak zelfs als Hallo kunt u het totale aantal records lager dan de maximumquotum Hallo is.</span><span class="sxs-lookup"><span data-stu-id="c4e09-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="c4e09-108">Bijvoorbeeld: op 1 April 2017 elke record taak in uw account die ouder zijn dan 31 December 2016, worden automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4e09-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="c4e09-109">Als u tooarchive Hallo projecttaak/informatie nodig hebt, kunt u Hallo-code in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="c4e09-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4e09-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c4e09-110">Prerequisites</span></span>

<span data-ttu-id="c4e09-111">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c4e09-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="c4e09-112">Een verwijzing naar een activum ophalen</span><span class="sxs-lookup"><span data-stu-id="c4e09-112">Get an Asset Reference</span></span>
<span data-ttu-id="c4e09-113">Een taak die vaak is tooget een verwijzing tooan van bestaande asset in Media Services.</span><span class="sxs-lookup"><span data-stu-id="c4e09-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="c4e09-114">Hallo volgende codevoorbeeld ziet u hoe u krijgt een verwijzing naar een asset uit Hallo activa verzameling op Hallo server context-object, op basis van een asset-Id. Hallo volgende code wordt een Linq query tooget tooan bestaande IAsset referentieobject.</span><span class="sxs-lookup"><span data-stu-id="c4e09-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

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

## <a name="list-all-assets"></a><span data-ttu-id="c4e09-115">Lijst van alle activa</span><span class="sxs-lookup"><span data-stu-id="c4e09-115">List All Assets</span></span>
<span data-ttu-id="c4e09-116">Zoals het aantal activa dat u in de opslag hebt Hallo groeit, is het handig toolist uw assets.</span><span class="sxs-lookup"><span data-stu-id="c4e09-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="c4e09-117">Hallo volgende codevoorbeeld toont hoe tooiterate via Hallo activa verzameling op Hallo server context-object.</span><span class="sxs-lookup"><span data-stu-id="c4e09-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="c4e09-118">Aan elke asset schrijft Hallo codevoorbeeld ook enkele van de eigenschap waarden toohello-console.</span><span class="sxs-lookup"><span data-stu-id="c4e09-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="c4e09-119">Elk activum kan bijvoorbeeld veel mediabestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4e09-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="c4e09-120">Hallo-codevoorbeeld schrijft alle bestanden die zijn gekoppeld aan elke asset.</span><span class="sxs-lookup"><span data-stu-id="c4e09-120">hello code example writes out all files associated with each asset.</span></span>

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

## <a name="get-a-job-reference"></a><span data-ttu-id="c4e09-121">De taakverwijzing van een ophalen</span><span class="sxs-lookup"><span data-stu-id="c4e09-121">Get a Job Reference</span></span>

<span data-ttu-id="c4e09-122">Wanneer u met het verwerken van de taken in Media Services-code werkt, moet u vaak een verwijzing tooan bestaande taak op basis van een id Hallo volgende codevoorbeeld ziet u hoe een verwijzing tooan IJob tooget object uit de verzameling taken Hallo tooget.</span><span class="sxs-lookup"><span data-stu-id="c4e09-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="c4e09-123">U kunt tooget de verwijzing naar een taak moet bij het starten van de coderingstaak van een langlopende en moet toocheck Hallo taakstatus op een thread.</span><span class="sxs-lookup"><span data-stu-id="c4e09-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="c4e09-124">In gevallen als volgt wanneer Hallo-methode vanuit een thread retourneert moet u een vernieuwd verwijzing tooa taak tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="c4e09-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

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

## <a name="list-jobs-and-assets"></a><span data-ttu-id="c4e09-125">Lijst met taken en activa</span><span class="sxs-lookup"><span data-stu-id="c4e09-125">List Jobs and Assets</span></span>
<span data-ttu-id="c4e09-126">Een belangrijke taak gerelateerde is toolist activa met de bijbehorende taken in Media Services.</span><span class="sxs-lookup"><span data-stu-id="c4e09-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="c4e09-127">Hallo volgende voorbeeldcode laat zien u hoe toolist elk object IJob voor elke taak wordt vervolgens het eigenschappen over Hallo taak, alle gerelateerde taken, alle invoer activa en alle activa uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4e09-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="c4e09-128">Hallo-code in dit voorbeeld kan handig zijn voor tal van andere opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c4e09-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="c4e09-129">Bijvoorbeeld, als u toolist Hallo uitvoer elementen uit een of meer codering taken die u eerder hebt uitgevoerd wilt, deze code laat zien hoe tooaccess Hallo activa uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4e09-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="c4e09-130">Wanneer u een verwijzing tooan uitvoerasset hebt, kunt u vervolgens Hallo inhoud tooother gebruikers of toepassingen te downloaden of URL's naar ons leveren.</span><span class="sxs-lookup"><span data-stu-id="c4e09-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="c4e09-131">Zie voor meer informatie over opties voor het leveren van assets [activa leveren met Media Services SDK voor .NET Hallo](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="c4e09-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="list-all-access-policies"></a><span data-ttu-id="c4e09-132">Lijst van alle beleidsregels voor toegang</span><span class="sxs-lookup"><span data-stu-id="c4e09-132">List all Access Policies</span></span>
<span data-ttu-id="c4e09-133">U kunt een toegangsbeleid definiëren op een actief of de bestanden in Media Services.</span><span class="sxs-lookup"><span data-stu-id="c4e09-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="c4e09-134">Een toegangsbeleid definieert Hallo machtigingen voor een bestand of een asset (welk type toegang en Hallo duur).</span><span class="sxs-lookup"><span data-stu-id="c4e09-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="c4e09-135">In uw code Media Services u doorgaans een toegangsbeleid definiëren door het maken van een object IAccessPolicy en vervolgens te koppelen aan een bestaande asset.</span><span class="sxs-lookup"><span data-stu-id="c4e09-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="c4e09-136">Vervolgens maakt u een object ILocator, waarmee u directe toegang tooassets in Media Services te leveren.</span><span class="sxs-lookup"><span data-stu-id="c4e09-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="c4e09-137">Hallo Visual Studio-project die wordt meegestuurd met deze reeks documentatie bevat enkele codevoorbeelden die laten zien hoe toocreate en toewijzen toegang beleid en locators tooassets tot.</span><span class="sxs-lookup"><span data-stu-id="c4e09-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="c4e09-138">Hallo van de volgende code voorbeeld ziet u hoe alle beleidsregels voor toegang op Hallo-server en toont Hallo type machtigingen die zijn gekoppeld aan elk toolist.</span><span class="sxs-lookup"><span data-stu-id="c4e09-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="c4e09-139">Een andere handige manier tooview-beleid is toolist alle ILocator objecten op Hallo-server en vervolgens voor elke locator u kunt een lijst voor de bijbehorende toegangsbeleid met behulp van de eigenschap AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="c4e09-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="c4e09-140">Limiet-beleid</span><span class="sxs-lookup"><span data-stu-id="c4e09-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="c4e09-141">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="c4e09-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="c4e09-142">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="c4e09-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="c4e09-143">Bijvoorbeeld, kunt u een algemene reeks beleidsregels Hello code die één keer kan alleen worden uitgevoerd in uw toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="c4e09-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="c4e09-144">U kunt zich aanmelden id's tooa logboekbestand voor later gebruik:</span><span class="sxs-lookup"><span data-stu-id="c4e09-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="c4e09-145">Vervolgens gebruikt u Hallo bestaande id's in uw code als volgt:</span><span class="sxs-lookup"><span data-stu-id="c4e09-145">Then, you can use hello existing IDs in your code like this:</span></span>

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

## <a name="list-all-locators"></a><span data-ttu-id="c4e09-146">Lijst van alle Locators</span><span class="sxs-lookup"><span data-stu-id="c4e09-146">List All Locators</span></span>
<span data-ttu-id="c4e09-147">Een locator is een URL die een directe paden tooaccess een asset, samen met machtigingen toohello asset biedt zoals gedefinieerd door de bijbehorende toegangsbeleid Hallo-locator.</span><span class="sxs-lookup"><span data-stu-id="c4e09-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="c4e09-148">Elke asset kan een verzameling ILocator objecten gekoppeld in de eigenschap Locators hebben.</span><span class="sxs-lookup"><span data-stu-id="c4e09-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="c4e09-149">Hallo servercontext heeft ook een Locators-verzameling die alle locators bevat.</span><span class="sxs-lookup"><span data-stu-id="c4e09-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="c4e09-150">Hallo volgende codevoorbeeld geeft een lijst van alle locators op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="c4e09-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="c4e09-151">Voor elke locator wordt Hallo Id voor Hallo gerelateerde asset en -beleid.</span><span class="sxs-lookup"><span data-stu-id="c4e09-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="c4e09-152">Hallo type machtigingen, Hallo vervaldatum en Hallo volledig pad toohello asset worden ook weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4e09-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="c4e09-153">Houd er rekening mee dat een locator pad tooan actief is alleen een base URL toohello actief.</span><span class="sxs-lookup"><span data-stu-id="c4e09-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="c4e09-154">toocreate die een directe paden tooindividual waarin een gebruiker of toepassing naar bladeren kan bestanden, moet uw code Hallo specifieke pad toohello locator bestandspad toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c4e09-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="c4e09-155">Voor meer informatie over het toodo deze, Zie Hallo onderwerp [activa leveren met Media Services SDK voor .NET Hallo](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="c4e09-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="c4e09-156">Door grote verzamelingen van entiteiten opsommen</span><span class="sxs-lookup"><span data-stu-id="c4e09-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="c4e09-157">Tijdens het opvragen van entiteiten, moet u er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten resultaten too1000 beperkt is.</span><span class="sxs-lookup"><span data-stu-id="c4e09-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="c4e09-158">U moet de toouse overslaan en nemen bij het opsommen van via grote verzamelingen van entiteiten.</span><span class="sxs-lookup"><span data-stu-id="c4e09-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="c4e09-159">Hallo functie lussen via alle Hallo taken in Media Services-Account opgegeven hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="c4e09-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="c4e09-160">Media Services retourneert 1000 taken in de verzameling taken.</span><span class="sxs-lookup"><span data-stu-id="c4e09-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="c4e09-161">Hallo-functie maakt gebruik van overslaan en toomake zeker die alle taken worden geïnventariseerd (als u meer dan 1000 taken in uw account hebt).</span><span class="sxs-lookup"><span data-stu-id="c4e09-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

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

## <a name="delete-an-asset"></a><span data-ttu-id="c4e09-162">Een activum verwijderen</span><span class="sxs-lookup"><span data-stu-id="c4e09-162">Delete an Asset</span></span>
<span data-ttu-id="c4e09-163">Hallo volgende voorbeeld wordt een asset verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4e09-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="c4e09-164">Een taak verwijderen</span><span class="sxs-lookup"><span data-stu-id="c4e09-164">Delete a Job</span></span>
<span data-ttu-id="c4e09-165">een taak toodelete, moet u Hallo status van taak Hallo zoals aangegeven in de eigenschap State Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="c4e09-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="c4e09-166">Taken die zijn voltooid of geannuleerd kunnen worden verwijderd terwijl de taken die zich in een bepaalde status, zoals in de wachtrij, geplande of verwerking, moeten eerst worden geannuleerd, en vervolgens kunnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4e09-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="c4e09-167">Hallo toont volgende codevoorbeeld een methode voor het verwijderen van een taak met taakstatussen controleren en vervolgens te verwijderen wanneer het Hallo-status is voltooid of geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="c4e09-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="c4e09-168">Deze code is afhankelijk van de vorige sectie Hallo in dit onderwerp voor het ophalen van een verwijzing tooa taak: de taakverwijzing van een ophalen.</span><span class="sxs-lookup"><span data-stu-id="c4e09-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

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


## <a name="delete-an-access-policy"></a><span data-ttu-id="c4e09-169">Verwijderen van toegangsbeleid instellen</span><span class="sxs-lookup"><span data-stu-id="c4e09-169">Delete an Access Policy</span></span>
<span data-ttu-id="c4e09-170">Hallo volgende voorbeeldcode laat zien hoe tooget een verwijzing tooan-beleid op basis van een beleids-Id en toodelete Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="c4e09-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="c4e09-171">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c4e09-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4e09-172">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c4e09-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

