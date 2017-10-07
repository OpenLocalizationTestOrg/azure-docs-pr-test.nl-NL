---
title: aaaHow tooencode een Azure-asset met behulp van Media Encoder Standard | Microsoft Docs
description: Meer informatie over hoe toouse Media Encoder Standard tooencode media inhoud op Azure Media Services. Codevoorbeelden REST API gebruiken.
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
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="7a98e-104">Hoe tooencode een asset met behulp van Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="7a98e-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a98e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7a98e-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="7a98e-106">REST</span><span class="sxs-lookup"><span data-stu-id="7a98e-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="7a98e-107">Portal</span><span class="sxs-lookup"><span data-stu-id="7a98e-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="7a98e-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7a98e-108">Overview</span></span>
<span data-ttu-id="7a98e-109">toodeliver digitale video via Internet hello, moet u Hallo media comprimeren.</span><span class="sxs-lookup"><span data-stu-id="7a98e-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="7a98e-110">Digitale videobestanden groot en mogelijk te groot toodeliver over Hallo Internet of voor uw klanten apparaten toodisplay goed.</span><span class="sxs-lookup"><span data-stu-id="7a98e-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="7a98e-111">Codering is Hallo-proces van het comprimeren van video en audio zodat uw klanten het medium kunnen bekijken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="7a98e-112">Codering taken zijn een van de meest voorkomende verwerkingen Hallo in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a98e-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="7a98e-113">U maakt codering taken tooconvert media-bestanden vanuit een codering tooanother.</span><span class="sxs-lookup"><span data-stu-id="7a98e-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="7a98e-114">Wanneer u codeert, kunt u Hallo Media Services ingebouwde codering (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="7a98e-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="7a98e-115">U kunt ook een encoder geleverd door een partner Media Services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="7a98e-116">Coderingsprogramma's van derden zijn beschikbaar via hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7a98e-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="7a98e-117">U kunt details op Hallo van coderingstaken met behulp van vooraf ingestelde tekenreeksen die zijn gedefinieerd voor het coderingsprogramma of met behulp van vooraf ingestelde configuratiebestanden opgeven.</span><span class="sxs-lookup"><span data-stu-id="7a98e-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="7a98e-118">toosee hello typen standaardinstellingen die beschikbaar zijn, Zie [taak standaardinstellingen voor Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="7a98e-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="7a98e-119">Elke taak kan een of meer taken, afhankelijk van Hallo type verwerken die u wilt dat tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="7a98e-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="7a98e-120">U kunt via Hallo REST-API, taken en hun bijbehorende taken maken op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="7a98e-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="7a98e-121">Taken kunnen worden gedefinieerd in line via Hallo taken navigatie-eigenschap op taak entiteiten.</span><span class="sxs-lookup"><span data-stu-id="7a98e-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="7a98e-122">Gebruik de OData-batch-verwerking.</span><span class="sxs-lookup"><span data-stu-id="7a98e-122">Use OData batch processing.</span></span>

