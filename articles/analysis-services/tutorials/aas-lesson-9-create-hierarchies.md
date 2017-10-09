---
<span data-ttu-id="2d56c-101">titel: aaa "Azure Analysis Services-zelfstudie les 9: Maak hiërarchieën | Microsoft Docs' Beschrijving: services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="2d56c-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="2d56c-102">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="2d56c-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="2d56c-103">Les 9: Hiërarchieën maken</span><span class="sxs-lookup"><span data-stu-id="2d56c-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="2d56c-104">In deze les gaat u hiërarchieën maken.</span><span class="sxs-lookup"><span data-stu-id="2d56c-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="2d56c-105">Hiërarchieën zijn groepen van kolommen die op niveaus zijn gerangschikt. Zo kan een hiërarchie Geografie onderliggende niveaus bevatten voor land, provincie en stad.</span><span class="sxs-lookup"><span data-stu-id="2d56c-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="2d56c-106">Hiërarchieën kunnen worden weergegeven gescheiden van andere kolommen in een reporting client veld lijst met toepassingen, zodat u ze gemakkelijker voor client gebruikers toonavigate en opnemen in een rapport.</span><span class="sxs-lookup"><span data-stu-id="2d56c-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="2d56c-107">toolearn meer, Zie [hiërarchieën](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="2d56c-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="2d56c-108">toocreate hiërarchieën, gebruik Hallo model designer in *diagramweergave*.</span><span class="sxs-lookup"><span data-stu-id="2d56c-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="2d56c-109">De gegevensweergave is niet geschikt voor het maken en beheren van hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="2d56c-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="2d56c-110">Geschatte tijd toocomplete deze les: **20 minuten**</span><span class="sxs-lookup"><span data-stu-id="2d56c-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2d56c-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2d56c-111">Prerequisites</span></span>  
<span data-ttu-id="2d56c-112">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2d56c-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="2d56c-113">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 8: Maak perspectieven](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="2d56c-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="2d56c-114">Hiërarchieën maken</span><span class="sxs-lookup"><span data-stu-id="2d56c-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="2d56c-115">een hiërarchie in Hallo DimProduct tabel toocreate</span><span class="sxs-lookup"><span data-stu-id="2d56c-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="2d56c-116">Hallo model designer (diagramweergave) met de rechtermuisknop op Hallo **DimProduct** tabel > **hiërarchie maken**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="2d56c-117">Een nieuwe hiërarchie wordt weergegeven onder Hallo van venster Hallo-tabel.</span><span class="sxs-lookup"><span data-stu-id="2d56c-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="2d56c-118">Wijzig de naam van de hiërarchie Hallo **categorie**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="2d56c-119">Klik en sleep Hallo **ProductCategoryName** kolom toohello nieuwe **categorie** hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="2d56c-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="2d56c-120">In Hallo **categorie** -hiërarchie, klik met de rechtermuisknop Hallo **ProductCategoryName** > **naam**, en typ vervolgens **categorie**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="2d56c-121">Deze kolom in tabel Hallo niet de naam van een kolom in een hiërarchie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2d56c-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="2d56c-122">Een kolom in een hiërarchie is slechts een weergave van de kolom in tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d56c-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="2d56c-123">Klik en sleep Hallo **ProductSubcategoryName** kolom toohello **categorie** hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="2d56c-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="2d56c-124">Wijzig de naam in **Subcategory**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="2d56c-125">Klik met de rechtermuisknop Hallo **ModelName** kolom > **toevoegen toohierarchy**, en selecteer vervolgens **categorie**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="2d56c-126">Wijzig de naam in **Model**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="2d56c-127">Voeg **EnglishProductName** toohello hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="2d56c-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="2d56c-128">Wijzig de naam in **Product**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="2d56c-130">toocreate hiërarchieën in Hallo DimDate tabel</span><span class="sxs-lookup"><span data-stu-id="2d56c-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="2d56c-131">In Hallo **DimDate** tabel, maakt u een hiërarchie genaamd **kalender**.</span><span class="sxs-lookup"><span data-stu-id="2d56c-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="2d56c-132">Hallo kolommen in volgorde toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2d56c-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="2d56c-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="2d56c-133">CalendarYear</span></span>
    *  <span data-ttu-id="2d56c-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="2d56c-134">CalendarSemester</span></span>
    *  <span data-ttu-id="2d56c-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="2d56c-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="2d56c-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="2d56c-136">MonthCalendar</span></span>
    *  <span data-ttu-id="2d56c-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="2d56c-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="2d56c-138">In Hallo **DimDate** tabel, maakt u een **fiscale** hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="2d56c-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="2d56c-139">Hallo kolommen in order volgende omvatten:</span><span class="sxs-lookup"><span data-stu-id="2d56c-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="2d56c-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="2d56c-140">FiscalYear</span></span>
    *  <span data-ttu-id="2d56c-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="2d56c-141">FiscalSemester</span></span>
    *  <span data-ttu-id="2d56c-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="2d56c-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="2d56c-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="2d56c-143">MonthCalendar</span></span>
    *  <span data-ttu-id="2d56c-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="2d56c-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="2d56c-145">Ten slotte in Hallo **DimDate** tabel, maakt u een **ProductionCalendar** hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="2d56c-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="2d56c-146">Hallo kolommen in order volgende omvatten:</span><span class="sxs-lookup"><span data-stu-id="2d56c-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="2d56c-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="2d56c-147">CalendarYear</span></span>
    *  <span data-ttu-id="2d56c-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="2d56c-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="2d56c-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="2d56c-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="2d56c-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d56c-150">What's next?</span></span>
<span data-ttu-id="2d56c-151">[Les 10: Partities maken](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="2d56c-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
