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
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="4a85d-103">Azure Data Factory gebruiken met SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="4a85d-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="4a85d-104">Azure Data Factory biedt een volledig beheerde methode voor het organiseren van Hallo overdracht van gegevens en de uitvoering van opgeslagen procedures op de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a85d-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="4a85d-105">Hierdoor kunt u toomore eenvoudig instellen en planning complexe extraheren Transform and Load (ETL) voor procedures met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a85d-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="4a85d-106">Zie voor een volledig overzicht van Azure Data Factory Hallo [documentatie Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="4a85d-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="4a85d-107">Gegevensverplaatsing</span><span class="sxs-lookup"><span data-stu-id="4a85d-107">Data Movement</span></span>
<span data-ttu-id="4a85d-108">Azure Data Factory kunt verplaatsing van gegevens tussen zowel lokale bronnen en andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="4a85d-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="4a85d-109">Algemene, de huidige integratie met Azure Data Factory ondersteunt data movement tooand van Hallo volgende locaties:</span><span class="sxs-lookup"><span data-stu-id="4a85d-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="4a85d-110">Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="4a85d-110">Azure blob storage</span></span>
* <span data-ttu-id="4a85d-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="4a85d-111">Azure SQL Database</span></span>
* <span data-ttu-id="4a85d-112">On-premises SQL Server</span><span class="sxs-lookup"><span data-stu-id="4a85d-112">On-premises SQL Server</span></span>
* <span data-ttu-id="4a85d-113">SQL Server op IaaS</span><span class="sxs-lookup"><span data-stu-id="4a85d-113">SQL Server on IaaS</span></span>

<span data-ttu-id="4a85d-114">Zie voor informatie over hoe de activiteit voor het kopiëren van tooset van een data [kopiëren van gegevens met Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="4a85d-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="4a85d-115">Opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="4a85d-115">Stored Procedures</span></span>
 <span data-ttu-id="4a85d-116">In Hallo dezelfde manier kan zijn gebruikt tooschedule gegevensoverdracht, Azure Data Factory kan ook worden gebruikte tooorchestrate Hallo uitvoering van opgeslagen procedures.</span><span class="sxs-lookup"><span data-stu-id="4a85d-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="4a85d-117">Hiermee kan complexere pijplijnen toobe gemaakt en wordt uitgebreid Azure Data Factory mogelijkheid tooleverage Hallo verwerkingskracht van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a85d-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a85d-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a85d-118">Next steps</span></span>
<span data-ttu-id="4a85d-119">Zie voor een overzicht van de integratie van [overzicht van de integratie van SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="4a85d-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="4a85d-120">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="4a85d-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

