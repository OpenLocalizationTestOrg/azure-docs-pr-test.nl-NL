---
title: aaaUpgrading toohello Azure Search .NET SDK versie 1.1 | Microsoft Docs
description: Een upgrade toohello Azure Search .NET SDK versie 1.1
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="d4bca-103">Een upgrade toohello Azure Search .NET SDK versie 3</span><span class="sxs-lookup"><span data-stu-id="d4bca-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="d4bca-104">Als u versie 2.0 preview of oudere Hallo [Azure Search .NET SDK](https://aka.ms/search-sdk), dit artikel helpt u bij het bijwerken van uw toepassing toouse versie 3.</span><span class="sxs-lookup"><span data-stu-id="d4bca-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="d4bca-105">Zie voor een meer algemene overzicht Hallo SDK inclusief voorbeelden [hoe toouse Azure zoeken vanuit een .NET-toepassing](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d4bca-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="d4bca-106">Versie 3 van hello Azure Search .NET SDK bevat een aantal wijzigingen uit eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="d4bca-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="d4bca-107">Dit zijn vooral kleine, zodat u uw code wijzigt, moet alleen minimale inspanning nodig.</span><span class="sxs-lookup"><span data-stu-id="d4bca-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="d4bca-108">Zie [stappen tooupgrade](#UpgradeSteps) voor instructies over het toochange uw code toouse Hallo nieuwe SDK-versie.</span><span class="sxs-lookup"><span data-stu-id="d4bca-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="d4bca-109">Als u versie 1.0.2-preview of ouder, u moet eerst tooversion 1.1 upgraden en vervolgens bijwerken tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="d4bca-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="d4bca-110">Zie [bijlage: stappen tooupgrade tooversion 1.1](#UpgradeStepsV1) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="d4bca-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="d4bca-111">Verschillende versies van de REST-API, met inbegrip van de meest recente Hallo biedt ondersteuning voor uw Azure Search-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d4bca-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="d4bca-112">Wanneer deze niet langer Hallo recentste is, maar het is raadzaam dat u de nieuwste versie van code toouse Hallo migreert, kunt u een versie toouse blijven.</span><span class="sxs-lookup"><span data-stu-id="d4bca-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="d4bca-113">Wanneer u Hallo REST-API gebruikt, moet u Hallo API-versie opgeven in elke aanvraag via Hallo api-versie-parameter.</span><span class="sxs-lookup"><span data-stu-id="d4bca-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="d4bca-114">Wanneer u Hallo .NET SDK, bepaalt Hallo-versie van Hallo SDK u de desbetreffende versie Hallo Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="d4bca-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="d4bca-115">Als u een oudere SDK gebruikt, kunt u blijven toorun die code zonder wijzigingen als Hallo service bijgewerkte toosupport een nieuwere API-versie.</span><span class="sxs-lookup"><span data-stu-id="d4bca-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="d4bca-116">Wat is er nieuw in versie 3</span><span class="sxs-lookup"><span data-stu-id="d4bca-116">What's new in version 3</span></span>
<span data-ttu-id="d4bca-117">Versie 3 hello Azure Search .NET SDK doelen Hallo laatste algemeen beschikbaar versie van hello Azure Search REST API specifiek 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="d4bca-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="d4bca-118">Dit maakt het mogelijk toouse vele nieuwe functies van Azure Search vanuit een .NET-toepassing, waaronder de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4bca-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="d4bca-119">Analysevoorzieningen aanpassen</span><span class="sxs-lookup"><span data-stu-id="d4bca-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="d4bca-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) en [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeerfunctie-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="d4bca-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="d4bca-121">Aanpassing van de indexeerfunctie via [veld toewijzingen](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="d4bca-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="d4bca-122">ETags ondersteuning voor het tooenable veilige gelijktijdige bijwerken van definities, Indexeerfuncties en gegevensbronnen van index</span><span class="sxs-lookup"><span data-stu-id="d4bca-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="d4bca-123">Ondersteuning voor het bouwen van de index velddefinities declaratief door uw modelklasse versieren en Hallo nieuwe `FieldBuilder` klasse.</span><span class="sxs-lookup"><span data-stu-id="d4bca-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="d4bca-124">Ondersteuning voor .NET Core en draagbare .NET-profiel 111</span><span class="sxs-lookup"><span data-stu-id="d4bca-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="d4bca-125">Stappen tooupgrade</span><span class="sxs-lookup"><span data-stu-id="d4bca-125">Steps tooupgrade</span></span>
<span data-ttu-id="d4bca-126">Eerst uw NuGet-verwijzing voor bijwerken `Microsoft.Azure.Search` beide Hallo NuGet Package Manager-Console of door met de rechtermuisknop op uw projectverwijzingen te selecteren 'Beheren NuGet-pakketten...' in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4bca-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="d4bca-127">Zodra de NuGet heeft nieuwe hello-pakketten en afhankelijkheden zijn gedownload, opnieuw worden opgebouwd uw project.</span><span class="sxs-lookup"><span data-stu-id="d4bca-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="d4bca-128">Afhankelijk van hoe uw code is gestructureerd, deze mogelijk opnieuw worden opgebouwd is.</span><span class="sxs-lookup"><span data-stu-id="d4bca-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="d4bca-129">Als dit het geval is, bent u klaar toogo!</span><span class="sxs-lookup"><span data-stu-id="d4bca-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="d4bca-130">Als uw build is mislukt, kunt u een opbouwfout Hallo volgende moeten zien:</span><span class="sxs-lookup"><span data-stu-id="d4bca-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="d4bca-131">de volgende stap Hallo toofix is deze build-fout.</span><span class="sxs-lookup"><span data-stu-id="d4bca-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="d4bca-132">Zie [wijzigingen op te splitsen in versie 3](#ListOfChanges) voor meer informatie over wat Hallo-fout veroorzaakt en hoe toofix deze.</span><span class="sxs-lookup"><span data-stu-id="d4bca-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="d4bca-133">Mogelijk ziet u extra build waarschuwingen gerelateerde tooobsolete methoden of eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="d4bca-134">Hallo waarschuwingen bevat instructies over welke toouse in plaats daarvan Hallo functie afgeschafte.</span><span class="sxs-lookup"><span data-stu-id="d4bca-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="d4bca-135">Bijvoorbeeld, als uw toepassing gebruikt Hallo `IndexingParameters.Base64EncodeKeys` eigenschap, krijgt u een waarschuwing dat`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="d4bca-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="d4bca-136">Als u eventuele fouten in de build hebt opgelost, kunt u wijzigingen aanbrengen tooyour toepassing tootake profiteren van nieuwe functionaliteit als u wenst.</span><span class="sxs-lookup"><span data-stu-id="d4bca-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="d4bca-137">Nieuwe functies in Hallo SDK worden beschreven in [wat is er nieuw in versie 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="d4bca-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="d4bca-138">Wijzigingen op te splitsen in versie 3</span><span class="sxs-lookup"><span data-stu-id="d4bca-138">Breaking changes in version 3</span></span>
<span data-ttu-id="d4bca-139">Er wijzigingen een klein aantal grote wijzigingen in versie 3 waarvoor code bovendien toorebuilding uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d4bca-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="d4bca-140">Het retourtype Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="d4bca-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="d4bca-141">Hallo `Indexes.GetClient` methode heeft een nieuwe retourtype.</span><span class="sxs-lookup"><span data-stu-id="d4bca-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="d4bca-142">Voorheen geretourneerd `SearchIndexClient`, maar dit is te wijzigen`ISearchIndexClient` in preview-versie 2.0 en die wijziging weerspiegelt tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="d4bca-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="d4bca-143">Dit is toosupport klanten die toomock Hallo willen `GetClient` methode voor de eenheidstests door te retourneren van een mock-implementatie van `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="d4bca-144">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-144">Example</span></span>
<span data-ttu-id="d4bca-145">Als uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="d4bca-146">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="d4bca-147">AnalyzerName, gegevenstype en andere zijn niet langer impliciet converteerbare toostrings</span><span class="sxs-lookup"><span data-stu-id="d4bca-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="d4bca-148">Er zijn vele typen in hello Azure Search .NET SDK, die zijn afgeleid van `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="d4bca-149">Eerder deze typen zijn alle impliciet converteerbare tootype `string`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="d4bca-150">Echter een probleem is gedetecteerd op Hallo `Object.Equals` implementatie voor deze klassen en corrigeren Hallo bug vereist deze impliciete conversie uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="d4bca-151">Expliciete conversie te`string` is wel toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d4bca-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="d4bca-152">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-152">Example</span></span>
<span data-ttu-id="d4bca-153">Als uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="d4bca-154">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="d4bca-155">Verouderd leden verwijderd</span><span class="sxs-lookup"><span data-stu-id="d4bca-155">Removed obsolete members</span></span>

<span data-ttu-id="d4bca-156">Mogelijk ziet u eigenschappen die zijn gemarkeerd als verouderd in de preview-versie 2.0 en daarna zijn verwijderd in versie 3 of build fouten gerelateerde toomethods.</span><span class="sxs-lookup"><span data-stu-id="d4bca-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="d4bca-157">Als u dergelijke fouten optreden, wordt hier hoe tooresolve ze:</span><span class="sxs-lookup"><span data-stu-id="d4bca-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="d4bca-158">Als u deze constructor: `ScoringParameter(string name, string value)`, gebruik in plaats daarvan deze:`ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="d4bca-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="d4bca-159">Als u eerder Hallo `ScoringParameter.Value` eigenschap, gebruik Hallo `ScoringParameter.Values` eigenschap of Hallo `ToString` methode in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d4bca-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="d4bca-160">Als u eerder Hallo `SearchRequestOptions.RequestId` eigenschap, gebruik Hallo `ClientRequestId` eigenschap in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d4bca-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="d4bca-161">Verwijderde preview-functies</span><span class="sxs-lookup"><span data-stu-id="d4bca-161">Removed preview features</span></span>

<span data-ttu-id="d4bca-162">Als u een van versie 2.0 preview tooversion 3 upgrade, worden op de hoogte dat JSON en CSV-ondersteuning voor Blob indexeerfuncties parseren is verwijderd omdat deze functies zijn nog steeds in preview.</span><span class="sxs-lookup"><span data-stu-id="d4bca-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="d4bca-163">In het bijzonder Hallo volgende methoden Hallo `IndexingParametersExtensions` klasse zijn verwijderd:</span><span class="sxs-lookup"><span data-stu-id="d4bca-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="d4bca-164">Als uw toepassing een vaste afhankelijkheid van deze functies heeft, zich u niet kunnen tooupgrade tooversion 3 Hallo Azure Search .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d4bca-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="d4bca-165">U kunt blijven toouse versie 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="d4bca-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="d4bca-166">Echter, neem Houd rekening met het **we raden niet met behulp van voorbeeld SDK's in productietoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d4bca-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="d4bca-167">Preview-functies voor evaluatie alleen zijn en kunnen worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d4bca-168">Conclusie</span><span class="sxs-lookup"><span data-stu-id="d4bca-168">Conclusion</span></span>
<span data-ttu-id="d4bca-169">Als u meer informatie over het gebruik van Azure Search .NET SDK Hallo nodig hebt, raadpleegt u onze onlangs bijgewerkt [How-to](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d4bca-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="d4bca-170">Uw feedback is Welkom op Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="d4bca-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="d4bca-171">Als u problemen ondervindt, kunt u gratis tooask ons voor hulp bij het Hallo [Azure Search MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="d4bca-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="d4bca-172">Als u een bug vinden, kunt u een probleem bestanden per Hallo [Azure .NET SDK GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="d4bca-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="d4bca-173">Zorg ervoor dat tooprefix de titel van uw probleem met ' Search SDK: '.</span><span class="sxs-lookup"><span data-stu-id="d4bca-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="d4bca-174">Hartelijk dank voor het gebruik van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d4bca-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="d4bca-175">Bijlage: Stappen tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="d4bca-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="d4bca-176">Deze sectie geldt alleen toousers van hello Azure Search .NET SDK versie 1.0.2-preview en ouder.</span><span class="sxs-lookup"><span data-stu-id="d4bca-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="d4bca-177">Eerst uw NuGet-verwijzing voor bijwerken `Microsoft.Azure.Search` beide Hallo NuGet Package Manager-Console of door met de rechtermuisknop op uw projectverwijzingen te selecteren 'Beheren NuGet-pakketten...' in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4bca-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="d4bca-178">Zodra de NuGet heeft nieuwe hello-pakketten en afhankelijkheden zijn gedownload, opnieuw worden opgebouwd uw project.</span><span class="sxs-lookup"><span data-stu-id="d4bca-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="d4bca-179">Als u eerder met versie 1.0.0-preview, 1.0.1-preview of 1.0.2-preview, Hallo build moet slagen en u bent klaar toogo!</span><span class="sxs-lookup"><span data-stu-id="d4bca-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="d4bca-180">Als u eerder versie 0.13.0-preview of ouder, ziet u fouten Hallo volgende maken:</span><span class="sxs-lookup"><span data-stu-id="d4bca-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="d4bca-181">de volgende stap Hallo is fouten in de build toofix Hallo één voor één.</span><span class="sxs-lookup"><span data-stu-id="d4bca-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="d4bca-182">De meeste moeten sommige klasse en methode namen die zijn gewijzigd in Hallo SDK wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="d4bca-183">[Lijst met wijzigingen op te splitsen in versie 1.1](#ListOfChangesV1) bevat een overzicht van deze wijzigingen in de naam.</span><span class="sxs-lookup"><span data-stu-id="d4bca-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="d4bca-184">Als u aangepaste klassen toomodel uw documenten en deze klassen eigenschappen met niet-nullbare primitieve typen hebben (bijvoorbeeld `int` of `bool` in C#), er is een fix bug in Hallo 1.1-versie van Hallo-SDK van waarmee u houden moet rekening.</span><span class="sxs-lookup"><span data-stu-id="d4bca-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="d4bca-185">Zie [oplossingen voor problemen in versie 1.1](#BugFixesV1) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d4bca-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="d4bca-186">Ten slotte, als u eventuele fouten in de build hebt opgelost, kunt u wijzigingen aanbrengen tooyour toepassing tootake profiteren van nieuwe functionaliteit als u wenst.</span><span class="sxs-lookup"><span data-stu-id="d4bca-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="d4bca-187">Lijst met wijzigingen op te splitsen in versie 1.1</span><span class="sxs-lookup"><span data-stu-id="d4bca-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="d4bca-188">Hallo is hieronder geordend op Hallo kans dat Hallo wijziging invloed is op uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="d4bca-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="d4bca-189">Wijzigingen in IndexBatch en IndexAction</span><span class="sxs-lookup"><span data-stu-id="d4bca-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="d4bca-190">`IndexBatch.Create`de naam is gewijzigd te`IndexBatch.New` en niet langer heeft een `params` argument.</span><span class="sxs-lookup"><span data-stu-id="d4bca-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="d4bca-191">U kunt `IndexBatch.New` voor batches die een mix van verschillende soorten acties (samenvoegingen, verwijderingen, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="d4bca-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="d4bca-192">Bovendien, er zijn nieuwe statische methoden voor het maken van batches waar alle Hallo acties zijn Hallo dezelfde: `Delete`, `Merge`, `MergeOrUpload`, en `Upload`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="d4bca-193">`IndexAction`Openbare constructors beschikt niet langer over en de eigenschappen zijn nu niet-wijzigbaar.</span><span class="sxs-lookup"><span data-stu-id="d4bca-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="d4bca-194">U moet Hallo nieuwe statische methoden gebruiken voor het maken van acties voor verschillende doeleinden: `Delete`, `Merge`, `MergeOrUpload`, en `Upload`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="d4bca-195">`IndexAction.Create`is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="d4bca-196">Als u Hallo overbelasting waarvoor alleen een document hebt gebruikt, moet u ervoor toouse `Upload` in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d4bca-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="d4bca-197">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-197">Example</span></span>
<span data-ttu-id="d4bca-198">Als uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="d4bca-199">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="d4bca-200">Als u wilt, kunt u verder vereenvoudigen het toothis:</span><span class="sxs-lookup"><span data-stu-id="d4bca-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="d4bca-201">IndexBatchException wijzigingen</span><span class="sxs-lookup"><span data-stu-id="d4bca-201">IndexBatchException changes</span></span>
<span data-ttu-id="d4bca-202">Hallo `IndexBatchException.IndexResponse` eigenschap heeft gekregen te`IndexingResults`, en het type is nu `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="d4bca-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-203">Example</span></span>
<span data-ttu-id="d4bca-204">Als uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="d4bca-205">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="d4bca-206">Bewerking methode wijzigingen</span><span class="sxs-lookup"><span data-stu-id="d4bca-206">Operation method changes</span></span>
<span data-ttu-id="d4bca-207">Elke bewerking in hello Azure Search .NET SDK is beschikbaar als een set van methode overloads voor synchrone en asynchrone aanroepfuncties.</span><span class="sxs-lookup"><span data-stu-id="d4bca-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="d4bca-208">Hallo is handtekeningen en waarbij van de overloads van deze methode gewijzigd in versie 1.1.</span><span class="sxs-lookup"><span data-stu-id="d4bca-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="d4bca-209">Hallo 'indexstatistieken ophalen'-bewerking in oudere versies van Hallo SDK blootgesteld bijvoorbeeld deze handtekeningen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="d4bca-210">In `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="d4bca-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="d4bca-211">In `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="d4bca-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="d4bca-212">Hallo methode handtekeningen voor Hallo dezelfde bewerking in versie 1.1 zien er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="d4bca-213">In `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="d4bca-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="d4bca-214">In `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="d4bca-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="d4bca-215">Vanaf versie 1.1 ordent hello Azure Search .NET SDK bewerking methoden anders:</span><span class="sxs-lookup"><span data-stu-id="d4bca-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="d4bca-216">Optionele parameters zijn nu gemodelleerd als parameters in plaats daarvan standaard dan aanvullende methode overloads.</span><span class="sxs-lookup"><span data-stu-id="d4bca-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="d4bca-217">Hierdoor Hallo aantal methode overloads, soms aanzienlijk wordt gereduceerd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="d4bca-218">Hallo uitbreidingsmethoden verbergen nu een groot aantal Hallo overbodige details van HTTP van Hallo aanroeper.</span><span class="sxs-lookup"><span data-stu-id="d4bca-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="d4bca-219">Bijvoorbeeld, oudere versies van Hallo SDK een antwoordobject met een HTTP-statuscode die u vaak een geretourneerd toocheck niet nodig omdat bewerking methoden throw `CloudException` voor elke statuscode die een fout aangeeft.</span><span class="sxs-lookup"><span data-stu-id="d4bca-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="d4bca-220">nieuwe uitbreiding methoden NET return modelobjecten Hallo, Hallo niet meer toounwrap hoeft op te slaan u ze in uw code.</span><span class="sxs-lookup"><span data-stu-id="d4bca-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="d4bca-221">Als u daarentegen tonen hello core interfaces nu methoden waarmee u meer controle op Hallo HTTP niveau als u deze nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="d4bca-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="d4bca-222">U kunt nu doorgeven in aangepaste HTTP-headers toobe opgenomen in aanvragen en nieuwe Hallo `AzureOperationResponse<T>` retourneren type biedt u directe toegang toohello `HttpRequestMessage` en `HttpResponseMessage` voor Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="d4bca-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="d4bca-223">`AzureOperationResponse`is gedefinieerd in Hallo `Microsoft.Rest.Azure` naamruimte en vervangt `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="d4bca-224">ScoringParameters wijzigingen</span><span class="sxs-lookup"><span data-stu-id="d4bca-224">ScoringParameters changes</span></span>
<span data-ttu-id="d4bca-225">Een nieuwe klasse met de naam `ScoringParameter` is toegevoegd in de nieuwste SDK toomake Hallo eenvoudiger tooprovide parameters tooscoring profielen in een zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="d4bca-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="d4bca-226">Eerder Hallo `ScoringProfiles` eigenschap Hallo `SearchParameters` klasse was getypeerd als `IList<string>`; Nu het is getypeerd als `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="d4bca-227">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-227">Example</span></span>
<span data-ttu-id="d4bca-228">Als uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="d4bca-229">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="d4bca-230">Wijzigingen in het gegevensmodel klasse</span><span class="sxs-lookup"><span data-stu-id="d4bca-230">Model class changes</span></span>
<span data-ttu-id="d4bca-231">Vervaldatum toohello handtekening wijzigingen beschreven in [bewerking methode wijzigingen](#OperationMethodChanges), veel klassen in Hallo `Microsoft.Azure.Search.Models` naamruimte hebt gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="d4bca-232">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d4bca-232">For example:</span></span>

* <span data-ttu-id="d4bca-233">`IndexDefinitionResponse`is vervangen door`AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="d4bca-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="d4bca-234">`DocumentSearchResponse`naam te is gewijzigd`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="d4bca-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="d4bca-235">`IndexResult`naam te is gewijzigd`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="d4bca-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="d4bca-236">`Documents.Count()`nu retourneert een `long` met Hallo document telling in plaats van een`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="d4bca-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="d4bca-237">`IndexGetStatisticsResponse`naam te is gewijzigd`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="d4bca-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="d4bca-238">`IndexListResponse`naam te is gewijzigd`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="d4bca-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="d4bca-239">toosummarize, `OperationResponse`-afgeleide klassen die beschikbaar waren alleen toowrap een modelobject zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="d4bca-240">Hallo resterende klassen hebben gehad hun achtervoegsel gewijzigd van `Response` te`Result`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="d4bca-241">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-241">Example</span></span>
<span data-ttu-id="d4bca-242">Als uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="d4bca-243">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="d4bca-244">Antwoord klassen en IEnumerable</span><span class="sxs-lookup"><span data-stu-id="d4bca-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="d4bca-245">Een aanvullende wijzigen die invloed kan zijn op uw code is dat antwoord-klassen die verzamelingen houdt niet langer implementeren `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="d4bca-246">In plaats daarvan kunt u de verzamelingseigenschap Hallo rechtstreeks openen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="d4bca-247">Als bijvoorbeeld uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="d4bca-248">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="d4bca-249">Speciaal geval voor webtoepassingen</span><span class="sxs-lookup"><span data-stu-id="d4bca-249">Special case for web applications</span></span>
<span data-ttu-id="d4bca-250">Als u een webtoepassing die serialiseert `DocumentSearchResponse` direct toosend toohello browser zoekresultaten, moet u toochange uw code of Hallo resultaten niet correct worden geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="d4bca-251">Als bijvoorbeeld uw code ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="d4bca-252">U kunt dit wijzigen door Hallo `.Results` eigenschap van Hallo zoeken antwoord toofix zoeken resultaat rendering:</span><span class="sxs-lookup"><span data-stu-id="d4bca-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="d4bca-253">Hebt u toolook voor dergelijke gevallen in uw code zelf; **Hallo compiler wordt geen waarschuwing** omdat `JsonResult.Data` is van het type `object`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="d4bca-254">CloudException wijzigingen</span><span class="sxs-lookup"><span data-stu-id="d4bca-254">CloudException changes</span></span>
<span data-ttu-id="d4bca-255">Hallo `CloudException` klasse is verplaatst van Hallo `Hyak.Common` naamruimte toohello `Microsoft.Rest.Azure` naamruimte.</span><span class="sxs-lookup"><span data-stu-id="d4bca-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="d4bca-256">Ook de `Error` eigenschap heeft gekregen te`Body`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="d4bca-257">Wijzigingen in SearchServiceClient en SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="d4bca-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="d4bca-258">type Hallo Hallo `Credentials` eigenschap is gewijzigd van `SearchCredentials` tooits basisklasse `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="d4bca-259">Als u nodig hebt tooaccess hello `SearchCredentials` van een `SearchIndexClient` of `SearchServiceClient`, gebruik Hallo nieuwe `SearchCredentials` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d4bca-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="d4bca-260">In oudere versies van Hallo SDK, `SearchServiceClient` en `SearchIndexClient` had constructors die een `HttpClient` parameter.</span><span class="sxs-lookup"><span data-stu-id="d4bca-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="d4bca-261">Deze zijn vervangen door een constructors die een `HttpClientHandler` en een matrix van `DelegatingHandler` objecten.</span><span class="sxs-lookup"><span data-stu-id="d4bca-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="d4bca-262">Dit maakt het eenvoudiger tooinstall aangepaste handlers toopre proces HTTP-aanvragen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="d4bca-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="d4bca-263">Ten slotte Hallo constructors die een `Uri` en `SearchCredentials` zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="d4bca-264">Bijvoorbeeld, als er een code die er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="d4bca-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="d4bca-265">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="d4bca-266">Ook opmerking dat Hallo Hallo type parameter referenties te is gewijzigd`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="d4bca-267">Dit is waarschijnlijk niet tooaffect uw code sinds `SearchCredentials` is afgeleid van `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="d4bca-268">Een aanvraag-ID doorgeven</span><span class="sxs-lookup"><span data-stu-id="d4bca-268">Passing a request ID</span></span>
<span data-ttu-id="d4bca-269">In oudere versies van Hallo SDK kan stelt u een aanvraag-ID op Hallo `SearchServiceClient` of `SearchIndexClient` en zou worden opgenomen in elke aanvraag toohello REST-API.</span><span class="sxs-lookup"><span data-stu-id="d4bca-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="d4bca-270">Dit is handig voor het oplossen van problemen met uw search-service als u toocontact ondersteuning nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="d4bca-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="d4bca-271">Het is echter nuttiger tooset een unieke aanvraag-ID voor elke bewerking in plaats van toouse Hallo dezelfde ID voor alle bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="d4bca-272">Om deze reden Hallo `SetClientRequestId` methoden van `SearchServiceClient` en `SearchIndexClient` zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d4bca-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="d4bca-273">In plaats daarvan kunt u doorgeven een aanvraag-ID tooeach bewerkingsmethode via Hallo optionele `SearchRequestOptions` parameter.</span><span class="sxs-lookup"><span data-stu-id="d4bca-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="d4bca-274">In een toekomstige release Hallo SDK wordt er een nieuw mechanisme voor het instellen van een aanvraag-ID globaal op Hallo client objecten die consistent zijn met de Hallo benadering die wordt gebruikt door andere Azure-SDK toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="d4bca-275">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d4bca-275">Example</span></span>
<span data-ttu-id="d4bca-276">Als u hebt de code die er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="d4bca-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="d4bca-277">U kunt deze wel wijzigen toothis toofix eventuele fouten bouwen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="d4bca-278">Wijzigingen in de naam van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="d4bca-278">Interface name changes</span></span>
<span data-ttu-id="d4bca-279">Hallo bewerking groepsnamen interface hebben alle gewijzigde toobe consistent zijn met de bijbehorende Eigenschapsnamen:</span><span class="sxs-lookup"><span data-stu-id="d4bca-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="d4bca-280">type Hallo `ISearchServiceClient.Indexes` gewijzigd van `IIndexOperations` te`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="d4bca-281">type Hallo `ISearchServiceClient.Indexers` gewijzigd van `IIndexerOperations` te`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="d4bca-282">type Hallo `ISearchServiceClient.DataSources` gewijzigd van `IDataSourceOperations` te`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="d4bca-283">type Hallo `ISearchIndexClient.Documents` gewijzigd van `IDocumentOperations` te`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="d4bca-284">Deze wijziging is waarschijnlijk niet tooaffect uw code, tenzij u mocks van deze interfaces voor testdoeleinden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4bca-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="d4bca-285">Oplossingen voor problemen in versie 1.1</span><span class="sxs-lookup"><span data-stu-id="d4bca-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="d4bca-286">Er is een fout in oudere versies van hello Azure Search .NET SDK betreffende tooserialization van aangepaste modelklassen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="d4bca-287">Hallo fout kan optreden als u een aangepaste modelklasse met een eigenschap van een niet-nullbare waardetype gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4bca-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="d4bca-288">Stappen tooreproduce</span><span class="sxs-lookup"><span data-stu-id="d4bca-288">Steps tooreproduce</span></span>
<span data-ttu-id="d4bca-289">Maak een aangepaste modelklasse met een eigenschap van niet-nullbare waardetype.</span><span class="sxs-lookup"><span data-stu-id="d4bca-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="d4bca-290">Bijvoorbeeld, Voeg een openbare `UnitCount` eigenschap van het type `int` in plaats van `int?`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="d4bca-291">Als u een document met de standaardwaarde Hallo van dat type index (bijvoorbeeld 0 voor `int`), Hallo veld wordt niet null zijn in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d4bca-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="d4bca-292">Als u dat document vervolgens zoekt, Hallo `Search` aanroep genereert `JsonSerializationException` klagen dat kan niet worden geconverteerd `null` te`int`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="d4bca-293">Ook filters werkt mogelijk niet zoals verwacht omdat null toohello index in plaats van de waarde Hallo bedoeld is geschreven.</span><span class="sxs-lookup"><span data-stu-id="d4bca-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="d4bca-294">Gegevens herstellen</span><span class="sxs-lookup"><span data-stu-id="d4bca-294">Fix details</span></span>
<span data-ttu-id="d4bca-295">We hebben dit probleem opgelost in versie 1.1 van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="d4bca-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="d4bca-296">Op dit moment hebt u een modelklasse als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4bca-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="d4bca-297">en u `IntValue` too0, dat waarde is nu correct geserialiseerd als 0 op Hallo kabel en als 0 in Hallo index opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d4bca-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="d4bca-298">Ophalen ook werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="d4bca-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="d4bca-299">Er is een mogelijk probleem toobe op de hoogte met deze methode: als u een modeltype met een niet-nullbare eigenschap gebruikt, hebt u te**garanderen** dat de documenten in uw index geen null-waarde voor het betreffende veld Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="d4bca-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="d4bca-300">Hallo SDK noch hello Azure Search REST API kunt u tooenforce dit.</span><span class="sxs-lookup"><span data-stu-id="d4bca-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="d4bca-301">Dit is niet alleen een hypothetische probleem: Stel een scenario waarin het toevoegen van een nieuw veld tooan bestaande index van het type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="d4bca-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="d4bca-302">Na het bijwerken van de indexdefinitie hello, moeten alle documenten een null-waarde voor het nieuwe veld (omdat alle typen null in Azure Search).</span><span class="sxs-lookup"><span data-stu-id="d4bca-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="d4bca-303">Als u vervolgens een modelklasse met een niet-nullbare `int` eigenschap voor dat veld gebruikt, ontvangt u een `JsonSerializationException` zoals deze bij het tooretrieve documenten:</span><span class="sxs-lookup"><span data-stu-id="d4bca-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="d4bca-304">Daarom nog steeds wordt aangeraden nullbare typen te gebruiken in uw modelklassen als een best practice.</span><span class="sxs-lookup"><span data-stu-id="d4bca-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="d4bca-305">Zie voor meer informatie over deze fout en Hallo correctie [dit probleem op GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="d4bca-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

