---
title: Transacties in SQL datawarehouse | Microsoft Docs
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
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="efb77-103">Transacties in SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="efb77-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="efb77-104">Zoals u verwachten zou, SQL Data Warehouse biedt ondersteuning voor transacties als onderdeel van de datawarehouse-workload.</span><span class="sxs-lookup"><span data-stu-id="efb77-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="efb77-105">Om te controleren of dat de prestaties van SQL Data Warehouse wordt onderhouden op grote schaal zijn sommige functies echter beperkt in vergelijking tot SQL Server.</span><span class="sxs-lookup"><span data-stu-id="efb77-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="efb77-106">In dit artikel worden de verschillen gemarkeerd en geeft een lijst van de andere.</span><span class="sxs-lookup"><span data-stu-id="efb77-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="efb77-107">Transactie-isolatieniveaus</span><span class="sxs-lookup"><span data-stu-id="efb77-107">Transaction isolation levels</span></span>
<span data-ttu-id="efb77-108">SQL Data Warehouse implementeert ACID-transactions.</span><span class="sxs-lookup"><span data-stu-id="efb77-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="efb77-109">De isolatie van de transactionele ondersteuning is echter beperkt tot `READ UNCOMMITTED` en dit kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="efb77-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="efb77-110">U kunt een aantal methoden om te voorkomen dat niet-weggeschreven gelezen gegevens van de gegevens als dit een probleem voor u is coderen implementeren.</span><span class="sxs-lookup"><span data-stu-id="efb77-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="efb77-111">De meest populaire methoden gebruikmaken van CTAS en tabel partitie overschakelen (vaak het sliding venster-patroon genoemd) om te voorkomen dat gebruikers een query die nog steeds wordt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="efb77-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="efb77-112">Weergaven die vooraf filter de gegevens is ook een populaire benadering.</span><span class="sxs-lookup"><span data-stu-id="efb77-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="efb77-113">De grootte van de transactie</span><span class="sxs-lookup"><span data-stu-id="efb77-113">Transaction size</span></span>
<span data-ttu-id="efb77-114">Er is een wijziging één transactie in grootte beperkt.</span><span class="sxs-lookup"><span data-stu-id="efb77-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="efb77-115">De limiet is vandaag de dag "per distributiepunt' toegepast.</span><span class="sxs-lookup"><span data-stu-id="efb77-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="efb77-116">Daarom kan de totale toewijzing worden berekend door de limiet vermenigvuldigen met het aantal distributiepunten.</span><span class="sxs-lookup"><span data-stu-id="efb77-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="efb77-117">Naar geschatte het maximale aantal rijen in de transactie deelt het kapje distributie door de totale grootte van elke rij.</span><span class="sxs-lookup"><span data-stu-id="efb77-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="efb77-118">Houd rekening met een gemiddelde kolomlengte duurt dan de maximumgrootte voor kolommen met variabele lengte.</span><span class="sxs-lookup"><span data-stu-id="efb77-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="efb77-119">In de tabel hieronder de volgende veronderstellingen zijn aangebracht:</span><span class="sxs-lookup"><span data-stu-id="efb77-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="efb77-120">Een gelijkmatige verdeling van gegevens is opgetreden</span><span class="sxs-lookup"><span data-stu-id="efb77-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="efb77-121">De gemiddelde rijlengte is 250 bytes</span><span class="sxs-lookup"><span data-stu-id="efb77-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="efb77-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="efb77-122">[DWU][DWU]</span></span> | <span data-ttu-id="efb77-123">Cap per distributiepunt (GiB)</span><span class="sxs-lookup"><span data-stu-id="efb77-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="efb77-124">Aantal distributies</span><span class="sxs-lookup"><span data-stu-id="efb77-124">Number of Distributions</span></span> | <span data-ttu-id="efb77-125">Transactie maximumgrootte (GiB)</span><span class="sxs-lookup"><span data-stu-id="efb77-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="efb77-126"># Rijen per distributiepunt</span><span class="sxs-lookup"><span data-stu-id="efb77-126"># Rows per distribution</span></span> | <span data-ttu-id="efb77-127">Maximumaantal rijen per transactie</span><span class="sxs-lookup"><span data-stu-id="efb77-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="efb77-128">DW100</span><span class="sxs-lookup"><span data-stu-id="efb77-128">DW100</span></span> |<span data-ttu-id="efb77-129">1</span><span class="sxs-lookup"><span data-stu-id="efb77-129">1</span></span> |<span data-ttu-id="efb77-130">60</span><span class="sxs-lookup"><span data-stu-id="efb77-130">60</span></span> |<span data-ttu-id="efb77-131">60</span><span class="sxs-lookup"><span data-stu-id="efb77-131">60</span></span> |<span data-ttu-id="efb77-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-132">4,000,000</span></span> |<span data-ttu-id="efb77-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-133">240,000,000</span></span> |
| <span data-ttu-id="efb77-134">DW200</span><span class="sxs-lookup"><span data-stu-id="efb77-134">DW200</span></span> |<span data-ttu-id="efb77-135">1.5</span><span class="sxs-lookup"><span data-stu-id="efb77-135">1.5</span></span> |<span data-ttu-id="efb77-136">60</span><span class="sxs-lookup"><span data-stu-id="efb77-136">60</span></span> |<span data-ttu-id="efb77-137">90</span><span class="sxs-lookup"><span data-stu-id="efb77-137">90</span></span> |<span data-ttu-id="efb77-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-138">6,000,000</span></span> |<span data-ttu-id="efb77-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-139">360,000,000</span></span> |
| <span data-ttu-id="efb77-140">DW300</span><span class="sxs-lookup"><span data-stu-id="efb77-140">DW300</span></span> |<span data-ttu-id="efb77-141">2.25</span><span class="sxs-lookup"><span data-stu-id="efb77-141">2.25</span></span> |<span data-ttu-id="efb77-142">60</span><span class="sxs-lookup"><span data-stu-id="efb77-142">60</span></span> |<span data-ttu-id="efb77-143">135</span><span class="sxs-lookup"><span data-stu-id="efb77-143">135</span></span> |<span data-ttu-id="efb77-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-144">9,000,000</span></span> |<span data-ttu-id="efb77-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-145">540,000,000</span></span> |
| <span data-ttu-id="efb77-146">DW400</span><span class="sxs-lookup"><span data-stu-id="efb77-146">DW400</span></span> |<span data-ttu-id="efb77-147">3</span><span class="sxs-lookup"><span data-stu-id="efb77-147">3</span></span> |<span data-ttu-id="efb77-148">60</span><span class="sxs-lookup"><span data-stu-id="efb77-148">60</span></span> |<span data-ttu-id="efb77-149">180</span><span class="sxs-lookup"><span data-stu-id="efb77-149">180</span></span> |<span data-ttu-id="efb77-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-150">12,000,000</span></span> |<span data-ttu-id="efb77-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-151">720,000,000</span></span> |
| <span data-ttu-id="efb77-152">DW500</span><span class="sxs-lookup"><span data-stu-id="efb77-152">DW500</span></span> |<span data-ttu-id="efb77-153">3.75</span><span class="sxs-lookup"><span data-stu-id="efb77-153">3.75</span></span> |<span data-ttu-id="efb77-154">60</span><span class="sxs-lookup"><span data-stu-id="efb77-154">60</span></span> |<span data-ttu-id="efb77-155">225</span><span class="sxs-lookup"><span data-stu-id="efb77-155">225</span></span> |<span data-ttu-id="efb77-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-156">15,000,000</span></span> |<span data-ttu-id="efb77-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-157">900,000,000</span></span> |
| <span data-ttu-id="efb77-158">DW600</span><span class="sxs-lookup"><span data-stu-id="efb77-158">DW600</span></span> |<span data-ttu-id="efb77-159">4.5</span><span class="sxs-lookup"><span data-stu-id="efb77-159">4.5</span></span> |<span data-ttu-id="efb77-160">60</span><span class="sxs-lookup"><span data-stu-id="efb77-160">60</span></span> |<span data-ttu-id="efb77-161">270</span><span class="sxs-lookup"><span data-stu-id="efb77-161">270</span></span> |<span data-ttu-id="efb77-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-162">18,000,000</span></span> |<span data-ttu-id="efb77-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-163">1,080,000,000</span></span> |
| <span data-ttu-id="efb77-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="efb77-164">DW1000</span></span> |<span data-ttu-id="efb77-165">7.5</span><span class="sxs-lookup"><span data-stu-id="efb77-165">7.5</span></span> |<span data-ttu-id="efb77-166">60</span><span class="sxs-lookup"><span data-stu-id="efb77-166">60</span></span> |<span data-ttu-id="efb77-167">450</span><span class="sxs-lookup"><span data-stu-id="efb77-167">450</span></span> |<span data-ttu-id="efb77-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-168">30,000,000</span></span> |<span data-ttu-id="efb77-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-169">1,800,000,000</span></span> |
| <span data-ttu-id="efb77-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="efb77-170">DW1200</span></span> |<span data-ttu-id="efb77-171">9</span><span class="sxs-lookup"><span data-stu-id="efb77-171">9</span></span> |<span data-ttu-id="efb77-172">60</span><span class="sxs-lookup"><span data-stu-id="efb77-172">60</span></span> |<span data-ttu-id="efb77-173">540</span><span class="sxs-lookup"><span data-stu-id="efb77-173">540</span></span> |<span data-ttu-id="efb77-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-174">36,000,000</span></span> |<span data-ttu-id="efb77-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-175">2,160,000,000</span></span> |
| <span data-ttu-id="efb77-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="efb77-176">DW1500</span></span> |<span data-ttu-id="efb77-177">11.25</span><span class="sxs-lookup"><span data-stu-id="efb77-177">11.25</span></span> |<span data-ttu-id="efb77-178">60</span><span class="sxs-lookup"><span data-stu-id="efb77-178">60</span></span> |<span data-ttu-id="efb77-179">675</span><span class="sxs-lookup"><span data-stu-id="efb77-179">675</span></span> |<span data-ttu-id="efb77-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-180">45,000,000</span></span> |<span data-ttu-id="efb77-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-181">2,700,000,000</span></span> |
| <span data-ttu-id="efb77-182">DW2000 ZIJN</span><span class="sxs-lookup"><span data-stu-id="efb77-182">DW2000</span></span> |<span data-ttu-id="efb77-183">15</span><span class="sxs-lookup"><span data-stu-id="efb77-183">15</span></span> |<span data-ttu-id="efb77-184">60</span><span class="sxs-lookup"><span data-stu-id="efb77-184">60</span></span> |<span data-ttu-id="efb77-185">900</span><span class="sxs-lookup"><span data-stu-id="efb77-185">900</span></span> |<span data-ttu-id="efb77-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-186">60,000,000</span></span> |<span data-ttu-id="efb77-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-187">3,600,000,000</span></span> |
| <span data-ttu-id="efb77-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="efb77-188">DW3000</span></span> |<span data-ttu-id="efb77-189">22.5</span><span class="sxs-lookup"><span data-stu-id="efb77-189">22.5</span></span> |<span data-ttu-id="efb77-190">60</span><span class="sxs-lookup"><span data-stu-id="efb77-190">60</span></span> |<span data-ttu-id="efb77-191">1,350</span><span class="sxs-lookup"><span data-stu-id="efb77-191">1,350</span></span> |<span data-ttu-id="efb77-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-192">90,000,000</span></span> |<span data-ttu-id="efb77-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-193">5,400,000,000</span></span> |
| <span data-ttu-id="efb77-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="efb77-194">DW6000</span></span> |<span data-ttu-id="efb77-195">45</span><span class="sxs-lookup"><span data-stu-id="efb77-195">45</span></span> |<span data-ttu-id="efb77-196">60</span><span class="sxs-lookup"><span data-stu-id="efb77-196">60</span></span> |<span data-ttu-id="efb77-197">2,700</span><span class="sxs-lookup"><span data-stu-id="efb77-197">2,700</span></span> |<span data-ttu-id="efb77-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-198">180,000,000</span></span> |<span data-ttu-id="efb77-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="efb77-199">10,800,000,000</span></span> |

