---
title: beheer van aaaConcurrency en de belasting in SQL Data Warehouse | Microsoft Docs
description: Begrijpen en de belasting van gelijktijdigheid management in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="d0344-103">Beheer van gelijktijdigheid van taken en de belasting in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0344-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="d0344-104">toodeliver voorspelbare prestaties op schaal, Microsoft Azure SQL Data Warehouse kunt u bepalen gelijktijdigheid niveaus en toewijzingen zoals geheugen en CPU-prioriteit.</span><span class="sxs-lookup"><span data-stu-id="d0344-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="d0344-105">In dit artikel vindt u toohello concepten van gelijktijdigheid en werkbelasting management, waarin wordt uitgelegd hoe u beide functies geïmplementeerd en hoe u ze kunt beheren in uw datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="d0344-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="d0344-106">Beheer van SQL Data Warehouse werkbelasting is beoogde toohelp omgeving met meerdere gebruikers die u ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="d0344-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="d0344-107">Het is niet bedoeld voor werkbelastingen van meerdere tenants.</span><span class="sxs-lookup"><span data-stu-id="d0344-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="d0344-108">Limieten voor gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="d0344-108">Concurrency limits</span></span>
<span data-ttu-id="d0344-109">SQL Data Warehouse kunt up too1, 024 gelijktijdige verbindingen.</span><span class="sxs-lookup"><span data-stu-id="d0344-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="d0344-110">Alle 1024 verbindingen kunnen query's tegelijk verzenden.</span><span class="sxs-lookup"><span data-stu-id="d0344-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="d0344-111">Toooptimize doorvoer, SQL Data Warehouse kan echter een aantal query's tooensure dat elke query een minimale geheugentoekenning ontvangt wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d0344-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="d0344-112">Queuing treedt op tijdens het uitvoeren van een query.</span><span class="sxs-lookup"><span data-stu-id="d0344-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="d0344-113">Wanneer gelijktijdigheid limieten zijn bereikt, SQL Data Warehouse kunt verhogen nodig totale doorvoer door ervoor te zorgen dat de actieve query's toocritically toegang krijgen door queuing query's geheugenbronnen.</span><span class="sxs-lookup"><span data-stu-id="d0344-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="d0344-114">Limieten voor gelijktijdigheid van taken worden bepaald door twee concepten: *gelijktijdige query's* en *gelijktijdigheid sleuven*.</span><span class="sxs-lookup"><span data-stu-id="d0344-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="d0344-115">Moet in een tooexecute query uitvoeren in zowel Hallo query gelijktijdigheid limiet en Hallo gelijktijdigheid sleuf toewijzing.</span><span class="sxs-lookup"><span data-stu-id="d0344-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="d0344-116">Gelijktijdige query's zijn Hallo query's uitvoeren op Hallo van dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="d0344-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="d0344-117">SQL Data Warehouse biedt ondersteuning voor maximaal too32 gelijktijdige query's op Hallo grotere DWU.</span><span class="sxs-lookup"><span data-stu-id="d0344-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="d0344-118">Gelijktijdigheid sleuven worden toegewezen op basis van DWU.</span><span class="sxs-lookup"><span data-stu-id="d0344-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="d0344-119">Elke DWU 100 biedt 4 gelijktijdigheid sleuven.</span><span class="sxs-lookup"><span data-stu-id="d0344-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="d0344-120">Bijvoorbeeld, een DW100 toewijst 4 gelijktijdigheid sleuven en DW1000 40 toewijst.</span><span class="sxs-lookup"><span data-stu-id="d0344-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="d0344-121">Elke query maakt gebruik van een of meer gelijktijdigheid sleuven, afhankelijk van Hallo [bronklasse](#resource-classes) van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="d0344-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="d0344-122">Query uitvoeren in Hallo smallrc bronklasse één gelijktijdigheid sleuf in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="d0344-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="d0344-123">Query uitvoeren in een hogere bronklasse verbruikt meer gelijktijdigheid sleuven.</span><span class="sxs-lookup"><span data-stu-id="d0344-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="d0344-124">Hallo volgende tabel beschrijft Hallo limieten voor gelijktijdige query's en gelijktijdigheid sleuven op Hallo verschillende grootten van DWU.</span><span class="sxs-lookup"><span data-stu-id="d0344-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="d0344-125">Limieten voor gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="d0344-125">Concurrency limits</span></span>
| <span data-ttu-id="d0344-126">DWU</span><span class="sxs-lookup"><span data-stu-id="d0344-126">DWU</span></span> | <span data-ttu-id="d0344-127">Maximum aantal gelijktijdige query 's</span><span class="sxs-lookup"><span data-stu-id="d0344-127">Max concurrent queries</span></span> | <span data-ttu-id="d0344-128">Gelijktijdigheid sleuven toegewezen</span><span class="sxs-lookup"><span data-stu-id="d0344-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="d0344-129">DW100</span><span class="sxs-lookup"><span data-stu-id="d0344-129">DW100</span></span> |<span data-ttu-id="d0344-130">4</span><span class="sxs-lookup"><span data-stu-id="d0344-130">4</span></span> |<span data-ttu-id="d0344-131">4</span><span class="sxs-lookup"><span data-stu-id="d0344-131">4</span></span> |
| <span data-ttu-id="d0344-132">DW200</span><span class="sxs-lookup"><span data-stu-id="d0344-132">DW200</span></span> |<span data-ttu-id="d0344-133">8</span><span class="sxs-lookup"><span data-stu-id="d0344-133">8</span></span> |<span data-ttu-id="d0344-134">8</span><span class="sxs-lookup"><span data-stu-id="d0344-134">8</span></span> |
| <span data-ttu-id="d0344-135">DW300</span><span class="sxs-lookup"><span data-stu-id="d0344-135">DW300</span></span> |<span data-ttu-id="d0344-136">12</span><span class="sxs-lookup"><span data-stu-id="d0344-136">12</span></span> |<span data-ttu-id="d0344-137">12</span><span class="sxs-lookup"><span data-stu-id="d0344-137">12</span></span> |
| <span data-ttu-id="d0344-138">DW400</span><span class="sxs-lookup"><span data-stu-id="d0344-138">DW400</span></span> |<span data-ttu-id="d0344-139">16</span><span class="sxs-lookup"><span data-stu-id="d0344-139">16</span></span> |<span data-ttu-id="d0344-140">16</span><span class="sxs-lookup"><span data-stu-id="d0344-140">16</span></span> |
| <span data-ttu-id="d0344-141">DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-141">DW500</span></span> |<span data-ttu-id="d0344-142">20</span><span class="sxs-lookup"><span data-stu-id="d0344-142">20</span></span> |<span data-ttu-id="d0344-143">20</span><span class="sxs-lookup"><span data-stu-id="d0344-143">20</span></span> |
| <span data-ttu-id="d0344-144">DW600</span><span class="sxs-lookup"><span data-stu-id="d0344-144">DW600</span></span> |<span data-ttu-id="d0344-145">24</span><span class="sxs-lookup"><span data-stu-id="d0344-145">24</span></span> |<span data-ttu-id="d0344-146">24</span><span class="sxs-lookup"><span data-stu-id="d0344-146">24</span></span> |
| <span data-ttu-id="d0344-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="d0344-147">DW1000</span></span> |<span data-ttu-id="d0344-148">32</span><span class="sxs-lookup"><span data-stu-id="d0344-148">32</span></span> |<span data-ttu-id="d0344-149">40</span><span class="sxs-lookup"><span data-stu-id="d0344-149">40</span></span> |
| <span data-ttu-id="d0344-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="d0344-150">DW1200</span></span> |<span data-ttu-id="d0344-151">32</span><span class="sxs-lookup"><span data-stu-id="d0344-151">32</span></span> |<span data-ttu-id="d0344-152">48</span><span class="sxs-lookup"><span data-stu-id="d0344-152">48</span></span> |
| <span data-ttu-id="d0344-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="d0344-153">DW1500</span></span> |<span data-ttu-id="d0344-154">32</span><span class="sxs-lookup"><span data-stu-id="d0344-154">32</span></span> |<span data-ttu-id="d0344-155">60</span><span class="sxs-lookup"><span data-stu-id="d0344-155">60</span></span> |
| <span data-ttu-id="d0344-156">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="d0344-156">DW2000</span></span> |<span data-ttu-id="d0344-157">32</span><span class="sxs-lookup"><span data-stu-id="d0344-157">32</span></span> |<span data-ttu-id="d0344-158">80</span><span class="sxs-lookup"><span data-stu-id="d0344-158">80</span></span> |
| <span data-ttu-id="d0344-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="d0344-159">DW3000</span></span> |<span data-ttu-id="d0344-160">32</span><span class="sxs-lookup"><span data-stu-id="d0344-160">32</span></span> |<span data-ttu-id="d0344-161">120</span><span class="sxs-lookup"><span data-stu-id="d0344-161">120</span></span> |
| <span data-ttu-id="d0344-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="d0344-162">DW6000</span></span> |<span data-ttu-id="d0344-163">32</span><span class="sxs-lookup"><span data-stu-id="d0344-163">32</span></span> |<span data-ttu-id="d0344-164">240</span><span class="sxs-lookup"><span data-stu-id="d0344-164">240</span></span> |

