---
title: aaaHow toowrite query's in de Stream Analytics | Microsoft Docs
description: Query's in de Stream Analytics en querygegevens schrijven | leren padsegment.
keywords: hoe toowrite query's gegevens opvragen, een query schrijven van query's schrijven
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="bfa94-104">Hoe toowrite in Stream Analytics query 's</span><span class="sxs-lookup"><span data-stu-id="bfa94-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="bfa94-105">Schrijven van query's voor stroomverwerkingslogica schrijft in Azure Stream Analytics wordt geïmplementeerd als een 'permanente query' die is gedefinieerd voordat een taak wordt gestart en wordt uitgevoerd op gegevens, zoals het Hallo-taak is bereikt.</span><span class="sxs-lookup"><span data-stu-id="bfa94-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="bfa94-106">Hallo gegevenstransformatie wordt uitgedrukt in een SQL-achtige query-taal, die is grotendeels een subset van T-SQL met enkele taal extensies als toegevoegd [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) tooexpress tijdelijke semantiek gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfa94-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="bfa94-107">Schrijven van query's:</span><span class="sxs-lookup"><span data-stu-id="bfa94-107">Writing Queries:</span></span>
1. <span data-ttu-id="bfa94-108">Klik in de Stream Analytics-taak in hello Azure-beheerportal op **Query**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Query selecteren](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="bfa94-110">In Azure Portal hello, klikt u op **Query**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Selecteer de Query-Preview](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="bfa94-112">Nieuwe taken hebben een query sjabloon toohelp u op weg.</span><span class="sxs-lookup"><span data-stu-id="bfa94-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="bfa94-113">Hallo query sjabloon 'doorgangsschijf' voert query dat projecten alle velden uit de invoervelden in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bfa94-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="bfa94-114">Als u ten minste één invoer en uitvoer voor uw taak hebt gedefinieerd, kunt u Hallo tijdelijke aanduiding '[YourOutputAlias]' en '[YourInputAlias]' velden vervangen door Hallo aliassen Hallo invoer en uitvoer dat u wenst dat gebruik eerst.</span><span class="sxs-lookup"><span data-stu-id="bfa94-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="bfa94-115">U kunt bovendien nog steeds ontwerpen en testen van uw query in de klassieke Azure-Portal Hallo zonder te definiëren in- en uitgangen op Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="bfa94-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="bfa94-116">Als u tooperform meer dan een eenvoudige pass-through-verwerking wenst, kunt u de querydefinitie Hallo kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="bfa94-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="bfa94-117">tooget gestart met het ontwerpen van query verdiepen in enkele algemene query patronen worden vastgelegd [hier](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="bfa94-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Querygegevens venster](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="bfa94-119">querygegevens toovalidate werkt:</span><span class="sxs-lookup"><span data-stu-id="bfa94-119">toovalidate query data is working:</span></span>
<span data-ttu-id="bfa94-120">U kunt testen dat uw query werkt zoals verwacht in de browser Hallo worden uitgevoerd via een of meer lokale JSON-bestanden met testgegevens.</span><span class="sxs-lookup"><span data-stu-id="bfa94-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="bfa94-121">Dit wordt niet Hallo taak starten of hebben invloed op de facturering.</span><span class="sxs-lookup"><span data-stu-id="bfa94-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="bfa94-122">Testen van query's in de browser is momenteel niet ondersteund in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="bfa94-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="bfa94-123">Zorg ervoor dat er geen fouten zijn opgetreden in Hallo-query (anders de knop testen hello wordt uitgeschakeld) en klik vervolgens op de knop testen Hallo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Querygegevens Test](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="bfa94-125">U zult na vragen aan gebruiker toospecify bestanden voor elk waarnaar wordt verwezen in de query Hallo Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="bfa94-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="bfa94-126">In dit voorbeeld Hallo sjabloon query wordt gehandhaafd-is, dus Hallo dialoogvenster gevraagd om voor invoer met de naam 'yourinputalias'.</span><span class="sxs-lookup"><span data-stu-id="bfa94-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![De query gegevens testen](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="bfa94-128">Blader tooa testbestand.</span><span class="sxs-lookup"><span data-stu-id="bfa94-128">Browse tooa test file.</span></span> <span data-ttu-id="bfa94-129">Verschillende voorbeeldbestanden zijn beschikbaar op [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) en u kunt ook voorbeeldgegevens ophalen uit de invoer van uw eigen gegevens stream via Hallo voorbeeldgegevens-functie op Hallo invoer tabblad.</span><span class="sxs-lookup"><span data-stu-id="bfa94-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Invoer voor de query](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="bfa94-131">Na het Hallo-dialoogvenster te sluiten, uw query wilt uitvoeren via de testgegevens Hallo en Hallo resultaten onderaan Hallo Hallo querypagina worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bfa94-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Samenvatting van de query](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="bfa94-133">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="bfa94-133">Get help</span></span>
<span data-ttu-id="bfa94-134">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="bfa94-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfa94-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfa94-135">Next steps</span></span>
* [<span data-ttu-id="bfa94-136">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bfa94-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bfa94-137">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bfa94-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bfa94-138">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="bfa94-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bfa94-139">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="bfa94-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bfa94-140">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="bfa94-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

