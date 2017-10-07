---
title: UI-definitie functies maken voor aaaAzure beheerde toepassingen | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse tijdens het construeren van UI-definities voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a>CreateUiDefinition functies
Deze sectie bevat Hallo handtekeningen voor alle ondersteunde functies van een CreateUiDefinition.

toouse een functie rond Hallo declaratie vierkante haken. Bijvoorbeeld:

```json
"[function()]"
```

Tekenreeksen en andere functies kunnen worden verwezen als parameters voor een functie, maar tekenreeksen moeten tussen enkele aanhalingstekens worden geplaatst. Bijvoorbeeld:

```json
"[fn1(fn2(), 'foobar')]"
```

Indien van toepassing, kunt u de eigenschappen van het Hallo-uitvoer van een functie met behulp van Hallo bewerkingsteken raadplegen. Bijvoorbeeld:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Functies die verwijzen naar
Deze functies kunnen worden gebruikt tooreference uitvoer van Hallo eigenschappen of context van een CreateUiDefinition.

### <a name="basics"></a>basisbeginselen
Hallo uitvoerwaarden van een element dat is gedefinieerd in Hallo basisbeginselen stap retourneert.

Hallo volgende voorbeeld wordt de uitvoer Hallo van Hallo-element met de naam `foo` in Hallo basisbeginselen stap:

```json
"[basics('foo')]"
```

### <a name="steps"></a>Stappen
Hallo uitvoerwaarden van een element dat is gedefinieerd in de opgegeven stap Hallo retourneert. tooget hello uitvoerwaarden van elementen in Hallo basisbeginselen stap gebruiken `basics()` in plaats daarvan.

Hallo volgende voorbeeld wordt de uitvoer Hallo van Hallo-element met de naam `bar` in Hallo stap met de naam `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Retourneert Hallo locatie in Hallo basisbeginselen stap of de huidige context Hallo geselecteerd.

Hallo volgende voorbeeld kan retourneren `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Tekenreeks-functies
Deze functies kunnen alleen worden gebruikt met een JSON-tekenreeks.

### <a name="concat"></a>concat
Een of meer reeksen aaneengeschakeld.

Bijvoorbeeld, als Hallo uitvoer de waarde van `element1` als `"bar"`, en vervolgens in dit voorbeeld Hallo tekenreeks retourneert `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>de subtekenreeks
Retourneert de subtekenreeks Hallo Hallo opgegeven tekenreeks. Hallo subtekenreeks wordt gestart op de opgegeven index Hallo en heeft Hallo opgegeven lengte.

Hallo volgende voorbeeld retourneert `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>vervangen
Retourneert een tekenreeks in welke alle instanties van Hallo tekenreeks in de huidige tekenreeks Hallo opgegeven worden vervangen door een andere tekenreeks.

Hallo volgende voorbeeld retourneert `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
Genereert een globally unique identifier (GUID)-tekenreeks.

Hallo volgende voorbeeld kan retourneren `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Retourneert een tekenreeks die is omgezet toolowercase.

Hallo volgende voorbeeld retourneert `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Retourneert een tekenreeks die is omgezet toouppercase.

Hallo volgende voorbeeld retourneert `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Functies van de verzameling
Deze functies kunnen worden gebruikt met verzamelingen, zoals JSON tekenreeksen, matrices en objecten.

### <a name="contains"></a>Bevat
Retourneert `true` als een tekenreeks bevat Hallo opgegeven subtekenreeks, bevat een matrix Hallo opgegeven waarde of een object opgegeven Hallo-sleutel bevat.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>lengte
Retourneert het aantal tekens Hallo in een tekenreeks, Hallo aantal waarden in een matrix of Hallo aantal sleutels in een object.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hallo volgende voorbeeld retourneert `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>leeg
Retourneert `true` als Hallo tekenreekswaarde, een matrix of object null of leeg is.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hallo volgende voorbeeld retourneert `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Voorbeeld 4: null zijn en niet-gedefinieerde
Stel `element1` is `null` of niet-gedefinieerde. Hallo volgende voorbeeld retourneert `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>eerste
Retourneert Hallo eerste teken van Hallo opgegeven tekenreeks; eerste waarde van de opgegeven matrix Hallo; of de eerste sleutel en waarde van het opgegeven object Hallo Hallo.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hallo volgende voorbeeld retourneert `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>laatste
Retourneert Hallo laatste teken van Hallo opgegeven verbindingsreeks, Hallo laatste waarde van de opgegeven matrix hello, of laatste sleutel en waarde van het opgegeven object Hallo Hallo.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hallo volgende voorbeeld retourneert `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>duren
Retourneert een opgegeven aantal aaneengesloten tekens vanaf het begin van Hallo tekenreeks hello, een opgegeven aantal opeenvolgende waarden vanaf het begin van de matrix Hallo hello of een opgegeven aantal aaneengesloten sleutels en waarden van Hallo Hallo-object is gestart.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hallo volgende voorbeeld retourneert `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>Overslaan
Een opgegeven aantal elementen in een verzameling omzeilt en retourneert vervolgens Hallo resterende elementen.

