---
title: "Azure Analysis Services-zelfstudie - Aanvullende les: Onregelmatige hiërarchieën | Microsoft Docs"
description: "In deze les wordt beschreven hoe u onregelmatige hiërarchieën herstelt in de zelfstudie over Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 0f02ff73eb126cc397312e87bde50b3ee2d6ce53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="3e321-103">Aanvullende les: Onregelmatige hiërarchieën</span><span class="sxs-lookup"><span data-stu-id="3e321-103">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3e321-104">In deze aanvullende les gaat u een probleem oplossen dat vaak optreedt bij het maken van een draaitabel van hiërarchieën die op verschillende niveaus lege waarden (leden) bevatten.</span><span class="sxs-lookup"><span data-stu-id="3e321-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="3e321-105">Dit is bijvoorbeeld het geval als een hoge manager in een organisatie zowel afdelingsmanagers als niet-managers als direct ondergeschikten heeft.</span><span class="sxs-lookup"><span data-stu-id="3e321-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="3e321-106">Of bij een geografische hiërarchie die bestaat uit land-provincie-stad, waarbij voor sommige steden geen bovenliggende provincie is ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="3e321-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="3e321-107">Wanneer een hiërarchie lege leden heeft, worden deze vaak overgebracht naar andere, afwijkende niveaus waardoor er een onregelmatige hiërarchie ontstaat.</span><span class="sxs-lookup"><span data-stu-id="3e321-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="3e321-109">Tabellaire modellen op het compatibiliteitsniveau 1400 hebben een extra eigenschap **Hide Members** voor hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="3e321-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="3e321-110">Bij de instelling **Default** voor deze eigenschap wordt ervan uitgegaan dat er op geen enkel niveau lege leden bestaan.</span><span class="sxs-lookup"><span data-stu-id="3e321-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="3e321-111">Bij de instelling **Hide blank members** worden lege leden uitgesloten van de hiërarchie wanneer deze wordt toegevoegd aan een draaitabel of -rapport.</span><span class="sxs-lookup"><span data-stu-id="3e321-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="3e321-112">Geschatte tijd voor het voltooien van deze les: **20 minuten**</span><span class="sxs-lookup"><span data-stu-id="3e321-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3e321-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3e321-113">Prerequisites</span></span>  
<span data-ttu-id="3e321-114">Deze aanvullende les maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model.</span><span class="sxs-lookup"><span data-stu-id="3e321-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="3e321-115">U kunt de taken in deze aanvullende les pas uitvoeren nadat u alle voorgaande lessen hebt afgerond of het voorbeeldproject Adventure Works Internet Sales hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="3e321-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="3e321-116">Als u tijdens de zelfstudie het project AW Internet Sales hebt gemaakt, bevat het model nog geen gegevens of hiërarchieën die onregelmatig zijn.</span><span class="sxs-lookup"><span data-stu-id="3e321-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="3e321-117">Om deze aanvullende les te voltooien, moet u eerst het probleem introduceren door een paar extra tabellen toe te voegen, en relaties, berekende kolommen, een meting en een nieuwe hiërarchie Organization te maken.</span><span class="sxs-lookup"><span data-stu-id="3e321-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="3e321-118">Dat gedeelte neemt ongeveer 15 minuten in beslag.</span><span class="sxs-lookup"><span data-stu-id="3e321-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="3e321-119">Vervolgens hebt u nog maar een paar minuten nodig om het probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="3e321-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="3e321-120">Tabellen en objecten toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e321-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="3e321-121">Nieuwe tabellen toevoegen aan uw model</span><span class="sxs-lookup"><span data-stu-id="3e321-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="3e321-122">Vouw in Tabular Model Explorer de optie **Data Sources** uit, klik met de rechtermuisknop op uw verbinding en klik vervolgens op **Import New Tables**.</span><span class="sxs-lookup"><span data-stu-id="3e321-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="3e321-123">Selecteer in Navigator **DimEmployee** en **FactResellerSales**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e321-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="3e321-124">Klik in Query-editor op **Import**.</span><span class="sxs-lookup"><span data-stu-id="3e321-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="3e321-125">Maak de volgende [relaties](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="3e321-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="3e321-126">Tabel 1</span><span class="sxs-lookup"><span data-stu-id="3e321-126">Table 1</span></span>           | <span data-ttu-id="3e321-127">Kolom</span><span class="sxs-lookup"><span data-stu-id="3e321-127">Column</span></span>       | <span data-ttu-id="3e321-128">Filterrichting</span><span class="sxs-lookup"><span data-stu-id="3e321-128">Filter Direction</span></span>   | <span data-ttu-id="3e321-129">Tabel 2</span><span class="sxs-lookup"><span data-stu-id="3e321-129">Table 2</span></span>     | <span data-ttu-id="3e321-130">Kolom</span><span class="sxs-lookup"><span data-stu-id="3e321-130">Column</span></span>      | <span data-ttu-id="3e321-131">Actief</span><span class="sxs-lookup"><span data-stu-id="3e321-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="3e321-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="3e321-132">FactResellerSales</span></span> | <span data-ttu-id="3e321-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="3e321-133">OrderDateKey</span></span> | <span data-ttu-id="3e321-134">Standaard</span><span class="sxs-lookup"><span data-stu-id="3e321-134">Default</span></span>            | <span data-ttu-id="3e321-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="3e321-135">DimDate</span></span>     | <span data-ttu-id="3e321-136">Date</span><span class="sxs-lookup"><span data-stu-id="3e321-136">Date</span></span>        | <span data-ttu-id="3e321-137">Ja</span><span class="sxs-lookup"><span data-stu-id="3e321-137">Yes</span></span>    |
    | <span data-ttu-id="3e321-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="3e321-138">FactResellerSales</span></span> | <span data-ttu-id="3e321-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="3e321-139">DueDate</span></span>      | <span data-ttu-id="3e321-140">Standaard</span><span class="sxs-lookup"><span data-stu-id="3e321-140">Default</span></span>            | <span data-ttu-id="3e321-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="3e321-141">DimDate</span></span>     | <span data-ttu-id="3e321-142">Date</span><span class="sxs-lookup"><span data-stu-id="3e321-142">Date</span></span>        | <span data-ttu-id="3e321-143">Nee</span><span class="sxs-lookup"><span data-stu-id="3e321-143">No</span></span>     |
    | <span data-ttu-id="3e321-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="3e321-144">FactResellerSales</span></span> | <span data-ttu-id="3e321-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="3e321-145">ShipDateKey</span></span>  | <span data-ttu-id="3e321-146">Standaard</span><span class="sxs-lookup"><span data-stu-id="3e321-146">Default</span></span>            | <span data-ttu-id="3e321-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="3e321-147">DimDate</span></span>     | <span data-ttu-id="3e321-148">Date</span><span class="sxs-lookup"><span data-stu-id="3e321-148">Date</span></span>        | <span data-ttu-id="3e321-149">Nee</span><span class="sxs-lookup"><span data-stu-id="3e321-149">No</span></span>     |
    | <span data-ttu-id="3e321-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="3e321-150">FactResellerSales</span></span> | <span data-ttu-id="3e321-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="3e321-151">ProductKey</span></span>   | <span data-ttu-id="3e321-152">Standaard</span><span class="sxs-lookup"><span data-stu-id="3e321-152">Default</span></span>            | <span data-ttu-id="3e321-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="3e321-153">DimProduct</span></span>  | <span data-ttu-id="3e321-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="3e321-154">ProductKey</span></span>  | <span data-ttu-id="3e321-155">Ja</span><span class="sxs-lookup"><span data-stu-id="3e321-155">Yes</span></span>    |
    | <span data-ttu-id="3e321-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="3e321-156">FactResellerSales</span></span> | <span data-ttu-id="3e321-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="3e321-157">EmployeeKey</span></span>  | <span data-ttu-id="3e321-158">Naar beide tabellen</span><span class="sxs-lookup"><span data-stu-id="3e321-158">To Both Tables</span></span> | <span data-ttu-id="3e321-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="3e321-159">DimEmployee</span></span> | <span data-ttu-id="3e321-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="3e321-160">EmployeeKey</span></span> | <span data-ttu-id="3e321-161">Ja</span><span class="sxs-lookup"><span data-stu-id="3e321-161">Yes</span></span>    |

