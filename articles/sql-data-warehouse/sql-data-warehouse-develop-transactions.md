---
title: aaaTransactions in SQL Data Warehouse | Microsoft Docs
description: Tips voor het implementeren van transacties in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="4c227-103">Transacties in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="4c227-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="4c227-104">Zoals u verwachten zou, SQL Data Warehouse biedt ondersteuning voor transacties als onderdeel van de datawarehouse-workload Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c227-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="4c227-105">Echter wordt tooensure Hallo prestaties van SQL Data Warehouse onderhouden op grote schaal die sommige functies beperkt wanneer zijn vergeleken tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c227-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="4c227-106">In dit artikel worden gemarkeerd Hallo verschillen en lijsten Hallo anderen.</span><span class="sxs-lookup"><span data-stu-id="4c227-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="4c227-107">Transactie-isolatieniveaus</span><span class="sxs-lookup"><span data-stu-id="4c227-107">Transaction isolation levels</span></span>
<span data-ttu-id="4c227-108">SQL Data Warehouse implementeert ACID-transactions.</span><span class="sxs-lookup"><span data-stu-id="4c227-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="4c227-109">Hallo isolatie van Hallo transactionele ondersteuning is echter beperkt te`READ UNCOMMITTED` en dit kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4c227-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="4c227-110">U kunt een aantal codering methoden tooprevent vervuild gegevens leest als dit een probleem voor u is kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="4c227-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="4c227-111">Hallo populairste methoden gebruikmaken van CTAS en tabel partitie overschakelen (vaak ook bekend als verschuivende venster patroon Hallo) tooprevent gebruikers van een query die nog steeds wordt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="4c227-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="4c227-112">Weergaven die vooraf filter Hallo gegevens is ook een populaire benadering.</span><span class="sxs-lookup"><span data-stu-id="4c227-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="4c227-113">De grootte van de transactie</span><span class="sxs-lookup"><span data-stu-id="4c227-113">Transaction size</span></span>
<span data-ttu-id="4c227-114">Er is een wijziging één transactie in grootte beperkt.</span><span class="sxs-lookup"><span data-stu-id="4c227-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="4c227-115">Hallo limiet is vandaag de dag "per distributiepunt' toegepast.</span><span class="sxs-lookup"><span data-stu-id="4c227-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="4c227-116">Daarom kan Hallo totale toewijzing worden vermenigvuldigd Hallo limiet Hallo distributie count.</span><span class="sxs-lookup"><span data-stu-id="4c227-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="4c227-117">Hallo distributie cap deelt tooapproximate Hallo maximale aantal rijen in de transactie Hallo door Hallo totale grootte van elke rij.</span><span class="sxs-lookup"><span data-stu-id="4c227-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="4c227-118">Houd rekening met een gemiddelde kolomlengte duurt in plaats van met behulp van de maximale grootte Hallo voor kolommen met variabele lengte.</span><span class="sxs-lookup"><span data-stu-id="4c227-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="4c227-119">In de tabel hieronder Hallo Hallo zijn volgende veronderstellingen aangebracht:</span><span class="sxs-lookup"><span data-stu-id="4c227-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="4c227-120">Een gelijkmatige verdeling van gegevens is opgetreden</span><span class="sxs-lookup"><span data-stu-id="4c227-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="4c227-121">de gemiddelde rijlengte Hallo is 250 bytes</span><span class="sxs-lookup"><span data-stu-id="4c227-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="4c227-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="4c227-122">[DWU][DWU]</span></span> | <span data-ttu-id="4c227-123">Cap per distributiepunt (GiB)</span><span class="sxs-lookup"><span data-stu-id="4c227-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="4c227-124">Aantal distributies</span><span class="sxs-lookup"><span data-stu-id="4c227-124">Number of Distributions</span></span> | <span data-ttu-id="4c227-125">Transactie maximumgrootte (GiB)</span><span class="sxs-lookup"><span data-stu-id="4c227-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="4c227-126"># Rijen per distributiepunt</span><span class="sxs-lookup"><span data-stu-id="4c227-126"># Rows per distribution</span></span> | <span data-ttu-id="4c227-127">Maximumaantal rijen per transactie</span><span class="sxs-lookup"><span data-stu-id="4c227-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4c227-128">DW100</span><span class="sxs-lookup"><span data-stu-id="4c227-128">DW100</span></span> |<span data-ttu-id="4c227-129">1</span><span class="sxs-lookup"><span data-stu-id="4c227-129">1</span></span> |<span data-ttu-id="4c227-130">60</span><span class="sxs-lookup"><span data-stu-id="4c227-130">60</span></span> |<span data-ttu-id="4c227-131">60</span><span class="sxs-lookup"><span data-stu-id="4c227-131">60</span></span> |<span data-ttu-id="4c227-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-132">4,000,000</span></span> |<span data-ttu-id="4c227-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-133">240,000,000</span></span> |
| <span data-ttu-id="4c227-134">DW200</span><span class="sxs-lookup"><span data-stu-id="4c227-134">DW200</span></span> |<span data-ttu-id="4c227-135">1.5</span><span class="sxs-lookup"><span data-stu-id="4c227-135">1.5</span></span> |<span data-ttu-id="4c227-136">60</span><span class="sxs-lookup"><span data-stu-id="4c227-136">60</span></span> |<span data-ttu-id="4c227-137">90</span><span class="sxs-lookup"><span data-stu-id="4c227-137">90</span></span> |<span data-ttu-id="4c227-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-138">6,000,000</span></span> |<span data-ttu-id="4c227-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-139">360,000,000</span></span> |
| <span data-ttu-id="4c227-140">DW300</span><span class="sxs-lookup"><span data-stu-id="4c227-140">DW300</span></span> |<span data-ttu-id="4c227-141">2.25</span><span class="sxs-lookup"><span data-stu-id="4c227-141">2.25</span></span> |<span data-ttu-id="4c227-142">60</span><span class="sxs-lookup"><span data-stu-id="4c227-142">60</span></span> |<span data-ttu-id="4c227-143">135</span><span class="sxs-lookup"><span data-stu-id="4c227-143">135</span></span> |<span data-ttu-id="4c227-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-144">9,000,000</span></span> |<span data-ttu-id="4c227-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-145">540,000,000</span></span> |
| <span data-ttu-id="4c227-146">DW400</span><span class="sxs-lookup"><span data-stu-id="4c227-146">DW400</span></span> |<span data-ttu-id="4c227-147">3</span><span class="sxs-lookup"><span data-stu-id="4c227-147">3</span></span> |<span data-ttu-id="4c227-148">60</span><span class="sxs-lookup"><span data-stu-id="4c227-148">60</span></span> |<span data-ttu-id="4c227-149">180</span><span class="sxs-lookup"><span data-stu-id="4c227-149">180</span></span> |<span data-ttu-id="4c227-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-150">12,000,000</span></span> |<span data-ttu-id="4c227-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-151">720,000,000</span></span> |
| <span data-ttu-id="4c227-152">DW500</span><span class="sxs-lookup"><span data-stu-id="4c227-152">DW500</span></span> |<span data-ttu-id="4c227-153">3.75</span><span class="sxs-lookup"><span data-stu-id="4c227-153">3.75</span></span> |<span data-ttu-id="4c227-154">60</span><span class="sxs-lookup"><span data-stu-id="4c227-154">60</span></span> |<span data-ttu-id="4c227-155">225</span><span class="sxs-lookup"><span data-stu-id="4c227-155">225</span></span> |<span data-ttu-id="4c227-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-156">15,000,000</span></span> |<span data-ttu-id="4c227-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-157">900,000,000</span></span> |
| <span data-ttu-id="4c227-158">DW600</span><span class="sxs-lookup"><span data-stu-id="4c227-158">DW600</span></span> |<span data-ttu-id="4c227-159">4.5</span><span class="sxs-lookup"><span data-stu-id="4c227-159">4.5</span></span> |<span data-ttu-id="4c227-160">60</span><span class="sxs-lookup"><span data-stu-id="4c227-160">60</span></span> |<span data-ttu-id="4c227-161">270</span><span class="sxs-lookup"><span data-stu-id="4c227-161">270</span></span> |<span data-ttu-id="4c227-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-162">18,000,000</span></span> |<span data-ttu-id="4c227-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-163">1,080,000,000</span></span> |
| <span data-ttu-id="4c227-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="4c227-164">DW1000</span></span> |<span data-ttu-id="4c227-165">7.5</span><span class="sxs-lookup"><span data-stu-id="4c227-165">7.5</span></span> |<span data-ttu-id="4c227-166">60</span><span class="sxs-lookup"><span data-stu-id="4c227-166">60</span></span> |<span data-ttu-id="4c227-167">450</span><span class="sxs-lookup"><span data-stu-id="4c227-167">450</span></span> |<span data-ttu-id="4c227-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-168">30,000,000</span></span> |<span data-ttu-id="4c227-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-169">1,800,000,000</span></span> |
| <span data-ttu-id="4c227-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="4c227-170">DW1200</span></span> |<span data-ttu-id="4c227-171">9</span><span class="sxs-lookup"><span data-stu-id="4c227-171">9</span></span> |<span data-ttu-id="4c227-172">60</span><span class="sxs-lookup"><span data-stu-id="4c227-172">60</span></span> |<span data-ttu-id="4c227-173">540</span><span class="sxs-lookup"><span data-stu-id="4c227-173">540</span></span> |<span data-ttu-id="4c227-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-174">36,000,000</span></span> |<span data-ttu-id="4c227-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-175">2,160,000,000</span></span> |
| <span data-ttu-id="4c227-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="4c227-176">DW1500</span></span> |<span data-ttu-id="4c227-177">11.25</span><span class="sxs-lookup"><span data-stu-id="4c227-177">11.25</span></span> |<span data-ttu-id="4c227-178">60</span><span class="sxs-lookup"><span data-stu-id="4c227-178">60</span></span> |<span data-ttu-id="4c227-179">675</span><span class="sxs-lookup"><span data-stu-id="4c227-179">675</span></span> |<span data-ttu-id="4c227-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-180">45,000,000</span></span> |<span data-ttu-id="4c227-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-181">2,700,000,000</span></span> |
| <span data-ttu-id="4c227-182">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="4c227-182">DW2000</span></span> |<span data-ttu-id="4c227-183">15</span><span class="sxs-lookup"><span data-stu-id="4c227-183">15</span></span> |<span data-ttu-id="4c227-184">60</span><span class="sxs-lookup"><span data-stu-id="4c227-184">60</span></span> |<span data-ttu-id="4c227-185">900</span><span class="sxs-lookup"><span data-stu-id="4c227-185">900</span></span> |<span data-ttu-id="4c227-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-186">60,000,000</span></span> |<span data-ttu-id="4c227-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-187">3,600,000,000</span></span> |
| <span data-ttu-id="4c227-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="4c227-188">DW3000</span></span> |<span data-ttu-id="4c227-189">22.5</span><span class="sxs-lookup"><span data-stu-id="4c227-189">22.5</span></span> |<span data-ttu-id="4c227-190">60</span><span class="sxs-lookup"><span data-stu-id="4c227-190">60</span></span> |<span data-ttu-id="4c227-191">1,350</span><span class="sxs-lookup"><span data-stu-id="4c227-191">1,350</span></span> |<span data-ttu-id="4c227-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-192">90,000,000</span></span> |<span data-ttu-id="4c227-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-193">5,400,000,000</span></span> |
| <span data-ttu-id="4c227-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="4c227-194">DW6000</span></span> |<span data-ttu-id="4c227-195">45</span><span class="sxs-lookup"><span data-stu-id="4c227-195">45</span></span> |<span data-ttu-id="4c227-196">60</span><span class="sxs-lookup"><span data-stu-id="4c227-196">60</span></span> |<span data-ttu-id="4c227-197">2,700</span><span class="sxs-lookup"><span data-stu-id="4c227-197">2,700</span></span> |<span data-ttu-id="4c227-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-198">180,000,000</span></span> |<span data-ttu-id="4c227-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="4c227-199">10,800,000,000</span></span> |

