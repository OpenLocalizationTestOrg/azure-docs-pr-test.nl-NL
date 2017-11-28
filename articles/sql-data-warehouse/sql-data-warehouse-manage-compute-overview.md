---
title: aaaManage rekencapaciteit in Azure SQL Data Warehouse (overzicht) | Microsoft Docs
description: Prestaties scale-out mogelijkheden in Azure SQL Data Warehouse. Uitbreiden door dwu's aan te passen of onderbreken en hervatten van compute resources toosave kosten.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="2f06c-104">De rekencapaciteit in Azure SQL Data Warehouse (overzicht) beheren</span><span class="sxs-lookup"><span data-stu-id="2f06c-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f06c-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2f06c-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="2f06c-106">Portal</span><span class="sxs-lookup"><span data-stu-id="2f06c-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="2f06c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f06c-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="2f06c-108">REST</span><span class="sxs-lookup"><span data-stu-id="2f06c-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="2f06c-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="2f06c-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="2f06c-110">Hallo-architectuur van SQL Data Warehouse scheidt opslag en berekeningen, zodat elke tooscale onafhankelijk.</span><span class="sxs-lookup"><span data-stu-id="2f06c-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="2f06c-111">Als gevolg hiervan mag compute onafhankelijk van de hoeveelheid gegevens Hallo geschaalde toomeet prestatie-eisen.</span><span class="sxs-lookup"><span data-stu-id="2f06c-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="2f06c-112">Een natuurlijke gevolg van deze architectuur is dat [facturering] [ billed] voor berekeningen en opslag is gescheiden.</span><span class="sxs-lookup"><span data-stu-id="2f06c-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="2f06c-113">Dit overzicht beschrijft hoe uitbreiden werkt met SQL Data Warehouse en hoe tooutilize Hallo onderbreken, hervatten en scale-mogelijkheden van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2f06c-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="2f06c-114">Raadpleeg Hallo [data warehouse units (dwu's)] [ data warehouse units (DWUs)] pagina toolearn dwu's en prestaties van de relatie.</span><span class="sxs-lookup"><span data-stu-id="2f06c-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="2f06c-115">Hoe compute beheerbewerkingen werken in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2f06c-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="2f06c-116">Hallo-architectuur voor SQL Data Warehouse bestaat uit een beheerknooppunt, rekenknooppunten en Hallo opslaglaag verspreid over 60 distributies.</span><span class="sxs-lookup"><span data-stu-id="2f06c-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="2f06c-117">Tijdens een normale actieve sessie in SQL Data Warehouse het hoofdknooppunt van het systeem beheert Hallo metagegevens en Hallo gedistribueerde queryoptimalisatie bevat.</span><span class="sxs-lookup"><span data-stu-id="2f06c-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="2f06c-118">Onder deze node head zijn uw rekenknooppunten en uw storage-laag.</span><span class="sxs-lookup"><span data-stu-id="2f06c-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="2f06c-119">Voor een 400 DWU heeft uw systeem één hoofdknooppunt, vier rekenknooppunten en Hallo opslaglaag, die bestaan uit 60 distributies.</span><span class="sxs-lookup"><span data-stu-id="2f06c-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="2f06c-120">Wanneer u een schaal ondergaan of bewerking onderbreken, Hallo system eerst is funest alle binnenkomende query's en vervolgens teruggedraaid transacties tooensure een consistente status.</span><span class="sxs-lookup"><span data-stu-id="2f06c-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="2f06c-121">Voor scale-bewerkingen vindt schalen alleen plaats wanneer deze transactionele terugdraaien is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2f06c-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="2f06c-122">Voor het uitvoeren van een scale-up Hallo system bepalingen Hallo extra gewenste aantal rekenknooppunten en begint vervolgens met de Hallo knooppunten toohello opslag berekeningslaag opnieuw te koppelen.</span><span class="sxs-lookup"><span data-stu-id="2f06c-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="2f06c-123">Voor een bewerking omlaag schalen hello overbodige knooppunten worden vrijgegeven en Hallo resterende compute nodes toohello kunt u het juiste aantal distributies opnieuw zichzelf koppelen.</span><span class="sxs-lookup"><span data-stu-id="2f06c-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="2f06c-124">Voor een bewerking onderbreken compute alle knooppunten worden vrijgegeven en uw systeem ietwat tal van metagegevens operations tooleave uw laatste systeem stabiel is.</span><span class="sxs-lookup"><span data-stu-id="2f06c-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="2f06c-125">DWU</span><span class="sxs-lookup"><span data-stu-id="2f06c-125">DWU</span></span>  | <span data-ttu-id="2f06c-126">\#van rekenknooppunten</span><span class="sxs-lookup"><span data-stu-id="2f06c-126">\#of compute nodes</span></span> | <span data-ttu-id="2f06c-127">\#van distributies per knooppunt</span><span class="sxs-lookup"><span data-stu-id="2f06c-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="2f06c-128">100</span><span class="sxs-lookup"><span data-stu-id="2f06c-128">100</span></span>  | <span data-ttu-id="2f06c-129">1</span><span class="sxs-lookup"><span data-stu-id="2f06c-129">1</span></span>                  | <span data-ttu-id="2f06c-130">60</span><span class="sxs-lookup"><span data-stu-id="2f06c-130">60</span></span>                           |
| <span data-ttu-id="2f06c-131">200</span><span class="sxs-lookup"><span data-stu-id="2f06c-131">200</span></span>  | <span data-ttu-id="2f06c-132">2</span><span class="sxs-lookup"><span data-stu-id="2f06c-132">2</span></span>                  | <span data-ttu-id="2f06c-133">30</span><span class="sxs-lookup"><span data-stu-id="2f06c-133">30</span></span>                           |
| <span data-ttu-id="2f06c-134">300</span><span class="sxs-lookup"><span data-stu-id="2f06c-134">300</span></span>  | <span data-ttu-id="2f06c-135">3</span><span class="sxs-lookup"><span data-stu-id="2f06c-135">3</span></span>                  | <span data-ttu-id="2f06c-136">20</span><span class="sxs-lookup"><span data-stu-id="2f06c-136">20</span></span>                           |
| <span data-ttu-id="2f06c-137">400</span><span class="sxs-lookup"><span data-stu-id="2f06c-137">400</span></span>  | <span data-ttu-id="2f06c-138">4</span><span class="sxs-lookup"><span data-stu-id="2f06c-138">4</span></span>                  | <span data-ttu-id="2f06c-139">15</span><span class="sxs-lookup"><span data-stu-id="2f06c-139">15</span></span>                           |
| <span data-ttu-id="2f06c-140">500</span><span class="sxs-lookup"><span data-stu-id="2f06c-140">500</span></span>  | <span data-ttu-id="2f06c-141">5</span><span class="sxs-lookup"><span data-stu-id="2f06c-141">5</span></span>                  | <span data-ttu-id="2f06c-142">12</span><span class="sxs-lookup"><span data-stu-id="2f06c-142">12</span></span>                           |
| <span data-ttu-id="2f06c-143">600</span><span class="sxs-lookup"><span data-stu-id="2f06c-143">600</span></span>  | <span data-ttu-id="2f06c-144">6</span><span class="sxs-lookup"><span data-stu-id="2f06c-144">6</span></span>                  | <span data-ttu-id="2f06c-145">10</span><span class="sxs-lookup"><span data-stu-id="2f06c-145">10</span></span>                           |
| <span data-ttu-id="2f06c-146">1000</span><span class="sxs-lookup"><span data-stu-id="2f06c-146">1000</span></span> | <span data-ttu-id="2f06c-147">10</span><span class="sxs-lookup"><span data-stu-id="2f06c-147">10</span></span>                 | <span data-ttu-id="2f06c-148">6</span><span class="sxs-lookup"><span data-stu-id="2f06c-148">6</span></span>                            |
| <span data-ttu-id="2f06c-149">1200</span><span class="sxs-lookup"><span data-stu-id="2f06c-149">1200</span></span> | <span data-ttu-id="2f06c-150">12</span><span class="sxs-lookup"><span data-stu-id="2f06c-150">12</span></span>                 | <span data-ttu-id="2f06c-151">5</span><span class="sxs-lookup"><span data-stu-id="2f06c-151">5</span></span>                            |
| <span data-ttu-id="2f06c-152">1500</span><span class="sxs-lookup"><span data-stu-id="2f06c-152">1500</span></span> | <span data-ttu-id="2f06c-153">15</span><span class="sxs-lookup"><span data-stu-id="2f06c-153">15</span></span>                 | <span data-ttu-id="2f06c-154">4</span><span class="sxs-lookup"><span data-stu-id="2f06c-154">4</span></span>                            |
| <span data-ttu-id="2f06c-155">2000</span><span class="sxs-lookup"><span data-stu-id="2f06c-155">2000</span></span> | <span data-ttu-id="2f06c-156">20</span><span class="sxs-lookup"><span data-stu-id="2f06c-156">20</span></span>                 | <span data-ttu-id="2f06c-157">3</span><span class="sxs-lookup"><span data-stu-id="2f06c-157">3</span></span>                            |
| <span data-ttu-id="2f06c-158">3000</span><span class="sxs-lookup"><span data-stu-id="2f06c-158">3000</span></span> | <span data-ttu-id="2f06c-159">30</span><span class="sxs-lookup"><span data-stu-id="2f06c-159">30</span></span>                 | <span data-ttu-id="2f06c-160">2</span><span class="sxs-lookup"><span data-stu-id="2f06c-160">2</span></span>                            |
| <span data-ttu-id="2f06c-161">6000</span><span class="sxs-lookup"><span data-stu-id="2f06c-161">6000</span></span> | <span data-ttu-id="2f06c-162">60</span><span class="sxs-lookup"><span data-stu-id="2f06c-162">60</span></span>                 | <span data-ttu-id="2f06c-163">1</span><span class="sxs-lookup"><span data-stu-id="2f06c-163">1</span></span>                            |

