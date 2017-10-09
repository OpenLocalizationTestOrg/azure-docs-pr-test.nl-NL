---
title: aaaUse Azure Data Factory met SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Azure Data Factory (ADF) met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Azure Data Factory gebruiken met SQL datawarehouse
Azure Data Factory biedt een volledig beheerde methode voor het organiseren van Hallo overdracht van gegevens en de uitvoering van opgeslagen procedures op de SQL Data Warehouse.  Hierdoor kunt u toomore eenvoudig instellen en planning complexe extraheren Transform and Load (ETL) voor procedures met SQL Data Warehouse. Zie voor een volledig overzicht van Azure Data Factory Hallo [documentatie Azure Data Factory][Azure Data Factory documentation].

## <a name="data-movement"></a>Gegevensverplaatsing
Azure Data Factory kunt verplaatsing van gegevens tussen zowel lokale bronnen en andere Azure-services.  Algemene, de huidige integratie met Azure Data Factory ondersteunt data movement tooand van Hallo volgende locaties:

* Azure blob-opslag
* Azure SQL Database
* On-premises SQL Server
* SQL Server op IaaS

Zie voor informatie over hoe de activiteit voor het kopiëren van tooset van een data [kopiëren van gegevens met Azure Data Factory][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Opgeslagen procedures
 In Hallo dezelfde manier kan zijn gebruikt tooschedule gegevensoverdracht, Azure Data Factory kan ook worden gebruikte tooorchestrate Hallo uitvoering van opgeslagen procedures.  Hiermee kan complexere pijplijnen toobe gemaakt en wordt uitgebreid Azure Data Factory mogelijkheid tooleverage Hallo verwerkingskracht van SQL Data Warehouse.

## <a name="next-steps"></a>Volgende stappen
Zie voor een overzicht van de integratie van [overzicht van de integratie van SQL Data Warehouse][SQL Data Warehouse integration overview].
Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

