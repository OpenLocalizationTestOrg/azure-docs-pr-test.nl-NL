---
title: aaaAnalyze gegevens met Azure Machine Learning | Microsoft Docs
description: Gebruik toobuild Azure Machine Learning een Voorspellend machine learning-model op basis van gegevens die zijn opgeslagen in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="9def3-103">Gegevens analyseren met Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9def3-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9def3-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="9def3-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="9def3-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9def3-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="9def3-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9def3-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="9def3-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="9def3-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="9def3-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="9def3-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="9def3-109">Deze zelfstudie wordt toobuild Azure Machine Learning een Voorspellend machine learning-model op basis van gegevens die zijn opgeslagen in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9def3-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="9def3-110">In het bijzonder het resultaat hiervan is een gerichte marketingcampagne voor Adventure Works, de fietsenwinkel hello, door te voorspellen als een klant waarschijnlijk toobuy een fiets is of niet.</span><span class="sxs-lookup"><span data-stu-id="9def3-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9def3-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9def3-111">Prerequisites</span></span>
<span data-ttu-id="9def3-112">toostep voor deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="9def3-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="9def3-113">Een SQL Data Warehouse waarin AdventureWorksDW-voorbeeldgegevens zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="9def3-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="9def3-114">tooprovision deze, Zie [maken van een SQL Data Warehouse] [ Create a SQL Data Warehouse] en kies tooload Hallo voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="9def3-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="9def3-115">Als u wel een datawarehouse hebt maar nog geen voorbeeldgegevens, kunt u [voorbeeldgegevens handmatig laden][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="9def3-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="9def3-116">1. Hallo-gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="9def3-116">1. Get hello data</span></span>
<span data-ttu-id="9def3-117">Hallo-gegevens zijn in de weergave dbo.vTargetMail Hallo in de database AdventureWorksDW Hallo.</span><span class="sxs-lookup"><span data-stu-id="9def3-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="9def3-118">tooread deze gegevens:</span><span class="sxs-lookup"><span data-stu-id="9def3-118">tooread this data:</span></span>

1. <span data-ttu-id="9def3-119">Meld u aan bij [Azure Machine Learning Studio][Azure Machine Learning studio] en klik op My experiments (Mijn experimenten).</span><span class="sxs-lookup"><span data-stu-id="9def3-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="9def3-120">Klik op **+NEW** (Nieuw) en selecteer **Blank Experiment** (Leeg experiment).</span><span class="sxs-lookup"><span data-stu-id="9def3-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="9def3-121">Voer een naam in voor uw experiment: Targeted Marketing.</span><span class="sxs-lookup"><span data-stu-id="9def3-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="9def3-122">Sleep Hallo **lezer** module op basis van het deelvenster met modules Hallo naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="9def3-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="9def3-123">Geef details op Hallo van uw SQL Data Warehouse-database in deelvenster Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="9def3-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="9def3-124">Geef Hallo database **query** tooread Hallo gegevens van belang.</span><span class="sxs-lookup"><span data-stu-id="9def3-124">Specify hello database **query** tooread hello data of interest.</span></span>

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

<span data-ttu-id="9def3-125">Hallo-experiment uitvoeren door te klikken op **uitvoeren** onder het experimentcanvas Hallo.</span><span class="sxs-lookup"><span data-stu-id="9def3-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="9def3-126">![Hallo-experiment uitvoeren][1]</span><span class="sxs-lookup"><span data-stu-id="9def3-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="9def3-127">Nadat het Hallo-experiment is uitgevoerd, klikt u op de uitvoerpoort Hallo HALLO hallo leesmodule onderaan in en selecteert u **Visualize** toosee Hallo geïmporteerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="9def3-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="9def3-128">![Geïmporteerde gegevens weergeven][3]</span><span class="sxs-lookup"><span data-stu-id="9def3-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="9def3-129">2. Schone Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="9def3-129">2. Clean hello data</span></span>
<span data-ttu-id="9def3-130">tooclean hello gegevens, verwijderen kolommen die niet relevant voor Hallo model.</span><span class="sxs-lookup"><span data-stu-id="9def3-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="9def3-131">toodo dit:</span><span class="sxs-lookup"><span data-stu-id="9def3-131">toodo this:</span></span>

