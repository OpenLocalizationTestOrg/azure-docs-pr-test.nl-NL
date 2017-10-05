---
title: Een upgrade naar de Azure Search Service REST API versie 2016-09-01 | Microsoft Docs
description: Een upgrade naar de Azure Search Service REST API versie 2016-09-01
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
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="8b38d-103">Een upgrade naar de Azure Search Service REST API versie 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="8b38d-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="8b38d-104">Als u versie 2015-02-28 of 2015-02-28-Preview van de [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), dit artikel helpt u bij het bijwerken van uw toepassing gebruik de volgende algemeen beschikbaar API-versie, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="8b38d-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="8b38d-105">Versie 2016-09-01 van de REST API bevat een aantal wijzigingen uit eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="8b38d-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="8b38d-106">Dit zijn vooral achterwaarts compatibel, zodat uw code te wijzigen, moet alleen minimale inspanning, afhankelijk van welke versie u hebt gebruikt vóór nodig.</span><span class="sxs-lookup"><span data-stu-id="8b38d-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="8b38d-107">Zie [stappen voor het upgraden](#UpgradeSteps) voor instructies over het wijzigen van uw code voor het gebruik van de nieuwe API-versie.</span><span class="sxs-lookup"><span data-stu-id="8b38d-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="8b38d-108">Uw Azure Search-service-exemplaar ondersteunt verschillende versies van de REST-API, met inbegrip van de meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="8b38d-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="8b38d-109">U kunt blijven gebruiken van een versie wanneer het is niet meer de meest recente versie, maar het is raadzaam dat u uw code voor het gebruik van de nieuwste versie migreren.</span><span class="sxs-lookup"><span data-stu-id="8b38d-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="8b38d-110">Wat is er nieuw in versie 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="8b38d-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="8b38d-111">Versie 2016-09-01 is de tweede algemeen beschikbaar versie van de Azure Search Service REST-API.</span><span class="sxs-lookup"><span data-stu-id="8b38d-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="8b38d-112">Nieuwe functies in deze API-versie:</span><span class="sxs-lookup"><span data-stu-id="8b38d-112">New features in this API version include:</span></span>

* <span data-ttu-id="8b38d-113">[Aangepaste analyzers](https://aka.ms/customanalyzers), waarmee u controle over het proces van het converteren van tekst in worden geïndexeerd en doorzoekbare tokens krijgen.</span><span class="sxs-lookup"><span data-stu-id="8b38d-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="8b38d-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) en [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeerfuncties waarmee u kunt eenvoudig gegevens importeren uit Azure storage in Azure Search op een planning of op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8b38d-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="8b38d-115">[Veld toewijzingen](search-indexer-field-mappings.md), waarmee u aanpassen hoe indexeerfuncties gegevens importeren in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b38d-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="8b38d-116">ETags, waarmee u kunt de definities van indexen, Indexeerfuncties en gegevensbronnen op een gelijktijdigheid-veilige manier bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8b38d-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="8b38d-117">Stappen voor het upgraden</span><span class="sxs-lookup"><span data-stu-id="8b38d-117">Steps to upgrade</span></span>
<span data-ttu-id="8b38d-118">Als u een van versie 2015-02-28 upgrade, hoeft u waarschijnlijk te wijzigingen aanbrengt aan uw code anders dan het versienummer wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8b38d-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="8b38d-119">De enige situaties waarin u code wijzigen mogelijk moet zijn wanneer:</span><span class="sxs-lookup"><span data-stu-id="8b38d-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="8b38d-120">Uw code mislukt wanneer het niet-herkende eigenschappen worden geretourneerd in een API-reactie.</span><span class="sxs-lookup"><span data-stu-id="8b38d-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="8b38d-121">Standaard moet worden genegeerd in uw toepassing eigenschappen die niet wordt herkend.</span><span class="sxs-lookup"><span data-stu-id="8b38d-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="8b38d-122">Uw code zich blijft voordoen API-aanvragen en probeert opnieuw te verzenden naar de nieuwe API-versie.</span><span class="sxs-lookup"><span data-stu-id="8b38d-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="8b38d-123">Bijvoorbeeld: dit kan gebeuren als uw toepassing blijft voortzetting tokens die zijn geretourneerd door de Search-API draaien (voor meer informatie zoekt `@search.nextPageParameters` in de [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="8b38d-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="8b38d-124">Als beide situaties van toepassing is, moet u mogelijk uw code dienovereenkomstig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8b38d-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="8b38d-125">Anders wordt er geen wijzigingen moeten niet nodig, tenzij u wilt beginnen met de [nieuwe functies](#WhatsNew) van 2016-09-01-versie.</span><span class="sxs-lookup"><span data-stu-id="8b38d-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="8b38d-126">Als u een van versie 2015-02-28-Preview upgrade, de bovenstaande ook van toepassing, maar u moet ook rekening houden sommige preview-functies zijn niet beschikbaar in versie 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="8b38d-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="8b38d-127">Azure Blob Storage-indexeerfunctie ondersteuning voor CSV-bestanden en blobs met JSON-matrices.</span><span class="sxs-lookup"><span data-stu-id="8b38d-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="8b38d-128">Synoniemen</span><span class="sxs-lookup"><span data-stu-id="8b38d-128">Synonyms</span></span>
* <span data-ttu-id="8b38d-129">'Meer als volgt' query 's</span><span class="sxs-lookup"><span data-stu-id="8b38d-129">"More like this" queries</span></span>

<span data-ttu-id="8b38d-130">Als uw code deze functies gebruikt, is het niet mogelijk om te werken naar 2016-09-01 zonder uw gebruik ervan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8b38d-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b38d-131">Maak onthouden, preview-API's zijn bedoeld voor testen en evalueren en mag niet worden gebruikt in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8b38d-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="8b38d-132">Conclusie</span><span class="sxs-lookup"><span data-stu-id="8b38d-132">Conclusion</span></span>
<span data-ttu-id="8b38d-133">Als u meer informatie over het gebruik van de Azure Search Service REST API, Zie de onlangs bijgewerkt [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="8b38d-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="8b38d-134">Uw feedback is Welkom op Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b38d-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="8b38d-135">Als u problemen ondervindt, gerust ons om hulp te vragen op de [Azure Search MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) of [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="8b38d-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="8b38d-136">Als u een vraag over de Azure Search op StackOverflow vraagt, controleert u of deze met een label `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="8b38d-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="8b38d-137">Hartelijk dank voor het gebruik van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b38d-137">Thank you for using Azure Search!</span></span>

