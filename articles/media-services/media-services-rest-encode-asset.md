---
title: Het Azure-asset coderen met behulp van Media Encoder Standard | Microsoft Docs
description: Informatie over het gebruik van Media Encoder Standard voor het coderen van media-inhoud op Azure Media Services. Codevoorbeelden REST API gebruiken.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="0af58-104">Hoe u een asset coderen met behulp van Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="0af58-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0af58-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0af58-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="0af58-106">REST</span><span class="sxs-lookup"><span data-stu-id="0af58-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="0af58-107">Portal</span><span class="sxs-lookup"><span data-stu-id="0af58-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="0af58-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0af58-108">Overview</span></span>
<span data-ttu-id="0af58-109">Voor het leveren van digitale video via Internet, moet u de media comprimeren.</span><span class="sxs-lookup"><span data-stu-id="0af58-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="0af58-110">Digitale videobestanden groot en mogelijk te groot om te leveren via Internet of voor uw klanten apparaten goed weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0af58-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="0af58-111">Codering is het proces van het comprimeren van video en audio zodat uw klanten het medium kunnen bekijken.</span><span class="sxs-lookup"><span data-stu-id="0af58-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="0af58-112">Codering taken zijn een van de meest voorkomende verwerking in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0af58-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="0af58-113">U creëert coderingstaken om mediabestanden te converteren van de ene naar de andere indeling.</span><span class="sxs-lookup"><span data-stu-id="0af58-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="0af58-114">Wanneer u codeert, kunt u de Media Services ingebouwde encoder (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="0af58-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="0af58-115">U kunt ook een encoder geleverd door een partner Media Services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0af58-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="0af58-116">Coderingsprogramma's van derden zijn beschikbaar via Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0af58-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="0af58-117">U kunt de details van de codering van taken met behulp van vooraf ingestelde tekenreeksen die zijn gedefinieerd voor het coderingsprogramma of met behulp van vooraf ingestelde configuratiebestanden opgeven.</span><span class="sxs-lookup"><span data-stu-id="0af58-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="0af58-118">Zie voor de soorten standaardinstellingen die beschikbaar zijn [taak standaardinstellingen voor Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="0af58-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="0af58-119">Elke taak kan een of meer taken afhankelijk van het type verwerking die u wilt bereiken hebben.</span><span class="sxs-lookup"><span data-stu-id="0af58-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="0af58-120">Met de REST-API kunt u taken en hun bijbehorende taken op twee manieren maken:</span><span class="sxs-lookup"><span data-stu-id="0af58-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="0af58-121">Taken kunnen worden gedefinieerd in line via de navigatie-eigenschap van de taken op taak entiteiten.</span><span class="sxs-lookup"><span data-stu-id="0af58-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="0af58-122">Gebruik de OData-batch-verwerking.</span><span class="sxs-lookup"><span data-stu-id="0af58-122">Use OData batch processing.</span></span>

