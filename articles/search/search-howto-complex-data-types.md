---
title: Het model van complexe gegevenstypen in Azure Search | Microsoft Docs
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
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="08b11-103">Het model complexe gegevenstypen in Azure Search</span><span class="sxs-lookup"><span data-stu-id="08b11-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="08b11-104">Externe gegevenssets die worden gebruikt voor het vullen van een Azure Search-index soms bevatten hiërarchische of geneste substructuren die niet netjes in een rijenset in tabelvorm doen uitgesplitst.</span><span class="sxs-lookup"><span data-stu-id="08b11-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="08b11-105">Voorbeelden van dergelijke structuren mogelijk meerdere locaties en telefoonnummers omvatten voor één klant, meerdere kleuren en grootten voor een enkele SKU, meerdere auteurs van één boek, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="08b11-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="08b11-106">Voorwaarden modelleren, ziet u mogelijk deze aangeduid als structuren *complexe gegevenstypen*, *samengestelde gegevenstypen*, *samengestelde gegevenstypen*, of *gegevenstypen cumulatieve*, enz.</span><span class="sxs-lookup"><span data-stu-id="08b11-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="08b11-107">Complexe gegevenstypen worden niet standaard ondersteund in Azure Search, maar een beproefde tijdelijke oplossing omvat een proces in twee stappen van de structuur plat en vervolgens via een **verzameling** gegevenstype voor de interior structuur opnieuw samenstellen.</span><span class="sxs-lookup"><span data-stu-id="08b11-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="08b11-108">Na de techniek die wordt beschreven in dit artikel kan de inhoud die moet worden doorzocht, meervoudige, gefilterd en gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="08b11-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="08b11-109">Voorbeeld van een complexe gegevensstructuur</span><span class="sxs-lookup"><span data-stu-id="08b11-109">Example of a complex data structure</span></span>
<span data-ttu-id="08b11-110">De betrokken gegevens bevindt zich doorgaans voor als een set van JSON of XML-documenten, of als items in een NoSQL-opslag, zoals Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="08b11-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="08b11-111">De uitdaging komen structureel, voort van het hebben van meerdere onderliggende items die moeten worden doorzocht en gefilterd.</span><span class="sxs-lookup"><span data-stu-id="08b11-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="08b11-112">Neem de volgende JSON-document dat een lijst met contactpersonen als voorbeeld wordt als een beginpunt voor het aanduiden van de tijdelijke oplossing:</span><span class="sxs-lookup"><span data-stu-id="08b11-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="08b11-113">Hoewel de velden met de naam 'id', 'name' en 'bedrijf' kunnen eenvoudig worden toegewezen-op-een volgens de velden in een Azure Search-index, het veld 'locaties' bevat een matrix met een set locatie-id's, evenals de beschrijvingen van de locatie-locaties.</span><span class="sxs-lookup"><span data-stu-id="08b11-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="08b11-114">Gezien het feit dat Azure Search geen een gegevenstype dat wordt ondersteund, moeten we een andere manier om dit te modelleren in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="08b11-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="08b11-115">Deze methode wordt ook beschreven door Kirk Evans in een blogbericht [DocumentDB met Azure Search indexeren](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), waarin een techniek die genoemd 'plat de gegevens', waarbij u een veld met de naam hebt `locationsID` en `locationsDescription` die geen van beide [verzamelingen](https://msdn.microsoft.com/library/azure/dn798938.aspx) (of een matrix met tekenreeksen).</span><span class="sxs-lookup"><span data-stu-id="08b11-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="08b11-116">Deel 1: De matrix plat in afzonderlijke velden</span><span class="sxs-lookup"><span data-stu-id="08b11-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="08b11-117">Voor het maken van een Azure Search-index die geschikt is voor deze gegevensset, maakt u afzonderlijke velden voor de geneste substructure: `locationsID` en `locationsDescription` met het gegevenstype van [verzamelingen](https://msdn.microsoft.com/library/azure/dn798938.aspx) (of een matrix met tekenreeksen).</span><span class="sxs-lookup"><span data-stu-id="08b11-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="08b11-118">In deze velden zou u de waarden '1' en '2' index naar de `locationsID` veld voor John Smith en de waarden '3' & '4' in de `locationsID` voor Jen Campbell veld.</span><span class="sxs-lookup"><span data-stu-id="08b11-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="08b11-119">Uw gegevens in Azure Search eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="08b11-119">Your data within Azure Search would look like this:</span></span> 

