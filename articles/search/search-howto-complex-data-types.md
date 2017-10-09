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
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="860b4-103">Hoe toomodel complexe gegevenstypen in Azure Search</span><span class="sxs-lookup"><span data-stu-id="860b4-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="860b4-104">Externe gegevenssets gebruikt een Azure Search-index bevatten soms hiërarchische of geneste substructuren die niet netjes in een rijenset in tabelvorm doen uitgesplitst toopopulate.</span><span class="sxs-lookup"><span data-stu-id="860b4-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="860b4-105">Voorbeelden van dergelijke structuren mogelijk meerdere locaties en telefoonnummers omvatten voor één klant, meerdere kleuren en grootten voor een enkele SKU, meerdere auteurs van één boek, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="860b4-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="860b4-106">Voorwaarden modelleren, ziet u mogelijk deze structuren bedoelde tooas *complexe gegevenstypen*, *samengestelde gegevenstypen*, *samengestelde gegevenstypen*, of *cumulatieve gegevenstypen*, tooname een enkele.</span><span class="sxs-lookup"><span data-stu-id="860b4-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="860b4-107">Complexe gegevenstypen worden niet standaard ondersteund in Azure Search, maar een beproefde tijdelijke oplossing omvat een proces in twee stappen plat Hallo structuur en vervolgens via een **verzameling** gegevenstype tooreconstitute Hallo interior structuur.</span><span class="sxs-lookup"><span data-stu-id="860b4-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="860b4-108">Volgende Hallo techniek die wordt beschreven in dit artikel kan inhoud toobe Hallo gezocht, meervoudige, gefilterd en gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="860b4-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="860b4-109">Voorbeeld van een complexe gegevensstructuur</span><span class="sxs-lookup"><span data-stu-id="860b4-109">Example of a complex data structure</span></span>
<span data-ttu-id="860b4-110">Hallo gegevens betreffende bevindt zich doorgaans voor als een set van JSON of XML-documenten, of als items in een NoSQL-opslag, zoals Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="860b4-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="860b4-111">Hallo uitdaging komen structureel, voort van meerdere onderliggende items die toobe doorzocht en gefilterd nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="860b4-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="860b4-112">Uitvoeren als een beginpunt voor het aanduiden van tijdelijke oplossing Hallo Hallo JSON-document dat een lijst met contactpersonen als voorbeeld wordt te volgen:</span><span class="sxs-lookup"><span data-stu-id="860b4-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="860b4-113">Hoewel Hallo velden met de naam 'id', 'name' en 'bedrijf' kunnen eenvoudig worden toegewezen-op-een volgens de velden in een Azure Search-index, Hallo 'locaties' veld bevat een matrix met een set locatie-id's, evenals de beschrijvingen van de locatie-locaties.</span><span class="sxs-lookup"><span data-stu-id="860b4-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="860b4-114">Gezien het feit dat Azure Search geen een gegevenstype dat wordt ondersteund, moeten we een andere manier toomodel dit in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="860b4-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="860b4-115">Deze methode wordt ook beschreven door Kirk Evans in een blogbericht [DocumentDB met Azure Search indexeren](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), waarin een techniek die genoemd 'afvlakken Hallo gegevens', waarbij u een veld met de naam hebt `locationsID` en `locationsDescription` die geen van beide [verzamelingen](https://msdn.microsoft.com/library/azure/dn798938.aspx) (of een matrix met tekenreeksen).</span><span class="sxs-lookup"><span data-stu-id="860b4-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="860b4-116">Deel 1: Plat Hallo-matrix in afzonderlijke velden</span><span class="sxs-lookup"><span data-stu-id="860b4-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="860b4-117">een Azure Search-index die geschikt is voor deze gegevensset toocreate afzonderlijke velden voor de geneste substructure Hallo maken: `locationsID` en `locationsDescription` met het gegevenstype van [verzamelingen](https://msdn.microsoft.com/library/azure/dn798938.aspx) (of een matrix met tekenreeksen).</span><span class="sxs-lookup"><span data-stu-id="860b4-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="860b4-118">In deze velden zou u de waarden Hallo '1' en '2' index naar Hallo `locationsID` veld voor de John Smith en Hallo '3' & '4' in hello `locationsID` voor Jen Campbell veld.</span><span class="sxs-lookup"><span data-stu-id="860b4-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="860b4-119">Uw gegevens in Azure Search eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="860b4-119">Your data within Azure Search would look like this:</span></span> 

