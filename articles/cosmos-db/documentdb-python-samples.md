---
title: Voorbeelden van Python aaaDocumentDB API voor Azure Cosmos DB | Microsoft Docs
description: Python-voorbeelden op github voor algemene taken in Azure Cosmos DB, inclusief CRUD-bewerkingen niet vinden.
keywords: Python-voorbeelden
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Azure Cosmos DB Python-voorbeelden
> [!div class="op_single_selector"]
> * [.NET-voorbeelden](documentdb-dotnet-samples.md)
> * [Node.js-voorbeelden](documentdb-nodejs-samples.md)
> * [Python-voorbeelden](documentdb-python-samples.md)
> * [Voorbeeld van Azure Codegalerie](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

Voorbeeldoplossingen die worden uitgevoerd CRUD-bewerkingen en andere veelvoorkomende bewerkingen op Azure DB die Cosmos-bronnen zijn opgenomen in Hallo [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub-opslagplaats. Dit artikel bevat:

* Koppelingen toohello taken in elk Hallo Python voorbeeld project-bestanden. 
* Koppelingen toohello gerelateerd API-referentie-inhoud.

**Vereisten**

1. U moet een Azure-account toouse deze Python-voorbeelden:
   * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/): U ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze allemaal hebt gebruikt kunt u maximaal Hallo account houden en gebruik gratis Azure-services, zoals Websites. Uw creditcard wordt nooit worden in rekening gebracht, tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.
     * U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
2. U moet ook Hallo [Python SDK](documentdb-sdk-python.md). 
   
   > [!NOTE]
   > Elk voorbeeld staat op zichzelf, het zelf wordt ingesteld en opgeschoond. Als zodanig Hallo voorbeelden meerdere aanroepen te verlenen[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Telkens wanneer dit wordt gedaan uw abonnement wordt gefactureerd voor gebruik per Hallo prestatielaag van Hallo verzameling wordt gemaakt van 1 uur. 
   > 
   > 

## <a name="database-examples"></a>Database-voorbeelden
Hallo [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) bestand Hallo [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project ziet u hoe tooperform Hallo na taken.

| Taak | API-verwijzing |
| --- | --- |
| [Een database maken](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client. CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Query uitvoeren op een account voor een database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client. QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Lezen van een database met Id](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client. ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Lijst met databases voor een account](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client. ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Een database verwijderen](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client. DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Voorbeelden van de verzameling
Hallo [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) bestand Hallo [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project ziet u hoe tooperform Hallo na taken.

| Taak | API-verwijzing |
| --- | --- |
| [Een verzameling maken](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Een lijst van alle verzamelingen in een database lezen](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client. ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Een verzameling door-Id ophalen](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client. ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Laag van de prestaties van een verzameling ophalen](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Laag van de prestaties van een verzameling wijzigen](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client. ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Een verzameling verwijderen](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client. DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

