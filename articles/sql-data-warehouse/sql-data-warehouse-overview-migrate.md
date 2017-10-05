---
title: Migreren van uw oplossing naar SQL Data Warehouse | Microsoft Docs
description: Migratie-instructies voor uw oplossing te brengen naar Azure SQL Data Warehouse-platform.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="3254f-103">Uw oplossing voor het migreren naar Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3254f-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="3254f-104">Zie wat betrokken bij het migreren van een bestaande databaseoplossing naar Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3254f-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="3254f-105">De werkbelasting van uw profiel</span><span class="sxs-lookup"><span data-stu-id="3254f-105">Profile your workload</span></span>
<span data-ttu-id="3254f-106">Voordat u migreert, die u wilt worden dat bepaalde SQL Data Warehouse is de juiste oplossing voor uw workload.</span><span class="sxs-lookup"><span data-stu-id="3254f-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="3254f-107">SQL Data Warehouse is een gedistribueerd systeem ontworpen voor het uitvoeren van analyses op grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="3254f-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="3254f-108">Migreren naar SQL Data Warehouse vereist sommige ontwerpwijzigingen die zijn niet te hard om te begrijpen maar het kunnen even duren om te implementeren.</span><span class="sxs-lookup"><span data-stu-id="3254f-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="3254f-109">Als uw bedrijf een datawarehouse bedrijfsniveau vereist, zijn de voordelen winnen.</span><span class="sxs-lookup"><span data-stu-id="3254f-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="3254f-110">Als u de kracht van SQL Data Warehouse hoeft, is het echter rendabeler SQL Server of Azure SQL Database wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3254f-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="3254f-111">Overweeg het gebruik van SQL Data Warehouse wanneer u:</span><span class="sxs-lookup"><span data-stu-id="3254f-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="3254f-112">Een of meer Terabytes aan gegevens hebben</span><span class="sxs-lookup"><span data-stu-id="3254f-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="3254f-113">Plan voor het uitvoeren van analyses op grote hoeveelheden gegevens</span><span class="sxs-lookup"><span data-stu-id="3254f-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="3254f-114">De mogelijkheid hebben om te schalen berekeningen en opslag</span><span class="sxs-lookup"><span data-stu-id="3254f-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="3254f-115">Wilt u kosten besparen door onderbreken rekenresources wanneer u ze niet nodig.</span><span class="sxs-lookup"><span data-stu-id="3254f-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="3254f-116">Gebruik geen SQL Data Warehouse voor operationele (OLTP-systemen)-werkbelastingen met:</span><span class="sxs-lookup"><span data-stu-id="3254f-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="3254f-117">Hoge frequentie leest en schrijft</span><span class="sxs-lookup"><span data-stu-id="3254f-117">High frequency reads and writes</span></span>
- <span data-ttu-id="3254f-118">Hiermee selecteert u een groot aantal singleton</span><span class="sxs-lookup"><span data-stu-id="3254f-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="3254f-119">Grote hoeveelheden één rij invoegen</span><span class="sxs-lookup"><span data-stu-id="3254f-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="3254f-120">Rij moet verwerken</span><span class="sxs-lookup"><span data-stu-id="3254f-120">Row by row processing needs</span></span>
- <span data-ttu-id="3254f-121">Niet-compatibele indeling (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="3254f-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="3254f-122">De migratie plannen</span><span class="sxs-lookup"><span data-stu-id="3254f-122">Plan the migration</span></span>

<span data-ttu-id="3254f-123">Zodra u hebt besloten om een bestaande oplossing voor het migreren naar SQL Data Warehouse, is het belangrijk om te plannen van de migratie voordat het aan de slag.</span><span class="sxs-lookup"><span data-stu-id="3254f-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="3254f-124">Een doel van de planning is om te controleren of dat uw gegevens, het tabelschema en uw code compatibel zijn met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3254f-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="3254f-125">Er zijn enkele verschillen compatibiliteit tussen uw huidige systeem- en SQL Data Warehouse omzeilen.</span><span class="sxs-lookup"><span data-stu-id="3254f-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="3254f-126">Bovendien door grote hoeveelheden gegevens te migreren naar Azure vergt tijd.</span><span class="sxs-lookup"><span data-stu-id="3254f-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="3254f-127">Een zorgvuldige planning versnelt opnemen van uw gegevens naar Azure.</span><span class="sxs-lookup"><span data-stu-id="3254f-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="3254f-128">Een ander doel van de planning is het ontwerp aanpassen om te controleren of dat uw oplossing maakt gebruik van de hoge queryprestaties die SQL Data Warehouse is ontworpen om te bieden.</span><span class="sxs-lookup"><span data-stu-id="3254f-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="3254f-129">Het ontwerpen van datawarehouses voor schaal introduceert verschillende ontwerp patronen en dus traditionele methoden niet altijd het beste.</span><span class="sxs-lookup"><span data-stu-id="3254f-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="3254f-130">Hoewel na de migratie kunt u bepaalde aanpassingen van het ontwerp, sneller wijzigingen aanbrengen in het proces op een later tijdstip, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3254f-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="3254f-131">Voor een succesvolle migratie, moet u uw tabelschema, uw code en uw gegevens te migreren.</span><span class="sxs-lookup"><span data-stu-id="3254f-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="3254f-132">Zie voor richtlijnen over deze migratieonderwerpen:</span><span class="sxs-lookup"><span data-stu-id="3254f-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="3254f-133">Uw schema's migreren</span><span class="sxs-lookup"><span data-stu-id="3254f-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="3254f-134">Uw code migreren</span><span class="sxs-lookup"><span data-stu-id="3254f-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="3254f-135">[Uw gegevens migreren](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="3254f-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="3254f-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3254f-136">Next steps</span></span>
<span data-ttu-id="3254f-137">De CAT (Customer Advisory Team) heeft ook enkele geweldige SQL Data Warehouse richtlijnen, ze via blogs publiceren.</span><span class="sxs-lookup"><span data-stu-id="3254f-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="3254f-138">Kijk eens naar hun artikel [gegevens voor het migreren naar Azure SQL Data Warehouse in de praktijk] [ Migrating data to Azure SQL Data Warehouse in practice] voor aanvullende hulp bij de migratie.</span><span class="sxs-lookup"><span data-stu-id="3254f-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
