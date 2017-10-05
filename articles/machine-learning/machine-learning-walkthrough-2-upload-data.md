---
title: 'Stap 2: Gegevens uploaden naar een Machine Learning-experiment | Microsoft Docs'
description: 'Stap 2 van het ontwikkelen van een voorspellende oplossing overzicht: het uploaden van openbare gegevens opgeslagen in Azure Machine Learning Studio.'
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
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="5fd75-103">Kennismaken, stap 2: Bestaande gegevens uploaden naar een Azure Machine Learning-experiment</span><span class="sxs-lookup"><span data-stu-id="5fd75-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="5fd75-104">Dit is de tweede stap van de procedure [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="5fd75-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="5fd75-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="5fd75-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="5fd75-106">**Bestaande gegevens uploaden**</span><span class="sxs-lookup"><span data-stu-id="5fd75-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="5fd75-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="5fd75-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="5fd75-108">De modellen trainen en evalueren</span><span class="sxs-lookup"><span data-stu-id="5fd75-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="5fd75-109">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="5fd75-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="5fd75-110">Toegang tot de webservice</span><span class="sxs-lookup"><span data-stu-id="5fd75-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="5fd75-111">Voor het ontwikkelen van een Voorspellend model voor kredietrisico, moeten we gegevens die u gebruiken kunt om te trainen en vervolgens het model te testen.</span><span class="sxs-lookup"><span data-stu-id="5fd75-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="5fd75-112">Voor dit scenario gebruiken we 'UCI Statlog (Duitse tegoed gegevens) Data Set' uit de opslagplaats UC Irvine Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5fd75-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="5fd75-113">U kunt deze hier vinden:</span><span class="sxs-lookup"><span data-stu-id="5fd75-113">You can find it here:</span></span>  
<span data-ttu-id="5fd75-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://Archive.ICS.uci.edu/ml/DataSets/Statlog+(German+credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="5fd75-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="5fd75-115">We gebruiken het bestand met de naam **german.data**.</span><span class="sxs-lookup"><span data-stu-id="5fd75-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="5fd75-116">Dit bestand downloaden naar uw lokale vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="5fd75-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="5fd75-117">De **german.data** gegevensset bevat rijen van 20 variabelen voor 1000 afgelopen aanvragers tegoed.</span><span class="sxs-lookup"><span data-stu-id="5fd75-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="5fd75-118">Deze 20 variabelen vertegenwoordigen de gegevensset reeks functies (de *functie vector*), waarmee u identificatiekenmerken op voor elke aanvrager tegoed.</span><span class="sxs-lookup"><span data-stu-id="5fd75-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="5fd75-119">Een extra kolom in elke rij vertegenwoordigt de aanvrager berekende kredietrisico, met 700 aanvrager aangeduid als een lage kredietrisico en 300 als een hoog risico.</span><span class="sxs-lookup"><span data-stu-id="5fd75-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="5fd75-120">De website UCI biedt een beschrijving van de kenmerken van de functie-vector voor deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="5fd75-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="5fd75-121">Dit omvat financiële gegevens, kredietgeschiedenis werkstatus en persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="5fd75-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="5fd75-122">Voor iedere aanvrager een binaire classificatie is opgegeven waarmee wordt aangegeven of ze zich een lage of hoge kredietrisico.</span><span class="sxs-lookup"><span data-stu-id="5fd75-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="5fd75-123">We gebruiken deze gegevens om een predictive analytics-model te trainen.</span><span class="sxs-lookup"><span data-stu-id="5fd75-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="5fd75-124">Als we bent klaar, is het model moet kunnen accepteren van een functie-vector voor een nieuwe afzonderlijke en voorspelt of hij of zij een lage of hoge kredietrisico is.</span><span class="sxs-lookup"><span data-stu-id="5fd75-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="5fd75-125">Hier volgt een interessante twist.</span><span class="sxs-lookup"><span data-stu-id="5fd75-125">Here's an interesting twist.</span></span> <span data-ttu-id="5fd75-126">De beschrijving van de gegevensset op de website UCI noemt wat kost als we iemands kredietrisico misclassify.</span><span class="sxs-lookup"><span data-stu-id="5fd75-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="5fd75-127">Als het model een hoge kredietrisico voor iemand die daadwerkelijk een lage kredietrisico is voorspelt, heeft een misclassification doorgevoerd in het model.</span><span class="sxs-lookup"><span data-stu-id="5fd75-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="5fd75-128">Maar de omgekeerde misclassification vijf keer duurder aan de financiële instelling is: als het model wordt voorspeld een lage kredietrisico voor iemand die daadwerkelijk een hoge kredietrisico is.</span><span class="sxs-lookup"><span data-stu-id="5fd75-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="5fd75-129">Ja, willen we onze model te trainen, zodat de kosten van dit laatste type misclassification vijf keer hoger is dan de andere manier onjuiste.</span><span class="sxs-lookup"><span data-stu-id="5fd75-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="5fd75-130">Een eenvoudige manier om dit te doen bij het trainen van het model in onze experiment is door het dupliceren van (vijfmaal) die items die iemand met een hoge kredietrisico vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="5fd75-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="5fd75-131">Klik, als het model ten onrechte iemand als een lage kredietrisico classificeert wanneer ze daadwerkelijk een hoog risico, het model geen die dezelfde misclassification vijf keer één keer voor elke kopie.</span><span class="sxs-lookup"><span data-stu-id="5fd75-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="5fd75-132">Dit verhoogt de kosten van deze fout in de resultaten training.</span><span class="sxs-lookup"><span data-stu-id="5fd75-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="5fd75-133">De dataset-indeling converteren</span><span class="sxs-lookup"><span data-stu-id="5fd75-133">Convert the dataset format</span></span>
<span data-ttu-id="5fd75-134">De oorspronkelijke gegevensset gebruikt een leeg gescheiden-indeling.</span><span class="sxs-lookup"><span data-stu-id="5fd75-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="5fd75-135">Machine Learning Studio werkt beter met een bestand met door komma's gescheiden waarden (CSV), zodat we de gegevensset converteren moet door spaties vervangen door komma's.</span><span class="sxs-lookup"><span data-stu-id="5fd75-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="5fd75-136">Er zijn veel manieren om deze gegevens te converteren.</span><span class="sxs-lookup"><span data-stu-id="5fd75-136">There are many ways to convert this data.</span></span> <span data-ttu-id="5fd75-137">Een manier is door de volgende Windows PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5fd75-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="5fd75-138">Een andere manier is door de Unix-ype-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5fd75-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="5fd75-139">In beide gevallen is er een door komma's gescheiden versie van de gegevens in een bestand met de naam gemaakt **german.csv** die we in ons experiment kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5fd75-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="5fd75-140">Uploaden van de gegevensset naar Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5fd75-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="5fd75-141">Nadat de gegevens is geconverteerd naar een CSV-indeling, moeten we naar Machine Learning Studio te uploaden.</span><span class="sxs-lookup"><span data-stu-id="5fd75-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="5fd75-142">Open de startpagina van de Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="5fd75-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="5fd75-143">Klik op het menu ![Menu][1] in de linkerbovenhoek van het venster, klikt u op **Azure Machine Learning**, selecteer **Studio**, en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="5fd75-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="5fd75-144">Klik op **+ nieuw** aan de onderkant van het venster.</span><span class="sxs-lookup"><span data-stu-id="5fd75-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="5fd75-145">Selecteer **GEGEVENSSET**.</span><span class="sxs-lookup"><span data-stu-id="5fd75-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="5fd75-146">Selecteer **vanuit het lokale bestand**.</span><span class="sxs-lookup"><span data-stu-id="5fd75-146">Select **FROM LOCAL FILE**.</span></span>

    ![Voeg een gegevensset toe vanuit het lokale bestand][2]

