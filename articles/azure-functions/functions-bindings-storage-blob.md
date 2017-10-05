---
title: Azure Functions Blob Storage-bindingen | Microsoft Docs
description: Het gebruik van Azure Storage-triggers en bindingen in de Azure Functions begrijpen.
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
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="ba960-104">Azure Functions Blob storage-bindingen</span><span class="sxs-lookup"><span data-stu-id="ba960-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ba960-105">In dit artikel wordt uitgelegd hoe configureren en werken met Azure Blob storage bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ba960-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="ba960-106">Azure Functions ondersteunt worden geactiveerd, invoer en uitvoer van de bindingen voor Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ba960-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="ba960-107">Zie functies die beschikbaar in alle bindingen zijn [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="ba960-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="ba960-108">Een [blob storage-account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ba960-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="ba960-109">BLOB storage triggers en bindingen vereisen een algemeen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ba960-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="ba960-110">BLOB storage triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="ba960-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="ba960-111">Met behulp van de Azure Blob storage-trigger wordt uw functiecode aangeroepen wanneer een nieuwe of bijgewerkte blob wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="ba960-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="ba960-112">De blobinhoud worden geleverd als invoer voor de functie.</span><span class="sxs-lookup"><span data-stu-id="ba960-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="ba960-113">Definieer een blob storage trigger met de **integreren** tabblad in de portal functies.</span><span class="sxs-lookup"><span data-stu-id="ba960-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="ba960-114">De portal maakt de volgende definitie in de **bindingen** sectie van *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ba960-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="ba960-115">BLOB-invoer en uitvoer bindingen zijn gedefinieerd met behulp van `blob` als het bindingstype:</span><span class="sxs-lookup"><span data-stu-id="ba960-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="ba960-116">De `path` ondersteunt de eigenschap binding expressies en filterparameters.</span><span class="sxs-lookup"><span data-stu-id="ba960-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="ba960-117">Zie [patronen naam](#pattern).</span><span class="sxs-lookup"><span data-stu-id="ba960-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="ba960-118">De `connection` eigenschap moet bevatten de naam van een app-instelling met een verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="ba960-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ba960-119">In de Azure portal, de standaard editor in de **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="ba960-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="ba960-120">Wanneer u een blob-trigger op een plan verbruik, kunnen er maximaal 10 minuten vertraging bij de verwerking van nieuwe blobs nadat een functie-app niet actief is geworden.</span><span class="sxs-lookup"><span data-stu-id="ba960-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="ba960-121">Nadat de functie-app wordt uitgevoerd, worden onmiddellijk blobs verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ba960-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="ba960-122">Overweeg om te voorkomen dat deze initiële vertraging, een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="ba960-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="ba960-123">Gebruik een App Service-abonnement met altijd op ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ba960-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="ba960-124">Gebruik een ander mechanisme voor het activeren van de blob verwerken, zoals een wachtrijbericht met de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="ba960-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="ba960-125">Zie voor een voorbeeld [wachtrij trigger met blob invoer binding](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="ba960-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="ba960-126">Bestandsnaampatronen</span><span class="sxs-lookup"><span data-stu-id="ba960-126">Name patterns</span></span>
<span data-ttu-id="ba960-127">U kunt opgeven dat een naampatroon blob in de `path` eigenschap, die een filter of binding-expressie.</span><span class="sxs-lookup"><span data-stu-id="ba960-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="ba960-128">Zie [Binding expressies en patronen](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="ba960-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="ba960-129">Bijvoorbeeld als u wilt filteren op blobs die met de tekenreeks 'oorspronkelijke beginnen', gebruiken de volgende definitie.</span><span class="sxs-lookup"><span data-stu-id="ba960-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="ba960-130">Dit pad zoeken naar een blob met de naam *oorspronkelijke Blob1.txt* in de *invoer* container en de waarde van de `name` variabele in functiecode is `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="ba960-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="ba960-131">Als u wilt koppelen aan de blob-bestandsnaam en de extensie afzonderlijk, gebruikmaken van twee patronen.</span><span class="sxs-lookup"><span data-stu-id="ba960-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="ba960-132">Dit pad ook zoeken naar een blob met de naam *oorspronkelijke Blob1.txt*, en de waarde van de `blobname` en `blobextension` variabelen in de functiecode zijn *oorspronkelijke Blob1* en *txt*.</span><span class="sxs-lookup"><span data-stu-id="ba960-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="ba960-133">U kunt het bestandstype blobs beperken met behulp van een vaste waarde voor de bestandsextensie.</span><span class="sxs-lookup"><span data-stu-id="ba960-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="ba960-134">Gebruik bijvoorbeeld het volgende patroon volgen zodat alleen op PNG-bestanden:</span><span class="sxs-lookup"><span data-stu-id="ba960-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="ba960-135">Accolades zijn speciale tekens in de naam van patronen.</span><span class="sxs-lookup"><span data-stu-id="ba960-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="ba960-136">Voor blob-namen die accolades hebben met de naam opgeeft, kunt u de accolades met behulp van twee accolades escape.</span><span class="sxs-lookup"><span data-stu-id="ba960-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="ba960-137">Het volgende voorbeeld wordt gezocht naar een blob met de naam *{20140101}-soundfile.mp3* in de *installatiekopieën* -container, en de `name` variabele waarde in de functiecode *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="ba960-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="ba960-138">Trigger metagegevens</span><span class="sxs-lookup"><span data-stu-id="ba960-138">Trigger metadata</span></span>

<span data-ttu-id="ba960-139">De blob-trigger biedt verschillende eigenschappen voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="ba960-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="ba960-140">Deze eigenschappen kunnen worden gebruikt als onderdeel van de expressies bindingen in andere bindingen of als parameters in uw code.</span><span class="sxs-lookup"><span data-stu-id="ba960-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="ba960-141">Deze waarden hebben dezelfde betekenis als [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="ba960-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="ba960-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="ba960-142">**BlobTrigger**.</span></span> <span data-ttu-id="ba960-143">Typ `string`.</span><span class="sxs-lookup"><span data-stu-id="ba960-143">Type `string`.</span></span> <span data-ttu-id="ba960-144">Het activerende blobpad</span><span class="sxs-lookup"><span data-stu-id="ba960-144">The triggering blob path</span></span>
- <span data-ttu-id="ba960-145">**URI**.</span><span class="sxs-lookup"><span data-stu-id="ba960-145">**Uri**.</span></span> <span data-ttu-id="ba960-146">Typ `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="ba960-146">Type `System.Uri`.</span></span> <span data-ttu-id="ba960-147">De blob-URI voor de primaire locatie.</span><span class="sxs-lookup"><span data-stu-id="ba960-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="ba960-148">**Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ba960-148">**Properties**.</span></span> <span data-ttu-id="ba960-149">Typ `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="ba960-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="ba960-150">Eigenschappen van de blob.</span><span class="sxs-lookup"><span data-stu-id="ba960-150">The blob's system properties.</span></span>
- <span data-ttu-id="ba960-151">**Metagegevens**.</span><span class="sxs-lookup"><span data-stu-id="ba960-151">**Metadata**.</span></span> <span data-ttu-id="ba960-152">Typ `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="ba960-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="ba960-153">De gebruiker gedefinieerde metagegevens voor de blob.</span><span class="sxs-lookup"><span data-stu-id="ba960-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="ba960-154">BLOB ontvangstbevestigingen</span><span class="sxs-lookup"><span data-stu-id="ba960-154">Blob receipts</span></span>
<span data-ttu-id="ba960-155">De Azure Functions-runtime zorgt ervoor dat er is geen blob-activeringsfunctie meer dan één keer wordt aangeroepen voor de dezelfde nieuwe of bijgewerkte blob.</span><span class="sxs-lookup"><span data-stu-id="ba960-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="ba960-156">Om te bepalen of een versie van de opgegeven blob is verwerkt, wordt bijgehouden *blob ontvangstbevestigingen*.</span><span class="sxs-lookup"><span data-stu-id="ba960-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="ba960-157">Azure Functions winkels blob ontvangstbevestigingen in een container met de naam *webjobs-azure-hosts* in de Azure storage-account voor de functie-app (gedefinieerd door de app-instelling `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="ba960-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="ba960-158">De ontvangst van een blob heeft de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="ba960-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="ba960-159">De geactiveerde functie ('*&lt;functie app-naam >*. Functies.  *&lt;functienaam >*', bijvoorbeeld: 'MyFunctionApp.Functions.CopyBlob')</span><span class="sxs-lookup"><span data-stu-id="ba960-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="ba960-160">De containernaam</span><span class="sxs-lookup"><span data-stu-id="ba960-160">The container name</span></span>
* <span data-ttu-id="ba960-161">Het blobtype ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="ba960-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ba960-162">De blob-naam</span><span class="sxs-lookup"><span data-stu-id="ba960-162">The blob name</span></span>
* <span data-ttu-id="ba960-163">De ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="ba960-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="ba960-164">Verwijder de ontvangst van de blob voor blob uit om af te dwingen opnieuw verwerken van een blob, de *webjobs-azure-hosts* container handmatig.</span><span class="sxs-lookup"><span data-stu-id="ba960-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="ba960-165">Verwerken van verontreinigde blobs</span><span class="sxs-lookup"><span data-stu-id="ba960-165">Handling poison blobs</span></span>
<span data-ttu-id="ba960-166">Als een functie van de trigger blob is mislukt voor een bepaalde functies van Azure-blob pogingen die een totaal van 5 maal standaard functioneren.</span><span class="sxs-lookup"><span data-stu-id="ba960-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="ba960-167">Als alle 5 pogingen mislukken, wordt een bericht met Azure Functions toegevoegd aan een opslagwachtrij met de naam *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="ba960-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="ba960-168">Bericht uit de wachtrij voor verontreinigde blobs is een JSON-object met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ba960-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="ba960-169">FunctionId (in de notatie  *&lt;functie app-naam >*. Functies.  *&lt;functienaam >*)</span><span class="sxs-lookup"><span data-stu-id="ba960-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="ba960-170">BlobType ('BlockBlob' of 'PageBlob')</span><span class="sxs-lookup"><span data-stu-id="ba960-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ba960-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="ba960-171">ContainerName</span></span>
* <span data-ttu-id="ba960-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="ba960-172">BlobName</span></span>
* <span data-ttu-id="ba960-173">ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="ba960-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="ba960-174">Er wordt gedelegeerd voor grote containers BLOB</span><span class="sxs-lookup"><span data-stu-id="ba960-174">Blob polling for large containers</span></span>
<span data-ttu-id="ba960-175">Als de blob-container die wordt bewaakt meer dan 10.000 blobs bevat, logboekbestanden de functies runtime scans moeten worden gecontroleerd voor nieuwe of gewijzigde blobs.</span><span class="sxs-lookup"><span data-stu-id="ba960-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="ba960-176">Dit proces is niet realtime.</span><span class="sxs-lookup"><span data-stu-id="ba960-176">This process is not real time.</span></span> <span data-ttu-id="ba960-177">Een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat de blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ba960-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="ba960-178">Bovendien [opslag logboeken worden gemaakt op een 'best effort'](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span><span class="sxs-lookup"><span data-stu-id="ba960-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="ba960-179">Er is geen garantie dat alle gebeurtenissen worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="ba960-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="ba960-180">Onder bepaalde omstandigheden wellicht Logboeken niet opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ba960-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="ba960-181">Als u sneller of betrouwbaarder blob verwerking vereist, kunt u een [wachtrijbericht](../storage/queues/storage-dotnet-how-to-use-queues.md) bij het maken van de blob.</span><span class="sxs-lookup"><span data-stu-id="ba960-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="ba960-182">Vervolgens gebruikt u een [wachtrij trigger](functions-bindings-storage-queue.md) in plaats van een blob-trigger voor het verwerken van de blob.</span><span class="sxs-lookup"><span data-stu-id="ba960-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="ba960-183">Met behulp van een blob-trigger en invoer binding</span><span class="sxs-lookup"><span data-stu-id="ba960-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="ba960-184">In .NET-functies, toegang tot de blobgegevens met een parameter van de methode, zoals `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="ba960-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="ba960-185">Hier `paramName` is de waarde die u hebt opgegeven in de [trigger configuratie](#trigger).</span><span class="sxs-lookup"><span data-stu-id="ba960-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="ba960-186">Toegang tot de blob-invoerbron gegevens in Node.js-functies, `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="ba960-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ba960-187">U kunt in .NET binden aan een van de typen in de onderstaande lijst.</span><span class="sxs-lookup"><span data-stu-id="ba960-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="ba960-188">Als gebruikt als een invoer-binding, is enkele van deze typen vereisen een `inout` richting in binding *function.json*.</span><span class="sxs-lookup"><span data-stu-id="ba960-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="ba960-189">Deze richting wordt niet ondersteund door de standard-editor, zodat u de geavanceerde editor moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ba960-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="ba960-190">`ICloudBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="ba960-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ba960-191">`CloudBlockBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="ba960-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ba960-192">`CloudPageBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="ba960-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ba960-193">`CloudAppendBlob`('inout' binding richting vereist)</span><span class="sxs-lookup"><span data-stu-id="ba960-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="ba960-194">Als tekst blobs worden verwacht, kunt u ook binden aan een .NET `string` type.</span><span class="sxs-lookup"><span data-stu-id="ba960-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="ba960-195">Dit wordt alleen aanbevolen als de Blobgrootte van de klein is als de volledige blobinhoud in het geheugen geladen.</span><span class="sxs-lookup"><span data-stu-id="ba960-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="ba960-196">In het algemeen is het raadzaam om het gebruik van een `Stream` of `CloudBlockBlob` type.</span><span class="sxs-lookup"><span data-stu-id="ba960-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="ba960-197">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="ba960-197">Trigger sample</span></span>
<span data-ttu-id="ba960-198">Stel dat u hebt de volgende function.json die de trigger van een blob-opslag definieert:</span><span class="sxs-lookup"><span data-stu-id="ba960-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="ba960-199">Zie het voorbeeld taalspecifieke waarmee de inhoud van elke blob die wordt toegevoegd aan de bewaakte container zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="ba960-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="ba960-200">C#</span><span class="sxs-lookup"><span data-stu-id="ba960-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="ba960-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba960-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="ba960-202">Voorbeelden van BLOB-trigger in C#</span><span class="sxs-lookup"><span data-stu-id="ba960-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="ba960-203">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="ba960-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="ba960-204">Binding met een blob uitvoer</span><span class="sxs-lookup"><span data-stu-id="ba960-204">Using a blob output binding</span></span>

<span data-ttu-id="ba960-205">.NET-functies, moet u gebruiken een `out string` parameter in uw functiehandtekening of gebruik een van de typen in de volgende lijst.</span><span class="sxs-lookup"><span data-stu-id="ba960-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="ba960-206">In een Node.js-functies, opent u de uitvoer-blob via `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="ba960-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ba960-207">In de .NET-functies kunt u uitvoeren met een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="ba960-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="ba960-208">Wachtrij-trigger met blob-invoer en uitvoer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ba960-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="ba960-209">Stel dat u hebt de volgende function.json, die definieert een [Queue Storage trigger](functions-bindings-storage-queue.md), een blob-opslag-invoer en uitvoer van een blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ba960-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="ba960-210">Let op het gebruik van de `queueTrigger` metagegevenseigenschap.</span><span class="sxs-lookup"><span data-stu-id="ba960-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="ba960-211">in de blob-invoer en uitvoer `path` eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ba960-211">in the blob input and output `path` properties:</span></span>

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

<span data-ttu-id="ba960-212">Zie het voorbeeld taalspecifieke waarmee de blob-invoerbron worden gekopieerd naar de uitvoer-blob.</span><span class="sxs-lookup"><span data-stu-id="ba960-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="ba960-213">C#</span><span class="sxs-lookup"><span data-stu-id="ba960-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="ba960-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba960-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="ba960-215">Voorbeeld van BLOB-binding in C#</span><span class="sxs-lookup"><span data-stu-id="ba960-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="ba960-216">Voorbeeld van BLOB-binding in Node.js</span><span class="sxs-lookup"><span data-stu-id="ba960-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ba960-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba960-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

