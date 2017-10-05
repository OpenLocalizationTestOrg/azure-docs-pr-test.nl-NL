---
title: Azure Functions C# Script-referentie voor ontwikkelaars | Microsoft Docs
description: Begrijpen hoe Azure-functies met C# ontwikkelen.
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="c0f0a-104">Azure Functions C# script referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c0f0a-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0f0a-105">C#-script</span><span class="sxs-lookup"><span data-stu-id="c0f0a-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="c0f0a-106">F # script</span><span class="sxs-lookup"><span data-stu-id="c0f0a-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="c0f0a-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c0f0a-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="c0f0a-108">De C# script-ervaring voor Azure Functions is gebaseerd op de Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="c0f0a-109">Gegevensstromen in uw C#-functie via argumenten van de methode.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="c0f0a-110">Argumentnamen zijn opgegeven in `function.json`, en er zijn vooraf gedefinieerde namen voor toegang tot de beheerder de functie berichtenlogboek en annulering tokens.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="c0f0a-111">In dit artikel wordt ervan uitgegaan dat u al hebt gelezen de [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="c0f0a-112">Klasse voor informatie over het gebruik van C#-bibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="c0f0a-113">De werking van .csx</span><span class="sxs-lookup"><span data-stu-id="c0f0a-113">How .csx works</span></span>
<span data-ttu-id="c0f0a-114">De `.csx` indeling kunt u minder 'standaard' schrijven en zich richten op het schrijven van slechts een C#-functie.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="c0f0a-115">Assembly-verwijzingen en naamruimten aan het begin van het bestand zoals gebruikelijk bevatten.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="c0f0a-116">In plaats van dat u alles verpakt in een naamruimte en klassenaam, net definiëren een `Run` methode.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="c0f0a-117">Als u wilt bijvoorbeeld alle klassen, zijn gewoon oude CLR Object (POCO) om objecten te definiëren, kunt u een klasse in hetzelfde bestand opnemen.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="c0f0a-118">Binding met argumenten</span><span class="sxs-lookup"><span data-stu-id="c0f0a-118">Binding to arguments</span></span>
<span data-ttu-id="c0f0a-119">De verschillende bindingen zijn gebonden aan een functie C# via de `name` eigenschap in de *function.json* configuratie.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="c0f0a-120">Elke binding heeft een eigen ondersteunde typen; een trigger blob kan bijvoorbeeld een tekenreeks, een POCO of een CloudBlockBlob ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="c0f0a-121">De ondersteunde typen zijn gedocumenteerd in de documentatie voor elke binding.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="c0f0a-122">Een POCO-object moet een getter en setter gedefinieerd voor elke eigenschap hebben.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="c0f0a-123">Met behulp van de retourwaarde van de methode voor het binden van uitvoer</span><span class="sxs-lookup"><span data-stu-id="c0f0a-123">Using method return value for output binding</span></span>

<span data-ttu-id="c0f0a-124">U kunt de geretourneerde waarde van een methode voor een binding uitvoer met de naam `$return` in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="c0f0a-125">Schrijven van meerdere uitvoerwaarden</span><span class="sxs-lookup"><span data-stu-id="c0f0a-125">Writing multiple output values</span></span>

