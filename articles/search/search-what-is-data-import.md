---
title: aaaData uploaden in Azure Search | Microsoft Docs
description: Meer informatie over hoe tooupload gegevens tooan in Azure Search index.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Uploaden van gegevens tooAzure zoeken
> [!div class="op_single_selector"]
> * [Overzicht](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Er zijn twee manieren toopopulate een index met uw gegevens. de eerste optie Hallo is handmatig pushen van de gegevens in Hallo-index met behulp van hello Azure Search [REST-API](search-import-data-rest-api.md) of [.NET SDK](search-import-data-dotnet.md). de tweede optie Hallo is te[wijst u een ondersteunde gegevensbron](search-indexer-overview.md) tooyour indexeren en zorgen dat Azure Search automatisch in Hallo-gegevens ophalen.

## <a name="push-data-tooan-index"></a>Index van het tooan push
Deze aanpak verwijst tooprogrammatically verzenden van uw gegevens tooAzure Search toomake deze beschikbaar zijn voor het zoeken. Hallo pushmodel is voor toepassingen met zeer lage latentie is vereist (bijvoorbeeld wanneer en zoekopdracht operations toobe synchroon met dynamische inventarisatiedatabases), de enige optie.

U kunt Hallo [REST-API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) of [.NET SDK](search-import-data-dotnet.md) toopush gegevens tooan index. Er is momenteel geen ondersteuning voor het pushen van gegevens via het Hallo-portal.

Deze aanpak is flexibeler dan Hallo pull-model omdat kunt u documenten afzonderlijk of in batches uploaden (up too1000 per batch of 16 MB, ongeacht de limiet ligt). Hallo pushmodel kunt u ook tooupload documenten tooAzure zoeken ongeacht waar uw gegevens.

Hallo gegevensindeling begrepen door Azure Search is JSON en alle documenten in Hallo gegevensset moeten velden die zijn gedefinieerd in uw indexschema toofields toegewezen hebben. 

## <a name="pull-data-into-an-index"></a>Gegevens in een index ophalen
Hallo pull-model verkent een ondersteunde gegevensbron en uploadt automatisch Hallo gegevens in uw index. In Azure Search is deze mogelijkheid geïmplementeerd via *indexeerfuncties*, die momenteel beschikbaar zijn voor [Blob Storage](search-howto-indexing-azure-blob-storage.md), [Table Storage](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Azure SQL-database en SQL Server op Azure VM's](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Indexeerfuncties verbinding maken met een index tooa gegevensbron (meestal een tabel, weergave of gelijkwaardige structuur) en bron velden tooequivalent velden in de index Hallo toewijzen. Bij het uitvoeren Hallo rijenset is automatisch getransformeerde tooJSON en in de opgegeven index Hallo geladen. Alle indexeerfuncties ondersteuning voor het plannen, zodat u kunt opgeven hoe vaak gegevens Hallo toobe vernieuwd. De meeste indexeerfuncties opgeven als de gegevensbron Hallo het ondersteunt bijhouden van wijzigingen. Door het bijhouden van wijzigingen en verwijderingen tooexisting documenten bovendien toorecognizing nieuwe documenten, indexeerfuncties verwijderen Hallo nodig tooactively Hallo gegevens beheren in uw index. 

Functionaliteit van de indexeerfunctie wordt weergegeven in Hallo [Azure-portal](search-import-data-portal.md), Hallo [REST-API](/rest/api/searchservice/Indexer-operations), en Hallo [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Een voordeel toousing Hallo-portal is dat Azure Search meestal een standaardschema index voor u genereren kunt door te lezen van de metagegevens van Hallo bron gegevensset Hallo. Totdat het Hallo-index wordt verwerkt, na welke Hallo alleen schema toegestaan zijn die niet opnieuw indexeren hoeven, kunt u de gegenereerde index Hallo wijzigen. Als de gewenste toomake impact Hallo-wijzigingen hello rechtstreeks schema, moet u toorebuild Hallo index. 

Nadat het Hallo-index is ingevuld, kunt u **Search Explorer** in de portal opdrachtbalk Hallo als een verificatiestap.

## <a name="query-an-index-using-search-explorer"></a>Gegevens uit een index opvragen met Search Explorer

Een snelle manier tooperform voorlopige controle op Hallo uploaden van het document is toouse **Search Explorer** in Hallo-portal. Hallo explorer kunt u een index een query zonder toowrite code. Hallo zoekervaring is op basis van standaardinstellingen, zoals Hallo [eenvoudige syntaxis](/rest/api/searchservice/simple-query-syntax-in-azure-search) en standaard [searchMode queryparameter](/rest/api/searchservice/search-documents). Resultaten worden geretourneerd in JSON zodat u kunt het hele document Hallo inspecteren.

> [!TIP]
> Talrijke [Azure Search-codevoorbeelden](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) zijn ingesloten of direct beschikbaar gegevenssets, biedt een eenvoudige manier tooget gestart. Hallo-portal biedt ook een indexeerfunctie voorbeeld en de gegevensbron die bestaan uit een kleine vastgoed gegevensset (met de naam 'onroerend goed-ons-sample'). Wanneer u de vooraf geconfigureerde indexeerfunctie Hallo op Hallo voorbeeld gegevensbron uitvoert, wordt er een index gemaakt en geladen met de documenten die vervolgens kunnen worden opgevraagd in Search Explorer of door de code die u schrijft.