<span data-ttu-id="4c227-200">Hallo transactie groottelimiet wordt per transactie of bewerking toegepast.</span><span class="sxs-lookup"><span data-stu-id="4c227-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="4c227-201">Het is niet toegepast op alle gelijktijdige transacties.</span><span class="sxs-lookup"><span data-stu-id="4c227-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="4c227-202">Elke transactie is daarom toowrite deze hoeveelheid gegevens toohello logboek toegestaan.</span><span class="sxs-lookup"><span data-stu-id="4c227-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="4c227-203">toooptimize en minimaliseren Hallo en de hoeveelheid gegevens geschreven toohello logboek Raadpleeg toohello [transacties aanbevolen procedures] [ Transactions best practices] artikel.</span><span class="sxs-lookup"><span data-stu-id="4c227-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="4c227-204">maximale grootte van de transactie kan alleen worden bereikt voor HASH of ROUND_ROBIN gedistribueerd tabellen waarbij Hallo verspreiden Hallo gegevens Hallo is even.</span><span class="sxs-lookup"><span data-stu-id="4c227-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="4c227-205">Als Hallo transactie is schrijven van gegevens op een wijze vertekende toohello distributies is hello limiet waarschijnlijk toobe voorafgaande toohello transactie maximale grootte heeft bereikt.</span><span class="sxs-lookup"><span data-stu-id="4c227-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="4c227-206">Transactiestatus</span><span class="sxs-lookup"><span data-stu-id="4c227-206">Transaction state</span></span>
<span data-ttu-id="4c227-207">SQL Data Warehouse gebruikt Hallo XACT_STATE() functie tooreport een mislukte transactie Hallo waarde -2.</span><span class="sxs-lookup"><span data-stu-id="4c227-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="4c227-208">Dit betekent dat Hallo transactie is mislukt en is gemarkeerd voor alleen terugdraaien</span><span class="sxs-lookup"><span data-stu-id="4c227-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="4c227-209">Hallo gebruiken-2 Hallo XACT_STATE functie toodenote een mislukte transactie vertegenwoordigt verschillend gedrag tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c227-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="4c227-210">Hallo waarde -1 toorepresent een niet-doorvoerbare transactie maakt gebruik van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4c227-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="4c227-211">SQL Server kan een aantal fouten binnen een transactie zonder toobe gemarkeerd als niet-doorvoerbare tolereren.</span><span class="sxs-lookup"><span data-stu-id="4c227-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="4c227-212">Bijvoorbeeld `SELECT 1/0` wordt een fout veroorzaken, maar niet afdwingen van een transactie in een niet-doorvoerbare staat.</span><span class="sxs-lookup"><span data-stu-id="4c227-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="4c227-213">SQL Server kan ook leesbewerkingen in niet-doorvoerbare transactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c227-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="4c227-214">Echter kunt SQL Data Warehouse u niet doen.</span><span class="sxs-lookup"><span data-stu-id="4c227-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="4c227-215">Als een fout in een SQL Data Warehouse-transactie optreedt wordt automatisch overgeschakeld naar de Hallo -2-status en kunt u niet kunt toomake selecteren een verdere instructies tot het Hallo-instructie is teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="4c227-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="4c227-216">Het is daarom belangrijk toocheck uw toepassing code toosee als XACT_STATE() als u gebruikt moet mogelijk toomake codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="4c227-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="4c227-217">Bijvoorbeeld, in SQL Server mogelijk ziet u een transactie die er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4c227-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="4c227-218">Als u uw code laat als hierboven krijgt u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4c227-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="4c227-219">Bericht 111233, 16 niveau 1 staat, regel 1 111233; Hallo huidige transactie is afgebroken en alle wijzigingen in afwachting zijn teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="4c227-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="4c227-220">Oorzaak: Een transactie in een status terugdraaien van de alleen-lezen is niet expliciet teruggedraaid voordat een DDL-, DML- of SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="4c227-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="4c227-221">U wordt ook Hallo-uitvoer van Hallo ERROR_ * functies niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="4c227-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="4c227-222">Hallo-code moet in SQL Data Warehouse toobe enigszins gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="4c227-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="4c227-223">Hallo verwacht gedrag is nu waargenomen.</span><span class="sxs-lookup"><span data-stu-id="4c227-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="4c227-224">Hallo-fout in Hallo transactie wordt beheerd en Hallo ERROR_ * functies waarden opgeven, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="4c227-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="4c227-225">Alles wat is gewijzigd dat Hallo is `ROLLBACK` Hallo transactie toohappen had voordat Hallo Hallo foutinformatie in Hallo lezen `CATCH` blok.</span><span class="sxs-lookup"><span data-stu-id="4c227-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="4c227-226">De functie Error_Line()</span><span class="sxs-lookup"><span data-stu-id="4c227-226">Error_Line() function</span></span>
<span data-ttu-id="4c227-227">Het is ook opgemerkt dat SQL Data Warehouse niet implementeren of Hallo ERROR_LINE() functie ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="4c227-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="4c227-228">Als u dit in uw code u tooremove, moet deze toobe compatibel zijn met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4c227-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="4c227-229">Query labels in uw code gebruiken in plaats daarvan tooimplement dezelfde functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="4c227-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="4c227-230">Raadpleeg toohello [LABEL] [ LABEL] artikel voor meer informatie over deze functie.</span><span class="sxs-lookup"><span data-stu-id="4c227-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="4c227-231">Met behulp van THROW en RAISERROR</span><span class="sxs-lookup"><span data-stu-id="4c227-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="4c227-232">THROW is moderne implementatie voor uitzonderingen in SQL Data Warehouse Hallo maar RAISERROR wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4c227-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="4c227-233">Er zijn een paar verschillen waarde aandacht toohowever betaalt.</span><span class="sxs-lookup"><span data-stu-id="4c227-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="4c227-234">De gebruiker gedefinieerde foutberichten cijfers mogen niet in Hallo 100.000 150.000 bereik voor WEGGOOIEN</span><span class="sxs-lookup"><span data-stu-id="4c227-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="4c227-235">Foutberichten voor RAISERROR worden opgelost op 50.000</span><span class="sxs-lookup"><span data-stu-id="4c227-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="4c227-236">Gebruik van sys.messages wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4c227-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="4c227-237">Limitiations</span><span class="sxs-lookup"><span data-stu-id="4c227-237">Limitiations</span></span>
<span data-ttu-id="4c227-238">SQL Data Warehouse heeft enkele andere beperkingen die betrekking tootransactions hebben.</span><span class="sxs-lookup"><span data-stu-id="4c227-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="4c227-239">Ze zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="4c227-239">They are as follows:</span></span>

