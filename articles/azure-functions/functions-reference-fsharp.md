---
title: 'Azure Functions F # referentie voor ontwikkelaars | Microsoft Docs'
description: 'Begrijpen hoe Azure-functies met F # ontwikkelen.'
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: 'Azure functions, functies, gebeurtenisverwerking webhooks, dynamische compute, zonder server architectuur, F #'
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="2d469-104">Naslaginformatie over Azure Functions-F # ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2d469-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d469-105">C#-script</span><span class="sxs-lookup"><span data-stu-id="2d469-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="2d469-106">F # script</span><span class="sxs-lookup"><span data-stu-id="2d469-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="2d469-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="2d469-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="2d469-108">F # voor Azure Functions is een oplossing voor het eenvoudig uitvoeren van kleine stukjes code of 'functies' in de cloud.</span><span class="sxs-lookup"><span data-stu-id="2d469-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="2d469-109">Gegevensstromen in de functie F # via functieargumenten.</span><span class="sxs-lookup"><span data-stu-id="2d469-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="2d469-110">Argumentnamen zijn opgegeven in `function.json`, en er zijn vooraf gedefinieerde namen voor toegang tot de beheerder de functie berichtenlogboek en annulering tokens.</span><span class="sxs-lookup"><span data-stu-id="2d469-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="2d469-111">In dit artikel wordt ervan uitgegaan dat u al hebt gelezen de [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2d469-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="2d469-112">De werking van .fsx</span><span class="sxs-lookup"><span data-stu-id="2d469-112">How .fsx works</span></span>
<span data-ttu-id="2d469-113">Een `.fsx` bestand is een script F #.</span><span class="sxs-lookup"><span data-stu-id="2d469-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="2d469-114">Deze kan worden beschouwd als een F #-project dat opgenomen in één bestand.</span><span class="sxs-lookup"><span data-stu-id="2d469-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="2d469-115">Het bestand bevat zowel de code voor het programma (in dit geval uw Azure-functie) en richtlijnen voor het beheren van afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="2d469-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="2d469-116">Als u werkt met een `.fsx` voor een Azure-functie vaak vereiste assembly's worden automatisch opgenomen voor u, zodat u zich richten op de functie in plaats van 'standaard'-code.</span><span class="sxs-lookup"><span data-stu-id="2d469-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="2d469-117">Binding met argumenten</span><span class="sxs-lookup"><span data-stu-id="2d469-117">Binding to arguments</span></span>
<span data-ttu-id="2d469-118">Elke binding ondersteunt sommige set argumenten, zoals beschreven in de [Azure Functions triggers en bindingen naslaginformatie](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="2d469-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="2d469-119">Een van de argument bindingen die ondersteuning biedt voor een trigger blob is bijvoorbeeld een POCO die kan worden uitgedrukt met behulp van een record F #.</span><span class="sxs-lookup"><span data-stu-id="2d469-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="2d469-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="2d469-121">Uw Azure-functie F # duurt een of meer argumenten.</span><span class="sxs-lookup"><span data-stu-id="2d469-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="2d469-122">Wanneer we over Azure Functions argumenten hebben, is *invoer* argumenten en *uitvoer* argumenten.</span><span class="sxs-lookup"><span data-stu-id="2d469-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="2d469-123">Een invoerargument is precies deze klinkt als: invoer voor uw Azure-functie F #.</span><span class="sxs-lookup"><span data-stu-id="2d469-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="2d469-124">Een *uitvoer* -argument is veranderlijke gegevens of een `byref<>` argument die fungeert als een manier om gegevens weer te geven *uit* van de functie.</span><span class="sxs-lookup"><span data-stu-id="2d469-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="2d469-125">In het bovenstaande voorbeeld `blob` is een invoerargument en `output` is een argument van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2d469-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="2d469-126">U ziet dat we gebruikt `byref<>` voor `output` (is niet nodig om toe te voegen de `[<Out>]` aantekening).</span><span class="sxs-lookup"><span data-stu-id="2d469-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="2d469-127">Met behulp van een `byref<>` type biedt de mogelijkheid uw functie te wijzigen welke record of het argument naar verwijst object.</span><span class="sxs-lookup"><span data-stu-id="2d469-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="2d469-128">Wanneer een record F # wordt gebruikt als een type invoer, de definitie van de record moet worden gemarkeerd met `[<CLIMutable>]` om de Azure Functions-framework de velden op de juiste wijze instellen voordat de record aan de functie doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="2d469-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="2d469-129">Achter de schermen `[<CLIMutable>]` genereert setters voor de recordeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="2d469-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="2d469-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="2d469-131">Een klasse F # kan ook worden gebruikt voor zowel in- en argumenten.</span><span class="sxs-lookup"><span data-stu-id="2d469-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="2d469-132">Voor een klasse moet eigenschappen meestal getters en setters.</span><span class="sxs-lookup"><span data-stu-id="2d469-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="2d469-133">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="2d469-134">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="2d469-134">Logging</span></span>
<span data-ttu-id="2d469-135">Aanmelden van uitvoer naar uw [streaminglogboeken](../app-service-web/web-sites-streaming-logs-and-console.md) in F #, de functie moet rekening houden met een argument van het type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="2d469-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="2d469-136">Voor consistentie, raden we dit argument heet `log`.</span><span class="sxs-lookup"><span data-stu-id="2d469-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="2d469-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="2d469-138">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="2d469-138">Async</span></span>
<span data-ttu-id="2d469-139">De `async` werkstroom kan worden gebruikt, maar het resultaat moet retourneren een `Task`.</span><span class="sxs-lookup"><span data-stu-id="2d469-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="2d469-140">Dit kan worden gedaan met `Async.StartAsTask`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="2d469-141">Annulering Token</span><span class="sxs-lookup"><span data-stu-id="2d469-141">Cancellation Token</span></span>
<span data-ttu-id="2d469-142">Als de functie afsluiten probleemloos verwerken moet, u kunt daarvoor een [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span><span class="sxs-lookup"><span data-stu-id="2d469-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="2d469-143">Dit kan worden gecombineerd met `async`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="2d469-144">Naamruimten importeren</span><span class="sxs-lookup"><span data-stu-id="2d469-144">Importing namespaces</span></span>
<span data-ttu-id="2d469-145">Naamruimten kan worden geopend in de gebruikelijke manier:</span><span class="sxs-lookup"><span data-stu-id="2d469-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="2d469-146">Automatisch geopend op de volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="2d469-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="2d469-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="2d469-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="2d469-148">Verwijzen naar externe assembly 's</span><span class="sxs-lookup"><span data-stu-id="2d469-148">Referencing External Assemblies</span></span>
<span data-ttu-id="2d469-149">Op deze manier framework-assembly verwijzingen worden toegevoegd met de `#r "AssemblyName"` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="2d469-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="2d469-150">De volgende assembly's worden automatisch toegevoegd door de Azure Functions hostomgeving:</span><span class="sxs-lookup"><span data-stu-id="2d469-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="2d469-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="2d469-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="2d469-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="2d469-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="2d469-153">Bovendien de volgende assembly's zijn speciale geïntegreerd en kan worden verwezen door simplename (bijvoorbeeld `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="2d469-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="2d469-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="2d469-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="2d469-155">Als u nodig hebt om te verwijzen naar een persoonlijke assembly, kunt u in het assembly-bestand uploaden een `bin` map ten opzichte van uw functie en de verwijzing naar deze met behulp van het bestand (bijvoorbeeld een naam  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="2d469-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="2d469-156">Zie voor meer informatie over de bestanden uploaden naar uw map voor de functie in de volgende sectie op het gebied van pakket.</span><span class="sxs-lookup"><span data-stu-id="2d469-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="2d469-157">Editor Prelude</span><span class="sxs-lookup"><span data-stu-id="2d469-157">Editor Prelude</span></span>
<span data-ttu-id="2d469-158">Een editor die ondersteuning biedt voor F # Compiler-Services worden niet op de hoogte van de naamruimten en assembly's met Azure Functions automatisch.</span><span class="sxs-lookup"><span data-stu-id="2d469-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="2d469-159">Hierdoor kan het handig zijn om op te nemen van een prelude waarmee de editor voor de assembly's die u gebruikt vinden en openen expliciet naamruimten.</span><span class="sxs-lookup"><span data-stu-id="2d469-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="2d469-160">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="2d469-161">Wanneer uw code wordt uitgevoerd in Azure Functions, verwerking van de bron met `COMPILED` gedefinieerd, zodat de prelude editor worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="2d469-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="2d469-162">Pakket management</span><span class="sxs-lookup"><span data-stu-id="2d469-162">Package management</span></span>
<span data-ttu-id="2d469-163">Als u NuGet-pakketten in een functie F #, Voeg een `project.json` van het bestand in de map van de functie in het bestandssysteem van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="2d469-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="2d469-164">Hier volgt een voorbeeld `project.json` -bestand dat wordt toegevoegd een NuGet-pakket verwijzing naar `Microsoft.ProjectOxford.Face` versie 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="2d469-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="2d469-165">Alleen .NET Framework 4.6 wordt ondersteund, dus zorg ervoor dat uw `project.json` bestand geeft `net46` zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2d469-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="2d469-166">Wanneer u uploadt een `project.json` bestand, de runtime opgehaald van de pakketten en verwijzingen naar de pakket-assembly's worden automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2d469-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="2d469-167">U hoeft niet te voegen `#r "AssemblyName"` richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="2d469-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="2d469-168">Alleen toe te voegen de vereiste `open` instructies voor uw `.fsx` bestand.</span><span class="sxs-lookup"><span data-stu-id="2d469-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="2d469-169">U kunt desgewenst automatisch verwijzingen naar assembly's in uw editor prelude, voor het verbeteren van uw editor interactie met F # compileren Services plaatsen.</span><span class="sxs-lookup"><span data-stu-id="2d469-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="2d469-170">Het toevoegen van een `project.json` bestand naar uw Azure-functie</span><span class="sxs-lookup"><span data-stu-id="2d469-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="2d469-171">Begin door te controleren of de functie-app wordt uitgevoerd, die u kunt doen door de functie openen in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2d469-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="2d469-172">Dit biedt ook toegang naar de streaminglogboeken waar pakket installatie uitvoer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2d469-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="2d469-173">Voor het uploaden van een `project.json` bestand, gebruikt u een van de methoden van [het bijwerken van de functie app-bestanden](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="2d469-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="2d469-174">Als u [continue implementatie voor Azure Functions](functions-continuous-deployment.md), kunt u toevoegen een `project.json` bestand naar uw vertakking test om te experimenteren voordat u deze toevoegt aan uw vertakking implementatie.</span><span class="sxs-lookup"><span data-stu-id="2d469-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="2d469-175">Na de `project.json` bestand wordt toegevoegd, ziet u uitvoer die vergelijkbaar is met het volgende voorbeeld in de functie de streaming-logboek:</span><span class="sxs-lookup"><span data-stu-id="2d469-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="2d469-176">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="2d469-176">Environment variables</span></span>
<span data-ttu-id="2d469-177">Als u een omgevingsvariabele of een app die waarde instellen, gebruikt `System.Environment.GetEnvironmentVariable`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="2d469-178">Hergebruik van code .fsx</span><span class="sxs-lookup"><span data-stu-id="2d469-178">Reusing .fsx code</span></span>
<span data-ttu-id="2d469-179">U kunt de code van andere `.fsx` bestanden met behulp van een `#load` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="2d469-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="2d469-180">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2d469-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="2d469-181">Paden biedt aan de `#load` richtlijn zijn ten opzichte van de locatie van uw `.fsx` bestand.</span><span class="sxs-lookup"><span data-stu-id="2d469-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="2d469-182">`#load "logger.fsx"`een bestand in de map van de functie laadt.</span><span class="sxs-lookup"><span data-stu-id="2d469-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="2d469-183">`#load "package\logger.fsx"`laden van een bestand in de `package` map in de map van de functie.</span><span class="sxs-lookup"><span data-stu-id="2d469-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="2d469-184">`#load "..\shared\mylogger.fsx"`laden van een bestand in de `shared` map op hetzelfde niveau als de functie-map, dat wil zeggen, direct onder `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="2d469-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="2d469-185">De `#load` richtlijn werkt alleen met `.fsx` (F # script)-bestanden, en niet met `.fs` bestanden.</span><span class="sxs-lookup"><span data-stu-id="2d469-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d469-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d469-186">Next steps</span></span>
<span data-ttu-id="2d469-187">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="2d469-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="2d469-188">F # handleiding</span><span class="sxs-lookup"><span data-stu-id="2d469-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="2d469-189">Aanbevolen procedures voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2d469-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="2d469-190">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2d469-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="2d469-191">Azure Functions C# referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2d469-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="2d469-192">Azure Functions NodeJS-referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2d469-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="2d469-193">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="2d469-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="2d469-194">Azure Functions testen</span><span class="sxs-lookup"><span data-stu-id="2d469-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="2d469-195">Azure Functions schalen</span><span class="sxs-lookup"><span data-stu-id="2d469-195">Azure Functions scaling</span></span>](functions-scale.md)

