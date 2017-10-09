---
title: aaaWork met triggers en bindingen in de Azure Functions | Microsoft Docs
description: Informatie over hoe toouse triggers en bindingen in de Azure Functions tooconnect uw code uitvoering tooonline gebeurtenissen en cloud-gebaseerde services.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="1c256-104">Azure Functions-triggers en bindingen concepten</span><span class="sxs-lookup"><span data-stu-id="1c256-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="1c256-105">Azure Functions kunt u toowrite code in het antwoord tooevents in Azure en andere services via *triggers* en *bindingen*.</span><span class="sxs-lookup"><span data-stu-id="1c256-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="1c256-106">Dit artikel is een conceptueel overzicht van triggers en bindingen voor alle programmeertalen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1c256-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="1c256-107">Functies die algemene tooall bindingen zijn worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="1c256-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="1c256-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1c256-108">Overview</span></span>

<span data-ttu-id="1c256-109">Triggers en bindingen zijn een declaratieve manier toodefine hoe een functie is aangeroepen en welke gegevens het werkt met.</span><span class="sxs-lookup"><span data-stu-id="1c256-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="1c256-110">Een *trigger* definieert hoe een functie wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1c256-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="1c256-111">Een functie moet exact één trigger hebben.</span><span class="sxs-lookup"><span data-stu-id="1c256-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="1c256-112">Triggers hebt gekoppeld aan gegevens, die is gewoonlijk het Hallo-nettolading waarmee Hallo-functie is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1c256-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="1c256-113">Invoer en uitvoer *bindingen* bieden een declaratieve manier tooconnect toodata vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="1c256-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="1c256-114">Vergelijkbare tootriggers, geeft u verbindingsreeksen en andere eigenschappen in de configuratie van de functie.</span><span class="sxs-lookup"><span data-stu-id="1c256-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="1c256-115">Bindingen zijn optioneel en een functie kunt meerdere invoer en uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="1c256-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="1c256-116">Met triggers en bindingen kunt u code die is meer algemeen en heeft dit geen hardcode Hallo details over Hallo services waarmee deze communiceert schrijven.</span><span class="sxs-lookup"><span data-stu-id="1c256-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="1c256-117">Gegevens die afkomstig zijn van de invoerwaarden services simpelweg zijn voor uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="1c256-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="1c256-118">toooutput gegevensservice tooanother (zoals het maken van een nieuwe rij in de Azure Table Storage), gebruik Hallo geretourneerde waarde van Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="1c256-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="1c256-119">Of als u toooutput meerdere waarden moet, gebruikt u een helperobject.</span><span class="sxs-lookup"><span data-stu-id="1c256-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="1c256-120">Triggers en bindingen hebben een **naam** eigenschap, die een id die u in uw code tooaccess Hallo-binding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c256-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="1c256-121">U kunt triggers en bindingen configureren in Hallo **integreren** tabblad in hello Azure Functions-portal.</span><span class="sxs-lookup"><span data-stu-id="1c256-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="1c256-122">Onder Hallo-dekt Hallo gebruikersinterface een bestand met de naam wijzigt *function.json* in Hallo functie map.</span><span class="sxs-lookup"><span data-stu-id="1c256-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="1c256-123">U kunt dit bestand bewerken door het wijzigen van toohello **geavanceerde editor**.</span><span class="sxs-lookup"><span data-stu-id="1c256-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="1c256-124">Hallo volgende tabel toont Hallo triggers en bindingen die worden ondersteund door Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1c256-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="1c256-125">Voorbeeld: wachtrij trigger en tabel uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="1c256-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="1c256-126">Stel dat u een nieuwe rij tooAzure Table Storage toowrite wilt zien wanneer een nieuw bericht wordt weergegeven in Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="1c256-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="1c256-127">Dit scenario kan worden geïmplementeerd met behulp van een Azure-wachtrij trigger en een tabel uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="1c256-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="1c256-128">Een trigger wachtrij vereist Hallo volgende informatie in Hallo **integreren** tabblad:</span><span class="sxs-lookup"><span data-stu-id="1c256-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="1c256-129">Hallo-naam van app-instelling voor Hallo Hallo account verbindingsreeks voor opslag voor Hallo wachtrij met</span><span class="sxs-lookup"><span data-stu-id="1c256-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="1c256-130">de wachtrijnaam Hallo</span><span class="sxs-lookup"><span data-stu-id="1c256-130">hello queue name</span></span>
* <span data-ttu-id="1c256-131">Hallo-id in de inhoud van uw code tooread Hallo van wachtrij het Hallo-bericht, zoals `order`.</span><span class="sxs-lookup"><span data-stu-id="1c256-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="1c256-132">een binding uitvoer toowrite tooAzure Table Storage gebruiken met Hallo volgende details:</span><span class="sxs-lookup"><span data-stu-id="1c256-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="1c256-133">Hallo-naam van app-instelling voor Hallo Hallo account verbindingsreeks voor opslag voor Hallo tabel met</span><span class="sxs-lookup"><span data-stu-id="1c256-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="1c256-134">Hallo-tabelnaam</span><span class="sxs-lookup"><span data-stu-id="1c256-134">hello table name</span></span>
* <span data-ttu-id="1c256-135">Hallo-id in uw code toocreate items of Hallo geretourneerde waarde van Hallo-functie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1c256-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="1c256-136">Bindingen app-instellingen gebruiken voor verbinding tekenreeksen tooenforce Hallo beste praktijk die *function.json* bevat geen geheimen van de service.</span><span class="sxs-lookup"><span data-stu-id="1c256-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="1c256-137">Gebruik vervolgens Hallo-id's die u opgaf toointegrate met Azure Storage in uw code.</span><span class="sxs-lookup"><span data-stu-id="1c256-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="1c256-138">Hier volgt Hallo *function.json* die overeenkomt met toohello voorafgaand aan code.</span><span class="sxs-lookup"><span data-stu-id="1c256-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="1c256-139">Houd er rekening mee dat dezelfde configuratie kan worden gebruikt, ongeacht de taal van functie-implementatie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="1c256-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="1c256-140">inhoud van de Hallo tooview en bewerken van *function.json* in hello Azure-portal, klikt u op Hallo **geavanceerde editor** optie op Hallo **integreren** tabblad van de functie.</span><span class="sxs-lookup"><span data-stu-id="1c256-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="1c256-141">Zie voor meer voorbeelden van code en meer informatie over de integratie met Azure Storage [Azure Functions triggers en bindingen voor Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1c256-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="1c256-142">Richting van de binding</span><span class="sxs-lookup"><span data-stu-id="1c256-142">Binding direction</span></span>