<span data-ttu-id="7a98e-123">Het is raadzaam dat u altijd de bronbestanden te in een adaptive bitrate MP4-set coderen, en vervolgens Hallo set toohello gewenste indeling te met behulp van converteren [dynamische pakketten](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="7a98e-124">Als uw uitvoerasset opslag versleuteld is, moet u Hallo-leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="7a98e-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="7a98e-125">Zie voor meer informatie [leveringsbeleid voor Assets configureren](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="7a98e-126">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="7a98e-126">Considerations</span></span>

<span data-ttu-id="7a98e-127">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="7a98e-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="7a98e-128">Zie voor meer informatie [Setup voor het ontwikkelen van Media Services REST API](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="7a98e-129">Voordat u verwijst naar de media processors, moet u controleren of hebt u Hallo juiste media processor-ID.</span><span class="sxs-lookup"><span data-stu-id="7a98e-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="7a98e-130">Zie voor meer informatie [mediaprocessoren ophalen](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="7a98e-131">Verbinding maken met tooMedia Services</span><span class="sxs-lookup"><span data-stu-id="7a98e-131">Connect tooMedia Services</span></span>

<span data-ttu-id="7a98e-132">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="7a98e-133">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a98e-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7a98e-134">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="7a98e-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="7a98e-135">Een taak maken met een enkele taak voor codering</span><span class="sxs-lookup"><span data-stu-id="7a98e-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="7a98e-136">Wanneer u met Hallo REST API voor Media Services werkt, letten hello volgende:</span><span class="sxs-lookup"><span data-stu-id="7a98e-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="7a98e-137">Bij het openen van entiteiten in Media Services, moet u specifieke header-velden en waarden instellen in uw HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="7a98e-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="7a98e-138">Zie voor meer informatie [Setup voor het ontwikkelen van REST-API voor Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="7a98e-139">Nadat de verbinding tot stand toohttps://media.windows.net, ontvangt u een 301 omleiding opgeven van een andere URI van de Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a98e-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7a98e-140">U moet de volgende aanroepen toohello ervoor nieuwe URI.</span><span class="sxs-lookup"><span data-stu-id="7a98e-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="7a98e-141">Voor informatie over hoe tooconnect toohello AMS API, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="7a98e-142">Wanneer met behulp van JSON en geven toouse hello **__metadata** sleutelwoord in Hallo-aanvraag (bijvoorbeeld tooreferences gekoppelde objecten), moet u Hallo instellen **accepteren** header te[uitgebreide JSON-indeling ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accepteren: application/json; odata = verbose.</span><span class="sxs-lookup"><span data-stu-id="7a98e-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="7a98e-143">Hallo volgende voorbeeld ziet u hoe toocreate en na een taak met één taak ingesteld tooencode video op een specifieke oplossingsstatus en kwaliteit.</span><span class="sxs-lookup"><span data-stu-id="7a98e-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="7a98e-144">Wanneer u met Media Encoder Standard codeert, kunt u taak configuratie standaardinstellingen opgegeven [hier](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="7a98e-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="7a98e-145">Aanvraag:</span><span class="sxs-lookup"><span data-stu-id="7a98e-145">Request:</span></span>

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

<span data-ttu-id="7a98e-146">Antwoord:</span><span class="sxs-lookup"><span data-stu-id="7a98e-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="7a98e-147">Hallo uitvoerasset naam instellen</span><span class="sxs-lookup"><span data-stu-id="7a98e-147">Set hello output asset's name</span></span>
<span data-ttu-id="7a98e-148">Hallo volgende voorbeeld ziet u hoe tooset Hallo assetName kenmerk:</span><span class="sxs-lookup"><span data-stu-id="7a98e-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="7a98e-149">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="7a98e-149">Considerations</span></span>
* <span data-ttu-id="7a98e-150">TaskBody eigenschappen moeten letterlijke XML toodefine Hallo aantal invoer of uitvoer-elementen die worden gebruikt door de taak hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="7a98e-151">Hallo onderwerp bevat Hallo XML-schemadefinitie voor Hallo XML.</span><span class="sxs-lookup"><span data-stu-id="7a98e-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="7a98e-152">In Hallo TaskBody definition, elke interne waarde voor <inputAsset> en <outputAsset> JobInputAsset(value) of JobOutputAsset(value) moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7a98e-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="7a98e-153">Een taak kan meerdere uitvoer elementen hebben.</span><span class="sxs-lookup"><span data-stu-id="7a98e-153">A task can have multiple output assets.</span></span> <span data-ttu-id="7a98e-154">Één JobOutputAsset(x) kan slechts eenmaal worden gebruikt als uitvoer van een taak in een taak.</span><span class="sxs-lookup"><span data-stu-id="7a98e-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="7a98e-155">U kunt JobInputAsset of JobOutputAsset opgeven als een invoer actief van een taak.</span><span class="sxs-lookup"><span data-stu-id="7a98e-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="7a98e-156">Taken moeten vormen geen cyclus.</span><span class="sxs-lookup"><span data-stu-id="7a98e-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="7a98e-157">Hallo waardeparameter u doorgeeft tooJobInputAsset of JobOutputAsset vertegenwoordigt de indexwaarde Hallo voor een asset.</span><span class="sxs-lookup"><span data-stu-id="7a98e-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="7a98e-158">Hallo werkelijke activa zijn gedefinieerd in Hallo InputMediaAssets en OutputMediaAssets navigatie-eigenschappen op Hallo entiteit taakdefinitie.</span><span class="sxs-lookup"><span data-stu-id="7a98e-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="7a98e-159">Omdat het Media Services is gebouwd op OData v3, afzonderlijke activa in Hallo InputMediaAssets Hallo en OutputMediaAssets navigatie-eigenschap verzamelingen wordt verwezen door een ' __metadata: uri ' naam / waarde-paar.</span><span class="sxs-lookup"><span data-stu-id="7a98e-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="7a98e-160">InputMediaAssets maps tooone of meer elementen die u hebt gemaakt in Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a98e-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="7a98e-161">OutputMediaAssets zijn gemaakt door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="7a98e-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="7a98e-162">Ze niet verwijzen naar een bestaande asset.</span><span class="sxs-lookup"><span data-stu-id="7a98e-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="7a98e-163">OutputMediaAssets kan worden benoemd met Hallo assetName kenmerk.</span><span class="sxs-lookup"><span data-stu-id="7a98e-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="7a98e-164">Als dit kenmerk niet aanwezig is, wordt de naam van de Hallo Hallo OutputMediaAsset de waarde van de interne tekst hello Hallo is <outputAsset> -element is en het achtervoegsel Hallo taaknaam waarde of Hallo taak-Id-waarde (in geval van Hallo waar Hallo Name-eigenschap niet is gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="7a98e-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="7a98e-165">Bijvoorbeeld, als u een waarde voor assetName instellen Sample te "Voorbeeld" en vervolgens Hallo OutputMediaAsset de naam van de eigenschap is ingesteld te'."</span><span class="sxs-lookup"><span data-stu-id="7a98e-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="7a98e-166">Als u niet een waarde voor assetName instellen, maar de taaknaam Hallo hebt ingesteld zou te 'NewJob' en klik vervolgens Hallo OutputMediaAsset naam wel "JobOutputAsset (waarde) _NewJob."</span><span class="sxs-lookup"><span data-stu-id="7a98e-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="7a98e-167">Maken van een taak met gekoppelde taken</span><span class="sxs-lookup"><span data-stu-id="7a98e-167">Create a job with chained tasks</span></span>
<span data-ttu-id="7a98e-168">In veel scenario's van toepassing wilt ontwikkelaars toocreate een reeks taken te verwerken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="7a98e-169">U kunt een reeks keten taken maken in Media Services.</span><span class="sxs-lookup"><span data-stu-id="7a98e-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="7a98e-170">Elke taak voert de van de verschillende verwerkingsstappen en processors van verschillende media kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="7a98e-171">Hallo teruggekoppeld taken kunnen een asset aanlevert uit één taak tooanother, een lineaire reeks taken uitvoeren op Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="7a98e-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="7a98e-172">Hallo-taken in een taak wordt uitgevoerd, zijn echter niet vereist toobe in een reeks.</span><span class="sxs-lookup"><span data-stu-id="7a98e-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="7a98e-173">Wanneer u een keten taak maakt, Hallo teruggekoppeld **ITask** objecten worden gemaakt in een enkel **IJob** object.</span><span class="sxs-lookup"><span data-stu-id="7a98e-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="7a98e-174">Er is een limiet van 30 taken per taak.</span><span class="sxs-lookup"><span data-stu-id="7a98e-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="7a98e-175">Als u toochain meer dan 30 taken moet, maakt u meer dan één taak toocontain Hallo taken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="7a98e-176">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="7a98e-176">Considerations</span></span>
<span data-ttu-id="7a98e-177">tooenable taak koppeling:</span><span class="sxs-lookup"><span data-stu-id="7a98e-177">tooenable task chaining:</span></span>

* <span data-ttu-id="7a98e-178">Een taak moet ten minste twee taken hebben.</span><span class="sxs-lookup"><span data-stu-id="7a98e-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="7a98e-179">Er moet ten minste één taak waarvan invoer Hallo-uitvoer van een andere taak in het Hallo-taak is.</span><span class="sxs-lookup"><span data-stu-id="7a98e-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="7a98e-180">Verwerking van gebruiken OData-batch</span><span class="sxs-lookup"><span data-stu-id="7a98e-180">Use OData batch processing</span></span>
<span data-ttu-id="7a98e-181">Hallo volgende voorbeeld ziet u hoe toouse OData verwerking toocreate batch een job en taken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="7a98e-182">Zie voor informatie over batchverwerking, [Open Data Protocol (OData) batchverwerking](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="7a98e-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="7a98e-183">Een taak maken met behulp van een taaksjabloon</span><span class="sxs-lookup"><span data-stu-id="7a98e-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="7a98e-184">Wanneer u meerdere activa verwerken met behulp van een gemeenschappelijke set taken, gebruik die een standaardtaak taaksjabloon toospecify Hallo voorinstellingen of tooset Hallo volgorde van taken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="7a98e-185">Hallo volgende voorbeeld ziet u hoe toocreate een taaksjabloon met een TaskTemplate die inline gedefinieerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="7a98e-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="7a98e-186">Hallo TaskTemplate maakt gebruik van Media Encoder Standard Hallo als Hallo MediaProcessor tooencode Hallo asset-bestand.</span><span class="sxs-lookup"><span data-stu-id="7a98e-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="7a98e-187">Andere MediaProcessors kan echter ook worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7a98e-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="7a98e-188">In tegenstelling tot andere entiteiten Media Services, moet u een nieuwe GUID-id definiëren voor elke TaskTemplate en plaats deze in Hallo taskTemplateId en Id-eigenschap in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="7a98e-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="7a98e-189">Hallo inhoud-id-schema moet volgen op Hallo schema beschreven in Azure Media Services-entiteiten identificeren.</span><span class="sxs-lookup"><span data-stu-id="7a98e-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="7a98e-190">Bovendien kan niet JobTemplates worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7a98e-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="7a98e-191">In plaats daarvan moet u een nieuw bestand met de bijgewerkte wijzigingen maken.</span><span class="sxs-lookup"><span data-stu-id="7a98e-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="7a98e-192">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="7a98e-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="7a98e-193">Hallo volgende voorbeeld wordt getoond hoe toocreate een taak die verwijst naar een taaksjabloon-Id:</span><span class="sxs-lookup"><span data-stu-id="7a98e-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="7a98e-194">Als dit lukt, wordt de Hallo volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="7a98e-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="7a98e-195">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="7a98e-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7a98e-196">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="7a98e-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7a98e-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a98e-197">Next steps</span></span>
<span data-ttu-id="7a98e-198">Als u weet hoe toocreate een taak tooencode een activum, Zie [hoe toocheck taak uitgevoerd met Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="7a98e-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a98e-199">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7a98e-199">See also</span></span>
[<span data-ttu-id="7a98e-200">Ophalen van Media-Processors</span><span class="sxs-lookup"><span data-stu-id="7a98e-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
