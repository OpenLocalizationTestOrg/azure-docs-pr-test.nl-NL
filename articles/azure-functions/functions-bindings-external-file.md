---
title: aaaAzure-bestand met externe functies Bindingen (Preview) | Microsoft Docs
description: Met behulp van extern bestand bindingen in de Azure-functies
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="f900a-103">Azure Functions-bestand met externe Bindingen (Preview)</span><span class="sxs-lookup"><span data-stu-id="f900a-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="f900a-104">Dit artikel laat zien hoe toomanipulate bestanden van verschillende SaaS providers (zoals OneDrive, Dropbox) in de functie met behulp van de ingebouwde bindingen.</span><span class="sxs-lookup"><span data-stu-id="f900a-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="f900a-105">Azure functions ondersteunt activeren, invoer en uitvoer van de bindingen voor extern bestand.</span><span class="sxs-lookup"><span data-stu-id="f900a-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="f900a-106">Deze binding API verbindingen tooSaaS providers maakt of bestaande API-verbindingen van de resourcegroep van de functie-App wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f900a-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="f900a-107">Ondersteunde bestand-verbindingen</span><span class="sxs-lookup"><span data-stu-id="f900a-107">Supported File connections</span></span>

|<span data-ttu-id="f900a-108">Connector</span><span class="sxs-lookup"><span data-stu-id="f900a-108">Connector</span></span>|<span data-ttu-id="f900a-109">Trigger</span><span class="sxs-lookup"><span data-stu-id="f900a-109">Trigger</span></span>|<span data-ttu-id="f900a-110">Invoer</span><span class="sxs-lookup"><span data-stu-id="f900a-110">Input</span></span>|<span data-ttu-id="f900a-111">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="f900a-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="f900a-112">Vak</span><span class="sxs-lookup"><span data-stu-id="f900a-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="f900a-113">x</span><span class="sxs-lookup"><span data-stu-id="f900a-113">x</span></span>|<span data-ttu-id="f900a-114">x</span><span class="sxs-lookup"><span data-stu-id="f900a-114">x</span></span>|<span data-ttu-id="f900a-115">x</span><span class="sxs-lookup"><span data-stu-id="f900a-115">x</span></span>
|[<span data-ttu-id="f900a-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="f900a-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="f900a-117">x</span><span class="sxs-lookup"><span data-stu-id="f900a-117">x</span></span>|<span data-ttu-id="f900a-118">x</span><span class="sxs-lookup"><span data-stu-id="f900a-118">x</span></span>|<span data-ttu-id="f900a-119">x</span><span class="sxs-lookup"><span data-stu-id="f900a-119">x</span></span>
|[<span data-ttu-id="f900a-120">FTP</span><span class="sxs-lookup"><span data-stu-id="f900a-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="f900a-121">x</span><span class="sxs-lookup"><span data-stu-id="f900a-121">x</span></span>|<span data-ttu-id="f900a-122">x</span><span class="sxs-lookup"><span data-stu-id="f900a-122">x</span></span>|<span data-ttu-id="f900a-123">x</span><span class="sxs-lookup"><span data-stu-id="f900a-123">x</span></span>
|[<span data-ttu-id="f900a-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="f900a-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="f900a-125">x</span><span class="sxs-lookup"><span data-stu-id="f900a-125">x</span></span>|<span data-ttu-id="f900a-126">x</span><span class="sxs-lookup"><span data-stu-id="f900a-126">x</span></span>|<span data-ttu-id="f900a-127">x</span><span class="sxs-lookup"><span data-stu-id="f900a-127">x</span></span>
|[<span data-ttu-id="f900a-128">OneDrive voor Bedrijven</span><span class="sxs-lookup"><span data-stu-id="f900a-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="f900a-129">x</span><span class="sxs-lookup"><span data-stu-id="f900a-129">x</span></span>|<span data-ttu-id="f900a-130">x</span><span class="sxs-lookup"><span data-stu-id="f900a-130">x</span></span>|<span data-ttu-id="f900a-131">x</span><span class="sxs-lookup"><span data-stu-id="f900a-131">x</span></span>
|[<span data-ttu-id="f900a-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="f900a-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="f900a-133">x</span><span class="sxs-lookup"><span data-stu-id="f900a-133">x</span></span>|<span data-ttu-id="f900a-134">x</span><span class="sxs-lookup"><span data-stu-id="f900a-134">x</span></span>|<span data-ttu-id="f900a-135">x</span><span class="sxs-lookup"><span data-stu-id="f900a-135">x</span></span>
|[<span data-ttu-id="f900a-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="f900a-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="f900a-137">x</span><span class="sxs-lookup"><span data-stu-id="f900a-137">x</span></span>|<span data-ttu-id="f900a-138">x</span><span class="sxs-lookup"><span data-stu-id="f900a-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="f900a-139">Externe verbindingen van het bestand kunnen ook worden gebruikt [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="f900a-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="f900a-140">Bestand met externe binding activeren</span><span class="sxs-lookup"><span data-stu-id="f900a-140">External File trigger binding</span></span>

<span data-ttu-id="f900a-141">Hello Azure extern bestand trigger kunt u een externe map bewaken en de functiecode uitvoeren als er wijzigingen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="f900a-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="f900a-142">Hallo-bestand met externe trigger gebruikt Hallo volgende JSON-objecten in Hallo `bindings` matrix van function.json</span><span class="sxs-lookup"><span data-stu-id="f900a-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="f900a-143">Bestandsnaampatronen</span><span class="sxs-lookup"><span data-stu-id="f900a-143">Name patterns</span></span>
<span data-ttu-id="f900a-144">U kunt een bestandsnaampatroon opgeven in Hallo `path` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f900a-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="f900a-145">Hallo-map waarnaar wordt verwezen, moet bestaan in Hallo SaaS-provider.</span><span class="sxs-lookup"><span data-stu-id="f900a-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="f900a-146">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="f900a-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="f900a-147">Dit pad wilt zoeken naar een bestand met de naam *oorspronkelijke Bestand1.txt* in Hallo *invoer* map en de waarde Hallo Hallo `name` variabele in functiecode zou worden `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="f900a-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="f900a-148">Nog een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f900a-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="f900a-149">Dit pad zou ook een bestand met de naam vinden *oorspronkelijke Bestand1.txt*, en de waarde van Hallo Hallo `filename` en `fileextension` variabelen in de functiecode zou worden *oorspronkelijke File1* en  *txt*.</span><span class="sxs-lookup"><span data-stu-id="f900a-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="f900a-150">U kunt bestandstype Hallo van bestanden met behulp van een vaste waarde voor de bestandsextensie Hallo beperken.</span><span class="sxs-lookup"><span data-stu-id="f900a-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="f900a-151">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f900a-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="f900a-152">In dit geval wordt alleen *PNG* bestanden in Hallo *voorbeelden* map Hallo activeringsfunctie.</span><span class="sxs-lookup"><span data-stu-id="f900a-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="f900a-153">Accolades zijn speciale tekens in de naam van patronen.</span><span class="sxs-lookup"><span data-stu-id="f900a-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="f900a-154">bestandsnamen toospecify die accolades in Hallo-naam, dubbele Hallo accolades hebben.</span><span class="sxs-lookup"><span data-stu-id="f900a-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="f900a-155">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f900a-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="f900a-156">Dit pad wilt zoeken naar een bestand met de naam *{20140101}-soundfile.mp3* in Hallo *installatiekopieën* map en Hallo `name` variabele waarde in de functiecode Hallo *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="f900a-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="f900a-157">Verwerken van verontreinigde bestanden</span><span class="sxs-lookup"><span data-stu-id="f900a-157">Handling poison files</span></span>
<span data-ttu-id="f900a-158">Als er een extern bestand activeringsfunctie uitvalt, probeert Azure Functions die functie van too5 tijden opnieuw standaard (inclusief de eerste poging Hallo) voor een bepaald bestand.</span><span class="sxs-lookup"><span data-stu-id="f900a-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="f900a-159">Als alle 5 pogingen mislukken, functies wordt toegevoegd een tooa opslag berichtenwachtrij met de naam *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="f900a-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="f900a-160">Hallo-bericht van wachtrij voor verontreinigde bestanden is een JSON-object met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="f900a-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="f900a-161">FunctionId (Hallo indeling  *&lt;functie app-naam >*. Functies.  *&lt;functienaam >*)</span><span class="sxs-lookup"><span data-stu-id="f900a-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="f900a-162">Bestandstype</span><span class="sxs-lookup"><span data-stu-id="f900a-162">FileType</span></span>
* <span data-ttu-id="f900a-163">Mapnaam</span><span class="sxs-lookup"><span data-stu-id="f900a-163">FolderName</span></span>
* <span data-ttu-id="f900a-164">Bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="f900a-164">FileName</span></span>
* <span data-ttu-id="f900a-165">ETag (een bestand versie-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="f900a-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="f900a-166">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="f900a-166">Trigger usage</span></span>
<span data-ttu-id="f900a-167">In de C# functies, bindt u toohello invoerbestand gegevens met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="f900a-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="f900a-168">Waar `T` is Hallo gegevenstype dat u wilt dat toodeserialize Hallo gegevens in, en `paramName` Hallo-naam die u hebt opgegeven in de [activeert JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="f900a-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="f900a-169">In een Node.js-functies, opent u Hallo invoerbestand gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f900a-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f900a-170">Hallo-bestand kan worden gedeserialiseerd in een van de volgende typen Hallo:</span><span class="sxs-lookup"><span data-stu-id="f900a-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="f900a-171">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-geserialiseerd bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="f900a-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="f900a-172">Als u een aangepaste invoertype declareren (bijvoorbeeld `FooType`), Azure Functions probeert toodeserialize Hallo JSON-gegevens in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="f900a-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="f900a-173">Tekenreeks - nuttig voor tekst-bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="f900a-173">String - useful for text file data.</span></span>

<span data-ttu-id="f900a-174">In C#-functies, kunt u ook tooany van de volgende typen Hallo binden en Hallo functies runtime probeert te deserialiseren Hallo bestandsgegevens met behulp van dat type:</span><span class="sxs-lookup"><span data-stu-id="f900a-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="f900a-175">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="f900a-175">Trigger sample</span></span>
<span data-ttu-id="f900a-176">Stel dat u hebt na function.json hello, definieert die de trigger van een extern bestand:</span><span class="sxs-lookup"><span data-stu-id="f900a-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="f900a-177">Zie Hallo taalspecifieke steekproef die het Hallo-inhoud van elk bestand dat wordt toegevoegd toohello bewaakte map registreert.</span><span class="sxs-lookup"><span data-stu-id="f900a-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="f900a-178">C#</span><span class="sxs-lookup"><span data-stu-id="f900a-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="f900a-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="f900a-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="f900a-180">Gebruik van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="f900a-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="f900a-181">Gebruik van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="f900a-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="f900a-182">Bestand met externe invoer binding</span><span class="sxs-lookup"><span data-stu-id="f900a-182">External File input binding</span></span>
<span data-ttu-id="f900a-183">Hello Azure extern bestand invoer binding kunt u een bestand vanaf een externe map in de functie toouse.</span><span class="sxs-lookup"><span data-stu-id="f900a-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="f900a-184">Hallo-bestand met externe invoer tooa functie maakt gebruik van volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="f900a-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="f900a-185">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f900a-185">Note hello following:</span></span>

* <span data-ttu-id="f900a-186">`path`moet de naam van de map Hallo en Hallo-bestandsnaam bevatten.</span><span class="sxs-lookup"><span data-stu-id="f900a-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="f900a-187">Als u hebt bijvoorbeeld een [wachtrij trigger](functions-bindings-storage-queue.md) in de functie, kunt u `"path": "samples-workitems/{queueTrigger}"` toopoint tooa bestand in Hallo `samples-workitems` map met een naam die overeenkomt met Hallo-bestandsnaam is opgegeven in de trigger het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="f900a-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="f900a-188">Invoer-gebruik</span><span class="sxs-lookup"><span data-stu-id="f900a-188">Input usage</span></span>
<span data-ttu-id="f900a-189">In de C# functies, bindt u toohello invoerbestand gegevens met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="f900a-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="f900a-190">Waar `T` is Hallo gegevenstype dat u wilt dat toodeserialize Hallo gegevens in, en `paramName` Hallo-naam die u hebt opgegeven in de [invoer binding](#input).</span><span class="sxs-lookup"><span data-stu-id="f900a-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="f900a-191">In een Node.js-functies, opent u Hallo invoerbestand gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f900a-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f900a-192">Hallo-bestand kan worden gedeserialiseerd in een van de volgende typen Hallo:</span><span class="sxs-lookup"><span data-stu-id="f900a-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="f900a-193">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-geserialiseerd bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="f900a-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="f900a-194">Als u een aangepaste invoertype declareren (bijvoorbeeld `InputType`), Azure Functions probeert toodeserialize Hallo JSON-gegevens in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="f900a-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="f900a-195">Tekenreeks - nuttig voor tekst-bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="f900a-195">String - useful for text file data.</span></span>

<span data-ttu-id="f900a-196">In C#-functies, kunt u ook tooany van de volgende typen Hallo binden en Hallo functies runtime probeert te deserialiseren Hallo bestandsgegevens met behulp van dat type:</span><span class="sxs-lookup"><span data-stu-id="f900a-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="f900a-197">Bestand met externe uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="f900a-197">External File output binding</span></span>
<span data-ttu-id="f900a-198">Hello Azure-bestand met externe uitvoer binding kunt u toowrite bestanden tooan externe map in de functie.</span><span class="sxs-lookup"><span data-stu-id="f900a-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="f900a-199">Hallo-bestand met externe uitvoer voor een functie maakt gebruik van volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="f900a-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="f900a-200">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f900a-200">Note hello following:</span></span>

* <span data-ttu-id="f900a-201">`path`moet Hallo mapnaam en Hallo bestand naam toowrite te bevatten.</span><span class="sxs-lookup"><span data-stu-id="f900a-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="f900a-202">Als u hebt bijvoorbeeld een [wachtrij trigger](functions-bindings-storage-queue.md) in de functie, kunt u `"path": "samples-workitems/{queueTrigger}"` toopoint tooa bestand in Hallo `samples-workitems` map met een naam die overeenkomt met Hallo-bestandsnaam is opgegeven in de trigger het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="f900a-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="f900a-203">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="f900a-203">Output usage</span></span>
<span data-ttu-id="f900a-204">In de C# functies, bindt u toohello uitvoerbestand door gebruik te maken met de naam Hallo `out` parameter in de functiehandtekening, zoals `out <T> <name>`, waarbij `T` is Hallo gegevenstype dat u wilt dat tooserialize Hallo gegevens in, en `paramName` is Hallo servernaam die u hebt opgegeven in de [uitvoer binding](#output).</span><span class="sxs-lookup"><span data-stu-id="f900a-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="f900a-205">In een Node.js-functies, opent u Hallo uitvoer-bestand met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f900a-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f900a-206">U kunt schrijven toohello uitvoerbestand met behulp van een Hallo volgende typen:</span><span class="sxs-lookup"><span data-stu-id="f900a-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="f900a-207">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="f900a-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="f900a-208">Als u een aangepaste uitvoertype declareren (bijvoorbeeld `out OutputType paramName`), Azure Functions probeert tooserialize object naar JSON.</span><span class="sxs-lookup"><span data-stu-id="f900a-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="f900a-209">Als bij het verlaten van de functie Hallo Hallo output-parameter null is, maakt Hallo Functions-runtime-bestand als een null-object.</span><span class="sxs-lookup"><span data-stu-id="f900a-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="f900a-210">String - (`out string paramName`) nuttig voor tekst-bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="f900a-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="f900a-211">Hallo functies runtime maakt een bestand alleen als de tekenreeksparameter niet-null is bij het Hallo-functie wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="f900a-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="f900a-212">U kunt ook tooany van de volgende typen Hallo in C#-functies uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f900a-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="f900a-213">Invoer en uitvoer-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="f900a-213">Input + Output sample</span></span>
<span data-ttu-id="f900a-214">Stel dat u hebt na function.json hello, die definieert een [opslag wachtrij trigger](functions-bindings-storage-queue.md), voert u een extern bestand en een bestand met externe uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f900a-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="f900a-215">Zie Hallo taalspecifieke steekproef die het Hallo invoerbestand toohello uitvoerbestand kopieert.</span><span class="sxs-lookup"><span data-stu-id="f900a-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="f900a-216">C#</span><span class="sxs-lookup"><span data-stu-id="f900a-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="f900a-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="f900a-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="f900a-218">Gebruik in C#</span><span class="sxs-lookup"><span data-stu-id="f900a-218">Usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a><span data-ttu-id="f900a-219">Gebruik in Node.js</span><span class="sxs-lookup"><span data-stu-id="f900a-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="f900a-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f900a-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
