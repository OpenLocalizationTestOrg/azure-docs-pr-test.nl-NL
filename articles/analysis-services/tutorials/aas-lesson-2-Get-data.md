---
<span data-ttu-id="a247a-101">titel: aaa "Azure Analysis Services-zelfstudie les 2: gegevens ophalen | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe gegevens tooget en importeren in Hallo zelfstudie Azure Analysis Services-project.</span><span class="sxs-lookup"><span data-stu-id="a247a-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="a247a-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="a247a-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="a247a-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="a247a-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="a247a-104">Les 2: Gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="a247a-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a247a-105">In deze les kunt u gegevens ophalen gebruiken in SSDT tooconnect toohello AdventureWorksDW2014 voorbeelddatabase, selecteert u gegevens, voorbeeld en filter, en vervolgens importeren in uw modelwerkruimte.</span><span class="sxs-lookup"><span data-stu-id="a247a-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="a247a-106">Met behulp van Get Data kunt u gegevens importeren uit een groot aantal gegevensbronnen: Azure SQL Database, Oracle, Sybase, OData-Feed, Teradata, bestanden en meer.</span><span class="sxs-lookup"><span data-stu-id="a247a-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="a247a-107">U kunt ook query's uitvoeren op gegevens met een formule-expressie van Power Query M.</span><span class="sxs-lookup"><span data-stu-id="a247a-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="a247a-108">Geschatte tijd toocomplete deze les: **10 minuten**</span><span class="sxs-lookup"><span data-stu-id="a247a-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a247a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a247a-109">Prerequisites</span></span>  
<span data-ttu-id="a247a-110">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a247a-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a247a-111">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 1: Maak een nieuw model in tabelvorm project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="a247a-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="a247a-112">Een verbinding maken</span><span class="sxs-lookup"><span data-stu-id="a247a-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="a247a-113">een databaseverbinding toohello AdventureWorksDW2014 toocreate</span><span class="sxs-lookup"><span data-stu-id="a247a-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="a247a-114">Klik in Tabular Model Explorer met de rechtermuisknop op **Data Sources** > **Import from Data Source**.</span><span class="sxs-lookup"><span data-stu-id="a247a-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="a247a-115">Gegevens ophalen die u bij het maken van verbinding tooa gegevensbron begeleidt wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a247a-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="a247a-116">Als er geen Tabellair Model Explorer in **Solution Explorer**, dubbelklikt u op **Model.bim** tooopen Hallo-model in Hallo designer.</span><span class="sxs-lookup"><span data-stu-id="a247a-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="a247a-118">Klik in Get Data op **Database** > **SQL Server database** > **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a247a-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="a247a-119">In Hallo **SQL Server-Database** dialoogvenster in **Server**, typ de naam Hallo van Hallo-server waarop u Hallo AdventureWorksDW2014 database hebt geïnstalleerd en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a247a-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="a247a-120">Als u wordt gevraagd referenties tooenter, moet u toospecify Hallo referenties Analysis Services tooconnect toohello gegevensbron gebruikt bij het importeren en verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="a247a-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="a247a-121">Selecteer **Impersonate Account** in de lijst **Impersonation Mode**, geef referenties op en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a247a-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="a247a-122">Het verdient aanbeveling om dat u een account gebruiken waarbij Hallo wachtwoord verloopt niet.</span><span class="sxs-lookup"><span data-stu-id="a247a-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="a247a-124">Met een Windows-gebruikersaccount en wachtwoord, biedt de veiligste methode Hallo van verbindende tooa-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a247a-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="a247a-125">Selecteer in de Navigator Hallo **AdventureWorksDW2014** database en klik vervolgens op **OK**. Hiermee maakt u Hallo toohello databaseverbinding.</span><span class="sxs-lookup"><span data-stu-id="a247a-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="a247a-126">In Navigator Selecteer selectievakje in voor de tabellen na Hallo Hallo: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, en **heeft**.</span><span class="sxs-lookup"><span data-stu-id="a247a-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="a247a-128">Als u op OK klikt, wordt Query Editor geopend.</span><span class="sxs-lookup"><span data-stu-id="a247a-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="a247a-129">In de volgende sectie hello selecteert u alleen Hallo gewenste gegevens tooimport.</span><span class="sxs-lookup"><span data-stu-id="a247a-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="a247a-130">Hallo tabelgegevens filteren</span><span class="sxs-lookup"><span data-stu-id="a247a-130">Filter hello table data</span></span>  
<span data-ttu-id="a247a-131">Tabellen in Hallo AdventureWorksDW2014 voorbeelddatabase hebben gegevens die niet nodig tooinclude in uw model.</span><span class="sxs-lookup"><span data-stu-id="a247a-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="a247a-132">Indien mogelijk, wilt u toofilter uit onnodige gegevens toosave in het geheugen die wordt gebruikt door Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="a247a-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="a247a-133">U kunt uitfilteren aantal kolommen uit tabellen Hallo zodat ze zijn niet geïmporteerd in Hallo werkruimtedatabase, of de modeldatabase Hallo nadat deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a247a-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="a247a-134">toofilter hello tabelgegevens vóór het importeren</span><span class="sxs-lookup"><span data-stu-id="a247a-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="a247a-135">Selecteer in de Query-Editor Hallo **DimCustomer** tabel.</span><span class="sxs-lookup"><span data-stu-id="a247a-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="a247a-136">Hallo DimCustomer tabel op Hallo datasource (de voorbeelddatabase AdventureWorksDWQ2014) weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a247a-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="a247a-137">Selecteer de kolommen **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** en **FrenchOccupation** (Ctrl ingedrukt houden en klikken), klik met de rechtermuisknop en klik op **Remove Columns**.</span><span class="sxs-lookup"><span data-stu-id="a247a-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="a247a-139">Aangezien het Hallo-waarden voor deze kolommen zijn niet relevant tooInternet analyse, is er geen tooimport nodig deze kolommen.</span><span class="sxs-lookup"><span data-stu-id="a247a-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="a247a-140">Door overbodige kolommen te verwijderen, wordt uw model kleiner en efficiënter.</span><span class="sxs-lookup"><span data-stu-id="a247a-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="a247a-141">Hallo tabellen resterende door het verwijderen van de volgende kolommen in elke tabel Hallo filteren:</span><span class="sxs-lookup"><span data-stu-id="a247a-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="a247a-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="a247a-142">**DimDate**</span></span>
    
      |<span data-ttu-id="a247a-143">Kolom</span><span class="sxs-lookup"><span data-stu-id="a247a-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="a247a-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="a247a-144">DateKey</span></span>|  
      |<span data-ttu-id="a247a-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a247a-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="a247a-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a247a-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="a247a-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="a247a-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="a247a-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="a247a-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="a247a-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="a247a-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="a247a-150">Kolom</span><span class="sxs-lookup"><span data-stu-id="a247a-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="a247a-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="a247a-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="a247a-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="a247a-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="a247a-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="a247a-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="a247a-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="a247a-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="a247a-155">Kolom</span><span class="sxs-lookup"><span data-stu-id="a247a-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="a247a-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="a247a-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="a247a-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="a247a-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="a247a-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="a247a-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="a247a-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="a247a-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="a247a-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="a247a-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="a247a-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="a247a-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="a247a-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="a247a-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="a247a-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="a247a-167">Kolom</span><span class="sxs-lookup"><span data-stu-id="a247a-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="a247a-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="a247a-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="a247a-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="a247a-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="a247a-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="a247a-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="a247a-171">Kolom</span><span class="sxs-lookup"><span data-stu-id="a247a-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="a247a-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="a247a-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="a247a-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="a247a-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="a247a-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="a247a-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="a247a-175">Kolom</span><span class="sxs-lookup"><span data-stu-id="a247a-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="a247a-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="a247a-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="a247a-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="a247a-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="a247a-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="a247a-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="a247a-179"><a name="Import"></a>Hallo geselecteerd tabellen en kolommen gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="a247a-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="a247a-180">Nu dat u hebt bekeken en onnodige gegevens uitgefilterd, kunt u Hallo rest Hallo-gegevens die u wilt importeren.</span><span class="sxs-lookup"><span data-stu-id="a247a-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="a247a-181">Hallo wizard importeert Hallo tabelgegevens samen met de relaties tussen tabellen.</span><span class="sxs-lookup"><span data-stu-id="a247a-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="a247a-182">Nieuwe tabellen en kolommen worden gemaakt in Hallo model en gegevens die u hebt gefilterd is niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="a247a-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="a247a-183">Hallo tooimport tabellen en kolomgegevens geselecteerd</span><span class="sxs-lookup"><span data-stu-id="a247a-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="a247a-184">Bekijk de selecties.</span><span class="sxs-lookup"><span data-stu-id="a247a-184">Review your selections.</span></span> <span data-ttu-id="a247a-185">Als alles er goed uitziet, klikt u op **Import**.</span><span class="sxs-lookup"><span data-stu-id="a247a-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="a247a-186">Hallo gegevensverwerking dialoogvenster ziet Hallo status van gegevens uit uw gegevensbron in uw werkruimtedatabase wordt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="a247a-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="a247a-188">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="a247a-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="a247a-189">Het modelproject opslaan</span><span class="sxs-lookup"><span data-stu-id="a247a-189">Save your model project</span></span>  
<span data-ttu-id="a247a-190">Het is belangrijk toofrequently Sla het modelproject.</span><span class="sxs-lookup"><span data-stu-id="a247a-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="a247a-191">toosave hello model-project</span><span class="sxs-lookup"><span data-stu-id="a247a-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="a247a-192">Klik op **File** > **Save All**.</span><span class="sxs-lookup"><span data-stu-id="a247a-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="a247a-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a247a-193">What's next?</span></span>
<span data-ttu-id="a247a-194">[Les 3: Als gegevenstabel markeren](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="a247a-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
