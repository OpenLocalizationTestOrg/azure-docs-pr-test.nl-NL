---
title: Werken met triggers en bindingen in de Azure Functions | Microsoft Docs
description: Informatie over het gebruik van triggers en bindingen in de Azure Functions verbinding maken met de uitvoering van uw code online gebeurtenissen en cloudservices.
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
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="b1b88-104">Azure Functions-triggers en bindingen concepten</span><span class="sxs-lookup"><span data-stu-id="b1b88-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="b1b88-105">Azure Functions, kunt u code te schrijven in reactie op gebeurtenissen in Azure en andere services via *triggers* en *bindingen*.</span><span class="sxs-lookup"><span data-stu-id="b1b88-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="b1b88-106">Dit artikel is een conceptueel overzicht van triggers en bindingen voor alle programmeertalen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b1b88-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="b1b88-107">Functies die gemeenschappelijk voor alle bindingen zijn worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="b1b88-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="b1b88-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b1b88-108">Overview</span></span>

<span data-ttu-id="b1b88-109">Triggers en bindingen zijn een declaratieve manier om te definiëren hoe een functie is aangeroepen en wat dit proces met werkt gegevens.</span><span class="sxs-lookup"><span data-stu-id="b1b88-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="b1b88-110">Een *trigger* definieert hoe een functie wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b1b88-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="b1b88-111">Een functie moet exact één trigger hebben.</span><span class="sxs-lookup"><span data-stu-id="b1b88-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="b1b88-112">Triggers hebt gekoppeld aan gegevens, die is meestal de nettolading waarmee de functie is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b1b88-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="b1b88-113">Invoer en uitvoer *bindingen* bieden een declaratieve manier verbinding maken met gegevens vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="b1b88-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="b1b88-114">Net als de triggers, geeft u verbindingsreeksen en andere eigenschappen in de configuratie van de functie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="b1b88-115">Bindingen zijn optioneel en een functie kunt meerdere invoer en uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="b1b88-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="b1b88-116">Met behulp van triggers en bindingen kunt u code schrijven die meer algemeen en heeft geen hardcode de details van de services met waarmee deze communiceert.</span><span class="sxs-lookup"><span data-stu-id="b1b88-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="b1b88-117">Gegevens die afkomstig zijn van de invoerwaarden services simpelweg zijn voor uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="b1b88-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="b1b88-118">Gebruik de retourwaarde van de methode om de uitvoer van gegevens op een andere service (zoals het maken van een nieuwe rij in de Azure Table Storage).</span><span class="sxs-lookup"><span data-stu-id="b1b88-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="b1b88-119">Of als u uitvoer van meerdere waarden moet, gebruikt u een helperobject.</span><span class="sxs-lookup"><span data-stu-id="b1b88-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="b1b88-120">Triggers en bindingen hebben een **naam** eigenschap, een id die u in uw code gebruiken voor toegang tot de binding.</span><span class="sxs-lookup"><span data-stu-id="b1b88-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="b1b88-121">U kunt configureren, triggers en bindingen in de **integreren** tabblad in de Azure Functions-portal.</span><span class="sxs-lookup"><span data-stu-id="b1b88-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="b1b88-122">Onder de behandelt de gebruikersinterface een bestand met de naam wijzigt *function.json* bestand in de map van de functie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="b1b88-123">U kunt dit bestand bewerken door te wijzigen in de **geavanceerde editor**.</span><span class="sxs-lookup"><span data-stu-id="b1b88-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="b1b88-124">De volgende tabel toont de triggers en bindingen die worden ondersteund door Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b1b88-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="b1b88-125">Voorbeeld: wachtrij trigger en tabel uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="b1b88-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="b1b88-126">Stel dat u een nieuwe rij naar Azure Table Storage schrijven telkens wanneer een nieuw bericht wordt weergegeven in Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="b1b88-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="b1b88-127">Dit scenario kan worden geïmplementeerd met behulp van een Azure-wachtrij trigger en een tabel uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="b1b88-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="b1b88-128">Een trigger wachtrij vereist de volgende gegevens in de **integreren** tabblad:</span><span class="sxs-lookup"><span data-stu-id="b1b88-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="b1b88-129">De naam van de app-instelling met de verbindingsreeks voor opslag-account voor de wachtrij</span><span class="sxs-lookup"><span data-stu-id="b1b88-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="b1b88-130">Naam van de wachtrij</span><span class="sxs-lookup"><span data-stu-id="b1b88-130">The queue name</span></span>
* <span data-ttu-id="b1b88-131">De id in uw code te lezen van de inhoud van het bericht uit de wachtrij, zoals `order`.</span><span class="sxs-lookup"><span data-stu-id="b1b88-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="b1b88-132">Voor het schrijven naar Azure Table Storage, gebruikt u een uitvoer-binding met de volgende details:</span><span class="sxs-lookup"><span data-stu-id="b1b88-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="b1b88-133">De naam van de app-instelling met de verbindingsreeks voor opslag-account voor de tabel</span><span class="sxs-lookup"><span data-stu-id="b1b88-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="b1b88-134">Naam van de tabel</span><span class="sxs-lookup"><span data-stu-id="b1b88-134">The table name</span></span>
* <span data-ttu-id="b1b88-135">De id in uw code maken Uitvoeritems, of de retourwaarde van de functie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="b1b88-136">Bindingen gebruik app-instellingen voor verbindingsreeksen om af te dwingen de beste praktijk die *function.json* bevat geen geheimen van de service.</span><span class="sxs-lookup"><span data-stu-id="b1b88-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="b1b88-137">Vervolgens gebruikt u de id's die u hebt opgegeven om te integreren met Azure Storage in uw code.</span><span class="sxs-lookup"><span data-stu-id="b1b88-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
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