<span data-ttu-id="efb77-200">De transactie maximale grootte wordt per transactie of bewerking toegepast.</span><span class="sxs-lookup"><span data-stu-id="efb77-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="efb77-201">Het is niet toegepast op alle gelijktijdige transacties.</span><span class="sxs-lookup"><span data-stu-id="efb77-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="efb77-202">Elke transactie mag daarom deze hoeveelheid gegevens naar het logboek schrijven.</span><span class="sxs-lookup"><span data-stu-id="efb77-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="efb77-203">Om te optimaliseren en de hoeveelheid gegevens geschreven naar het logboek te minimaliseren raadpleegt u de [transacties aanbevolen procedures] [ Transactions best practices] artikel.</span><span class="sxs-lookup"><span data-stu-id="efb77-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="efb77-204">De grootte van de maximale transactie kan alleen worden bereikt voor HASH of ROUND_ROBIN gedistribueerd tabellen waarbij de spreiding van de gegevens is zelfs.</span><span class="sxs-lookup"><span data-stu-id="efb77-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="efb77-205">Als de transactie is schrijven van gegevens op een wijze vertekende naar de distributies zijn de limiet is waarschijnlijk worden bereikt voordat de transactie maximale grootte.</span><span class="sxs-lookup"><span data-stu-id="efb77-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="efb77-206">Transactiestatus</span><span class="sxs-lookup"><span data-stu-id="efb77-206">Transaction state</span></span>
<span data-ttu-id="efb77-207">SQL Data Warehouse maakt gebruik van de functie XACT_STATE() voor het rapporteren van een mislukte transactie met de waarde -2.</span><span class="sxs-lookup"><span data-stu-id="efb77-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="efb77-208">Dit betekent dat de transactie is mislukt en is gemarkeerd voor alleen terugdraaien</span><span class="sxs-lookup"><span data-stu-id="efb77-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="efb77-209">Het gebruik van -2 door de functie XACT_STATE om aan te geven van een mislukte transactie vertegenwoordigt verschillend gedrag met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="efb77-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="efb77-210">SQL Server gebruikt de waarde -1 vertegenwoordigt een niet-doorvoerbare transactie.</span><span class="sxs-lookup"><span data-stu-id="efb77-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="efb77-211">SQL Server kan een aantal fouten binnen een transactie zonder zijn gemarkeerd als niet-doorvoerbare tolereren.</span><span class="sxs-lookup"><span data-stu-id="efb77-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="efb77-212">Bijvoorbeeld `SELECT 1/0` wordt een fout veroorzaken, maar niet afdwingen van een transactie in een niet-doorvoerbare staat.</span><span class="sxs-lookup"><span data-stu-id="efb77-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="efb77-213">SQL Server wordt ook gelezen kan in de niet-doorvoerbare transactie.</span><span class="sxs-lookup"><span data-stu-id="efb77-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="efb77-214">Echter kunt SQL Data Warehouse u niet doen.</span><span class="sxs-lookup"><span data-stu-id="efb77-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="efb77-215">Als er een fout optreedt in een SQL Data Warehouse-transactie wordt automatisch overgeschakeld naar de status-2 en u zich niet Breng een select-instructies verder totdat de instructie is teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="efb77-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="efb77-216">Daarom is het belangrijk om te controleren dat de toepassingscode om te zien als XACT_STATE() wordt gebruikt als u moet mogelijk codewijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="efb77-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="efb77-217">Bijvoorbeeld, in SQL Server mogelijk ziet u een transactie die er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="efb77-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="efb77-218">Als u uw code laat ongewijzigd hierboven krijgt u het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="efb77-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="efb77-219">Bericht 111233, 16 niveau status 1, regel 1 111233; De huidige transactie is afgebroken en eventuele wijzigingen in behandeling zijn teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="efb77-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="efb77-220">Oorzaak: Een transactie in een status terugdraaien van de alleen-lezen is niet expliciet teruggedraaid voordat een DDL-, DML- of SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="efb77-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="efb77-221">U wordt ook de uitvoer van de functies ERROR_ * niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="efb77-221">You will also not get the output of the ERROR_* functions.</span></span>

