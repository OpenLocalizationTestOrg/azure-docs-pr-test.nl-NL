---
title: aaaAzure functies Blob Storage bindingen | Microsoft Docs
description: Begrijpen hoe Azure Storage toouse triggers en bindingen in Azure Functions.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="2af5a-104">Azure Functions Blob storage-bindingen</span><span class="sxs-lookup"><span data-stu-id="2af5a-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="2af5a-105">Dit artikel wordt uitgelegd hoe tooconfigure en werken met Azure Blob storage bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="2af5a-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="2af5a-106">Azure Functions ondersteunt worden geactiveerd, invoer en uitvoer van de bindingen voor Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="2af5a-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="2af5a-107">Zie functies die beschikbaar in alle bindingen zijn [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="2af5a-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="2af5a-108">Een [blob storage-account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2af5a-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="2af5a-109">BLOB storage triggers en bindingen vereisen een algemeen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2af5a-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="2af5a-110">BLOB storage triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="2af5a-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="2af5a-111">Hallo Azure Blob storage-trigger gebruikt, wordt de functiecode aangeroepen wanneer een nieuwe of bijgewerkte blob wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="2af5a-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="2af5a-112">Hallo blob-inhoud worden geleverd als invoer toohello-functie.</span><span class="sxs-lookup"><span data-stu-id="2af5a-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="2af5a-113">Definieer een blob storage-trigger met Hallo **integreren** tabblad in Hallo Functions-portal.</span><span class="sxs-lookup"><span data-stu-id="2af5a-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="2af5a-114">Hallo portal maakt na definitie in Hallo Hallo **bindingen** sectie van *function.json*:</span><span class="sxs-lookup"><span data-stu-id="2af5a-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="2af5a-115">BLOB-invoer en uitvoer bindingen zijn gedefinieerd met behulp van `blob` als het bindingstype Hallo:</span><span class="sxs-lookup"><span data-stu-id="2af5a-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="2af5a-116">Hallo `path` ondersteunt de eigenschap binding expressies en filterparameters.</span><span class="sxs-lookup"><span data-stu-id="2af5a-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="2af5a-117">Zie [patronen naam](#pattern).</span><span class="sxs-lookup"><span data-stu-id="2af5a-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="2af5a-118">Hallo `connection` eigenschap Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="2af5a-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="2af5a-119">Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="2af5a-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="2af5a-120">Wanneer u een blob-trigger op een plan verbruik, kunnen er up tooa 10 minuten vertraging bij de verwerking van nieuwe blobs nadat een functie-app niet actief is geworden.</span><span class="sxs-lookup"><span data-stu-id="2af5a-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="2af5a-121">Nadat het Hallo-functie-app wordt uitgevoerd, worden onmiddellijk blobs verwerkt.</span><span class="sxs-lookup"><span data-stu-id="2af5a-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="2af5a-122">Dit eerste tooavoid uitstellen, kunt u een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="2af5a-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="2af5a-123">Gebruik een App Service-abonnement met altijd op ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2af5a-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="2af5a-124">Gebruik een ander mechanisme tootrigger Hallo blob verwerken, zoals een wachtrijbericht die Hallo blob-naam bevat.</span><span class="sxs-lookup"><span data-stu-id="2af5a-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="2af5a-125">Zie voor een voorbeeld [wachtrij trigger met blob invoer binding](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="2af5a-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="2af5a-126">Bestandsnaampatronen</span><span class="sxs-lookup"><span data-stu-id="2af5a-126">Name patterns</span></span>
<span data-ttu-id="2af5a-127">U kunt een naampatroon blob opgeven in Hallo `path` eigenschap, die een filter of binding-expressie.</span><span class="sxs-lookup"><span data-stu-id="2af5a-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="2af5a-128">Zie [Binding expressies en patronen](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="2af5a-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="2af5a-129">Bijvoorbeeld gebruiken toofilter tooblobs die beginnen met Hallo tekenreeks 'oorspronkelijke' hello definitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="2af5a-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="2af5a-130">Dit pad zoeken naar een blob met de naam *oorspronkelijke Blob1.txt* in Hallo *invoer* container en de waarde Hallo Hallo `name` variabele in functiecode is `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="2af5a-131">toobind toohello blob-bestandsnaam en extensie afzonderlijk twee patronen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2af5a-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="2af5a-132">Dit pad ook zoeken naar een blob met de naam *oorspronkelijke Blob1.txt*, en de waarde van Hallo Hallo `blobname` en `blobextension` variabelen in de functiecode zijn *oorspronkelijke Blob1* en *txt*.</span><span class="sxs-lookup"><span data-stu-id="2af5a-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="2af5a-133">U kunt Hallo bestandstype blobs beperken met behulp van een vaste waarde voor de bestandsextensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2af5a-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="2af5a-134">Bijvoorbeeld: tootrigger alleen op PNG-bestanden, gebruik Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="2af5a-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="2af5a-135">Accolades zijn speciale tekens in de naam van patronen.</span><span class="sxs-lookup"><span data-stu-id="2af5a-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="2af5a-136">toospecify blob-namen die accolades in de naam van de hello hebben, escape Hallo accolades u twee gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2af5a-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="2af5a-137">Hallo volgende voorbeeld wordt gezocht naar een blob met de naam *{20140101}-soundfile.mp3* in Hallo *installatiekopieën* container en Hallo `name` variabelewaarde in Hallo functiecode is  *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="2af5a-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="2af5a-138">Trigger metagegevens</span><span class="sxs-lookup"><span data-stu-id="2af5a-138">Trigger metadata</span></span>

<span data-ttu-id="2af5a-139">Hallo blob trigger biedt verschillende eigenschappen voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="2af5a-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="2af5a-140">Deze eigenschappen kunnen worden gebruikt als onderdeel van de expressies bindingen in andere bindingen of als parameters in uw code.</span><span class="sxs-lookup"><span data-stu-id="2af5a-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="2af5a-141">Deze waarden Hallo hebben dezelfde betekenis als [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="2af5a-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="2af5a-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="2af5a-142">**BlobTrigger**.</span></span> <span data-ttu-id="2af5a-143">Typ `string`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-143">Type `string`.</span></span> <span data-ttu-id="2af5a-144">Hallo activerende blobpad</span><span class="sxs-lookup"><span data-stu-id="2af5a-144">hello triggering blob path</span></span>
- <span data-ttu-id="2af5a-145">**URI**.</span><span class="sxs-lookup"><span data-stu-id="2af5a-145">**Uri**.</span></span> <span data-ttu-id="2af5a-146">Typ `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-146">Type `System.Uri`.</span></span> <span data-ttu-id="2af5a-147">Hallo-blob-URI voor de primaire locatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2af5a-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="2af5a-148">**Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="2af5a-148">**Properties**.</span></span> <span data-ttu-id="2af5a-149">Typ `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="2af5a-150">Hallo van blob-Systeemeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2af5a-150">hello blob's system properties.</span></span>
- <span data-ttu-id="2af5a-151">**Metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="2af5a-151">**Metadata**.</span></span> <span data-ttu-id="2af5a-152">Typ `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="2af5a-153">Hallo gebruiker gedefinieerde metagegevens voor Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="2af5a-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="2af5a-154">BLOB ontvangstbevestigingen</span><span class="sxs-lookup"><span data-stu-id="2af5a-154">Blob receipts</span></span>
<span data-ttu-id="2af5a-155">Hello Azure Functions-runtime zorgt ervoor dat er geen blob-activeringsfunctie meer dan één keer wordt aangeroepen voor dezelfde nieuwe of bijgewerkte blob Hallo.</span><span class="sxs-lookup"><span data-stu-id="2af5a-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="2af5a-156">toodetermine als een versie van de opgegeven blob is verwerkt, houdt *blob ontvangstbevestigingen*.</span><span class="sxs-lookup"><span data-stu-id="2af5a-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="2af5a-157">Azure Functions winkels blob ontvangstbevestigingen in een container met de naam *webjobs-azure-hosts* in hello Azure storage-account voor de functie-app (gedefinieerd door de app-instelling Hallo `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="2af5a-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="2af5a-158">De ontvangst van een blob heeft Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="2af5a-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="2af5a-159">Hallo functie geactiveerd ('*&lt;functie app-naam >*. Functies.  *&lt;functienaam >*', bijvoorbeeld: 'MyFunctionApp.Functions.CopyBlob')</span><span class="sxs-lookup"><span data-stu-id="2af5a-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="2af5a-160">Hallo-containernaam</span><span class="sxs-lookup"><span data-stu-id="2af5a-160">hello container name</span></span>
* <span data-ttu-id="2af5a-161">Hallo blobtype ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="2af5a-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="2af5a-162">Hallo blob-naam</span><span class="sxs-lookup"><span data-stu-id="2af5a-162">hello blob name</span></span>
* <span data-ttu-id="2af5a-163">Hallo ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="2af5a-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="2af5a-164">Hallo blob ontvangst voor blob tooforce opnieuw verwerken van een blob verwijderen uit Hallo *webjobs-azure-hosts* container handmatig.</span><span class="sxs-lookup"><span data-stu-id="2af5a-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="2af5a-165">Verwerken van verontreinigde blobs</span><span class="sxs-lookup"><span data-stu-id="2af5a-165">Handling poison blobs</span></span>
<span data-ttu-id="2af5a-166">Als een functie van de trigger blob is mislukt voor een bepaalde functies van Azure-blob pogingen die een totaal van 5 maal standaard functioneren.</span><span class="sxs-lookup"><span data-stu-id="2af5a-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="2af5a-167">Als alle 5 pogingen mislukken, Azure Functions wordt toegevoegd een tooa opslag berichtenwachtrij met de naam *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="2af5a-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="2af5a-168">Hallo-bericht van wachtrij voor verontreinigde blobs is een JSON-object met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="2af5a-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="2af5a-169">FunctionId (Hallo indeling  *&lt;functie app-naam >*. Functies.  *&lt;functienaam >*)</span><span class="sxs-lookup"><span data-stu-id="2af5a-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="2af5a-170">BlobType ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="2af5a-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="2af5a-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="2af5a-171">ContainerName</span></span>
* <span data-ttu-id="2af5a-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="2af5a-172">BlobName</span></span>
* <span data-ttu-id="2af5a-173">ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="2af5a-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="2af5a-174">Er wordt gedelegeerd voor grote containers BLOB</span><span class="sxs-lookup"><span data-stu-id="2af5a-174">Blob polling for large containers</span></span>
<span data-ttu-id="2af5a-175">Als Hallo blob-container wordt bewaakt meer dan 10.000 blobs bevat, meld Hallo functies runtime scant bestanden toowatch voor nieuwe of gewijzigde blobs.</span><span class="sxs-lookup"><span data-stu-id="2af5a-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="2af5a-176">Dit proces is niet realtime.</span><span class="sxs-lookup"><span data-stu-id="2af5a-176">This process is not real time.</span></span> <span data-ttu-id="2af5a-177">Een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat Hallo blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2af5a-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="2af5a-178">Bovendien [opslag logboeken worden gemaakt op een 'best effort'](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span><span class="sxs-lookup"><span data-stu-id="2af5a-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="2af5a-179">Er is geen garantie dat alle gebeurtenissen worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="2af5a-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="2af5a-180">Onder bepaalde omstandigheden wellicht Logboeken niet opgehaald.</span><span class="sxs-lookup"><span data-stu-id="2af5a-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="2af5a-181">Als u sneller of betrouwbaarder blob verwerking vereist, kunt u een [wachtrijbericht](../storage/queues/storage-dotnet-how-to-use-queues.md) bij het maken van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="2af5a-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="2af5a-182">Vervolgens gebruikt u een [wachtrij trigger](functions-bindings-storage-queue.md) in plaats van een blob trigger tooprocess Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="2af5a-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="2af5a-183">Met behulp van een blob-trigger en invoer binding</span><span class="sxs-lookup"><span data-stu-id="2af5a-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="2af5a-184">In .NET-functies, toegang tot blobgegevens Hallo met een parameter van de methode, zoals `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="2af5a-185">Hier `paramName` is Hallo-waarde die u hebt opgegeven in Hallo [trigger configuratie](#trigger).</span><span class="sxs-lookup"><span data-stu-id="2af5a-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="2af5a-186">In de Node.js-functies toegang Hallo invoer blob-gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="2af5a-187">In .NET, kunt u tooany typen Hallo Hallo onderstaande binden.</span><span class="sxs-lookup"><span data-stu-id="2af5a-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="2af5a-188">Als gebruikt als een invoer-binding, is enkele van deze typen vereisen een `inout` richting in binding *function.json*.</span><span class="sxs-lookup"><span data-stu-id="2af5a-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="2af5a-189">Deze richting wordt niet ondersteund door Hallo standaardeditor, zodat u Hallo geavanceerde editor moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2af5a-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="2af5a-190">`ICloudBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="2af5a-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="2af5a-191">`CloudBlockBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="2af5a-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="2af5a-192">`CloudPageBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="2af5a-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="2af5a-193">`CloudAppendBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="2af5a-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="2af5a-194">Als tekst blobs worden verwacht, kunt u ook .NET tooa binden `string` type.</span><span class="sxs-lookup"><span data-stu-id="2af5a-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="2af5a-195">Dit wordt alleen aanbevolen als Hallo blob klein is, zoals Hallo gehele blob-inhoud in het geheugen geladen.</span><span class="sxs-lookup"><span data-stu-id="2af5a-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="2af5a-196">In het algemeen is het beter toouse een `Stream` of `CloudBlockBlob` type.</span><span class="sxs-lookup"><span data-stu-id="2af5a-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="2af5a-197">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="2af5a-197">Trigger sample</span></span>
<span data-ttu-id="2af5a-198">Stel dat u hebt Hallo function.json die een blob storage-trigger definieert te volgen:</span><span class="sxs-lookup"><span data-stu-id="2af5a-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="2af5a-199">Zie Hallo taalspecifieke steekproef die het Hallo-inhoud van elke blob die wordt toegevoegd toohello bewaakte container registreert.</span><span class="sxs-lookup"><span data-stu-id="2af5a-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="2af5a-200">C#</span><span class="sxs-lookup"><span data-stu-id="2af5a-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="2af5a-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="2af5a-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="2af5a-202">Voorbeelden van BLOB-trigger in C#</span><span class="sxs-lookup"><span data-stu-id="2af5a-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="2af5a-203">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="2af5a-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="2af5a-204">Binding met een blob uitvoer</span><span class="sxs-lookup"><span data-stu-id="2af5a-204">Using a blob output binding</span></span>

<span data-ttu-id="2af5a-205">.NET-functies, moet u gebruiken een `out string` parameter in uw functiehandtekening of gebruik een van de typen Hallo in Hallo lijst te volgen.</span><span class="sxs-lookup"><span data-stu-id="2af5a-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="2af5a-206">In Node.js-functies, opent u met behulp Hallo uitvoer blob `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="2af5a-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="2af5a-207">In de .NET-functies kunt u tooany Hallo typen volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2af5a-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="2af5a-208">Wachtrij-trigger met blob-invoer en uitvoer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2af5a-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="2af5a-209">Stel dat u hebt na function.json hello, die definieert een [Queue Storage trigger](functions-bindings-storage-queue.md), een blob-opslag-invoer en uitvoer van een blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="2af5a-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="2af5a-210">Gebruik van de kennisgeving Hallo Hallo `queueTrigger` metagegevenseigenschap.</span><span class="sxs-lookup"><span data-stu-id="2af5a-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="2af5a-211">in de blob Hallo invoer en uitvoer `path` eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="2af5a-211">in hello blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="2af5a-212">Zie Hallo taalspecifieke steekproef die het Hallo blob-invoerbron toohello uitvoer blob kopieert.</span><span class="sxs-lookup"><span data-stu-id="2af5a-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="2af5a-213">C#</span><span class="sxs-lookup"><span data-stu-id="2af5a-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="2af5a-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="2af5a-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="2af5a-215">Voorbeeld van BLOB-binding in C#</span><span class="sxs-lookup"><span data-stu-id="2af5a-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="2af5a-216">Voorbeeld van BLOB-binding in Node.js</span><span class="sxs-lookup"><span data-stu-id="2af5a-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="2af5a-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2af5a-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

