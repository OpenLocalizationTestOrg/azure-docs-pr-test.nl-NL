---
title: aaaWorkflow Definition Language schema - Azure Logic Apps | Microsoft Docs
description: "Werkstromen op basis van Hallo werkstroom definitie schema voor Azure Logic Apps definiëren"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Werkstroom Definition Language-schema voor Azure Logic Apps

De werkstroomdefinitie van een bevat Hallo werkelijke logica die wordt uitgevoerd als onderdeel van uw logische app. Deze definitie bevat een of meer triggers die Hallo logische app start en een of meer acties voor Hallo logic app tootake.  
  
## <a name="basic-workflow-definition-structure"></a>Basiswerkstroom definitie structuur

Hier volgt Hallo basisstructuur van een werkstroomdefinitie:  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Hallo [werkstroom Management REST API](https://docs.microsoft.com/rest/api/logic/workflows) documentatie bevat informatie over het toocreate en logic app werkstromen beheren.
  
|Elementnaam|Vereist|Beschrijving|  
|------------------|--------------|-----------------|  
|$schema|Nee|Geeft de locatie Hallo voor Hallo JSON-schema-bestand dat Hallo-versie van Hallo definitietaal beschrijft. Deze locatie is vereist wanneer u verwijst naar een extern-definitie. Dit document is Hallo locatie: <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|Nee|Hiermee geeft u versie Hallo-definitie. Wanneer u een werkstroom met Hallo definitie implementeert, kunt u deze waarde toomake ervoor dat de juiste definitie Hallo wordt gebruikt.|  
|parameters|Nee|Hiermee geeft u parameters tooinput gegevens in de definitie van Hallo gebruikt. Een maximum van 50 parameters kan worden gedefinieerd.|  
|Triggers|Nee|Hiermee geeft u informatie voor Hallo-triggers die Hallo werkstroom initiëren. Er kan maximaal 10 triggers worden gedefinieerd.|  
|acties|Nee|Geeft de acties die worden uitgevoerd als het Hallo-stroom wordt uitgevoerd. Maximaal 250 acties kan worden gedefinieerd.|  
|uitvoer|Nee|Hiermee geeft u informatie over Hallo geïmplementeerd resource. Maximaal 10 uitvoer kan worden gedefinieerd.|  
  
## <a name="parameters"></a>Parameters

Deze sectie geeft alle Hallo-parameters die worden gebruikt in de workflowdefinitie Hallo tijdens de implementatie. Alle parameters moeten worden gedeclareerd in deze sectie voordat ze kunnen worden gebruikt in andere gedeelten van Hallo definitie.  
  
Hallo toont volgende voorbeeld Hallo-structuur van de parameterdefinitie van een:  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Elementnaam|Vereist|Beschrijving|  
|------------------|--------------|-----------------|  
|type|Ja|**Type**: tekenreeks <p> **Declaratie**:`"parameters": {"parameter1": {"type": "string"}` <p> **Specificatie**:`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Type**: securestring <p> **Declaratie**:`"parameters": {"parameter1": {"type": "securestring"}}` <p> **Specificatie**:`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Type**: int <p> **Declaratie**:`"parameters": {"parameter1": {"type": "int"}}` <p> **Specificatie**:`"parameters": {"parameter1": {"value" : 5}}` <p> **Type**: bool <p> **Declaratie**:`"parameters": {"parameter1": {"type": "bool"}}` <p> **Specificatie**:`"parameters": {"parameter1": { "value": true }}` <p> **Type**: matrix <p> **Declaratie**:`"parameters": {"parameter1": {"type": "array"}}` <p> **Specificatie**:`"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Type**: object <p> **Declaratie**:`"parameters": {"parameter1": {"type": "object"}}` <p> **Specificatie**:`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Type**: secureobject <p> **Declaratie**:`"parameters": {"parameter1": {"type": "object"}}` <p> **Specificatie**:`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Opmerking:** hello `securestring` en `secureobject` typen worden niet geretourneerd `GET` bewerkingen. Alle wachtwoorden, sleutels en geheimen moeten gebruiken voor dit type.|  
|Standaardwaarde|Nee|Geeft de standaardwaarde Hallo voor Hallo parameter wanneer er geen waarde wordt opgegeven tijdens het Hallo Hallo resource is gemaakt.|  
|allowedValues|Nee|Hiermee geeft u een matrix van toegestane waarden voor Hallo-parameter.|  
|Metagegevens|Nee|Hiermee geeft u aanvullende informatie over het Hallo-parameter, zoals een leesbare beschrijving of het moment van ontwerp gegevens die worden gebruikt door Visual Studio of andere hulpprogramma's.|  
  
Dit voorbeeld ziet hoe u een parameter in de hoofdsectie Hallo van een actie kunt gebruiken:  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 Parameters kunnen ook worden gebruikt in de uitvoer.  
  
## <a name="triggers-and-actions"></a>Triggers en acties  

Triggers en acties opgeven Hallo-aanroepen die kunnen deelnemen in een werkstroom kan worden uitgevoerd. Zie voor meer informatie over deze sectie [werkstroomacties en Triggers](logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>uitvoer  

Uitvoer geven informatie op die kan worden geretourneerd van een werkstroom uitgevoerd. Bijvoorbeeld, als er een specifieke status of een waarde wilt u tootrack voor elke uitvoering, kunt u opnemen dat gegevens in Hallo uitvoer uitgevoerd. Hallo gegevens worden weergegeven in Hallo Management REST API voor die run en in Hallo beheersgebruikersinterface voor die run in hello Azure-portal. U kunt ook deze uitvoer tooother externe systemen zoals Power BI stromen om dashboards te maken. Uitvoer zijn *niet* toorespond tooincoming aanvragen op Hallo REST-API-Service gebruikt. toorespond tooan inkomende aanvraag met Hallo `response` actietype, Hier volgt een voorbeeld:
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Elementnaam|Vereist|Beschrijving|  
|------------------|--------------|-----------------|  
|Key1|Ja|Hiermee geeft u Hallo sleutel-id voor Hallo uitvoer. Vervang **key1** met een naam die u wilt dat toouse tooidentify Hallo uitvoer.|  
|waarde|Ja|Hiermee wordt de waarde Hallo van Hallo uitvoer.|  
|type|Ja|Hiermee geeft u Hallo-type voor Hallo-waarde die is opgegeven. Mogelijke zijn waarden: <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>Expressies  

JSON-waarden in de definitie van Hallo letterlijk kunnen zijn kunnen, of ze expressies die worden geëvalueerd wanneer Hallo definitie wordt gebruikt. Bijvoorbeeld:  
  
```json
"name": "value"
```

 of  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Aantal expressies worden de waarden van de runtime-acties die niet aan begin Hallo Hallo uitvoering bestaat mogelijk. U kunt **functies** toohelp sommige van deze waarden worden opgehaald.  
  
Expressies kunnen overal voorkomen in een string-waarde van JSON en altijd resulteren in een andere JSON-waarde. Wanneer een JSON-waarde bepaald toobe een expressie is, Hallo-hoofdtekst van het Hallo-expressie wordt opgehaald door het verwijderen van Hallo at-teken (@). Als een letterlijke tekenreeks is vereist dat met begint @, dat tekenreeks moet worden voorafgegaan door@. Hallo volgende voorbeelden laten zien hoe expressies worden geëvalueerd.  
  
|JSON-waarde|Resultaat|  
|----------------|------------|  
|'parameters'|Hallo tekens 'parameters' geretourneerd.|  
|'[1] parameters'|Hallo tekens 'parameters [1]' geretourneerd.|  
|"@@"|Een tekenreeks 1 teken ' @' wordt geretourneerd.|  
|" @"|Een tekenreeks 2 teken ' @' wordt geretourneerd.|  
  
Met *interpolatie string*, expressies kunnen ook worden weergegeven in tekenreeksen waar expressies zijn samengevoegd in `@{ ... }`. Bijvoorbeeld: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

Hallo-resultaat is altijd een tekenreeks, waardoor deze functie vergelijkbare toohello `concat` functie. Stel dat u hebt gedefinieerd `myNumber` als `42` en `myString` als `sampleString`:  
  
|JSON-waarde|Resultaat|  
|----------------|------------|  
|"@parameters(myString)"|Retourneert `sampleString` als een tekenreeks.|  
|"@{parameters('myString')}"|Retourneert `sampleString` als een tekenreeks.|  
|"@parameters(myNumber)"|Retourneert `42` als een *nummer*.|  
|"@{parameters('myNumber')}"|Retourneert `42` als een *tekenreeks*.|  
|"Antwoord is: @{parameters('myNumber')}"|Retourneert de tekenreeks Hallo `Answer is: 42`.|  
|'@concat(' Antwoord is: ', string(parameters('myNumber'))) '|Retourneert Hallo tekenreeks`Answer is: 42`|  
|"Antwoord: @@ {parameters('myNumber')}"|Retourneert de tekenreeks Hallo `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>Operators  

Operators zijn Hallo tekens die u in expressies of functies gebruiken kunt. 
  
|Operator|Beschrijving|  
|--------------|-----------------|  
|.|Hallo-punt kunt u de eigenschappen van een object tooreference|  
|?|Hallo vraagteken operator kunt u verwijzen naar null eigenschappen van een object zonder een runtime-fout. Bijvoorbeeld, kunt u deze toohandle expressie null uitvoer activeren: <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|enkel aanhalingsteken Hallo is Hallo alleen manier toowrap letterlijke tekenreeks. U kunt dubbele aanhalingstekens in expressies niet gebruiken omdat deze leestekens strijdig is met de Hallo JSON aanhalingsteken die de hele expressie Hallo terugloopt.|  
|[]|Hallo vierkante haken kan gebruikte tooget een waarde uit een array met een specifieke index zijn. Bijvoorbeeld, als u hebt een actie die wordt doorgegeven `range(0,10)`in toohello `forEach` functioneren, kunt u deze functie tooget artikelen van matrices gebruiken:  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Functies  

U kunt ook functies binnen expressies aanroepen. Hallo volgende tabel toont Hallo-functies die kunnen worden gebruikt in een expressie.  
  
|expressie|Evaluatie|  
|----------------|----------------|  
|'@function('Hallo') '|Aanroepen Hallo lid van de functie van Hallo definitie van Hallo letterlijke tekenreeks Hallo als eerste parameter Hallo.|  
|'@function('Dit is Cool!') '|Roept Hallo functie lid Hallo definitie van de letterlijke tekenreeks Hallo 'is Cool!' Als de eerste parameter Hallo|  
|'@function.prop1 () '|Retourneert de waarde van eigenschap van prop1 Hallo HALLO hallo `myfunction` lid is van het Hallo-definitie.|  
|'@function('Hallo') .prop1 '|Aanroepen Hallo functie lid van de definitie van Hallo letterlijke tekenreeks 'Hallo' hello als Hallo eerste parameter en retourneert Hallo eig1-eigenschap van Hallo-object.|  
|'@function(parameters('Hello')) '|Hallo Hallo parameter geëvalueerd en wordt doorgegeven Hallo waarde toofunction|  
  
### <a name="referencing-functions"></a>Functies die verwijzen naar  

U kunt de uitvoer van deze functies tooreference van andere acties in Hallo logische app of waarden die worden doorgegeven als Hallo logische app is gemaakt. Bijvoorbeeld, u kunt verwijzen naar Hallo gegevens uit één stap toouse in een andere.  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|parameters|Retourneert een parameterwaarde die is gedefinieerd in het Hallo-definitie. <p>`parameters('password')` <p> **Parameternummer**: 1 <p> **Naam**: Parameter <p> **Beschrijving**: vereist. Hallo-naam van Hallo parameter waarvan de gewenste waarden.|  
|Actie|Hiermee kunt een tooderive expressie de waarde van andere JSON-naam en waarde-paren of Hallo-uitvoer van de huidige runtime actie Hallo. dat wordt vertegenwoordigd door propertyPath in het volgende voorbeeld Hallo Hallo-eigenschap is optioneel. Als propertyPath niet is opgegeven, is het Hallo-verwijzing toohello hele actie-object. Deze functie kan alleen worden gebruikt binnen een-totdat de voorwaarden van een actie. <p>`action().outputs.body.propertyPath`|  
|acties|Hiermee kunt een tooderive expressie de waarde van andere JSON-naam en waarde-paren of Hallo-uitvoer van Hallo runtime actie. Deze expressies declareren expliciet dat één actie afhankelijk van een andere actie is. dat wordt vertegenwoordigd door propertyPath in het volgende voorbeeld Hallo Hallo-eigenschap is optioneel. Als propertyPath niet is opgegeven, is het Hallo-verwijzing toohello hele actie-object. Kunt u beide dit element of Hallo condities element toospecify afhankelijkheden, maar u hoeft geen toouse beide voor Hallo dezelfde afhankelijke bron. <p>`actions('myAction').outputs.body.propertyPath` <p> **Parameternummer**: 1 <p> **Naam**: naam van de actie <p> **Beschrijving**: vereist. Hallo-naam van Hallo actie waarvan de gewenste waarden. <p> Beschikbare eigenschappen op Hallo actie-object zijn: <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Zie Hallo [Rest-API](http://go.microsoft.com/fwlink/p/?LinkID=850646) voor meer informatie over deze eigenschappen.|
|Trigger|Hiermee kunt een tooderive expressie de waarde van andere JSON-naam en waarde-paren of Hallo-uitvoer van Hallo runtime trigger. dat wordt vertegenwoordigd door propertyPath in het volgende voorbeeld Hallo Hallo-eigenschap is optioneel. Als propertyPath niet is opgegeven, is het Hallo-verwijzing toohello hele triggerobject. <p>`trigger().outputs.body.propertyPath` <p>Binnen een trigger invoer retourneert Hallo functie Hallo uitvoerwaarden van de vorige uitvoering Hallo. Echter, wanneer gebruikt in de voorwaarde van een trigger, Hallo `trigger` functie Hallo uitvoerwaarden van de huidige uitvoering Hallo retourneert. <p> Beschikbare eigenschappen op Hallo triggerobject zijn: <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Zie Hallo [Rest-API](http://go.microsoft.com/fwlink/p/?LinkID=850644) voor meer informatie over deze eigenschappen.|
|actionOutputs|Deze functie is de afkorting van`actions('actionName').outputs` <p> **Parameternummer**: 1 <p> **Naam**: naam van de actie <p> **Beschrijving**: vereist. Hallo-naam van Hallo actie waarvan de gewenste waarden.|  
|actionBody en hoofdtekst|Deze functies zijn steno voor`actions('actionName').outputs.body` <p> **Parameternummer**: 1 <p> **Naam**: naam van de actie <p> **Beschrijving**: vereist. Hallo-naam van Hallo actie waarvan de gewenste waarden.|  
|triggerOutputs|Deze functie is de afkorting van`trigger().outputs`|  
|triggerBody|Deze functie is de afkorting van`trigger().outputs.body`|  
|item|Wanneer gebruikt in een terugkerende actie, retourneert deze functie Hallo-item bevindt zich in de matrix Hallo voor deze herhaling van Hallo actie. Bijvoorbeeld, als u een actie die wordt uitgevoerd voor elk item een matrix van berichten hebt, kunt u deze syntaxis: <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Functies van de verzameling  

Deze functies bepalen het verloop van verzamelingen en tooArrays, tekenreeksen, en soms woordenlijsten in het algemeen van toepassing.  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|Bevat|Retourneert waar als het woordenboek bevat een lijst met sleutels, bevat een waarde of tekenreeks subtekenreeks bevat. Bijvoorbeeld: deze functie retourneert `true`: <p>`contains('abacaba','aca')` <p> **Parameternummer**: 1 <p> **Naam**: binnen de verzameling <p> **Beschrijving**: vereist. Hallo verzameling toosearch binnen. <p> **Parameternummer**: 2 <p> **Naam**: Find-object <p> **Beschrijving**: vereist. object toofind binnen Hallo Hallo **binnen verzameling**.|  
|lengte|Retourneert Hallo het aantal elementen in een matrix of tekenreeks. Bijvoorbeeld: deze functie retourneert `3`:  <p>`length('abc')` <p> **Parameternummer**: 1 <p> **Naam**: verzameling <p> **Beschrijving**: vereist. Hallo-verzameling voor tooget Hallo tekens.|  
|leeg|Retourneert waar als het object, matrix of tekenreeks leeg is. Bijvoorbeeld: deze functie retourneert `true`: <p>`empty('')` <p> **Parameternummer**: 1 <p> **Naam**: verzameling <p> **Beschrijving**: vereist. Hallo verzameling toocheck als deze leeg is.|  
|snijpunt|Retourneert een matrix of object waarvoor standaardelementen tussen matrices of objecten die zijn doorgegeven. Bijvoorbeeld: deze functie retourneert `[1, 2]`: <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>Hallo parameters op voor het Hallo-functie kunnen een set van objecten of een set van matrices (niet een combinatie van beide) zijn. Als er twee objecten Hello naam dezelfde, laatste Hallo-object met deze naam wordt weergegeven in de definitieve Hallo-object. <p> **Parameternummer**: 1...*n* <p> **Naam**: verzameling*n* <p> **Beschrijving**: vereist. Hallo verzamelingen tooevaluate. Een object moet zich in alle verzamelingen tooappear in Hallo resultaat doorgegeven.|  
|Union|Retourneert een matrix of object met alle Hallo-elementen die in de matrix of object toothis-functie doorgegeven zijn. Bijvoorbeeld: deze functie retourneert `[1, 2, 3, 10, 101]`: <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>Hallo parameters op voor het Hallo-functie kunnen een set van objecten of een set van matrices (niet een combinatie daarvan) zijn. Als er twee objecten met dezelfde naam Hallo in de uiteindelijke uitvoer hello, is laatste Hallo-object met die naam wordt weergegeven in de definitieve Hallo-object. <p> **Parameternummer**: 1...*n* <p> **Naam**: verzameling*n* <p> **Beschrijving**: vereist. Hallo verzamelingen tooevaluate. Een object dat wordt weergegeven in de Hallo verzamelingen wordt ook weergegeven in Hallo resultaat.|  
|eerste|Retourneert de eerste element in de matrix Hallo Hallo of tekenreeks ingevoerd. Bijvoorbeeld: deze functie retourneert `0`: <p>`first([0,2,3])` <p> **Parameternummer**: 1 <p> **Naam**: verzameling <p> **Beschrijving**: vereist. Hallo tootake Hallo eerste verzamelingsobject van.|  
|laatste|Retourneert de laatste element in de matrix Hallo Hallo of tekenreeks ingevoerd. Bijvoorbeeld: deze functie retourneert `3`: <p>`last('0123')` <p> **Parameternummer**: 1 <p> **Naam**: verzameling <p> **Beschrijving**: vereist. Hallo tootake Hallo laatste verzamelingsobject van.|  
|duren|Retourneert Hallo eerst **aantal** elementen uit Hallo matrix of tekenreeks doorgegeven. Bijvoorbeeld: deze functie retourneert `[1, 2]`:  <p>`take([1, 2, 3, 4], 2)` <p> **Parameternummer**: 1 <p> **Naam**: verzameling <p> **Beschrijving**: vereist. Hallo-verzameling van tootake Hallo waar eerst **aantal** objecten. <p> **Parameternummer**: 2 <p> **Naam**: aantal <p> **Beschrijving**: vereist. het aantal objecten tootake van Hallo Hallo **verzameling**. Moet een positief geheel getal zijn.|  
|Overslaan|Retourneert de elementen in Hallo matrix begint bij index Hallo **aantal**. Bijvoorbeeld: deze functie retourneert `[3, 4]`: <p>`skip([1, 2 ,3 ,4], 2)` <p> **Parameternummer**: 1 <p> **Naam**: verzameling <p> **Beschrijving**: vereist. verzameling tooskip Hallo eerst Hallo **aantal** objecten uit. <p> **Parameternummer**: 2 <p> **Naam**: aantal <p> **Beschrijving**: vereist. aantal objecten tooremove van Hallo voor van Hallo **verzameling**. Moet een positief geheel getal zijn.|  
|join|Retourneert een tekenreeks die bij elk item van een matrix die is gekoppeld met een scheidingsteken, bijvoorbeeld dit retourneert `"1,2,3,4"`:<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: verzameling<br /><br /> **Beschrijving**: vereist. Hallo verzameling toojoin items uit.<br /><br /> **Parameternummer**: 2<br /><br /> **Naam**: scheidingsteken<br /><br /> **Beschrijving**: vereist. Hallo tekenreeks toodelimit items.|  
  
### <a name="string-functions"></a>Tekenreeks-functies

Hallo na functies alleen van toepassing toostrings. U kunt ook sommige functies van de verzameling op tekenreeksen.  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|concat|Een combinatie van een willekeurig aantal tekenreeksen samen. Bijvoorbeeld, als parameter 1 `p1`, retourneert deze functie `somevalue-p1-somevalue`: <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Parameternummer**: 1...*n* <p> **Naam**: tekenreeks*n* <p> **Beschrijving**: vereist. Hallo tekenreeksen toocombine in één tekenreeks.|  
|de subtekenreeks|Retourneert een subset van tekens van een tekenreeks. Bijvoorbeeld: deze functie retourneert `abc`: <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks welke Hallo subtekenreeks wordt opgehaald. <p> **Parameternummer**: 2 <p> **Naam**: startIndex <p> **Beschrijving**: vereist. Hallo-index van waar Hallo subtekenreeks in de parameter 1 begint. <p> **Parameternummer**: 3 <p> **Naam**: lengte <p> **Beschrijving**: vereist. Hallo-lengte van Hallo substring.|  
|vervangen|Vervangt een tekenreeks door een bepaalde tekenreeks. Bijvoorbeeld: deze functie retourneert `hello new string`: <p>`replace('hello old string', 'old', 'new')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks die wordt doorzocht voor parameter 2 en 3,-parameter bijgewerkt als parameter 2 wordt gevonden in parameter 1. <p> **Parameternummer**: 2 <p> **Naam**: oude tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks tooreplace met de parameter 3, wanneer een overeenkomst is gevonden in de parameter 1 <p> **Parameternummer**: 3 <p> **Naam**: nieuwe tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks die gebruikte tooreplace Hallo tekenreeks in de parameter 2 wanneer een overeenkomst is gevonden in de parameter 1.|  
|GUID|Deze functie genereert een globally unique identifier (GUID)-tekenreeks. Deze functie kan bijvoorbeeld deze GUID genereren:`c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Parameternummer**: 1 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Een enkele indelingsopgave die aangeeft [hoe tooformat waarde van deze Guid Hallo](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). Hallo indelingsparameter is "N", "D", "B", 'P' of 'X'. Als de indeling niet is opgegeven, wordt "D" gebruikt.|  
|toLower|Zet een tekenreeks toolowercase. Bijvoorbeeld: deze functie retourneert `two by two is four`: <p>`toLower('Two by Two is Four')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks tooconvert toolower hoofdlettergebruik. Als een teken in de reeks Hallo is geen equivalent van een kleine letter, is Hallo teken opgenomen in Hallo tekenreeks geretourneerd ongewijzigd.|  
|toUpper|Zet een tekenreeks toouppercase. Bijvoorbeeld: deze functie retourneert `TWO BY TWO IS FOUR`: <p>`toUpper('Two by Two is Four')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks tooconvert tooupper hoofdlettergebruik. Als een teken in de reeks Hallo geen hoofdletters equivalent is Hallo-teken opgenomen in Hallo tekenreeks geretourneerd ongewijzigd.|  
|indexOf|Hallo-index van een waarde binnen case tekenreeks insensitively vinden. Bijvoorbeeld: deze functie retourneert `7`: <p>`indexof('hello, world.', 'world')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks die Hallo-waarde kan bevatten. <p> **Parameternummer**: 2 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo waarde toosearch Hallo index van.|  
|lastIndexOf|Hallo laatste index van een waarde binnen case tekenreeks insensitively vinden. Bijvoorbeeld: deze functie retourneert `3`: <p>`lastindexof('foofoo', 'foo')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks die Hallo-waarde kan bevatten. <p> **Parameternummer**: 2 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo waarde toosearch Hallo index van.|  
|StartsWith|Controleert of Hallo tekenreeks op de insensitively met een waarde-aanvraag begint. Bijvoorbeeld: deze functie retourneert `true`: <p>`startswith('hello, world', 'hello')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks die Hallo-waarde kan bevatten. <p> **Parameternummer**: 2 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo Hallo tekenreekswaarde kan beginnen met.|  
|EndsWith|Controleert of Hallo tekenreeks op de insensitively op een waarde-aanvraag eindigt. Bijvoorbeeld: deze functie retourneert `true`: <p>`endswith('hello, world', 'world')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks die Hallo-waarde kan bevatten. <p> **Parameternummer**: 2 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo Hallo tekenreekswaarde kan eindigen op.|  
|split|Splitst Hallo tekenreeks met een scheidingsteken. Bijvoorbeeld: deze functie retourneert `["a", "b", "c"]`: <p>`split('a;b;c',';')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo-tekenreeks die wordt gesplitst. <p> **Parameternummer**: 2 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo scheidingsteken.|  
  
### <a name="logical-functions"></a>Logische functies  

Deze functies zijn nuttig in voorwaarden en gebruikte tooevaluate elk type logica kunnen worden.  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|is gelijk aan|Retourneert waar als twee waarden gelijk zijn. Bijvoorbeeld, parameter1 someValue wordt deze functie retourneert `true`: <p>`equals(parameters('parameter1'), 'someValue')` <p> **Parameternummer**: 1 <p> **Naam**: 1-Object <p> **Beschrijving**: vereist. Hallo object toocompare te**Object 2**. <p> **Parameternummer**: 2 <p> **Naam**: Object-2 <p> **Beschrijving**: vereist. Hallo object toocompare te**1 Object**.|  
|minder|Retourneert waar als het eerste argument Hallo kleiner dan Hallo tweede is. Houd er rekening mee waarden kunnen alleen worden van het type geheel getal, float of string. Bijvoorbeeld: deze functie retourneert `true`: <p>`less(10,100)` <p> **Parameternummer**: 1 <p> **Naam**: 1-Object <p> **Beschrijving**: vereist. Hallo object toocheck als het is minder dan **Object 2**. <p> **Parameternummer**: 2 <p> **Naam**: Object-2 <p> **Beschrijving**: vereist. Hallo object toocheck groter is dan **1 Object**.|  
|lessOrEquals|Retourneert waar als het eerste argument Hallo is kleiner dan of gelijk zijn aan toohello tweede. Houd er rekening mee waarden kunnen alleen worden van het type geheel getal, float of string. Bijvoorbeeld: deze functie retourneert `true`: <p>`lessOrEquals(10,10)` <p> **Parameternummer**: 1 <p> **Naam**: 1-Object <p> **Beschrijving**: vereist. Hallo object toocheck als kleiner is dan of gelijk te**Object 2**. <p> **Parameternummer**: 2 <p> **Naam**: Object-2 <p> **Beschrijving**: vereist. Hallo object toocheck als deze groter dan is of gelijk zijn aan te**1 Object**.|  
|groter|Retourneert waar als het eerste argument Hallo groter dan Hallo tweede is. Houd er rekening mee waarden kunnen alleen worden van het type geheel getal, float of string. Bijvoorbeeld: deze functie retourneert `false`:  <p>`greater(10,10)` <p> **Parameternummer**: 1 <p> **Naam**: 1-Object <p> **Beschrijving**: vereist. Hallo object toocheck groter is dan **Object 2**. <p> **Parameternummer**: 2 <p> **Naam**: Object-2 <p> **Beschrijving**: vereist. Hallo object toocheck als het is minder dan **1 Object**.|  
|greaterOrEquals|Retourneert waar als eerste argument Hallo groter dan of gelijk toohello seconde is. Houd er rekening mee waarden kunnen alleen worden van het type geheel getal, float of string. Bijvoorbeeld: deze functie retourneert `false`: <p>`greaterOrEquals(10,100)` <p> **Parameternummer**: 1 <p> **Naam**: 1-Object <p> **Beschrijving**: vereist. Hallo object toocheck als deze groter dan is of gelijk zijn aan te**Object 2**. <p> **Parameternummer**: 2 <p> **Naam**: Object-2 <p> **Beschrijving**: vereist. Hallo object toocheck als kleiner dan of gelijk is te**1 Object**.|  
|en|Retourneert waar als beide parameters van toepassing zijn. Beide argumenten moeten toobe Booleaanse waarden. Bijvoorbeeld: deze functie retourneert `false`: <p>`and(greater(1,10),equals(0,0))` <p> **Parameternummer**: 1 <p> **Naam**: Booleaanse 1 <p> **Beschrijving**: vereist. eerste argument die moet worden Hallo `true`. <p> **Parameternummer**: 2 <p> **Naam**: Booleaanse 2 <p> **Beschrijving**: vereist. het tweede argument Hallo moet `true`.|  
|of|Retourneert waar als de parameter ingesteld op true is. Beide argumenten moeten toobe Booleaanse waarden. Bijvoorbeeld: deze functie retourneert `true`: <p>`or(greater(1,10),equals(0,0))` <p> **Parameternummer**: 1 <p> **Naam**: Booleaanse 1 <p> **Beschrijving**: vereist. het eerste argument die mogelijk Hallo `true`. <p> **Parameternummer**: 2 <p> **Naam**: Booleaanse 2 <p> **Beschrijving**: vereist. het tweede argument Hallo mogelijk `true`.|  
|niet|Retourneert waar als Hallo parameters zijn `false`. Beide argumenten moeten toobe Booleaanse waarden. Bijvoorbeeld: deze functie retourneert `true`: <p>`not(contains('200 Success','Fail'))` <p> **Parameternummer**: 1 <p> **Naam**: Booleaanse <p> **Beschrijving**: retourneert true als het Hallo-parameters zijn `false`. Beide argumenten moeten toobe Booleaanse waarden. Deze functie retourneert `true`:`not(contains('200 Success','Fail'))`|  
|Als|Retourneert een opgegeven waarde, op basis van of Hallo expressie uitgewezen `true` of `false`.  Bijvoorbeeld: deze functie retourneert `"yes"`: <p>`if(equals(1, 1), 'yes', 'no')` <p> **Parameternummer**: 1 <p> **Naam**: expressie <p> **Beschrijving**: vereist. Een Booleaanse waarde die welke waarde Hallo-expressie bepaalt moet worden geretourneerd. <p> **Parameternummer**: 2 <p> **Naam**: True <p> **Beschrijving**: vereist. Hallo waarde tooreturn als Hallo expressie `true`. <p> **Parameternummer**: 3 <p> **Naam**: False <p> **Beschrijving**: vereist. Hallo waarde tooreturn als Hallo expressie `false`.|  
  
### <a name="conversion-functions"></a>Van conversiefuncties  

Deze functies zijn gebruikt tooconvert tussen elk van de systeemeigen typen Hallo in Hallo taal:  
  
- Tekenreeks  
  
- geheel getal  
  
- Float  
  
- Booleaanse waarde  
  
- Matrices  
  
- woordenlijsten  

-   Formulieren  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|int|Hallo parameter tooan integer niet converteren. Deze functie retourneert bijvoorbeeld 100 als een getal in plaats van een tekenreeks: <p>`int('100')` <p> **Parameternummer**: 1 <p> **Naam**: waarde <p> **Beschrijving**: vereist. Hallo-waarde die is geconverteerd tooan geheel getal.|  
|Tekenreeks|Hallo parameter tooa tekenreeks converteren. Bijvoorbeeld: deze functie retourneert `'10'`: <p>`string(10)` <p>U kunt ook een tekenreeks van de tooa object converteren. Bijvoorbeeld, als hello `myPar` parameter is een object met één eigenschap `abc : xyz`, retourneert deze functie `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Parameternummer**: 1 <p> **Naam**: waarde <p> **Beschrijving**: vereist. Hallo waarde die is geconverteerd tooa tekenreeks.|  
|JSON|Hallo tooa JSON type parameterwaarde converteren en is Hallo tegenovergestelde van `string()`. Bijvoorbeeld: deze functie retourneert `[1,2,3]` als een matrix in plaats van een tekenreeks: <p>`json('[1,2,3]')` <p>U kunt ook een tekenreeksobject tooan converteren. Bijvoorbeeld: deze functie retourneert `{ "abc" : "xyz" }`: <p>`json('{"abc" : "xyz"}')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreekswaarde is geconverteerde tooa systeemeigen type. <p>Hallo `json()` functie XML te invoer ondersteunt. Bijvoorbeeld, Hallo parameterwaarde van: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>geconverteerde toothis JSON is: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|Float|Hallo parameter argument tooa kommagetal converteren. Bijvoorbeeld: deze functie retourneert `10.333`: <p>`float('10.333')` <p> **Parameternummer**: 1 <p> **Naam**: waarde <p> **Beschrijving**: vereist. Hallo waarde die is geconverteerd tooa kommagetal.|  
|BOOL|Hallo parameter tooa Booleaanse waarde converteren. Bijvoorbeeld: deze functie retourneert `false`: <p>`bool(0)` <p> **Parameternummer**: 1 <p> **Naam**: waarde <p> **Beschrijving**: vereist. Hallo-waarde die is geconverteerd tooa Boolean-waarde.|  
|Coalesce|Retourneert de eerste niet-null-object Hallo Hallo argumenten doorgegeven. **Opmerking**: een lege tekenreeks niet null is. Bijvoorbeeld, als parameters 1 en 2 niet zijn gedefinieerd, deze functie retourneert `fallback`:  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Parameternummer**: 1...*n* <p> **Naam**: Object*n* <p> **Beschrijving**: vereist. Hallo objecten toocheck voor null.|  
|Base64|Retourneert Hallo base64-weergave van de invoertekenreeks Hallo. Bijvoorbeeld: deze functie retourneert `c29tZSBzdHJpbmc=`: <p>`base64('some string')` <p> **Parameternummer**: 1 <p> **Naam**: String 1 <p> **Beschrijving**: vereist. Hallo tekenreeks tooencode in base64-weergave.|  
|base64ToBinary|Retourneert een binaire voorstelling van een base64-gecodeerde tekenreeks. Bijvoorbeeld: deze functie retourneert Hallo binaire voorstelling van `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo base64-gecodeerde tekenreeks.|  
|base64ToString|Retourneert een string-weergave van een based64 gecodeerde tekenreeks. Bijvoorbeeld: deze functie retourneert `some string`: <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo base64-gecodeerde tekenreeks.|  
|Binaire|Retourneert een binaire voorstelling van een waarde.  Bijvoorbeeld: deze functie retourneert een binaire voorstelling van `some string`: <p>`binary('some string')` <p> **Parameternummer**: 1 <p> **Naam**: waarde <p> **Beschrijving**: vereist. Hallo-waarde die is geconverteerd toobinary.|  
|dataUriToBinary|Retourneert een binaire voorstelling van een gegevens-URI. Bijvoorbeeld: deze functie retourneert Hallo binaire voorstelling van `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo gegevens URI tooconvert toobinary weergave.|  
|dataUriToString|Retourneert een tekenreeksrepresentatie van een gegevens-URI. Bijvoorbeeld: deze functie retourneert `some string`: <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks<p> **Beschrijving**: vereist. Hallo gegevens URI tooconvert tooString weergave.|  
|dataUri|Retourneert een gegevens-URI van een waarde. Bijvoorbeeld: deze functie retourneert deze gegevens URI `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`: <p>`dataUri('some string')` <p> **Parameternummer**: 1<p> **Naam**: waarde<p> **Beschrijving**: vereist. Hallo waarde tooconvert toodata URI.|  
|decodeBase64|Retourneert een tekenreeksrepresentatie van een invoer based64-tekenreeks. Bijvoorbeeld: deze functie retourneert `some string`: <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: een tekenreeksrepresentatie van een invoer based64-tekenreeks geretourneerd.|  
|encodeUriComponent|URL-Hiermee heft Hallo-tekenreeks die doorgegeven. Bijvoorbeeld: deze functie retourneert `You+Are%3ACool%2FAwesome`: <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks tooescape URL onveilige tekens uit.|  
|decodeUriComponent|Ongedaan maken-URL-Hiermee heft Hallo-tekenreeks die doorgegeven. Bijvoorbeeld: deze functie retourneert `You Are:Cool/Awesome`: <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks toodecode Hallo URL onveilige tekens uit.|  
|decodeDataUri|Retourneert een binaire voorstelling van invoergegevens URI-tekenreeks. Bijvoorbeeld: deze functie retourneert Hallo binaire voorstelling van `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo dataURI toodecode in een binaire voorstelling.|  
|uriComponent|Retourneert een URI gecodeerde representatie van een waarde. Bijvoorbeeld: deze functie retourneert `You+Are%3ACool%2FAwesome`: <p>`uriComponent('You Are:Cool/Awesome')` <p> **Parameternummer**: 1<p> **Naam**: tekenreeks <p> **Beschrijving**: vereist. Hallo tekenreeks toobe URI gecodeerd.|  
|uriComponentToBinary|Retourneert dat een binaire voorstelling van een URI-gecodeerde tekenreeks. Bijvoorbeeld: deze functie retourneert een binaire voorstelling van `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Parameternummer**: 1 <p> **Naam**: tekenreeks<p> **Beschrijving**: vereist. Hallo URI-gecodeerde tekenreeks.|  
|uriComponentToString|Retourneert dat een tekenreeksrepresentatie van een URI-gecodeerde tekenreeks. Bijvoorbeeld: deze functie retourneert `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Parameternummer**: 1<p> **Naam**: tekenreeks<p> **Beschrijving**: vereist. Hallo URI-gecodeerde tekenreeks.|  
|xml|Een XML-representatie van Hallo waarde retourneren. Bijvoorbeeld: deze functie retourneert XML-inhoud dat wordt vertegenwoordigd door `'\<name>Alan\</name>'`: <p>`xml('\<name>Alan\</name>')` <p>Hallo `xml()` functie biedt ondersteuning voor JSON-object te invoer. Bijvoorbeeld, Hallo parameter `{ "abc": "xyz" }` is geconverteerde tooXML inhoud:`\<abc>xyz\</abc>` <p> **Parameternummer**: 1<p> **Naam**: waarde<p> **Beschrijving**: vereist. Hallo waarde tooconvert tooXML.|  
|XPath|Retourneert een matrix van XML-knooppunt die overeenkomt met de Hallo xpath-expressie van een waarde die het resultaat Hallo xpath-expressie. <p> **Voorbeeld 1** <p>Wordt ervan uitgegaan dat de waarde van parameter Hallo `p1` een tekenreeksrepresentatie van deze XML is: <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Deze code:`xpath(xml(parameters('p1'), '/lab/robot/name')` <p>retourneert <p>`[ <name>R1</name>, <name>R2</name> ]` <p>tijdens deze code: <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>retourneert <p>`13` <p> <p> **Voorbeeld 2** <p>Opgegeven Hallo XML-inhoud te volgen: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Deze code:`@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>of deze code: <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>retourneert <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>En deze code:`@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>retourneert <p>``xyz`` <p> **Parameternummer**: 1 <p> **Naam**: Xml <p> **Beschrijving**: vereist. Hallo-XML op welke tooevaluate Hallo XPath expressie. <p> **Parameternummer**: 2 <p> **Naam**: XPath <p> **Beschrijving**: vereist. Hallo XPath-expressie tooevaluate.|  
|matrix|Hallo tooan parametermatrix converteren. Bijvoorbeeld: deze functie retourneert `["abc"]`: <p>`array('abc')` <p> **Parameternummer**: 1 <p> **Naam**: waarde <p> **Beschrijving**: vereist. Hallo-waarde die is geconverteerd tooan matrix.|
|createArray|Maakt een matrix van Hallo-parameters. Bijvoorbeeld: deze functie retourneert `["a", "c"]`: <p>`createArray('a', 'c')` <p> **Parameternummer**: 1...*n* <p> **Naam**:*n* <p> **Beschrijving**: vereist. Hallo toocombine van de waarden in een matrix.|
|triggerFormDataValue|Retourneert één waarde die overeenkomt met de sleutelnaam Hallo van gegevens van een formulier of trigger formulier gecodeerde uitvoer.  Als er meerdere overeenkomt met deze fout wordt.  Bijvoorbeeld de volgende Hallo retourneert `bar`:`triggerFormDataValue('foo')`<br /><br />**Parameternummer**: 1<br /><br />**Naam**: naam sleutel<br /><br />**Beschrijving**: vereist. sleutelnaam van Hallo formulier gegevens waarde tooreturn Hallo.|
|triggerFormDataMultiValues|Retourneert een matrix met waarden die overeenkomen met de sleutelnaam Hallo van gegevens van een formulier of trigger formulier gecodeerde uitvoer.  Bijvoorbeeld de volgende Hallo retourneert `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Parameternummer**: 1<br /><br />**Naam**: naam sleutel<br /><br />**Beschrijving**: vereist. sleutelnaam van formuliergegevens Hallo Hallo tooreturn waarden.|
|triggerMultipartBody|Retourneert Hallo hoofdtekst voor een onderdeel in de uitvoer van een meerdelige van Hallo-trigger.<br /><br />**Parameternummer**: 1<br /><br />**Naam**: Index<br /><br />**Beschrijving**: vereist. Hallo-index van Hallo onderdeel tooretrieve.|
|formDataValue|Retourneert één waarde die overeenkomt met de Hallo sleutelnaam van gegevens van een formulier of actie formulier gecodeerde uitvoer.  Als er meerdere overeenkomt met deze fout wordt.  Bijvoorbeeld de volgende Hallo retourneert `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Parameternummer**: 1<br /><br />**Naam**: naam van de actie<br /><br />**Beschrijving**: vereist. Hallo-naam van Hallo actie met het antwoord op een formulier gegevens of formulier-codering.<br /><br />**Parameternummer**: 2<br /><br />**Naam**: naam sleutel<br /><br />**Beschrijving**: vereist. sleutelnaam van Hallo formulier gegevens waarde tooreturn Hallo.|
|formDataMultiValues|Retourneert een matrix met waarden die overeenkomen met Hallo sleutelnaam van gegevens van een formulier of actie formulier gecodeerde uitvoer.  Bijvoorbeeld de volgende Hallo retourneert `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Parameternummer**: 1<br /><br />**Naam**: naam van de actie<br /><br />**Beschrijving**: vereist. Hallo-naam van Hallo actie met het antwoord op een formulier gegevens of formulier-codering.<br /><br />**Parameternummer**: 2<br /><br />**Naam**: naam sleutel<br /><br />**Beschrijving**: vereist. sleutelnaam van formuliergegevens Hallo Hallo tooreturn waarden.|
|multipartBody|Retourneert Hallo hoofdtekst voor een onderdeel in de uitvoer van een meerdelige van een actie.<br /><br />**Parameternummer**: 1<br /><br />**Naam**: naam van de actie<br /><br />**Beschrijving**: vereist. Hallo-naam van Hallo actie met een meerdelige antwoord.<br /><br />**Parameternummer**: 2<br /><br />**Naam**: Index<br /><br />**Beschrijving**: vereist. Hallo-index van Hallo onderdeel tooretrieve.|

### <a name="math-functions"></a>Rekenkundige functies  

Deze functies kunnen worden gebruikt voor beide typen van de getallen: **gehele getallen** en **zwevend**.  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|toevoegen|Hallo resultaat van het toevoegen van Hallo twee getallen. Bijvoorbeeld: deze functie retourneert `20.333`: <p>`add(10,10.333)` <p> **Parameternummer**: 1 <p> **Naam**: Summand 1 <p> **Beschrijving**: vereist. aantal tooadd te Hallo**Summand 2**. <p> **Parameternummer**: 2 <p> **Naam**: Summand 2 <p> **Beschrijving**: vereist. aantal tooadd te Hallo**Summand 1**.|  
|Sub|Hallo resultaat van de twee getallen af te trekken. Bijvoorbeeld: deze functie retourneert `-0.333`: <p>`sub(10,10.333)` <p> **Parameternummer**: 1 <p> **Naam**: Minuend <p> **Beschrijving**: vereist. Hallo-nummer **Subtrahend** wordt verwijderd uit. <p> **Parameternummer**: 2 <p> **Naam**: Subtrahend <p> **Beschrijving**: vereist. aantal tooremove van Hallo Hallo **Minuend**.|  
|mul|Hallo resultaat van het Hallo twee getallen vermenigvuldigen. Bijvoorbeeld: deze functie retourneert `103.33`: <p>`mul(10,10.333)` <p> **Parameternummer**: 1 <p> **Naam**: Multiplicand 1 <p> **Beschrijving**: vereist. aantal toomultiply Hallo **Multiplicand 2** met. <p> **Parameternummer**: 2 <p> **Naam**: Multiplicand 2 <p> **Beschrijving**: vereist. aantal toomultiply Hallo **Multiplicand 1** met.|  
|div|Hallo resultaat van de deling van Hallo twee getallen. Bijvoorbeeld: deze functie retourneert `1.0333`: <p>`div(10.333,10)` <p> **Parameternummer**: 1 <p> **Naam**: deeltal <p> **Beschrijving**: vereist. aantal toodivide door Hallo Hallo **deler**. <p> **Parameternummer**: 2 <p> **Naam**: deler <p> **Beschrijving**: vereist. het aantal toodivide Hallo Hallo **deeltal** door.|  
|Mod|Retourneert Hallo restgetal deling van twee getallen hello (modulo). Bijvoorbeeld: deze functie retourneert `2`: <p>`mod(10,4)` <p> **Parameternummer**: 1 <p> **Naam**: deeltal <p> **Beschrijving**: vereist. aantal toodivide door Hallo Hallo **deler**. <p> **Parameternummer**: 2 <p> **Naam**: deler <p> **Beschrijving**: vereist. het aantal toodivide Hallo Hallo **deeltal** door. Hallo rest wordt na Hallo deling worden genomen.|  
|min.|Er zijn twee verschillende patronen voor het aanroepen van deze functie. <p>Hier `min` neemt een matrix en Hallo functie retourneert `0`: <p>`min([0,1,2])` <p>U kunt ook deze functie kan duren voordat een door komma's gescheiden lijst met waarden en ook retourneert `0`: <p>`min(0,1,2)` <p> **Opmerking**: alle waarden moeten getallen, zodat als Hallo-parameter is een matrix, Hallo matrix heeft tooonly getallen hebben. <p> **Parameternummer**: 1 <p> **Naam**: verzameling of -waarde <p> **Beschrijving**: vereist. Ofwel een matrix met waarden toofind Hallo minimumwaarde of Hallo eerste waarde van een set. <p> **Parameternummer**: 2...*n* <p> **Naam**: waarde*n* <p> **Beschrijving**: optioneel. Als de eerste parameter Hallo waarde is, klikt u vervolgens kunt u aanvullende waarden doorgeven en hello minimum van alle doorgegeven waarden geretourneerd.|  
|Maximum aantal|Er zijn twee verschillende patronen voor het aanroepen van deze functie. <p>Hier `max` neemt een matrix en Hallo functie retourneert `2`: <p>`max([0,1,2])` <p>U kunt ook deze functie kan duren voordat een door komma's gescheiden lijst met waarden en ook retourneert `2`: <p>`max(0,1,2)` <p> **Opmerking**: alle waarden moeten getallen, zodat als Hallo-parameter is een matrix, Hallo matrix heeft tooonly getallen hebben. <p> **Parameternummer**: 1 <p> **Naam**: verzameling of -waarde <p> **Beschrijving**: vereist. Ofwel een matrix met waarden toofind Hallo maximumwaarde of Hallo eerste waarde van een set. <p> **Parameternummer**: 2...*n* <p> **Naam**: waarde*n* <p> **Beschrijving**: optioneel. Als de eerste parameter Hallo waarde is, klikt u vervolgens kunt u aanvullende waarden doorgeven en hello maximum van alle doorgegeven waarden geretourneerd.|  
|bereik|Genereert een matrix van gehele getallen vanaf een bepaald aantal. Definieert u Hallo lengte van Hallo matrix geretourneerd. <p>Bijvoorbeeld: deze functie retourneert `[3,4,5,6]`: <p>`range(3,4)` <p> **Parameternummer**: 1 <p> **Naam**: startIndex <p> **Beschrijving**: vereist. Hallo eerste geheel getal in Hallo matrix. <p> **Parameternummer**: 2 <p> **Naam**: aantal <p> **Beschrijving**: vereist. Deze waarde is Hallo aantal gehele getallen die in het Hallo-matrix.|  
|rand|Genereert een willekeurige geheel getal zijn binnen Hallo opgegeven bereik (inclusief alleen op de eerste end). Deze functie kunt bijvoorbeeld een `0` of '1': <p>`rand(0,2)` <p> **Parameternummer**: 1 <p> **Naam**: minimale <p> **Beschrijving**: vereist. Hallo laagste geheel getal dat kan worden geretourneerd. <p> **Parameternummer**: 2 <p> **Naam**: maximale <p> **Beschrijving**: vereist. Deze waarde is Hallo volgende gehele getal na Hallo hoogste integer die kan worden geretourneerd.|  
  
### <a name="date-functions"></a>Datumfuncties  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|utcnow|Retourneert Hallo Huidig timestamp als een tekenreeks, bijvoorbeeld: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Parameternummer**: 1 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|addSeconds|Een geheel aantal seconden tooa tekenreeks tijdstempel doorgegeven toegevoegd. Hallo aantal seconden mag positief of negatief zijn. Standaard Hallo resultaat is een tekenreeks in de ISO 8601-notatie ("o"), tenzij een indelingsopgave is opgegeven. Bijvoorbeeld: `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Parameternummer**: 1 <p> **Naam**: Timestamp <p> **Beschrijving**: vereist. Een tekenreeks waarin Hallo tijd. <p> **Parameternummer**: 2 <p> **Naam**: seconden <p> **Beschrijving**: vereist. Hallo aantal seconden tooadd. Negatieve toosubtract seconden kan zijn. <p> **Parameternummer**: 3 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|addminutes|Een geheel aantal minuten tooa tekenreeks tijdstempel doorgegeven toegevoegd. het aantal minuten Hallo mag positief of negatief zijn. Standaard Hallo resultaat is een tekenreeks in de ISO 8601-notatie ("o"), tenzij een indelingsopgave is opgegeven. Bijvoorbeeld: `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Parameternummer**: 1 <p> **Naam**: Timestamp <p> **Beschrijving**: vereist. Een tekenreeks waarin Hallo tijd. <p> **Parameternummer**: 2 <p> **Naam**: minuten <p> **Beschrijving**: vereist. Hallo aantal minuten tooadd. Negatieve toosubtract minuten kan zijn. <p> **Parameternummer**: 3 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|addhours|Een geheel aantal uren tooa tekenreeks tijdstempel doorgegeven toegevoegd. het aantal uren Hallo mag positief of negatief zijn. Standaard Hallo resultaat is een tekenreeks in de ISO 8601-notatie ("o"), tenzij een indelingsopgave is opgegeven. Bijvoorbeeld: `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Parameternummer**: 1 <p> **Naam**: Timestamp <p> **Beschrijving**: vereist. Een tekenreeks waarin Hallo tijd. <p> **Parameternummer**: 2 <p> **Naam**: uren <p> **Beschrijving**: vereist. Hallo aantal uren tooadd. Negatieve toosubtract uren kan zijn. <p> **Parameternummer**: 3 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|addDays|Een geheel aantal dagen tooa tekenreeks tijdstempel doorgegeven toegevoegd. het aantal dagen Hallo mag positief of negatief zijn. Standaard Hallo resultaat is een tekenreeks in de ISO 8601-notatie ("o"), tenzij een indelingsopgave is opgegeven. Bijvoorbeeld: `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Parameternummer**: 1 <p> **Naam**: Timestamp <p> **Beschrijving**: vereist. Een tekenreeks waarin Hallo tijd. <p> **Parameternummer**: 2 <p> **Naam**: dagen <p> **Beschrijving**: vereist. Hallo aantal dagen tooadd. Negatieve toosubtract dagen kan zijn. <p> **Parameternummer**: 3 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|formatDateTime|Retourneert een tekenreeks in datumnotatie. Standaard Hallo resultaat is een tekenreeks in de ISO 8601-notatie ("o"), tenzij een indelingsopgave is opgegeven. Bijvoorbeeld: `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Parameternummer**: 1 <p> **Naam**: datum <p> **Beschrijving**: vereist. Een tekenreeks met Hallo datum. <p> **Parameternummer**: 2 <p> **Naam**: indeling <p> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|startOfHour|Retourneert Hallo starten van het Hallo uur tooa tekenreeks timestamp doorgegeven. Bijvoorbeeld `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.<br /><br />**Parameternummer**: 2<br /><br /> **Naam**: indeling<br /><br /> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.|  
|startOfDay|Retourneert Hallo starten van het Hallo dag tooa tekenreeks timestamp doorgegeven. Bijvoorbeeld `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.<br /><br />**Parameternummer**: 2<br /><br /> **Naam**: indeling<br /><br /> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.| 
|startOfMonth|Retourneert Hallo starten van het Hallo maand tooa tekenreeks timestamp doorgegeven. Bijvoorbeeld `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.<br /><br />**Parameternummer**: 2<br /><br /> **Naam**: indeling<br /><br /> **Beschrijving**: optioneel. Ofwel een [enkel indeling aanduiding teken](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) of een [aangepaste indeling patroon](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) die aangeeft hoe tooformat waarde van dit tijdstempel Hallo. Als indeling niet opgegeven is, wordt Hallo ISO 8601-notatie ("o") gebruikt.| 
|DayOfWeek|Retourneert Hallo dag van het onderdeel van de week van een tijdstempel voor een tekenreeks.  Zondag is ingesteld op 0, maandag 1, enzovoort. Bijvoorbeeld `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.| 
|DayOfMonth|Retourneert Hallo dag van het onderdeel van de maand van een tijdstempel voor een tekenreeks. Bijvoorbeeld `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.| 
|DayOfYear|Retourneert Hallo dag van het jaar onderdeel van een tijdstempel voor een tekenreeks. Bijvoorbeeld `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.| 
|ticks|Retourneert Hallo ticks eigenschap van een tijdstempel voor een tekenreeks. Bijvoorbeeld `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Parameternummer**: 1<br /><br /> **Naam**: Timestamp<br /><br /> **Beschrijving**: vereist. Dit is een tekenreeks die Hallo tijd bevat.| 
  
### <a name="workflow-functions"></a>Werkstroom-functies  

Deze functies vindt u informatie over Hallo werkstroom zichzelf tijdens runtime.  
  
|Functienaam|Beschrijving|  
|-------------------|-----------------|  
|listCallbackUrl|Retourneert een tekenreeks toocall tooinvoke Hallo trigger of actie. <p> **Opmerking**: deze functie kan alleen worden gebruikt een **httpWebhook** en **apiConnectionWebhook**, niet in een **handmatige**, **terugkeerpatroon**, **http**, of **apiConnection**. <p>Bijvoorbeeld, Hallo `listCallbackUrl()` retourneert werken: <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|werkstroom|Deze functie biedt alle Hallo details voor Hallo werkstroom zichzelf tijdens runtime Hallo. <p> Beschikbare eigenschappen op Hallo werkstroomobject zijn: <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> waarde van Hallo Hallo `run` eigenschap is een object met de volgende eigenschappen: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Zie Hallo [Rest-API](http://go.microsoft.com/fwlink/p/?LinkID=525617) voor meer informatie over deze eigenschappen.<p> Bijvoorbeeld: tooget Hallo naam Hallo huidige uitvoert, gebruik Hallo `"@workflow().run.name"` expressie. |

## <a name="next-steps"></a>Volgende stappen

[Werkstroomacties en -triggers](logic-apps-workflow-actions-triggers.md)