6. <span data-ttu-id="5fd75-148">In de **uploaden van een nieuwe gegevensset** dialoogvenster, klikt u op **Bladeren** en zoek de **german.csv** dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5fd75-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="5fd75-149">Voer een naam voor de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5fd75-149">Enter a name for the dataset.</span></span> <span data-ttu-id="5fd75-150">Voor dit scenario moet aanroepen 'UCI Duits creditcardgegevens'.</span><span class="sxs-lookup"><span data-stu-id="5fd75-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="5fd75-151">Selecteer voor gegevenstype **generieke CSV-bestand met geen koptekst (. nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="5fd75-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="5fd75-152">Een beschrijving toevoegen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="5fd75-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="5fd75-153">Klik op de **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5fd75-153">Click the **OK** check mark.</span></span>  

    ![Uploaden van de gegevensset][3]

<span data-ttu-id="5fd75-155">Dit uploadt u de gegevens in een gegevensset-module die u in een experiment gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="5fd75-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="5fd75-156">U kunt beheren gegevenssets die u naar Studio hebt geüpload door te klikken op de **GEGEVENSSETS** tabblad aan de linkerkant van het venster Studio.</span><span class="sxs-lookup"><span data-stu-id="5fd75-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![Gegevenssets beheren][4]

<span data-ttu-id="5fd75-158">Zie voor meer informatie over het importeren van andere typen gegevens in een experiment [uw trainingsgegevens importeren in Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="5fd75-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="5fd75-159">**Volgende stap: [een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="5fd75-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