#### <a name="example-1-string"></a>Voorbeeld 1: tekenreeks
Hallo volgende voorbeeld retourneert `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Voorbeeld 2: matrix
Stel `element1` retourneert `[1, 2, 3]`. Hallo volgende voorbeeld retourneert `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Voorbeeld 3: object
Stel `element1` geretourneerd:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hallo volgende voorbeeld retourneert `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Logische functies
Deze functies kunnen worden gebruikt in voorwaardelijke. Sommige functies mogelijk niet alle JSON-gegevenstypen ondersteund.

### <a name="equals"></a>is gelijk aan
Retourneert `true` als beide parameters Hallo hetzelfde type en de waarde hebben. Deze functie ondersteunt alle JSON-gegevenstypen.

Hallo volgende voorbeeld retourneert `true`:

```json
"[equals(0, 0)]"
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[equals('foo', 'foo')]"
```

Hallo volgende voorbeeld retourneert `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>minder
Retourneert `true` als eerste parameter Hallo strikt kleiner is dan de tweede parameter Hallo. Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.

Hallo volgende voorbeeld retourneert `true`:

```json
"[less(1, 2)]"
```

Hallo volgende voorbeeld retourneert `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Retourneert `true` als eerste parameter Hallo kleiner dan of gelijk is toohello tweede parameter. Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.

Hallo volgende voorbeeld retourneert `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>groter
Retourneert `true` als eerste parameter Hallo strikt groter is dan de tweede parameter Hallo. Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.

Hallo volgende voorbeeld retourneert `false`:

```json
"[greater(1, 2)]"
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Retourneert `true` als eerste parameter Hallo groter dan of gelijk toohello tweede parameter is. Deze functie biedt ondersteuning voor parameters alleen van het nummer van het type en de tekenreeks.

Hallo volgende voorbeeld retourneert `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>en
Retourneert `true` als alle Hallo parameters te evalueren`true`. Deze functie biedt ondersteuning voor twee of meer parameters van het type Booleaans alleen.

Hallo volgende voorbeeld retourneert `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hallo volgende voorbeeld retourneert `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>of
Retourneert `true` als ten minste één Hallo parameters te evalueert`true`. Deze functie biedt ondersteuning voor twee of meer parameters van het type Booleaans alleen.

Hallo volgende voorbeeld retourneert `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>niet
Retourneert `true` als parameter Hallo te evalueert`false`. Deze functie biedt ondersteuning voor parameters van het type Booleaans alleen.

Hallo volgende voorbeeld retourneert `true`:

```json
"[not(false)]"
```

Hallo volgende voorbeeld retourneert `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>Coalesce
Retourneert Hallo de waarde van de eerste niet-null-parameter Hallo. Deze functie ondersteunt alle JSON-gegevenstypen.

Stel `element1` en `element2` zijn niet gedefinieerd. Hallo volgende voorbeeld retourneert `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Van conversiefuncties
Deze functies kunnen worden gebruikt tooconvert waarden tussen JSON-gegevenstypen en coderingen.

### <a name="int"></a>int
Converteert Hallo parameter tooan geheel getal. Deze functie biedt ondersteuning voor parameters van het nummer van het type en de tekenreeks.

Hallo volgende voorbeeld retourneert `1`:

```json
"[int('1')]"
```

Hallo volgende voorbeeld retourneert `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>Float
Converteert Hallo parameter tooa met drijvende komma. Deze functie biedt ondersteuning voor parameters van het nummer van het type en de tekenreeks.

Hallo volgende voorbeeld retourneert `1.0`:

```json
"[float('1.0')]"
```