5. <span data-ttu-id="3e321-162">Maak in de tabel **DimEmployee** de volgende [berekende kolommen](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="3e321-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="3e321-163">**Pad**</span><span class="sxs-lookup"><span data-stu-id="3e321-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="3e321-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="3e321-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="3e321-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="3e321-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="3e321-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="3e321-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="3e321-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="3e321-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="3e321-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="3e321-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="3e321-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="3e321-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="3e321-170">Maak in de tabel **DimEmployee** een [hiërarchie](../tutorials/aas-lesson-9-create-hierarchies.md) met de naam **Organization**.</span><span class="sxs-lookup"><span data-stu-id="3e321-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="3e321-171">Voeg de volgende kolommen in deze volgorde toe: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="3e321-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="3e321-172">Maak in de tabel **FactResellerSales** de volgende [meting](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="3e321-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="3e321-173">Gebruik [Analyse in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) om Excel te openen en automatisch een draaitabel te maken.</span><span class="sxs-lookup"><span data-stu-id="3e321-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="3e321-174">Ga naar **Draaitabelvelden**, voeg de hiërarchie **Organization** uit de tabel **DimEmployee** toe aan **Rijen**, en de meting **ResellerTotalSales** uit de tabel **FactResellerSales** aan **Waarden**.</span><span class="sxs-lookup"><span data-stu-id="3e321-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="3e321-176">Zoals u ziet in de draaitabel, bevat de hiërarchie onregelmatige rijen.</span><span class="sxs-lookup"><span data-stu-id="3e321-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="3e321-177">Er zijn veel rijen waarin lege leden worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3e321-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="3e321-178">Het probleem met de onregelmatige hiërarchie oplossen door de eigenschap Hide Members in te stellen</span><span class="sxs-lookup"><span data-stu-id="3e321-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="3e321-179">Ga naar **Tabular Model Explorer** en vouw **Tables** > **DimEmployee** > **Hierarchies** > **Organization** uit.</span><span class="sxs-lookup"><span data-stu-id="3e321-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="3e321-180">Selecteer **Hide blank members** bij **Properties** > **Hide Members**.</span><span class="sxs-lookup"><span data-stu-id="3e321-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="3e321-182">Ga terug naar Excel en vernieuw de draaitabel.</span><span class="sxs-lookup"><span data-stu-id="3e321-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="3e321-184">Dat ziet er al veel beter uit.</span><span class="sxs-lookup"><span data-stu-id="3e321-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="3e321-185">Zie ook</span><span class="sxs-lookup"><span data-stu-id="3e321-185">See Also</span></span>   
[<span data-ttu-id="3e321-186">Les 9: Hiërarchieën maken</span><span class="sxs-lookup"><span data-stu-id="3e321-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="3e321-187">Aanvullende les: Dynamische beveiliging</span><span class="sxs-lookup"><span data-stu-id="3e321-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="3e321-188">Aanvullende les: Detailrijen</span><span class="sxs-lookup"><span data-stu-id="3e321-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  