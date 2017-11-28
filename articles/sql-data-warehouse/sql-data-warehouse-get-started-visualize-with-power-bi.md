---
title: aaaVisualize SQL Data Warehouse-gegevens met Power BI | Microsoft Azure
description: SQL Data Warehouse-gegevens visualiseren met Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="aefc7-103">Gegevens visualiseren met Power BI</span><span class="sxs-lookup"><span data-stu-id="aefc7-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aefc7-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="aefc7-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="aefc7-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aefc7-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="aefc7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aefc7-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="aefc7-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="aefc7-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="aefc7-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="aefc7-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="aefc7-109">Deze zelfstudie leert u hoe toouse Power BI tooconnect tooSQL Data Warehouse en enkele eenvoudige visualisaties maakt.</span><span class="sxs-lookup"><span data-stu-id="aefc7-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="aefc7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aefc7-110">Prerequisites</span></span>
<span data-ttu-id="aefc7-111">toostep voor deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="aefc7-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="aefc7-112">Een SQL Data Warehouse worden vooraf geladen met de database AdventureWorksDW Hallo.</span><span class="sxs-lookup"><span data-stu-id="aefc7-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="aefc7-113">tooprovision deze, Zie [maken van een SQL Data Warehouse] [ Create a SQL Data Warehouse] en kies tooload Hallo voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="aefc7-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="aefc7-114">Als u wel een datawarehouse hebt maar nog geen voorbeeldgegevens, kunt u [voorbeeldgegevens handmatig laden][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="aefc7-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="aefc7-115">1. Verbinding maken met database tooyour</span><span class="sxs-lookup"><span data-stu-id="aefc7-115">1. Connect tooyour database</span></span>
<span data-ttu-id="aefc7-116">tooopen Power BI en verbinding maken met de database AdventureWorksDW tooyour:</span><span class="sxs-lookup"><span data-stu-id="aefc7-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="aefc7-117">Meld u aan bij Hallo [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="aefc7-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="aefc7-118">Klik op **SQL-databases** en kies de SQL Data Warehouse-database AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="aefc7-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![De database zoeken][1]
3. <span data-ttu-id="aefc7-120">Klik op 'Openen in Power BI' Hallo-knop.</span><span class="sxs-lookup"><span data-stu-id="aefc7-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Power BI-knop][2]
4. <span data-ttu-id="aefc7-122">U ziet nu Hallo verbindingspagina voor SQL Data Warehouse om het webadres van uw database weer te geven.</span><span class="sxs-lookup"><span data-stu-id="aefc7-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="aefc7-123">Klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="aefc7-123">Click next.</span></span>
   
    ![Verbinding met Power BI][3]
5. <span data-ttu-id="aefc7-125">Voer uw Azure SQL server-gebruikersnaam en wachtwoord en kunt u zich volledig verbonden tooyour SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="aefc7-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Aanmelden bij Power BI][4]
6. <span data-ttu-id="aefc7-127">Nadat u bent aangemeld bij Power BI, klikt u op Hallo AdventureWorksDW gegevensset op Hallo links blade.</span><span class="sxs-lookup"><span data-stu-id="aefc7-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="aefc7-128">Hiermee opent u het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="aefc7-128">This will open hello database.</span></span>
   
    ![AdventureWorksDW wordt geopend in Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="aefc7-130">2. Een rapport maken</span><span class="sxs-lookup"><span data-stu-id="aefc7-130">2. Create a report</span></span>
<span data-ttu-id="aefc7-131">U bent nu klaar toouse Power BI tooanalyze uw voorbeeldgegevens van AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="aefc7-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="aefc7-132">tooperform hello analyse, AdventureWorksDW heeft een weergave die aggregatesales wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="aefc7-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="aefc7-133">Deze weergave bevat een aantal Hallo belangrijkste metrische gegevens voor het analyseren van Hallo verkoop van Hallo bedrijf.</span><span class="sxs-lookup"><span data-stu-id="aefc7-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="aefc7-134">toocreate een toewijzing van omzet volgens toopostal-code in deelvenster Hallo rechterdeelvenster met velden, klikt u op Hallo AggregateSales weergave tooexpand deze.</span><span class="sxs-lookup"><span data-stu-id="aefc7-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="aefc7-135">Klik op Hallo PostalCode en SalesAmount kolommen tooselect ze.</span><span class="sxs-lookup"><span data-stu-id="aefc7-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![AggregateSales selecteren in Power BI][6]
   
    <span data-ttu-id="aefc7-137">De gegevens, die in Power BI automatisch worden herkend als geografische gegevens, worden in een kaart geplaatst.</span><span class="sxs-lookup"><span data-stu-id="aefc7-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI-kaart][7]
2. <span data-ttu-id="aefc7-139">In deze stap maakt u een staafdiagram waarin de totale verkoop per klantinkomen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aefc7-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="aefc7-140">toocreate deze Ga toohello uitgevouwen weergave AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="aefc7-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="aefc7-141">Klik op Hallo SalesAmount veld.</span><span class="sxs-lookup"><span data-stu-id="aefc7-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="aefc7-142">Hallo Customer Income veld toohello links Sleep en zet het neer in as.</span><span class="sxs-lookup"><span data-stu-id="aefc7-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![As selecteren in Power BI][8]
   
    <span data-ttu-id="aefc7-144">We verplaatst Hallo staafdiagram via Hallo links.</span><span class="sxs-lookup"><span data-stu-id="aefc7-144">We moved hello bar chart over hello left.</span></span>
   
    ![Power BI-staafdiagram][9]
3. <span data-ttu-id="aefc7-146">Met deze stap maakt u een lijndiagram waarin de omzet per datum wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aefc7-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="aefc7-147">toocreate deze Ga toohello uitgevouwen weergave AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="aefc7-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="aefc7-148">Klik op SalesAmount en OrderDate.</span><span class="sxs-lookup"><span data-stu-id="aefc7-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="aefc7-149">Klik in Hallo visualisaties kolom Hallo lijndiagram pictogram; Dit is het eerste pictogram Hallo in Hallo tweede regel onder visualisaties.</span><span class="sxs-lookup"><span data-stu-id="aefc7-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Lijndiagram selecteren in Power BI][10]
   
    <span data-ttu-id="aefc7-151">U hebt nu een rapport met drie verschillende visualisaties van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="aefc7-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Power BI-lijndiagram][11]

<span data-ttu-id="aefc7-153">U kunt de voortgang op elk moment opslaan door op **Bestand** te klikken en **Opslaan** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="aefc7-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aefc7-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aefc7-154">Next steps</span></span>
<span data-ttu-id="aefc7-155">Nu we hebt u enige tijd toowarm maximaal verleend met voorbeeldgegevens hello, gaat u naar hoe te[ontwikkelen][develop], [laden][load], of [ migreren][migrate].</span><span class="sxs-lookup"><span data-stu-id="aefc7-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="aefc7-156">Of bekijk Hallo [website van Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="aefc7-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
