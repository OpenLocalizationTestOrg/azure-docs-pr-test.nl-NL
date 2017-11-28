---
title: aaaMigrate uw oplossing tooSQL Data Warehouse | Microsoft Docs
description: Migratie-instructies voor uw oplossing tooAzure SQL Data Warehouse-platform te brengen.
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
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="06b81-103">Uw oplossing tooAzure SQL Data Warehouse migreren</span><span class="sxs-lookup"><span data-stu-id="06b81-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="06b81-104">Zie wat betrokken bij de migratie van een bestaande database oplossing tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06b81-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="06b81-105">De werkbelasting van uw profiel</span><span class="sxs-lookup"><span data-stu-id="06b81-105">Profile your workload</span></span>
<span data-ttu-id="06b81-106">Voordat u migreert, wilt u toobe bepaalde dat SQL Data Warehouse is Hallo juiste oplossing voor uw workload.</span><span class="sxs-lookup"><span data-stu-id="06b81-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="06b81-107">SQL Data Warehouse is een gedistribueerd systeem ontworpen tooperform analytics op grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="06b81-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="06b81-108">Migreren tooSQL Data Warehouse is vereist voor sommige ontwerpwijzigingen die niet te moeilijk toounderstand, maar sommige tooimplement tijd kunnen duren.</span><span class="sxs-lookup"><span data-stu-id="06b81-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="06b81-109">Als uw bedrijf een datawarehouse bedrijfsniveau vereist, zijn Hallo voordelen waard Hallo inspanning.</span><span class="sxs-lookup"><span data-stu-id="06b81-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="06b81-110">Als u geen power Hallo van SQL Data Warehouse, is het echter meer rendabele toouse SQL Server of Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="06b81-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="06b81-111">Overweeg het gebruik van SQL Data Warehouse wanneer u:</span><span class="sxs-lookup"><span data-stu-id="06b81-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="06b81-112">Een of meer Terabytes aan gegevens hebben</span><span class="sxs-lookup"><span data-stu-id="06b81-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="06b81-113">Toorun analytics voor grote hoeveelheden gegevens plannen</span><span class="sxs-lookup"><span data-stu-id="06b81-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="06b81-114">Hallo mogelijkheid tooscale berekeningen en opslag nodig</span><span class="sxs-lookup"><span data-stu-id="06b81-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="06b81-115">Gewenste toosave kosten door onderbreken bronnen berekenen wanneer u ze niet nodig.</span><span class="sxs-lookup"><span data-stu-id="06b81-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="06b81-116">Gebruik geen SQL Data Warehouse voor operationele (OLTP-systemen)-werkbelastingen met:</span><span class="sxs-lookup"><span data-stu-id="06b81-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="06b81-117">Hoge frequentie leest en schrijft</span><span class="sxs-lookup"><span data-stu-id="06b81-117">High frequency reads and writes</span></span>
- <span data-ttu-id="06b81-118">Hiermee selecteert u een groot aantal singleton</span><span class="sxs-lookup"><span data-stu-id="06b81-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="06b81-119">Grote hoeveelheden één rij invoegen</span><span class="sxs-lookup"><span data-stu-id="06b81-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="06b81-120">Rij moet verwerken</span><span class="sxs-lookup"><span data-stu-id="06b81-120">Row by row processing needs</span></span>
- <span data-ttu-id="06b81-121">Niet-compatibele indeling (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="06b81-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="06b81-122">Hallo-migratie plannen</span><span class="sxs-lookup"><span data-stu-id="06b81-122">Plan hello migration</span></span>

<span data-ttu-id="06b81-123">Zodra u hebt besloten een bestaande oplossing tooSQL Data Warehouse toomigrate, is het belangrijk tooplan Hallo migratie voordat het aan de slag.</span><span class="sxs-lookup"><span data-stu-id="06b81-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="06b81-124">Een doel van de planning is tooensure uw gegevens, het tabelschema en uw code compatibel zijn met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06b81-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="06b81-125">Er zijn bepaalde verschillen toowork compatibiliteit tussen uw huidige systeem- en SQL Data Warehouse rond.</span><span class="sxs-lookup"><span data-stu-id="06b81-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="06b81-126">Plus, migreert u grote hoeveelheden gegevens tooAzure vergt tijd.</span><span class="sxs-lookup"><span data-stu-id="06b81-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="06b81-127">Een zorgvuldige planning versnelt uw tooAzure gegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="06b81-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="06b81-128">Een ander doel van de planning is toomake ontwerp aanpassingen tooensure die uw oplossing maakt gebruik van hoge queryprestaties Hallo die SQL Data Warehouse tooprovide ontworpen.</span><span class="sxs-lookup"><span data-stu-id="06b81-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="06b81-129">Ontwerppatronen voor verschillende ontwerpen van datawarehouses voor schaal introduceert en dus traditionele methoden zijn niet altijd Hallo beste.</span><span class="sxs-lookup"><span data-stu-id="06b81-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="06b81-130">Hoewel na de migratie kunt u bepaalde aanpassingen van het ontwerp, sneller wijzigingen aanbrengen in Hallo-proces op een later tijdstip, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="06b81-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="06b81-131">tooperform een geslaagde migratie, moet u toomigrate uw tabelschema, uw code en uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="06b81-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="06b81-132">Zie voor richtlijnen over deze migratieonderwerpen:</span><span class="sxs-lookup"><span data-stu-id="06b81-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="06b81-133">Uw schema's migreren</span><span class="sxs-lookup"><span data-stu-id="06b81-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="06b81-134">Uw code migreren</span><span class="sxs-lookup"><span data-stu-id="06b81-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="06b81-135">[Uw gegevens migreren](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="06b81-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="06b81-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="06b81-136">Next steps</span></span>
<span data-ttu-id="06b81-137">Hallo CAT (Customer Advisory Team) heeft ook enkele geweldige SQL Data Warehouse richtlijnen, ze via blogs publiceren.</span><span class="sxs-lookup"><span data-stu-id="06b81-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="06b81-138">Kijk eens naar hun artikel [migreren tooAzure SQL Data Warehouse-gegevens in de praktijk] [ Migrating data tooAzure SQL Data Warehouse in practice] voor aanvullende hulp bij de migratie.</span><span class="sxs-lookup"><span data-stu-id="06b81-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
