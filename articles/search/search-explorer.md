---
title: Een query uitvoeren voor een index (Portal - Azure Search) | Microsoft Docs
description: Een zoekopdracht in de Search Explorer van Azure Portal uitvoeren.
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
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a><span data-ttu-id="577fe-103">Een query uitvoeren voor een Azure Search-index met behulp van Search Explorer van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="577fe-103">Query an Azure Search index using Search Explorer in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="577fe-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="577fe-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="577fe-105">Portal</span><span class="sxs-lookup"><span data-stu-id="577fe-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="577fe-106">.NET</span><span class="sxs-lookup"><span data-stu-id="577fe-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="577fe-107">REST</span><span class="sxs-lookup"><span data-stu-id="577fe-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="577fe-108">In dit artikel ziet u hoe u een query kunt uitvoeren voor een Azure Search-index met behulp van **Search Explorer** van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="577fe-108">This article shows you how to query an Azure Search index using **Search Explorer** in the Azure portal.</span></span> <span data-ttu-id="577fe-109">U kunt Search Explorer gebruiken om eenvoudige of volledige Lucene-queryreeksen te verzenden naar elke bestaande index in uw service.</span><span class="sxs-lookup"><span data-stu-id="577fe-109">You can use Search Explorer to submit simple or full Lucene query strings to any existing index in your service.</span></span>

## <a name="open-the-service-dashboard"></a><span data-ttu-id="577fe-110">De servicedashboard openen</span><span class="sxs-lookup"><span data-stu-id="577fe-110">Open the service dashboard</span></span>
1. <span data-ttu-id="577fe-111">Klik in de snelbalk aan de linkerkant van [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices) op **Alle resources**.</span><span class="sxs-lookup"><span data-stu-id="577fe-111">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="577fe-112">Selecteer uw Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="577fe-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="577fe-113">Een index selecteren</span><span class="sxs-lookup"><span data-stu-id="577fe-113">Select an index</span></span>

<span data-ttu-id="577fe-114">Selecteer via de tegel **Indexen** de index waarin u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="577fe-114">Select the index you would like to search from the **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="577fe-115">Search Explorer openen</span><span class="sxs-lookup"><span data-stu-id="577fe-115">Open Search Explorer</span></span>

<span data-ttu-id="577fe-116">Klik op de tegel Search Explorer om de zoekbalk en het resultatenvenster te openen.</span><span class="sxs-lookup"><span data-stu-id="577fe-116">Click on the Search Explorer tile to slide open the search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="577fe-117">Beginnen met zoeken</span><span class="sxs-lookup"><span data-stu-id="577fe-117">Start searching</span></span>

<span data-ttu-id="577fe-118">Wanneer u Search Explorer gebruikt, kunt u [queryparameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) opgeven om de query te formuleren.</span><span class="sxs-lookup"><span data-stu-id="577fe-118">When using the Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span></span>

1. <span data-ttu-id="577fe-119">Typ in **Queryreeks** een query en druk vervolgens op **Zoeken**.</span><span class="sxs-lookup"><span data-stu-id="577fe-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="577fe-120">De queryreeks wordt automatisch geparseerd in de juiste aanvraag-URL om een HTTP-aanvraag te verzenden naar de Azure Search REST-API.</span><span class="sxs-lookup"><span data-stu-id="577fe-120">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span></span>   
   
   <span data-ttu-id="577fe-121">U kunt elke geldige eenvoudige of volledige Lucene-querysyntaxis gebruiken om de aanvraag te maken.</span><span class="sxs-lookup"><span data-stu-id="577fe-121">You can use any valid simple or full Lucene query syntax to create the request.</span></span> <span data-ttu-id="577fe-122">Het teken `*` komt overeen met een lege of niet-opgegeven zoekopdracht die alle documenten in willekeurige volgorde retourneert.</span><span class="sxs-lookup"><span data-stu-id="577fe-122">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="577fe-123">In **Resultaten** worden de queryresultaten weergegeven als onbewerkte JSON, identiek aan de nettolading die wordt geretourneerd in een HTTP-antwoordtekst wanneer aanvragen via een programma worden uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="577fe-123">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="577fe-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="577fe-124">Next steps</span></span>

<span data-ttu-id="577fe-125">De volgende resources bieden extra informatie over querysyntaxis en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="577fe-125">The following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="577fe-126">Vereenvoudigde querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="577fe-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="577fe-127">Lucene-querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="577fe-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="577fe-128">Voorbeelden van Lucene-querysyntaxis</span><span class="sxs-lookup"><span data-stu-id="577fe-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="577fe-129">OData-filterexpressiesyntaxis</span><span class="sxs-lookup"><span data-stu-id="577fe-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 