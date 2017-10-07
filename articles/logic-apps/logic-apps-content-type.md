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
# <a name="handle-content-types-in-logic-apps"></a>De inhoudstypen die ingang in logic apps

Veel verschillende typen inhoud kunnen door een logische app, met inbegrip van de JSON, XML, platte bestanden en binaire gegevens stromen. Tijdens het Hallo Logic Apps-Engine ondersteunt alle typen inhoud, worden sommige systeemeigen begrepen door Hallo Logic Apps-Engine. Anderen mogelijk casten of conversies indien nodig. Dit artikel wordt beschreven hoe Hallo-engine verwerkt voor verschillende typen inhoud en hoe toocorrectly verwerken voor deze typen indien nodig.

## <a name="content-type-header"></a>Content-Type-Header

toostart in principe bekijken we Hallo twee `Content-Types` waarvoor geen conversie of casten die u in een logische app gebruiken kunt: `application/json` en `text/plain`.

## <a name="applicationjson"></a>Application/JSON

Hallo werkstroom-engine is afhankelijk van Hallo `Content-Type` kop van HTTP-aanroepen toodetermine Hallo juiste verwerking. Een aanvraag met Hallo inhoudstype `application/json` wordt opgeslagen en verwerkt als een JSON-Object. JSON-inhoud kan ook standaard zonder eventuele casten worden geparseerd. 

Bijvoorbeeld, u een aanvraag die Hallo content-type-header is kan parseren `application/json ` in een werkstroom met behulp van een expressie zoals `@body('myAction')['foo'][0]` tooget Hallo waarde `bar` in dit geval:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Er is geen aanvullende casten nodig. Als u met gegevens die JSON is, maar niet een header die is opgegeven werkt, u kunt handmatig gecast tooJSON Hallo met `@json()` functioneren, bijvoorbeeld: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Schema- en schema-generator

Hallo aanvraag trigger kunt u tooenter een JSON-schema voor Hallo nettolading u tooreceive verwacht. Dit schema kunt Hallo designer tokens genereren zodat u Hallo inhoud van de aanvraag Hallo kunt gebruiken. Als u een schema gereed geen hebt, selecteert u **gebruik voorbeeld nettolading toogenerate schema**, zodat u een JSON-schema van een voorbeeld-nettolading genereren kunt.

![Schema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Parseren van JSON-actie

Hallo `Parse JSON` actie kunt u JSON-inhoud in beschrijvende tokens voor logic app consumptie parseren. Vergelijkbare toohello aanvraag worden geactiveerd, met deze actie kunt u invoeren of een JSON-schema voor Hallo inhoud dat u tooparse wilt configureren. Dit hulpprogramma maakt in beslag neemt gegevens van Service Bus, Azure Cosmos DB enzovoort eenvoudiger.

![Parseren van JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>text/plain

Vergelijkbare te`application/json`, HTTP-berichten ontvangen met Hallo `Content-Type` koptekst van `text/plain` in onbewerkte vorm worden opgeslagen. Ook als deze berichten zijn opgenomen in de volgende acties zonder casten, deze aanvragen gaat met `Content-Type`: `text/plain` header. Bijvoorbeeld, als u werkt met een plat bestand, mogelijk, krijgt u dit HTTP inhoud als `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

Als u in de volgende actie hello, als Hallo hoofdcode van een andere aanvraag Hallo aanvraag verzendt (`@body('flatfile')`), Hallo verzoek moet een `text/plain` header Content-Type. Als u met gegevens die als tekst zonder opmaak, maar niet hebben een koptekst opgegeven werkt, kunt u handmatig Hallo gegevens tootext met Hallo casten `@string()` functioneren, bijvoorbeeld: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml en toepassing/octet-stream en converter functies

Hallo Logic Apps-Engine behoudt altijd Hallo `Content-Type` die op Hallo HTTP-aanvraag of antwoord is ontvangen. Als het Hallo-engine ontvangt inhoud Hello `Content-Type` van `application/octet-stream`, en dat de inhoud van een verdere actie zonder casten, Hallo uitgaande aanvraag heeft opneemt `Content-Type`: `application/octet-stream`. Op deze manier kan Hallo engine garanderen geen gegevens verloren gaan tijdens het verplaatsen van via Hallo workflow. Hallo Actiestatus (invoer en uitvoer) wordt echter opgeslagen in een JSON-object als Hallo status doorloopt Hallo werkstroom. Dus toopreserve sommige gegevenstypen, Hallo engine converteert inhoud tooa binary base64-gecodeerde tekenreeks met de juiste metagegevens bestandsservergegevens beide Hallo `$content` en `$content-type`, die automatisch worden geconverteerd. 

* `@json()`-gegevens te cast`application/json`
* `@xml()`-gegevens te cast`application/xml`
* `@binary()`-gegevens te cast`application/octet-stream`
* `@string()`-gegevens te cast`text/plain`
* `@base64()`-Zet inhoud tooa base64-tekenreeks
* `@base64toString()`-een base64-gecodeerde tekenreeks te worden geconverteerd`text/plain`
* `@base64toBinary()`-een base64-gecodeerde tekenreeks te worden geconverteerd`application/octet-stream`
* `@encodeDataUri()`-een tekenreeks als een bytematrix dataUri codeert
* `@decodeDataUri()`-een dataUri decodeert naar een bytematrix

Bijvoorbeeld, als u een HTTP-aanvraag met ontvangen `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

U kunt cast-conversie en later gebruiken met ongeveer `@xml(triggerBody())`, of in een functie als `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Andere typen inhoud

Andere typen inhoud worden ondersteund en werken met logic apps, maar mogelijk handmatig ophalen Hallo berichttekst door het decoderen van Hallo `$content`. Stel bijvoorbeeld dat u activeert een `application/x-www-url-formencoded` aanvragen waar `$content` is Hallo nettolading gecodeerd als een base64-tekenreeks toopreserve alle gegevens:

```
CustomerName=Frank&Address=123+Avenue
```

Omdat het Hallo-aanvraag is niet als tekst zonder opmaak of JSON, is Hallo-aanvraag opgeslagen in Hallo actie als volgt:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Op dit moment is er een systeemeigen functie voor formuliergegevens niet, zodat u deze gegevens nog steeds kan gebruiken in een werkstroom met het openen van handmatig Hallo-gegevens met een functie, zoals `@string(body('formdataAction'))`. Indien u wenste de uitgaande aanvraag tooalso hebben Hallo Hallo `application/x-www-url-formencoded` inhoudstype-koptekst, zou u Hallo toohello actie aanvraagtekst zonder eventuele casten zoals `@body('formdataAction')`. Maar deze methode werkt alleen als hoofdtekst Hallo Hallo enige parameter in Hallo `body` invoer. Als u toouse probeert `@body('formdataAction')` in een `application/json` vragen, u een runtime-fout niet ophalen omdat Hallo gecodeerde tekst verzonden.

