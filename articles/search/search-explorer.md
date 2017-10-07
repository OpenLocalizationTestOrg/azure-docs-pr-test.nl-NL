---
title: aaa "query uitvoeren in een index (portal - Azure Search) | Microsoft Docs'
description: Een zoekopdracht in hello Azure Portal Search Explorer uitgeven.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="fedc8-103">Query uitvoeren op een Azure Search-index met behulp van de Search Explorer in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fedc8-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fedc8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fedc8-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="fedc8-105">Portal</span><span class="sxs-lookup"><span data-stu-id="fedc8-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="fedc8-106">.NET</span><span class="sxs-lookup"><span data-stu-id="fedc8-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="fedc8-107">REST</span><span class="sxs-lookup"><span data-stu-id="fedc8-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="fedc8-108">Dit artikel laat zien hoe tooquery een Azure Search-index met behulp van **Search Explorer** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fedc8-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="fedc8-109">U kunt de Search Explorer toosubmit eenvoudige of volledige Lucene query tekenreeksen tooany bestaande index gebruiken in uw service.</span><span class="sxs-lookup"><span data-stu-id="fedc8-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="fedc8-110">Open Hallo servicedashboard</span><span class="sxs-lookup"><span data-stu-id="fedc8-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="fedc8-111">Klik op **alle resources** in de snelbalk Hallo op Hallo linkerkant Hallo [Azure-portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="fedc8-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="fedc8-112">Selecteer uw Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="fedc8-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="fedc8-113">Een index selecteren</span><span class="sxs-lookup"><span data-stu-id="fedc8-113">Select an index</span></span>

<span data-ttu-id="fedc8-114">Selecteer Hallo index gewenst toosearch van Hallo **indexen** tegel.</span><span class="sxs-lookup"><span data-stu-id="fedc8-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="fedc8-115">Search Explorer openen</span><span class="sxs-lookup"><span data-stu-id="fedc8-115">Open Search Explorer</span></span>

<span data-ttu-id="fedc8-116">Klik op Hallo Search Explorer tegel tooslide open Hallo-zoekbalk en het deelvenster met resultaten.</span><span class="sxs-lookup"><span data-stu-id="fedc8-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="fedc8-117">Beginnen met zoeken</span><span class="sxs-lookup"><span data-stu-id="fedc8-117">Start searching</span></span>

<span data-ttu-id="fedc8-118">Wanneer u Hallo Search Explorer gebruikt, kunt u [queryparameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate Hallo query.</span><span class="sxs-lookup"><span data-stu-id="fedc8-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="fedc8-119">Typ in **Queryreeks** een query en druk vervolgens op **Zoeken**.</span><span class="sxs-lookup"><span data-stu-id="fedc8-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="fedc8-120">Hallo-queryreeks worden automatisch verdeeld in de juiste aanvraag Hallo URL toosubmit een HTTP-aanvraag tegen hello Azure Search REST-API.</span><span class="sxs-lookup"><span data-stu-id="fedc8-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="fedc8-121">U kunt elk geldig eenvoudige of volledige Lucene syntaxis toocreate Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="fedc8-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="fedc8-122">Hallo `*` teken is gelijkwaardig tooan leeg of niet-gespecificeerde zoekquery waarmee alle documenten in willekeurige volgorde.</span><span class="sxs-lookup"><span data-stu-id="fedc8-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="fedc8-123">In **resultaten**, queryresultaten worden weergegeven in de onbewerkte JSON, identieke toohello nettolading geretourneerd in een HTTP-antwoordtekst bij de uitgifte van aanvragen via een programma.</span><span class="sxs-lookup"><span data-stu-id="fedc8-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="fedc8-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fedc8-124">Next steps</span></span>

<span data-ttu-id="fedc8-125">Hallo na bronnen bieden informatie over extra query-syntaxis en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="fedc8-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="fedc8-126">Vereenvoudigde querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="fedc8-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="fedc8-127">Lucene-querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="fedc8-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="fedc8-128">Voorbeelden van Lucene-querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="fedc8-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="fedc8-129">OData-filterexpressiesyntaxis</span><span class="sxs-lookup"><span data-stu-id="fedc8-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 