<span data-ttu-id="c0f0a-126">Als meerdere waarden opslaan op een uitvoer-binding, gebruiken de [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) of [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typen.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="c0f0a-127">Deze typen zijn alleen-schrijven verzamelingen die zijn geschreven voor de binding uitvoer wanneer de methode is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="c0f0a-128">In dit voorbeeld schrijft meerdere Wachtrijberichten met `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="c0f0a-129">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="c0f0a-129">Logging</span></span>
<span data-ttu-id="c0f0a-130">Om te registreren uitvoer in uw streaminglogboeken in C#, een argument van het type bevatten `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="c0f0a-131">Het is raadzaam dat u deze de naam `log`.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="c0f0a-132">Vermijd het gebruik van `Console.Write` in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="c0f0a-133">`TraceWriter`is gedefinieerd in de [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="c0f0a-134">Het logboek-niveau voor `TraceWriter` kunnen worden geconfigureerd in [host\.json].</span><span class="sxs-lookup"><span data-stu-id="c0f0a-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="c0f0a-135">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="c0f0a-135">Async</span></span>
<span data-ttu-id="c0f0a-136">Als u een functie asynchrone, gebruikt u de `async` sleutelwoord en retourneren een `Task` object.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="c0f0a-137">Annulering Token</span><span class="sxs-lookup"><span data-stu-id="c0f0a-137">Cancellation Token</span></span>
<span data-ttu-id="c0f0a-138">Bepaalde bewerkingen vereisen correct afsluiten.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="c0f0a-139">Terwijl het is verstandig code schrijven waarmee gecrasht kan verwerken, in gevallen waar u wilt aanvragen voor het afhandelen van correct afsluiten, definieert u een [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="c0f0a-140">Een `CancellationToken` wordt geleverd om aan te geven dat een afsluiten van de host is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="c0f0a-141">Naamruimten importeren</span><span class="sxs-lookup"><span data-stu-id="c0f0a-141">Importing namespaces</span></span>
<span data-ttu-id="c0f0a-142">Als u importeren, naamruimten wilt, kunt u doen dus gebruikelijke met de `using` component.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="c0f0a-143">De volgende naamruimten automatisch worden geïmporteerd en zijn daarom optioneel:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="c0f0a-144">Verwijzen naar externe assembly 's</span><span class="sxs-lookup"><span data-stu-id="c0f0a-144">Referencing External Assemblies</span></span>
<span data-ttu-id="c0f0a-145">Voor de framework-assembly's, voeg verwijzingen toe met behulp van de `#r "AssemblyName"` richtlijn.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="c0f0a-146">De volgende assembly's worden automatisch toegevoegd door de Azure Functions hostomgeving:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="c0f0a-147">De volgende assembly's kunnen worden verwezen met eenvoudige naam (bijvoorbeeld `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="c0f0a-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="c0f0a-148">Aangepaste assembly's die verwijzen naar</span><span class="sxs-lookup"><span data-stu-id="c0f0a-148">Referencing custom assemblies</span></span>

<span data-ttu-id="c0f0a-149">Om te verwijzen naar een aangepaste assembly, kunt u ofwel een *gedeelde* assembly of een *persoonlijke* assembly:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="c0f0a-150">Gedeelde assembly's worden gedeeld door alle functies binnen een functie-app.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="c0f0a-151">Om te verwijzen naar een aangepaste assembly, uploadt u de assembly die de functie-app, zoals een `bin` map in de functie app-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="c0f0a-152">Persoonlijke assembly's deel uitmaken van een bepaalde functie context en ondersteuning voor sideloading van verschillende versies.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="c0f0a-153">Persoonlijke assembly's moeten worden geüpload een `bin` map in de functie Active directory.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="c0f0a-154">Verwijst naar de bestandsnaam, zoals met `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="c0f0a-155">Zie voor meer informatie over de bestanden uploaden naar uw map voor de functie in de volgende sectie op het gebied van pakket.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="c0f0a-156">Gecontroleerde mappen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-156">Watched directories</span></span>

<span data-ttu-id="c0f0a-157">De map waarin het scriptbestand functie wordt automatisch weergegeven voor wijzigingen in de assembly's.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="c0f0a-158">Als u wilt bekijken voor assembly-wijzigingen in andere directory's, voeg deze toe aan de `watchDirectories` in lijst [host\.json].</span><span class="sxs-lookup"><span data-stu-id="c0f0a-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="c0f0a-159">NuGet-pakketten gebruiken</span><span class="sxs-lookup"><span data-stu-id="c0f0a-159">Using NuGet packages</span></span>
<span data-ttu-id="c0f0a-160">Als u NuGet-pakketten in een C#-functie, uploaden een *project.json* -bestand naar de map van de functie in het bestandssysteem van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="c0f0a-161">Hier volgt een voorbeeld *project.json* -bestand dat wordt toegevoegd een verwijzing naar versie 1.1.0 Microsoft.ProjectOxford.Face:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="c0f0a-162">Alleen .NET Framework 4.6 wordt ondersteund, dus zorg ervoor dat uw *project.json* bestand geeft `net46` zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="c0f0a-163">Wanneer u uploadt een *project.json* bestand, de runtime opgehaald van de pakketten en verwijzingen naar de pakket-assembly's worden automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="c0f0a-164">U hoeft niet te voegen `#r "AssemblyName"` richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="c0f0a-165">Voeg de vereiste voor het gebruik van de typen gedefinieerd in de NuGet-pakketten `using` instructies voor uw *run.csx* bestand</span><span class="sxs-lookup"><span data-stu-id="c0f0a-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="c0f0a-166">In de runtime van Functions NuGet terugzetten werkt door te vergelijken `project.json` en `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="c0f0a-167">Als de stempels datum en tijd van de bestanden **niet** overeenkomst, een NuGet-herstelbewerking wordt uitgevoerd en NuGet downloads pakketten bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="c0f0a-168">Echter, als de stempels datum en tijd van de bestanden **doen** overeenkomen, NuGet voert een terugzetbewerking.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="c0f0a-169">Daarom `project.lock.json` moeten niet worden geïmplementeerd omdat het ervoor zorgt dat NuGet package restore overslaan.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="c0f0a-170">U kunt de implementatie van het vergrendelingsbestand voorkomen de `project.lock.json` naar de `.gitignore` bestand.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="c0f0a-171">Geef de feed in voor het gebruik van een aangepaste NuGet feed een *Nuget.Config* bestand in de hoofdmap van de functie-App.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="c0f0a-172">Zie voor meer informatie [NuGet configureren gedrag](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="c0f0a-173">Met behulp van een bestand project.json</span><span class="sxs-lookup"><span data-stu-id="c0f0a-173">Using a project.json file</span></span>
1. <span data-ttu-id="c0f0a-174">De functie openen in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="c0f0a-175">Het tabblad logboeken geeft de uitvoer van de installatie van pakket.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="c0f0a-176">Als u wilt een project.json-bestand uploadt, gebruikt u een van de methoden die worden beschreven de [het bijwerken van de functie app-bestanden](functions-reference.md#fileupdate) in het naslagonderwerp voor ontwikkelaars van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="c0f0a-177">Na de *project.json* bestand wordt geüpload, ziet u uitvoer zoals in het volgende voorbeeld in de functie de streaming-logboek:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="c0f0a-178">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-178">Environment variables</span></span>
<span data-ttu-id="c0f0a-179">Als u een omgevingsvariabele of een app die waarde instellen, gebruikt `System.Environment.GetEnvironmentVariable`, zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="c0f0a-180">Hergebruik van code .csx</span><span class="sxs-lookup"><span data-stu-id="c0f0a-180">Reusing .csx code</span></span>
<span data-ttu-id="c0f0a-181">U kunt klassen en methoden die zijn gedefinieerd in andere *.csx* bestanden in uw *run.csx* bestand.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="c0f0a-182">Gebruik hiervoor `#load` richtlijnen op uw *run.csx* bestand.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="c0f0a-183">In het volgende voorbeeld wordt een routine logboekregistratie met de naam `MyLogger` wordt gedeeld *myLogger.csx* en geladen in *run.csx* met behulp van de `#load` richtlijn:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="c0f0a-184">Voorbeeld *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="c0f0a-185">Voorbeeld *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="c0f0a-186">Met behulp van een gedeelde *.csx* is een algemene patroon wanneer u wilt uw sterk typeargumenten tussen functies met een POCO-object.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="c0f0a-187">In de volgende eenvoudige voorbeeld een HTTP-trigger en wachtrij-trigger delen een POCO-object met de naam `Order` sterk de volgorde om gegevens te typen:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="c0f0a-188">Voorbeeld *run.csx* voor HTTP-trigger:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="c0f0a-189">Voorbeeld *run.csx* voor wachtrij trigger:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="c0f0a-190">Voorbeeld *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="c0f0a-191">U kunt een relatief pad zijn met de `#load` richtlijn:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="c0f0a-192">`#load "mylogger.csx"`een bestand in de map van de functie laadt.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="c0f0a-193">`#load "loadedfiles\mylogger.csx"`een bestand in een map in de map functie laadt.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="c0f0a-194">`#load "..\shared\mylogger.csx"`een bestand in een map op hetzelfde niveau als de functie-map, dat wil zeggen, laadt rechtstreeks onder *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="c0f0a-195">De `#load` richtlijn werkt alleen met *.csx* (C# script)-bestanden, niet bij *.cs* bestanden.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="c0f0a-196">Binding tijdens runtime via imperatieve bindingen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="c0f0a-197">In C# en andere .NET-talen, kunt u een [imperatieve](https://en.wikipedia.org/wiki/Imperative_programming) binding patroon, niet de [ *declaratieve* ](https://en.wikipedia.org/wiki/Declarative_programming) bindingen in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="c0f0a-198">Imperatieve binding is handig wanneer bindende parameters moeten worden berekend tijdens runtime in plaats van ontwerp.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="c0f0a-199">U kunt met dit patroon binden aan de ondersteunde invoer en uitvoer van de binding op het moment in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="c0f0a-200">Definieer een imperatieve binding als volgt:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="c0f0a-201">**Geen** een vermelding in *function.json* voor uw gewenste imperatieve bindingen.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="c0f0a-202">Geeft een invoerparameter [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) of [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="c0f0a-203">De volgende C#-patroon gebruiken om uit te voeren van de gegevensbinding.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="c0f0a-204">waar `BindingTypeAttribute` is de .NET-kenmerk dat de binding wordt gedefinieerd en `T` is de invoer- of -type dat wordt ondersteund door deze bindingstype.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="c0f0a-205">`T`ook kan niet een `out` parametertype (zoals `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="c0f0a-206">Bijvoorbeeld, de tabel Mobile Apps binding ondersteunt uitvoer [zes typen uitvoer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), maar u kunt alleen [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) of [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) voor `T`.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="c0f0a-207">De volgende voorbeeldcode maakt een [Storage-blob uitvoer binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) met blob pad dat gedefinieerd tijdens runtime, hierna schrijft een tekenreeks naar de blob.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="c0f0a-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definieert de [Storage-blob](functions-bindings-storage-blob.md) invoer of uitvoer van de binding en [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is een ondersteunde binding uitvoertype.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="c0f0a-209">Als is, haalt de code in de standaardinstelling van de app voor de verbindingsreeks voor opslag-account (dit is `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="c0f0a-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="c0f0a-210">U kunt een aangepaste app-instelling te gebruiken door toe te voegen opgeven de [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) en het doorgeven van de kenmerk-matrix in `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="c0f0a-211">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-211">For example,</span></span>

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

<span data-ttu-id="c0f0a-212">De volgende tabel bevat de .NET-kenmerken voor elk bindingstype en de pakketten waarin ze worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c0f0a-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="c0f0a-213">Binding</span><span class="sxs-lookup"><span data-stu-id="c0f0a-213">Binding</span></span> | <span data-ttu-id="c0f0a-214">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="c0f0a-214">Attribute</span></span> | <span data-ttu-id="c0f0a-215">Verwijzing toevoegen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="c0f0a-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c0f0a-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="c0f0a-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c0f0a-217">Event Hubs</span></span> | <span data-ttu-id="c0f0a-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="c0f0a-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="c0f0a-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="c0f0a-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="c0f0a-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="c0f0a-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="c0f0a-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="c0f0a-221">Service Bus</span></span> | <span data-ttu-id="c0f0a-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="c0f0a-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="c0f0a-223">Storage-wachtrij</span><span class="sxs-lookup"><span data-stu-id="c0f0a-223">Storage queue</span></span> | <span data-ttu-id="c0f0a-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="c0f0a-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="c0f0a-225">Storage-blob</span><span class="sxs-lookup"><span data-stu-id="c0f0a-225">Storage blob</span></span> | <span data-ttu-id="c0f0a-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="c0f0a-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="c0f0a-227">Table Storage</span><span class="sxs-lookup"><span data-stu-id="c0f0a-227">Storage table</span></span> | <span data-ttu-id="c0f0a-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="c0f0a-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="c0f0a-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="c0f0a-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="c0f0a-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-230">Next steps</span></span>
<span data-ttu-id="c0f0a-231">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c0f0a-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="c0f0a-232">Aanbevolen procedures voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c0f0a-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="c0f0a-233">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c0f0a-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="c0f0a-234">Azure Functions F # referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c0f0a-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="c0f0a-235">Azure Functions NodeJS-referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c0f0a-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="c0f0a-236">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="c0f0a-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