Hallo volgende voorbeeld retourneert `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>Tekenreeks
Converteert Hallo parameter tooa. Deze functie biedt ondersteuning voor parameters van alle JSON-gegevenstypen.

Hallo volgende voorbeeld retourneert `"1"`:

```json
"[string(1)]"
```

Hallo volgende voorbeeld retourneert `"2.9"`:

```json
"[string(2.9)]"
```

Hallo volgende voorbeeld retourneert `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Hallo volgende voorbeeld retourneert `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>BOOL
Converteert Hallo parameter tooa Booleaanse waarde. Deze functie biedt ondersteuning voor parameters van het nummer van het type tekenreeks en Booleaanse waarde. Vergelijkbare tooBooleans in JavaScript, een willekeurige waarde behalve `0` of `'false'` retourneert `true`.

Hallo volgende voorbeeld retourneert `true`:

```json
"[bool(1)]"
```

Hallo volgende voorbeeld retourneert `false`:

```json
"[bool(0)]"
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[bool(true)]"
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parseren
Converteert Hallo tooa parametereigen type. Met andere woorden, deze functie is Hallo inverse van `string()`. Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.

Hallo volgende voorbeeld retourneert `1`:

```json
"[parse('1')]"
```

Hallo volgende voorbeeld retourneert `true`:

```json
"[parse('true')]"
```

Hallo volgende voorbeeld retourneert `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Hallo volgende voorbeeld retourneert `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Codeert Hallo parameter tooa base-64 gecodeerde tekenreeks. Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.

Hallo volgende voorbeeld retourneert `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Decodeert Hallo-parameter van een Base64-gecodeerde tekenreeks. Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.

Hallo volgende voorbeeld retourneert `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Codeert Hallo parameter tooa URL gecodeerde tekenreeks. Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.

Hallo volgende voorbeeld retourneert `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Decodeert Hallo-parameter van een URL-gecodeerde tekenreeks. Deze functie biedt ondersteuning voor parameters die alleen van het type tekenreeks.

Hallo volgende voorbeeld retourneert `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Rekenkundige functies
### <a name="add"></a>toevoegen
Telt twee getallen en retourneert Hallo resultaat.

Hallo volgende voorbeeld retourneert `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>Sub
Tweede nummer van het eerste nummer Hallo Hallo aftrekken en retourneert Hallo resultaat.

Hallo volgende voorbeeld retourneert `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Vermenigvuldigt twee getallen en retourneert Hallo resultaat.

Hallo volgende voorbeeld retourneert `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Deelt Hallo eerste getal door het tweede getal Hallo en Hallo resultaat retourneert. Hallo-resultaat is altijd een geheel getal.

Hallo volgende voorbeeld retourneert `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>Mod
Eerste getal door het tweede getal Hallo Hallo deelt, en retourneert Hallo rest.

Hallo volgende voorbeeld retourneert `0`:

```json
"[mod(6, 3)]"
```

Hallo volgende voorbeeld retourneert `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>min.
Retourneert Hallo klein Hallo twee getallen.

Hallo volgende voorbeeld retourneert `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>Maximum aantal
Retourneert hello grotere van Hallo twee getallen.

Hallo volgende voorbeeld retourneert `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>bereik
Genereert een reeks integraal getallen in Hallo opgegeven bereik.

Hallo volgende voorbeeld retourneert `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Retourneert een willekeurig geheel getal in Hallo opgegeven bereik. Deze functie geen cryptografisch beveiligde willekeurige getallen gegenereerd.

Hallo volgende voorbeeld kan retourneren `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>Floor
Retourneert de grootste integer Hallo kleiner dan of gelijk toohello opgegeven getal.

Hallo volgende voorbeeld retourneert `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Retourneert Hallo grootste gehele getal groter dan of gelijk zijn toohello opgegeven getal.

Hallo volgende voorbeeld retourneert `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Datumfuncties
### <a name="utcnow"></a>utcNow
Retourneert een tekenreeks in de ISO 8601-notatie Hallo huidige datum en tijd op de lokale computer Hallo.

Hallo volgende voorbeeld kan retourneren `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
Voegt een geheel getal van seconden toohello opgegeven timestamp.

Hallo volgende voorbeeld retourneert `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Voegt een geheel getal van minuten toohello opgegeven timestamp.

Hallo volgende voorbeeld retourneert `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Voegt een geheel getal van uren toohello opgegeven timestamp.

Hallo volgende voorbeeld retourneert `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tooAzure Resource Manager, [overzicht van Azure Resource Manager](resource-group-overview.md).

