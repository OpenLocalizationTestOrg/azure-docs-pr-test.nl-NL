---
title: SQL Data Warehouse-gegevens visualiseren met Power BI | Microsoft Azure
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
ms.openlocfilehash: a41393730143b14e91318a61858d989fff3786c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="c7772-103">Gegevens visualiseren met Power BI</span><span class="sxs-lookup"><span data-stu-id="c7772-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7772-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="c7772-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="c7772-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c7772-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="c7772-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7772-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="c7772-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c7772-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="c7772-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="c7772-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="c7772-109">In deze zelfstudie leert u hoe u Power BI gebruikt om verbinding te maken met SQL Data Warehouse en hoe u enkele eenvoudige visualisaties maakt.</span><span class="sxs-lookup"><span data-stu-id="c7772-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c7772-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c7772-110">Prerequisites</span></span>
<span data-ttu-id="c7772-111">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="c7772-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="c7772-112">Een SQL Data Warehouse die vooraf is geladen met de AdventureWorksDW-dataware.</span><span class="sxs-lookup"><span data-stu-id="c7772-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="c7772-113">Zie voor het inrichten hiervan [Een SQL Data Warehouse maken][Create a SQL Data Warehouse] en kies ervoor om de voorbeeldgegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="c7772-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="c7772-114">Als u wel een datawarehouse hebt maar nog geen voorbeeldgegevens, kunt u [voorbeeldgegevens handmatig laden][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="c7772-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="c7772-115">1. Verbinding maken met uw database</span><span class="sxs-lookup"><span data-stu-id="c7772-115">1. Connect to your database</span></span>
<span data-ttu-id="c7772-116">Ga als volgt te werk om Power BI te openen en verbinding te maken met de database AdventureWorksDW:</span><span class="sxs-lookup"><span data-stu-id="c7772-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="c7772-117">Meld u aan bij [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="c7772-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="c7772-118">Klik op **SQL-databases** en kies de SQL Data Warehouse-database AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="c7772-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![De database zoeken][1]
3. <span data-ttu-id="c7772-120">Klik op de knop Openen in Power BI.</span><span class="sxs-lookup"><span data-stu-id="c7772-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Power BI-knop][2]
4. <span data-ttu-id="c7772-122">Nu ziet u de verbindingspagina voor SQL Data Warehouse met het webadres van uw database.</span><span class="sxs-lookup"><span data-stu-id="c7772-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="c7772-123">Klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="c7772-123">Click next.</span></span>
   
    ![Verbinding met Power BI][3]
5. <span data-ttu-id="c7772-125">Voer de gebruikersnaam en het wachtwoord van uw Azure SQL server in, waarna u volledig wordt verbonden met uw SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="c7772-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Aanmelden bij Power BI][4]
6. <span data-ttu-id="c7772-127">Wanneer u bent aangemeld bij Power BI, klikt u in de linkerblade op de gegevensset AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="c7772-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="c7772-128">De database wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c7772-128">This will open the database.</span></span>
   
    ![AdventureWorksDW wordt geopend in Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="c7772-130">2. Een rapport maken</span><span class="sxs-lookup"><span data-stu-id="c7772-130">2. Create a report</span></span>
<span data-ttu-id="c7772-131">Nu kunt u Power BI gebruiken om de voorbeeldgegevens uit AdventureWorksDW te analyseren.</span><span class="sxs-lookup"><span data-stu-id="c7772-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="c7772-132">Voor de analyse heeft AdventureWorksDW een weergave die AggregateSales wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="c7772-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="c7772-133">Deze weergave bevat enkele van de belangrijkste metrische gegevens om de verkoopcijfers van het bedrijf te analyseren.</span><span class="sxs-lookup"><span data-stu-id="c7772-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="c7772-134">Als u een kaart wilt maken van de totale verkoop op postcode, klikt u in het rechterdeelvenster met velden op de weergave AggregateSales om deze uit te vouwen.</span><span class="sxs-lookup"><span data-stu-id="c7772-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="c7772-135">Klik op de kolommen PostalCode en SalesAmount om deze te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c7772-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![AggregateSales selecteren in Power BI][6]
   
    <span data-ttu-id="c7772-137">De gegevens, die in Power BI automatisch worden herkend als geografische gegevens, worden in een kaart geplaatst.</span><span class="sxs-lookup"><span data-stu-id="c7772-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI-kaart][7]
2. <span data-ttu-id="c7772-139">In deze stap maakt u een staafdiagram waarin de totale verkoop per klantinkomen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c7772-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="c7772-140">Daarvoor gaat u naar de uitgevouwen weergave AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="c7772-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="c7772-141">Klik in het veld SalesAmount.</span><span class="sxs-lookup"><span data-stu-id="c7772-141">Click the SalesAmount field.</span></span> <span data-ttu-id="c7772-142">Sleep het veld Customer Income naar links en zet het neer in As.</span><span class="sxs-lookup"><span data-stu-id="c7772-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![As selecteren in Power BI][8]
   
    <span data-ttu-id="c7772-144">We hebben het staafdiagram over het linkerdiagram geplaatst.</span><span class="sxs-lookup"><span data-stu-id="c7772-144">We moved the bar chart over the left.</span></span>
   
    ![Power BI-staafdiagram][9]
3. <span data-ttu-id="c7772-146">Met deze stap maakt u een lijndiagram waarin de omzet per datum wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c7772-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="c7772-147">Daarvoor gaat u naar de uitgevouwen weergave AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="c7772-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="c7772-148">Klik op SalesAmount en OrderDate.</span><span class="sxs-lookup"><span data-stu-id="c7772-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="c7772-149">Klik in de kolom Visualisaties op het pictogram Lijndiagram. Dit is het eerste pictogram in de tweede regel onder Visualisaties.</span><span class="sxs-lookup"><span data-stu-id="c7772-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Lijndiagram selecteren in Power BI][10]
   
    <span data-ttu-id="c7772-151">U hebt nu een rapport met drie verschillende visualisaties van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c7772-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![Power BI-lijndiagram][11]

<span data-ttu-id="c7772-153">U kunt de voortgang op elk moment opslaan door op **Bestand** te klikken en **Opslaan** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c7772-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7772-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7772-154">Next steps</span></span>
<span data-ttu-id="c7772-155">U hebt wat kunnen oefenen met behulp van de voorbeeldgegevens en gaat nu leren hoe u kunt [ontwikkelen][develop], [laden][load] of [migreren][migrate].</span><span class="sxs-lookup"><span data-stu-id="c7772-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="c7772-156">U kunt natuurlijk ook een kijkje nemen op de [website van Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="c7772-156">Or take a look at the [Power BI website][Power BI website].</span></span>

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
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