<span data-ttu-id="efb77-222">In SQL Data Warehouse moet de code enigszins worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="efb77-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

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

<span data-ttu-id="efb77-223">Het verwachte gedrag is nu waargenomen.</span><span class="sxs-lookup"><span data-stu-id="efb77-223">The expected behavior is now observed.</span></span> <span data-ttu-id="efb77-224">De fout in de transactie wordt beheerd en de functies ERROR_ * Geef waarden op zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="efb77-224">The error in the transaction is managed and the ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="efb77-225">Alle die is gewijzigd, is dat de `ROLLBACK` van de transactie moest gebeuren voor het lezen van de foutgegevens in de `CATCH` blok.</span><span class="sxs-lookup"><span data-stu-id="efb77-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="efb77-226">De functie Error_Line()</span><span class="sxs-lookup"><span data-stu-id="efb77-226">Error_Line() function</span></span>
<span data-ttu-id="efb77-227">Het is ook opgemerkt dat SQL Data Warehouse niet implementeert of ondersteuning voor de functie ERROR_LINE().</span><span class="sxs-lookup"><span data-stu-id="efb77-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="efb77-228">Als u in uw code hoeft hebt te verwijderen om te voldoen aan de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="efb77-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="efb77-229">Query labels in uw code in plaats daarvan gebruiken voor het implementeren van dezelfde functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="efb77-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="efb77-230">Raadpleeg de [LABEL] [ LABEL] artikel voor meer informatie over deze functie.</span><span class="sxs-lookup"><span data-stu-id="efb77-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="efb77-231">Met behulp van THROW en RAISERROR</span><span class="sxs-lookup"><span data-stu-id="efb77-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="efb77-232">THROW is de moderne implementatie voor uitzonderingen in SQL Data Warehouse maar RAISERROR wordt ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="efb77-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="efb77-233">Er zijn een paar verschillen waarde Let echter op.</span><span class="sxs-lookup"><span data-stu-id="efb77-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="efb77-234">De gebruiker gedefinieerde foutberichten getallen kan niet binnen het bereik 100.000 150.000 voor WEGGOOIEN</span><span class="sxs-lookup"><span data-stu-id="efb77-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="efb77-235">Foutberichten voor RAISERROR worden opgelost op 50.000</span><span class="sxs-lookup"><span data-stu-id="efb77-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="efb77-236">Gebruik van sys.messages wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="efb77-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="efb77-237">Limitiations</span><span class="sxs-lookup"><span data-stu-id="efb77-237">Limitiations</span></span>
<span data-ttu-id="efb77-238">SQL Data Warehouse heeft enkele andere beperkingen met betrekking tot transacties.</span><span class="sxs-lookup"><span data-stu-id="efb77-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="efb77-239">Ze zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="efb77-239">They are as follows:</span></span>

