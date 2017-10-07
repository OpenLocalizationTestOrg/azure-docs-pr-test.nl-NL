---
title: aaaAzure functies C# Script-referentie voor ontwikkelaars | Microsoft Docs
description: Begrijpen hoe toodevelop Azure Functions met C#.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="f65bb-104">Azure Functions C# script referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="f65bb-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f65bb-105">C#-script</span><span class="sxs-lookup"><span data-stu-id="f65bb-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="f65bb-106">F # script</span><span class="sxs-lookup"><span data-stu-id="f65bb-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="f65bb-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f65bb-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="f65bb-108">Hallo C# script ervaring voor Azure Functions is gebaseerd op Hallo Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="f65bb-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="f65bb-109">Gegevensstromen in uw C#-functie via argumenten van de methode.</span><span class="sxs-lookup"><span data-stu-id="f65bb-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="f65bb-110">Argumentnamen zijn opgegeven in `function.json`, en er zijn vooraf gedefinieerde namen voor toegang tot bepaalde acties Hallo functie berichtenlogboek en annulering tokens.</span><span class="sxs-lookup"><span data-stu-id="f65bb-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="f65bb-111">In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f65bb-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="f65bb-112">Klasse voor informatie over het gebruik van C#-bibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="f65bb-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="f65bb-113">De werking van .csx</span><span class="sxs-lookup"><span data-stu-id="f65bb-113">How .csx works</span></span>
<span data-ttu-id="f65bb-114">Hallo `.csx` notatie kunt u toowrite minder 'standaard' en u richten op het schrijven van slechts een C#-functie.</span><span class="sxs-lookup"><span data-stu-id="f65bb-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="f65bb-115">Assembly-verwijzingen en naamruimten aan Hallo begin van Hallo bestand gewoon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f65bb-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="f65bb-116">In plaats van dat u alles verpakt in een naamruimte en klassenaam, net definiëren een `Run` methode.</span><span class="sxs-lookup"><span data-stu-id="f65bb-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="f65bb-117">Als u nodig hebt tooinclude Hallo alle klassen, voor het exemplaar toodefine zonder opmaak objecten oude CLR-Object (POCO), kunt u een klasse in opnemen hetzelfde bestand.</span><span class="sxs-lookup"><span data-stu-id="f65bb-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="f65bb-118">Binding tooarguments</span><span class="sxs-lookup"><span data-stu-id="f65bb-118">Binding tooarguments</span></span>
<span data-ttu-id="f65bb-119">Hallo verschillende bindingen zijn gebonden tooa C#-functie via Hallo `name` eigenschap in Hallo *function.json* configuratie.</span><span class="sxs-lookup"><span data-stu-id="f65bb-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="f65bb-120">Elke binding heeft een eigen ondersteunde typen; een trigger blob kan bijvoorbeeld een tekenreeks, een POCO of een CloudBlockBlob ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="f65bb-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="f65bb-121">Hallo ondersteunde typen zijn gedocumenteerd in Hallo-verwijzing voor elke binding.</span><span class="sxs-lookup"><span data-stu-id="f65bb-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="f65bb-122">Een POCO-object moet een getter en setter gedefinieerd voor elke eigenschap hebben.</span><span class="sxs-lookup"><span data-stu-id="f65bb-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="f65bb-123">Met behulp van de retourwaarde van de methode voor het binden van uitvoer</span><span class="sxs-lookup"><span data-stu-id="f65bb-123">Using method return value for output binding</span></span>

<span data-ttu-id="f65bb-124">Kunt u de geretourneerde waarde van een methode voor een binding uitvoer met de naam Hallo `$return` in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f65bb-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="f65bb-125">Schrijven van meerdere uitvoerwaarden</span><span class="sxs-lookup"><span data-stu-id="f65bb-125">Writing multiple output values</span></span>