<span data-ttu-id="2f06c-164">Hallo drie primaire functies voor het beheren van compute zijn:</span><span class="sxs-lookup"><span data-stu-id="2f06c-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="2f06c-165">Onderbreken</span><span class="sxs-lookup"><span data-stu-id="2f06c-165">Pause</span></span>
2. <span data-ttu-id="2f06c-166">Hervatten</span><span class="sxs-lookup"><span data-stu-id="2f06c-166">Resume</span></span>
3. <span data-ttu-id="2f06c-167">Schalen</span><span class="sxs-lookup"><span data-stu-id="2f06c-167">Scale</span></span>

<span data-ttu-id="2f06c-168">Elk van deze bewerkingen kan toocomplete van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="2f06c-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="2f06c-169">Als u automatisch bent schalen/onderbreken/hervatten klikt, kunt u tooimplement logica tooensure dat bepaalde bewerkingen zijn voltooid voordat u doorgaat met een andere actie.</span><span class="sxs-lookup"><span data-stu-id="2f06c-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="2f06c-170">Controleren van de status van database Hallo via verschillende eindpunten kunt u toocorrectly implementeren automatisering van dergelijke bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2f06c-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="2f06c-171">Hallo-portal biedt melding na voltooiing van een bewerking en Hallo databases huidige status, maar is niet toegestaan voor de programmatische controle van status.</span><span class="sxs-lookup"><span data-stu-id="2f06c-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="2f06c-172">COMPUTE beheerfunctionaliteit bestaat niet in alle eindpunten.</span><span class="sxs-lookup"><span data-stu-id="2f06c-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="2f06c-173">Onderbreken/hervatten</span><span class="sxs-lookup"><span data-stu-id="2f06c-173">Pause/Resume</span></span> | <span data-ttu-id="2f06c-174">Schalen</span><span class="sxs-lookup"><span data-stu-id="2f06c-174">Scale</span></span> | <span data-ttu-id="2f06c-175">Controleer de databasestatus van de</span><span class="sxs-lookup"><span data-stu-id="2f06c-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="2f06c-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2f06c-176">Azure portal</span></span> | <span data-ttu-id="2f06c-177">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-177">Yes</span></span>          | <span data-ttu-id="2f06c-178">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-178">Yes</span></span>   | <span data-ttu-id="2f06c-179">**Nee**</span><span class="sxs-lookup"><span data-stu-id="2f06c-179">**No**</span></span>               |
| <span data-ttu-id="2f06c-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f06c-180">PowerShell</span></span>   | <span data-ttu-id="2f06c-181">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-181">Yes</span></span>          | <span data-ttu-id="2f06c-182">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-182">Yes</span></span>   | <span data-ttu-id="2f06c-183">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-183">Yes</span></span>                  |
| <span data-ttu-id="2f06c-184">REST API</span><span class="sxs-lookup"><span data-stu-id="2f06c-184">REST API</span></span>     | <span data-ttu-id="2f06c-185">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-185">Yes</span></span>          | <span data-ttu-id="2f06c-186">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-186">Yes</span></span>   | <span data-ttu-id="2f06c-187">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-187">Yes</span></span>                  |
| <span data-ttu-id="2f06c-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="2f06c-188">T-SQL</span></span>        | <span data-ttu-id="2f06c-189">**Nee**</span><span class="sxs-lookup"><span data-stu-id="2f06c-189">**No**</span></span>       | <span data-ttu-id="2f06c-190">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-190">Yes</span></span>   | <span data-ttu-id="2f06c-191">Ja</span><span class="sxs-lookup"><span data-stu-id="2f06c-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="2f06c-192">Scale compute</span><span class="sxs-lookup"><span data-stu-id="2f06c-192">Scale compute</span></span>