![voorbeeldgegevens, 2 rijen](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="08b11-121">Deel 2: Een verzameling veld toevoegen in de indexdefinitie</span><span class="sxs-lookup"><span data-stu-id="08b11-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="08b11-122">In het schema van de index eruit de velddefinities als in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="08b11-122">In the index schema, the field definitions might look similar to this example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="08b11-123">Zoekgedrag valideren en de index uitbreiden</span><span class="sxs-lookup"><span data-stu-id="08b11-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="08b11-124">Ervan uitgaande dat u hebt gemaakt van de index en de gegevens geladen, test u de oplossing om te controleren of de queryuitvoering zoeken op basis van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="08b11-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="08b11-125">Elke **verzameling** veld moet **doorzoekbare**, **Filterbaar** en **geschikt voor facetten**.</span><span class="sxs-lookup"><span data-stu-id="08b11-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="08b11-126">U moet uitvoeren van query's zoals:</span><span class="sxs-lookup"><span data-stu-id="08b11-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="08b11-127">Alle mensen die in het hoofdkantoor van het Adventureworks werken vinden.</span><span class="sxs-lookup"><span data-stu-id="08b11-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="08b11-128">Haal een telling van het aantal mensen die in een Home Office werken.</span><span class="sxs-lookup"><span data-stu-id="08b11-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="08b11-129">Weergeven van de personen die op een startpagina Office werkt, welke andere kantoren ze samen met een telling van de personen die u in elke vestiging werken.</span><span class="sxs-lookup"><span data-stu-id="08b11-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="08b11-130">Indien deze techniek valt uit elkaar is wanneer u wilt een zoekopdracht die zowel de locatie-id als de beschrijving van de locatie combineert.</span><span class="sxs-lookup"><span data-stu-id="08b11-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="08b11-131">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08b11-131">For example:</span></span>

* <span data-ttu-id="08b11-132">Alle personen vinden waar ze een kantoor aan huis hebben en een locatie-ID 4 heeft.</span><span class="sxs-lookup"><span data-stu-id="08b11-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="08b11-133">Als u de oorspronkelijke inhoud opgezocht als volgt:</span><span class="sxs-lookup"><span data-stu-id="08b11-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="08b11-134">Echter, nu dat we de gegevens in afzonderlijke velden gescheiden hebben, we hebben geen manier omdat u weet dat als de Home Office voor Jen Campbell is gekoppeld aan `locationsID 3` of `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="08b11-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="08b11-135">Definieer een ander veld in de index waarin alle gegevens worden gecombineerd in één verzameling voor de verwerking van deze aanvraag.</span><span class="sxs-lookup"><span data-stu-id="08b11-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="08b11-136">In ons voorbeeld noemen we dit veld `locationsCombined` en we zullen de inhoud met afzonderlijke een `||` maar u kunt scheidingsteken die u denkt dat een unieke reeks tekens voor uw inhoud zijn.</span><span class="sxs-lookup"><span data-stu-id="08b11-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="08b11-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08b11-137">For example:</span></span> 

![voorbeeldgegevens, 2 rijen met scheidingsteken](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="08b11-139">Met deze `locationsCombined` veld we nu aankan nog meer query's, zoals:</span><span class="sxs-lookup"><span data-stu-id="08b11-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="08b11-140">Een aantal van mensen die op een 'Home kantoor' locatie-Id van '4 werken' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08b11-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="08b11-141">Zoeken naar personen die op een startpagina Office werkt met Id '4' locatie.</span><span class="sxs-lookup"><span data-stu-id="08b11-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="08b11-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="08b11-142">Limitations</span></span>
<span data-ttu-id="08b11-143">Dit is handig voor een aantal scenario's, maar het is niet van toepassing is in elk geval.</span><span class="sxs-lookup"><span data-stu-id="08b11-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="08b11-144">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="08b11-144">For example:</span></span>

1. <span data-ttu-id="08b11-145">Als u geen een vaste set van velden in uw complex gegevenstype hebt en er kon geen enkele manier de mogelijke typen worden toegewezen aan één veld.</span><span class="sxs-lookup"><span data-stu-id="08b11-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="08b11-146">Bijwerken van de geneste objecten vereist extra bewerkingen uitvoeren om te bepalen wat moet exact worden bijgewerkt in de Azure Search-index</span><span class="sxs-lookup"><span data-stu-id="08b11-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="08b11-147">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="08b11-147">Sample code</span></span>
<span data-ttu-id="08b11-148">U kunt een voorbeeld zien over het een complexe verzameling van de JSON-gegevens in Azure Search-index en een aantal query's uitvoeren via deze gegevensset op deze [GitHub-repo-](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="08b11-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="08b11-149">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="08b11-149">Next step</span></span>
<span data-ttu-id="08b11-150">[Stem voor systeemeigen ondersteuning voor complexe gegevenstypen](https://feedback.azure.com/forums/263029-azure-search) pagina op de Azure Search UserVoice en eventuele aanvullende gegevens die u graag in overweging moet nemen met betrekking tot uitvoering van de functie opgeven.</span><span class="sxs-lookup"><span data-stu-id="08b11-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="08b11-151">U kunt ook bereiken mij rechtstreeks op Twitter op @liamca.</span><span class="sxs-lookup"><span data-stu-id="08b11-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