<span data-ttu-id="1c256-143">Alle triggers en bindingen hebben een `direction` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="1c256-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="1c256-144">Voor triggers is Hallo richting altijd`in`</span><span class="sxs-lookup"><span data-stu-id="1c256-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="1c256-145">Invoer- en uitvoergegevens bindingen gebruiken `in` en`out`</span><span class="sxs-lookup"><span data-stu-id="1c256-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="1c256-146">Sommige bindingen ondersteuning voor een speciale richting `inout`.</span><span class="sxs-lookup"><span data-stu-id="1c256-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="1c256-147">Als u `inout`, alleen Hallo **geavanceerde editor** is beschikbaar in Hallo **integreren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1c256-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="1c256-148">Met behulp van Hallo functie retourtype tooreturn één uitvoer</span><span class="sxs-lookup"><span data-stu-id="1c256-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="1c256-149">Hallo voorgaande voorbeeld ziet u hoe toouse Hallo functie retourwaarde tooprovide tooa binding die wordt bereikt door middel van de speciale parameter Hallo uitvoer `$return`.</span><span class="sxs-lookup"><span data-stu-id="1c256-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="1c256-150">(Dit wordt alleen ondersteund in de talen die u een retourwaarde, zoals C#, JavaScript en F hebt #.) Als een functie meerdere bindingen van de uitvoer heeft, gebruikt u `$return` voor slechts één Hallo uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="1c256-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="1c256-151">Hallo-voorbeelden hieronder tonen retourneren hoe typen worden gebruikt met bindingen in C#, JavaScript en F # uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1c256-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="1c256-152">De eigenschap dataType binding</span><span class="sxs-lookup"><span data-stu-id="1c256-152">Binding dataType property</span></span>

<span data-ttu-id="1c256-153">Gebruik in .NET Hallo typen toodefine Hallo-gegevenstype voor invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="1c256-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="1c256-154">Gebruik bijvoorbeeld `string` toobind toohello tekst van de trigger van een wachtrij en een byte-matrix tooread als binair.</span><span class="sxs-lookup"><span data-stu-id="1c256-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="1c256-155">Gebruik voor de talen die dynamisch worden getypeerd zoals JavaScript, Hallo `dataType` eigenschap in de definitie van de binding Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c256-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="1c256-156">Bijvoorbeeld: tooread Hallo inhoud van een HTTP-aanvraag in binaire indeling, gebruik Hallo type `binary`:</span><span class="sxs-lookup"><span data-stu-id="1c256-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="1c256-157">Andere opties voor `dataType` zijn `stream` en `string`.</span><span class="sxs-lookup"><span data-stu-id="1c256-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="1c256-158">Het omzetten van app-instellingen</span><span class="sxs-lookup"><span data-stu-id="1c256-158">Resolving app settings</span></span>
<span data-ttu-id="1c256-159">Als een best practice moeten geheimen en verbindingsreeksen worden beheerd met behulp van app-instellingen, in plaats van configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="1c256-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="1c256-160">Dit beperkt toegang toothese geheimen en maakt het veilige toostore *function.json* in een openbare resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="1c256-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="1c256-161">App-instellingen zijn ook handig wanneer u wilt dat toochange configuratie op basis van Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1c256-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="1c256-162">In een testomgeving kunt u bijvoorbeeld toomonitor een andere wachtrij of blob storage-container.</span><span class="sxs-lookup"><span data-stu-id="1c256-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="1c256-163">Appinstellingen zijn opgelost wanneer een waarde procenttekens, zoals tussen `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="1c256-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="1c256-164">Houd er rekening mee dat Hallo `connection` eigenschap van triggers en bindingen is een speciaal geval en -waarden als de app-instellingen automatisch worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="1c256-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="1c256-165">Hallo volgende voorbeeld wordt een wachtrij-trigger die gebruikmaakt van een app-instelling `%input-queue-name%` toodefine Hallo wachtrij tootrigger op.</span><span class="sxs-lookup"><span data-stu-id="1c256-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="1c256-166">Eigenschappen van de trigger-metagegevens</span><span class="sxs-lookup"><span data-stu-id="1c256-166">Trigger metadata properties</span></span>

<span data-ttu-id="1c256-167">In de nettolading voor toevoeging toohello geleverd door een trigger (zoals Hallo wachtrijbericht waarmee een functie is geactiveerd), veel triggers bieden aanvullende metagegevenswaarden.</span><span class="sxs-lookup"><span data-stu-id="1c256-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="1c256-168">Deze waarden kunnen worden gebruikt als de invoerparameters in C# en F # of eigenschappen op Hallo `context.bindings` -object in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1c256-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="1c256-169">Een wachtrij-trigger ondersteunt bijvoorbeeld Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="1c256-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="1c256-170">QueueTrigger - activering van de inhoud van het bericht als een geldige tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1c256-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="1c256-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="1c256-171">DequeueCount</span></span>
* <span data-ttu-id="1c256-172">expirationTime</span><span class="sxs-lookup"><span data-stu-id="1c256-172">ExpirationTime</span></span>
* <span data-ttu-id="1c256-173">Id</span><span class="sxs-lookup"><span data-stu-id="1c256-173">Id</span></span>
* <span data-ttu-id="1c256-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="1c256-174">InsertionTime</span></span>
* <span data-ttu-id="1c256-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="1c256-175">NextVisibleTime</span></span>
* <span data-ttu-id="1c256-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="1c256-176">PopReceipt</span></span>

<span data-ttu-id="1c256-177">Details van de eigenschappen van de metagegevens voor elke trigger worden beschreven in de bijbehorende naslagonderwerp Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c256-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="1c256-178">Documentatie is ook beschikbaar in Hallo **integreren** tabblad van het Hallo-portal in Hallo **documentatie** hieronder configuratiegebied Hallo-binding.</span><span class="sxs-lookup"><span data-stu-id="1c256-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="1c256-179">Bijvoorbeeld, omdat het blob-triggers vertragingen voordoen, kunt u een wachtrij trigger toorun uw-functie (Zie [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="1c256-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="1c256-180">Hallo-bericht van wachtrij zou Hallo blob filename tootrigger op bevatten.</span><span class="sxs-lookup"><span data-stu-id="1c256-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="1c256-181">Met behulp van Hallo `queueTrigger` metagegevenseigenschap, kunt u dit gedrag in uw configuratie, in plaats van uw code.</span><span class="sxs-lookup"><span data-stu-id="1c256-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="1c256-182">Eigenschappen van de metagegevens van een trigger kunnen ook worden gebruikt een *bindende expressie* voor een andere binding, als beschreven in Hallo volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="1c256-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="1c256-183">Expressies voor gegevensbinding en patronen</span><span class="sxs-lookup"><span data-stu-id="1c256-183">Binding expressions and patterns</span></span>

<span data-ttu-id="1c256-184">Een van de meest krachtige functies Hallo van triggers en bindingen is *bindingsexpressies*.</span><span class="sxs-lookup"><span data-stu-id="1c256-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="1c256-185">U kunt patroon expressies die vervolgens kunnen worden gebruikt binnen uw binding definiëren in andere bindingen of uw code.</span><span class="sxs-lookup"><span data-stu-id="1c256-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="1c256-186">Metagegevens van de trigger kan ook worden gebruikt in expressies als weergeven in voorbeeld in de voorgaande sectie Hallo Hallo binding.</span><span class="sxs-lookup"><span data-stu-id="1c256-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="1c256-187">Stel bijvoorbeeld dat u wilt dat tooresize afbeeldingen in bepaalde blob storage-container, vergelijkbare toohello **Image-aanwijzer Formaat** sjabloon in Hallo **nieuwe functie** pagina.</span><span class="sxs-lookup"><span data-stu-id="1c256-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="1c256-188">Ga te**nieuwe functie** -> taal **C#** -> Scenario **voorbeelden** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="1c256-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="1c256-189">Hier volgt Hallo *function.json* definitie:</span><span class="sxs-lookup"><span data-stu-id="1c256-189">Here is hello *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="1c256-190">U ziet dat Hallo `filename` parameter wordt gebruikt in zowel de definitie van de trigger blob Hallo als Hallo blob uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="1c256-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="1c256-191">Deze parameter kan ook worden gebruikt in de functiecode.</span><span class="sxs-lookup"><span data-stu-id="1c256-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="1c256-192">Willekeurige GUID 's</span><span class="sxs-lookup"><span data-stu-id="1c256-192">Random GUIDs</span></span>
<span data-ttu-id="1c256-193">Azure Functions bevat een gemak-syntaxis voor het genereren van GUID's in uw bindingen, via Hallo `{rand-guid}` bindende expressie.</span><span class="sxs-lookup"><span data-stu-id="1c256-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="1c256-194">Hallo wordt volgende voorbeeld een unieke blob-naam van deze toogenerate:</span><span class="sxs-lookup"><span data-stu-id="1c256-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="1c256-195">Huidige tijd</span><span class="sxs-lookup"><span data-stu-id="1c256-195">Current time</span></span>

<span data-ttu-id="1c256-196">U kunt een expressie voor gegevensbinding Hallo `DateTime`, die wordt omgezet te`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="1c256-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="1c256-197">Invoereigenschappen toocustom binding in een expressie voor gegevensbinding</span><span class="sxs-lookup"><span data-stu-id="1c256-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="1c256-198">Bindingsexpressies kan ook verwijzen naar eigenschappen die zijn gedefinieerd in Hallo trigger nettolading zelf.</span><span class="sxs-lookup"><span data-stu-id="1c256-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="1c256-199">U kunt bijvoorbeeld toodynamically bind tooa blob storage-bestand van een bestandsnaam is opgegeven in een webhook.</span><span class="sxs-lookup"><span data-stu-id="1c256-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="1c256-200">Bijvoorbeeld Hallo na *function.json* maakt gebruik van een eigenschap genaamd `BlobName` van Hallo trigger nettolading:</span><span class="sxs-lookup"><span data-stu-id="1c256-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="1c256-201">tooaccomplish deze in C#- en F #, moet u een POCO die definieert Hallo velden die zullen worden gedeserialiseerd in Hallo trigger nettolading definiëren.</span><span class="sxs-lookup"><span data-stu-id="1c256-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="1c256-202">JSON-deserialisatie wordt automatisch uitgevoerd in JavaScript, en kunt u rechtstreeks Hallo eigenschappen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c256-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="1c256-203">Configureren van die gegevens bindt tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="1c256-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="1c256-204">In C# en andere .NET-talen, kunt u een patroon imperatieve binding gebruiken als declaratieve bindingen in tegenstelling tot toohello *function.json*.</span><span class="sxs-lookup"><span data-stu-id="1c256-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="1c256-205">Imperatieve binding is handig als bindparameters toobe berekend tijdens runtime in plaats van ontwerp moeten.</span><span class="sxs-lookup"><span data-stu-id="1c256-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="1c256-206">toolearn meer, Zie [Binding tijdens runtime via imperatieve bindingen](functions-reference-csharp.md#imperative-bindings) in Hallo C#-referentie voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1c256-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c256-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c256-207">Next steps</span></span>
<span data-ttu-id="1c256-208">Zie voor meer informatie over een specifieke binding Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c256-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="1c256-209">HTTP en webhooks</span><span class="sxs-lookup"><span data-stu-id="1c256-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="1c256-210">Timer</span><span class="sxs-lookup"><span data-stu-id="1c256-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="1c256-211">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="1c256-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="1c256-212">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1c256-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="1c256-213">Table Storage</span><span class="sxs-lookup"><span data-stu-id="1c256-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="1c256-214">Event Hub</span><span class="sxs-lookup"><span data-stu-id="1c256-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="1c256-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="1c256-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="1c256-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1c256-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="1c256-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="1c256-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="1c256-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="1c256-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="1c256-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="1c256-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="1c256-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="1c256-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="1c256-221">Extern bestand</span><span class="sxs-lookup"><span data-stu-id="1c256-221">External file</span></span>](functions-bindings-external-file.md)