* <span data-ttu-id="efb77-240">Er is geen gedistribueerde transacties</span><span class="sxs-lookup"><span data-stu-id="efb77-240">No distributed transactions</span></span>
* <span data-ttu-id="efb77-241">Er is geen geneste transacties toegestaan</span><span class="sxs-lookup"><span data-stu-id="efb77-241">No nested transactions permitted</span></span>
* <span data-ttu-id="efb77-242">Er is geen opslaan punten toegestaan</span><span class="sxs-lookup"><span data-stu-id="efb77-242">No save points allowed</span></span>
* <span data-ttu-id="efb77-243">Er zijn geen benoemde transacties</span><span class="sxs-lookup"><span data-stu-id="efb77-243">No named transactions</span></span>
* <span data-ttu-id="efb77-244">Er is geen gemarkeerde transacties</span><span class="sxs-lookup"><span data-stu-id="efb77-244">No marked transactions</span></span>
* <span data-ttu-id="efb77-245">Er is geen ondersteuning voor DDL zoals `CREATE TABLE` gedefinieerd binnen een transactie</span><span class="sxs-lookup"><span data-stu-id="efb77-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="efb77-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="efb77-246">Next steps</span></span>
<span data-ttu-id="efb77-247">Zie voor meer informatie over het optimaliseren van transacties, [transacties aanbevolen procedures][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="efb77-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="efb77-248">Zie voor meer informatie over andere aanbevelingen voor SQL Data Warehouse, [aanbevolen procedures voor SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="efb77-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
