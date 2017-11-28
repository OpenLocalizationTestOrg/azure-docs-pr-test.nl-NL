---
title: aaaHandle inhoudstypen - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="41a02-103">De inhoudstypen die ingang in logic apps</span><span class="sxs-lookup"><span data-stu-id="41a02-103">Handle content types in logic apps</span></span>

<span data-ttu-id="41a02-104">Veel verschillende typen inhoud kunnen door een logische app, met inbegrip van de JSON, XML, platte bestanden en binaire gegevens stromen.</span><span class="sxs-lookup"><span data-stu-id="41a02-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="41a02-105">Tijdens het Hallo Logic Apps-Engine ondersteunt alle typen inhoud, worden sommige systeemeigen begrepen door Hallo Logic Apps-Engine.</span><span class="sxs-lookup"><span data-stu-id="41a02-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="41a02-106">Anderen mogelijk casten of conversies indien nodig.</span><span class="sxs-lookup"><span data-stu-id="41a02-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="41a02-107">Dit artikel wordt beschreven hoe Hallo-engine verwerkt voor verschillende typen inhoud en hoe toocorrectly verwerken voor deze typen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="41a02-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="41a02-108">Content-Type-Header</span><span class="sxs-lookup"><span data-stu-id="41a02-108">Content-Type Header</span></span>

<span data-ttu-id="41a02-109">toostart in principe bekijken we Hallo twee `Content-Types` waarvoor geen conversie of casten die u in een logische app gebruiken kunt: `application/json` en `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="41a02-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="41a02-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="41a02-110">Application/JSON</span></span>

<span data-ttu-id="41a02-111">Hallo werkstroom-engine is afhankelijk van Hallo `Content-Type` kop van HTTP-aanroepen toodetermine Hallo juiste verwerking.</span><span class="sxs-lookup"><span data-stu-id="41a02-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="41a02-112">Een aanvraag met Hallo inhoudstype `application/json` wordt opgeslagen en verwerkt als een JSON-Object.</span><span class="sxs-lookup"><span data-stu-id="41a02-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="41a02-113">JSON-inhoud kan ook standaard zonder eventuele casten worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="41a02-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="41a02-114">Bijvoorbeeld, u een aanvraag die Hallo content-type-header is kan parseren `application/json ` in een werkstroom met behulp van een expressie zoals `@body('myAction')['foo'][0]` tooget Hallo waarde `bar` in dit geval:</span><span class="sxs-lookup"><span data-stu-id="41a02-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="41a02-115">Er is geen aanvullende casten nodig.</span><span class="sxs-lookup"><span data-stu-id="41a02-115">No additional casting is needed.</span></span> <span data-ttu-id="41a02-116">Als u met gegevens die JSON is, maar niet een header die is opgegeven werkt, u kunt handmatig gecast tooJSON Hallo met `@json()` functioneren, bijvoorbeeld: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="41a02-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="41a02-117">Schema- en schema-generator</span><span class="sxs-lookup"><span data-stu-id="41a02-117">Schema and schema generator</span></span>

<span data-ttu-id="41a02-118">Hallo aanvraag trigger kunt u tooenter een JSON-schema voor Hallo nettolading u tooreceive verwacht.</span><span class="sxs-lookup"><span data-stu-id="41a02-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="41a02-119">Dit schema kunt Hallo designer tokens genereren zodat u Hallo inhoud van de aanvraag Hallo kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="41a02-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="41a02-120">Als u een schema gereed geen hebt, selecteert u **gebruik voorbeeld nettolading toogenerate schema**, zodat u een JSON-schema van een voorbeeld-nettolading genereren kunt.</span><span class="sxs-lookup"><span data-stu-id="41a02-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="41a02-122">Parseren van JSON-actie</span><span class="sxs-lookup"><span data-stu-id="41a02-122">'Parse JSON' action</span></span>

<span data-ttu-id="41a02-123">Hallo `Parse JSON` actie kunt u JSON-inhoud in beschrijvende tokens voor logic app consumptie parseren.</span><span class="sxs-lookup"><span data-stu-id="41a02-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="41a02-124">Vergelijkbare toohello aanvraag worden geactiveerd, met deze actie kunt u invoeren of een JSON-schema voor Hallo inhoud dat u tooparse wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="41a02-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="41a02-125">Dit hulpprogramma maakt in beslag neemt gegevens van Service Bus, Azure Cosmos DB enzovoort eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="41a02-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parseren van JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="41a02-127">text/plain</span><span class="sxs-lookup"><span data-stu-id="41a02-127">Text/plain</span></span>

<span data-ttu-id="41a02-128">Vergelijkbare te`application/json`, HTTP-berichten ontvangen met Hallo `Content-Type` koptekst van `text/plain` in onbewerkte vorm worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="41a02-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="41a02-129">Ook als deze berichten zijn opgenomen in de volgende acties zonder casten, deze aanvragen gaat met `Content-Type`: `text/plain` header.</span><span class="sxs-lookup"><span data-stu-id="41a02-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="41a02-130">Bijvoorbeeld, als u werkt met een plat bestand, mogelijk, krijgt u dit HTTP inhoud als `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="41a02-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="41a02-131">Als u in de volgende actie hello, als Hallo hoofdcode van een andere aanvraag Hallo aanvraag verzendt (`@body('flatfile')`), Hallo verzoek moet een `text/plain` header Content-Type.</span><span class="sxs-lookup"><span data-stu-id="41a02-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="41a02-132">Als u met gegevens die als tekst zonder opmaak, maar niet hebben een koptekst opgegeven werkt, kunt u handmatig Hallo gegevens tootext met Hallo casten `@string()` functioneren, bijvoorbeeld: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="41a02-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="41a02-133">Application/xml en toepassing/octet-stream en converter functies</span><span class="sxs-lookup"><span data-stu-id="41a02-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="41a02-134">Hallo Logic Apps-Engine behoudt altijd Hallo `Content-Type` die op Hallo HTTP-aanvraag of antwoord is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="41a02-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="41a02-135">Als het Hallo-engine ontvangt inhoud Hello `Content-Type` van `application/octet-stream`, en dat de inhoud van een verdere actie zonder casten, Hallo uitgaande aanvraag heeft opneemt `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="41a02-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="41a02-136">Op deze manier kan Hallo engine garanderen geen gegevens verloren gaan tijdens het verplaatsen van via Hallo workflow.</span><span class="sxs-lookup"><span data-stu-id="41a02-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="41a02-137">Hallo Actiestatus (invoer en uitvoer) wordt echter opgeslagen in een JSON-object als Hallo status doorloopt Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="41a02-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="41a02-138">Dus toopreserve sommige gegevenstypen, Hallo engine converteert inhoud tooa binary base64-gecodeerde tekenreeks met de juiste metagegevens bestandsservergegevens beide Hallo `$content` en `$content-type`, die automatisch worden geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="41a02-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="41a02-139">`@json()`-gegevens te cast`application/json`</span><span class="sxs-lookup"><span data-stu-id="41a02-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="41a02-140">`@xml()`-gegevens te cast`application/xml`</span><span class="sxs-lookup"><span data-stu-id="41a02-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="41a02-141">`@binary()`-gegevens te cast`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="41a02-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="41a02-142">`@string()`-gegevens te cast`text/plain`</span><span class="sxs-lookup"><span data-stu-id="41a02-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="41a02-143">`@base64()`-Zet inhoud tooa base64-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="41a02-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="41a02-144">`@base64toString()`-een base64-gecodeerde tekenreeks te worden geconverteerd`text/plain`</span><span class="sxs-lookup"><span data-stu-id="41a02-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="41a02-145">`@base64toBinary()`-een base64-gecodeerde tekenreeks te worden geconverteerd`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="41a02-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="41a02-146">`@encodeDataUri()`-een tekenreeks als een bytematrix dataUri codeert</span><span class="sxs-lookup"><span data-stu-id="41a02-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="41a02-147">`@decodeDataUri()`-een dataUri decodeert naar een bytematrix</span><span class="sxs-lookup"><span data-stu-id="41a02-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="41a02-148">Bijvoorbeeld, als u een HTTP-aanvraag met ontvangen `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="41a02-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="41a02-149">U kunt cast-conversie en later gebruiken met ongeveer `@xml(triggerBody())`, of in een functie als `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="41a02-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="41a02-150">Andere typen inhoud</span><span class="sxs-lookup"><span data-stu-id="41a02-150">Other content types</span></span>

