---
title: 'Stap 2: Gegevens uploaden naar een Machine Learning-experiment | Microsoft Docs'
description: 'Stap 2 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: het uploaden van openbare gegevens opgeslagen in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="a730c-103">Kennismaken, stap 2: Bestaande gegevens uploaden naar een Azure Machine Learning-experiment</span><span class="sxs-lookup"><span data-stu-id="a730c-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="a730c-104">Dit is de tweede stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a730c-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a730c-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="a730c-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="a730c-106">**Bestaande gegevens uploaden**</span><span class="sxs-lookup"><span data-stu-id="a730c-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="a730c-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="a730c-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a730c-108">Trainen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="a730c-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a730c-109">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="a730c-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a730c-110">Toegang tot Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="a730c-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a730c-111">een Voorspellend model voor kredietrisico toodevelop, moeten we gegevens we kunnen tootrain gebruiken en test u Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="a730c-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="a730c-112">Voor dit scenario gebruiken we Hallo 'UCI Statlog (Duitse tegoed gegevens) Data Set' uit Hallo UC Irvine Machine Learning-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a730c-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="a730c-113">U kunt deze hier vinden:</span><span class="sxs-lookup"><span data-stu-id="a730c-113">You can find it here:</span></span>  
<span data-ttu-id="a730c-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://Archive.ICS.uci.edu/ml/DataSets/Statlog+(German+credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="a730c-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="a730c-115">We gebruiken Hallo-bestand met de naam **german.data**.</span><span class="sxs-lookup"><span data-stu-id="a730c-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="a730c-116">Downloaden van dit bestand tooyour lokale vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="a730c-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="a730c-117">Hallo **german.data** gegevensset bevat rijen van 20 variabelen voor 1000 afgelopen aanvragers tegoed.</span><span class="sxs-lookup"><span data-stu-id="a730c-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="a730c-118">Deze 20 variabelen vertegenwoordigen reeks functies van deze dataset hello (Hallo *functie vector*), waarmee u identificatiekenmerken op voor elke aanvrager tegoed.</span><span class="sxs-lookup"><span data-stu-id="a730c-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="a730c-119">Een extra kolom in elke rij vertegenwoordigt van de aanvrager Hallo berekende kredietrisico, met 700 aanvrager aangeduid als een lage kredietrisico en 300 als een hoog risico.</span><span class="sxs-lookup"><span data-stu-id="a730c-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="a730c-120">Hallo UCI website bevat een beschrijving van Hallo kenmerken van de functie-vector Hallo voor deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="a730c-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="a730c-121">Dit omvat financiële gegevens, kredietgeschiedenis werkstatus en persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="a730c-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="a730c-122">Voor iedere aanvrager een binaire classificatie is opgegeven waarmee wordt aangegeven of ze zich een lage of hoge kredietrisico.</span><span class="sxs-lookup"><span data-stu-id="a730c-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="a730c-123">We gebruiken deze gegevens tootrain een predictive analytics-model.</span><span class="sxs-lookup"><span data-stu-id="a730c-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="a730c-124">Als we bent klaar, moet het model kunnen tooaccept een functie-vector voor een nieuwe persoon en of hij of zij een lage of hoge kredietrisico is voorspellen.</span><span class="sxs-lookup"><span data-stu-id="a730c-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="a730c-125">Hier volgt een interessante twist.</span><span class="sxs-lookup"><span data-stu-id="a730c-125">Here's an interesting twist.</span></span> <span data-ttu-id="a730c-126">Hallo beschrijving van gegevensset Hallo op Hallo UCI website vermeldingen die het kost als we iemands kredietrisico misclassify.</span><span class="sxs-lookup"><span data-stu-id="a730c-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="a730c-127">Als u een hoge kredietrisico Hallo model voorspelt voor iemand die daadwerkelijk een lage kredietrisico is, heeft Hallo model een misclassification doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a730c-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="a730c-128">Maar Hallo omgekeerde misclassification vijf keer duurder toohello financiële instelling is: indien Hallo model voorspelt een lage kredietrisico voor iemand die daadwerkelijk een hoge kredietrisico is.</span><span class="sxs-lookup"><span data-stu-id="a730c-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="a730c-129">Ja, willen we tootrain ons model zodat Hallo kosten van dit laatste type misclassification vijf keer hoger is dan onjuiste Hallo andere manier.</span><span class="sxs-lookup"><span data-stu-id="a730c-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="a730c-130">Een eenvoudige manier toodo dit wanneer Hallo model bij ons experiment training is door te dupliceren (vijfmaal) die items die iemand met een hoge kredietrisico vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="a730c-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="a730c-131">Vervolgens als Hallo model ten onrechte iemand als een lage kredietrisico classificeert wanneer ze daadwerkelijk een hoog risico, Hallo model geen die dezelfde misclassification vijf keer één keer voor elke kopie.</span><span class="sxs-lookup"><span data-stu-id="a730c-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="a730c-132">Hierdoor neemt Hallo kosten van deze fout in Hallo training resultaten.</span><span class="sxs-lookup"><span data-stu-id="a730c-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="a730c-133">Hallo gegevensset-indeling converteren</span><span class="sxs-lookup"><span data-stu-id="a730c-133">Convert hello dataset format</span></span>
<span data-ttu-id="a730c-134">de oorspronkelijke gegevensset Hallo gebruikt een leeg gescheiden-indeling.</span><span class="sxs-lookup"><span data-stu-id="a730c-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="a730c-135">Machine Learning Studio werkt beter met een bestand met door komma's gescheiden waarden (CSV), zodat we Hallo gegevensset converteren je door spaties vervangen door komma's.</span><span class="sxs-lookup"><span data-stu-id="a730c-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="a730c-136">Er zijn veel manieren tooconvert deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="a730c-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="a730c-137">Eenzijdige is met behulp van de volgende Windows PowerShell-opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a730c-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="a730c-138">Er is een andere manier met behulp van Hallo Unix ype opdracht:</span><span class="sxs-lookup"><span data-stu-id="a730c-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="a730c-139">In beide gevallen is er een door komma's gescheiden versie Hallo-gegevens in een bestand met de naam gemaakt **german.csv** die we in ons experiment kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a730c-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="a730c-140">Hallo gegevensset tooMachine Learning Studio uploaden</span><span class="sxs-lookup"><span data-stu-id="a730c-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="a730c-141">Zodra het Hallo-gegevens zijn geconverteerde tooCSV indeling, moeten we tooupload in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="a730c-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="a730c-142">Open Hallo Machine Learning Studio-startpagina ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="a730c-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="a730c-143">Klik op Hallo menu ![Menu][1] in Hallo linkerbovenhoek van Hallo-venster, klikt u op **Azure Machine Learning**, selecteer **Studio**, en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="a730c-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="a730c-144">Klik op **+ nieuw** onderaan Hallo Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="a730c-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="a730c-145">Selecteer **GEGEVENSSET**.</span><span class="sxs-lookup"><span data-stu-id="a730c-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="a730c-146">Selecteer **vanuit het lokale bestand**.</span><span class="sxs-lookup"><span data-stu-id="a730c-146">Select **FROM LOCAL FILE**.</span></span>

    ![Voeg een gegevensset toe vanuit het lokale bestand][2]