![voorbeeldgegevens, 2 rijen](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="860b4-121">Deel 2: Een verzameling veld toevoegen in de indexdefinitie Hallo</span><span class="sxs-lookup"><span data-stu-id="860b4-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="860b4-122">In het schema van de index hello uitzien Hallo velddefinities vergelijkbaar toothis voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="860b4-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="860b4-123">Zoekgedrag valideren en Hallo index uitbreiden</span><span class="sxs-lookup"><span data-stu-id="860b4-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="860b4-124">Ervan uitgaande dat u gemaakte Hallo index en geladen hello, kunt u nu testen Hallo oplossing tooverify zoeken query uitgevoerd op Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="860b4-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="860b4-125">Elke **verzameling** veld moet **doorzoekbare**, **Filterbaar** en **geschikt voor facetten**.</span><span class="sxs-lookup"><span data-stu-id="860b4-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="860b4-126">U moet kunnen toorun-query's, zoals:</span><span class="sxs-lookup"><span data-stu-id="860b4-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="860b4-127">Alle mensen die op Hallo 'Adventureworks Headquarters werken' vinden.</span><span class="sxs-lookup"><span data-stu-id="860b4-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="860b4-128">Aantal Hallo mensen in een Home Office werken ophalen.</span><span class="sxs-lookup"><span data-stu-id="860b4-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="860b4-129">Hallo mensen die op een startpagina Office werkt, laten zien welke andere kantoren ze samen met een telling van Hallo mensen in elke vestiging werken.</span><span class="sxs-lookup"><span data-stu-id="860b4-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="860b4-130">Indien deze techniek valt uit elkaar is wanneer u een zoekopdracht die zowel Hallo locatie-id, evenals een beschrijving van de locatie Hallo combineert toodo nodig.</span><span class="sxs-lookup"><span data-stu-id="860b4-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="860b4-131">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="860b4-131">For example:</span></span>

* <span data-ttu-id="860b4-132">Alle personen vinden waar ze een kantoor aan huis hebben en een locatie-ID 4 heeft.</span><span class="sxs-lookup"><span data-stu-id="860b4-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="860b4-133">Als u de oorspronkelijke inhoud Hallo opgezocht als volgt:</span><span class="sxs-lookup"><span data-stu-id="860b4-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="860b4-134">Nu dat we Hallo gegevens in afzonderlijke velden gescheiden hebben, we hebben echter geen enkele manier weten te komen of Hallo kantoor aan huis voor Jen Campbell te is gekoppeld`locationsID 3` of `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="860b4-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="860b4-135">toohandle dit geval kunt u een ander veld in Hallo-index die alle Hallo gegevens worden gecombineerd in één verzameling definiëren.</span><span class="sxs-lookup"><span data-stu-id="860b4-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="860b4-136">In ons voorbeeld noemen we dit veld `locationsCombined` en we worden gescheiden Hallo inhoud met een `||` maar u kunt scheidingsteken die u denkt dat een unieke reeks tekens voor uw inhoud zijn.</span><span class="sxs-lookup"><span data-stu-id="860b4-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="860b4-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="860b4-137">For example:</span></span> 

![voorbeeldgegevens, 2 rijen met scheidingsteken](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="860b4-139">Met deze `locationsCombined` veld we nu aankan nog meer query's, zoals:</span><span class="sxs-lookup"><span data-stu-id="860b4-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="860b4-140">Een aantal van mensen die op een 'Home kantoor' locatie-Id van '4 werken' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="860b4-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="860b4-141">Zoeken naar personen die op een startpagina Office werkt met Id '4' locatie.</span><span class="sxs-lookup"><span data-stu-id="860b4-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="860b4-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="860b4-142">Limitations</span></span>
<span data-ttu-id="860b4-143">Dit is handig voor een aantal scenario's, maar het is niet van toepassing is in elk geval.</span><span class="sxs-lookup"><span data-stu-id="860b4-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="860b4-144">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="860b4-144">For example:</span></span>

1. <span data-ttu-id="860b4-145">Als u geen een vaste set van velden in uw complex gegevenstype hebt en er geen toomap manier is typt alle Hallo mogelijke tooa één veld.</span><span class="sxs-lookup"><span data-stu-id="860b4-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="860b4-146">Een aantal extra werk toodetermine vereist Hallo geneste objecten bijwerken precies wat toobe bijgewerkt in Azure Search-index Hallo nodig heeft</span><span class="sxs-lookup"><span data-stu-id="860b4-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="860b4-147">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="860b4-147">Sample code</span></span>
<span data-ttu-id="860b4-148">U kunt een voorbeeld zien over hoe tooindex complexe JSON-gegevens ingesteld in Azure Search en een aantal query's uitvoeren via deze gegevensset op deze [GitHub-repo-](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="860b4-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="860b4-149">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="860b4-149">Next step</span></span>
<span data-ttu-id="860b4-150">[Stem voor systeemeigen ondersteuning voor complexe gegevenstypen](https://feedback.azure.com/forums/263029-azure-search) op Hallo Azure Search UserVoice pagina en eventuele aanvullende gegevens opgeven dat u graag tooconsider met betrekking tot implementatie.</span><span class="sxs-lookup"><span data-stu-id="860b4-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="860b4-151">U kunt ook bereiken toome rechtstreeks op Twitter op @liamca.</span><span class="sxs-lookup"><span data-stu-id="860b4-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

