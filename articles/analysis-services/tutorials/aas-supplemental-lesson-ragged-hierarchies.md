---
<span data-ttu-id="8d06e-101">titel: aaa "zelfstudie aanvullende les Azure Analysis Services: onregelmatige hiërarchieën | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toofix hiërarchieën onregelmatige in hello Azure Analysis Services-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8d06e-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="8d06e-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="8d06e-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="8d06e-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="8d06e-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="8d06e-104">Aanvullende les: Onregelmatige hiërarchieën</span><span class="sxs-lookup"><span data-stu-id="8d06e-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8d06e-105">In deze aanvullende les gaat u een probleem oplossen dat vaak optreedt bij het maken van een draaitabel van hiërarchieën die op verschillende niveaus lege waarden (leden) bevatten.</span><span class="sxs-lookup"><span data-stu-id="8d06e-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="8d06e-106">Dit is bijvoorbeeld het geval als een hoge manager in een organisatie zowel afdelingsmanagers als niet-managers als direct ondergeschikten heeft.</span><span class="sxs-lookup"><span data-stu-id="8d06e-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="8d06e-107">Of bij een geografische hiërarchie die bestaat uit land-provincie-stad, waarbij voor sommige steden geen bovenliggende provincie is ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="8d06e-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="8d06e-108">Wanneer een hiërarchie lege leden heeft, het vaak toodifferent daalt of onregelmatige, niveaus.</span><span class="sxs-lookup"><span data-stu-id="8d06e-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="8d06e-110">Tabelmodellen op Hallo 1400 compatibiliteitsniveau hebben een extra **leden verbergen** eigenschap voor hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="8d06e-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="8d06e-111">Hallo **standaard** instelling wordt ervan uitgegaan er zijn geen lege leden op elk niveau.</span><span class="sxs-lookup"><span data-stu-id="8d06e-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="8d06e-112">Hallo **lege leden verbergen** instelling lege leden van Hallo hiërarchie bij het toevoegen van uitsluit tooa draaitabel of -rapport.</span><span class="sxs-lookup"><span data-stu-id="8d06e-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="8d06e-113">Geschatte tijd toocomplete deze les: **20 minuten**</span><span class="sxs-lookup"><span data-stu-id="8d06e-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8d06e-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d06e-114">Prerequisites</span></span>  
<span data-ttu-id="8d06e-115">Deze aanvullende les maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model.</span><span class="sxs-lookup"><span data-stu-id="8d06e-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="8d06e-116">Voordat u Hallo taken uitvoert in deze aanvullende les, u moet voltooid alle vorige uitkomsten of een voltooide Adventure Works Internet verkoop model voorbeeldproject hebben.</span><span class="sxs-lookup"><span data-stu-id="8d06e-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="8d06e-117">Als u Hallo AW Internet verkoop-project hebt gemaakt als onderdeel van de zelfstudie hello, bevat het model nog geen gegevens of niet-aaneengesloten hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="8d06e-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="8d06e-118">toocomplete deze aanvullende les u hebben toocreate Hallo probleem door een aantal aanvullende tabellen toe te voegen, maakt u relaties, berekende kolommen, een meting en een nieuwe organisatiehiërarchie.</span><span class="sxs-lookup"><span data-stu-id="8d06e-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="8d06e-119">Dat gedeelte neemt ongeveer 15 minuten in beslag.</span><span class="sxs-lookup"><span data-stu-id="8d06e-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="8d06e-120">Vervolgens krijgt u toosolve in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="8d06e-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="8d06e-121">Tabellen en objecten toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d06e-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="8d06e-122">nieuw model voor tabellen tooyour tooadd</span><span class="sxs-lookup"><span data-stu-id="8d06e-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="8d06e-123">Vouw in Tabular Model Explorer de optie **Data Sources** uit, klik met de rechtermuisknop op uw verbinding en klik vervolgens op **Import New Tables**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="8d06e-124">Selecteer in Navigator **DimEmployee** en **FactResellerSales**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="8d06e-125">Klik in Query-editor op **Import**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="8d06e-126">Maak de volgende Hallo [relaties](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="8d06e-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="8d06e-127">Tabel 1</span><span class="sxs-lookup"><span data-stu-id="8d06e-127">Table 1</span></span>           | <span data-ttu-id="8d06e-128">Kolom</span><span class="sxs-lookup"><span data-stu-id="8d06e-128">Column</span></span>       | <span data-ttu-id="8d06e-129">Filterrichting</span><span class="sxs-lookup"><span data-stu-id="8d06e-129">Filter Direction</span></span>   | <span data-ttu-id="8d06e-130">Tabel 2</span><span class="sxs-lookup"><span data-stu-id="8d06e-130">Table 2</span></span>     | <span data-ttu-id="8d06e-131">Kolom</span><span class="sxs-lookup"><span data-stu-id="8d06e-131">Column</span></span>      | <span data-ttu-id="8d06e-132">Actief</span><span class="sxs-lookup"><span data-stu-id="8d06e-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="8d06e-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8d06e-133">FactResellerSales</span></span> | <span data-ttu-id="8d06e-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="8d06e-134">OrderDateKey</span></span> | <span data-ttu-id="8d06e-135">Standaard</span><span class="sxs-lookup"><span data-stu-id="8d06e-135">Default</span></span>            | <span data-ttu-id="8d06e-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="8d06e-136">DimDate</span></span>     | <span data-ttu-id="8d06e-137">Date</span><span class="sxs-lookup"><span data-stu-id="8d06e-137">Date</span></span>        | <span data-ttu-id="8d06e-138">Ja</span><span class="sxs-lookup"><span data-stu-id="8d06e-138">Yes</span></span>    |
    | <span data-ttu-id="8d06e-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8d06e-139">FactResellerSales</span></span> | <span data-ttu-id="8d06e-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="8d06e-140">DueDate</span></span>      | <span data-ttu-id="8d06e-141">Standaard</span><span class="sxs-lookup"><span data-stu-id="8d06e-141">Default</span></span>            | <span data-ttu-id="8d06e-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="8d06e-142">DimDate</span></span>     | <span data-ttu-id="8d06e-143">Date</span><span class="sxs-lookup"><span data-stu-id="8d06e-143">Date</span></span>        | <span data-ttu-id="8d06e-144">Nee</span><span class="sxs-lookup"><span data-stu-id="8d06e-144">No</span></span>     |
    | <span data-ttu-id="8d06e-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8d06e-145">FactResellerSales</span></span> | <span data-ttu-id="8d06e-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="8d06e-146">ShipDateKey</span></span>  | <span data-ttu-id="8d06e-147">Standaard</span><span class="sxs-lookup"><span data-stu-id="8d06e-147">Default</span></span>            | <span data-ttu-id="8d06e-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="8d06e-148">DimDate</span></span>     | <span data-ttu-id="8d06e-149">Date</span><span class="sxs-lookup"><span data-stu-id="8d06e-149">Date</span></span>        | <span data-ttu-id="8d06e-150">Nee</span><span class="sxs-lookup"><span data-stu-id="8d06e-150">No</span></span>     |
    | <span data-ttu-id="8d06e-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8d06e-151">FactResellerSales</span></span> | <span data-ttu-id="8d06e-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="8d06e-152">ProductKey</span></span>   | <span data-ttu-id="8d06e-153">Standaard</span><span class="sxs-lookup"><span data-stu-id="8d06e-153">Default</span></span>            | <span data-ttu-id="8d06e-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="8d06e-154">DimProduct</span></span>  | <span data-ttu-id="8d06e-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="8d06e-155">ProductKey</span></span>  | <span data-ttu-id="8d06e-156">Ja</span><span class="sxs-lookup"><span data-stu-id="8d06e-156">Yes</span></span>    |
    | <span data-ttu-id="8d06e-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="8d06e-157">FactResellerSales</span></span> | <span data-ttu-id="8d06e-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="8d06e-158">EmployeeKey</span></span>  | <span data-ttu-id="8d06e-159">tooBoth tabellen</span><span class="sxs-lookup"><span data-stu-id="8d06e-159">tooBoth Tables</span></span> | <span data-ttu-id="8d06e-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="8d06e-160">DimEmployee</span></span> | <span data-ttu-id="8d06e-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="8d06e-161">EmployeeKey</span></span> | <span data-ttu-id="8d06e-162">Ja</span><span class="sxs-lookup"><span data-stu-id="8d06e-162">Yes</span></span>    |

