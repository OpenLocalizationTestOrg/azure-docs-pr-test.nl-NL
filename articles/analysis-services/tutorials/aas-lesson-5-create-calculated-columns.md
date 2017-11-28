---
<span data-ttu-id="88cbe-101">titel: aaa "Azure Analysis Services-zelfstudie les 5: maken van berekende kolommen | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate berekende kolommen in de zelfstudie hello Azure Analysis Services-project.</span><span class="sxs-lookup"><span data-stu-id="88cbe-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="88cbe-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="88cbe-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="88cbe-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="88cbe-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="88cbe-104">Les 5: Berekende kolommen maken</span><span class="sxs-lookup"><span data-stu-id="88cbe-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="88cbe-105">In deze les maakt u gegevens in het model door berekende kolommen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="88cbe-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="88cbe-106">U kunt berekende kolommen (als aangepaste kolommen) maken wanneer u gegevens ophalen, met behulp van Hallo Query-Editor of later in de ontwerpfunctie model-achtige Hallo u hier doen.</span><span class="sxs-lookup"><span data-stu-id="88cbe-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="88cbe-107">toolearn meer, Zie [berekende kolommen](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="88cbe-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="88cbe-108">U gaat vijf nieuwe berekende kolommen maken in drie verschillende tabellen.</span><span class="sxs-lookup"><span data-stu-id="88cbe-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="88cbe-109">Hallo stappen zijn enigszins verschillen voor elke taak waarin er zijn verschillende manieren toocreate kolommen, wijzigen en plaats deze in verschillende locaties in een tabel.</span><span class="sxs-lookup"><span data-stu-id="88cbe-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="88cbe-110">Dit is trouwens ook de les waarin we voor het eerst DAX (Data Analysis Expressions) gaan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88cbe-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="88cbe-111">DAX is een speciale taal voor het maken van in hoge mate aanpasbare formule-expressies voor tabellaire modellen.</span><span class="sxs-lookup"><span data-stu-id="88cbe-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="88cbe-112">In deze zelfstudie gebruikt u DAX toocreate berekende kolommen, metingen en filters die rol.</span><span class="sxs-lookup"><span data-stu-id="88cbe-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="88cbe-113">toolearn meer, Zie [DAX in modellen in tabelvorm](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="88cbe-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="88cbe-114">Geschatte tijd toocomplete deze les: **15 minuten**</span><span class="sxs-lookup"><span data-stu-id="88cbe-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="88cbe-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88cbe-115">Prerequisites</span></span>  
<span data-ttu-id="88cbe-116">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="88cbe-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="88cbe-117">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 4: relaties](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="88cbe-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="88cbe-118">Berekende kolommen maken</span><span class="sxs-lookup"><span data-stu-id="88cbe-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="88cbe-119">Een berekende kolom van de MonthCalendar in Hallo DimDate tabel maken</span><span class="sxs-lookup"><span data-stu-id="88cbe-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="88cbe-120">Klik op Hallo **Model** menu > **modelweergave** > **gegevensweergave**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="88cbe-121">Berekende kolommen kunnen alleen worden gemaakt met behulp van Hallo model designer in de gegevensweergave.</span><span class="sxs-lookup"><span data-stu-id="88cbe-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="88cbe-122">Klik op Hallo in Hallo model designer **DimDate** tabel (tabblad).</span><span class="sxs-lookup"><span data-stu-id="88cbe-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="88cbe-123">Klik met de rechtermuisknop Hallo **CalendarQuarter** kolomkop en klik vervolgens op **kolom invoegen**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="88cbe-124">Een nieuwe kolom die met de naam **berekende kolom 1** ingevoegde toohello links Hallo **kalenderkwartaal** kolom.</span><span class="sxs-lookup"><span data-stu-id="88cbe-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="88cbe-125">Typ in de formulebalk Hallo boven Hallo tabel Hallo volgende DAX-formule: automatisch aanvullen helpt u typt Hallo FQDN-namen van kolommen en tabellen en lijsten Hallo functies die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="88cbe-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="88cbe-126">Waarden worden vervolgens voor alle Hallo rijen in de berekende kolom Hallo ingevuld.</span><span class="sxs-lookup"><span data-stu-id="88cbe-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="88cbe-127">Als u omlaag Hallo tabel schuift, ziet u rijen kunnen verschillende waarden voor deze kolom op basis van gegevens in elke rij Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="88cbe-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="88cbe-128">Wijzig de naam van deze kolom te**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="88cbe-130">Hallo MonthCalendar berekende kolom bevat een sorteerbare naam voor de maand.</span><span class="sxs-lookup"><span data-stu-id="88cbe-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="88cbe-131">Maken van een berekende kolom DayOfWeek in Hallo DimDate tabel</span><span class="sxs-lookup"><span data-stu-id="88cbe-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="88cbe-132">Hello **DimDate** tabel steeds actief is, klikt u op Hallo **kolom** menu en klik vervolgens op **kolom toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="88cbe-133">Typ in de formulebalk hello, Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="88cbe-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="88cbe-134">Wanneer u klaar bent met het bouwen van Hallo formule, druk op ENTER.</span><span class="sxs-lookup"><span data-stu-id="88cbe-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="88cbe-135">de nieuwe kolom Hallo is toohello helemaal rechts op Hallo tabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="88cbe-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="88cbe-136">Wijzig de naam van de kolom hello te**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="88cbe-137">Klik op de kolomkop Hallo en sleep Hallo kolom tussen Hallo **EnglishDayNameOfWeek** kolom en Hallo **DayNumberOfMonth** kolom.</span><span class="sxs-lookup"><span data-stu-id="88cbe-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="88cbe-138">Kolommen verplaatsen in de tabel, maakt het eenvoudiger toonavigate.</span><span class="sxs-lookup"><span data-stu-id="88cbe-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="88cbe-139">Hallo DayOfWeek berekende kolom bevat een sorteerbare naam voor de dag van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="88cbe-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="88cbe-140">Maken van een berekende kolom ProductSubcategoryName in Hallo DimProduct tabel</span><span class="sxs-lookup"><span data-stu-id="88cbe-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="88cbe-141">In Hallo **DimProduct** tabel, toohello uiterst rechts in de tabel Hallo schuiven.</span><span class="sxs-lookup"><span data-stu-id="88cbe-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="88cbe-142">Kennisgeving Hallo meest rechtse kolom heet **kolom toevoegen** (cursief) op Hallo kolomkop te klikken.</span><span class="sxs-lookup"><span data-stu-id="88cbe-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="88cbe-143">Typ in de formulebalk hello, Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="88cbe-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="88cbe-144">Wijzig de naam van de kolom hello te**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="88cbe-145">Hallo ProductSubcategoryName berekende kolom is gebruikte toocreate een hiërarchie in de tabel DimProduct hello, waaronder gegevens van de kolom met Hallo EnglishProductSubcategoryName in Hallo DimProductSubcategory tabel.</span><span class="sxs-lookup"><span data-stu-id="88cbe-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="88cbe-146">Hiërarchieën kunnen niet meer dan één tabel omvatten.</span><span class="sxs-lookup"><span data-stu-id="88cbe-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="88cbe-147">U gaat later hiërarchieën maken in les 9.</span><span class="sxs-lookup"><span data-stu-id="88cbe-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="88cbe-148">Maken van een berekende kolom ProductCategoryName in Hallo DimProduct tabel</span><span class="sxs-lookup"><span data-stu-id="88cbe-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="88cbe-149">Hello **DimProduct** tabel steeds actief is, klikt u op Hallo **kolom** menu en klik vervolgens op **kolom toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="88cbe-150">Typ in de formulebalk hello, Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="88cbe-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="88cbe-151">Wijzig de naam van de kolom hello te**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="88cbe-152">Hallo ProductCategoryName berekende kolom is gebruikte toocreate een hiërarchie in de tabel DimProduct hello, waaronder gegevens van de kolom met Hallo EnglishProductCategoryName in Hallo DimProductCategory tabel.</span><span class="sxs-lookup"><span data-stu-id="88cbe-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="88cbe-153">Hiërarchieën kunnen niet meer dan één tabel omvatten.</span><span class="sxs-lookup"><span data-stu-id="88cbe-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="88cbe-154">Maken van een berekende kolom marge in Hallo heeft tabel</span><span class="sxs-lookup"><span data-stu-id="88cbe-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="88cbe-155">Selecteer Hallo in Hallo model designer **heeft** tabel.</span><span class="sxs-lookup"><span data-stu-id="88cbe-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="88cbe-156">Maak een nieuwe berekende kolom tussen Hallo **SalesAmount** kolom en Hallo **TaxAmt** kolom.</span><span class="sxs-lookup"><span data-stu-id="88cbe-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="88cbe-157">Typ in de formulebalk hello, Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="88cbe-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="88cbe-158">Wijzig de naam van de kolom hello te**marge**.</span><span class="sxs-lookup"><span data-stu-id="88cbe-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="88cbe-160">Hallo marge berekende kolom is gebruikte tooanalyze winstmarge voor elke verkoop.</span><span class="sxs-lookup"><span data-stu-id="88cbe-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="88cbe-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88cbe-161">What's next?</span></span>
<span data-ttu-id="88cbe-162">[Les 6: Metingen maken](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="88cbe-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
