---
title: aaaField toewijzingen in Azure Search indexeerfuncties
description: Azure Search indexeerfunctie veld toewijzingen tooaccount voor verschillen in het veld namen en gegevens verklaringen configureren
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Veld-verwijzingen in Azure Search indexeerfuncties
Wanneer u Azure Search indexeerfuncties, kunt u zelf zo nu en dan vinden in situaties waar uw invoergegevens behoorlijk Hallo-schema van de doelindex komt niet overeen. In deze gevallen kunt u **veld toewijzingen** tootransform uw gegevens in Hallo gewenst vorm.

Sommige situaties waarin het veldtoewijzingen handig:

* De gegevensbron bevat een veld `_id`, maar Azure Search mag geen veldnamen die beginnen met een onderstrepingsteken. Een veldtoewijzing kunt u te '' van een veld wijzigen.
* U wilt dat verschillende velden in Hallo index Hello toopopulate dezelfde gegevensbron gegevens, bijvoorbeeld omdat u wilt dat tooapply verschillende analyzers toothose velden. Veldtoewijzingen kunnen u een gegevensbronveld ' vertakken'.
* U moet tooBase64 coderen of uw gegevens te decoderen. Veldtoewijzingen ondersteuning voor diverse **toewijzing functies**, waaronder functies voor Base64 coderen en decoderen.   

## <a name="setting-up-field-mappings"></a>Instellen van veld-verwijzingen
U kunt veldtoewijzingen toevoegen bij het maken van een nieuwe indexeerfunctie Hallo met [indexeerfunctie maken](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. U kunt beheren veldtoewijzingen voor een indexering indexeerfunctie Hallo met [Update indexeerfunctie](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Een veldtoewijzing bestaat uit 3 onderdelen:

1. Een `sourceFieldName`, die staat voor een veld in de gegevensbron. Deze eigenschap is vereist.
2. Een optionele `targetFieldName`, die staat voor een veld in uw search-index. Als u dit weglaat, wordt hello dezelfde naam als in het Hallo-gegevensbron gebruikt.
3. Een optionele `mappingFunction`, die kunt transformeert u uw gegevens met behulp van een van de vooraf gedefinieerde functies. Hallo volledige lijst met functies is [hieronder](#mappingFunctions).

Velden toewijzingen worden toegevoegd toohello `fieldMappings` matrix op Hallo indexeerfunctie definitie.

Dit is hoe u aankan verschillen in veldnamen:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Een indexeerfunctie kan meerdere veldtoewijzingen hebben. Hier volgt een voorbeeld van hoe u kunt "vertakken' een veld:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Azure Search gebruikt niet-hoofdlettergevoelige vergelijking tooresolve Hallo veld en functie namen in veld-verwijzingen. Dit is handig (u hebt geen tooget alle Hallo hoofdlettergebruik rechts), maar het betekent dat de gegevensbron en index kan geen velden hebben die alleen geval verschillen.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Veld toewijzing functies
Deze functies worden momenteel ondersteund:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Voert *URL-safe* Base64-codering Hallo invoerreeks. Wordt ervan uitgegaan dat Hallo invoer UTF-8-codering.

#### <a name="sample-use-case"></a>Voorbeeld gebruiksvoorbeeld
URL-safe tekens kunnen alleen voorkomen in een documentsleutel Azure Search (omdat klanten kunnen tooaddress Hallo document Hallo Lookup-API, bijvoorbeeld met moet). Als uw gegevens URL onveilige tekens bevat en u wilt dat toouse het toopopulate een sleutelveld in uw zoekindex deze functie wilt gebruiken.   

#### <a name="example"></a>Voorbeeld
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Voert het decoderen van Base64 van Hallo invoertekenreeks. Hallo invoer wordt aangenomen dat tooa *URL-safe* Base64-gecodeerde tekenreeks.

#### <a name="sample-use-case"></a>Voorbeeld gebruiksvoorbeeld
BLOB aangepaste metagegevenswaarden moet ASCII-codering. U kunt Base64-codering toorepresent willekeurige Unicode-tekenreeksen in aangepaste metagegevens van de blob. Echter toomake zoeken zinvolle, kunt u deze functie tooturn Hallo gecodeerde gegevens naar 'reguliere' tekenreeksen wanneer uw search-index te vullen.  

#### <a name="example"></a>Voorbeeld
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Splitsingen een tekenreeksveld met Hallo scheidingsteken en uitgelicht Hallo token in het opgegeven opgegeven positie in de resulterende splitsing Hallo Hallo.

Bijvoorbeeld, als hello invoer is `Jane Doe`, Hallo `delimiter` is `" "`(spatie) en Hallo `position` is ingesteld op 0, Hallo uitkomst `Jane`; als hello `position` 1 is, Hallo resultaat is `Doe`. Als de positie Hallo tooa-token dat niet bestaat verwijst, wordt er een fout geretourneerd.

#### <a name="sample-use-case"></a>Voorbeeld gebruiksvoorbeeld
De gegevensbron bevat een `PersonName` veld en u wilt dat tooindex als twee aparte `FirstName` en `LastName` velden. U kunt deze functie toosplit Hallo invoer met gebruikmaking van Hallo spatie als scheidingsteken hello gebruiken.

#### <a name="parameters"></a>Parameters
* `delimiter`: een tekenreeks toouse Hallo scheiding wanneer invoerreeks splitsen Hallo.
* `position`: de op nul gebaseerde positie van een geheel getal van Hallo token toopick nadat Hallo invoerreeks wordt gesplitst.    

#### <a name="example"></a>Voorbeeld
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Een tekenreeks die is opgemaakt als een JSON-matrix van tekenreeksen in een tekenreeksmatrix die gebruikt toopopulate worden kan transformaties een `Collection(Edm.String)` veld Hallo index.

Bijvoorbeeld, als Hallo invoerreeks is `["red", "white", "blue"]`, en vervolgens het doelveld Hallo van het type `Collection(Edm.String)` worden ingevuld met Hallo drie waarden `red`, `white` en `blue`. Voor invoerwaarden kunnen niet worden geparseerd als matrices van JSON-tekenreeks, een fout geretourneerd.

#### <a name="sample-use-case"></a>Voorbeeld gebruiksvoorbeeld
Azure SQL-database beschikt niet over een ingebouwde gegevenstype dat is natuurlijk te toegewezen`Collection(Edm.String)` velden in Azure Search. toopopulate verzameling velden string formatteren van de brongegevens als een tekenreeksmatrix JSON en deze functie wilt gebruiken.

#### <a name="example"></a>Voorbeeld
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Help ons Azure Search te verbeteren
Als u functieaanvragen of suggesties voor verbeteringen hebt, kunt contact toous op onze [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).