<span data-ttu-id="0af58-123">Het is raadzaam dat u altijd de bronbestanden te in een adaptive bitrate MP4-set coderen en vervolgens de set naar de gewenste indeling met behulp van converteren [dynamische pakketten](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="0af58-124">Als uw uitvoerasset opslag versleuteld is, moet u het leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="0af58-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="0af58-125">Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="0af58-126">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="0af58-126">Considerations</span></span>

<span data-ttu-id="0af58-127">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="0af58-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0af58-128">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="0af58-129">Voordat u verwijst naar de media processors, Controleer of u de juiste media processor-ID.</span><span class="sxs-lookup"><span data-stu-id="0af58-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="0af58-130">Zie voor meer informatie [mediaprocessoren ophalen](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="0af58-131">Verbinding met Media Services maken</span><span class="sxs-lookup"><span data-stu-id="0af58-131">Connect to Media Services</span></span>

<span data-ttu-id="0af58-132">Zie voor meer informatie over de verbinding maken met de AMS API [toegang tot de API van Azure Media Services met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0af58-133">Na het correct verbinding maakt met https://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="0af58-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0af58-134">U moet de volgende aanroepen naar de nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="0af58-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="0af58-135">Een taak maken met een enkele taak voor codering</span><span class="sxs-lookup"><span data-stu-id="0af58-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="0af58-136">Als u met de REST-API van Media Services werkt, past u de volgende overwegingen:</span><span class="sxs-lookup"><span data-stu-id="0af58-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="0af58-137">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="0af58-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0af58-138">Zie voor meer informatie [Setup voor het ontwikkelen van REST-API voor Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="0af58-139">Na het correct verbinding maakt met https://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="0af58-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0af58-140">U moet de volgende aanroepen naar de nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="0af58-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="0af58-141">Zie voor meer informatie over de verbinding maken met de AMS API [toegang tot de API van Azure Media Services met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="0af58-142">Wanneer met behulp van JSON en op te geven voor het gebruik van de **__metadata** -sleutelwoord in de aanvraag (bijvoorbeeld naar verwijst naar een gekoppelde object), stelt u de **accepteren** koptekst tot [uitgebreide JSON-indeling](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): accepteren: application/json; odata = verbose.</span><span class="sxs-lookup"><span data-stu-id="0af58-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="0af58-143">Het volgende voorbeeld laat zien hoe maken en een taak met één taak ingesteld voor het coderen van een video op een specifieke oplossingsstatus en kwaliteit boeken.</span><span class="sxs-lookup"><span data-stu-id="0af58-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="0af58-144">Wanneer u met Media Encoder Standard codeert, kunt u taak configuratie standaardinstellingen opgegeven [hier](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="0af58-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="0af58-145">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="0af58-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="0af58-146">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="0af58-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="0af58-147">Naam van de uitvoerasset instellen</span><span class="sxs-lookup"><span data-stu-id="0af58-147">Set the output asset's name</span></span>
<span data-ttu-id="0af58-148">Het volgende voorbeeld ziet u hoe het kenmerk assetName instellen:</span><span class="sxs-lookup"><span data-stu-id="0af58-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="0af58-149">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="0af58-149">Considerations</span></span>
* <span data-ttu-id="0af58-150">TaskBody eigenschappen moeten letterlijke XML gebruiken voor het definiëren van het aantal invoer of uitvoer van de activa die worden gebruikt door de taak.</span><span class="sxs-lookup"><span data-stu-id="0af58-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="0af58-151">Het onderwerp bevat de XML-Schema-definitie voor het XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="0af58-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="0af58-152">In de definitie TaskBody elke interne waarde voor <inputAsset> en <outputAsset> JobInputAsset(value) of JobOutputAsset(value) moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0af58-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="0af58-153">Een taak kan meerdere uitvoer elementen hebben.</span><span class="sxs-lookup"><span data-stu-id="0af58-153">A task can have multiple output assets.</span></span> <span data-ttu-id="0af58-154">Één JobOutputAsset(x) kan slechts eenmaal worden gebruikt als uitvoer van een taak in een taak.</span><span class="sxs-lookup"><span data-stu-id="0af58-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="0af58-155">U kunt JobInputAsset of JobOutputAsset opgeven als een invoer actief van een taak.</span><span class="sxs-lookup"><span data-stu-id="0af58-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="0af58-156">Taken moeten vormen geen cyclus.</span><span class="sxs-lookup"><span data-stu-id="0af58-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="0af58-157">De waardeparameter die u aan JobInputAsset of JobOutputAsset doorgeeft vertegenwoordigt de indexwaarde voor een asset.</span><span class="sxs-lookup"><span data-stu-id="0af58-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="0af58-158">De werkelijke activa zijn gedefinieerd in de InputMediaAssets en OutputMediaAssets navigatie-eigenschappen op de definitie van de taak entiteit.</span><span class="sxs-lookup"><span data-stu-id="0af58-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="0af58-159">Omdat het Media Services is gebouwd op OData v3, de afzonderlijke elementen in de verzamelingen InputMediaAssets en OutputMediaAssets navigatie-eigenschap wordt verwezen door een ' __metadata: uri ' naam / waarde-paar.</span><span class="sxs-lookup"><span data-stu-id="0af58-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="0af58-160">InputMediaAssets toegewezen aan een of meer elementen die u hebt gemaakt in een Media Services.</span><span class="sxs-lookup"><span data-stu-id="0af58-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="0af58-161">OutputMediaAssets worden gemaakt door het systeem.</span><span class="sxs-lookup"><span data-stu-id="0af58-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="0af58-162">Ze niet verwijzen naar een bestaande asset.</span><span class="sxs-lookup"><span data-stu-id="0af58-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="0af58-163">OutputMediaAssets kan worden benoemd met het kenmerk assetName.</span><span class="sxs-lookup"><span data-stu-id="0af58-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="0af58-164">Als dit kenmerk niet aanwezig is is, is de naam van de OutputMediaAsset ongeacht de interne tekst-waarde van de <outputAsset> -element is met een achtervoegsel van de waarde van de taak, of de taak-Id-waarde (in het geval waarbij de eigenschap Name is niet gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="0af58-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="0af58-165">Bijvoorbeeld, als u een waarde voor assetName met "Voorbeeld" instelt, wordt de eigenschap OutputMediaAsset Name ingesteld op "Voorbeeld".</span><span class="sxs-lookup"><span data-stu-id="0af58-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="0af58-166">Echter als u een waarde voor assetName niet hebt ingesteld, maar de taaknaam van de aan 'NewJob' ingesteld, zou klikt u vervolgens de naam van de OutputMediaAsset zijn "JobOutputAsset (waarde) _NewJob."</span><span class="sxs-lookup"><span data-stu-id="0af58-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="0af58-167">Maken van een taak met gekoppelde taken</span><span class="sxs-lookup"><span data-stu-id="0af58-167">Create a job with chained tasks</span></span>
<span data-ttu-id="0af58-168">In veel scenario's van toepassing willen ontwikkelaars maken van een reeks taken te verwerken.</span><span class="sxs-lookup"><span data-stu-id="0af58-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="0af58-169">U kunt een reeks keten taken maken in Media Services.</span><span class="sxs-lookup"><span data-stu-id="0af58-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="0af58-170">Elke taak voert de van de verschillende verwerkingsstappen en processors van verschillende media kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0af58-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="0af58-171">De keten taken kunnen overdragen een asset van de ene taak naar de andere een lineaire reeks taken uitvoeren op de asset.</span><span class="sxs-lookup"><span data-stu-id="0af58-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="0af58-172">De taken uitgevoerd in een taak zijn echter niet vereist zijn in een reeks.</span><span class="sxs-lookup"><span data-stu-id="0af58-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="0af58-173">Wanneer u een keten taak, de keten maakt **ITask** objecten worden gemaakt in een enkel **IJob** object.</span><span class="sxs-lookup"><span data-stu-id="0af58-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="0af58-174">Er is een limiet van 30 taken per taak.</span><span class="sxs-lookup"><span data-stu-id="0af58-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="0af58-175">Als u meer dan 30 taken zijn gekoppeld wilt, maakt u meer dan één taak om de taken te bevatten.</span><span class="sxs-lookup"><span data-stu-id="0af58-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="0af58-176">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="0af58-176">Considerations</span></span>
<span data-ttu-id="0af58-177">Inschakelen van taak-koppeling:</span><span class="sxs-lookup"><span data-stu-id="0af58-177">To enable task chaining:</span></span>

* <span data-ttu-id="0af58-178">Een taak moet ten minste twee taken hebben.</span><span class="sxs-lookup"><span data-stu-id="0af58-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="0af58-179">Er moet ten minste één taak waarvan invoer de uitvoer van een andere taak in de taak is.</span><span class="sxs-lookup"><span data-stu-id="0af58-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="0af58-180">Verwerking van gebruiken OData-batch</span><span class="sxs-lookup"><span data-stu-id="0af58-180">Use OData batch processing</span></span>
<span data-ttu-id="0af58-181">Het volgende voorbeeld laat zien hoe OData batchverwerking gebruiken om te maken van een job en taken.</span><span class="sxs-lookup"><span data-stu-id="0af58-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="0af58-182">Zie voor informatie over batchverwerking, [Open Data Protocol (OData) batchverwerking](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="0af58-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="0af58-183">Een taak maken met behulp van een taaksjabloon</span><span class="sxs-lookup"><span data-stu-id="0af58-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="0af58-184">Wanneer u meerdere elementen verwerkt met behulp van een gemeenschappelijke set taken, gebruiken een taaksjabloon opgeven van de standaardinstellingen van de taak standaard of instellen van de volgorde van taken.</span><span class="sxs-lookup"><span data-stu-id="0af58-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="0af58-185">Het volgende voorbeeld laat zien hoe een taaksjabloon maken met een TaskTemplate die is gedefinieerd in line.</span><span class="sxs-lookup"><span data-stu-id="0af58-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="0af58-186">De TaskTemplate gebruikt Media Encoder Standard als de MediaProcessor voor het coderen van het assetbestand.</span><span class="sxs-lookup"><span data-stu-id="0af58-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="0af58-187">Andere MediaProcessors kan echter ook worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0af58-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="0af58-188">In tegenstelling tot andere entiteiten Media Services, moet u een nieuwe GUID-id definiëren voor elke TaskTemplate en plaats deze in de taskTemplateId en Id-eigenschap in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="0af58-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="0af58-189">Het schema met content-ID moet voldoen aan het schema dat wordt beschreven in Azure Media Services-entiteiten identificeren.</span><span class="sxs-lookup"><span data-stu-id="0af58-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="0af58-190">Bovendien kan niet JobTemplates worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="0af58-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="0af58-191">In plaats daarvan moet u een nieuw bestand met de bijgewerkte wijzigingen maken.</span><span class="sxs-lookup"><span data-stu-id="0af58-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="0af58-192">Als dit lukt, wordt het volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="0af58-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="0af58-193">Het volgende voorbeeld ziet u hoe een taak die verwijst naar een taaksjabloon-Id te maken:</span><span class="sxs-lookup"><span data-stu-id="0af58-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="0af58-194">Als dit lukt, wordt het volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="0af58-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="0af58-195">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="0af58-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0af58-196">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="0af58-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0af58-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0af58-197">Next steps</span></span>
<span data-ttu-id="0af58-198">Als u weet dat het maken van een taak voor een asset coderen, Zie [het controleren van de voortgang van de taak met Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0af58-199">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0af58-199">See also</span></span>
[<span data-ttu-id="0af58-200">Ophalen van Media-Processors</span><span class="sxs-lookup"><span data-stu-id="0af58-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
