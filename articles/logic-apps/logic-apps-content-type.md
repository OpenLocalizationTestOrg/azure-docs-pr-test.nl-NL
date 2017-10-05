---
title: Verwerken van de typen inhoud - Azure Logic Apps | Microsoft Docs
description: Hoe Azure Logic Apps omgaat met inhoudstypen in de ontwerp- en runtime
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="8b15c-103">De inhoudstypen die ingang in logic apps</span><span class="sxs-lookup"><span data-stu-id="8b15c-103">Handle content types in logic apps</span></span>

<span data-ttu-id="8b15c-104">Veel verschillende typen inhoud kunnen door een logische app, met inbegrip van de JSON, XML, platte bestanden en binaire gegevens stromen.</span><span class="sxs-lookup"><span data-stu-id="8b15c-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="8b15c-105">Terwijl de Logic Apps-Engine alle typen inhoud ondersteunt, worden sommige systeemeigen begrepen door de Engine voor Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="8b15c-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="8b15c-106">Anderen mogelijk casten of conversies indien nodig.</span><span class="sxs-lookup"><span data-stu-id="8b15c-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="8b15c-107">In dit artikel wordt beschreven hoe de engine voor verschillende typen inhoud verwerkt en hoe deze typen indien nodig de juiste manier verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8b15c-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="8b15c-108">Content-Type-Header</span><span class="sxs-lookup"><span data-stu-id="8b15c-108">Content-Type Header</span></span>

<span data-ttu-id="8b15c-109">Om te starten in feite, bekijken we de twee `Content-Types` waarvoor geen conversie of casten die u in een logische app gebruiken kunt: `application/json` en `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="8b15c-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="8b15c-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="8b15c-110">Application/JSON</span></span>

<span data-ttu-id="8b15c-111">De werkstroom-engine is afhankelijk van de `Content-Type` kop van HTTP-aanroepen om te bepalen van de juiste verwerking.</span><span class="sxs-lookup"><span data-stu-id="8b15c-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="8b15c-112">Een aanvraag met het type inhoud `application/json` wordt opgeslagen en verwerkt als een JSON-Object.</span><span class="sxs-lookup"><span data-stu-id="8b15c-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="8b15c-113">JSON-inhoud kan ook standaard zonder eventuele casten worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="8b15c-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="8b15c-114">U kan bijvoorbeeld een aanvraag waarvoor de header inhoudstype parseren `application/json ` in een werkstroom met behulp van een expressie zoals `@body('myAction')['foo'][0]` om de waarde `bar` in dit geval:</span><span class="sxs-lookup"><span data-stu-id="8b15c-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="8b15c-115">Er is geen aanvullende casten nodig.</span><span class="sxs-lookup"><span data-stu-id="8b15c-115">No additional casting is needed.</span></span> <span data-ttu-id="8b15c-116">Als u met gegevens die JSON is, maar niet een header die is opgegeven werkt, u kunt handmatig dit casten naar JSON met behulp van de `@json()` functioneren, bijvoorbeeld: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="8b15c-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="8b15c-117">Schema- en schema-generator</span><span class="sxs-lookup"><span data-stu-id="8b15c-117">Schema and schema generator</span></span>

<span data-ttu-id="8b15c-118">De aanvraag-trigger kunt u het invoeren van een JSON-schema voor de nettolading die u verwacht te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8b15c-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="8b15c-119">Dit schema kunt de tokens designer genereren zodat u de inhoud van de aanvraag kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b15c-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="8b15c-120">Als u een schema gereed geen hebt, selecteert u **gebruik voorbeeld nettolading voor het genereren van schema**, zodat u een JSON-schema van een voorbeeld-nettolading genereren kunt.</span><span class="sxs-lookup"><span data-stu-id="8b15c-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="8b15c-122">Parseren van JSON-actie</span><span class="sxs-lookup"><span data-stu-id="8b15c-122">'Parse JSON' action</span></span>

<span data-ttu-id="8b15c-123">De `Parse JSON` actie kunt u JSON-inhoud in beschrijvende tokens voor logic app consumptie parseren.</span><span class="sxs-lookup"><span data-stu-id="8b15c-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="8b15c-124">Deze actie is vergelijkbaar met de aanvraag-trigger, kunt u opgeven of een JSON-schema voor de inhoud die u wilt parseren configureren.</span><span class="sxs-lookup"><span data-stu-id="8b15c-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="8b15c-125">Dit hulpprogramma maakt in beslag neemt gegevens van Service Bus, Azure Cosmos DB enzovoort eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="8b15c-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parseren van JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="8b15c-127">text/plain</span><span class="sxs-lookup"><span data-stu-id="8b15c-127">Text/plain</span></span>

<span data-ttu-id="8b15c-128">Net als bij `application/json`, HTTP-berichten ontvangen met de `Content-Type` koptekst van `text/plain` in onbewerkte vorm worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8b15c-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="8b15c-129">Ook als deze berichten zijn opgenomen in de volgende acties zonder casten, deze aanvragen gaat met `Content-Type`: `text/plain` header.</span><span class="sxs-lookup"><span data-stu-id="8b15c-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="8b15c-130">Bijvoorbeeld, als u werkt met een plat bestand, mogelijk, krijgt u dit HTTP inhoud als `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="8b15c-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="8b15c-131">Als u in de volgende actie als de hoofdtekst van een andere aanvraag de aanvraag verzendt (`@body('flatfile')`), de aanvraag heeft een `text/plain` header Content-Type.</span><span class="sxs-lookup"><span data-stu-id="8b15c-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="8b15c-132">Als u met gegevens die als tekst zonder opmaak, maar niet hebben een koptekst opgegeven werkt, kunt u handmatig de gegevens voor het gebruik van tekst geconverteerd de `@string()` functioneren, bijvoorbeeld: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="8b15c-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="8b15c-133">Application/xml en toepassing/octet-stream en converter functies</span><span class="sxs-lookup"><span data-stu-id="8b15c-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="8b15c-134">De Engine voor Logic Apps behoudt altijd de `Content-Type` die op de HTTP-aanvraag of antwoord is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8b15c-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="8b15c-135">Als de engine ontvangt inhoud met de `Content-Type` van `application/octet-stream`, en dat de inhoud van een verdere actie zonder casten, de uitgaande aanvraag heeft opneemt `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="8b15c-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="8b15c-136">Op deze manier de engine kan worden gegarandeerd dat geen gegevens verloren gaan tijdens het verplaatsen van via de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="8b15c-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="8b15c-137">De actiestatus van de (invoer en uitvoer) wordt echter opgeslagen in een JSON-object als de status van de door de workflow wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="8b15c-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="8b15c-138">Dus om bepaalde gegevenstypen behouden, de engine de inhoud heeft geconverteerd naar een binaire base64-gecodeerde tekenreeks met de juiste metagegevens bestandsservergegevens beide `$content` en `$content-type`, die automatisch worden geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="8b15c-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="8b15c-139">`@json()`-gegevens naar cast`application/json`</span><span class="sxs-lookup"><span data-stu-id="8b15c-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="8b15c-140">`@xml()`-gegevens naar cast`application/xml`</span><span class="sxs-lookup"><span data-stu-id="8b15c-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="8b15c-141">`@binary()`-gegevens naar cast`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="8b15c-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="8b15c-142">`@string()`-gegevens naar cast`text/plain`</span><span class="sxs-lookup"><span data-stu-id="8b15c-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="8b15c-143">`@base64()`-inhoud converteert naar een base64-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8b15c-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="8b15c-144">`@base64toString()`-een base64-gecodeerde tekenreeks converteren naar`text/plain`</span><span class="sxs-lookup"><span data-stu-id="8b15c-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="8b15c-145">`@base64toBinary()`-een base64-gecodeerde tekenreeks converteren naar`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="8b15c-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="8b15c-146">`@encodeDataUri()`-een tekenreeks als een bytematrix dataUri codeert</span><span class="sxs-lookup"><span data-stu-id="8b15c-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="8b15c-147">`@decodeDataUri()`-een dataUri decodeert naar een bytematrix</span><span class="sxs-lookup"><span data-stu-id="8b15c-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="8b15c-148">Bijvoorbeeld, als u een HTTP-aanvraag met ontvangen `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="8b15c-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="8b15c-149">U kunt cast-conversie en later gebruiken met ongeveer `@xml(triggerBody())`, of in een functie als `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="8b15c-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="8b15c-150">Andere typen inhoud</span><span class="sxs-lookup"><span data-stu-id="8b15c-150">Other content types</span></span>

