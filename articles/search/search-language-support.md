---
title: Taal van de meerdere Azure Search | Microsoft Docs
description: Azure Search biedt ondersteuning voor 56 talen gebruik taalanalyse van Lucene en het verwerken van natuurlijke taal-technologie van Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="4d49b-103">Een index voor documenten in meerdere talen in Azure Search maken</span><span class="sxs-lookup"><span data-stu-id="4d49b-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="4d49b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4d49b-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="4d49b-105">REST</span><span class="sxs-lookup"><span data-stu-id="4d49b-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="4d49b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="4d49b-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="4d49b-107">De kracht van taalanalyse unleashing is net zo eenvoudig als een eigenschap van de instelling voor een doorzoekbaar veld in de definitie van de index.</span><span class="sxs-lookup"><span data-stu-id="4d49b-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="4d49b-108">Nu kunt u deze stap in de portal doen.</span><span class="sxs-lookup"><span data-stu-id="4d49b-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="4d49b-109">Hieronder vindt u schermafbeeldingen van de Azure Portal-blades voor Azure Search die toestaan dat gebruikers een indexschema definiëren.</span><span class="sxs-lookup"><span data-stu-id="4d49b-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="4d49b-110">Gebruikers kunnen via deze blade alle velden maken en stel de eigenschap analyzer voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="4d49b-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d49b-111">U kunt alleen een taalanalyse ingesteld tijdens de definitie van veld als in bij het maken van een nieuwe index van de grond van of als u een nieuw veld toevoegt aan een bestaande index.</span><span class="sxs-lookup"><span data-stu-id="4d49b-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="4d49b-112">Zorg ervoor dat u alle kenmerken, zoals de analyzer tijdens het maken van het veld volledig opgeven.</span><span class="sxs-lookup"><span data-stu-id="4d49b-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="4d49b-113">Het niet mogelijk zijn de kenmerken bewerken of wijzigen van het type analyzer nadat u uw wijzigingen hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4d49b-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="4d49b-114">De velddefinitie van een nieuw definiëren</span><span class="sxs-lookup"><span data-stu-id="4d49b-114">Define a new field definition</span></span>
1. <span data-ttu-id="4d49b-115">Aanmelden bij de [Azure-portal](https://portal.azure.com) en open de service-blade van uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="4d49b-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="4d49b-116">Klik op **toevoegen index** in de opdrachtbalk aan de bovenkant van het servicedashboard start een nieuwe index of open een bestaande index om in te stellen van een analyzer op nieuwe velden die u aan een bestaande index toevoegt.</span><span class="sxs-lookup"><span data-stu-id="4d49b-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="4d49b-117">De velden blade wordt weergegeven, zodat u de opties voor het definiëren van het schema van de index, met inbegrip van het tabblad Analyzer gebruikt voor het kiezen van een taalanalyse.</span><span class="sxs-lookup"><span data-stu-id="4d49b-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="4d49b-118">In velden, start u de velddefinitie van een door een naam geven, het kiezen van het gegevenstype en instellen van kenmerken markeert het veld als volledige tekst kan worden doorzocht, worden opgehaald in de zoekresultaten, kan worden gebruikt in de navigatiestructuur facet, sorteerbaar, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="4d49b-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="4d49b-119">Voordat u doorgaat naar het volgende veld, opent u de **Analyzer** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4d49b-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="4d49b-120">![][1]
*Als u wilt een analyzer selecteert, klikt u op het tabblad Analyzer op de blade velden*</span><span class="sxs-lookup"><span data-stu-id="4d49b-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="4d49b-121">Kies een analyzer</span><span class="sxs-lookup"><span data-stu-id="4d49b-121">Choose an analyzer</span></span>
1. <span data-ttu-id="4d49b-122">Ga naar het veld dat u definieert.</span><span class="sxs-lookup"><span data-stu-id="4d49b-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="4d49b-123">Als u het veld als doorzoekbaar nog niet hebt gemarkeerd, klikt u op het selectievakje nu om verder te markeren als **doorzoekbaar**.</span><span class="sxs-lookup"><span data-stu-id="4d49b-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="4d49b-124">Klik op het gebied van de analysefunctie voor om de lijst met beschikbare analyzers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4d49b-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="4d49b-125">Kies de analyzer die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4d49b-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="4d49b-126">![][2]
*Selecteer een van de ondersteunde analyzers voor elk veld*</span><span class="sxs-lookup"><span data-stu-id="4d49b-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="4d49b-127">De doorzoekbare velden gebruikt standaard de [standaard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) welke taal networkdirect is.</span><span class="sxs-lookup"><span data-stu-id="4d49b-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="4d49b-128">De volledige lijst met ondersteunde analyzers Zie [taalondersteuning in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d49b-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="4d49b-129">Nadat de taalanalyse voor een veld is geselecteerd, wordt deze aan elke aanvraag indexeren en de zoekcriteria voor dat veld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4d49b-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="4d49b-130">Wanneer een query op basis van meerdere velden met behulp van verschillende analyzers is uitgegeven, wordt de query onafhankelijk worden verwerkt door de juiste analyzers voor elk veld.</span><span class="sxs-lookup"><span data-stu-id="4d49b-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="4d49b-131">Veel webtoepassingen en mobiele toepassingen fungeren gebruikers overal ter wereld met behulp van verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="4d49b-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="4d49b-132">Het is mogelijk voor het definiëren van een index voor een scenario als volgt door het maken van een veld voor elke taal die wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4d49b-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="4d49b-133">![][3]
*Definitie van de index met een beschrijvingsveld voor elke taal ondersteund*</span><span class="sxs-lookup"><span data-stu-id="4d49b-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="4d49b-134">Als de taal van de agent een query uitvoert bekend is, een zoekaanvraag kan worden gericht op een bepaald veld met de **searchFields** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="4d49b-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="4d49b-135">De volgende query worden uitgegeven alleen op basis van de beschrijving in pools:</span><span class="sxs-lookup"><span data-stu-id="4d49b-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="4d49b-136">U kunt uw index van de portal een query met **Search explorer** te plakken in een query die lijkt op de hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d49b-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="4d49b-137">Search explorer is beschikbaar in de opdrachtbalk in de blade van de service.</span><span class="sxs-lookup"><span data-stu-id="4d49b-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="4d49b-138">Zie [query uitvoeren op uw Azure Search-index in de portal](search-explorer.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d49b-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="4d49b-139">Soms de taal van de agent een query uitvoert niet bekend is, in welk geval de query kan worden uitgegeven op basis van alle velden tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="4d49b-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="4d49b-140">Indien nodig, de voorkeur voor de resultaten in een bepaalde taal kan worden gedefinieerd met behulp van [score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d49b-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="4d49b-141">In het onderstaande voorbeeld overeenkomsten gevonden in de beschrijving in het Engels score hoger ten opzichte van de overeenkomsten in Pools en Frans:</span><span class="sxs-lookup"><span data-stu-id="4d49b-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="4d49b-142">Als u een .NET-ontwikkelaar bent, houd er rekening mee dat u kunt configureren dat taalanalyse met behulp van de [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="4d49b-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="4d49b-143">De meest recente versie biedt ondersteuning voor de taalanalyse Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4d49b-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
