---
title: aaaUpgrading toohello Azure Search Service REST API versie 2016-09-01 | Microsoft Docs
description: Een upgrade toohello Azure Search Service REST API versie 2016-09-01
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="c5c04-103">Een upgrade toohello Azure Search Service REST API versie 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="c5c04-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="c5c04-104">Als u versie 2015-02-28 of 2015-02-28-Preview Hallo [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), dit artikel helpt u bij het bijwerken van uw toepassing toouse Hallo volgende algemeen beschikbaar API-versie, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="c5c04-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="c5c04-105">Versie 2016-09-01 Hallo REST-API bevat een aantal wijzigingen uit eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="c5c04-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="c5c04-106">Dit zijn vooral achterwaarts compatibel, zodat uw code te wijzigen, moet alleen minimale inspanning, afhankelijk van welke versie u hebt gebruikt vóór nodig.</span><span class="sxs-lookup"><span data-stu-id="c5c04-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="c5c04-107">Zie [stappen tooupgrade](#UpgradeSteps) voor instructies over het toochange uw code toouse Hallo nieuwe API-versie.</span><span class="sxs-lookup"><span data-stu-id="c5c04-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="c5c04-108">Verschillende versies van de REST-API, met inbegrip van de meest recente Hallo biedt ondersteuning voor uw Azure Search-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c5c04-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="c5c04-109">Wanneer deze niet langer Hallo recentste is, maar het is raadzaam dat u de nieuwste versie van code toouse Hallo migreert, kunt u een versie toouse blijven.</span><span class="sxs-lookup"><span data-stu-id="c5c04-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="c5c04-110">Wat is er nieuw in versie 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="c5c04-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="c5c04-111">Versie 2016-09-01 is Hallo tweede algemeen beschikbaar release van hello Azure Search Service REST API.</span><span class="sxs-lookup"><span data-stu-id="c5c04-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="c5c04-112">Nieuwe functies in deze API-versie:</span><span class="sxs-lookup"><span data-stu-id="c5c04-112">New features in this API version include:</span></span>

* <span data-ttu-id="c5c04-113">[Aangepaste analyzers](https://aka.ms/customanalyzers), waarmee u tootake controle over Hallo proces van het converteren van tekst in worden geïndexeerd en doorzoekbare tokens.</span><span class="sxs-lookup"><span data-stu-id="c5c04-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="c5c04-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) en [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeerfuncties waarmee u tooeasily gegevens importeren uit Azure storage in Azure Search op een planning of op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c5c04-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="c5c04-115">[Veld toewijzingen](search-indexer-field-mappings.md), waarmee u toocustomize hoe indexeerfuncties gegevens importeren in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="c5c04-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="c5c04-116">ETags, waarmee u tooupdate Hallo definities van indexen, Indexeerfuncties en gegevensbronnen op een manier gelijktijdigheid-safe.</span><span class="sxs-lookup"><span data-stu-id="c5c04-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="c5c04-117">Stappen tooupgrade</span><span class="sxs-lookup"><span data-stu-id="c5c04-117">Steps tooupgrade</span></span>
<span data-ttu-id="c5c04-118">Als u een van versie 2015-02-28 upgrade, u waarschijnlijk geen toomake wijzigingen tooyour code, dan toochange Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="c5c04-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="c5c04-119">Hallo alleen situaties waarin u toochange code mogelijk moet zijn wanneer:</span><span class="sxs-lookup"><span data-stu-id="c5c04-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="c5c04-120">Uw code mislukt wanneer het niet-herkende eigenschappen worden geretourneerd in een API-reactie.</span><span class="sxs-lookup"><span data-stu-id="c5c04-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="c5c04-121">Standaard moet worden genegeerd in uw toepassing eigenschappen die niet wordt herkend.</span><span class="sxs-lookup"><span data-stu-id="c5c04-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="c5c04-122">Uw code zich blijft voordoen API-aanvragen en tooresend probeert ze toohello nieuwe API-versie.</span><span class="sxs-lookup"><span data-stu-id="c5c04-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="c5c04-123">Bijvoorbeeld: dit kan gebeuren als uw toepassing blijft voortzetting tokens die zijn geretourneerd door het Hallo-API van zoekservice draaien (voor meer informatie zoekt `@search.nextPageParameters` in Hallo [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="c5c04-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="c5c04-124">Als beide situaties tooyou toepast, vervolgens moet u mogelijk toochange uw code dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="c5c04-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="c5c04-125">Anders geen wijzigingen moeten niet nodig, tenzij u wilt dat toostart met Hallo [nieuwe functies](#WhatsNew) van 2016-09-01-versie.</span><span class="sxs-lookup"><span data-stu-id="c5c04-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="c5c04-126">Als u een van versie 2015-02-28-Preview upgrade, Hallo hierboven is ook van toepassing, maar u moet ook rekening houden sommige preview-functies zijn niet beschikbaar in versie 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="c5c04-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="c5c04-127">Azure Blob Storage-indexeerfunctie ondersteuning voor CSV-bestanden en blobs met JSON-matrices.</span><span class="sxs-lookup"><span data-stu-id="c5c04-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="c5c04-128">Synoniemen</span><span class="sxs-lookup"><span data-stu-id="c5c04-128">Synonyms</span></span>
* <span data-ttu-id="c5c04-129">'Meer als volgt' query 's</span><span class="sxs-lookup"><span data-stu-id="c5c04-129">"More like this" queries</span></span>

<span data-ttu-id="c5c04-130">Als uw code deze functies gebruikt, zich u niet kunnen tooupgrade too2016-09-01 zonder uw gebruik ervan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c5c04-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5c04-131">Maak onthouden, preview-API's zijn bedoeld voor testen en evalueren en mag niet worden gebruikt in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c5c04-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="c5c04-132">Conclusie</span><span class="sxs-lookup"><span data-stu-id="c5c04-132">Conclusion</span></span>
<span data-ttu-id="c5c04-133">Als u meer informatie over het gebruik van Azure Search Service REST API Hallo nodig, raadpleegt u Hallo onlangs bijgewerkt [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="c5c04-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="c5c04-134">Uw feedback is Welkom op Azure Search.</span><span class="sxs-lookup"><span data-stu-id="c5c04-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="c5c04-135">Als u problemen ondervindt, kunt u gratis tooask ons voor hulp bij het Hallo [Azure Search MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) of [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="c5c04-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="c5c04-136">Als vraagt u een vraag over Azure zoeken op StackOverflow, zorg ervoor dat tootag met `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="c5c04-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="c5c04-137">Hartelijk dank voor het gebruik van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="c5c04-137">Thank you for using Azure Search!</span></span>

