---
<span data-ttu-id="f1d3e-101">titel: aaa "Azure Analysis Services-zelfstudie les 7: Key Performance Indicators maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate Key Performance Indicators in Hallo zelfstudie Azure Analysis Services-project.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="f1d3e-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="f1d3e-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="f1d3e-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="f1d3e-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="f1d3e-104">Les 7: Key Performance Indicators maken</span><span class="sxs-lookup"><span data-stu-id="f1d3e-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f1d3e-105">In deze les gaat u Key Performance Indicators (KPI's) maken.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="f1d3e-106">KPI's zijn gebruikte toogauge prestaties van een waarde die is gedefinieerd door een *Base* meting, op basis van een *doel* waarde ook gedefinieerd door een meting of door een absolute waarde.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="f1d3e-107">Op rapportage clienttoepassingen, bieden KPI's zakelijke professionals een snelle en gemakkelijke manier toounderstand een samenvatting van zakelijke slagen of tooidentify trends.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="f1d3e-108">toolearn meer, Zie [KPI's](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="f1d3e-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="f1d3e-109">Geschatte tijd toocomplete deze les: **15 minuten**</span><span class="sxs-lookup"><span data-stu-id="f1d3e-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f1d3e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f1d3e-110">Prerequisites</span></span>  
<span data-ttu-id="f1d3e-111">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="f1d3e-112">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 6: maken van metingen](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="f1d3e-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="f1d3e-113">Key Performance Indicators maken</span><span class="sxs-lookup"><span data-stu-id="f1d3e-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="f1d3e-114">een KPI InternetCurrentQuarterSalesPerformance toocreate</span><span class="sxs-lookup"><span data-stu-id="f1d3e-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="f1d3e-115">Klik op Hallo in Hallo model designer **heeft** tabel.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="f1d3e-116">Klik op een lege cel in Hallo meting raster.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="f1d3e-117">Typ in de formulebalk Hallo boven Hallo-tabel Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="f1d3e-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="f1d3e-118">Deze meting fungeert als Hallo basismeting voor Hallo KPI.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="f1d3e-119">Klik met de rechtermuisknop op **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="f1d3e-120">Hallo Key Performance Indicator (KPI) in het dialoogvenster in **doel** Selecteer **Absolute waarde**, en typ vervolgens **1.1**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="f1d3e-121">Typ in Hallo links (laag) schuifregelaar veld **1**, en klik vervolgens in Hallo rechts (hoog) schuifregelaar veld **1.07**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="f1d3e-122">In **Selecteer pictogramstijl**, selecteert u Hallo ruitvormige (rood), driehoek (geel), (groen) Pictogramtype cirkel.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="f1d3e-124">Kennisgeving Hallo uitbreidbare **beschrijvingen** label onder Hallo pictogram beschikbaar stijlen.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="f1d3e-125">Gebruik beschrijvingen voor Hallo verschillende KPI elementen toomake ze meer persoonsgegevens in clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="f1d3e-126">Klik op **OK** toocomplete Hallo KPI.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="f1d3e-127">Let op Hallo pictogram volgende toohello in Hallo meting raster **InternetCurrentQuarterSalesPerformance** meting.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="f1d3e-128">Dit pictogram geeft aan dat deze meting fungeert als een basislijn voor een KPI.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="f1d3e-129">een KPI InternetCurrentQuarterMarginPerformance toocreate</span><span class="sxs-lookup"><span data-stu-id="f1d3e-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="f1d3e-130">In Hallo meting raster voor Hallo **heeft** tabel, klikt u op een lege cel.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="f1d3e-131">Typ in de formulebalk Hallo boven Hallo-tabel Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="f1d3e-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="f1d3e-132">Klik met de rechtermuisknop op **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="f1d3e-133">Hallo Key Performance Indicator (KPI) in het dialoogvenster in **doel** Selecteer **Absolute waarde**, en typ vervolgens **1,25**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="f1d3e-134">Schuif totdat Hallo veld wordt weergegeven in Hallo links (laag) schuifregelaar veld **0,8**, en vervolgens dia Hallo rechts (hoog) schuifregelaar veld totdat Hallo veld bevat **1,03**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="f1d3e-135">In **Selecteer pictogramstijl**Hallo ruitvormige (rood), driehoek (geel), cirkel (groen) Pictogramtype selecteren en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1d3e-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="f1d3e-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1d3e-136">What's next?</span></span>
<span data-ttu-id="f1d3e-137">[Les 8: Perspectieven maken](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="f1d3e-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