<span data-ttu-id="2f06c-193">Prestaties in SQL Data Warehouse wordt gemeten in [data warehouse units (dwu's)] [ data warehouse units (DWUs)] dit is een abstracte meting van de compute-bronnen zoals CPU, geheugen en i/o-bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="2f06c-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="2f06c-194">Een gebruiker die u tooscale hun systeemprestaties wenst kunt doen met behulp van verschillende middelen zoals via het Hallo-portal, T-SQL en REST-API's.</span><span class="sxs-lookup"><span data-stu-id="2f06c-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="2f06c-195">Hoe ik compute schalen?</span><span class="sxs-lookup"><span data-stu-id="2f06c-195">How do I scale compute?</span></span>
<span data-ttu-id="2f06c-196">Rekencapaciteit wordt voor u SQL Data Warehouse beheerd door Hallo DWU-instelling te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2f06c-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="2f06c-197">Prestaties [lineair] [ linearly] als u meer DWU voor bepaalde bewerkingen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="2f06c-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="2f06c-198">We bieden DWU-aanbiedingen die ervoor zorgen dat de prestaties van uw merkbaar wordt veranderen wanneer u uw systeem omhoog of omlaag schalen.</span><span class="sxs-lookup"><span data-stu-id="2f06c-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="2f06c-199">tooadjust dwu's, kunt u een van deze afzonderlijke methoden kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f06c-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="2f06c-200">[Schaal rekenkracht met Azure portal][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="2f06c-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="2f06c-201">[Schaal rekenkracht met PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2f06c-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="2f06c-202">[De rekencapaciteit schaal met REST-API 's][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2f06c-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="2f06c-203">[Schaal rekenkracht met TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="2f06c-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="2f06c-204">Het aantal dwu's moet ik gebruiken?</span><span class="sxs-lookup"><span data-stu-id="2f06c-204">How many DWUs should I use?</span></span>

<span data-ttu-id="2f06c-205">toounderstand welke de ideale DWU-waarde is, probeer omhoog en omlaag schalen en na het laden van uw gegevens enkele query's uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="2f06c-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="2f06c-206">Omdat schalen snel is, kunt u verschillende prestatieniveaus proberen in een uur of minder.</span><span class="sxs-lookup"><span data-stu-id="2f06c-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="2f06c-207">SQL Data Warehouse is ontworpen tooprocess grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="2f06c-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="2f06c-208">toosee-mogelijkheden voor schaling vooral op grotere Dwu ervan waar u wilt dat toouse een grote gegevensset die nadert of hoger is dan 1 TB.</span><span class="sxs-lookup"><span data-stu-id="2f06c-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="2f06c-209">Aanbevelingen voor het zoeken naar Hallo best DWU voor uw workload:</span><span class="sxs-lookup"><span data-stu-id="2f06c-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="2f06c-210">Beginnen met het selecteren van een kleinere DWU-prestatieniveau voor een datawarehouse in ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="2f06c-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="2f06c-211">Een goed uitgangspunt is DW400 of DW200.</span><span class="sxs-lookup"><span data-stu-id="2f06c-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="2f06c-212">De toepassingsprestaties van uw te bewaken, toohello prestaties die u merkt observeren Hallo aantal dwu's geselecteerd vergeleken.</span><span class="sxs-lookup"><span data-stu-id="2f06c-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="2f06c-213">Bepalen hoeveel prestatievermogen sneller of langzamer lineaire schaal ervan uitgaande dat moet worden voor u tooreach Hallo optimaal prestatieniveau voor uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="2f06c-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="2f06c-214">Vergroten of verkleinen Hallo aantal dwu's in verhouding toohow veel sneller of langzamer dat u wilt dat uw tooperform werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="2f06c-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="2f06c-215">Blijven correcties totdat u een optimaal prestatieniveau voor uw zakelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="2f06c-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2f06c-216">Prestaties van query's worden alleen verhoogd met meer garandeert als Hallo werk kan worden gesplitst tussen rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="2f06c-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="2f06c-217">Als u merkt dat schalen niet van de prestaties van uw wijzigen is, check onze artikelen toocheck of uw gegevens ongelijkmatig verdeeld is of als u een grote hoeveelheid gegevensverplaatsing introduceren afstemmen van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="2f06c-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="2f06c-218">Wanneer moet ik dwu's schalen?</span><span class="sxs-lookup"><span data-stu-id="2f06c-218">When should I scale DWUs?</span></span>
<span data-ttu-id="2f06c-219">Dwu's schalen wijzigt Hallo belangrijke scenario's te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f06c-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="2f06c-220">Prestaties van systeem voor scans, aggregaties en CTAS instructies Hallo wijzigen lineair</span><span class="sxs-lookup"><span data-stu-id="2f06c-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="2f06c-221">Hallo aantal en schrijfprogramma te verhogen bij het laden met PolyBase</span><span class="sxs-lookup"><span data-stu-id="2f06c-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="2f06c-222">Maximum aantal gelijktijdige query's en gelijktijdigheid sleuven</span><span class="sxs-lookup"><span data-stu-id="2f06c-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="2f06c-223">Aanbevelingen voor wanneer tooscale dwu's:</span><span class="sxs-lookup"><span data-stu-id="2f06c-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="2f06c-224">Voordat u een zware laad- of transformatiebewerking bewerking uitvoert, opschalen dwu's zodat uw gegevens sneller beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2f06c-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="2f06c-225">Tijdens de kantooruren piek, schalen tooaccommodate grotere aantallen gelijktijdige query's.</span><span class="sxs-lookup"><span data-stu-id="2f06c-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="2f06c-226">De rekencapaciteit onderbreken</span><span class="sxs-lookup"><span data-stu-id="2f06c-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="2f06c-227">een database toopause gebruik van deze afzonderlijke methoden.</span><span class="sxs-lookup"><span data-stu-id="2f06c-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="2f06c-228">[Compute onderbreken met de Azure-portal][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="2f06c-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="2f06c-229">[De rekencapaciteit onderbreken met PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2f06c-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="2f06c-230">[De rekencapaciteit onderbreken met REST-API 's][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2f06c-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="2f06c-231">Compute hervatten</span><span class="sxs-lookup"><span data-stu-id="2f06c-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="2f06c-232">een database tooresume gebruik van deze afzonderlijke methoden.</span><span class="sxs-lookup"><span data-stu-id="2f06c-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="2f06c-233">[De berekeningen hervatten met Azure portal][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="2f06c-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="2f06c-234">[De berekeningen hervatten met PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2f06c-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="2f06c-235">[De berekeningen hervatten met REST-API 's][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2f06c-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="2f06c-236">Controleer de databasestatus van de</span><span class="sxs-lookup"><span data-stu-id="2f06c-236">Check database state</span></span> 

<span data-ttu-id="2f06c-237">een database tooresume gebruik van deze afzonderlijke methoden.</span><span class="sxs-lookup"><span data-stu-id="2f06c-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="2f06c-238">[Controleer de databasestatus van de met T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="2f06c-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="2f06c-239">[Controleer de databasestatus van de met PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="2f06c-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="2f06c-240">[Controleer de databasestatus van de met de REST-API 's][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="2f06c-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="2f06c-241">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="2f06c-241">Permissions</span></span>

<span data-ttu-id="2f06c-242">Schalen Hallo-database vereist Hallo machtigingen die zijn beschreven in [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="2f06c-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="2f06c-243">Onderbreken en hervatten vereisen Hallo [SQL DB Contributor] [ SQL DB Contributor] machtiging specifiek Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="2f06c-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="2f06c-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f06c-244">Next steps</span></span>
<span data-ttu-id="2f06c-245">Raadpleeg toohello artikelen toohelp u enkele aanvullende prestatie-concepten begrijpt te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f06c-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="2f06c-246">[Werkbelasting en gelijktijdigheid management][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="2f06c-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="2f06c-247">[Overzicht van de tabel-ontwerp][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="2f06c-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="2f06c-248">[Tabeldistributie][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="2f06c-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="2f06c-249">[Tabel indexeren][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="2f06c-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="2f06c-250">[Partitioneren van tabel][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="2f06c-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="2f06c-251">[Tabelstatistieken][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="2f06c-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="2f06c-252">[Aanbevolen procedures][Best practices]</span><span class="sxs-lookup"><span data-stu-id="2f06c-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
