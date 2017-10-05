---
title: Azure Functions-bestand met externe Bindingen (Preview) | Microsoft Docs
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
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="33efb-103">Azure Functions-bestand met externe Bindingen (Preview)</span><span class="sxs-lookup"><span data-stu-id="33efb-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="33efb-104">Dit artikel laat zien hoe u kunt bestanden van verschillende aanbieders van SaaS (zoals OneDrive, Dropbox) bewerken binnen de functie met behulp van de ingebouwde bindingen.</span><span class="sxs-lookup"><span data-stu-id="33efb-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="33efb-105">Azure functions ondersteunt activeren, invoer en uitvoer van de bindingen voor extern bestand.</span><span class="sxs-lookup"><span data-stu-id="33efb-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="33efb-106">Deze binding API-verbindingen met SaaS-providers maakt of bestaande API-verbindingen van de resourcegroep van de functie-App wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="33efb-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="33efb-107">Ondersteunde bestand-verbindingen</span><span class="sxs-lookup"><span data-stu-id="33efb-107">Supported File connections</span></span>

|<span data-ttu-id="33efb-108">Connector</span><span class="sxs-lookup"><span data-stu-id="33efb-108">Connector</span></span>|<span data-ttu-id="33efb-109">Trigger</span><span class="sxs-lookup"><span data-stu-id="33efb-109">Trigger</span></span>|<span data-ttu-id="33efb-110">Invoer</span><span class="sxs-lookup"><span data-stu-id="33efb-110">Input</span></span>|<span data-ttu-id="33efb-111">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="33efb-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="33efb-112">Vak</span><span class="sxs-lookup"><span data-stu-id="33efb-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="33efb-113">x</span><span class="sxs-lookup"><span data-stu-id="33efb-113">x</span></span>|<span data-ttu-id="33efb-114">x</span><span class="sxs-lookup"><span data-stu-id="33efb-114">x</span></span>|<span data-ttu-id="33efb-115">x</span><span class="sxs-lookup"><span data-stu-id="33efb-115">x</span></span>
|[<span data-ttu-id="33efb-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="33efb-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="33efb-117">x</span><span class="sxs-lookup"><span data-stu-id="33efb-117">x</span></span>|<span data-ttu-id="33efb-118">x</span><span class="sxs-lookup"><span data-stu-id="33efb-118">x</span></span>|<span data-ttu-id="33efb-119">x</span><span class="sxs-lookup"><span data-stu-id="33efb-119">x</span></span>
|[<span data-ttu-id="33efb-120">FTP</span><span class="sxs-lookup"><span data-stu-id="33efb-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="33efb-121">x</span><span class="sxs-lookup"><span data-stu-id="33efb-121">x</span></span>|<span data-ttu-id="33efb-122">x</span><span class="sxs-lookup"><span data-stu-id="33efb-122">x</span></span>|<span data-ttu-id="33efb-123">x</span><span class="sxs-lookup"><span data-stu-id="33efb-123">x</span></span>
|[<span data-ttu-id="33efb-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="33efb-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="33efb-125">x</span><span class="sxs-lookup"><span data-stu-id="33efb-125">x</span></span>|<span data-ttu-id="33efb-126">x</span><span class="sxs-lookup"><span data-stu-id="33efb-126">x</span></span>|<span data-ttu-id="33efb-127">x</span><span class="sxs-lookup"><span data-stu-id="33efb-127">x</span></span>
|[<span data-ttu-id="33efb-128">OneDrive voor Bedrijven</span><span class="sxs-lookup"><span data-stu-id="33efb-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="33efb-129">x</span><span class="sxs-lookup"><span data-stu-id="33efb-129">x</span></span>|<span data-ttu-id="33efb-130">x</span><span class="sxs-lookup"><span data-stu-id="33efb-130">x</span></span>|<span data-ttu-id="33efb-131">x</span><span class="sxs-lookup"><span data-stu-id="33efb-131">x</span></span>
|[<span data-ttu-id="33efb-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="33efb-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="33efb-133">x</span><span class="sxs-lookup"><span data-stu-id="33efb-133">x</span></span>|<span data-ttu-id="33efb-134">x</span><span class="sxs-lookup"><span data-stu-id="33efb-134">x</span></span>|<span data-ttu-id="33efb-135">x</span><span class="sxs-lookup"><span data-stu-id="33efb-135">x</span></span>
|[<span data-ttu-id="33efb-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="33efb-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="33efb-137">x</span><span class="sxs-lookup"><span data-stu-id="33efb-137">x</span></span>|<span data-ttu-id="33efb-138">x</span><span class="sxs-lookup"><span data-stu-id="33efb-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="33efb-139">Externe verbindingen van het bestand kunnen ook worden gebruikt [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="33efb-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="33efb-140">Bestand met externe binding activeren</span><span class="sxs-lookup"><span data-stu-id="33efb-140">External File trigger binding</span></span>

<span data-ttu-id="33efb-141">De trigger Azure extern bestand kunt u een externe map bewaken en de functiecode uitvoeren als er wijzigingen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="33efb-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="33efb-142">De trigger-bestand met externe gebruikt de volgende JSON-objecten in de `bindings` matrix van function.json</span><span class="sxs-lookup"><span data-stu-id="33efb-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="33efb-143">Bestandsnaampatronen</span><span class="sxs-lookup"><span data-stu-id="33efb-143">Name patterns</span></span>
<span data-ttu-id="33efb-144">U kunt opgeven dat een bestandsnaampatroon in de `path` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="33efb-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="33efb-145">De map waarnaar wordt verwezen, moet bestaan in de SaaS-provider.</span><span class="sxs-lookup"><span data-stu-id="33efb-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="33efb-146">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="33efb-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="33efb-147">Dit pad wilt zoeken naar een bestand met de naam *oorspronkelijke Bestand1.txt* in de *invoer* map en de waarde van de `name` variabele in functiecode zou worden `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="33efb-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="33efb-148">Nog een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33efb-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="33efb-149">Dit pad zou ook een bestand met de naam vinden *oorspronkelijke Bestand1.txt*, en de waarde van de `filename` en `fileextension` variabelen in de functiecode zou worden *oorspronkelijke File1* en *txt* .</span><span class="sxs-lookup"><span data-stu-id="33efb-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="33efb-150">U kunt het type van bestanden beperken met behulp van een vaste waarde voor de bestandsextensie.</span><span class="sxs-lookup"><span data-stu-id="33efb-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="33efb-151">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33efb-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="33efb-152">In dit geval wordt alleen *PNG* bestanden in de *voorbeelden* map activeringsfunctie.</span><span class="sxs-lookup"><span data-stu-id="33efb-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="33efb-153">Accolades zijn speciale tekens in de naam van patronen.</span><span class="sxs-lookup"><span data-stu-id="33efb-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="33efb-154">Dubbelklik om op te geven bestandsnamen die accolades hebben met de naam, de accolades.</span><span class="sxs-lookup"><span data-stu-id="33efb-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="33efb-155">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33efb-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="33efb-156">Dit pad wilt zoeken naar een bestand met de naam *{20140101}-soundfile.mp3* in de *installatiekopieën* map, en de `name` variabele waarde in de functiecode *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="33efb-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="33efb-157">Verwerken van verontreinigde bestanden</span><span class="sxs-lookup"><span data-stu-id="33efb-157">Handling poison files</span></span>
<span data-ttu-id="33efb-158">Wanneer een bestand met externe activeringsfunctie mislukt pogingen Azure Functions die functie maximaal 5 maal standaard (inclusief de eerste poging) voor een bepaald bestand.</span><span class="sxs-lookup"><span data-stu-id="33efb-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="33efb-159">Als alle 5 pogingen mislukken, wordt een bericht met functies toegevoegd aan een opslagwachtrij met de naam *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="33efb-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="33efb-160">Bericht uit de wachtrij voor verontreinigde bestanden is een JSON-object met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="33efb-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="33efb-161">FunctionId (in de notatie  *&lt;functie app-naam >*. Functies.  *&lt;functienaam >*)</span><span class="sxs-lookup"><span data-stu-id="33efb-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="33efb-162">Bestandstype</span><span class="sxs-lookup"><span data-stu-id="33efb-162">FileType</span></span>
* <span data-ttu-id="33efb-163">Mapnaam</span><span class="sxs-lookup"><span data-stu-id="33efb-163">FolderName</span></span>
* <span data-ttu-id="33efb-164">Bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="33efb-164">FileName</span></span>
* <span data-ttu-id="33efb-165">ETag (een bestand versie-id, bijvoorbeeld: '0x8D1DC6E70A277EF')</span><span class="sxs-lookup"><span data-stu-id="33efb-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="33efb-166">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="33efb-166">Trigger usage</span></span>
<span data-ttu-id="33efb-167">In de C# functies, bindt u tot de gegevens van het bestand voor invoer met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="33efb-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="33efb-168">Waar `T` is het gegevenstype dat u wilt deserialiseren van de gegevens in, en `paramName` is de naam die u hebt opgegeven in de [activeert JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="33efb-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="33efb-169">In een Node.js-functies, opent u het invoerbestand gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="33efb-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="33efb-170">Het bestand kan worden gedeserialiseerd in een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="33efb-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="33efb-171">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-geserialiseerd bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="33efb-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="33efb-172">Als u een aangepaste invoertype declareren (bijvoorbeeld `FooType`), Azure Functions geprobeerd te deserialiseren van de JSON-gegevens in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="33efb-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="33efb-173">Tekenreeks - nuttig voor tekst-bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="33efb-173">String - useful for text file data.</span></span>

<span data-ttu-id="33efb-174">U kunt ook binden aan een van de volgende typen in C#-functies, en de runtime van Functions geprobeerd te deserialiseren van de gegevens uit een bestand met behulp van dat type:</span><span class="sxs-lookup"><span data-stu-id="33efb-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="33efb-175">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="33efb-175">Trigger sample</span></span>
<span data-ttu-id="33efb-176">Stel dat u hebt de volgende function.json die de trigger van een extern bestand definieert:</span><span class="sxs-lookup"><span data-stu-id="33efb-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="33efb-177">Zie het voorbeeld taalspecifieke waarmee de inhoud van elk bestand dat wordt toegevoegd aan de bewaakte map zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="33efb-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="33efb-178">C#</span><span class="sxs-lookup"><span data-stu-id="33efb-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="33efb-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="33efb-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="33efb-180">Gebruik van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="33efb-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="33efb-181">Gebruik van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="33efb-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="33efb-182">Bestand met externe invoer binding</span><span class="sxs-lookup"><span data-stu-id="33efb-182">External File input binding</span></span>
<span data-ttu-id="33efb-183">De invoer binding Azure extern bestand kunt u een bestand te gebruiken vanaf een externe map in de functie.</span><span class="sxs-lookup"><span data-stu-id="33efb-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="33efb-184">De invoer van het externe bestand aan een functie maakt gebruik van de volgende JSON-objecten in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="33efb-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="33efb-185">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="33efb-185">Note the following:</span></span>

* <span data-ttu-id="33efb-186">`path`moet de naam van de map en de bestandsnaam bevatten.</span><span class="sxs-lookup"><span data-stu-id="33efb-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="33efb-187">Als u hebt bijvoorbeeld een [wachtrij trigger](functions-bindings-storage-queue.md) in de functie, kunt u `"path": "samples-workitems/{queueTrigger}"` om te verwijzen naar een bestand in de `samples-workitems` map met een naam die overeenkomt met de bestandsnaam in het bericht trigger opgegeven.</span><span class="sxs-lookup"><span data-stu-id="33efb-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="33efb-188">Invoer-gebruik</span><span class="sxs-lookup"><span data-stu-id="33efb-188">Input usage</span></span>
<span data-ttu-id="33efb-189">In de C# functies, bindt u tot de gegevens van het bestand voor invoer met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="33efb-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="33efb-190">Waar `T` is het gegevenstype dat u wilt deserialiseren van de gegevens in, en `paramName` is de naam die u hebt opgegeven in de [invoer binding](#input).</span><span class="sxs-lookup"><span data-stu-id="33efb-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="33efb-191">In een Node.js-functies, opent u het invoerbestand gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="33efb-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="33efb-192">Het bestand kan worden gedeserialiseerd in een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="33efb-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="33efb-193">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-geserialiseerd bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="33efb-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="33efb-194">Als u een aangepaste invoertype declareren (bijvoorbeeld `InputType`), Azure Functions geprobeerd te deserialiseren van de JSON-gegevens in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="33efb-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="33efb-195">Tekenreeks - nuttig voor tekst-bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="33efb-195">String - useful for text file data.</span></span>

<span data-ttu-id="33efb-196">U kunt ook binden aan een van de volgende typen in C#-functies, en de runtime van Functions geprobeerd te deserialiseren van de gegevens uit een bestand met behulp van dat type:</span><span class="sxs-lookup"><span data-stu-id="33efb-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="33efb-197">Bestand met externe uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="33efb-197">External File output binding</span></span>
<span data-ttu-id="33efb-198">De Azure bestand met externe uitvoer binding kunt u bestanden naar een externe map in uw functie te schrijven.</span><span class="sxs-lookup"><span data-stu-id="33efb-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="33efb-199">Het externe bestand uitvoer voor een functie maakt gebruik van de volgende JSON-objecten in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="33efb-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="33efb-200">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="33efb-200">Note the following:</span></span>

* <span data-ttu-id="33efb-201">`path`moet de naam van de map en de naam van het bestand om te schrijven naar bevatten.</span><span class="sxs-lookup"><span data-stu-id="33efb-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="33efb-202">Als u hebt bijvoorbeeld een [wachtrij trigger](functions-bindings-storage-queue.md) in de functie, kunt u `"path": "samples-workitems/{queueTrigger}"` om te verwijzen naar een bestand in de `samples-workitems` map met een naam die overeenkomt met de bestandsnaam in het bericht trigger opgegeven.</span><span class="sxs-lookup"><span data-stu-id="33efb-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="33efb-203">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="33efb-203">Output usage</span></span>
<span data-ttu-id="33efb-204">In de C# functies, bindt u naar het uitvoerbestand met behulp van de benoemde `out` parameter in de functiehandtekening, zoals `out <T> <name>`, waarbij `T` is het gegevenstype dat u wilt serialiseren van de gegevens in, en `paramName` is de naam die u hebt opgegeven in de [uitvoer binding](#output).</span><span class="sxs-lookup"><span data-stu-id="33efb-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="33efb-205">In een Node.js-functies, opent u de uitvoer-bestand met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="33efb-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="33efb-206">U kunt schrijven naar het uitvoerbestand met behulp van een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="33efb-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="33efb-207">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="33efb-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="33efb-208">Als u een aangepaste uitvoertype declareren (bijvoorbeeld `out OutputType paramName`), Azure Functions probeert om object te serialiseren naar JSON.</span><span class="sxs-lookup"><span data-stu-id="33efb-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="33efb-209">Als de output-parameter null is wanneer de functie wordt afgesloten, wordt in de runtime van Functions een bestand gemaakt als een null-object.</span><span class="sxs-lookup"><span data-stu-id="33efb-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="33efb-210">String - (`out string paramName`) nuttig voor tekst-bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="33efb-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="33efb-211">de runtime van Functions maakt een bestand alleen als de tekenreeksparameter niet-null wanneer de functie wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="33efb-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="33efb-212">In C#-functies kunt u ook uitvoeren met een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="33efb-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="33efb-213">Invoer en uitvoer-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="33efb-213">Input + Output sample</span></span>
<span data-ttu-id="33efb-214">Stel dat u hebt de volgende function.json, die definieert een [opslag wachtrij trigger](functions-bindings-storage-queue.md), voert u een extern bestand en een bestand met externe uitvoer:</span><span class="sxs-lookup"><span data-stu-id="33efb-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="33efb-215">Zie de taalspecifieke steekproef die het invoerbestand gekopieerd naar het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="33efb-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="33efb-216">C#</span><span class="sxs-lookup"><span data-stu-id="33efb-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="33efb-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="33efb-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="33efb-218">Gebruik in C#</span><span class="sxs-lookup"><span data-stu-id="33efb-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="33efb-219">Gebruik in Node.js</span><span class="sxs-lookup"><span data-stu-id="33efb-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="33efb-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33efb-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
