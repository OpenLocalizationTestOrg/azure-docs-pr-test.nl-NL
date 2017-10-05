---
title: Gegevens analyseren met Azure Machine Learning | Microsoft Docs
description: Gebruik Azure Machine Learning om een voorspellend Machine Learning-model te maken dat is gebaseerd op gegevens die zijn opgeslagen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="3cd81-103">Gegevens analyseren met Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3cd81-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cd81-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="3cd81-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="3cd81-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3cd81-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="3cd81-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3cd81-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="3cd81-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="3cd81-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="3cd81-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="3cd81-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="3cd81-109">In deze zelfstudie wordt gebruikgemaakt van Azure Machine Learning om een voorspellend Machine Learning-model te maken dat is gebaseerd op gegevens die zijn opgeslagen in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3cd81-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3cd81-110">U maakt een gerichte marketingcampagne voor Adventure Works, de fietsenwinkel, door te voorspellen of een klant een fiets waarschijnlijk wel of niet zal kopen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3cd81-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3cd81-111">Prerequisites</span></span>
<span data-ttu-id="3cd81-112">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="3cd81-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="3cd81-113">Een SQL Data Warehouse waarin AdventureWorksDW-voorbeeldgegevens zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="3cd81-114">Zie voor het inrichten hiervan [Een SQL Data Warehouse maken][Create a SQL Data Warehouse] en kies ervoor om de voorbeeldgegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="3cd81-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="3cd81-115">Als u wel een datawarehouse hebt maar nog geen voorbeeldgegevens, kunt u [voorbeeldgegevens handmatig laden][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="3cd81-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="3cd81-116">1. De gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="3cd81-116">1. Get the data</span></span>
<span data-ttu-id="3cd81-117">De gegevens bevinden zich in de weergave dbo.vTargetMail in de AdventureWorksDW-database.</span><span class="sxs-lookup"><span data-stu-id="3cd81-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="3cd81-118">Deze gegevens lezen:</span><span class="sxs-lookup"><span data-stu-id="3cd81-118">To read this data:</span></span>

1. <span data-ttu-id="3cd81-119">Meld u aan bij [Azure Machine Learning Studio][Azure Machine Learning studio] en klik op My experiments (Mijn experimenten).</span><span class="sxs-lookup"><span data-stu-id="3cd81-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="3cd81-120">Klik op **+NEW** (Nieuw) en selecteer **Blank Experiment** (Leeg experiment).</span><span class="sxs-lookup"><span data-stu-id="3cd81-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="3cd81-121">Voer een naam in voor uw experiment: Targeted Marketing.</span><span class="sxs-lookup"><span data-stu-id="3cd81-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="3cd81-122">Sleep de module **Reader** van het deelvenster met modules naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="3cd81-123">Geef de details van uw SQL Data Warehouse-database op in het deelvenster Properties.</span><span class="sxs-lookup"><span data-stu-id="3cd81-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="3cd81-124">Geef de database**query** op om de gewenste gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-124">Specify the database **query** to read the data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="3cd81-125">Voer het experiment uit door onder experimentencanvas op **RUN** (UITVOEREN) te klikken.</span><span class="sxs-lookup"><span data-stu-id="3cd81-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="3cd81-126">![Voer het experiment uit.][1]</span><span class="sxs-lookup"><span data-stu-id="3cd81-126">![Run the experiment][1]</span></span>

<span data-ttu-id="3cd81-127">Wanneer het experiment is uitgevoerd, klikt u op de uitvoerpoort onder in de module Reader en selecteert u **Visualize** (Visualiseren) om de geïmporteerde gegevens te zien.</span><span class="sxs-lookup"><span data-stu-id="3cd81-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="3cd81-128">![Geïmporteerde gegevens weergeven][3]</span><span class="sxs-lookup"><span data-stu-id="3cd81-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="3cd81-129">2. De gegevens opschonen</span><span class="sxs-lookup"><span data-stu-id="3cd81-129">2. Clean the data</span></span>
<span data-ttu-id="3cd81-130">Als u de gegevens wilt opschonen, verwijdert u enkele kolommen die niet relevant zijn voor het model.</span><span class="sxs-lookup"><span data-stu-id="3cd81-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="3cd81-131">Om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="3cd81-131">To do this:</span></span>

1. <span data-ttu-id="3cd81-132">Sleep de module **Project Columns** (Projectkolommen) naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="3cd81-133">Klik in het deelvenster Properties (Eigenschappen) op **Launch column selector** (Kolomselectie starten) om de kolommen op te geven die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="3cd81-134">![Projectkolommen][4]</span><span class="sxs-lookup"><span data-stu-id="3cd81-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="3cd81-135">Sluit twee kolommen uit: CustomerAlternateKey en GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="3cd81-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="3cd81-136">![Overbodige kolommen verwijderen][5]</span><span class="sxs-lookup"><span data-stu-id="3cd81-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="3cd81-137">3. Het model maken</span><span class="sxs-lookup"><span data-stu-id="3cd81-137">3. Build the model</span></span>
<span data-ttu-id="3cd81-138">U gaat de gegevens 80-20 splitsen: 80% om een Machine Learning-model te trainen en 20% om het model te testen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="3cd81-139">Voor dit binair klassificatieprobleem gaat u de algoritme Two-Class gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cd81-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="3cd81-140">Sleep de module **Split** (Splitsen) naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="3cd81-141">Typ 0,8 in Fraction of rows in the first output dataset (Fractie van rijen in de eerste gegevensset) in het deelvenster Properties (Eigenschappen).</span><span class="sxs-lookup"><span data-stu-id="3cd81-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="3cd81-142">![Gegevens splitsen in trainings- en testset][6]</span><span class="sxs-lookup"><span data-stu-id="3cd81-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="3cd81-143">Sleep de module **Two-Class Boosted Decision Tree** (Beslissingsstructuur op basis van twee klassen) naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="3cd81-144">Sleep de module **Train Model** (Model trainen) naar het canvas en geef de invoer op.</span><span class="sxs-lookup"><span data-stu-id="3cd81-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="3cd81-145">Klik vervolgens in het deelvenster Properties (Eigenschappen) op **Launch column selector** (Kolomselectie starten).</span><span class="sxs-lookup"><span data-stu-id="3cd81-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="3cd81-146">Eerste invoer: ML-algoritme.</span><span class="sxs-lookup"><span data-stu-id="3cd81-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="3cd81-147">Tweede invoer: de gegevens waarmee u het algoritme wilt trainen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="3cd81-148">![Verbinding maken met de module Train Model (Model trainen)][7]</span><span class="sxs-lookup"><span data-stu-id="3cd81-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="3cd81-149">Selecteer de kolom **BikeBuyer** als de kolom die u wilt voorspellen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="3cd81-150">![Te voorspellen kolom selecteren][8]</span><span class="sxs-lookup"><span data-stu-id="3cd81-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="3cd81-151">4. Het model scoren</span><span class="sxs-lookup"><span data-stu-id="3cd81-151">4. Score the model</span></span>
<span data-ttu-id="3cd81-152">Nu gaat u testen hoe het model functioneert met testgegevens.</span><span class="sxs-lookup"><span data-stu-id="3cd81-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="3cd81-153">U gaat het gekozen algoritme vergelijken met een ander algoritme om te zien welk algoritme de beste prestaties levert.</span><span class="sxs-lookup"><span data-stu-id="3cd81-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="3cd81-154">Sleep de module **Score Model** (Model beoordelen) naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="3cd81-155">Eerste invoer: getraind model Tweede invoer: testgegevens ![Het model beoordelen][9]</span><span class="sxs-lookup"><span data-stu-id="3cd81-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="3cd81-156">Sleep de **Two-Class Bayes Point Machine** naar het experimentencanvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="3cd81-157">U gaat dit algoritme vergelijken met de Two-Class Boosted Decision Tree (Beslissingsstructuur met twee klassen).</span><span class="sxs-lookup"><span data-stu-id="3cd81-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="3cd81-158">Kopieer en plak de modules Train Model en Score Model naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3cd81-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="3cd81-159">Sleep het model **Evaluate Model** (Model evalueren) naar het canvas om de twee algoritmen te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="3cd81-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="3cd81-160">**Voer het experiment uit**.</span><span class="sxs-lookup"><span data-stu-id="3cd81-160">**Run** the experiment.</span></span>
   <span data-ttu-id="3cd81-161">![Het experiment uitvoeren.][10]</span><span class="sxs-lookup"><span data-stu-id="3cd81-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="3cd81-162">Klik op de uitvoerpoort onder in de module Evaluate Model (Model evalueren) en klik op Visualize (Visualiseren).</span><span class="sxs-lookup"><span data-stu-id="3cd81-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="3cd81-163">![Evaluatieresultaten visualiseren][11]</span><span class="sxs-lookup"><span data-stu-id="3cd81-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="3cd81-164">De verstrekte metrische gegevens zijn de ROC-curve, het precisie-/oproepdiagram en de liftcurve.</span><span class="sxs-lookup"><span data-stu-id="3cd81-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="3cd81-165">Als u deze metrische gegevens bekijkt, ziet u dat het eerste model beter presteert dan het tweede.</span><span class="sxs-lookup"><span data-stu-id="3cd81-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="3cd81-166">Als u de voorspellingen van het eerste model wilt zien, klikt u op de uitvoerpoort van de module Score Model en op Visualize (Visualiseren).</span><span class="sxs-lookup"><span data-stu-id="3cd81-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="3cd81-167">![Scoreresultaten visualiseren][12]</span><span class="sxs-lookup"><span data-stu-id="3cd81-167">![Visualize score results][12]</span></span>

<span data-ttu-id="3cd81-168">U ziet dat er twee of meer kolommen aan de testgegevensset zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3cd81-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="3cd81-169">Scored Probabilities (Berekende kansen): de waarschijnlijkheid dat een klant een fiets koopt.</span><span class="sxs-lookup"><span data-stu-id="3cd81-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="3cd81-170">Scored Labels (Berekende Labels): de classificatie die door het model is uitgevoerd: fietskoper (1) of niet (0).</span><span class="sxs-lookup"><span data-stu-id="3cd81-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="3cd81-171">Deze drempelwaarde voor waarschijnlijkheid voor labeling is ingesteld op 50% en kan worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="3cd81-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="3cd81-172">Door de kolom BikeBuyer (werkelijk) te vergelijken met de kolom Scored Labels (voorspelling), ziet u hoe goed het model heeft gepresteerd.</span><span class="sxs-lookup"><span data-stu-id="3cd81-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="3cd81-173">In de volgende stappen kunt u dit model gebruiken om voorspellingen te doen voor nieuwe klanten, en dit model publiceren als een webservice of resultaten opslaan in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3cd81-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cd81-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cd81-174">Next steps</span></span>
<span data-ttu-id="3cd81-175">Raadpleeg [Inleiding tot Machine Learning in Azure][Introduction to Machine Learning on Azure] voor meer informatie over het bouwen van voorspellende Machine Learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="3cd81-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