6. <span data-ttu-id="a730c-148">In Hallo **uploaden van een nieuwe gegevensset** dialoogvenster, klikt u op **Bladeren** en Hallo zoeken **german.csv** dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a730c-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="a730c-149">Voer een naam voor de Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a730c-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="a730c-150">Voor dit scenario moet aanroepen 'UCI Duits creditcardgegevens'.</span><span class="sxs-lookup"><span data-stu-id="a730c-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="a730c-151">Selecteer voor gegevenstype **generieke CSV-bestand met geen koptekst (. nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="a730c-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="a730c-152">Een beschrijving toevoegen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="a730c-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="a730c-153">Klik op Hallo **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a730c-153">Click hello **OK** check mark.</span></span>  

    ![Hallo gegevensset uploaden][3]

<span data-ttu-id="a730c-155">Dit uploadt Hallo gegevens naar een gegevensset-module die u in een experiment gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="a730c-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="a730c-156">U kunt beheren die u hebt geüpload, tooStudio door te klikken op Hallo gegevenssets **GEGEVENSSETS** tabblad toohello links van de Hallo Studio-venster.</span><span class="sxs-lookup"><span data-stu-id="a730c-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Gegevenssets beheren][4]

<span data-ttu-id="a730c-158">Zie voor meer informatie over het importeren van andere typen gegevens in een experiment [uw trainingsgegevens importeren in Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="a730c-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="a730c-159">**Volgende stap: [een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="a730c-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
