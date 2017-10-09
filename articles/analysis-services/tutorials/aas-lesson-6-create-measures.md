---
<span data-ttu-id="7be5c-101">titel: aaa "Azure Analysis Services-zelfstudie les 6: eenheden maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate maatregelen in de zelfstudie hello Azure Analysis Services-project.</span><span class="sxs-lookup"><span data-stu-id="7be5c-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="7be5c-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="7be5c-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="7be5c-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="7be5c-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="7be5c-104">Les 6: Metingen maken</span><span class="sxs-lookup"><span data-stu-id="7be5c-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7be5c-105">In deze les maakt u maatregelen toobe opgenomen in het model.</span><span class="sxs-lookup"><span data-stu-id="7be5c-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="7be5c-106">Vergelijkbare toohello berekende kolommen die u hebt gemaakt, is een meting een berekening gemaakt met behulp van een DAX-formule.</span><span class="sxs-lookup"><span data-stu-id="7be5c-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="7be5c-107">In tegenstelling tot berekende kolommen worden metingen echter geëvalueerd op basis van een *filter* dat de gebruiker selecteert,</span><span class="sxs-lookup"><span data-stu-id="7be5c-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="7be5c-108">Bijvoorbeeld, een bepaalde kolom of een slicer toohello rijlabels veld toegevoegd in een draaitabel.</span><span class="sxs-lookup"><span data-stu-id="7be5c-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="7be5c-109">Een waarde op voor elke cel in Hallo filter wordt berekend door de maateenheid Hallo toegepast.</span><span class="sxs-lookup"><span data-stu-id="7be5c-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="7be5c-110">Metingen zijn krachtige, flexibele berekeningen die u wilt dat tooinclude in bijna alle modellen in tabelvorm tooperform dynamische berekeningen voor numerieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="7be5c-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="7be5c-111">toolearn meer, Zie [metingen](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="7be5c-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="7be5c-112">toocreate metingen, gebruikt u Hallo *meting raster*.</span><span class="sxs-lookup"><span data-stu-id="7be5c-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="7be5c-113">Elke tabel heeft standaard een leeg metingenraster, maar meestal hoeft u niet voor elke tabel metingen te maken.</span><span class="sxs-lookup"><span data-stu-id="7be5c-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="7be5c-114">Hallo meting raster onder een tabel in de ontwerpfunctie voor het model in de gegevensweergave hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7be5c-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="7be5c-115">wordt weergegeven of toohide Hallo meting raster voor een tabel, klikt u op Hallo **tabel** menu en klik vervolgens op **meting raster weergeven**.</span><span class="sxs-lookup"><span data-stu-id="7be5c-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="7be5c-116">Door een lege cel in Hallo meting raster klikken en vervolgens een DAX-formule typen in de formulebalk Hallo kunt u een meting.</span><span class="sxs-lookup"><span data-stu-id="7be5c-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="7be5c-117">Wanneer u klikt u op ENTER toocomplete Hallo formule, Hallo meting en vervolgens wordt weergegeven in de cel Hallo.</span><span class="sxs-lookup"><span data-stu-id="7be5c-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="7be5c-118">U kunt ook metingen met behulp van een standaard aggregatiefunctie door te klikken op een kolom maken en vervolgens te klikken op de knop AutoSom Hallo (**∑**) op de werkbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="7be5c-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="7be5c-119">Maatregelen die zijn gemaakt met Hallo AutoSom functie weergegeven in Hallo meting rastercel direct onder de kolom hello, maar kunnen worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="7be5c-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="7be5c-120">In deze les maakt u maatregelen door zowel een DAX-formule invoeren in de formulebalk Hallo en via Hallo AutoSom functie.</span><span class="sxs-lookup"><span data-stu-id="7be5c-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="7be5c-121">Geschatte tijd toocomplete deze les: **30 minuten**</span><span class="sxs-lookup"><span data-stu-id="7be5c-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7be5c-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7be5c-122">Prerequisites</span></span>  
<span data-ttu-id="7be5c-123">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7be5c-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="7be5c-124">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 5: maken van berekende kolommen](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7be5c-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="7be5c-125">Metingen maken</span><span class="sxs-lookup"><span data-stu-id="7be5c-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="7be5c-126">toocreate een meting DaysCurrentQuarterToDate in Hallo DimDate tabel</span><span class="sxs-lookup"><span data-stu-id="7be5c-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="7be5c-127">Klik op Hallo in Hallo model designer **DimDate** tabel.</span><span class="sxs-lookup"><span data-stu-id="7be5c-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="7be5c-128">Klik in Hallo meting raster op Hallo linksboven lege cel.</span><span class="sxs-lookup"><span data-stu-id="7be5c-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="7be5c-129">Typ in de formulebalk hello, Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="7be5c-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="7be5c-130">Kennisgeving Hallo linksboven cel bevat nu een metingnaam **DaysCurrentQuarterToDate**, gevolgd door het Hallo-resultaat **92**.</span><span class="sxs-lookup"><span data-stu-id="7be5c-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="7be5c-132">In tegenstelling tot berekende kolommen met meting formules kunt u de metingnaam hello, gevolgd door een dubbelepunt, gevolgd door de formule Hallo-expressie typen.</span><span class="sxs-lookup"><span data-stu-id="7be5c-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="7be5c-133">toocreate een meting DaysInCurrentQuarter in Hallo DimDate tabel</span><span class="sxs-lookup"><span data-stu-id="7be5c-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="7be5c-134">Hello **DimDate** tabel nog actief in Hallo model designer in Hallo meting raster, klikt u op de lege cel Hallo hieronder Hallo meting die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7be5c-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="7be5c-135">Typ in de formulebalk hello, Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="7be5c-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="7be5c-136">Bij het maken van een ratio van de vergelijking tussen één onvolledige periode en Hallo vorige periode.</span><span class="sxs-lookup"><span data-stu-id="7be5c-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="7be5c-137">Hallo formule moet Hallo-gedeelte van het Hallo-outperiode is verstreken berekenen en vergelijken het toohello dezelfde in Hallo vorige periode verhoudingen.</span><span class="sxs-lookup"><span data-stu-id="7be5c-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="7be5c-138">In dit geval, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] geeft Hallo verhouding huidige periode is verstreken in Hallo.</span><span class="sxs-lookup"><span data-stu-id="7be5c-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="7be5c-139">toocreate een meting InternetDistinctCountSalesOrder in Hallo heeft tabel</span><span class="sxs-lookup"><span data-stu-id="7be5c-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="7be5c-140">Klik op Hallo **heeft** tabel.</span><span class="sxs-lookup"><span data-stu-id="7be5c-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="7be5c-141">Klik op Hallo **SalesOrderNumber** kolomkop.</span><span class="sxs-lookup"><span data-stu-id="7be5c-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="7be5c-142">Klik op Hallo werkbalk op Hallo pijl-omlaag volgende toohello AutoSom (**∑**) en selecteer vervolgens **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="7be5c-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="7be5c-143">Hallo AutoSom functie maakt automatisch een eenheid voor de geselecteerde kolom Hallo Hallo DistinctCount standaard aggregatie formule.</span><span class="sxs-lookup"><span data-stu-id="7be5c-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="7be5c-145">Klik in Hallo meting raster op nieuwe meting Hallo, en klik vervolgens in Hallo **eigenschappen** venster in **Metingnaam**, Hallo meting te wijzigen**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="7be5c-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="7be5c-146">aanvullende maatregelen toocreate in Hallo heeft tabel</span><span class="sxs-lookup"><span data-stu-id="7be5c-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="7be5c-147">Hallo AutoSom functie gebruikt, maken en noem Hallo maatregelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7be5c-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="7be5c-148">Kolom</span><span class="sxs-lookup"><span data-stu-id="7be5c-148">Column</span></span>|<span data-ttu-id="7be5c-149">Naam van meting</span><span class="sxs-lookup"><span data-stu-id="7be5c-149">Measure name</span></span>|<span data-ttu-id="7be5c-150">AutoSom (∑)</span><span class="sxs-lookup"><span data-stu-id="7be5c-150">AutoSum (∑)</span></span>|<span data-ttu-id="7be5c-151">Formule</span><span class="sxs-lookup"><span data-stu-id="7be5c-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="7be5c-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="7be5c-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="7be5c-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="7be5c-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="7be5c-154">Count</span><span class="sxs-lookup"><span data-stu-id="7be5c-154">Count</span></span>|<span data-ttu-id="7be5c-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="7be5c-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="7be5c-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="7be5c-156">OrderQuantity</span></span>|<span data-ttu-id="7be5c-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="7be5c-157">InternetTotalUnits</span></span>|<span data-ttu-id="7be5c-158">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-158">Sum</span></span>|<span data-ttu-id="7be5c-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="7be5c-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="7be5c-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="7be5c-160">DiscountAmount</span></span>|<span data-ttu-id="7be5c-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="7be5c-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="7be5c-162">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-162">Sum</span></span>|<span data-ttu-id="7be5c-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="7be5c-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="7be5c-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="7be5c-164">TotalProductCost</span></span>|<span data-ttu-id="7be5c-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="7be5c-165">InternetTotalProductCost</span></span>|<span data-ttu-id="7be5c-166">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-166">Sum</span></span>|<span data-ttu-id="7be5c-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="7be5c-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="7be5c-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="7be5c-168">SalesAmount</span></span>|<span data-ttu-id="7be5c-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="7be5c-169">InternetTotalSales</span></span>|<span data-ttu-id="7be5c-170">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-170">Sum</span></span>|<span data-ttu-id="7be5c-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="7be5c-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="7be5c-172">Margin</span><span class="sxs-lookup"><span data-stu-id="7be5c-172">Margin</span></span>|<span data-ttu-id="7be5c-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="7be5c-173">InternetTotalMargin</span></span>|<span data-ttu-id="7be5c-174">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-174">Sum</span></span>|<span data-ttu-id="7be5c-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="7be5c-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="7be5c-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="7be5c-176">TaxAmt</span></span>|<span data-ttu-id="7be5c-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="7be5c-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="7be5c-178">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-178">Sum</span></span>|<span data-ttu-id="7be5c-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="7be5c-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="7be5c-180">Freight</span><span class="sxs-lookup"><span data-stu-id="7be5c-180">Freight</span></span>|<span data-ttu-id="7be5c-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="7be5c-181">InternetTotalFreight</span></span>|<span data-ttu-id="7be5c-182">Sum</span><span class="sxs-lookup"><span data-stu-id="7be5c-182">Sum</span></span>|<span data-ttu-id="7be5c-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="7be5c-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="7be5c-184">Door te klikken op een lege cel in Hallo meting raster en met behulp van de formulebalk hello, maken en na Hallo meet in volgorde:</span><span class="sxs-lookup"><span data-stu-id="7be5c-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="7be5c-185">Maatregelen die zijn gemaakt voor Hallo heeft tabel mag gebruikte tooanalyze kritische financiële gegevens zoals verkopen, kosten en winstmarge voor items die zijn gedefinieerd door Hallo gebruiker geselecteerde filter.</span><span class="sxs-lookup"><span data-stu-id="7be5c-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="7be5c-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7be5c-186">What's next?</span></span>
<span data-ttu-id="7be5c-187">[Les 7: Key Performance Indicators maken](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="7be5c-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
