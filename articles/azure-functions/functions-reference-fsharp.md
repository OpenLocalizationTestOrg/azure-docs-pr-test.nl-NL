---
title: 'aaaAzure functies F # referentie voor ontwikkelaars | Microsoft Docs'
description: 'Begrijpen hoe Azure-functies met F # toodevelop.'
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
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="104dd-104">Naslaginformatie over Azure Functions-F # ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="104dd-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="104dd-105">C#-script</span><span class="sxs-lookup"><span data-stu-id="104dd-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="104dd-106">F # script</span><span class="sxs-lookup"><span data-stu-id="104dd-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="104dd-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="104dd-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="104dd-108">F # voor Azure Functions is een oplossing voor het eenvoudig uitvoeren van kleine stukjes code of 'functies' in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="104dd-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="104dd-109">Gegevensstromen in de functie F # via functieargumenten.</span><span class="sxs-lookup"><span data-stu-id="104dd-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="104dd-110">Argumentnamen zijn opgegeven in `function.json`, en er zijn vooraf gedefinieerde namen voor toegang tot bepaalde acties Hallo functie berichtenlogboek en annulering tokens.</span><span class="sxs-lookup"><span data-stu-id="104dd-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="104dd-111">In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="104dd-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="104dd-112">De werking van .fsx</span><span class="sxs-lookup"><span data-stu-id="104dd-112">How .fsx works</span></span>
<span data-ttu-id="104dd-113">Een `.fsx` bestand is een script F #.</span><span class="sxs-lookup"><span data-stu-id="104dd-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="104dd-114">Deze kan worden beschouwd als een F #-project dat opgenomen in één bestand.</span><span class="sxs-lookup"><span data-stu-id="104dd-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="104dd-115">Hallo-bestand bevat zowel Hallo-code voor het programma (in dit geval uw Azure-functie) en richtlijnen voor het beheren van afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="104dd-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="104dd-116">Als u werkt met een `.fsx` voor een Azure-functie vaak vereiste assembly's worden automatisch opgenomen voor u, zodat u toofocus op Hallo-functie in plaats van 'standaard' code.</span><span class="sxs-lookup"><span data-stu-id="104dd-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="104dd-117">Binding tooarguments</span><span class="sxs-lookup"><span data-stu-id="104dd-117">Binding tooarguments</span></span>
<span data-ttu-id="104dd-118">Elke binding ondersteunt sommige set argumenten, als gedetailleerde in Hallo [Azure Functions triggers en bindingen naslaginformatie](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="104dd-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="104dd-119">Een van de Hallo argument bindingen die biedt ondersteuning voor een blob-trigger is bijvoorbeeld een POCO die kan worden uitgedrukt met behulp van een record F #.</span><span class="sxs-lookup"><span data-stu-id="104dd-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="104dd-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="104dd-121">Uw Azure-functie F # duurt een of meer argumenten.</span><span class="sxs-lookup"><span data-stu-id="104dd-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="104dd-122">Wanneer we over Azure Functions argumenten hebben, verwijzen we te*invoer* argumenten en *uitvoer* argumenten.</span><span class="sxs-lookup"><span data-stu-id="104dd-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="104dd-123">Een invoerargument is precies deze klinkt als: invoer tooyour F # Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="104dd-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="104dd-124">Een *uitvoer* -argument is veranderlijke gegevens of een `byref<>` argument die als een manier toopass gegevens terug fungeert *uit* van de functie.</span><span class="sxs-lookup"><span data-stu-id="104dd-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="104dd-125">In vorige Hallo voorbeeld `blob` is een invoerargument en `output` is een argument van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="104dd-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="104dd-126">U ziet dat we gebruikt `byref<>` voor `output` (Er is geen noodzaak tooadd hello `[<Out>]` aantekening).</span><span class="sxs-lookup"><span data-stu-id="104dd-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="104dd-127">Met behulp van een `byref<>` type kunnen de functie toochange welke record of een object Hallo argument naar verwezen.</span><span class="sxs-lookup"><span data-stu-id="104dd-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="104dd-128">Wanneer een record F # wordt gebruikt als een invoertype, Hallo record definitie moet worden gemarkeerd met `[<CLIMutable>]` in volgorde tooallow hello Azure Functions framework tooset Hallo velden op de juiste wijze Hallo record tooyour functie voordat wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="104dd-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="104dd-129">Achter de schermen hello, `[<CLIMutable>]` setters voor Hallo recordeigenschappen genereert.</span><span class="sxs-lookup"><span data-stu-id="104dd-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="104dd-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="104dd-131">Een klasse F # kan ook worden gebruikt voor zowel in- en argumenten.</span><span class="sxs-lookup"><span data-stu-id="104dd-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="104dd-132">Voor een klasse moet eigenschappen meestal getters en setters.</span><span class="sxs-lookup"><span data-stu-id="104dd-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="104dd-133">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="104dd-134">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="104dd-134">Logging</span></span>
<span data-ttu-id="104dd-135">toolog uitvoer tooyour [streaminglogboeken](../app-service-web/web-sites-streaming-logs-and-console.md) in F #, de functie moet rekening houden met een argument van het type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="104dd-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="104dd-136">Voor consistentie, raden we dit argument heet `log`.</span><span class="sxs-lookup"><span data-stu-id="104dd-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="104dd-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="104dd-138">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="104dd-138">Async</span></span>
<span data-ttu-id="104dd-139">Hallo `async` werkstroom kan worden gebruikt, maar Hallo resultaat tooreturn moet een `Task`.</span><span class="sxs-lookup"><span data-stu-id="104dd-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="104dd-140">Dit kan worden gedaan met `Async.StartAsTask`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="104dd-141">Annulering Token</span><span class="sxs-lookup"><span data-stu-id="104dd-141">Cancellation Token</span></span>
<span data-ttu-id="104dd-142">Als de functie probleemloos toohandle afsluiten moet, u kunt daarvoor een [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span><span class="sxs-lookup"><span data-stu-id="104dd-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="104dd-143">Dit kan worden gecombineerd met `async`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="104dd-144">Naamruimten importeren</span><span class="sxs-lookup"><span data-stu-id="104dd-144">Importing namespaces</span></span>
<span data-ttu-id="104dd-145">Naamruimten kan worden geopend in Hallo gebruikelijke manier:</span><span class="sxs-lookup"><span data-stu-id="104dd-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="104dd-146">Hallo na naamruimten automatisch geopend:</span><span class="sxs-lookup"><span data-stu-id="104dd-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="104dd-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="104dd-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="104dd-148">Verwijzen naar externe assembly 's</span><span class="sxs-lookup"><span data-stu-id="104dd-148">Referencing External Assemblies</span></span>
<span data-ttu-id="104dd-149">Op deze manier framework-assembly verwijzingen worden toegevoegd met de Hallo `#r "AssemblyName"` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="104dd-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="104dd-150">Hallo worden volgende assembly's automatisch toegevoegd door hello Azure Functions hostomgeving:</span><span class="sxs-lookup"><span data-stu-id="104dd-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="104dd-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="104dd-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="104dd-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="104dd-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="104dd-153">Bovendien Hallo volgende assembly's zijn speciale geïntegreerd en kan worden verwezen door simplename (bijvoorbeeld `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="104dd-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="104dd-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="104dd-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="104dd-155">Als u een persoonlijke assembly tooreference moet, kunt u uploaden Hallo assembly-bestand in een `bin` map relatieve tooyour functie en deze met behulp van de bestandsnaam (bijvoorbeeld Hallo-verwijzing  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="104dd-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="104dd-156">Zie voor informatie over hoe tooupload tooyour functie map bestanden, Hallo volgende sectie op het gebied van pakket.</span><span class="sxs-lookup"><span data-stu-id="104dd-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="104dd-157">Editor Prelude</span><span class="sxs-lookup"><span data-stu-id="104dd-157">Editor Prelude</span></span>
<span data-ttu-id="104dd-158">Een editor die ondersteuning biedt voor F # Compiler-Services worden niet op de hoogte van het Hallo-naamruimten en assembly's met Azure Functions automatisch.</span><span class="sxs-lookup"><span data-stu-id="104dd-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="104dd-159">Als zodanig kan zijn nuttig tooinclude een prelude waarmee Hallo editor Hallo-assembly's die u gebruikt vinden en tooexplicitly open naamruimten.</span><span class="sxs-lookup"><span data-stu-id="104dd-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="104dd-160">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-160">For example:</span></span>

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

<span data-ttu-id="104dd-161">Wanneer uw code wordt uitgevoerd in Azure Functions, verwerkt Hallo bron met `COMPILED` gedefinieerd, zodat het Hallo-editor prelude worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="104dd-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="104dd-162">Pakket management</span><span class="sxs-lookup"><span data-stu-id="104dd-162">Package management</span></span>
<span data-ttu-id="104dd-163">toouse NuGet-pakketten in een F # functie, Voeg een `project.json` toohello Hallo functie map in het bestandssysteem Hallo functie app-bestand.</span><span class="sxs-lookup"><span data-stu-id="104dd-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="104dd-164">Hier volgt een voorbeeld `project.json` -bestand dat de verwijzing naar een NuGet-pakket te voegt`Microsoft.ProjectOxford.Face` versie 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="104dd-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="104dd-165">Alleen hello .NET Framework 4.6 wordt ondersteund, dus zorg ervoor dat uw `project.json` bestand geeft `net46` zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="104dd-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="104dd-166">Wanneer u uploadt een `project.json` bestand, hello runtime opgehaald hello-pakketten en verwijzingen toohello pakket assembly's worden automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="104dd-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="104dd-167">U hoeft niet tooadd `#r "AssemblyName"` richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="104dd-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="104dd-168">Hallo vereist alleen toe te voegen `open` instructies tooyour `.fsx` bestand.</span><span class="sxs-lookup"><span data-stu-id="104dd-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="104dd-169">U kunt desgewenst tooput automatisch verwijst naar assembly's in uw editor prelude, tooimprove uw editor interactie met F # compileren Services.</span><span class="sxs-lookup"><span data-stu-id="104dd-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="104dd-170">Hoe tooadd een `project.json` bestand tooyour Azure-functie</span><span class="sxs-lookup"><span data-stu-id="104dd-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="104dd-171">Begin door te controleren of de functie-app wordt uitgevoerd, die u kunt doen door de functie openen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="104dd-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="104dd-172">Dit biedt ook toegang toohello streaminglogboeken waar pakket installatie uitvoer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="104dd-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="104dd-173">tooupload een `project.json` bestand, gebruikt u een Hallo methoden van [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="104dd-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="104dd-174">Als u [continue implementatie voor Azure Functions](functions-continuous-deployment.md), kunt u toevoegen een `project.json` tooyour vertakking in volgorde tooexperiment aan voordat u het toevoegt tooyour implementatie vertakking tijdelijke bestand.</span><span class="sxs-lookup"><span data-stu-id="104dd-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="104dd-175">Na het Hallo `project.json` bestand wordt toegevoegd, ziet u uitvoer vergelijkbare toohello voorbeeld in de functie na de streaming-logboek:</span><span class="sxs-lookup"><span data-stu-id="104dd-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="104dd-176">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="104dd-176">Environment variables</span></span>
<span data-ttu-id="104dd-177">tooget een omgevingsvariabele of een app-instelling-waarde gebruiken `System.Environment.GetEnvironmentVariable`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="104dd-178">Hergebruik van code .fsx</span><span class="sxs-lookup"><span data-stu-id="104dd-178">Reusing .fsx code</span></span>
<span data-ttu-id="104dd-179">U kunt de code van andere `.fsx` bestanden met behulp van een `#load` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="104dd-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="104dd-180">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="104dd-180">For example:</span></span>

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

<span data-ttu-id="104dd-181">Paden biedt toohello `#load` richtlijn zijn toohello relatieve locatie van uw `.fsx` bestand.</span><span class="sxs-lookup"><span data-stu-id="104dd-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="104dd-182">`#load "logger.fsx"`een bestand in Hallo functie map laadt.</span><span class="sxs-lookup"><span data-stu-id="104dd-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="104dd-183">`#load "package\logger.fsx"`een bestand in Hallo laadt `package` map in Hallo functie map.</span><span class="sxs-lookup"><span data-stu-id="104dd-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="104dd-184">`#load "..\shared\mylogger.fsx"`een bestand in Hallo laadt `shared` map op hetzelfde niveau als Hallo functie map, dat wil zeggen, Hallo rechtstreeks onder `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="104dd-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="104dd-185">Hallo `#load` richtlijn werkt alleen met `.fsx` (F # script)-bestanden, en niet met `.fs` bestanden.</span><span class="sxs-lookup"><span data-stu-id="104dd-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="104dd-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="104dd-186">Next steps</span></span>
<span data-ttu-id="104dd-187">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="104dd-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="104dd-188">F # handleiding</span><span class="sxs-lookup"><span data-stu-id="104dd-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="104dd-189">Aanbevolen procedures voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="104dd-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="104dd-190">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="104dd-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="104dd-191">Azure Functions C# referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="104dd-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="104dd-192">Azure Functions NodeJS-referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="104dd-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="104dd-193">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="104dd-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="104dd-194">Azure Functions testen</span><span class="sxs-lookup"><span data-stu-id="104dd-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="104dd-195">Azure Functions schalen</span><span class="sxs-lookup"><span data-stu-id="104dd-195">Azure Functions scaling</span></span>](functions-scale.md)