<span data-ttu-id="8b15c-151">Andere typen inhoud worden ondersteund en werken met logic apps, maar mogelijk handmatig bij het ophalen van de berichttekst door het decoderen van de `$content`.</span><span class="sxs-lookup"><span data-stu-id="8b15c-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="8b15c-152">Stel bijvoorbeeld dat u activeert een `application/x-www-url-formencoded` aanvragen waar `$content` is de nettolading gecodeerd als een base64-tekenreeks om alle gegevens te behouden:</span><span class="sxs-lookup"><span data-stu-id="8b15c-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="8b15c-153">Omdat de aanvraag niet tekst zonder opmaak of JSON, wordt de aanvraag opgeslagen in de actie als volgt:</span><span class="sxs-lookup"><span data-stu-id="8b15c-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Op dit moment is er een systeemeigen functie voor formuliergegevens niet, zodat u deze gegevens nog steeds kan gebruiken in een werkstroom door handmatig de toegang tot de gegevens met een functie, zoals `@string(body('formdataAction'))`. Als u de uitgaande aanvraag ook de `application/x-www-url-formencoded` inhoudstype-koptekst, zou u de aanvraag aan de hoofdtekst actie zonder eventuele casten zoals `@body('formdataAction')`. Maar deze methode werkt alleen als de instantie is de enige parameter in de `body` invoer. <span data-ttu-id="8b15c-157">Als u probeert te gebruiken `@body('formdataAction')` in een `application/json` vragen, u een runtime-fout niet ophalen omdat de gecodeerde hoofdcode wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="8b15c-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

