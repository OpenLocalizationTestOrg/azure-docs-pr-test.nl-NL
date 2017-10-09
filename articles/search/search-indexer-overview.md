---
title: aaaIndexers in Azure Search | Microsoft Docs
description: Azure SQL database, Azure Cosmos DB of Azure-opslag tooextract doorzoekbare gegevens verkennen en een Azure Search-index te vullen.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indexeerfuncties in Azure Search
> [!div class="op_single_selector"]
>
> * [Overzicht](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md)
> * [Azure-tabelopslag](search-howto-indexing-azure-tables.md)
>
>

Een **indexeerfunctie** in Azure Search is een Verkenner die doorzoekbare gegevens en metagegevens uit een externe gegevensbron haalt en een index vult op basis van veld naar toewijzingen tussen Hallo-index en de gegevensbron. Deze aanpak is het soms waarnaar wordt verwezen tooas een 'pullmodel' omdat Hallo service de gegevens ophaalt in zonder dat u toowrite hoeft code die gegevens tooan index pushes.

U kunt uitsluitend Hallo voor gegevensopname betekent een indexeerfunctie gebruiken of gebruik een combinatie van technieken die Hallo gebruik van een indexeerfunctie voor het laden van slechts enkele Hallo velden in de index bevatten.

U kunt indexeerfuncties op verzoek uitvoeren of op basis van een terugkerend schema voor gegevensvernieuwing, dat zo vaak als elke 15 minuten kan worden uitgevoerd. Als u vaker updates wilt uitvoeren, hebt u een pushmodel nodig dat tegelijkertijd gegevens in Azure Search en uw externe gegevensbron bijwerkt.

## <a name="approaches-for-creating-and-managing-indexers"></a>Strategieën voor het maken en beheren van indexeerfuncties
U kunt voor algemeen beschikbare indexeerfuncties zoals Azure SQL of Azure Cosmos DB met behulp van deze methoden indexeerfuncties maken en beheren:

* [Portal > Wizard Gegevens importeren](search-get-started-portal.md)
* [Service REST API](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Basisconfiguratiestappen
Indexeerfuncties kunnen functies die gegevensbron unieke toohello bieden. In dit opzicht variëren bepaalde aspecten van de configuratie van de indexeerfunctie of de gegevensbron al naar gelang het type indexeerfunctie. Echter alle indexeerfuncties Hallo delen dezelfde basic samenstelling en vereisten. Stappen die zijn algemene tooall indexeerfuncties worden hieronder behandeld.

### <a name="step-1-create-an-index"></a>Stap 1: een index maken
Een indexeerfunctie wordt de opname van sommige taken gerelateerde toodata automatiseren, maar maken van een index is niet een van beide. Een vereiste is dat u een vooraf gedefinieerde index moet hebben met velden die overeenkomen met de velden in uw externe gegevensbron. Zie [Create an Index (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx) (Een index maken (Azure Search REST API)) voor meer informatie over het structureren van een index.

### <a name="step-2-create-a-data-source"></a>Stap 2: een gegevensbron maken
Een indexeerfunctie haalt gegevens op uit een **gegevensbron** die informatie, zoals een verbindingsreeks, bevat. Hallo volgende gegevensbronnen worden momenteel ondersteund:

* [Azure SQL Database of SQL Server op een virtuele Azure-machine](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob storage](search-howto-indexing-azure-blob-storage.md), gebruikt u tooextract tekst uit PDF, Office-documenten, HTML of XML
* [Azure-tabelopslag](search-howto-indexing-azure-tables.md)

Gegevensbronnen worden geconfigureerd en onafhankelijk van Hallo indexeerfuncties die er gebruik, wat betekent dat een gegevensbron kan worden gebruikt door meerdere indexeerfuncties tooload meer dan één index op een tijdstip worden beheerd.

### <a name="step-3create-and-schedule-hello-indexer"></a>Stap 3: maken en plannen van Hallo indexeerfunctie
Hallo indexeerfunctie definitie is een constructie Hallo index, gegevensbron en een planning opgeven. Een indexeerfunctie kunt verwijzen naar een gegevensbron van een andere service, zolang die gegevensbron uit Hallo hetzelfde abonnement. Zie [Create Indexer (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx) (Een indexeerfunctie maken (Azure Search REST API)) voor meer informatie over het structureren van een indexeerfunctie.

## <a name="next-steps"></a>Volgende stappen
Nu dat u het uitgangspunt Hallo hebt, is de volgende stap Hallo tooreview vereisten en taken specifieke tooeach gegevensbrontype.

* [Azure SQL Database of SQL Server op een virtuele Azure-machine](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md), gebruikt u tooextract tekst uit PDF, Office-documenten, HTML of XML
* [Azure-tabelopslag](search-howto-indexing-azure-tables.md)
* [CSV blobs met Azure Search Blob-indexeerfunctie Hallo indexeren](search-howto-index-csv-blobs.md)
* [Indexeren van JSON-blobs met de indexeerfunctie Azure Search Blob](search-howto-index-json-blobs.md)
