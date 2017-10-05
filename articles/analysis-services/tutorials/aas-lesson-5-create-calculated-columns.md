---
title: 'Azure Analysis Services-zelfstudie - Les 5: Berekende kolommen maken | Microsoft Docs'
description: In deze les wordt beschreven hoe u berekende kolommen maakt in de zelfstudie over Azure Analysis Services.
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="4b326-103">Les 5: Berekende kolommen maken</span><span class="sxs-lookup"><span data-stu-id="4b326-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4b326-104">In deze les maakt u gegevens in het model door berekende kolommen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="4b326-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="4b326-105">U kunt berekende kolommen maken (als aangepaste kolommen) wanneer u Get Data uitvoert, met behulp van Query-editor of in de ontwerpfunctie voor modellen. De laatste methode gaan we verderop toepassen.</span><span class="sxs-lookup"><span data-stu-id="4b326-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="4b326-106">Zie [Berekende kolommen](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4b326-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="4b326-107">U gaat vijf nieuwe berekende kolommen maken in drie verschillende tabellen.</span><span class="sxs-lookup"><span data-stu-id="4b326-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="4b326-108">De stappen verschillen enigszins per taak, om aan te tonen dat er meerdere manieren zijn om kolommen te maken, ze een andere naam te geven en ze op diverse locaties in een tabel weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4b326-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="4b326-109">Dit is trouwens ook de les waarin we voor het eerst DAX (Data Analysis Expressions) gaan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4b326-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="4b326-110">DAX is een speciale taal voor het maken van in hoge mate aanpasbare formule-expressies voor tabellaire modellen.</span><span class="sxs-lookup"><span data-stu-id="4b326-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="4b326-111">In deze zelfstudie gebruikt u DAX voor het maken van berekende kolommen, metingen en rolfilters.</span><span class="sxs-lookup"><span data-stu-id="4b326-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="4b326-112">Zie [DAX in tabellaire modellen](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4b326-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="4b326-113">Geschatte tijd voor het voltooien van deze les: **15 minuten**</span><span class="sxs-lookup"><span data-stu-id="4b326-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4b326-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4b326-114">Prerequisites</span></span>  
<span data-ttu-id="4b326-115">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b326-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="4b326-116">Voordat u de taken in deze les gaat uitvoeren, moet u de vorige les hebben voltooid: [Les 4: Relaties maken](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="4b326-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="4b326-117">Berekende kolommen maken</span><span class="sxs-lookup"><span data-stu-id="4b326-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="4b326-118">Een berekende kolom MonthCalendar maken in de tabel DimDate:</span><span class="sxs-lookup"><span data-stu-id="4b326-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="4b326-119">Klik op het menu **Model** > **Model View** > **Data View**.</span><span class="sxs-lookup"><span data-stu-id="4b326-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="4b326-120">Berekende kolommen kunnen alleen worden gemaakt met behulp van de ontwerpfunctie voor modellen in de gegevensweergave.</span><span class="sxs-lookup"><span data-stu-id="4b326-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="4b326-121">Klik in de ontwerpfunctie voor modellen op de tabel (het tabblad) **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="4b326-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="4b326-122">Klik met de rechtermuisknop op de kolomkop **CalendarQuarter** en klik vervolgens op **Insert Column**.</span><span class="sxs-lookup"><span data-stu-id="4b326-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="4b326-123">Er wordt links van de kolom **Calendar Quarter** een nieuwe kolom ingevoegd met de naam **Calculated Column 1**.</span><span class="sxs-lookup"><span data-stu-id="4b326-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="4b326-124">Typ op de formulebalk boven de tabel de volgende DAX-formule. De functie Automatisch aanvullen zorgt ervoor dat u makkelijk de volledig gekwalificeerde namen van kolommen en tabellen kunt invullen en toont bovendien de functies die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="4b326-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="4b326-125">Vervolgens worden er voor alle rijen in de berekende kolom waarden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="4b326-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="4b326-126">Als u omlaag door de tabel schuift, ziet u dat rijen verschillende waarden kunnen hebben voor deze kolom, op basis van de gegevens in elke rij.</span><span class="sxs-lookup"><span data-stu-id="4b326-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="4b326-127">Wijzig de naam van deze kolom in **MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="4b326-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="4b326-129">De berekende kolom MonthCalendar bevat een sorteerbare naam voor de maanden.</span><span class="sxs-lookup"><span data-stu-id="4b326-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="4b326-130">Een berekende kolom DayOfWeek maken in de tabel DimDate:</span><span class="sxs-lookup"><span data-stu-id="4b326-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="4b326-131">Zorg dat de tabel **DimDate** nog actief is en klik vervolgens op het menu **Column** en **Add Column**.</span><span class="sxs-lookup"><span data-stu-id="4b326-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="4b326-132">Typ op de formulebalk de volgende formule:</span><span class="sxs-lookup"><span data-stu-id="4b326-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="4b326-133">Druk op Enter als de formule klaar is.</span><span class="sxs-lookup"><span data-stu-id="4b326-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="4b326-134">De nieuwe kolom wordt aan de rechterkant van de tabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4b326-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="4b326-135">Wijzig de naam van de kolom in **DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="4b326-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="4b326-136">Klik op de kolomkop en sleep de kolom tussen de kolom **EnglishDayNameOfWeek** en de kolom **DayNumberOfMonth**.</span><span class="sxs-lookup"><span data-stu-id="4b326-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="4b326-137">U kunt makkelijker navigeren door kolommen in de tabel te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="4b326-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="4b326-138">De berekende kolom DayOfWeek bevat een sorteerbare naam voor de dagen van de week.</span><span class="sxs-lookup"><span data-stu-id="4b326-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="4b326-139">Een berekende kolom ProductSubcategoryName maken in de tabel DimProduct:</span><span class="sxs-lookup"><span data-stu-id="4b326-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="4b326-140">Schuif in de tabel **DimProduct** helemaal naar de rechterkant van de tabel.</span><span class="sxs-lookup"><span data-stu-id="4b326-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="4b326-141">U ziet dat de meest rechtse kolom de naam **Add Column** (cursief) heeft. Klik op de kolomkop van deze kolom.</span><span class="sxs-lookup"><span data-stu-id="4b326-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="4b326-142">Typ op de formulebalk de volgende formule:</span><span class="sxs-lookup"><span data-stu-id="4b326-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="4b326-143">Wijzig de naam van de kolom in **ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="4b326-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="4b326-144">De berekende kolom ProductSubcategoryName wordt gebruikt voor het maken van een hiërarchie in de tabel DimProduct, die gegevens bevat uit de kolom EnglishProductSubcategoryName in de tabel DimProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="4b326-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="4b326-145">Hiërarchieën kunnen niet meer dan één tabel omvatten.</span><span class="sxs-lookup"><span data-stu-id="4b326-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="4b326-146">U gaat later hiërarchieën maken in les 9.</span><span class="sxs-lookup"><span data-stu-id="4b326-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="4b326-147">Een berekende kolom ProductCategoryName maken in de tabel DimProduct:</span><span class="sxs-lookup"><span data-stu-id="4b326-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="4b326-148">Zorg dat de tabel **DimProduct** nog actief is en klik vervolgens op het menu **Column** en **Add Column**.</span><span class="sxs-lookup"><span data-stu-id="4b326-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="4b326-149">Typ op de formulebalk de volgende formule:</span><span class="sxs-lookup"><span data-stu-id="4b326-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="4b326-150">Wijzig de naam van de kolom in **ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="4b326-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="4b326-151">De berekende kolom ProductCategoryName wordt gebruikt voor het maken van een hiërarchie in de tabel DimProduct, die gegevens bevat uit de kolom EnglishProductCategoryName in de tabel DimProductCategory.</span><span class="sxs-lookup"><span data-stu-id="4b326-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="4b326-152">Hiërarchieën kunnen niet meer dan één tabel omvatten.</span><span class="sxs-lookup"><span data-stu-id="4b326-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="4b326-153">Een berekende kolom Margin maken in de tabel FactInternetSales:</span><span class="sxs-lookup"><span data-stu-id="4b326-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="4b326-154">Selecteer in de ontwerpfunctie voor modellen de tabel **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="4b326-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="4b326-155">Maak een nieuwe berekende kolom tussen de kolommen **SalesAmount** en **TaxAmt**.</span><span class="sxs-lookup"><span data-stu-id="4b326-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="4b326-156">Typ op de formulebalk de volgende formule:</span><span class="sxs-lookup"><span data-stu-id="4b326-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="4b326-157">Wijzig de naam van de kolom in **Margin**.</span><span class="sxs-lookup"><span data-stu-id="4b326-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="4b326-159">De berekende kolom Margin wordt gebruikt voor het analyseren van winstmarge voor elke verkoop.</span><span class="sxs-lookup"><span data-stu-id="4b326-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="4b326-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b326-160">What's next?</span></span>
<span data-ttu-id="4b326-161">[Les 6: Metingen maken](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="4b326-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