<span data-ttu-id="f65bb-126">toowrite meerdere waarden tooan uitvoer binding, gebruikt u Hallo [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) of [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typen.</span><span class="sxs-lookup"><span data-stu-id="f65bb-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="f65bb-127">Deze typen zijn alleen-schrijven verzamelingen die geschreven toohello uitvoer binding zijn wanneer Hallo-methode is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f65bb-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="f65bb-128">In dit voorbeeld schrijft meerdere Wachtrijberichten met `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="f65bb-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="f65bb-129">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="f65bb-129">Logging</span></span>
<span data-ttu-id="f65bb-130">toolog uitvoer tooyour streaminglogboeken in C#, bevatten een argument van het type `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="f65bb-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="f65bb-131">Het is raadzaam dat u deze de naam `log`.</span><span class="sxs-lookup"><span data-stu-id="f65bb-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="f65bb-132">Vermijd het gebruik van `Console.Write` in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f65bb-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="f65bb-133">`TraceWriter`is gedefinieerd in Hallo [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="f65bb-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="f65bb-134">Hallo logboekniveau voor `TraceWriter` kunnen worden geconfigureerd in [host\.json].</span><span class="sxs-lookup"><span data-stu-id="f65bb-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="f65bb-135">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="f65bb-135">Async</span></span>
<span data-ttu-id="f65bb-136">een asynchrone functie toomake hello gebruiken `async` sleutelwoord en retourneren een `Task` object.</span><span class="sxs-lookup"><span data-stu-id="f65bb-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="f65bb-137">Annulering Token</span><span class="sxs-lookup"><span data-stu-id="f65bb-137">Cancellation Token</span></span>
<span data-ttu-id="f65bb-138">Bepaalde bewerkingen vereisen correct afsluiten.</span><span class="sxs-lookup"><span data-stu-id="f65bb-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="f65bb-139">Het is altijd best toowrite code dat kan worden verwerkt gecrasht in gevallen waar u toohandle correct afsluiten aanvragen, definieert u een [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f65bb-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="f65bb-140">Een `CancellationToken` toosignal dat een afsluiten van de host is geactiveerd is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f65bb-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="f65bb-141">Naamruimten importeren</span><span class="sxs-lookup"><span data-stu-id="f65bb-141">Importing namespaces</span></span>
<span data-ttu-id="f65bb-142">Als u tooimport naamruimten moet, kunt u doen gebruikelijke Hello `using` component.</span><span class="sxs-lookup"><span data-stu-id="f65bb-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="f65bb-143">Hallo volgende naamruimten automatisch worden geïmporteerd en zijn daarom optioneel:</span><span class="sxs-lookup"><span data-stu-id="f65bb-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="f65bb-144">Verwijzen naar externe assembly 's</span><span class="sxs-lookup"><span data-stu-id="f65bb-144">Referencing External Assemblies</span></span>
<span data-ttu-id="f65bb-145">Voor de framework-assembly's, voeg verwijzingen toe met behulp van Hallo `#r "AssemblyName"` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="f65bb-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="f65bb-146">Hallo worden volgende assembly's automatisch toegevoegd door hello Azure Functions hostomgeving:</span><span class="sxs-lookup"><span data-stu-id="f65bb-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="f65bb-147">Hallo volgende assembly's kunnen worden verwezen met eenvoudige naam (bijvoorbeeld `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="f65bb-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="f65bb-148">Aangepaste assembly's die verwijzen naar</span><span class="sxs-lookup"><span data-stu-id="f65bb-148">Referencing custom assemblies</span></span>

<span data-ttu-id="f65bb-149">een aangepaste assembly tooreference, kunt u ofwel een *gedeelde* assembly of een *persoonlijke* assembly:</span><span class="sxs-lookup"><span data-stu-id="f65bb-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="f65bb-150">Gedeelde assembly's worden gedeeld door alle functies binnen een functie-app.</span><span class="sxs-lookup"><span data-stu-id="f65bb-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="f65bb-151">een aangepaste assembly tooreference uploaden Hallo assembly tooyour functie-app, zoals een `bin` map in Hallo functie app-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="f65bb-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="f65bb-152">Persoonlijke assembly's deel uitmaken van een bepaalde functie context en ondersteuning voor sideloading van verschillende versies.</span><span class="sxs-lookup"><span data-stu-id="f65bb-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="f65bb-153">Persoonlijke assembly's moeten worden geüpload een `bin` map in Hallo functie directory.</span><span class="sxs-lookup"><span data-stu-id="f65bb-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="f65bb-154">Verwijzing naar het gebruik van Hallo bestandsnaam op, zoals `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="f65bb-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="f65bb-155">Zie voor informatie over hoe tooupload tooyour functie map bestanden, Hallo volgende sectie op het gebied van pakket.</span><span class="sxs-lookup"><span data-stu-id="f65bb-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="f65bb-156">Gecontroleerde mappen</span><span class="sxs-lookup"><span data-stu-id="f65bb-156">Watched directories</span></span>

<span data-ttu-id="f65bb-157">Hallo-map met de Hallo functie scriptbestand wordt automatisch weergegeven voor wijzigingen tooassemblies.</span><span class="sxs-lookup"><span data-stu-id="f65bb-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="f65bb-158">toowatch voor assembly-wijzigingen in andere mappen toohello toe te voegen `watchDirectories` in lijst [host\.json].</span><span class="sxs-lookup"><span data-stu-id="f65bb-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="f65bb-159">NuGet-pakketten gebruiken</span><span class="sxs-lookup"><span data-stu-id="f65bb-159">Using NuGet packages</span></span>
<span data-ttu-id="f65bb-160">toouse NuGet-pakketten in een C#-functie uploaden een *project.json* bestand van de functie toohello map in Hallo functie app-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="f65bb-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="f65bb-161">Hier volgt een voorbeeld *project.json* -bestand dat wordt een verwijzing tooMicrosoft.ProjectOxford.Face versie 1.1.0 toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="f65bb-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="f65bb-162">Alleen hello .NET Framework 4.6 wordt ondersteund, dus zorg ervoor dat uw *project.json* bestand geeft `net46` zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f65bb-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="f65bb-163">Wanneer u uploadt een *project.json* bestand, hello runtime opgehaald hello-pakketten en verwijzingen toohello pakket assembly's worden automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f65bb-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="f65bb-164">U hoeft niet tooadd `#r "AssemblyName"` richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="f65bb-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="f65bb-165">toouse Hallo-typen gedefinieerd in Hallo NuGet-pakketten toevoegen Hallo vereist `using` instructies tooyour *run.csx* bestand</span><span class="sxs-lookup"><span data-stu-id="f65bb-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="f65bb-166">Hallo runtime van Functions, NuGet terugzetten werkt door te vergelijken `project.json` en `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="f65bb-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="f65bb-167">Als datum- en tijdstempels van bestanden Hallo Hallo **niet** overeenkomst, een NuGet-herstelbewerking wordt uitgevoerd en NuGet downloads pakketten bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f65bb-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="f65bb-168">Echter, als hello datum- en tijdstempels van bestanden Hallo **doen** overeenkomen, NuGet voert een terugzetbewerking.</span><span class="sxs-lookup"><span data-stu-id="f65bb-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="f65bb-169">Daarom `project.lock.json` moeten niet worden geïmplementeerd omdat het ervoor zorgt NuGet tooskip pakket herstellen dat.</span><span class="sxs-lookup"><span data-stu-id="f65bb-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="f65bb-170">Hallo vergrendeling implementeren tooavoid bestand, het toevoegen van Hallo `project.lock.json` toohello `.gitignore` bestand.</span><span class="sxs-lookup"><span data-stu-id="f65bb-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="f65bb-171">een aangepaste NuGet-feed toouse Geef Hallo-kanaal in een *Nuget.Config* bestand in Hallo functie-App-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="f65bb-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="f65bb-172">Zie voor meer informatie [NuGet configureren gedrag](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="f65bb-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="f65bb-173">Met behulp van een bestand project.json</span><span class="sxs-lookup"><span data-stu-id="f65bb-173">Using a project.json file</span></span>
1. <span data-ttu-id="f65bb-174">Hallo functie openen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f65bb-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="f65bb-175">Hallo logboeken tabblad geeft Hallo pakket installatie uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f65bb-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="f65bb-176">tooupload een bestand project.json gebruik een van de methoden van Hallo Hallo [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate) in naslagonderwerp voor hello Azure Functions-ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="f65bb-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="f65bb-177">Na het Hallo *project.json* bestand wordt geüpload, ziet u uitvoer zoals Hallo voorbeeld in de functie na de streaming-logboek:</span><span class="sxs-lookup"><span data-stu-id="f65bb-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="f65bb-178">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="f65bb-178">Environment variables</span></span>
<span data-ttu-id="f65bb-179">tooget een omgevingsvariabele of een app-instelling-waarde gebruiken `System.Environment.GetEnvironmentVariable`, zoals weergegeven in het volgende codevoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="f65bb-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="f65bb-180">Hergebruik van code .csx</span><span class="sxs-lookup"><span data-stu-id="f65bb-180">Reusing .csx code</span></span>
<span data-ttu-id="f65bb-181">U kunt klassen en methoden die zijn gedefinieerd in andere *.csx* bestanden in uw *run.csx* bestand.</span><span class="sxs-lookup"><span data-stu-id="f65bb-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="f65bb-182">toodo die gebruikmaken van `#load` richtlijnen op uw *run.csx* bestand.</span><span class="sxs-lookup"><span data-stu-id="f65bb-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="f65bb-183">In de Hallo voorbeeld te volgen, een routine logboekregistratie met de naam `MyLogger` wordt gedeeld *myLogger.csx* en geladen in *run.csx* met Hallo `#load` richtlijn:</span><span class="sxs-lookup"><span data-stu-id="f65bb-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="f65bb-184">Voorbeeld *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="f65bb-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="f65bb-185">Voorbeeld *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="f65bb-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="f65bb-186">Met behulp van een gedeelde *.csx* is een algemene patroon als u wilt dat toostrongly uw typeargumenten tussen functies met een POCO-object.</span><span class="sxs-lookup"><span data-stu-id="f65bb-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="f65bb-187">In een Hallo vereenvoudigd voorbeeld te volgen, een HTTP-trigger en wachtrij-trigger delen een POCO-object met de naam `Order` toostrongly type Hallo ordenen van gegevens:</span><span class="sxs-lookup"><span data-stu-id="f65bb-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="f65bb-188">Voorbeeld *run.csx* voor HTTP-trigger:</span><span class="sxs-lookup"><span data-stu-id="f65bb-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="f65bb-189">Voorbeeld *run.csx* voor wachtrij trigger:</span><span class="sxs-lookup"><span data-stu-id="f65bb-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="f65bb-190">Voorbeeld *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="f65bb-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="f65bb-191">U kunt een relatief pad Hallo `#load` richtlijn:</span><span class="sxs-lookup"><span data-stu-id="f65bb-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="f65bb-192">`#load "mylogger.csx"`een bestand in Hallo functie map laadt.</span><span class="sxs-lookup"><span data-stu-id="f65bb-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="f65bb-193">`#load "loadedfiles\mylogger.csx"`een bestand in een map in Hallo functie map laadt.</span><span class="sxs-lookup"><span data-stu-id="f65bb-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="f65bb-194">`#load "..\shared\mylogger.csx"`een bestand in een map op hetzelfde niveau als Hallo functie map, dat wil zeggen, Hallo laadt rechtstreeks onder *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="f65bb-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="f65bb-195">Hallo `#load` richtlijn werkt alleen met *.csx* (C# script)-bestanden, niet bij *.cs* bestanden.</span><span class="sxs-lookup"><span data-stu-id="f65bb-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="f65bb-196">Binding tijdens runtime via imperatieve bindingen</span><span class="sxs-lookup"><span data-stu-id="f65bb-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="f65bb-197">In C# en andere .NET-talen, kunt u een [imperatieve](https://en.wikipedia.org/wiki/Imperative_programming) patroon van de binding, als tegengestelde toohello [ *declaratieve* ](https://en.wikipedia.org/wiki/Declarative_programming) bindingen in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f65bb-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="f65bb-198">Imperatieve binding is handig als bindparameters toobe berekend tijdens runtime in plaats van ontwerp moeten.</span><span class="sxs-lookup"><span data-stu-id="f65bb-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="f65bb-199">U kunt met dit patroon binden toosupported invoer en uitvoer van de binding op het moment in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="f65bb-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="f65bb-200">Definieer een imperatieve binding als volgt:</span><span class="sxs-lookup"><span data-stu-id="f65bb-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="f65bb-201">**Geen** een vermelding in *function.json* voor uw gewenste imperatieve bindingen.</span><span class="sxs-lookup"><span data-stu-id="f65bb-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="f65bb-202">Geeft een invoerparameter [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) of [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="f65bb-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="f65bb-203">Gebruik Hallo C# patroon tooperform Hallo gegevensbinding te volgen.</span><span class="sxs-lookup"><span data-stu-id="f65bb-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="f65bb-204">waar `BindingTypeAttribute` is Hallo .NET-kenmerk dat de binding wordt gedefinieerd en `T` is Hallo invoer- of -type dat wordt ondersteund door deze bindingstype.</span><span class="sxs-lookup"><span data-stu-id="f65bb-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="f65bb-205">`T`ook kan niet een `out` parametertype (zoals `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="f65bb-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="f65bb-206">Bijvoorbeeld, de tabel Mobile Apps binding ondersteunt uitvoer [zes typen uitvoer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), maar u kunt alleen [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) of [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) voor `T`.</span><span class="sxs-lookup"><span data-stu-id="f65bb-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="f65bb-207">Hallo volgende voorbeeldcode maakt een [Storage-blob uitvoer binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) met blob pad dat gedefinieerd tijdens runtime, schrijft u een tekenreeks toohello blob.</span><span class="sxs-lookup"><span data-stu-id="f65bb-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="f65bb-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definieert Hallo [Storage-blob](functions-bindings-storage-blob.md) invoer of uitvoer van de binding en [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is een ondersteunde binding uitvoertype.</span><span class="sxs-lookup"><span data-stu-id="f65bb-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="f65bb-209">Code Hallo Hallo standaard app-instelling voor Hallo verbindingsreeks voor opslag account opgehaald (dit is `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="f65bb-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="f65bb-210">U kunt een aangepaste app-instelling toouse opgeven door toe te voegen de [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) en Hallo kenmerk matrix in doorgeven `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="f65bb-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="f65bb-211">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f65bb-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="f65bb-212">Hallo bevat volgende tabel Hallo .NET kenmerken voor elke binding type hello-pakketten en waarin ze worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f65bb-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="f65bb-213">Binding</span><span class="sxs-lookup"><span data-stu-id="f65bb-213">Binding</span></span> | <span data-ttu-id="f65bb-214">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="f65bb-214">Attribute</span></span> | <span data-ttu-id="f65bb-215">Verwijzing toevoegen</span><span class="sxs-lookup"><span data-stu-id="f65bb-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="f65bb-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f65bb-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="f65bb-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f65bb-217">Event Hubs</span></span> | <span data-ttu-id="f65bb-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f65bb-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="f65bb-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f65bb-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="f65bb-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="f65bb-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="f65bb-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="f65bb-221">Service Bus</span></span> | <span data-ttu-id="f65bb-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f65bb-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="f65bb-223">Storage-wachtrij</span><span class="sxs-lookup"><span data-stu-id="f65bb-223">Storage queue</span></span> | <span data-ttu-id="f65bb-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f65bb-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="f65bb-225">Storage-blob</span><span class="sxs-lookup"><span data-stu-id="f65bb-225">Storage blob</span></span> | <span data-ttu-id="f65bb-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f65bb-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="f65bb-227">Table Storage</span><span class="sxs-lookup"><span data-stu-id="f65bb-227">Storage table</span></span> | <span data-ttu-id="f65bb-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="f65bb-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="f65bb-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="f65bb-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="f65bb-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f65bb-230">Next steps</span></span>
<span data-ttu-id="f65bb-231">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f65bb-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="f65bb-232">Aanbevolen procedures voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f65bb-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="f65bb-233">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="f65bb-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="f65bb-234">Azure Functions F # referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="f65bb-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="f65bb-235">Azure Functions NodeJS-referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="f65bb-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="f65bb-236">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="f65bb-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
