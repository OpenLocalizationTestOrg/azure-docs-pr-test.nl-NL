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
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Query uitvoeren op een Azure Search-index met behulp van de Search Explorer in hello Azure Portal
> [!div class="op_single_selector"]
> * [Overzicht](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Dit artikel laat zien hoe tooquery een Azure Search-index met behulp van **Search Explorer** in hello Azure-portal. U kunt de Search Explorer toosubmit eenvoudige of volledige Lucene query tekenreeksen tooany bestaande index gebruiken in uw service.

## <a name="open-hello-service-dashboard"></a>Open Hallo servicedashboard
1. Klik op **alle resources** in de snelbalk Hallo op Hallo linkerkant Hallo [Azure-portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Selecteer uw Azure Search-service.

## <a name="select-an-index"></a>Een index selecteren

Selecteer Hallo index gewenst toosearch van Hallo **indexen** tegel.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Search Explorer openen

Klik op Hallo Search Explorer tegel tooslide open Hallo-zoekbalk en het deelvenster met resultaten.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Beginnen met zoeken

Wanneer u Hallo Search Explorer gebruikt, kunt u [queryparameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate Hallo query.

1. Typ in **Queryreeks** een query en druk vervolgens op **Zoeken**. 

   Hallo-queryreeks worden automatisch verdeeld in de juiste aanvraag Hallo URL toosubmit een HTTP-aanvraag tegen hello Azure Search REST-API.   
   
   U kunt elk geldig eenvoudige of volledige Lucene syntaxis toocreate Hallo-aanvraag. Hallo `*` teken is gelijkwaardig tooan leeg of niet-gespecificeerde zoekquery waarmee alle documenten in willekeurige volgorde.

2. In **resultaten**, queryresultaten worden weergegeven in de onbewerkte JSON, identieke toohello nettolading geretourneerd in een HTTP-antwoordtekst bij de uitgifte van aanvragen via een programma.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Volgende stappen

Hallo na bronnen bieden informatie over extra query-syntaxis en voorbeelden.

 + [Vereenvoudigde querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Lucene-querysyntaxis](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Voorbeelden van Lucene-querysyntaxis](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData-filterexpressiesyntaxis](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 