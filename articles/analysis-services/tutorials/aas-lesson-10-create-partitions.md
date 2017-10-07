---
<span data-ttu-id="85426-101">titel: aaa "Azure Analysis Services-zelfstudie les 10: partities maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate partities in de zelfstudie hello Azure Analysis Services-project.</span><span class="sxs-lookup"><span data-stu-id="85426-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="85426-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="85426-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="85426-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="85426-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="85426-104">Les 10: Partities maken</span><span class="sxs-lookup"><span data-stu-id="85426-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="85426-105">In deze les kunt u partities toodivide Hallo heeft tabel maken in kleinere logische delen die verwerkt (vernieuwd) onafhankelijk van andere partities worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="85426-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="85426-106">Elke tabel die u in uw model opnemen heeft standaard één partitie, waaronder de kolommen en rijen alle Hallo-tabel.</span><span class="sxs-lookup"><span data-stu-id="85426-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="85426-107">Hallo heeft tabel willen we toodivide Hallo gegevens per jaar; één partitie voor elk van de tabel Hallo vijf jaar.</span><span class="sxs-lookup"><span data-stu-id="85426-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="85426-108">Elke partitie kan vervolgens onafhankelijk worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85426-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="85426-109">toolearn meer, Zie [partities](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="85426-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="85426-110">Geschatte tijd toocomplete deze les: **15 minuten**</span><span class="sxs-lookup"><span data-stu-id="85426-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="85426-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85426-111">Prerequisites</span></span>  
<span data-ttu-id="85426-112">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="85426-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="85426-113">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 9: hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="85426-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="85426-114">Partities maken</span><span class="sxs-lookup"><span data-stu-id="85426-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="85426-115">toocreate partities in Hallo heeft tabel</span><span class="sxs-lookup"><span data-stu-id="85426-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="85426-116">Vouw in Tabular Model Explorer het gedeelte **Tables** uit en klik vervolgens met de rechtermuisknop op **FactInternetSales** > **Partitions**.</span><span class="sxs-lookup"><span data-stu-id="85426-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="85426-117">Klik in partitiebeheer **kopie**, en wijzig vervolgens de naam van de Hallo te**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="85426-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="85426-118">Omdat u wilt dat Hallo partitie tooinclude alleen die rijen binnen een bepaalde periode Hallo jaar 2010, moet u de query-expressie Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="85426-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="85426-119">Klik op **ontwerp** tooopen Query-Editor en klik vervolgens op Hallo **FactInternetSales2010** query.</span><span class="sxs-lookup"><span data-stu-id="85426-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="85426-120">Preview-versie, klikt u op Hallo pijl-omlaag in Hallo **OrderDate** kolomkop en klik vervolgens op **datum/tijd-Filters** > **tussen**.</span><span class="sxs-lookup"><span data-stu-id="85426-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="85426-122">Hallo rijen filteren in het dialoogvenster in **rijen weergeven waarvoor: OrderDate**, laat **is na of is gelijk aan**, en voer vervolgens in het veld Hallo **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="85426-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="85426-123">Hallo laat **en** operator geselecteerd, selecteer vervolgens **voordat**, voert u vervolgens in het veld Hallo **1-1-2011**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="85426-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="85426-125">In Query-editor ziet u, bij TOEGEPASTE STAPPEN, een andere stap met de naam Filtered Rows.</span><span class="sxs-lookup"><span data-stu-id="85426-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="85426-126">Dit filter is het enige volgorde datums tooselect van 2010.</span><span class="sxs-lookup"><span data-stu-id="85426-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="85426-127">Klik op **Import**.</span><span class="sxs-lookup"><span data-stu-id="85426-127">Click **Import**.</span></span>

    <span data-ttu-id="85426-128">In partitiebeheer u ziet nu expressie heeft een extra rijen gefilterd component Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="85426-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="85426-130">Deze instructie geeft dat deze partitie alleen Hallo-gegevens in deze rijen waar Hallo OrderDate zich in Hallo 2010 kalenderjaar zoals opgegeven in de component van Hallo gefilterde rijen bevindt bevatten.</span><span class="sxs-lookup"><span data-stu-id="85426-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="85426-131">toocreate een partitie voor Hallo 2011 jaar</span><span class="sxs-lookup"><span data-stu-id="85426-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="85426-132">Klik in Hallo Partitielijst op Hallo **FactInternetSales2010** partitie-u hebt gemaakt en klik vervolgens op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="85426-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="85426-133">De partitienaam Hallo ook wijzigen**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="85426-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="85426-134">U hoeft niet toouse Query-Editor toocreate een nieuwe gefilterde rijen-component.</span><span class="sxs-lookup"><span data-stu-id="85426-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="85426-135">Omdat u een kopie van Hallo query gemaakt voor 2010, toodo hoeft u een kleine wijziging aanbrengt in het Hallo-query voor 2011.</span><span class="sxs-lookup"><span data-stu-id="85426-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="85426-136">In **Query-expressie**, in volgorde voor deze partitie tooinclude alleen die rijen voor Hallo 2011 jaar, vervang Hallo jaar in Hallo rijen gefilterd-component met **2011** en **2012**respectievelijk, zoals:</span><span class="sxs-lookup"><span data-stu-id="85426-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="85426-137">toocreate partities voor 2012, 2013 en 2014.</span><span class="sxs-lookup"><span data-stu-id="85426-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="85426-138">Stappen Hallo vorige, voor het maken van partities voor 2012, 2013 en 2014, Hallo jaren in Hallo rijen gefilterd component tooinclude alleen rijen voor dat jaar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="85426-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="85426-139">Hallo heeft partitie verwijderen</span><span class="sxs-lookup"><span data-stu-id="85426-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="85426-140">Nu dat u partities voor elk jaar hebt, kunt u Hallo heeft partitie; verwijderen Zo wordt voorkomen dat overlappen bij het proces alle kiezen bij het verwerken van partities.</span><span class="sxs-lookup"><span data-stu-id="85426-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="85426-141">toodelete hello heeft partitie</span><span class="sxs-lookup"><span data-stu-id="85426-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="85426-142">Klik op Hallo heeft partitie en klikt u vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="85426-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="85426-143">Partities verwerken</span><span class="sxs-lookup"><span data-stu-id="85426-143">Process partitions</span></span>  
<span data-ttu-id="85426-144">In partitiebeheer kennisgeving Hallo **laatste verwerkte** kolom voor elke Hallo nieuwe partities die u hebt gemaakt ziet deze partities nooit is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="85426-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="85426-145">Wanneer u partities maakt, moet u een proces partities of proces bewerking toorefresh Hallo tabelgegevens in deze partities uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="85426-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="85426-146">tooprocess hello heeft partities</span><span class="sxs-lookup"><span data-stu-id="85426-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="85426-147">Klik op **OK** tooclose partitiebeheer.</span><span class="sxs-lookup"><span data-stu-id="85426-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="85426-148">Klik op Hallo **heeft** tabel en klik op Hallo **Model** menu > **proces** > **proces partities**.</span><span class="sxs-lookup"><span data-stu-id="85426-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="85426-149">Hallo proces partities in het dialoogvenster controleren **modus** te is ingesteld,**Process standaard**.</span><span class="sxs-lookup"><span data-stu-id="85426-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="85426-150">Hallo selectievakje selecteert in Hallo **proces** kolom voor elke Hallo vijf partities u hebt gemaakt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="85426-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="85426-152">Als u wordt gevraagd om referenties voor imitatie, voert u Hallo Windows-gebruikersnaam en wachtwoord die u hebt opgegeven in les 2.</span><span class="sxs-lookup"><span data-stu-id="85426-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="85426-153">Hallo **gegevensverwerking** in het dialoogvenster wordt weergegeven en toont de Procesdetails van het voor elke partitie.</span><span class="sxs-lookup"><span data-stu-id="85426-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="85426-154">U ziet dat voor elke partitie een ander aantal rijen wordt overgebracht.</span><span class="sxs-lookup"><span data-stu-id="85426-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="85426-155">Elke partitie bevat alleen die rijen voor de opgegeven in de WHERE-component in SQL-instructie Hallo HALLO hallo-jaar.</span><span class="sxs-lookup"><span data-stu-id="85426-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="85426-156">Zodra de verwerking is voltooid, gaat u verder gaan en Hallo gegevensverwerking dialoogvenster te sluiten.</span><span class="sxs-lookup"><span data-stu-id="85426-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="85426-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85426-158">What's next?</span></span>
<span data-ttu-id="85426-159">De volgende les Ga toohello: [les 11: rollen maken](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="85426-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