<span data-ttu-id="b1b88-138">Hier volgt de *function.json* die overeenkomt met de bovenstaande code.</span><span class="sxs-lookup"><span data-stu-id="b1b88-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="b1b88-139">Houd er rekening mee dat dezelfde configuratie kan worden gebruikt, ongeacht de taal van de functie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

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
<span data-ttu-id="b1b88-140">Weergeven en bewerken van de inhoud van *function.json* in de Azure-portal klikt u op de **geavanceerde editor** kiezen op de **integreren** tabblad van de functie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="b1b88-141">Zie voor meer voorbeelden van code en meer informatie over de integratie met Azure Storage [Azure Functions triggers en bindingen voor Azure Storage](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b1b88-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="b1b88-142">Richting van de binding</span><span class="sxs-lookup"><span data-stu-id="b1b88-142">Binding direction</span></span>

<span data-ttu-id="b1b88-143">Alle triggers en bindingen hebben een `direction` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="b1b88-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="b1b88-144">Voor triggers is de richting altijd`in`</span><span class="sxs-lookup"><span data-stu-id="b1b88-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="b1b88-145">Invoer- en uitvoergegevens bindingen gebruiken `in` en`out`</span><span class="sxs-lookup"><span data-stu-id="b1b88-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="b1b88-146">Sommige bindingen ondersteuning voor een speciale richting `inout`.</span><span class="sxs-lookup"><span data-stu-id="b1b88-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="b1b88-147">Als u `inout`, alleen de **geavanceerde editor** is beschikbaar in de **integreren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b1b88-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="b1b88-148">Het retourtype van functie gebruiken om te retourneren van één uitvoer</span><span class="sxs-lookup"><span data-stu-id="b1b88-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="b1b88-149">Het vorige voorbeeld laat zien hoe de geretourneerde waarde van de functie gebruiken voor uitvoer naar een binding die wordt bereikt door middel van de parameter voor de speciale `$return`.</span><span class="sxs-lookup"><span data-stu-id="b1b88-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="b1b88-150">(Dit wordt alleen ondersteund in de talen die u een retourwaarde, zoals C#, JavaScript en F hebt #.) Als een functie meerdere bindingen van de uitvoer heeft, gebruikt u `$return` voor slechts één van de uitvoer-bindingen.</span><span class="sxs-lookup"><span data-stu-id="b1b88-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="b1b88-151">De voorbeelden hieronder tonen retourneren hoe typen worden gebruikt met bindingen in C#, JavaScript en F # uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b1b88-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in the second parameter to context.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="b1b88-152">De eigenschap dataType binding</span><span class="sxs-lookup"><span data-stu-id="b1b88-152">Binding dataType property</span></span>

<span data-ttu-id="b1b88-153">Gebruik in .NET de typen voor het definiëren van het gegevenstype voor invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="b1b88-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="b1b88-154">Gebruik bijvoorbeeld `string` verbinding maken met de tekst van de trigger van een wachtrij en een bytematrix lezen als binair.</span><span class="sxs-lookup"><span data-stu-id="b1b88-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="b1b88-155">Voor de talen die dynamisch worden getypeerd zoals JavaScript, gebruikt u de `dataType` eigenschap in de definitie van de binding.</span><span class="sxs-lookup"><span data-stu-id="b1b88-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="b1b88-156">Gebruik bijvoorbeeld om te lezen van de inhoud van een HTTP-aanvraag in binaire indeling, het type `binary`:</span><span class="sxs-lookup"><span data-stu-id="b1b88-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="b1b88-157">Andere opties voor `dataType` zijn `stream` en `string`.</span><span class="sxs-lookup"><span data-stu-id="b1b88-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="b1b88-158">Het omzetten van app-instellingen</span><span class="sxs-lookup"><span data-stu-id="b1b88-158">Resolving app settings</span></span>
<span data-ttu-id="b1b88-159">Als een best practice moeten geheimen en verbindingsreeksen worden beheerd met behulp van app-instellingen, in plaats van configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="b1b88-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="b1b88-160">Dit beperkt de toegang tot deze geheime gegevens en wordt het veilig om op te slaan *function.json* in een openbare resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="b1b88-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="b1b88-161">App-instellingen zijn ook nuttig wanneer u configuratie wilt wijzigen op basis van de omgeving.</span><span class="sxs-lookup"><span data-stu-id="b1b88-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="b1b88-162">In een testomgeving kunt u bijvoorbeeld voor het bewaken van een andere wachtrij of blob storage-container.</span><span class="sxs-lookup"><span data-stu-id="b1b88-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="b1b88-163">Appinstellingen zijn opgelost wanneer een waarde procenttekens, zoals tussen `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="b1b88-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="b1b88-164">Houd er rekening mee dat de `connection` eigenschap van triggers en bindingen is een speciaal geval en -waarden als de app-instellingen automatisch worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="b1b88-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="b1b88-165">Het volgende voorbeeld wordt een wachtrij-trigger die gebruikmaakt van een app-instelling `%input-queue-name%` voor het definiëren van de wachtrij voor het activeren van op.</span><span class="sxs-lookup"><span data-stu-id="b1b88-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="b1b88-166">Eigenschappen van de trigger-metagegevens</span><span class="sxs-lookup"><span data-stu-id="b1b88-166">Trigger metadata properties</span></span>

<span data-ttu-id="b1b88-167">Naast de nettolading van de gegevens die is geleverd door een trigger (zoals een bericht in de wachtrij waarmee een functie is geactiveerd), bieden veel triggers aanvullende metagegevenswaarden.</span><span class="sxs-lookup"><span data-stu-id="b1b88-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="b1b88-168">Deze waarden kunnen worden gebruikt als de invoerparameters in C# en F # of eigenschappen op de `context.bindings` -object in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1b88-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="b1b88-169">Een wachtrij-trigger ondersteunt bijvoorbeeld de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="b1b88-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="b1b88-170">QueueTrigger - activering van de inhoud van het bericht als een geldige tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b1b88-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="b1b88-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="b1b88-171">DequeueCount</span></span>
* <span data-ttu-id="b1b88-172">expirationTime</span><span class="sxs-lookup"><span data-stu-id="b1b88-172">ExpirationTime</span></span>
* <span data-ttu-id="b1b88-173">Id</span><span class="sxs-lookup"><span data-stu-id="b1b88-173">Id</span></span>
* <span data-ttu-id="b1b88-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="b1b88-174">InsertionTime</span></span>
* <span data-ttu-id="b1b88-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="b1b88-175">NextVisibleTime</span></span>
* <span data-ttu-id="b1b88-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="b1b88-176">PopReceipt</span></span>

<span data-ttu-id="b1b88-177">Details van de eigenschappen van de metagegevens voor elke trigger worden beschreven in het bijbehorende naslagonderwerp.</span><span class="sxs-lookup"><span data-stu-id="b1b88-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="b1b88-178">Documentatie is ook beschikbaar in de **integreren** tabblad van de portal in de **documentatie** hieronder de configuratiegebied binding.</span><span class="sxs-lookup"><span data-stu-id="b1b88-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="b1b88-179">Bijvoorbeeld, aangezien blob triggers sommige vertragingen hebben, kunt u een wachtrij-trigger voor het uitvoeren uw functie (Zie [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="b1b88-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="b1b88-180">Bericht uit de wachtrij kan de blob filename activeren op zou bevatten.</span><span class="sxs-lookup"><span data-stu-id="b1b88-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="b1b88-181">Met behulp van de `queueTrigger` metagegevenseigenschap, kunt u dit gedrag in uw configuratie, in plaats van uw code.</span><span class="sxs-lookup"><span data-stu-id="b1b88-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="b1b88-182">Eigenschappen van de metagegevens van een trigger kunnen ook worden gebruikt een *bindende expressie* voor een andere binding, zoals beschreven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="b1b88-183">Expressies voor gegevensbinding en patronen</span><span class="sxs-lookup"><span data-stu-id="b1b88-183">Binding expressions and patterns</span></span>

<span data-ttu-id="b1b88-184">Een van de meest krachtige functies van triggers en bindingen is *bindingsexpressies*.</span><span class="sxs-lookup"><span data-stu-id="b1b88-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="b1b88-185">U kunt patroon expressies die vervolgens kunnen worden gebruikt binnen uw binding definiëren in andere bindingen of uw code.</span><span class="sxs-lookup"><span data-stu-id="b1b88-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="b1b88-186">Metagegevens van de trigger kan ook worden gebruikt in expressies binding als weergeven in het voorbeeld in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="b1b88-187">Stel bijvoorbeeld dat u wilt dat het formaat van afbeeldingen in bepaalde blob storage-container, vergelijkbaar met de **Image-aanwijzer Formaat** sjabloon in de **nieuwe functie** pagina.</span><span class="sxs-lookup"><span data-stu-id="b1b88-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="b1b88-188">Ga naar **nieuwe functie** -> taal **C#** -> Scenario **voorbeelden** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="b1b88-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="b1b88-189">Hier volgt de *function.json* definitie:</span><span class="sxs-lookup"><span data-stu-id="b1b88-189">Here is the *function.json* definition:</span></span>

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

<span data-ttu-id="b1b88-190">U ziet dat de `filename` parameter wordt gebruikt in zowel de definitie van de blob, evenals de blob uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="b1b88-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="b1b88-191">Deze parameter kan ook worden gebruikt in de functiecode.</span><span class="sxs-lookup"><span data-stu-id="b1b88-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="b1b88-192">Willekeurige GUID 's</span><span class="sxs-lookup"><span data-stu-id="b1b88-192">Random GUIDs</span></span>
<span data-ttu-id="b1b88-193">Azure Functions bevat een gemak-syntaxis voor het genereren van GUID's in uw bindingen via de `{rand-guid}` bindende expressie.</span><span class="sxs-lookup"><span data-stu-id="b1b88-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="b1b88-194">Het volgende voorbeeld wordt dit gebruikt voor het genereren van een unieke blob-naam:</span><span class="sxs-lookup"><span data-stu-id="b1b88-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="b1b88-195">Huidige tijd</span><span class="sxs-lookup"><span data-stu-id="b1b88-195">Current time</span></span>

<span data-ttu-id="b1b88-196">U kunt de expressie voor gegevensbinding `DateTime`, die wordt omgezet naar `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="b1b88-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="b1b88-197">Verbinding maken met aangepaste eigenschappen voor de invoer in een expressie voor gegevensbinding</span><span class="sxs-lookup"><span data-stu-id="b1b88-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="b1b88-198">Bindingsexpressies kan ook verwijzen naar eigenschappen die zijn gedefinieerd in de nettolading van de trigger.</span><span class="sxs-lookup"><span data-stu-id="b1b88-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="b1b88-199">U wilt bijvoorbeeld dynamisch binding met een blob storage-bestand uit een bestandsnaam is opgegeven in een webhook.</span><span class="sxs-lookup"><span data-stu-id="b1b88-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="b1b88-200">Bijvoorbeeld de volgende *function.json* maakt gebruik van een eigenschap genaamd `BlobName` van de nettolading van de trigger:</span><span class="sxs-lookup"><span data-stu-id="b1b88-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

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

<span data-ttu-id="b1b88-201">U kunt dit doen in C# en F #, moet u een POCO waarin de velden die zullen worden gedeserialiseerd in de nettolading van de trigger definiëren.</span><span class="sxs-lookup"><span data-stu-id="b1b88-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

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

<span data-ttu-id="b1b88-202">JSON-deserialisatie wordt automatisch uitgevoerd in JavaScript, en kunt u de eigenschappen rechtstreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b1b88-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="b1b88-203">Configureren van die gegevens bindt tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="b1b88-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="b1b88-204">In C# en andere .NET-talen, kunt u een patroon imperatieve binding in plaats van de declaratieve bindingen in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="b1b88-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="b1b88-205">Imperatieve binding is handig wanneer bindende parameters moeten worden berekend tijdens runtime in plaats van ontwerp.</span><span class="sxs-lookup"><span data-stu-id="b1b88-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="b1b88-206">Zie voor meer informatie, [Binding tijdens runtime via imperatieve bindingen](functions-reference-csharp.md#imperative-bindings) in de C# naslaginformatie voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b1b88-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b88-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1b88-207">Next steps</span></span>
<span data-ttu-id="b1b88-208">Zie de volgende artikelen voor meer informatie over een specifieke binding:</span><span class="sxs-lookup"><span data-stu-id="b1b88-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="b1b88-209">HTTP en webhooks</span><span class="sxs-lookup"><span data-stu-id="b1b88-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="b1b88-210">Timer</span><span class="sxs-lookup"><span data-stu-id="b1b88-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="b1b88-211">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="b1b88-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="b1b88-212">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b1b88-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="b1b88-213">Table Storage</span><span class="sxs-lookup"><span data-stu-id="b1b88-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="b1b88-214">Event Hub</span><span class="sxs-lookup"><span data-stu-id="b1b88-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="b1b88-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b1b88-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="b1b88-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b1b88-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="b1b88-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="b1b88-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="b1b88-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="b1b88-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="b1b88-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="b1b88-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="b1b88-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="b1b88-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="b1b88-221">Extern bestand</span><span class="sxs-lookup"><span data-stu-id="b1b88-221">External file</span></span>](functions-bindings-external-file.md)
