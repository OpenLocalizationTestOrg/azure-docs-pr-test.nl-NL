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
# <a name="azure-functions-f-developer-reference"></a>Naslaginformatie over Azure Functions-F # ontwikkelaars
> [!div class="op_single_selector"]
> * [C#-script](functions-reference-csharp.md)
> * [F # script](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # voor Azure Functions is een oplossing voor het eenvoudig uitvoeren van kleine stukjes code of 'functies' in de cloud Hallo. Gegevensstromen in de functie F # via functieargumenten. Argumentnamen zijn opgegeven in `function.json`, en er zijn vooraf gedefinieerde namen voor toegang tot bepaalde acties Hallo functie berichtenlogboek en annulering tokens.

In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).

## <a name="how-fsx-works"></a>De werking van .fsx
Een `.fsx` bestand is een script F #. Deze kan worden beschouwd als een F #-project dat opgenomen in één bestand. Hallo-bestand bevat zowel Hallo-code voor het programma (in dit geval uw Azure-functie) en richtlijnen voor het beheren van afhankelijkheden.

Als u werkt met een `.fsx` voor een Azure-functie vaak vereiste assembly's worden automatisch opgenomen voor u, zodat u toofocus op Hallo-functie in plaats van 'standaard' code.

## <a name="binding-tooarguments"></a>Binding tooarguments
Elke binding ondersteunt sommige set argumenten, als gedetailleerde in Hallo [Azure Functions triggers en bindingen naslaginformatie](functions-triggers-bindings.md). Een van de Hallo argument bindingen die biedt ondersteuning voor een blob-trigger is bijvoorbeeld een POCO die kan worden uitgedrukt met behulp van een record F #. Bijvoorbeeld:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

Uw Azure-functie F # duurt een of meer argumenten. Wanneer we over Azure Functions argumenten hebben, verwijzen we te*invoer* argumenten en *uitvoer* argumenten. Een invoerargument is precies deze klinkt als: invoer tooyour F # Azure-functie. Een *uitvoer* -argument is veranderlijke gegevens of een `byref<>` argument die als een manier toopass gegevens terug fungeert *uit* van de functie.

In vorige Hallo voorbeeld `blob` is een invoerargument en `output` is een argument van de uitvoer. U ziet dat we gebruikt `byref<>` voor `output` (Er is geen noodzaak tooadd hello `[<Out>]` aantekening). Met behulp van een `byref<>` type kunnen de functie toochange welke record of een object Hallo argument naar verwezen.

Wanneer een record F # wordt gebruikt als een invoertype, Hallo record definitie moet worden gemarkeerd met `[<CLIMutable>]` in volgorde tooallow hello Azure Functions framework tooset Hallo velden op de juiste wijze Hallo record tooyour functie voordat wordt doorgegeven. Achter de schermen hello, `[<CLIMutable>]` setters voor Hallo recordeigenschappen genereert. Bijvoorbeeld:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

Een klasse F # kan ook worden gebruikt voor zowel in- en argumenten. Voor een klasse moet eigenschappen meestal getters en setters. Bijvoorbeeld:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Logboekregistratie
toolog uitvoer tooyour [streaminglogboeken](../app-service-web/web-sites-streaming-logs-and-console.md) in F #, de functie moet rekening houden met een argument van het type `TraceWriter`. Voor consistentie, raden we dit argument heet `log`. Bijvoorbeeld:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Asynchrone
Hallo `async` werkstroom kan worden gebruikt, maar Hallo resultaat tooreturn moet een `Task`. Dit kan worden gedaan met `Async.StartAsTask`, bijvoorbeeld:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Annulering Token
Als de functie probleemloos toohandle afsluiten moet, u kunt daarvoor een [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument. Dit kan worden gecombineerd met `async`, bijvoorbeeld:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Naamruimten importeren
Naamruimten kan worden geopend in Hallo gebruikelijke manier:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hallo na naamruimten automatisch geopend:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Verwijzen naar externe assembly 's
Op deze manier framework-assembly verwijzingen worden toegevoegd met de Hallo `#r "AssemblyName"` richtlijn.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hallo worden volgende assembly's automatisch toegevoegd door hello Azure Functions hostomgeving:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Bovendien Hallo volgende assembly's zijn speciale geïntegreerd en kan worden verwezen door simplename (bijvoorbeeld `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Als u een persoonlijke assembly tooreference moet, kunt u uploaden Hallo assembly-bestand in een `bin` map relatieve tooyour functie en deze met behulp van de bestandsnaam (bijvoorbeeld Hallo-verwijzing  `#r "MyAssembly.dll"`). Zie voor informatie over hoe tooupload tooyour functie map bestanden, Hallo volgende sectie op het gebied van pakket.

## <a name="editor-prelude"></a>Editor Prelude
Een editor die ondersteuning biedt voor F # Compiler-Services worden niet op de hoogte van het Hallo-naamruimten en assembly's met Azure Functions automatisch. Als zodanig kan zijn nuttig tooinclude een prelude waarmee Hallo editor Hallo-assembly's die u gebruikt vinden en tooexplicitly open naamruimten. Bijvoorbeeld:

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

Wanneer uw code wordt uitgevoerd in Azure Functions, verwerkt Hallo bron met `COMPILED` gedefinieerd, zodat het Hallo-editor prelude worden genegeerd.

<a name="package"></a>

## <a name="package-management"></a>Pakket management
toouse NuGet-pakketten in een F # functie, Voeg een `project.json` toohello Hallo functie map in het bestandssysteem Hallo functie app-bestand. Hier volgt een voorbeeld `project.json` -bestand dat de verwijzing naar een NuGet-pakket te voegt`Microsoft.ProjectOxford.Face` versie 1.1.0:

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

Alleen hello .NET Framework 4.6 wordt ondersteund, dus zorg ervoor dat uw `project.json` bestand geeft `net46` zoals hier wordt weergegeven.

Wanneer u uploadt een `project.json` bestand, hello runtime opgehaald hello-pakketten en verwijzingen toohello pakket assembly's worden automatisch toegevoegd. U hoeft niet tooadd `#r "AssemblyName"` richtlijnen. Hallo vereist alleen toe te voegen `open` instructies tooyour `.fsx` bestand.

U kunt desgewenst tooput automatisch verwijst naar assembly's in uw editor prelude, tooimprove uw editor interactie met F # compileren Services.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Hoe tooadd een `project.json` bestand tooyour Azure-functie
1. Begin door te controleren of de functie-app wordt uitgevoerd, die u kunt doen door de functie openen in hello Azure-portal. Dit biedt ook toegang toohello streaminglogboeken waar pakket installatie uitvoer wordt weergegeven.
2. tooupload een `project.json` bestand, gebruikt u een Hallo methoden van [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate). Als u [continue implementatie voor Azure Functions](functions-continuous-deployment.md), kunt u toevoegen een `project.json` tooyour vertakking in volgorde tooexperiment aan voordat u het toevoegt tooyour implementatie vertakking tijdelijke bestand.
3. Na het Hallo `project.json` bestand wordt toegevoegd, ziet u uitvoer vergelijkbare toohello voorbeeld in de functie na de streaming-logboek:

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

## <a name="environment-variables"></a>Omgevingsvariabelen
tooget een omgevingsvariabele of een app-instelling-waarde gebruiken `System.Environment.GetEnvironmentVariable`, bijvoorbeeld:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Hergebruik van code .fsx
U kunt de code van andere `.fsx` bestanden met behulp van een `#load` richtlijn. Bijvoorbeeld:

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

Paden biedt toohello `#load` richtlijn zijn toohello relatieve locatie van uw `.fsx` bestand.

* `#load "logger.fsx"`een bestand in Hallo functie map laadt.
* `#load "package\logger.fsx"`een bestand in Hallo laadt `package` map in Hallo functie map.
* `#load "..\shared\mylogger.fsx"`een bestand in Hallo laadt `shared` map op hetzelfde niveau als Hallo functie map, dat wil zeggen, Hallo rechtstreeks onder `wwwroot`.

Hallo `#load` richtlijn werkt alleen met `.fsx` (F # script)-bestanden, en niet met `.fs` bestanden.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie Hallo resources te volgen:

* [F # handleiding](/dotnet/articles/fsharp/index)
* [Aanbevolen procedures voor Azure Functions](functions-best-practices.md)
* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)
* [Azure Functions C# referentie voor ontwikkelaars](functions-reference-csharp.md)
* [Azure Functions NodeJS-referentie voor ontwikkelaars](functions-reference-node.md)
* [Azure Functions-triggers en bindingen](functions-triggers-bindings.md)
* [Azure Functions testen](functions-test-a-function.md)
* [Azure Functions schalen](functions-scale.md)