5. <span data-ttu-id="8d06e-163">In Hallo **DimEmployee** tabel, maakt u de volgende Hallo [berekende kolommen](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="8d06e-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="8d06e-164">**Pad**</span><span class="sxs-lookup"><span data-stu-id="8d06e-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="8d06e-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="8d06e-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="8d06e-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="8d06e-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="8d06e-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="8d06e-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="8d06e-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="8d06e-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="8d06e-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="8d06e-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="8d06e-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="8d06e-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="8d06e-171">In Hallo **DimEmployee** tabel, maakt u een [hiërarchie](../tutorials/aas-lesson-9-create-hierarchies.md) met de naam **organisatie**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="8d06e-172">Toevoegen van kolommen in volgorde Hallo: **Level1**, **2**, **3**, **4**, **5**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="8d06e-173">In Hallo **FactResellerSales** tabel, maakt u de volgende Hallo [meting](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="8d06e-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="8d06e-174">Gebruik [analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel en automatisch een draaitabel maken.</span><span class="sxs-lookup"><span data-stu-id="8d06e-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="8d06e-175">In **PivotTable-Fields**, Hallo toevoegen **organisatie** hiërarchie van Hallo **DimEmployee** tabel te**rijen**, en Hallo **ResellerTotalSales** meting uit Hallo **FactResellerSales** tabel te**waarden**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="8d06e-177">Zoals u in Hallo draaitabel ziet, Hallo hiërarchie rijen worden weergegeven die niet-aaneengesloten zijn.</span><span class="sxs-lookup"><span data-stu-id="8d06e-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="8d06e-178">Er zijn veel rijen waarin lege leden worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8d06e-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="8d06e-179">Hallo toofix onregelmatige hiërarchie door Hallo verbergen leden eigenschap</span><span class="sxs-lookup"><span data-stu-id="8d06e-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="8d06e-180">Ga naar **Tabular Model Explorer** en vouw **Tables** > **DimEmployee** > **Hierarchies** > **Organization** uit.</span><span class="sxs-lookup"><span data-stu-id="8d06e-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="8d06e-181">Selecteer **Hide blank members** bij **Properties** > **Hide Members**.</span><span class="sxs-lookup"><span data-stu-id="8d06e-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="8d06e-183">Vernieuwen Hallo draaitabel in Excel.</span><span class="sxs-lookup"><span data-stu-id="8d06e-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="8d06e-185">Dat ziet er al veel beter uit.</span><span class="sxs-lookup"><span data-stu-id="8d06e-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="8d06e-186">Zie ook</span><span class="sxs-lookup"><span data-stu-id="8d06e-186">See Also</span></span>   
[<span data-ttu-id="8d06e-187">Les 9: Hiërarchieën maken</span><span class="sxs-lookup"><span data-stu-id="8d06e-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="8d06e-188">Aanvullende les: Dynamische beveiliging</span><span class="sxs-lookup"><span data-stu-id="8d06e-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="8d06e-189">Aanvullende les: Detailrijen</span><span class="sxs-lookup"><span data-stu-id="8d06e-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  