---
title: aaaHow toomodel complexe gegevenstypen in Azure Search | Microsoft Docs
description: "Genest of hiërarchische gegevensstructuren kunnen worden gemodelleerd in een Azure Search-index met platte rijenset en verzamelingen gegevenstype."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Hoe toomodel complexe gegevenstypen in Azure Search
Externe gegevenssets gebruikt een Azure Search-index bevatten soms hiërarchische of geneste substructuren die niet netjes in een rijenset in tabelvorm doen uitgesplitst toopopulate. Voorbeelden van dergelijke structuren mogelijk meerdere locaties en telefoonnummers omvatten voor één klant, meerdere kleuren en grootten voor een enkele SKU, meerdere auteurs van één boek, enzovoort. Voorwaarden modelleren, ziet u mogelijk deze structuren bedoelde tooas *complexe gegevenstypen*, *samengestelde gegevenstypen*, *samengestelde gegevenstypen*, of *cumulatieve gegevenstypen*, tooname een enkele.

Complexe gegevenstypen worden niet standaard ondersteund in Azure Search, maar een beproefde tijdelijke oplossing omvat een proces in twee stappen plat Hallo structuur en vervolgens via een **verzameling** gegevenstype tooreconstitute Hallo interior structuur. Volgende Hallo techniek die wordt beschreven in dit artikel kan inhoud toobe Hallo gezocht, meervoudige, gefilterd en gesorteerd.

## <a name="example-of-a-complex-data-structure"></a>Voorbeeld van een complexe gegevensstructuur
Hallo gegevens betreffende bevindt zich doorgaans voor als een set van JSON of XML-documenten, of als items in een NoSQL-opslag, zoals Azure Cosmos DB. Hallo uitdaging komen structureel, voort van meerdere onderliggende items die toobe doorzocht en gefilterd nodig hebben.  Uitvoeren als een beginpunt voor het aanduiden van tijdelijke oplossing Hallo Hallo JSON-document dat een lijst met contactpersonen als voorbeeld wordt te volgen:

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Hoewel Hallo velden met de naam 'id', 'name' en 'bedrijf' kunnen eenvoudig worden toegewezen-op-een volgens de velden in een Azure Search-index, Hallo 'locaties' veld bevat een matrix met een set locatie-id's, evenals de beschrijvingen van de locatie-locaties. Gezien het feit dat Azure Search geen een gegevenstype dat wordt ondersteund, moeten we een andere manier toomodel dit in Azure Search. 

> [!NOTE]
> Deze methode wordt ook beschreven door Kirk Evans in een blogbericht [DocumentDB met Azure Search indexeren](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), waarin een techniek die genoemd 'afvlakken Hallo gegevens', waarbij u een veld met de naam hebt `locationsID` en `locationsDescription` die geen van beide [verzamelingen](https://msdn.microsoft.com/library/azure/dn798938.aspx) (of een matrix met tekenreeksen).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Deel 1: Plat Hallo-matrix in afzonderlijke velden
een Azure Search-index die geschikt is voor deze gegevensset toocreate afzonderlijke velden voor de geneste substructure Hallo maken: `locationsID` en `locationsDescription` met het gegevenstype van [verzamelingen](https://msdn.microsoft.com/library/azure/dn798938.aspx) (of een matrix met tekenreeksen). In deze velden zou u de waarden Hallo '1' en '2' index naar Hallo `locationsID` veld voor de John Smith en Hallo '3' & '4' in hello `locationsID` voor Jen Campbell veld.  

Uw gegevens in Azure Search eruit als volgt: 

![voorbeeldgegevens, 2 rijen](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Deel 2: Een verzameling veld toevoegen in de indexdefinitie Hallo
In het schema van de index hello uitzien Hallo velddefinities vergelijkbaar toothis voorbeeld.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Zoekgedrag valideren en Hallo index uitbreiden
Ervan uitgaande dat u gemaakte Hallo index en geladen hello, kunt u nu testen Hallo oplossing tooverify zoeken query uitgevoerd op Hallo gegevensset. Elke **verzameling** veld moet **doorzoekbare**, **Filterbaar** en **geschikt voor facetten**. U moet kunnen toorun-query's, zoals:

* Alle mensen die op Hallo 'Adventureworks Headquarters werken' vinden.
* Aantal Hallo mensen in een Home Office werken ophalen.  
* Hallo mensen die op een startpagina Office werkt, laten zien welke andere kantoren ze samen met een telling van Hallo mensen in elke vestiging werken.  

Indien deze techniek valt uit elkaar is wanneer u een zoekopdracht die zowel Hallo locatie-id, evenals een beschrijving van de locatie Hallo combineert toodo nodig. Bijvoorbeeld:

* Alle personen vinden waar ze een kantoor aan huis hebben en een locatie-ID 4 heeft.  

Als u de oorspronkelijke inhoud Hallo opgezocht als volgt:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Nu dat we Hallo gegevens in afzonderlijke velden gescheiden hebben, we hebben echter geen enkele manier weten te komen of Hallo kantoor aan huis voor Jen Campbell te is gekoppeld`locationsID 3` of `locationsID 4`.  

toohandle dit geval kunt u een ander veld in Hallo-index die alle Hallo gegevens worden gecombineerd in één verzameling definiëren.  In ons voorbeeld noemen we dit veld `locationsCombined` en we worden gescheiden Hallo inhoud met een `||` maar u kunt scheidingsteken die u denkt dat een unieke reeks tekens voor uw inhoud zijn. Bijvoorbeeld: 

![voorbeeldgegevens, 2 rijen met scheidingsteken](./media/search-howto-complex-data-types/sample-data-2.png)

Met deze `locationsCombined` veld we nu aankan nog meer query's, zoals:

* Een aantal van mensen die op een 'Home kantoor' locatie-Id van '4 werken' weergegeven.  
* Zoeken naar personen die op een startpagina Office werkt met Id '4' locatie. 

## <a name="limitations"></a>Beperkingen
Dit is handig voor een aantal scenario's, maar het is niet van toepassing is in elk geval.  Bijvoorbeeld:

1. Als u geen een vaste set van velden in uw complex gegevenstype hebt en er geen toomap manier is typt alle Hallo mogelijke tooa één veld. 
2. Een aantal extra werk toodetermine vereist Hallo geneste objecten bijwerken precies wat toobe bijgewerkt in Azure Search-index Hallo nodig heeft

## <a name="sample-code"></a>Voorbeeldcode
U kunt een voorbeeld zien over hoe tooindex complexe JSON-gegevens ingesteld in Azure Search en een aantal query's uitvoeren via deze gegevensset op deze [GitHub-repo-](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Volgende stap
[Stem voor systeemeigen ondersteuning voor complexe gegevenstypen](https://feedback.azure.com/forums/263029-azure-search) op Hallo Azure Search UserVoice pagina en eventuele aanvullende gegevens opgeven dat u graag tooconsider met betrekking tot implementatie. U kunt ook bereiken toome rechtstreeks op Twitter op @liamca.