* <span data-ttu-id="4c227-240">Er is geen gedistribueerde transacties</span><span class="sxs-lookup"><span data-stu-id="4c227-240">No distributed transactions</span></span>
* <span data-ttu-id="4c227-241">Er is geen geneste transacties toegestaan</span><span class="sxs-lookup"><span data-stu-id="4c227-241">No nested transactions permitted</span></span>
* <span data-ttu-id="4c227-242">Er is geen opslaan punten toegestaan</span><span class="sxs-lookup"><span data-stu-id="4c227-242">No save points allowed</span></span>
* <span data-ttu-id="4c227-243">Er zijn geen benoemde transacties</span><span class="sxs-lookup"><span data-stu-id="4c227-243">No named transactions</span></span>
* <span data-ttu-id="4c227-244">Er is geen gemarkeerde transacties</span><span class="sxs-lookup"><span data-stu-id="4c227-244">No marked transactions</span></span>
* <span data-ttu-id="4c227-245">Er is geen ondersteuning voor DDL zoals `CREATE TABLE` gedefinieerd binnen een transactie</span><span class="sxs-lookup"><span data-stu-id="4c227-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c227-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c227-246">Next steps</span></span>
<span data-ttu-id="4c227-247">toolearn meer informatie over het optimaliseren van transacties, Zie [transacties aanbevolen procedures][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="4c227-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="4c227-248">Zie toolearn over andere best practices SQL Data Warehouse [aanbevolen procedures voor SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="4c227-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