1. <span data-ttu-id="9def3-132">Sleep Hallo **Projectkolommen** module naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="9def3-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="9def3-133">Klik op **Launch column selector** in Hallo eigenschappen deelvenster toospecify kolommen die u wenst dat toodrop.</span><span class="sxs-lookup"><span data-stu-id="9def3-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="9def3-134">![Projectkolommen][4]</span><span class="sxs-lookup"><span data-stu-id="9def3-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="9def3-135">Sluit twee kolommen uit: CustomerAlternateKey en GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="9def3-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="9def3-136">![Overbodige kolommen verwijderen][5]</span><span class="sxs-lookup"><span data-stu-id="9def3-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="9def3-137">3. Hallo-model maken</span><span class="sxs-lookup"><span data-stu-id="9def3-137">3. Build hello model</span></span>
<span data-ttu-id="9def3-138">We zullen Hallo gegevens 80-20 splitsen: 80% tootrain een machine learning-model en 20% tootest Hallo model.</span><span class="sxs-lookup"><span data-stu-id="9def3-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="9def3-139">Maken we gebruik van Hallo 'Two-Class' algoritmen voor dit binair klassificatieprobleem.</span><span class="sxs-lookup"><span data-stu-id="9def3-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="9def3-140">Sleep Hallo **gesplitste** module naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="9def3-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="9def3-141">Typ 0,8 fractie van rijen in de eerste uitvoergegevensset Hallo in deelvenster Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="9def3-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="9def3-142">![Gegevens splitsen in trainings- en testset][6]</span><span class="sxs-lookup"><span data-stu-id="9def3-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="9def3-143">Sleep Hallo **Two-Class Boosted Decision Tree** module naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="9def3-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="9def3-144">Sleep Hallo **Train Model** module in Hallo canvas en geef Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="9def3-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="9def3-145">Klik vervolgens op **Launch column selector** in deelvenster Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="9def3-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="9def3-146">Eerste invoer: ML-algoritme.</span><span class="sxs-lookup"><span data-stu-id="9def3-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="9def3-147">Tweede invoer: gegevens tootrain Hallo algoritme op.</span><span class="sxs-lookup"><span data-stu-id="9def3-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="9def3-148">![Sluit Hallo Train Model-module][7]</span><span class="sxs-lookup"><span data-stu-id="9def3-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="9def3-149">Selecteer Hallo **BikeBuyer** Hallo kolom toopredict kolom.</span><span class="sxs-lookup"><span data-stu-id="9def3-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="9def3-150">![Selecteer de kolom toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="9def3-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="9def3-151">4. Hallo-score-model</span><span class="sxs-lookup"><span data-stu-id="9def3-151">4. Score hello model</span></span>
<span data-ttu-id="9def3-152">Nu gaat u testen hoe Hallo model functioneert met testgegevens.</span><span class="sxs-lookup"><span data-stu-id="9def3-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="9def3-153">Hallo-algoritme van onze keuze met een ander algoritme toosee die beter presteert gaat vergelijken.</span><span class="sxs-lookup"><span data-stu-id="9def3-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="9def3-154">Sleep **Score Model** module naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="9def3-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="9def3-155">Eerste invoer: getraind model tweede invoer: testgegevens ![Hallo-Score-model][9]</span><span class="sxs-lookup"><span data-stu-id="9def3-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="9def3-156">Sleep Hallo **Two-Class Bayes Point Machine** naar het experimentcanvas Hallo.</span><span class="sxs-lookup"><span data-stu-id="9def3-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="9def3-157">U gaat vergelijken hoe dit algoritme in vergelijking toohello Two-Class Boosted Decision Tree uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9def3-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="9def3-158">Kopiëren en plakken Hallo modules Train Model en Score-Model in Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="9def3-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="9def3-159">Sleep Hallo **Evaluate Model** module in Hallo canvas toocompare Hallo twee algoritmen.</span><span class="sxs-lookup"><span data-stu-id="9def3-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="9def3-160">**Voer** Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="9def3-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="9def3-161">![Hallo-experiment uitvoeren][10]</span><span class="sxs-lookup"><span data-stu-id="9def3-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="9def3-162">Hallo uitvoerpoort onder Hallo van de module Evaluate Model Hallo en klik op Visualize.</span><span class="sxs-lookup"><span data-stu-id="9def3-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="9def3-163">![Evaluatieresultaten visualiseren][11]</span><span class="sxs-lookup"><span data-stu-id="9def3-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="9def3-164">Hallo verstrekte metrische gegevens zijn Hallo ROC-curve, precisie-/ oproepdiagram diagram en lift-curve.</span><span class="sxs-lookup"><span data-stu-id="9def3-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="9def3-165">Deze metrische gegevens bekijkt, ziet u dat Hallo eerste model beter dan tweede Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9def3-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="9def3-166">toolook op Hallo wat Hallo eerste model voorspeld, klik op de uitvoerpoort van Hallo Score Model en klik op Visualize.</span><span class="sxs-lookup"><span data-stu-id="9def3-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="9def3-167">![Scoreresultaten visualiseren][12]</span><span class="sxs-lookup"><span data-stu-id="9def3-167">![Visualize score results][12]</span></span>

<span data-ttu-id="9def3-168">Ziet u dat twee of meer kolommen tooyour testgegevensset toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9def3-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="9def3-169">Scored kansen: Hallo kans dat een klant een fiets koopt is.</span><span class="sxs-lookup"><span data-stu-id="9def3-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="9def3-170">Scored Labels: Hallo classificatie gedaan door Hallo model: fietskoper (1) of niet (0).</span><span class="sxs-lookup"><span data-stu-id="9def3-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="9def3-171">Deze drempelwaarde voor waarschijnlijkheid voor labeling too50% wordt ingesteld en kan worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="9def3-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="9def3-172">Hallo kolom BikeBuyer (werkelijk) met Hallo Scored Labels (voorspelling) te vergelijken, kunt u zien hoe goed Hallo model heeft gepresteerd.</span><span class="sxs-lookup"><span data-stu-id="9def3-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="9def3-173">De volgende stappen kunt u dit model toomake voorspellingen gebruiken voor nieuwe klanten en dit model publiceren als een webservice of resultaten back tooSQL datawarehouse schrijven.</span><span class="sxs-lookup"><span data-stu-id="9def3-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9def3-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9def3-174">Next steps</span></span>
<span data-ttu-id="9def3-175">toolearn meer informatie over het bouwen van voorspellende machine learning-modellen, te verwijzen[inleiding tooMachine Learning in Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="9def3-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

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
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