<span data-ttu-id="41a02-151">Andere typen inhoud worden ondersteund en werken met logic apps, maar mogelijk handmatig ophalen Hallo berichttekst door het decoderen van Hallo `$content`.</span><span class="sxs-lookup"><span data-stu-id="41a02-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="41a02-152">Stel bijvoorbeeld dat u activeert een `application/x-www-url-formencoded` aanvragen waar `$content` is Hallo nettolading gecodeerd als een base64-tekenreeks toopreserve alle gegevens:</span><span class="sxs-lookup"><span data-stu-id="41a02-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="41a02-153">Omdat het Hallo-aanvraag is niet als tekst zonder opmaak of JSON, is Hallo-aanvraag opgeslagen in Hallo actie als volgt:</span><span class="sxs-lookup"><span data-stu-id="41a02-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Op dit moment is er een systeemeigen functie voor formuliergegevens niet, zodat u deze gegevens nog steeds kan gebruiken in een werkstroom met het openen van handmatig Hallo-gegevens met een functie, zoals `@string(body('formdataAction'))`. Indien u wenste de uitgaande aanvraag tooalso hebben Hallo Hallo `application/x-www-url-formencoded` inhoudstype-koptekst, zou u Hallo toohello actie aanvraagtekst zonder eventuele casten zoals `@body('formdataAction')`. Maar deze methode werkt alleen als hoofdtekst Hallo Hallo enige parameter in Hallo `body` invoer. <span data-ttu-id="41a02-157">Als u toouse probeert `@body('formdataAction')` in een `application/json` vragen, u een runtime-fout niet ophalen omdat Hallo gecodeerde tekst verzonden.</span><span class="sxs-lookup"><span data-stu-id="41a02-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