<span data-ttu-id="d0344-165">Als een van deze drempels wordt voldaan, worden de nieuwe query's in de wachtrij en de eerste in, First-out ' op basis van een uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="d0344-166">Als een query's is voltooid en Hallo aantal query's en sleuven onder Hallo limieten valt, worden in de wachtrij query's vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="d0344-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="d0344-167">*Selecteer* query's uitvoeren op uitsluitend dynamische Beheerweergave bekijkt (DMV's) of catalogusweergaven niet worden geregeld door een Hallo gelijktijdigheid limieten.</span><span class="sxs-lookup"><span data-stu-id="d0344-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="d0344-168">U kunt system ongeacht het aantal query's uitvoeren op het Hallo Hallo bewaken.</span><span class="sxs-lookup"><span data-stu-id="d0344-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="d0344-169">Resource-klassen</span><span class="sxs-lookup"><span data-stu-id="d0344-169">Resource classes</span></span>
<span data-ttu-id="d0344-170">Resource klassen help bepaalt u de toewijzing van geheugen en CPU-cycli tooa query opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d0344-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="d0344-171">U kunt twee soorten resource klassen tooa gebruiker in Hallo vorm databaserollen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d0344-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="d0344-172">Hallo twee soorten resource klassen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="d0344-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="d0344-173">Dynamische Resource-klassen (**smallrc, mediumrc, largerc, xlargerc**) toewijzen van een variabele hoeveelheid geheugen, afhankelijk van Hallo huidige DWU.</span><span class="sxs-lookup"><span data-stu-id="d0344-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="d0344-174">Dit betekent dat wanneer u tooa opschalen groter DWU uw query's ophalen automatisch meer geheugen.</span><span class="sxs-lookup"><span data-stu-id="d0344-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="d0344-175">Statische Resource-klassen (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) toewijzen Hallo dezelfde hoeveelheid geheugen ongeacht de huidige DWU Hallo (mits Hallo DWU zelf onvoldoende geheugen beschikbaar heeft.)</span><span class="sxs-lookup"><span data-stu-id="d0344-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="d0344-176">Dit betekent dat op een groter aantal dwu's, u meer query's in elke bronklasse gelijktijdig uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="d0344-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="d0344-177">Gebruikers in **smallrc** en **staticrc10** krijgen een kleinere hoeveelheid geheugen en kunnen profiteren van de hogere gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="d0344-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="d0344-178">Gebruikers toegewezen daarentegen te**xlargerc** of **staticrc80** grote hoeveelheden geheugen, zijn opgegeven en daarom minder van de query's kunnen tegelijkertijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="d0344-179">Standaard is elke gebruiker een lid van Hallo kleine bronklasse, **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="d0344-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="d0344-180">Hallo procedure `sp_addrolemember` is tooincrease Hallo bronklasse, gebruikt en `sp_droprolemember` is toodecrease Hallo bronklasse gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0344-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="d0344-181">Zou deze opdracht Hallo bronklasse van loaduser bijvoorbeeld te verhogen**largerc**:</span><span class="sxs-lookup"><span data-stu-id="d0344-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="d0344-182">Query's die niet voldoen aan voor resource-klassen</span><span class="sxs-lookup"><span data-stu-id="d0344-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="d0344-183">Er zijn enkele typen query's die niet van een grotere geheugentoewijzing profiteren.</span><span class="sxs-lookup"><span data-stu-id="d0344-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="d0344-184">Hallo system hun klasse resourcetoewijzing negeert en voer deze query's altijd in plaats daarvan in Hallo kleine bronklasse.</span><span class="sxs-lookup"><span data-stu-id="d0344-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="d0344-185">Als deze query's worden altijd uitgevoerd in de kleine bronklasse Hallo, kunnen ze worden uitgevoerd wanneer gelijktijdigheid sleuven onder druk zijn en ze meer sleuven dan nodig won't verbruiken.</span><span class="sxs-lookup"><span data-stu-id="d0344-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="d0344-186">Zie [Resource klasse uitzonderingen](#query-exceptions-to-concurrency-limits) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d0344-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="d0344-187">Meer informatie over klasse resourcetoewijzing</span><span class="sxs-lookup"><span data-stu-id="d0344-187">Details on resource class assignment</span></span>


<span data-ttu-id="d0344-188">Enkele meer informatie over de bronklasse:</span><span class="sxs-lookup"><span data-stu-id="d0344-188">A few more details on resource class:</span></span>

* <span data-ttu-id="d0344-189">*Rol ALTER* machtiging is vereist toochange Hallo bronklasse van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d0344-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="d0344-190">Hoewel u een gebruiker tooone of meer van de Hallo hogere resource klassen toevoegen kunt, voorrang dynamische Bronklassen statische resource klassen.</span><span class="sxs-lookup"><span data-stu-id="d0344-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="d0344-191">Dat wil zeggen, als een gebruiker is toegewezen tooboth **mediumrc**(dynamische) en **staticrc80**(statische) **mediumrc** Hallo resource klasse die wordt gehonoreerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="d0344-192">Wanneer een gebruiker toomore dan één resource-klasse in een specifieke klasse brontype (meer dan één dynamische bronklasse of meer dan één statische bronklasse) toegewezen wordt, wordt de hoogste bronklasse Hallo gehonoreerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="d0344-193">Dat wil zeggen, als een gebruiker is toegewezen tooboth mediumrc en largerc, is hoger bronklasse hello (largerc) gehonoreerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="d0344-194">En als een gebruiker is toegewezen tooboth **staticrc20** en **statirc80**, **staticrc80** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0344-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="d0344-195">De bronklasse Hallo van gebruiker met beheerdersrechten Hallo system kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d0344-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="d0344-196">Zie voor een gedetailleerd voorbeeld [Changing gebruiker resource klasse voorbeeld](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d0344-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="d0344-197">Toewijzing van geheugen</span><span class="sxs-lookup"><span data-stu-id="d0344-197">Memory allocation</span></span>
<span data-ttu-id="d0344-198">Er zijn voor- en nadelen tooincreasing bronklasse van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d0344-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="d0344-199">Een bronklasse voor een gebruiker stijgt, biedt de query's toegang toomore geheugen, wat kan betekenen dat query's sneller uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="d0344-200">Hogere resource klassen Verminder echter ook Hallo aantal gelijktijdige query's die kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="d0344-201">Dit is Hallo compromis tussen het toewijzen van grote hoeveelheden geheugen tooa één query of andere query's, die ook geheugentoewijzingen, toorun gelijktijdig moeten toestaan.</span><span class="sxs-lookup"><span data-stu-id="d0344-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="d0344-202">Als een gebruiker hoge toewijzingen van geheugen voor een query krijgt, andere gebruikers geen toegang toothat dezelfde geheugen toorun een query.</span><span class="sxs-lookup"><span data-stu-id="d0344-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="d0344-203">Hallo tabel maps Hallo geheugen toegewezen tooeach distributie door DWU en resource-klasse.</span><span class="sxs-lookup"><span data-stu-id="d0344-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="d0344-204">Geheugentoewijzingen per distributiepunt voor dynamische Bronklassen (MB)</span><span class="sxs-lookup"><span data-stu-id="d0344-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="d0344-205">DWU</span><span class="sxs-lookup"><span data-stu-id="d0344-205">DWU</span></span> | <span data-ttu-id="d0344-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="d0344-206">smallrc</span></span> | <span data-ttu-id="d0344-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="d0344-207">mediumrc</span></span> | <span data-ttu-id="d0344-208">largerc</span><span class="sxs-lookup"><span data-stu-id="d0344-208">largerc</span></span> | <span data-ttu-id="d0344-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="d0344-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="d0344-210">DW100</span><span class="sxs-lookup"><span data-stu-id="d0344-210">DW100</span></span> |<span data-ttu-id="d0344-211">100</span><span class="sxs-lookup"><span data-stu-id="d0344-211">100</span></span> |<span data-ttu-id="d0344-212">100</span><span class="sxs-lookup"><span data-stu-id="d0344-212">100</span></span> |<span data-ttu-id="d0344-213">200</span><span class="sxs-lookup"><span data-stu-id="d0344-213">200</span></span> |<span data-ttu-id="d0344-214">400</span><span class="sxs-lookup"><span data-stu-id="d0344-214">400</span></span> |
| <span data-ttu-id="d0344-215">DW200</span><span class="sxs-lookup"><span data-stu-id="d0344-215">DW200</span></span> |<span data-ttu-id="d0344-216">100</span><span class="sxs-lookup"><span data-stu-id="d0344-216">100</span></span> |<span data-ttu-id="d0344-217">200</span><span class="sxs-lookup"><span data-stu-id="d0344-217">200</span></span> |<span data-ttu-id="d0344-218">400</span><span class="sxs-lookup"><span data-stu-id="d0344-218">400</span></span> |<span data-ttu-id="d0344-219">800</span><span class="sxs-lookup"><span data-stu-id="d0344-219">800</span></span> |
| <span data-ttu-id="d0344-220">DW300</span><span class="sxs-lookup"><span data-stu-id="d0344-220">DW300</span></span> |<span data-ttu-id="d0344-221">100</span><span class="sxs-lookup"><span data-stu-id="d0344-221">100</span></span> |<span data-ttu-id="d0344-222">200</span><span class="sxs-lookup"><span data-stu-id="d0344-222">200</span></span> |<span data-ttu-id="d0344-223">400</span><span class="sxs-lookup"><span data-stu-id="d0344-223">400</span></span> |<span data-ttu-id="d0344-224">800</span><span class="sxs-lookup"><span data-stu-id="d0344-224">800</span></span> |
| <span data-ttu-id="d0344-225">DW400</span><span class="sxs-lookup"><span data-stu-id="d0344-225">DW400</span></span> |<span data-ttu-id="d0344-226">100</span><span class="sxs-lookup"><span data-stu-id="d0344-226">100</span></span> |<span data-ttu-id="d0344-227">400</span><span class="sxs-lookup"><span data-stu-id="d0344-227">400</span></span> |<span data-ttu-id="d0344-228">800</span><span class="sxs-lookup"><span data-stu-id="d0344-228">800</span></span> |<span data-ttu-id="d0344-229">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-229">1,600</span></span> |
| <span data-ttu-id="d0344-230">DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-230">DW500</span></span> |<span data-ttu-id="d0344-231">100</span><span class="sxs-lookup"><span data-stu-id="d0344-231">100</span></span> |<span data-ttu-id="d0344-232">400</span><span class="sxs-lookup"><span data-stu-id="d0344-232">400</span></span> |<span data-ttu-id="d0344-233">800</span><span class="sxs-lookup"><span data-stu-id="d0344-233">800</span></span> |<span data-ttu-id="d0344-234">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-234">1,600</span></span> |
| <span data-ttu-id="d0344-235">DW600</span><span class="sxs-lookup"><span data-stu-id="d0344-235">DW600</span></span> |<span data-ttu-id="d0344-236">100</span><span class="sxs-lookup"><span data-stu-id="d0344-236">100</span></span> |<span data-ttu-id="d0344-237">400</span><span class="sxs-lookup"><span data-stu-id="d0344-237">400</span></span> |<span data-ttu-id="d0344-238">800</span><span class="sxs-lookup"><span data-stu-id="d0344-238">800</span></span> |<span data-ttu-id="d0344-239">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-239">1,600</span></span> |
| <span data-ttu-id="d0344-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="d0344-240">DW1000</span></span> |<span data-ttu-id="d0344-241">100</span><span class="sxs-lookup"><span data-stu-id="d0344-241">100</span></span> |<span data-ttu-id="d0344-242">800</span><span class="sxs-lookup"><span data-stu-id="d0344-242">800</span></span> |<span data-ttu-id="d0344-243">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-243">1,600</span></span> |<span data-ttu-id="d0344-244">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-244">3,200</span></span> |
| <span data-ttu-id="d0344-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="d0344-245">DW1200</span></span> |<span data-ttu-id="d0344-246">100</span><span class="sxs-lookup"><span data-stu-id="d0344-246">100</span></span> |<span data-ttu-id="d0344-247">800</span><span class="sxs-lookup"><span data-stu-id="d0344-247">800</span></span> |<span data-ttu-id="d0344-248">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-248">1,600</span></span> |<span data-ttu-id="d0344-249">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-249">3,200</span></span> |
| <span data-ttu-id="d0344-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="d0344-250">DW1500</span></span> |<span data-ttu-id="d0344-251">100</span><span class="sxs-lookup"><span data-stu-id="d0344-251">100</span></span> |<span data-ttu-id="d0344-252">800</span><span class="sxs-lookup"><span data-stu-id="d0344-252">800</span></span> |<span data-ttu-id="d0344-253">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-253">1,600</span></span> |<span data-ttu-id="d0344-254">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-254">3,200</span></span> |
| <span data-ttu-id="d0344-255">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="d0344-255">DW2000</span></span> |<span data-ttu-id="d0344-256">100</span><span class="sxs-lookup"><span data-stu-id="d0344-256">100</span></span> |<span data-ttu-id="d0344-257">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-257">1,600</span></span> |<span data-ttu-id="d0344-258">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-258">3,200</span></span> |<span data-ttu-id="d0344-259">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-259">6,400</span></span> |
| <span data-ttu-id="d0344-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="d0344-260">DW3000</span></span> |<span data-ttu-id="d0344-261">100</span><span class="sxs-lookup"><span data-stu-id="d0344-261">100</span></span> |<span data-ttu-id="d0344-262">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-262">1,600</span></span> |<span data-ttu-id="d0344-263">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-263">3,200</span></span> |<span data-ttu-id="d0344-264">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-264">6,400</span></span> |
| <span data-ttu-id="d0344-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="d0344-265">DW6000</span></span> |<span data-ttu-id="d0344-266">100</span><span class="sxs-lookup"><span data-stu-id="d0344-266">100</span></span> |<span data-ttu-id="d0344-267">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-267">3,200</span></span> |<span data-ttu-id="d0344-268">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-268">6,400</span></span> |<span data-ttu-id="d0344-269">12,800</span><span class="sxs-lookup"><span data-stu-id="d0344-269">12,800</span></span> |

<span data-ttu-id="d0344-270">Hallo tabel maps Hallo geheugen toegewezen tooeach distributie door DWU en statische bronklasse.</span><span class="sxs-lookup"><span data-stu-id="d0344-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="d0344-271">Opmerking dat Hallo hogere resource klassen hun geheugen hebben verminderd toohonor Hallo globale DWU limieten.</span><span class="sxs-lookup"><span data-stu-id="d0344-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="d0344-272">Geheugentoewijzingen per distributiepunt voor statische resource klassen (MB)</span><span class="sxs-lookup"><span data-stu-id="d0344-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="d0344-273">DWU</span><span class="sxs-lookup"><span data-stu-id="d0344-273">DWU</span></span> | <span data-ttu-id="d0344-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="d0344-274">staticrc10</span></span> | <span data-ttu-id="d0344-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="d0344-275">staticrc20</span></span> | <span data-ttu-id="d0344-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="d0344-276">staticrc30</span></span> | <span data-ttu-id="d0344-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="d0344-277">staticrc40</span></span> | <span data-ttu-id="d0344-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="d0344-278">staticrc50</span></span> | <span data-ttu-id="d0344-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="d0344-279">staticrc60</span></span> | <span data-ttu-id="d0344-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="d0344-280">staticrc70</span></span> | <span data-ttu-id="d0344-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="d0344-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="d0344-282">DW100</span><span class="sxs-lookup"><span data-stu-id="d0344-282">DW100</span></span> |<span data-ttu-id="d0344-283">100</span><span class="sxs-lookup"><span data-stu-id="d0344-283">100</span></span> |<span data-ttu-id="d0344-284">200</span><span class="sxs-lookup"><span data-stu-id="d0344-284">200</span></span> |<span data-ttu-id="d0344-285">400</span><span class="sxs-lookup"><span data-stu-id="d0344-285">400</span></span> |<span data-ttu-id="d0344-286">400</span><span class="sxs-lookup"><span data-stu-id="d0344-286">400</span></span> |<span data-ttu-id="d0344-287">400</span><span class="sxs-lookup"><span data-stu-id="d0344-287">400</span></span> |<span data-ttu-id="d0344-288">400</span><span class="sxs-lookup"><span data-stu-id="d0344-288">400</span></span> |<span data-ttu-id="d0344-289">400</span><span class="sxs-lookup"><span data-stu-id="d0344-289">400</span></span> |<span data-ttu-id="d0344-290">400</span><span class="sxs-lookup"><span data-stu-id="d0344-290">400</span></span> |
| <span data-ttu-id="d0344-291">DW200</span><span class="sxs-lookup"><span data-stu-id="d0344-291">DW200</span></span> |<span data-ttu-id="d0344-292">100</span><span class="sxs-lookup"><span data-stu-id="d0344-292">100</span></span> |<span data-ttu-id="d0344-293">200</span><span class="sxs-lookup"><span data-stu-id="d0344-293">200</span></span> |<span data-ttu-id="d0344-294">400</span><span class="sxs-lookup"><span data-stu-id="d0344-294">400</span></span> |<span data-ttu-id="d0344-295">800</span><span class="sxs-lookup"><span data-stu-id="d0344-295">800</span></span> |<span data-ttu-id="d0344-296">800</span><span class="sxs-lookup"><span data-stu-id="d0344-296">800</span></span> |<span data-ttu-id="d0344-297">800</span><span class="sxs-lookup"><span data-stu-id="d0344-297">800</span></span> |<span data-ttu-id="d0344-298">800</span><span class="sxs-lookup"><span data-stu-id="d0344-298">800</span></span> |<span data-ttu-id="d0344-299">800</span><span class="sxs-lookup"><span data-stu-id="d0344-299">800</span></span> |
| <span data-ttu-id="d0344-300">DW300</span><span class="sxs-lookup"><span data-stu-id="d0344-300">DW300</span></span> |<span data-ttu-id="d0344-301">100</span><span class="sxs-lookup"><span data-stu-id="d0344-301">100</span></span> |<span data-ttu-id="d0344-302">200</span><span class="sxs-lookup"><span data-stu-id="d0344-302">200</span></span> |<span data-ttu-id="d0344-303">400</span><span class="sxs-lookup"><span data-stu-id="d0344-303">400</span></span> |<span data-ttu-id="d0344-304">800</span><span class="sxs-lookup"><span data-stu-id="d0344-304">800</span></span> |<span data-ttu-id="d0344-305">800</span><span class="sxs-lookup"><span data-stu-id="d0344-305">800</span></span> |<span data-ttu-id="d0344-306">800</span><span class="sxs-lookup"><span data-stu-id="d0344-306">800</span></span> |<span data-ttu-id="d0344-307">800</span><span class="sxs-lookup"><span data-stu-id="d0344-307">800</span></span> |<span data-ttu-id="d0344-308">800</span><span class="sxs-lookup"><span data-stu-id="d0344-308">800</span></span> |
| <span data-ttu-id="d0344-309">DW400</span><span class="sxs-lookup"><span data-stu-id="d0344-309">DW400</span></span> |<span data-ttu-id="d0344-310">100</span><span class="sxs-lookup"><span data-stu-id="d0344-310">100</span></span> |<span data-ttu-id="d0344-311">200</span><span class="sxs-lookup"><span data-stu-id="d0344-311">200</span></span> |<span data-ttu-id="d0344-312">400</span><span class="sxs-lookup"><span data-stu-id="d0344-312">400</span></span> |<span data-ttu-id="d0344-313">800</span><span class="sxs-lookup"><span data-stu-id="d0344-313">800</span></span> |<span data-ttu-id="d0344-314">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-314">1,600</span></span> |<span data-ttu-id="d0344-315">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-315">1,600</span></span> |<span data-ttu-id="d0344-316">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-316">1,600</span></span> |<span data-ttu-id="d0344-317">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-317">1,600</span></span> |
| <span data-ttu-id="d0344-318">DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-318">DW500</span></span> |<span data-ttu-id="d0344-319">100</span><span class="sxs-lookup"><span data-stu-id="d0344-319">100</span></span> |<span data-ttu-id="d0344-320">200</span><span class="sxs-lookup"><span data-stu-id="d0344-320">200</span></span> |<span data-ttu-id="d0344-321">400</span><span class="sxs-lookup"><span data-stu-id="d0344-321">400</span></span> |<span data-ttu-id="d0344-322">800</span><span class="sxs-lookup"><span data-stu-id="d0344-322">800</span></span> |<span data-ttu-id="d0344-323">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-323">1,600</span></span> |<span data-ttu-id="d0344-324">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-324">1,600</span></span> |<span data-ttu-id="d0344-325">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-325">1,600</span></span> |<span data-ttu-id="d0344-326">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-326">1,600</span></span> |
| <span data-ttu-id="d0344-327">DW600</span><span class="sxs-lookup"><span data-stu-id="d0344-327">DW600</span></span> |<span data-ttu-id="d0344-328">100</span><span class="sxs-lookup"><span data-stu-id="d0344-328">100</span></span> |<span data-ttu-id="d0344-329">200</span><span class="sxs-lookup"><span data-stu-id="d0344-329">200</span></span> |<span data-ttu-id="d0344-330">400</span><span class="sxs-lookup"><span data-stu-id="d0344-330">400</span></span> |<span data-ttu-id="d0344-331">800</span><span class="sxs-lookup"><span data-stu-id="d0344-331">800</span></span> |<span data-ttu-id="d0344-332">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-332">1,600</span></span> |<span data-ttu-id="d0344-333">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-333">1,600</span></span> |<span data-ttu-id="d0344-334">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-334">1,600</span></span> |<span data-ttu-id="d0344-335">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-335">1,600</span></span> |
| <span data-ttu-id="d0344-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="d0344-336">DW1000</span></span> |<span data-ttu-id="d0344-337">100</span><span class="sxs-lookup"><span data-stu-id="d0344-337">100</span></span> |<span data-ttu-id="d0344-338">200</span><span class="sxs-lookup"><span data-stu-id="d0344-338">200</span></span> |<span data-ttu-id="d0344-339">400</span><span class="sxs-lookup"><span data-stu-id="d0344-339">400</span></span> |<span data-ttu-id="d0344-340">800</span><span class="sxs-lookup"><span data-stu-id="d0344-340">800</span></span> |<span data-ttu-id="d0344-341">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-341">1,600</span></span> |<span data-ttu-id="d0344-342">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-342">3,200</span></span> |<span data-ttu-id="d0344-343">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-343">3,200</span></span> |<span data-ttu-id="d0344-344">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-344">3,200</span></span> |
| <span data-ttu-id="d0344-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="d0344-345">DW1200</span></span> |<span data-ttu-id="d0344-346">100</span><span class="sxs-lookup"><span data-stu-id="d0344-346">100</span></span> |<span data-ttu-id="d0344-347">200</span><span class="sxs-lookup"><span data-stu-id="d0344-347">200</span></span> |<span data-ttu-id="d0344-348">400</span><span class="sxs-lookup"><span data-stu-id="d0344-348">400</span></span> |<span data-ttu-id="d0344-349">800</span><span class="sxs-lookup"><span data-stu-id="d0344-349">800</span></span> |<span data-ttu-id="d0344-350">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-350">1,600</span></span> |<span data-ttu-id="d0344-351">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-351">3,200</span></span> |<span data-ttu-id="d0344-352">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-352">3,200</span></span> |<span data-ttu-id="d0344-353">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-353">3,200</span></span> |
| <span data-ttu-id="d0344-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="d0344-354">DW1500</span></span> |<span data-ttu-id="d0344-355">100</span><span class="sxs-lookup"><span data-stu-id="d0344-355">100</span></span> |<span data-ttu-id="d0344-356">200</span><span class="sxs-lookup"><span data-stu-id="d0344-356">200</span></span> |<span data-ttu-id="d0344-357">400</span><span class="sxs-lookup"><span data-stu-id="d0344-357">400</span></span> |<span data-ttu-id="d0344-358">800</span><span class="sxs-lookup"><span data-stu-id="d0344-358">800</span></span> |<span data-ttu-id="d0344-359">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-359">1,600</span></span> |<span data-ttu-id="d0344-360">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-360">3,200</span></span> |<span data-ttu-id="d0344-361">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-361">3,200</span></span> |<span data-ttu-id="d0344-362">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-362">3,200</span></span> |
| <span data-ttu-id="d0344-363">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="d0344-363">DW2000</span></span> |<span data-ttu-id="d0344-364">100</span><span class="sxs-lookup"><span data-stu-id="d0344-364">100</span></span> |<span data-ttu-id="d0344-365">200</span><span class="sxs-lookup"><span data-stu-id="d0344-365">200</span></span> |<span data-ttu-id="d0344-366">400</span><span class="sxs-lookup"><span data-stu-id="d0344-366">400</span></span> |<span data-ttu-id="d0344-367">800</span><span class="sxs-lookup"><span data-stu-id="d0344-367">800</span></span> |<span data-ttu-id="d0344-368">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-368">1,600</span></span> |<span data-ttu-id="d0344-369">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-369">3,200</span></span> |<span data-ttu-id="d0344-370">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-370">6,400</span></span> |<span data-ttu-id="d0344-371">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-371">6,400</span></span> |
| <span data-ttu-id="d0344-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="d0344-372">DW3000</span></span> |<span data-ttu-id="d0344-373">100</span><span class="sxs-lookup"><span data-stu-id="d0344-373">100</span></span> |<span data-ttu-id="d0344-374">200</span><span class="sxs-lookup"><span data-stu-id="d0344-374">200</span></span> |<span data-ttu-id="d0344-375">400</span><span class="sxs-lookup"><span data-stu-id="d0344-375">400</span></span> |<span data-ttu-id="d0344-376">800</span><span class="sxs-lookup"><span data-stu-id="d0344-376">800</span></span> |<span data-ttu-id="d0344-377">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-377">1,600</span></span> |<span data-ttu-id="d0344-378">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-378">3,200</span></span> |<span data-ttu-id="d0344-379">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-379">6,400</span></span> |<span data-ttu-id="d0344-380">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-380">6,400</span></span> |
| <span data-ttu-id="d0344-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="d0344-381">DW6000</span></span> |<span data-ttu-id="d0344-382">100</span><span class="sxs-lookup"><span data-stu-id="d0344-382">100</span></span> |<span data-ttu-id="d0344-383">200</span><span class="sxs-lookup"><span data-stu-id="d0344-383">200</span></span> |<span data-ttu-id="d0344-384">400</span><span class="sxs-lookup"><span data-stu-id="d0344-384">400</span></span> |<span data-ttu-id="d0344-385">800</span><span class="sxs-lookup"><span data-stu-id="d0344-385">800</span></span> |<span data-ttu-id="d0344-386">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-386">1,600</span></span> |<span data-ttu-id="d0344-387">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-387">3,200</span></span> |<span data-ttu-id="d0344-388">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-388">6,400</span></span> |<span data-ttu-id="d0344-389">12,800</span><span class="sxs-lookup"><span data-stu-id="d0344-389">12,800</span></span> |

<span data-ttu-id="d0344-390">Van Hallo voorafgaand aan de tabel, kunt u zien dat een query uitgevoerd op een dw2000 zijn in Hallo **xlargerc** bronklasse toegang too6, 400 MB aan geheugen binnen elke 60 gedistribueerde databases Hallo zou hebben.</span><span class="sxs-lookup"><span data-stu-id="d0344-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="d0344-391">In SQL Data Warehouse zijn er 60 distributies.</span><span class="sxs-lookup"><span data-stu-id="d0344-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="d0344-392">Daarom moet toocalculate Hallo totale geheugentoewijzing voor een query in een bepaalde bron-klasse, Hallo hierboven waarden worden vermenigvuldigd met 60.</span><span class="sxs-lookup"><span data-stu-id="d0344-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="d0344-393">Geheugen toewijzingen hele systeem (GB)</span><span class="sxs-lookup"><span data-stu-id="d0344-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="d0344-394">DWU</span><span class="sxs-lookup"><span data-stu-id="d0344-394">DWU</span></span> | <span data-ttu-id="d0344-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="d0344-395">smallrc</span></span> | <span data-ttu-id="d0344-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="d0344-396">mediumrc</span></span> | <span data-ttu-id="d0344-397">largerc</span><span class="sxs-lookup"><span data-stu-id="d0344-397">largerc</span></span> | <span data-ttu-id="d0344-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="d0344-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="d0344-399">DW100</span><span class="sxs-lookup"><span data-stu-id="d0344-399">DW100</span></span> |<span data-ttu-id="d0344-400">6</span><span class="sxs-lookup"><span data-stu-id="d0344-400">6</span></span> |<span data-ttu-id="d0344-401">6</span><span class="sxs-lookup"><span data-stu-id="d0344-401">6</span></span> |<span data-ttu-id="d0344-402">12</span><span class="sxs-lookup"><span data-stu-id="d0344-402">12</span></span> |<span data-ttu-id="d0344-403">23</span><span class="sxs-lookup"><span data-stu-id="d0344-403">23</span></span> |
| <span data-ttu-id="d0344-404">DW200</span><span class="sxs-lookup"><span data-stu-id="d0344-404">DW200</span></span> |<span data-ttu-id="d0344-405">6</span><span class="sxs-lookup"><span data-stu-id="d0344-405">6</span></span> |<span data-ttu-id="d0344-406">12</span><span class="sxs-lookup"><span data-stu-id="d0344-406">12</span></span> |<span data-ttu-id="d0344-407">23</span><span class="sxs-lookup"><span data-stu-id="d0344-407">23</span></span> |<span data-ttu-id="d0344-408">47</span><span class="sxs-lookup"><span data-stu-id="d0344-408">47</span></span> |
| <span data-ttu-id="d0344-409">DW300</span><span class="sxs-lookup"><span data-stu-id="d0344-409">DW300</span></span> |<span data-ttu-id="d0344-410">6</span><span class="sxs-lookup"><span data-stu-id="d0344-410">6</span></span> |<span data-ttu-id="d0344-411">12</span><span class="sxs-lookup"><span data-stu-id="d0344-411">12</span></span> |<span data-ttu-id="d0344-412">23</span><span class="sxs-lookup"><span data-stu-id="d0344-412">23</span></span> |<span data-ttu-id="d0344-413">47</span><span class="sxs-lookup"><span data-stu-id="d0344-413">47</span></span> |
| <span data-ttu-id="d0344-414">DW400</span><span class="sxs-lookup"><span data-stu-id="d0344-414">DW400</span></span> |<span data-ttu-id="d0344-415">6</span><span class="sxs-lookup"><span data-stu-id="d0344-415">6</span></span> |<span data-ttu-id="d0344-416">23</span><span class="sxs-lookup"><span data-stu-id="d0344-416">23</span></span> |<span data-ttu-id="d0344-417">47</span><span class="sxs-lookup"><span data-stu-id="d0344-417">47</span></span> |<span data-ttu-id="d0344-418">94</span><span class="sxs-lookup"><span data-stu-id="d0344-418">94</span></span> |
| <span data-ttu-id="d0344-419">DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-419">DW500</span></span> |<span data-ttu-id="d0344-420">6</span><span class="sxs-lookup"><span data-stu-id="d0344-420">6</span></span> |<span data-ttu-id="d0344-421">23</span><span class="sxs-lookup"><span data-stu-id="d0344-421">23</span></span> |<span data-ttu-id="d0344-422">47</span><span class="sxs-lookup"><span data-stu-id="d0344-422">47</span></span> |<span data-ttu-id="d0344-423">94</span><span class="sxs-lookup"><span data-stu-id="d0344-423">94</span></span> |
| <span data-ttu-id="d0344-424">DW600</span><span class="sxs-lookup"><span data-stu-id="d0344-424">DW600</span></span> |<span data-ttu-id="d0344-425">6</span><span class="sxs-lookup"><span data-stu-id="d0344-425">6</span></span> |<span data-ttu-id="d0344-426">23</span><span class="sxs-lookup"><span data-stu-id="d0344-426">23</span></span> |<span data-ttu-id="d0344-427">47</span><span class="sxs-lookup"><span data-stu-id="d0344-427">47</span></span> |<span data-ttu-id="d0344-428">94</span><span class="sxs-lookup"><span data-stu-id="d0344-428">94</span></span> |
| <span data-ttu-id="d0344-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="d0344-429">DW1000</span></span> |<span data-ttu-id="d0344-430">6</span><span class="sxs-lookup"><span data-stu-id="d0344-430">6</span></span> |<span data-ttu-id="d0344-431">47</span><span class="sxs-lookup"><span data-stu-id="d0344-431">47</span></span> |<span data-ttu-id="d0344-432">94</span><span class="sxs-lookup"><span data-stu-id="d0344-432">94</span></span> |<span data-ttu-id="d0344-433">188</span><span class="sxs-lookup"><span data-stu-id="d0344-433">188</span></span> |
| <span data-ttu-id="d0344-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="d0344-434">DW1200</span></span> |<span data-ttu-id="d0344-435">6</span><span class="sxs-lookup"><span data-stu-id="d0344-435">6</span></span> |<span data-ttu-id="d0344-436">47</span><span class="sxs-lookup"><span data-stu-id="d0344-436">47</span></span> |<span data-ttu-id="d0344-437">94</span><span class="sxs-lookup"><span data-stu-id="d0344-437">94</span></span> |<span data-ttu-id="d0344-438">188</span><span class="sxs-lookup"><span data-stu-id="d0344-438">188</span></span> |
| <span data-ttu-id="d0344-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="d0344-439">DW1500</span></span> |<span data-ttu-id="d0344-440">6</span><span class="sxs-lookup"><span data-stu-id="d0344-440">6</span></span> |<span data-ttu-id="d0344-441">47</span><span class="sxs-lookup"><span data-stu-id="d0344-441">47</span></span> |<span data-ttu-id="d0344-442">94</span><span class="sxs-lookup"><span data-stu-id="d0344-442">94</span></span> |<span data-ttu-id="d0344-443">188</span><span class="sxs-lookup"><span data-stu-id="d0344-443">188</span></span> |
| <span data-ttu-id="d0344-444">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="d0344-444">DW2000</span></span> |<span data-ttu-id="d0344-445">6</span><span class="sxs-lookup"><span data-stu-id="d0344-445">6</span></span> |<span data-ttu-id="d0344-446">94</span><span class="sxs-lookup"><span data-stu-id="d0344-446">94</span></span> |<span data-ttu-id="d0344-447">188</span><span class="sxs-lookup"><span data-stu-id="d0344-447">188</span></span> |<span data-ttu-id="d0344-448">375</span><span class="sxs-lookup"><span data-stu-id="d0344-448">375</span></span> |
| <span data-ttu-id="d0344-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="d0344-449">DW3000</span></span> |<span data-ttu-id="d0344-450">6</span><span class="sxs-lookup"><span data-stu-id="d0344-450">6</span></span> |<span data-ttu-id="d0344-451">94</span><span class="sxs-lookup"><span data-stu-id="d0344-451">94</span></span> |<span data-ttu-id="d0344-452">188</span><span class="sxs-lookup"><span data-stu-id="d0344-452">188</span></span> |<span data-ttu-id="d0344-453">375</span><span class="sxs-lookup"><span data-stu-id="d0344-453">375</span></span> |
| <span data-ttu-id="d0344-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="d0344-454">DW6000</span></span> |<span data-ttu-id="d0344-455">6</span><span class="sxs-lookup"><span data-stu-id="d0344-455">6</span></span> |<span data-ttu-id="d0344-456">188</span><span class="sxs-lookup"><span data-stu-id="d0344-456">188</span></span> |<span data-ttu-id="d0344-457">375</span><span class="sxs-lookup"><span data-stu-id="d0344-457">375</span></span> |<span data-ttu-id="d0344-458">750</span><span class="sxs-lookup"><span data-stu-id="d0344-458">750</span></span> |

<span data-ttu-id="d0344-459">In deze tabel van geheugentoewijzingen van het hele systeem, kunt u zien dat een totaal van 375 GB geheugen wordt toegewezen door een query uitgevoerd op een dw2000 zijn in Hallo xlargerc bronklasse (distributies 6400 MB * 60 * 1024 tooconvert tooGB) via Hallo geheel van uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d0344-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="d0344-460">Hallo geldt dezelfde berekening toostatic resource klassen.</span><span class="sxs-lookup"><span data-stu-id="d0344-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="d0344-461">Gelijktijdigheid sleuf verbruik</span><span class="sxs-lookup"><span data-stu-id="d0344-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="d0344-462">SQL Data Warehouse verleent meer geheugen tooqueries uitgevoerd in de hogere resource-klassen.</span><span class="sxs-lookup"><span data-stu-id="d0344-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="d0344-463">Geheugen is een vaste resource.</span><span class="sxs-lookup"><span data-stu-id="d0344-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="d0344-464">Daarom hello meer geheugen toegewezen per query, Hallo minder gelijktijdige query's kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d0344-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="d0344-465">Hallo herhaalt onderstaande alle vorige concepten Hallo in één weergave met Hallo aantal sleuven beschikbaar gelijktijdigheid van taken door DWU en Hallo sleuven verbruikt door de resourceklasse van elke.</span><span class="sxs-lookup"><span data-stu-id="d0344-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="d0344-466">Toewijzing en het verbruik van gelijktijdigheid sleuven voor dynamische Bronklassen</span><span class="sxs-lookup"><span data-stu-id="d0344-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="d0344-467">DWU</span><span class="sxs-lookup"><span data-stu-id="d0344-467">DWU</span></span> | <span data-ttu-id="d0344-468">Maximum aantal gelijktijdige query 's</span><span class="sxs-lookup"><span data-stu-id="d0344-468">Maximum concurrent queries</span></span> | <span data-ttu-id="d0344-469">Gelijktijdigheid sleuven toegewezen</span><span class="sxs-lookup"><span data-stu-id="d0344-469">Concurrency slots allocated</span></span> | <span data-ttu-id="d0344-470">Gebruikt door smallrc sleuven</span><span class="sxs-lookup"><span data-stu-id="d0344-470">Slots used by smallrc</span></span> | <span data-ttu-id="d0344-471">Gebruikt door mediumrc sleuven</span><span class="sxs-lookup"><span data-stu-id="d0344-471">Slots used by mediumrc</span></span> | <span data-ttu-id="d0344-472">Gebruikt door largerc sleuven</span><span class="sxs-lookup"><span data-stu-id="d0344-472">Slots used by largerc</span></span> | <span data-ttu-id="d0344-473">Gebruikt door xlargerc sleuven</span><span class="sxs-lookup"><span data-stu-id="d0344-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="d0344-474">DW100</span><span class="sxs-lookup"><span data-stu-id="d0344-474">DW100</span></span> |<span data-ttu-id="d0344-475">4</span><span class="sxs-lookup"><span data-stu-id="d0344-475">4</span></span> |<span data-ttu-id="d0344-476">4</span><span class="sxs-lookup"><span data-stu-id="d0344-476">4</span></span> |<span data-ttu-id="d0344-477">1</span><span class="sxs-lookup"><span data-stu-id="d0344-477">1</span></span> |<span data-ttu-id="d0344-478">1</span><span class="sxs-lookup"><span data-stu-id="d0344-478">1</span></span> |<span data-ttu-id="d0344-479">2</span><span class="sxs-lookup"><span data-stu-id="d0344-479">2</span></span> |<span data-ttu-id="d0344-480">4</span><span class="sxs-lookup"><span data-stu-id="d0344-480">4</span></span> |
| <span data-ttu-id="d0344-481">DW200</span><span class="sxs-lookup"><span data-stu-id="d0344-481">DW200</span></span> |<span data-ttu-id="d0344-482">8</span><span class="sxs-lookup"><span data-stu-id="d0344-482">8</span></span> |<span data-ttu-id="d0344-483">8</span><span class="sxs-lookup"><span data-stu-id="d0344-483">8</span></span> |<span data-ttu-id="d0344-484">1</span><span class="sxs-lookup"><span data-stu-id="d0344-484">1</span></span> |<span data-ttu-id="d0344-485">2</span><span class="sxs-lookup"><span data-stu-id="d0344-485">2</span></span> |<span data-ttu-id="d0344-486">4</span><span class="sxs-lookup"><span data-stu-id="d0344-486">4</span></span> |<span data-ttu-id="d0344-487">8</span><span class="sxs-lookup"><span data-stu-id="d0344-487">8</span></span> |
| <span data-ttu-id="d0344-488">DW300</span><span class="sxs-lookup"><span data-stu-id="d0344-488">DW300</span></span> |<span data-ttu-id="d0344-489">12</span><span class="sxs-lookup"><span data-stu-id="d0344-489">12</span></span> |<span data-ttu-id="d0344-490">12</span><span class="sxs-lookup"><span data-stu-id="d0344-490">12</span></span> |<span data-ttu-id="d0344-491">1</span><span class="sxs-lookup"><span data-stu-id="d0344-491">1</span></span> |<span data-ttu-id="d0344-492">2</span><span class="sxs-lookup"><span data-stu-id="d0344-492">2</span></span> |<span data-ttu-id="d0344-493">4</span><span class="sxs-lookup"><span data-stu-id="d0344-493">4</span></span> |<span data-ttu-id="d0344-494">8</span><span class="sxs-lookup"><span data-stu-id="d0344-494">8</span></span> |
| <span data-ttu-id="d0344-495">DW400</span><span class="sxs-lookup"><span data-stu-id="d0344-495">DW400</span></span> |<span data-ttu-id="d0344-496">16</span><span class="sxs-lookup"><span data-stu-id="d0344-496">16</span></span> |<span data-ttu-id="d0344-497">16</span><span class="sxs-lookup"><span data-stu-id="d0344-497">16</span></span> |<span data-ttu-id="d0344-498">1</span><span class="sxs-lookup"><span data-stu-id="d0344-498">1</span></span> |<span data-ttu-id="d0344-499">4</span><span class="sxs-lookup"><span data-stu-id="d0344-499">4</span></span> |<span data-ttu-id="d0344-500">8</span><span class="sxs-lookup"><span data-stu-id="d0344-500">8</span></span> |<span data-ttu-id="d0344-501">16</span><span class="sxs-lookup"><span data-stu-id="d0344-501">16</span></span> |
| <span data-ttu-id="d0344-502">DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-502">DW500</span></span> |<span data-ttu-id="d0344-503">20</span><span class="sxs-lookup"><span data-stu-id="d0344-503">20</span></span> |<span data-ttu-id="d0344-504">20</span><span class="sxs-lookup"><span data-stu-id="d0344-504">20</span></span> |<span data-ttu-id="d0344-505">1</span><span class="sxs-lookup"><span data-stu-id="d0344-505">1</span></span> |<span data-ttu-id="d0344-506">4</span><span class="sxs-lookup"><span data-stu-id="d0344-506">4</span></span> |<span data-ttu-id="d0344-507">8</span><span class="sxs-lookup"><span data-stu-id="d0344-507">8</span></span> |<span data-ttu-id="d0344-508">16</span><span class="sxs-lookup"><span data-stu-id="d0344-508">16</span></span> |
| <span data-ttu-id="d0344-509">DW600</span><span class="sxs-lookup"><span data-stu-id="d0344-509">DW600</span></span> |<span data-ttu-id="d0344-510">24</span><span class="sxs-lookup"><span data-stu-id="d0344-510">24</span></span> |<span data-ttu-id="d0344-511">24</span><span class="sxs-lookup"><span data-stu-id="d0344-511">24</span></span> |<span data-ttu-id="d0344-512">1</span><span class="sxs-lookup"><span data-stu-id="d0344-512">1</span></span> |<span data-ttu-id="d0344-513">4</span><span class="sxs-lookup"><span data-stu-id="d0344-513">4</span></span> |<span data-ttu-id="d0344-514">8</span><span class="sxs-lookup"><span data-stu-id="d0344-514">8</span></span> |<span data-ttu-id="d0344-515">16</span><span class="sxs-lookup"><span data-stu-id="d0344-515">16</span></span> |
| <span data-ttu-id="d0344-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="d0344-516">DW1000</span></span> |<span data-ttu-id="d0344-517">32</span><span class="sxs-lookup"><span data-stu-id="d0344-517">32</span></span> |<span data-ttu-id="d0344-518">40</span><span class="sxs-lookup"><span data-stu-id="d0344-518">40</span></span> |<span data-ttu-id="d0344-519">1</span><span class="sxs-lookup"><span data-stu-id="d0344-519">1</span></span> |<span data-ttu-id="d0344-520">8</span><span class="sxs-lookup"><span data-stu-id="d0344-520">8</span></span> |<span data-ttu-id="d0344-521">16</span><span class="sxs-lookup"><span data-stu-id="d0344-521">16</span></span> |<span data-ttu-id="d0344-522">32</span><span class="sxs-lookup"><span data-stu-id="d0344-522">32</span></span> |
| <span data-ttu-id="d0344-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="d0344-523">DW1200</span></span> |<span data-ttu-id="d0344-524">32</span><span class="sxs-lookup"><span data-stu-id="d0344-524">32</span></span> |<span data-ttu-id="d0344-525">48</span><span class="sxs-lookup"><span data-stu-id="d0344-525">48</span></span> |<span data-ttu-id="d0344-526">1</span><span class="sxs-lookup"><span data-stu-id="d0344-526">1</span></span> |<span data-ttu-id="d0344-527">8</span><span class="sxs-lookup"><span data-stu-id="d0344-527">8</span></span> |<span data-ttu-id="d0344-528">16</span><span class="sxs-lookup"><span data-stu-id="d0344-528">16</span></span> |<span data-ttu-id="d0344-529">32</span><span class="sxs-lookup"><span data-stu-id="d0344-529">32</span></span> |
| <span data-ttu-id="d0344-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="d0344-530">DW1500</span></span> |<span data-ttu-id="d0344-531">32</span><span class="sxs-lookup"><span data-stu-id="d0344-531">32</span></span> |<span data-ttu-id="d0344-532">60</span><span class="sxs-lookup"><span data-stu-id="d0344-532">60</span></span> |<span data-ttu-id="d0344-533">1</span><span class="sxs-lookup"><span data-stu-id="d0344-533">1</span></span> |<span data-ttu-id="d0344-534">8</span><span class="sxs-lookup"><span data-stu-id="d0344-534">8</span></span> |<span data-ttu-id="d0344-535">16</span><span class="sxs-lookup"><span data-stu-id="d0344-535">16</span></span> |<span data-ttu-id="d0344-536">32</span><span class="sxs-lookup"><span data-stu-id="d0344-536">32</span></span> |
| <span data-ttu-id="d0344-537">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="d0344-537">DW2000</span></span> |<span data-ttu-id="d0344-538">32</span><span class="sxs-lookup"><span data-stu-id="d0344-538">32</span></span> |<span data-ttu-id="d0344-539">80</span><span class="sxs-lookup"><span data-stu-id="d0344-539">80</span></span> |<span data-ttu-id="d0344-540">1</span><span class="sxs-lookup"><span data-stu-id="d0344-540">1</span></span> |<span data-ttu-id="d0344-541">16</span><span class="sxs-lookup"><span data-stu-id="d0344-541">16</span></span> |<span data-ttu-id="d0344-542">32</span><span class="sxs-lookup"><span data-stu-id="d0344-542">32</span></span> |<span data-ttu-id="d0344-543">64</span><span class="sxs-lookup"><span data-stu-id="d0344-543">64</span></span> |
| <span data-ttu-id="d0344-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="d0344-544">DW3000</span></span> |<span data-ttu-id="d0344-545">32</span><span class="sxs-lookup"><span data-stu-id="d0344-545">32</span></span> |<span data-ttu-id="d0344-546">120</span><span class="sxs-lookup"><span data-stu-id="d0344-546">120</span></span> |<span data-ttu-id="d0344-547">1</span><span class="sxs-lookup"><span data-stu-id="d0344-547">1</span></span> |<span data-ttu-id="d0344-548">16</span><span class="sxs-lookup"><span data-stu-id="d0344-548">16</span></span> |<span data-ttu-id="d0344-549">32</span><span class="sxs-lookup"><span data-stu-id="d0344-549">32</span></span> |<span data-ttu-id="d0344-550">64</span><span class="sxs-lookup"><span data-stu-id="d0344-550">64</span></span> |
| <span data-ttu-id="d0344-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="d0344-551">DW6000</span></span> |<span data-ttu-id="d0344-552">32</span><span class="sxs-lookup"><span data-stu-id="d0344-552">32</span></span> |<span data-ttu-id="d0344-553">240</span><span class="sxs-lookup"><span data-stu-id="d0344-553">240</span></span> |<span data-ttu-id="d0344-554">1</span><span class="sxs-lookup"><span data-stu-id="d0344-554">1</span></span> |<span data-ttu-id="d0344-555">32</span><span class="sxs-lookup"><span data-stu-id="d0344-555">32</span></span> |<span data-ttu-id="d0344-556">64</span><span class="sxs-lookup"><span data-stu-id="d0344-556">64</span></span> |<span data-ttu-id="d0344-557">128</span><span class="sxs-lookup"><span data-stu-id="d0344-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="d0344-558">Toewijzing en het verbruik van gelijktijdigheid sleuven voor statische resource klassen</span><span class="sxs-lookup"><span data-stu-id="d0344-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="d0344-559">DWU</span><span class="sxs-lookup"><span data-stu-id="d0344-559">DWU</span></span> | <span data-ttu-id="d0344-560">Maximum aantal gelijktijdige query 's</span><span class="sxs-lookup"><span data-stu-id="d0344-560">Maximum concurrent queries</span></span> | <span data-ttu-id="d0344-561">Gelijktijdigheid sleuven toegewezen</span><span class="sxs-lookup"><span data-stu-id="d0344-561">Concurrency slots allocated</span></span> |<span data-ttu-id="d0344-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="d0344-562">staticrc10</span></span> | <span data-ttu-id="d0344-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="d0344-563">staticrc20</span></span> | <span data-ttu-id="d0344-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="d0344-564">staticrc30</span></span> | <span data-ttu-id="d0344-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="d0344-565">staticrc40</span></span> | <span data-ttu-id="d0344-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="d0344-566">staticrc50</span></span> | <span data-ttu-id="d0344-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="d0344-567">staticrc60</span></span> | <span data-ttu-id="d0344-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="d0344-568">staticrc70</span></span> | <span data-ttu-id="d0344-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="d0344-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="d0344-570">DW100</span><span class="sxs-lookup"><span data-stu-id="d0344-570">DW100</span></span> |<span data-ttu-id="d0344-571">4</span><span class="sxs-lookup"><span data-stu-id="d0344-571">4</span></span> |<span data-ttu-id="d0344-572">4</span><span class="sxs-lookup"><span data-stu-id="d0344-572">4</span></span> |<span data-ttu-id="d0344-573">1</span><span class="sxs-lookup"><span data-stu-id="d0344-573">1</span></span> |<span data-ttu-id="d0344-574">2</span><span class="sxs-lookup"><span data-stu-id="d0344-574">2</span></span> |<span data-ttu-id="d0344-575">4</span><span class="sxs-lookup"><span data-stu-id="d0344-575">4</span></span> |<span data-ttu-id="d0344-576">4</span><span class="sxs-lookup"><span data-stu-id="d0344-576">4</span></span> |<span data-ttu-id="d0344-577">4</span><span class="sxs-lookup"><span data-stu-id="d0344-577">4</span></span> |<span data-ttu-id="d0344-578">4</span><span class="sxs-lookup"><span data-stu-id="d0344-578">4</span></span> |<span data-ttu-id="d0344-579">4</span><span class="sxs-lookup"><span data-stu-id="d0344-579">4</span></span> |<span data-ttu-id="d0344-580">4</span><span class="sxs-lookup"><span data-stu-id="d0344-580">4</span></span> |
| <span data-ttu-id="d0344-581">DW200</span><span class="sxs-lookup"><span data-stu-id="d0344-581">DW200</span></span> |<span data-ttu-id="d0344-582">8</span><span class="sxs-lookup"><span data-stu-id="d0344-582">8</span></span> |<span data-ttu-id="d0344-583">8</span><span class="sxs-lookup"><span data-stu-id="d0344-583">8</span></span> |<span data-ttu-id="d0344-584">1</span><span class="sxs-lookup"><span data-stu-id="d0344-584">1</span></span> |<span data-ttu-id="d0344-585">2</span><span class="sxs-lookup"><span data-stu-id="d0344-585">2</span></span> |<span data-ttu-id="d0344-586">4</span><span class="sxs-lookup"><span data-stu-id="d0344-586">4</span></span> |<span data-ttu-id="d0344-587">8</span><span class="sxs-lookup"><span data-stu-id="d0344-587">8</span></span> |<span data-ttu-id="d0344-588">8</span><span class="sxs-lookup"><span data-stu-id="d0344-588">8</span></span> |<span data-ttu-id="d0344-589">8</span><span class="sxs-lookup"><span data-stu-id="d0344-589">8</span></span> |<span data-ttu-id="d0344-590">8</span><span class="sxs-lookup"><span data-stu-id="d0344-590">8</span></span> |<span data-ttu-id="d0344-591">8</span><span class="sxs-lookup"><span data-stu-id="d0344-591">8</span></span> |
| <span data-ttu-id="d0344-592">DW300</span><span class="sxs-lookup"><span data-stu-id="d0344-592">DW300</span></span> |<span data-ttu-id="d0344-593">12</span><span class="sxs-lookup"><span data-stu-id="d0344-593">12</span></span> |<span data-ttu-id="d0344-594">12</span><span class="sxs-lookup"><span data-stu-id="d0344-594">12</span></span> |<span data-ttu-id="d0344-595">1</span><span class="sxs-lookup"><span data-stu-id="d0344-595">1</span></span> |<span data-ttu-id="d0344-596">2</span><span class="sxs-lookup"><span data-stu-id="d0344-596">2</span></span> |<span data-ttu-id="d0344-597">4</span><span class="sxs-lookup"><span data-stu-id="d0344-597">4</span></span> |<span data-ttu-id="d0344-598">8</span><span class="sxs-lookup"><span data-stu-id="d0344-598">8</span></span> |<span data-ttu-id="d0344-599">8</span><span class="sxs-lookup"><span data-stu-id="d0344-599">8</span></span> |<span data-ttu-id="d0344-600">8</span><span class="sxs-lookup"><span data-stu-id="d0344-600">8</span></span> |<span data-ttu-id="d0344-601">8</span><span class="sxs-lookup"><span data-stu-id="d0344-601">8</span></span> |<span data-ttu-id="d0344-602">8</span><span class="sxs-lookup"><span data-stu-id="d0344-602">8</span></span> |
| <span data-ttu-id="d0344-603">DW400</span><span class="sxs-lookup"><span data-stu-id="d0344-603">DW400</span></span> |<span data-ttu-id="d0344-604">16</span><span class="sxs-lookup"><span data-stu-id="d0344-604">16</span></span> |<span data-ttu-id="d0344-605">16</span><span class="sxs-lookup"><span data-stu-id="d0344-605">16</span></span> |<span data-ttu-id="d0344-606">1</span><span class="sxs-lookup"><span data-stu-id="d0344-606">1</span></span> |<span data-ttu-id="d0344-607">2</span><span class="sxs-lookup"><span data-stu-id="d0344-607">2</span></span> |<span data-ttu-id="d0344-608">4</span><span class="sxs-lookup"><span data-stu-id="d0344-608">4</span></span> |<span data-ttu-id="d0344-609">8</span><span class="sxs-lookup"><span data-stu-id="d0344-609">8</span></span> |<span data-ttu-id="d0344-610">16</span><span class="sxs-lookup"><span data-stu-id="d0344-610">16</span></span> |<span data-ttu-id="d0344-611">16</span><span class="sxs-lookup"><span data-stu-id="d0344-611">16</span></span> |<span data-ttu-id="d0344-612">16</span><span class="sxs-lookup"><span data-stu-id="d0344-612">16</span></span> |<span data-ttu-id="d0344-613">16</span><span class="sxs-lookup"><span data-stu-id="d0344-613">16</span></span> |
| <span data-ttu-id="d0344-614">DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-614">DW500</span></span> | <span data-ttu-id="d0344-615">20</span><span class="sxs-lookup"><span data-stu-id="d0344-615">20</span></span>| <span data-ttu-id="d0344-616">20</span><span class="sxs-lookup"><span data-stu-id="d0344-616">20</span></span>| <span data-ttu-id="d0344-617">1</span><span class="sxs-lookup"><span data-stu-id="d0344-617">1</span></span>| <span data-ttu-id="d0344-618">2</span><span class="sxs-lookup"><span data-stu-id="d0344-618">2</span></span>| <span data-ttu-id="d0344-619">4</span><span class="sxs-lookup"><span data-stu-id="d0344-619">4</span></span>| <span data-ttu-id="d0344-620">8</span><span class="sxs-lookup"><span data-stu-id="d0344-620">8</span></span>| <span data-ttu-id="d0344-621">16</span><span class="sxs-lookup"><span data-stu-id="d0344-621">16</span></span>| <span data-ttu-id="d0344-622">16</span><span class="sxs-lookup"><span data-stu-id="d0344-622">16</span></span>| <span data-ttu-id="d0344-623">16</span><span class="sxs-lookup"><span data-stu-id="d0344-623">16</span></span>| <span data-ttu-id="d0344-624">16</span><span class="sxs-lookup"><span data-stu-id="d0344-624">16</span></span>|
| <span data-ttu-id="d0344-625">DW600</span><span class="sxs-lookup"><span data-stu-id="d0344-625">DW600</span></span> | <span data-ttu-id="d0344-626">24</span><span class="sxs-lookup"><span data-stu-id="d0344-626">24</span></span>| <span data-ttu-id="d0344-627">24</span><span class="sxs-lookup"><span data-stu-id="d0344-627">24</span></span>| <span data-ttu-id="d0344-628">1</span><span class="sxs-lookup"><span data-stu-id="d0344-628">1</span></span>| <span data-ttu-id="d0344-629">2</span><span class="sxs-lookup"><span data-stu-id="d0344-629">2</span></span>| <span data-ttu-id="d0344-630">4</span><span class="sxs-lookup"><span data-stu-id="d0344-630">4</span></span>| <span data-ttu-id="d0344-631">8</span><span class="sxs-lookup"><span data-stu-id="d0344-631">8</span></span>| <span data-ttu-id="d0344-632">16</span><span class="sxs-lookup"><span data-stu-id="d0344-632">16</span></span>| <span data-ttu-id="d0344-633">16</span><span class="sxs-lookup"><span data-stu-id="d0344-633">16</span></span>| <span data-ttu-id="d0344-634">16</span><span class="sxs-lookup"><span data-stu-id="d0344-634">16</span></span>| <span data-ttu-id="d0344-635">16</span><span class="sxs-lookup"><span data-stu-id="d0344-635">16</span></span>|
| <span data-ttu-id="d0344-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="d0344-636">DW1000</span></span> | <span data-ttu-id="d0344-637">32</span><span class="sxs-lookup"><span data-stu-id="d0344-637">32</span></span>| <span data-ttu-id="d0344-638">40</span><span class="sxs-lookup"><span data-stu-id="d0344-638">40</span></span>| <span data-ttu-id="d0344-639">1</span><span class="sxs-lookup"><span data-stu-id="d0344-639">1</span></span>| <span data-ttu-id="d0344-640">2</span><span class="sxs-lookup"><span data-stu-id="d0344-640">2</span></span>| <span data-ttu-id="d0344-641">4</span><span class="sxs-lookup"><span data-stu-id="d0344-641">4</span></span>| <span data-ttu-id="d0344-642">8</span><span class="sxs-lookup"><span data-stu-id="d0344-642">8</span></span>| <span data-ttu-id="d0344-643">16</span><span class="sxs-lookup"><span data-stu-id="d0344-643">16</span></span>| <span data-ttu-id="d0344-644">32</span><span class="sxs-lookup"><span data-stu-id="d0344-644">32</span></span>| <span data-ttu-id="d0344-645">32</span><span class="sxs-lookup"><span data-stu-id="d0344-645">32</span></span>| <span data-ttu-id="d0344-646">32</span><span class="sxs-lookup"><span data-stu-id="d0344-646">32</span></span>|
| <span data-ttu-id="d0344-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="d0344-647">DW1200</span></span> | <span data-ttu-id="d0344-648">32</span><span class="sxs-lookup"><span data-stu-id="d0344-648">32</span></span>| <span data-ttu-id="d0344-649">48</span><span class="sxs-lookup"><span data-stu-id="d0344-649">48</span></span>| <span data-ttu-id="d0344-650">1</span><span class="sxs-lookup"><span data-stu-id="d0344-650">1</span></span>| <span data-ttu-id="d0344-651">2</span><span class="sxs-lookup"><span data-stu-id="d0344-651">2</span></span>| <span data-ttu-id="d0344-652">4</span><span class="sxs-lookup"><span data-stu-id="d0344-652">4</span></span>| <span data-ttu-id="d0344-653">8</span><span class="sxs-lookup"><span data-stu-id="d0344-653">8</span></span>| <span data-ttu-id="d0344-654">16</span><span class="sxs-lookup"><span data-stu-id="d0344-654">16</span></span>| <span data-ttu-id="d0344-655">32</span><span class="sxs-lookup"><span data-stu-id="d0344-655">32</span></span>| <span data-ttu-id="d0344-656">32</span><span class="sxs-lookup"><span data-stu-id="d0344-656">32</span></span>| <span data-ttu-id="d0344-657">32</span><span class="sxs-lookup"><span data-stu-id="d0344-657">32</span></span>|
| <span data-ttu-id="d0344-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="d0344-658">DW1500</span></span> | <span data-ttu-id="d0344-659">32</span><span class="sxs-lookup"><span data-stu-id="d0344-659">32</span></span>| <span data-ttu-id="d0344-660">60</span><span class="sxs-lookup"><span data-stu-id="d0344-660">60</span></span>| <span data-ttu-id="d0344-661">1</span><span class="sxs-lookup"><span data-stu-id="d0344-661">1</span></span>| <span data-ttu-id="d0344-662">2</span><span class="sxs-lookup"><span data-stu-id="d0344-662">2</span></span>| <span data-ttu-id="d0344-663">4</span><span class="sxs-lookup"><span data-stu-id="d0344-663">4</span></span>| <span data-ttu-id="d0344-664">8</span><span class="sxs-lookup"><span data-stu-id="d0344-664">8</span></span>| <span data-ttu-id="d0344-665">16</span><span class="sxs-lookup"><span data-stu-id="d0344-665">16</span></span>| <span data-ttu-id="d0344-666">32</span><span class="sxs-lookup"><span data-stu-id="d0344-666">32</span></span>| <span data-ttu-id="d0344-667">32</span><span class="sxs-lookup"><span data-stu-id="d0344-667">32</span></span>| <span data-ttu-id="d0344-668">32</span><span class="sxs-lookup"><span data-stu-id="d0344-668">32</span></span>|
| <span data-ttu-id="d0344-669">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="d0344-669">DW2000</span></span> | <span data-ttu-id="d0344-670">32</span><span class="sxs-lookup"><span data-stu-id="d0344-670">32</span></span>| <span data-ttu-id="d0344-671">80</span><span class="sxs-lookup"><span data-stu-id="d0344-671">80</span></span>| <span data-ttu-id="d0344-672">1</span><span class="sxs-lookup"><span data-stu-id="d0344-672">1</span></span>| <span data-ttu-id="d0344-673">2</span><span class="sxs-lookup"><span data-stu-id="d0344-673">2</span></span>| <span data-ttu-id="d0344-674">4</span><span class="sxs-lookup"><span data-stu-id="d0344-674">4</span></span>| <span data-ttu-id="d0344-675">8</span><span class="sxs-lookup"><span data-stu-id="d0344-675">8</span></span>| <span data-ttu-id="d0344-676">16</span><span class="sxs-lookup"><span data-stu-id="d0344-676">16</span></span>| <span data-ttu-id="d0344-677">32</span><span class="sxs-lookup"><span data-stu-id="d0344-677">32</span></span>| <span data-ttu-id="d0344-678">64</span><span class="sxs-lookup"><span data-stu-id="d0344-678">64</span></span>| <span data-ttu-id="d0344-679">64</span><span class="sxs-lookup"><span data-stu-id="d0344-679">64</span></span>|
| <span data-ttu-id="d0344-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="d0344-680">DW3000</span></span> | <span data-ttu-id="d0344-681">32</span><span class="sxs-lookup"><span data-stu-id="d0344-681">32</span></span>| <span data-ttu-id="d0344-682">120</span><span class="sxs-lookup"><span data-stu-id="d0344-682">120</span></span>| <span data-ttu-id="d0344-683">1</span><span class="sxs-lookup"><span data-stu-id="d0344-683">1</span></span>| <span data-ttu-id="d0344-684">2</span><span class="sxs-lookup"><span data-stu-id="d0344-684">2</span></span>| <span data-ttu-id="d0344-685">4</span><span class="sxs-lookup"><span data-stu-id="d0344-685">4</span></span>| <span data-ttu-id="d0344-686">8</span><span class="sxs-lookup"><span data-stu-id="d0344-686">8</span></span>| <span data-ttu-id="d0344-687">16</span><span class="sxs-lookup"><span data-stu-id="d0344-687">16</span></span>| <span data-ttu-id="d0344-688">32</span><span class="sxs-lookup"><span data-stu-id="d0344-688">32</span></span>| <span data-ttu-id="d0344-689">64</span><span class="sxs-lookup"><span data-stu-id="d0344-689">64</span></span>| <span data-ttu-id="d0344-690">64</span><span class="sxs-lookup"><span data-stu-id="d0344-690">64</span></span>|
| <span data-ttu-id="d0344-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="d0344-691">DW6000</span></span> | <span data-ttu-id="d0344-692">32</span><span class="sxs-lookup"><span data-stu-id="d0344-692">32</span></span>| <span data-ttu-id="d0344-693">240</span><span class="sxs-lookup"><span data-stu-id="d0344-693">240</span></span>| <span data-ttu-id="d0344-694">1</span><span class="sxs-lookup"><span data-stu-id="d0344-694">1</span></span>| <span data-ttu-id="d0344-695">2</span><span class="sxs-lookup"><span data-stu-id="d0344-695">2</span></span>| <span data-ttu-id="d0344-696">4</span><span class="sxs-lookup"><span data-stu-id="d0344-696">4</span></span>| <span data-ttu-id="d0344-697">8</span><span class="sxs-lookup"><span data-stu-id="d0344-697">8</span></span>| <span data-ttu-id="d0344-698">16</span><span class="sxs-lookup"><span data-stu-id="d0344-698">16</span></span>| <span data-ttu-id="d0344-699">32</span><span class="sxs-lookup"><span data-stu-id="d0344-699">32</span></span>| <span data-ttu-id="d0344-700">64</span><span class="sxs-lookup"><span data-stu-id="d0344-700">64</span></span>| <span data-ttu-id="d0344-701">128</span><span class="sxs-lookup"><span data-stu-id="d0344-701">128</span></span>|

<span data-ttu-id="d0344-702">Uit deze tabellen ziet u dat SQL Data Warehouse wordt uitgevoerd als DW1000 een maximum van 32 gelijktijdige query's en een totaal van 40 gelijktijdigheid sleuven wijst.</span><span class="sxs-lookup"><span data-stu-id="d0344-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="d0344-703">Als alle gebruikers worden uitgevoerd in smallrc, zou 32 gelijktijdige query's worden toegestaan, omdat elke query 1 gelijktijdigheid sleuf zou gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0344-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="d0344-704">Als alle gebruikers op een DW1000 in mediumrc werd uitgevoerd, elke query 800 MB per distributiepunt voor een toewijzing van het totale geheugen van 47 GB per query toegewezen zou en gelijktijdigheid beperkt too5 gebruikers worden zou (40 gelijktijdigheid sleuven / 8-sleuven per gebruiker mediumrc).</span><span class="sxs-lookup"><span data-stu-id="d0344-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="d0344-705">Juiste bronklasse selecteren</span><span class="sxs-lookup"><span data-stu-id="d0344-705">Selecting proper resource class</span></span>  
<span data-ttu-id="d0344-706">Het wordt aangeraden tooa bronklasse voor toopermanently toewijzen gebruikers in plaats van de resource-klassen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d0344-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="d0344-707">Bijvoorbeeld maken belasting tooclustered columnstore-tabellen voor hogere kwaliteit indexen wanneer meer geheugen toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d0344-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="d0344-708">tooensure die belastingen toegang toohigher geheugen hebben, specifiek voor het laden van gegevens maken van een gebruiker en deze tooa hogere resource gebruikersklasse permanent toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d0344-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="d0344-709">Er zijn een aantal best practices toofollow hier.</span><span class="sxs-lookup"><span data-stu-id="d0344-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="d0344-710">Zoals eerder vermeld, SQL DW ondersteunt twee soorten klasse brontypen: statische resource klassen en dynamische Bronklassen.</span><span class="sxs-lookup"><span data-stu-id="d0344-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="d0344-711">Bij het laden van aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="d0344-711">Loading best practices</span></span>
1.  <span data-ttu-id="d0344-712">Als Hallo verwachtingen belastingen met normale hoeveelheid gegevens, is een statische bronklasse een goede keuze.</span><span class="sxs-lookup"><span data-stu-id="d0344-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="d0344-713">Later, wanneer tooget schaalt meer verwerkingskracht, Hallo datawarehouse kan worden query toorun meer gelijktijdige out-of-the-box, zoals Hallo load gebruiker meer geheugen geen verbruikt.</span><span class="sxs-lookup"><span data-stu-id="d0344-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="d0344-714">Als Hallo verwachtingen grotere hoeveelheden in sommige gevallen, is een dynamische bronklasse een goede keuze.</span><span class="sxs-lookup"><span data-stu-id="d0344-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="d0344-715">Later, wanneer meer verwerkingskracht omhoog tooget schalen, krijgt Hallo load gebruiker meer geheugen out-of-the-box, zodat Hallo load tooperform daarom sneller.</span><span class="sxs-lookup"><span data-stu-id="d0344-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="d0344-716">Hallo nodig tooprocess geheugenbelasting efficiënt hangt af van Hallo aard van het Hallo-tabel is geladen en Hallo en de hoeveelheid gegevens verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d0344-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="d0344-717">Voor het exemplaar vereist bij het laden van gegevens in tabellen CCI dat sommige geheugen toolet CCI rowgroups bereiken optimalisatie.</span><span class="sxs-lookup"><span data-stu-id="d0344-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="d0344-718">Zie voor meer informatie kolomopslagindexen Hallo - richtlijnen laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d0344-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="d0344-719">Als een best practice we adviseren u toouse ten minste 200MB aan geheugen voor belastingen.</span><span class="sxs-lookup"><span data-stu-id="d0344-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="d0344-720">Aanbevolen procedures voor het opvragen</span><span class="sxs-lookup"><span data-stu-id="d0344-720">Querying best practices</span></span>
<span data-ttu-id="d0344-721">Query's hebben verschillende vereisten, afhankelijk van de complexiteit.</span><span class="sxs-lookup"><span data-stu-id="d0344-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="d0344-722">Geheugen per query verhogen of een uitbreiding van Hallo gelijktijdigheid zijn beide tooaugment geldige manieren totale doorvoer afhankelijk van Hallo query behoeften.</span><span class="sxs-lookup"><span data-stu-id="d0344-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="d0344-723">Indien de Hallo verwachtingen reguliere, complexe query's (bijvoorbeeld toogenerate dagelijkse en wekelijkse rapporten) en hoeft niet tootake profiteren van gelijktijdigheid van taken, is een dynamische bronklasse een goede keuze.</span><span class="sxs-lookup"><span data-stu-id="d0344-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="d0344-724">Als Hallo system meer gegevens tooprocess heeft, bieden schaalt Hallo datawarehouse daarom automatisch meer geheugen toohello gebruiker Hallo-query uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d0344-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="d0344-725">Indien de Hallo verwachtingen variabele of Dagverloop gelijktijdigheid patronen (bijvoorbeeld als Hallo database query wordt uitgevoerd via een webgebruikersinterface grotendeels toegankelijk), een statische bronklasse is een goede keuze.</span><span class="sxs-lookup"><span data-stu-id="d0344-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="d0344-726">Later, wanneer toodata datawarehouse schaalt, Hallo-gebruiker is gekoppeld aan de statische bronklasse hello wordt automatisch worden kunnen toorun meer gelijktijdige query's.</span><span class="sxs-lookup"><span data-stu-id="d0344-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="d0344-727">Selecteren juiste geheugentoekenning afhankelijk van het Hallo-behoeften van uw query is niet-triviale, omdat deze afhankelijk van veel factoren af zoals de hoeveelheid gegevens die zijn opgevraagd is, Hallo Hallo aard van het tabelschema hello, en verschillende join, selectie en groep predicaten.</span><span class="sxs-lookup"><span data-stu-id="d0344-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="d0344-728">Een algemeen verwerkt toewijzen van meer geheugen kunt query's toocomplete sneller, maar zou Hallo algehele gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="d0344-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="d0344-729">Als geen gelijktijdigheid van taken een probleem is, komt te veel toewijzen van geheugen niet schadelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="d0344-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="d0344-730">toofine afstemmen doorvoer, probeert verschillende versies van het resource-klassen is mogelijk vereist.</span><span class="sxs-lookup"><span data-stu-id="d0344-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="d0344-731">Kunt u Hallo volgende opgeslagen procedure toofigure uit gelijktijdigheid van taken en het geheugen verlenen per bronklasse op een gegeven SLO en Hallo dichtstbijzijnde best bronklasse voor geheugen rekenintensieve CCI bewerkingen op niet-gepartitioneerde CCI tabel op een bepaalde bron-klasse:</span><span class="sxs-lookup"><span data-stu-id="d0344-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="d0344-732">Beschrijving:</span><span class="sxs-lookup"><span data-stu-id="d0344-732">Description:</span></span>  
<span data-ttu-id="d0344-733">Hier volgt Hallo doel van deze opgeslagen procedure:</span><span class="sxs-lookup"><span data-stu-id="d0344-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="d0344-734">toohelp gebruiker uitzoeken gelijktijdigheid van taken en het geheugen verlenen per bronklasse op een gegeven SLO.</span><span class="sxs-lookup"><span data-stu-id="d0344-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="d0344-735">Gebruiker moet tooprovide NULL voor schema- en tablename voor deze zoals weergegeven in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="d0344-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="d0344-736">toohelp gebruiker Bereken Hallo dichtstbijzijnde best bronklasse voor Hallo geheugen intensed CCI operations (belasting, tabel kopiëren, opnieuw opbouwen index, enzovoort) in niet-gepartitioneerde CCI tabel op een bepaalde bron-klasse.</span><span class="sxs-lookup"><span data-stu-id="d0344-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="d0344-737">Hallo opgeslagen procedure maakt gebruik van tabel schema toofind uit Hallo vereiste geheugen toekennen voor deze.</span><span class="sxs-lookup"><span data-stu-id="d0344-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="d0344-738">Afhankelijkheden en beperkingen:</span><span class="sxs-lookup"><span data-stu-id="d0344-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="d0344-739">Deze opgeslagen procedure is niet ontworpen toocalculate geheugenvereiste voor de tabel is gepartitioneerd cci.</span><span class="sxs-lookup"><span data-stu-id="d0344-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="d0344-740">Deze opgeslagen procedure neemt geheugenvereiste in aanmerking voor Hallo Selecteer deel van INSERT-CTAS-selecteren en wordt ervan uitgegaan dat het toobe een eenvoudige SELECT.</span><span class="sxs-lookup"><span data-stu-id="d0344-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="d0344-741">Deze opgeslagen procedure wordt een tijdelijke tabel gebruikt, zodat deze kan worden gebruikt in Hallo sessie waarin deze opgeslagen procedure is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d0344-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="d0344-742">Deze opgeslagen procedure is afhankelijk van de huidige aanbiedingen hello (zoals de hardwareconfiguratie, DMS config) en als een van die verandert vervolgens deze opgeslagen procedure werkt niet correct.</span><span class="sxs-lookup"><span data-stu-id="d0344-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="d0344-743">Deze opgeslagen procedure is afhankelijk van bestaande aangeboden gelijktijdigheid limiet en als die wordt gewijzigd vervolgens deze opgeslagen procedure werkt niet correct.</span><span class="sxs-lookup"><span data-stu-id="d0344-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="d0344-744">Deze opgeslagen procedure is afhankelijk van bestaande resource klasse aanbiedingen en als die vervolgens dit wijzigingen juist proc wuold werkt het programma niet opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d0344-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="d0344-745">Als u geen uitvoer na uitvoering van opgeslagen procedure met parameters die zijn opgegeven, kan er twee situaties.</span><span class="sxs-lookup"><span data-stu-id="d0344-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="d0344-746">1. Beide DW-Parameter bevat ongeldige SLO waarde</span><span class="sxs-lookup"><span data-stu-id="d0344-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="d0344-747">2. OF er zijn geen overeenkomende bronklasse voor CCI bewerking als de tabelnaam is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d0344-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="d0344-748">Bijvoorbeeld: bij DW100, hoogste geheugentoekenning beschikbaar is 400MB en als tabelschema breed voldoende toocross Hallo vereiste van 400MB.</span><span class="sxs-lookup"><span data-stu-id="d0344-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="d0344-749">Voorbeeld van gebruik:</span><span class="sxs-lookup"><span data-stu-id="d0344-749">Usage example:</span></span>
<span data-ttu-id="d0344-750">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="d0344-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="d0344-751">@DWU:Geef een NULL-parameter tooextract huidige DWU van Hallo DW DB Hallo of geef alle DWU vorm van 'DW100' hello ondersteund</span><span class="sxs-lookup"><span data-stu-id="d0344-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="d0344-752">@SCHEMA_NAME:Geef een schemanaam van tabel Hallo</span><span class="sxs-lookup"><span data-stu-id="d0344-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="d0344-753">@TABLE_NAME:Geef een tabelnaam van belang zijn Hallo</span><span class="sxs-lookup"><span data-stu-id="d0344-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="d0344-754">Voorbeelden voor het uitvoeren van deze opgeslagen procedure:</span><span class="sxs-lookup"><span data-stu-id="d0344-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="d0344-755">Tabel1 in Hallo bovenstaande voorbeelden gebruikt kan worden gemaakt zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="d0344-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="d0344-756">Hier volgt de definitie van Hallo opgeslagen procedure:</span><span class="sxs-lookup"><span data-stu-id="d0344-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="d0344-757">Query urgentie</span><span class="sxs-lookup"><span data-stu-id="d0344-757">Query importance</span></span>
<span data-ttu-id="d0344-758">SQL Data Warehouse implementeert resource klassen met behulp van werkbelastinggroepen.</span><span class="sxs-lookup"><span data-stu-id="d0344-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="d0344-759">Er zijn een totaal van acht werkbelastinggroepen die Hallo gedrag van Hallo resource klassen via Hallo verschillende grootten van DWU beheren.</span><span class="sxs-lookup"><span data-stu-id="d0344-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="d0344-760">Voor elke DWU SQL Data Warehouse maakt gebruik van vier Hallo acht werkbelastinggroepen.</span><span class="sxs-lookup"><span data-stu-id="d0344-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="d0344-761">Dit is wel zinvol omdat elke werkbelastinggroep tooone van vier klassen van de resource is toegewezen: smallrc, mediumrc, largerc, of xlargerc.</span><span class="sxs-lookup"><span data-stu-id="d0344-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="d0344-762">Hallo belang van inzicht in werkbelastinggroepen Hallo is dat enkele van deze werkbelastinggroepen toohigher zijn ingesteld *belang*.</span><span class="sxs-lookup"><span data-stu-id="d0344-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="d0344-763">Urgentie wordt gebruikt voor CPU planning.</span><span class="sxs-lookup"><span data-stu-id="d0344-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="d0344-764">Query's uitvoeren met een hoge urgentie krijgt drie keer meer CPU-cycli dan die met een gemiddeld urgentie.</span><span class="sxs-lookup"><span data-stu-id="d0344-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="d0344-765">Daarom bepalen gelijktijdigheid sleuf toewijzingen ook voor CPU-prioriteit.</span><span class="sxs-lookup"><span data-stu-id="d0344-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="d0344-766">Als een query 16 of meer sleuven verbruikt, voert deze als hoge urgentie.</span><span class="sxs-lookup"><span data-stu-id="d0344-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="d0344-767">Hallo toont volgende tabel Hallo belang toewijzingen voor elke werkbelastinggroep.</span><span class="sxs-lookup"><span data-stu-id="d0344-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="d0344-768">Werkbelasting groep toewijzingen tooconcurrency sleuven en urgentie</span><span class="sxs-lookup"><span data-stu-id="d0344-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="d0344-769">Werkbelastinggroepen</span><span class="sxs-lookup"><span data-stu-id="d0344-769">Workload groups</span></span> | <span data-ttu-id="d0344-770">Gelijktijdigheid sleuf toewijzing</span><span class="sxs-lookup"><span data-stu-id="d0344-770">Concurrency slot mapping</span></span> | <span data-ttu-id="d0344-771">MB / distributie</span><span class="sxs-lookup"><span data-stu-id="d0344-771">MB / Distribution</span></span> | <span data-ttu-id="d0344-772">Toewijzing van belang</span><span class="sxs-lookup"><span data-stu-id="d0344-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="d0344-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="d0344-773">SloDWGroupC00</span></span> |<span data-ttu-id="d0344-774">1</span><span class="sxs-lookup"><span data-stu-id="d0344-774">1</span></span> |<span data-ttu-id="d0344-775">100</span><span class="sxs-lookup"><span data-stu-id="d0344-775">100</span></span> |<span data-ttu-id="d0344-776">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-776">Medium</span></span> |
| <span data-ttu-id="d0344-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="d0344-777">SloDWGroupC01</span></span> |<span data-ttu-id="d0344-778">2</span><span class="sxs-lookup"><span data-stu-id="d0344-778">2</span></span> |<span data-ttu-id="d0344-779">200</span><span class="sxs-lookup"><span data-stu-id="d0344-779">200</span></span> |<span data-ttu-id="d0344-780">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-780">Medium</span></span> |
| <span data-ttu-id="d0344-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="d0344-781">SloDWGroupC02</span></span> |<span data-ttu-id="d0344-782">4</span><span class="sxs-lookup"><span data-stu-id="d0344-782">4</span></span> |<span data-ttu-id="d0344-783">400</span><span class="sxs-lookup"><span data-stu-id="d0344-783">400</span></span> |<span data-ttu-id="d0344-784">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-784">Medium</span></span> |
| <span data-ttu-id="d0344-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-785">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-786">8</span><span class="sxs-lookup"><span data-stu-id="d0344-786">8</span></span> |<span data-ttu-id="d0344-787">800</span><span class="sxs-lookup"><span data-stu-id="d0344-787">800</span></span> |<span data-ttu-id="d0344-788">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-788">Medium</span></span> |
| <span data-ttu-id="d0344-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="d0344-789">SloDWGroupC04</span></span> |<span data-ttu-id="d0344-790">16</span><span class="sxs-lookup"><span data-stu-id="d0344-790">16</span></span> |<span data-ttu-id="d0344-791">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-791">1,600</span></span> |<span data-ttu-id="d0344-792">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-792">High</span></span> |
| <span data-ttu-id="d0344-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="d0344-793">SloDWGroupC05</span></span> |<span data-ttu-id="d0344-794">32</span><span class="sxs-lookup"><span data-stu-id="d0344-794">32</span></span> |<span data-ttu-id="d0344-795">3,200</span><span class="sxs-lookup"><span data-stu-id="d0344-795">3,200</span></span> |<span data-ttu-id="d0344-796">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-796">High</span></span> |
| <span data-ttu-id="d0344-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="d0344-797">SloDWGroupC06</span></span> |<span data-ttu-id="d0344-798">64</span><span class="sxs-lookup"><span data-stu-id="d0344-798">64</span></span> |<span data-ttu-id="d0344-799">6,400</span><span class="sxs-lookup"><span data-stu-id="d0344-799">6,400</span></span> |<span data-ttu-id="d0344-800">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-800">High</span></span> |
| <span data-ttu-id="d0344-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="d0344-801">SloDWGroupC07</span></span> |<span data-ttu-id="d0344-802">128</span><span class="sxs-lookup"><span data-stu-id="d0344-802">128</span></span> |<span data-ttu-id="d0344-803">12,800</span><span class="sxs-lookup"><span data-stu-id="d0344-803">12,800</span></span> |<span data-ttu-id="d0344-804">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-804">High</span></span> |

<span data-ttu-id="d0344-805">Van Hallo **toewijzing en het verbruik van gelijktijdigheid sleuven** grafiek, kunt u zien dat een DW500 1, 4, 8 of 16 gelijktijdigheid sleuven voor smallrc, mediumrc largerc en xlargerc, respectievelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0344-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="d0344-806">U kunt deze waarden opzoeken in de voorgaande diagram toofind Hallo belang voor elke objectklasse resource Hallo.</span><span class="sxs-lookup"><span data-stu-id="d0344-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="d0344-807">Toewijzing van resource klassen tooimportance DW500</span><span class="sxs-lookup"><span data-stu-id="d0344-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="d0344-808">Bronklasse</span><span class="sxs-lookup"><span data-stu-id="d0344-808">Resource class</span></span> | <span data-ttu-id="d0344-809">Werkbelastinggroep</span><span class="sxs-lookup"><span data-stu-id="d0344-809">Workload group</span></span> | <span data-ttu-id="d0344-810">Gelijktijdigheid sleuven gebruikt</span><span class="sxs-lookup"><span data-stu-id="d0344-810">Concurrency slots used</span></span> | <span data-ttu-id="d0344-811">MB / distributie</span><span class="sxs-lookup"><span data-stu-id="d0344-811">MB / Distribution</span></span> | <span data-ttu-id="d0344-812">Urgentie</span><span class="sxs-lookup"><span data-stu-id="d0344-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="d0344-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="d0344-813">smallrc</span></span> |<span data-ttu-id="d0344-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="d0344-814">SloDWGroupC00</span></span> |<span data-ttu-id="d0344-815">1</span><span class="sxs-lookup"><span data-stu-id="d0344-815">1</span></span> |<span data-ttu-id="d0344-816">100</span><span class="sxs-lookup"><span data-stu-id="d0344-816">100</span></span> |<span data-ttu-id="d0344-817">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-817">Medium</span></span> |
| <span data-ttu-id="d0344-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="d0344-818">mediumrc</span></span> |<span data-ttu-id="d0344-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="d0344-819">SloDWGroupC02</span></span> |<span data-ttu-id="d0344-820">4</span><span class="sxs-lookup"><span data-stu-id="d0344-820">4</span></span> |<span data-ttu-id="d0344-821">400</span><span class="sxs-lookup"><span data-stu-id="d0344-821">400</span></span> |<span data-ttu-id="d0344-822">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-822">Medium</span></span> |
| <span data-ttu-id="d0344-823">largerc</span><span class="sxs-lookup"><span data-stu-id="d0344-823">largerc</span></span> |<span data-ttu-id="d0344-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-824">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-825">8</span><span class="sxs-lookup"><span data-stu-id="d0344-825">8</span></span> |<span data-ttu-id="d0344-826">800</span><span class="sxs-lookup"><span data-stu-id="d0344-826">800</span></span> |<span data-ttu-id="d0344-827">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-827">Medium</span></span> |
| <span data-ttu-id="d0344-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="d0344-828">xlargerc</span></span> |<span data-ttu-id="d0344-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="d0344-829">SloDWGroupC04</span></span> |<span data-ttu-id="d0344-830">16</span><span class="sxs-lookup"><span data-stu-id="d0344-830">16</span></span> |<span data-ttu-id="d0344-831">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-831">1,600</span></span> |<span data-ttu-id="d0344-832">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-832">High</span></span> |
| <span data-ttu-id="d0344-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="d0344-833">staticrc10</span></span> |<span data-ttu-id="d0344-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="d0344-834">SloDWGroupC00</span></span> |<span data-ttu-id="d0344-835">1</span><span class="sxs-lookup"><span data-stu-id="d0344-835">1</span></span> |<span data-ttu-id="d0344-836">100</span><span class="sxs-lookup"><span data-stu-id="d0344-836">100</span></span> |<span data-ttu-id="d0344-837">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-837">Medium</span></span> |
| <span data-ttu-id="d0344-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="d0344-838">staticrc20</span></span> |<span data-ttu-id="d0344-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="d0344-839">SloDWGroupC01</span></span> |<span data-ttu-id="d0344-840">2</span><span class="sxs-lookup"><span data-stu-id="d0344-840">2</span></span> |<span data-ttu-id="d0344-841">200</span><span class="sxs-lookup"><span data-stu-id="d0344-841">200</span></span> |<span data-ttu-id="d0344-842">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-842">Medium</span></span> |
| <span data-ttu-id="d0344-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="d0344-843">staticrc30</span></span> |<span data-ttu-id="d0344-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="d0344-844">SloDWGroupC02</span></span> |<span data-ttu-id="d0344-845">4</span><span class="sxs-lookup"><span data-stu-id="d0344-845">4</span></span> |<span data-ttu-id="d0344-846">400</span><span class="sxs-lookup"><span data-stu-id="d0344-846">400</span></span> |<span data-ttu-id="d0344-847">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-847">Medium</span></span> |
| <span data-ttu-id="d0344-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="d0344-848">staticrc40</span></span> |<span data-ttu-id="d0344-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-849">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-850">8</span><span class="sxs-lookup"><span data-stu-id="d0344-850">8</span></span> |<span data-ttu-id="d0344-851">800</span><span class="sxs-lookup"><span data-stu-id="d0344-851">800</span></span> |<span data-ttu-id="d0344-852">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="d0344-852">Medium</span></span> |
| <span data-ttu-id="d0344-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="d0344-853">staticrc50</span></span> |<span data-ttu-id="d0344-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-854">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-855">16</span><span class="sxs-lookup"><span data-stu-id="d0344-855">16</span></span> |<span data-ttu-id="d0344-856">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-856">1,600</span></span> |<span data-ttu-id="d0344-857">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-857">High</span></span> |
| <span data-ttu-id="d0344-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="d0344-858">staticrc60</span></span> |<span data-ttu-id="d0344-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-859">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-860">16</span><span class="sxs-lookup"><span data-stu-id="d0344-860">16</span></span> |<span data-ttu-id="d0344-861">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-861">1,600</span></span> |<span data-ttu-id="d0344-862">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-862">High</span></span> |
| <span data-ttu-id="d0344-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="d0344-863">staticrc70</span></span> |<span data-ttu-id="d0344-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-864">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-865">16</span><span class="sxs-lookup"><span data-stu-id="d0344-865">16</span></span> |<span data-ttu-id="d0344-866">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-866">1,600</span></span> |<span data-ttu-id="d0344-867">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-867">High</span></span> |
| <span data-ttu-id="d0344-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="d0344-868">staticrc80</span></span> |<span data-ttu-id="d0344-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d0344-869">SloDWGroupC03</span></span> |<span data-ttu-id="d0344-870">16</span><span class="sxs-lookup"><span data-stu-id="d0344-870">16</span></span> |<span data-ttu-id="d0344-871">1,600</span><span class="sxs-lookup"><span data-stu-id="d0344-871">1,600</span></span> |<span data-ttu-id="d0344-872">Hoog</span><span class="sxs-lookup"><span data-stu-id="d0344-872">High</span></span> |

<span data-ttu-id="d0344-873">U kunt Hallo DMV-query toolook op Hallo verschillen in de geheugenbrontoewijzing in detail uit Hallo perspectief van de resourceregeling Hallo of tooanalyze actief en historische gebruik van de werkbelastinggroepen Hallo te volgen bij het oplossen.</span><span class="sxs-lookup"><span data-stu-id="d0344-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="d0344-874">Query's die worden geacht gelijktijdigheid limieten</span><span class="sxs-lookup"><span data-stu-id="d0344-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="d0344-875">De meeste query's worden geregeld door de resource-klassen.</span><span class="sxs-lookup"><span data-stu-id="d0344-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="d0344-876">Deze query's moeten binnen het Hallo gelijktijdige query zowel gelijktijdigheid sleuf drempelwaarden passen.</span><span class="sxs-lookup"><span data-stu-id="d0344-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="d0344-877">Een gebruiker kiezen niet, tooexclude een query uit Hallo gelijktijdigheid sleuf model.</span><span class="sxs-lookup"><span data-stu-id="d0344-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="d0344-878">tooreiterate, hello volgende instructies inwilligen resource klassen:</span><span class="sxs-lookup"><span data-stu-id="d0344-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="d0344-879">INSERT SELECT</span><span class="sxs-lookup"><span data-stu-id="d0344-879">INSERT-SELECT</span></span>
* <span data-ttu-id="d0344-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="d0344-880">UPDATE</span></span>
* <span data-ttu-id="d0344-881">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d0344-881">DELETE</span></span>
* <span data-ttu-id="d0344-882">Selecteer (tijdens het opvragen van gebruikerstabellen)</span><span class="sxs-lookup"><span data-stu-id="d0344-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="d0344-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="d0344-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="d0344-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="d0344-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="d0344-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="d0344-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="d0344-886">INDEX MAKEN</span><span class="sxs-lookup"><span data-stu-id="d0344-886">CREATE INDEX</span></span>
* <span data-ttu-id="d0344-887">GECLUSTERDE COLUMNSTORE-INDEX MAKEN</span><span class="sxs-lookup"><span data-stu-id="d0344-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="d0344-888">TABLE AS SELECT (CTAS) MAKEN</span><span class="sxs-lookup"><span data-stu-id="d0344-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="d0344-889">Gegevens laden</span><span class="sxs-lookup"><span data-stu-id="d0344-889">Data loading</span></span>
* <span data-ttu-id="d0344-890">Data movement-bewerkingen uitgevoerd door Hallo Data Movement Service (DMS)</span><span class="sxs-lookup"><span data-stu-id="d0344-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="d0344-891">Query uitzonderingen tooconcurrency limieten</span><span class="sxs-lookup"><span data-stu-id="d0344-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="d0344-892">Sommige query's kunnen niet van toepassing hello resource klasse toowhich Hallo gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d0344-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="d0344-893">Deze uitzonderingen toohello gelijktijdigheid limieten worden aangebracht als Hallo geheugenbronnen die nodig zijn voor een bepaalde opdracht laag, vaak zijn omdat Hallo-opdracht een Metagegevensbewerking is.</span><span class="sxs-lookup"><span data-stu-id="d0344-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="d0344-894">Hallo-doel van deze uitzonderingen is tooavoid groter geheugentoewijzingen voor query's die wordt nooit nodig.</span><span class="sxs-lookup"><span data-stu-id="d0344-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="d0344-895">In dergelijke gevallen toegewezen Hallo standaard kleine bronklasse (smallrc) altijd, ongeacht de werkelijke bronklasse Hallo gebruikt is toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d0344-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="d0344-896">Bijvoorbeeld: `CREATE LOGIN` altijd in smallrc wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d0344-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="d0344-897">Hallo-resources die vereist toofulfill deze bewerking zijn zeer lage dus maakt geen zin tooinclude Hallo query in Hallo gelijktijdigheid sleuf model.</span><span class="sxs-lookup"><span data-stu-id="d0344-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="d0344-898">Deze query's worden ook niet beperkt door de limiet van 32 Hallo gebruikers gelijktijdigheid, een onbeperkt aantal deze query's kunt uitvoeren om toohello sessielimiet van 1024-sessies.</span><span class="sxs-lookup"><span data-stu-id="d0344-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="d0344-899">Hallo instructies te volgen doen resource klassen niet van toepassing:</span><span class="sxs-lookup"><span data-stu-id="d0344-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="d0344-900">MAKEN of DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="d0344-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="d0344-901">ALTER TABLE... SWITCH, GESPLITSTE of partitie samenvoegen</span><span class="sxs-lookup"><span data-stu-id="d0344-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="d0344-902">ALTER INDEX UITSCHAKELEN</span><span class="sxs-lookup"><span data-stu-id="d0344-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="d0344-903">INDEX VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d0344-903">DROP INDEX</span></span>
* <span data-ttu-id="d0344-904">CREATE, UPDATE of DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="d0344-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="d0344-905">TABEL AFKAPPEN</span><span class="sxs-lookup"><span data-stu-id="d0344-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="d0344-906">ALTER AUTORISATIE</span><span class="sxs-lookup"><span data-stu-id="d0344-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="d0344-907">AANMELDING MAKEN</span><span class="sxs-lookup"><span data-stu-id="d0344-907">CREATE LOGIN</span></span>
* <span data-ttu-id="d0344-908">CREATE, ALTER of DROP USER</span><span class="sxs-lookup"><span data-stu-id="d0344-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="d0344-909">CREATE, ALTER of DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="d0344-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="d0344-910">MAKEN of weergave verwijderen</span><span class="sxs-lookup"><span data-stu-id="d0344-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="d0344-911">WAARDEN INVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d0344-911">INSERT VALUES</span></span>
* <span data-ttu-id="d0344-912">Selecteer in het systeemweergaven en DMV 's</span><span class="sxs-lookup"><span data-stu-id="d0344-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="d0344-913">UITLEGGEN</span><span class="sxs-lookup"><span data-stu-id="d0344-913">EXPLAIN</span></span>
* <span data-ttu-id="d0344-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="d0344-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="d0344-915"><a name="changing-user-resource-class-example"></a>Een voorbeeld van een gebruiker resource klasse wijzigen</span><span class="sxs-lookup"><span data-stu-id="d0344-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="d0344-916">**Aanmelding maken:** opent u een verbinding tooyour **master** op Hallo SQL server die als host fungeert voor uw SQL Data Warehouse-database van de database en Hallo volgende opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d0344-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d0344-917">Het is een goed idee toocreate een gebruiker in de hoofddatabase Hallo voor gebruikers van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d0344-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="d0344-918">Maken van een gebruiker in master, kunt een gebruiker toologin met hulpmiddelen zoals SSMS zonder een databasenaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="d0344-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="d0344-919">Ook kunnen ze toouse Hallo object explorer tooview alle databases op een SQL-server.</span><span class="sxs-lookup"><span data-stu-id="d0344-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="d0344-920">Zie voor meer informatie over het maken en beheren van gebruikers [beveiligen van een database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d0344-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="d0344-921">**SQL Data Warehouse-gebruiker maken:** opent u een verbinding toohello **SQL Data Warehouse** database en Hallo volgende opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d0344-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="d0344-922">**Machtigingen toekennen:** Hallo volgende voorbeeld verleent `CONTROL` op Hallo **SQL Data Warehouse** database.</span><span class="sxs-lookup"><span data-stu-id="d0344-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="d0344-923">`CONTROL`op Hallo is het equivalent van db_owner in SQL Server Hallo databaseniveau.</span><span class="sxs-lookup"><span data-stu-id="d0344-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="d0344-924">**Bronklasse verhogen:** gebruik Hallo volgende query tooadd een tooa hoger werkbelasting management gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="d0344-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="d0344-925">**Bronklasse verkleinen:** gebruik Hallo volgende query tooremove een gebruiker vanuit een beheerrol werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="d0344-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d0344-926">Het is niet mogelijk tooremove een gebruiker vanuit smallrc.</span><span class="sxs-lookup"><span data-stu-id="d0344-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="d0344-927">In de wachtrij query detectie- en andere DMV 's</span><span class="sxs-lookup"><span data-stu-id="d0344-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="d0344-928">U kunt Hallo `sys.dm_pdw_exec_requests` DMV tooidentify query's die in een wachtrij gelijktijdigheid wachten.</span><span class="sxs-lookup"><span data-stu-id="d0344-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="d0344-929">Query's te wachten op een site gelijktijdigheid van taken heeft een status van **onderbroken**.</span><span class="sxs-lookup"><span data-stu-id="d0344-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="d0344-930">Werkbelasting management-rollen kunnen worden bekeken met `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="d0344-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="d0344-931">Hallo volgende query ziet u welke rol u elke gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d0344-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="d0344-932">SQL Data Warehouse heeft Hallo volgende wacht typen:</span><span class="sxs-lookup"><span data-stu-id="d0344-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="d0344-933">**LocalQueriesConcurrencyResourceType**: query's die zich buiten de Hallo gelijktijdigheid sleuf framework.</span><span class="sxs-lookup"><span data-stu-id="d0344-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="d0344-934">Functies, zoals DMV-query's en system `SELECT @@VERSION` zijn voorbeelden van lokale query's.</span><span class="sxs-lookup"><span data-stu-id="d0344-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="d0344-935">**UserConcurrencyResourceType**: query's die zich in Hallo gelijktijdigheid sleuf framework bevinden.</span><span class="sxs-lookup"><span data-stu-id="d0344-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="d0344-936">Query's op tabellen van de eindgebruiker vertegenwoordigen voorbeelden die dit brontype wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0344-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="d0344-937">**DmsConcurrencyResourceType**: wacht ten gevolge van data movement-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d0344-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="d0344-938">**BackupConcurrencyResourceType**: deze wachttijd geeft aan dat een database worden back-up.</span><span class="sxs-lookup"><span data-stu-id="d0344-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="d0344-939">Hallo maximale waarde voor dit resourcetype is 1.</span><span class="sxs-lookup"><span data-stu-id="d0344-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="d0344-940">Als meerdere back-ups op Hallo aangevraagd hetzelfde moment, Hallo anderen in de wachtrij wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d0344-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="d0344-941">Hallo `sys.dm_pdw_waits` DMV mag gebruikte toosee welke resources een aanvraag wordt gewacht.</span><span class="sxs-lookup"><span data-stu-id="d0344-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="d0344-942">Hallo `sys.dm_pdw_resource_waits` DMV toont alleen Hallo resource-wacht gebruikt door een bepaalde query.</span><span class="sxs-lookup"><span data-stu-id="d0344-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="d0344-943">Alleen meet Hallo tijd wachten op resources toobe opgegeven wachttijd voor resource, zoals tegengestelde toosignal wachttijd is Hallo tijd die nodig is voor Hallo onderliggende SQL servers tooschedule Hallo-query op Hallo CPU.</span><span class="sxs-lookup"><span data-stu-id="d0344-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="d0344-944">Hallo `sys.dm_pdw_wait_stats` DMV kan worden gebruikt voor analyse van de historische trend van wacht.</span><span class="sxs-lookup"><span data-stu-id="d0344-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="d0344-945">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0344-945">Next steps</span></span>
<span data-ttu-id="d0344-946">Zie voor meer informatie over het beheren van databasegebruikers en beveiliging [beveiligen van een database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d0344-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="d0344-947">Zie voor meer informatie over hoe groter resource klassen kan worden verbeterd geclusterde columnstore-index kwaliteit [opnieuw opbouwen van indexen tooimprove segment kwaliteit].</span><span class="sxs-lookup"><span data-stu-id="d0344-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[opnieuw opbouwen van indexen tooimprove segment kwaliteit]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
