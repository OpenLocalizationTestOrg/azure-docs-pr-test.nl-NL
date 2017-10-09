---
title: aaaAzure zoeken multi taal | Microsoft Docs
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
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="0c66e-103">Een index voor documenten in meerdere talen in Azure Search maken</span><span class="sxs-lookup"><span data-stu-id="0c66e-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="0c66e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0c66e-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="0c66e-105">REST</span><span class="sxs-lookup"><span data-stu-id="0c66e-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="0c66e-106">.NET</span><span class="sxs-lookup"><span data-stu-id="0c66e-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="0c66e-107">Unleashing hello kracht van taalanalyse is net zo eenvoudig als een eigenschap van de instelling voor een doorzoekbaar veld in de indexdefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0c66e-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="0c66e-108">Nu kunt u deze stap bij het Hallo-portal doen.</span><span class="sxs-lookup"><span data-stu-id="0c66e-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="0c66e-109">Hieronder vindt u schermopnamen van hello Azure Portal-blades voor Azure Search waarmee gebruikers toodefine een indexschema.</span><span class="sxs-lookup"><span data-stu-id="0c66e-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="0c66e-110">Gebruikers kunnen via deze blade alle Hallo velden maken en Hallo analyzer eigenschap instellen voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="0c66e-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c66e-111">U kunt alleen een taalanalyse instellen tijdens de definitie van veld, zoals in wanneer maken van een nieuwe index van Hallo gemalen, of bij het toevoegen van een nieuw veld tooan bestaande index.</span><span class="sxs-lookup"><span data-stu-id="0c66e-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="0c66e-112">Zorg ervoor dat u alle kenmerken, zoals Hallo analyzer, tijdens het maken van Hallo veld volledig opgeven.</span><span class="sxs-lookup"><span data-stu-id="0c66e-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="0c66e-113">U niet kunt tooedit zijn Hallo-kenmerken en niet Hallo analyzer type niet wijzigen wanneer u uw wijzigingen hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0c66e-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="0c66e-114">De velddefinitie van een nieuw definiëren</span><span class="sxs-lookup"><span data-stu-id="0c66e-114">Define a new field definition</span></span>
1. <span data-ttu-id="0c66e-115">Meld u aan toohello [Azure-portal](https://portal.azure.com) en open Hallo service blade van uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="0c66e-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="0c66e-116">Klik op **toevoegen index** balk Hallo Hallo service dashboard toostart bovenaan in een nieuwe index of open een bestaande index tooset een analyzer op nieuwe velden die u wilt toevoegen in Hallo opdracht tooan bestaande index.</span><span class="sxs-lookup"><span data-stu-id="0c66e-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="0c66e-117">Hallo velden blade wordt weergegeven, zodat u de opties voor het definiëren van Hallo-schema van Hallo index, waaronder Hallo Analyzer tabblad gebruikt voor het kiezen van een taalanalyse.</span><span class="sxs-lookup"><span data-stu-id="0c66e-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="0c66e-118">In velden, start u de velddefinitie van een door een naam geven, Hallo gegevenstype te kiezen en instellen van kenmerken toomark Hallo veld als de volledige tekst doorzoekbaar, worden opgehaald in de zoekresultaten, kan worden gebruikt in de navigatiestructuur facet, sorteerbaar, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="0c66e-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="0c66e-119">Voordat u doorgaat toohello volgende veld, open Hallo **Analyzer** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0c66e-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="0c66e-120">![][1]
*tooselect een analyzer, klik op Hallo Analyzer tabblad op Hallo velden blade*</span><span class="sxs-lookup"><span data-stu-id="0c66e-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="0c66e-121">Kies een analyzer</span><span class="sxs-lookup"><span data-stu-id="0c66e-121">Choose an analyzer</span></span>
1. <span data-ttu-id="0c66e-122">Schuif toofind Hallo veld definiëren.</span><span class="sxs-lookup"><span data-stu-id="0c66e-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="0c66e-123">Als u dit nog niet hebt gemarkeerd Hallo veld als doorzoekbaar, klikt u op Hallo selectievakje nu toomark als **doorzoekbaar**.</span><span class="sxs-lookup"><span data-stu-id="0c66e-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="0c66e-124">Klik op Hallo Analyzer gebied toodisplay Hallo lijst met beschikbare analyzers.</span><span class="sxs-lookup"><span data-stu-id="0c66e-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="0c66e-125">Kies Hallo analyzer gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="0c66e-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="0c66e-126">![][2]
*Selecteer een van de analyzers Hallo ondersteund voor elk veld*</span><span class="sxs-lookup"><span data-stu-id="0c66e-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="0c66e-127">Standaard gebruiken alle doorzoekbare velden Hallo [standaard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) welke taal networkdirect is.</span><span class="sxs-lookup"><span data-stu-id="0c66e-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="0c66e-128">tooview hello volledige lijst met ondersteunde analyzers, Zie [taalondersteuning in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c66e-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="0c66e-129">Nadat Hallo taalanalyse voor een veld is geselecteerd, wordt deze met elke aanvraag indexeren en de zoekcriteria voor dat veld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0c66e-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="0c66e-130">Wanneer een query op basis van meerdere velden met behulp van verschillende analyzers is uitgegeven, zullen Hallo query onafhankelijk worden verwerkt door de juiste analyzers Hallo voor elk veld.</span><span class="sxs-lookup"><span data-stu-id="0c66e-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="0c66e-131">Veel webtoepassingen en mobiele toepassingen fungeren gebruikers hele Hallo wereld met behulp van verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="0c66e-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="0c66e-132">Het is mogelijk toodefine een index voor een scenario zoals deze door het maken van een veld voor elke taal die wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0c66e-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="0c66e-133">![][3]
*Definitie van de index met een beschrijvingsveld voor elke taal ondersteund*</span><span class="sxs-lookup"><span data-stu-id="0c66e-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="0c66e-134">Als de taal Hallo van Hallo agent een query uitvoert bekend is, een zoekaanvraag bereik tooa bepaald veld met de Hallo kan worden **searchFields** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="0c66e-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="0c66e-135">Hallo worden volgende query uitgegeven alleen tegen Hallo beschrijving in pools:</span><span class="sxs-lookup"><span data-stu-id="0c66e-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="0c66e-136">U kunt uw index vanuit de portal Hallo query met **Search explorer** toopaste in een query vergelijkbare toohello melding hierboven.</span><span class="sxs-lookup"><span data-stu-id="0c66e-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="0c66e-137">Search explorer is beschikbaar in de opdrachtbalk Hallo Hallo service blade.</span><span class="sxs-lookup"><span data-stu-id="0c66e-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="0c66e-138">Zie [query uitvoeren op uw Azure Search-index in de portal Hallo](search-explorer.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0c66e-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="0c66e-139">Soms hello taal van het Hallo-agent een query uitvoert niet bekend is, in welk geval Hallo query kan worden uitgegeven op basis van alle velden tegelijkertijd.</span><span class="sxs-lookup"><span data-stu-id="0c66e-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="0c66e-140">Indien nodig, de voorkeur voor de resultaten in een bepaalde taal kan worden gedefinieerd met behulp van [score berekenen voor profielen](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c66e-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="0c66e-141">In onderstaande Hallo voorbeeld, overeenkomsten gevonden in het vak Beschrijving in het Engels Hallo hogere relatieve toomatches in Pools en Frans score:</span><span class="sxs-lookup"><span data-stu-id="0c66e-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="0c66e-142">Als u een .NET-ontwikkelaar bent, houd er rekening mee dat u met behulp van Hallo taalanalyse kunt configureren [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="0c66e-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="0c66e-143">de meest recente release Hallo biedt ondersteuning voor Hallo Microsoft taalanalyse ook.</span><span class="sxs-lookup"><span data-stu-id="0c66e-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
