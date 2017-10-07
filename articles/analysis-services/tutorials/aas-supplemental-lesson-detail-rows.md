---
<span data-ttu-id="592e6-101">titel: aaa "zelfstudie aanvullende les Azure Analysis Services: detailrijen | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate een Detail rijen expressie in Azure analyseservices-zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="592e6-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="592e6-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="592e6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="592e6-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="592e6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="592e6-104">Aanvullende les: Detailrijen</span><span class="sxs-lookup"><span data-stu-id="592e6-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="592e6-105">In deze aanvullende les u Hallo DAX-Editor toodefine een aangepaste Detail rijen expressie.</span><span class="sxs-lookup"><span data-stu-id="592e6-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="592e6-106">Een expressie van de rijen Detail is een eigenschap van een meting biedt eindgebruikers meer informatie over de resultaten van een meting Hallo geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="592e6-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="592e6-107">Geschatte tijd toocomplete deze les: **10 minuten**</span><span class="sxs-lookup"><span data-stu-id="592e6-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="592e6-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="592e6-108">Prerequisites</span></span>  
<span data-ttu-id="592e6-109">Deze aanvullende les maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model.</span><span class="sxs-lookup"><span data-stu-id="592e6-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="592e6-110">Voordat u Hallo taken uitvoert in deze aanvullende les, u moet voltooid alle vorige uitkomsten of een voltooide Adventure Works Internet verkoop model voorbeeldproject hebben.</span><span class="sxs-lookup"><span data-stu-id="592e6-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="592e6-111">Wat doen we toosolve nodig?</span><span class="sxs-lookup"><span data-stu-id="592e6-111">What do we need toosolve?</span></span>
<span data-ttu-id="592e6-112">We bekijken Hallo details van de meting van onze InternetTotalSales, voordat u een expressie van de rijen Detail toevoegt.</span><span class="sxs-lookup"><span data-stu-id="592e6-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="592e6-113">In SSDT, klikt u op Hallo **Model** menu > **analyseren in Excel** tooopen Excel en maak een lege draaitabel.</span><span class="sxs-lookup"><span data-stu-id="592e6-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="592e6-114">In **PivotTable-Fields**, Hallo toevoegen **InternetTotalSales** te meten uit Hallo heeft tabel**waarden**, **kalenderjaar**van Hallo DimDate tabel te**kolommen**, en **EnglishCountryRegionName** te**rijen**.</span><span class="sxs-lookup"><span data-stu-id="592e6-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="592e6-115">Onze draaitabel biedt nu ons cumulatieve resultaten van Hallo InternetTotalSales meting door regio's en het jaar.</span><span class="sxs-lookup"><span data-stu-id="592e6-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="592e6-117">In de draaitabel Hallo, dubbelklikt u op een cumulatieve waarde voor een jaar en de regionaam van een.</span><span class="sxs-lookup"><span data-stu-id="592e6-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="592e6-118">Hier we op gedubbelklikt Hallo-waarde voor Australië en Hallo jaar 2014.</span><span class="sxs-lookup"><span data-stu-id="592e6-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="592e6-119">Er wordt een nieuw blad geopend met gegevens, maar dit zijn niet echt nuttige gegevens.</span><span class="sxs-lookup"><span data-stu-id="592e6-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="592e6-121">Resultaat van de meting van onze InternetTotalSales we zou toosee hier is een tabel met kolommen en rijen met gegevens die toohello bijdragen worden geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="592e6-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="592e6-122">toodo dat we een expressie van de rijen Detail als een eigenschap van Hallo meting kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="592e6-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="592e6-123">Een detailrijenexpressie maken</span><span class="sxs-lookup"><span data-stu-id="592e6-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="592e6-124">een expressie van de rijen Detail toocreate</span><span class="sxs-lookup"><span data-stu-id="592e6-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="592e6-125">Klik in SSDT, in Hallo heeft tabel maat raster op Hallo **InternetTotalSales** meting.</span><span class="sxs-lookup"><span data-stu-id="592e6-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="592e6-126">In **eigenschappen** > **Detail rijen expressie**, klikt u op Hallo editor knop tooopen Hallo DAX-Editor.</span><span class="sxs-lookup"><span data-stu-id="592e6-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="592e6-128">DAX-Editor, Voer Hallo expressie te volgen:</span><span class="sxs-lookup"><span data-stu-id="592e6-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="592e6-129">Deze expressie geeft de namen van kolommen en meting resultaten uit Hallo heeft tabel en gerelateerde tabellen die worden geretourneerd wanneer een gebruiker dubbelklikt op een samengevoegde resultaat in een draaitabel of -rapport.</span><span class="sxs-lookup"><span data-stu-id="592e6-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="592e6-130">Terug in Excel Hallo blad gemaakt in stap 3 verwijderen en dubbelklik op een cumulatieve waarde.</span><span class="sxs-lookup"><span data-stu-id="592e6-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="592e6-131">Deze tijd met een eigenschap Detail rijen expressie is gedefinieerd voor de meting hello, een nieuw blad wordt geopend met veel meer bruikbare gegevens.</span><span class="sxs-lookup"><span data-stu-id="592e6-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="592e6-133">Implementeer het model opnieuw.</span><span class="sxs-lookup"><span data-stu-id="592e6-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="592e6-134">Zie ook</span><span class="sxs-lookup"><span data-stu-id="592e6-134">See Also</span></span>  
<span data-ttu-id="592e6-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  (SELECTCOLUMNS, functie (DAX))</span><span class="sxs-lookup"><span data-stu-id="592e6-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="592e6-136">Aanvullende les: Dynamische beveiliging</span><span class="sxs-lookup"><span data-stu-id="592e6-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="592e6-137">Aanvullende les: Onregelmatige hiërarchieën</span><span class="sxs-lookup"><span data-stu-id="592e6-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
