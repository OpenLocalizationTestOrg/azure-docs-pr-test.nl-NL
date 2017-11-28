---
title: 'Stap 3: Maak een nieuwe Machine Learning-experiment | Microsoft Docs'
description: 'Stap 3 van de prognose een voorspellende oplossing overzicht: een nieuw trainingsexperiment maken in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="ae76e-103">Kennismaken, stap 3: Een nieuw Azure Machine Learning-experiment maken</span><span class="sxs-lookup"><span data-stu-id="ae76e-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="ae76e-104">Dit is de derde stap van de procedure [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="ae76e-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="ae76e-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="ae76e-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="ae76e-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="ae76e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="ae76e-107">**Een nieuw experiment maken**</span><span class="sxs-lookup"><span data-stu-id="ae76e-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="ae76e-108">De modellen trainen en evalueren</span><span class="sxs-lookup"><span data-stu-id="ae76e-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="ae76e-109">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="ae76e-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="ae76e-110">Toegang tot de webservice</span><span class="sxs-lookup"><span data-stu-id="ae76e-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="ae76e-111">De volgende stap in dit scenario is het maken van een experiment in Machine Learning Studio die gebruikmaakt van de gegevensset die wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="ae76e-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="ae76e-112">Klik in Studio **+ nieuw** aan de onderkant van het venster.</span><span class="sxs-lookup"><span data-stu-id="ae76e-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="ae76e-113">Selecteer **EXPERIMENT**, en selecteer vervolgens 'Leeg Experiment'.</span><span class="sxs-lookup"><span data-stu-id="ae76e-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Een nieuw experiment maken][0]

2. <span data-ttu-id="ae76e-115">Selecteer de naam van de standaard-experiment aan de bovenkant van het canvas en herkenbare naam.</span><span class="sxs-lookup"><span data-stu-id="ae76e-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Wijzig de naam van experiment][5]
   
   > [!TIP]
   > <span data-ttu-id="ae76e-117">Het is raadzaam om in te vullen **samenvatting** en **beschrijving** voor het experiment in de **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="ae76e-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="ae76e-118">Deze eigenschappen kunnen u de kans op het experiment documenteren, zodat iedereen die deze later wordt uw doelen en methodologie begrijpen.</span><span class="sxs-lookup"><span data-stu-id="ae76e-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Experiment eigenschappen][6]
   > 
3. <span data-ttu-id="ae76e-120">Vouw in het modulepalet links van het experimentcanvas **gegevenssets opgeslagen**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="ae76e-121">Zoek de gegevensset die u hebt gemaakt onder **mijn gegevenssets** en sleep deze naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="ae76e-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="ae76e-122">U kunt de gegevensset ook vinden door de naam in te voeren de **Search** vak boven het palet.</span><span class="sxs-lookup"><span data-stu-id="ae76e-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![De gegevensset naar het experimentcanvas toevoegen][7]

## <a name="prepare-the-data"></a><span data-ttu-id="ae76e-124">De gegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="ae76e-124">Prepare the data</span></span>
<span data-ttu-id="ae76e-125">U kunt de eerste 100 rijen van de gegevens en enkele statische gegevens voor de volledige gegevensset bekijken: klik op de uitvoerpoort van de gegevensset (kleine cirkel onderaan) en selecteer **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="ae76e-126">Omdat het bestand niet is meegeleverd met kolomkoppen, Studio algemene koppen is opgegeven (Col1, Col2, *enzovoort*).</span><span class="sxs-lookup"><span data-stu-id="ae76e-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="ae76e-127">Goede koppen niet essentieel is voor het maken van een model, maar ze gemakkelijker te werken met de gegevens in het experiment.</span><span class="sxs-lookup"><span data-stu-id="ae76e-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="ae76e-128">Ook als we uiteindelijk dit model in een webservice publiceren, de koppen helpen bij het identificeren van de kolommen voor de gebruiker van de service.</span><span class="sxs-lookup"><span data-stu-id="ae76e-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="ae76e-129">We kunt toevoegen met behulp van kolomkoppen de [metagegevens bewerken] [ edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="ae76e-130">U gebruikt de [metagegevens bewerken] [ edit-metadata] module die u wilt wijzigen van de metagegevens gekoppeld aan een dataset.</span><span class="sxs-lookup"><span data-stu-id="ae76e-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="ae76e-131">In dit geval gebruiken we het meer beschrijvende namen voor kolomkoppen op te geven.</span><span class="sxs-lookup"><span data-stu-id="ae76e-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="ae76e-132">Gebruik [metagegevens bewerken][edit-metadata], geeft u eerst welke kolommen te wijzigen (in dit geval ze allemaal.) Geef vervolgens de actie die moet worden uitgevoerd op deze kolommen (in dit geval kolomkoppen te wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="ae76e-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="ae76e-133">Typ in het modulepalet 'metagegevens' in de **Search** vak.</span><span class="sxs-lookup"><span data-stu-id="ae76e-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="ae76e-134">De [metagegevens bewerken] [ edit-metadata] wordt weergegeven in de modulelijst.</span><span class="sxs-lookup"><span data-stu-id="ae76e-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="ae76e-135">Klik en sleep de [metagegevens bewerken] [ edit-metadata] module naar het canvas en zet deze neer onder de gegevensset die we eerder hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ae76e-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="ae76e-136">Verbinding maken met de gegevensset naar de [metagegevens bewerken][edit-metadata]: klik op de uitvoerpoort van de gegevensset (kleine cirkel aan de onderkant van de gegevensset), sleept u naar de invoer-poort van [metagegevens bewerken] [ edit-metadata] (de kleine cirkel aan de bovenkant van de module), klikt u vervolgens de muisknop loslaat.</span><span class="sxs-lookup"><span data-stu-id="ae76e-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="ae76e-137">De module en gegevensset blijven verbonden, zelfs als u ofwel op het canvas verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="ae76e-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="ae76e-138">Het experiment moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="ae76e-138">The experiment should now look something like this:</span></span>  
   
   ![Metagegevens bewerken][1]
   
   <span data-ttu-id="ae76e-140">Rood uitroepteken geeft aan dat we de eigenschappen voor deze module nog niet hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ae76e-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="ae76e-141">We doen om het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ae76e-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ae76e-142">U kunt een opmerking aan een module toevoegen door te dubbelklikken op de module en tekst in te voeren.</span><span class="sxs-lookup"><span data-stu-id="ae76e-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="ae76e-143">Zodoende kunt u in één oogopslag zien wat de module in uw experiment doet.</span><span class="sxs-lookup"><span data-stu-id="ae76e-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="ae76e-144">In dit geval, dubbelklikt u op de [metagegevens bewerken] [ edit-metadata] module en typ de opmerking 'Add kolomkoppen'.</span><span class="sxs-lookup"><span data-stu-id="ae76e-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="ae76e-145">Klik ergens anders op het canvas te sluiten van het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="ae76e-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="ae76e-146">De opmerking, klikt u op de pijl-omlaag in de module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Metagegevens module bewerken met opmerkingen toegevoegd][8]
   > 
4. <span data-ttu-id="ae76e-148">Selecteer [metagegevens bewerken][edit-metadata], en in de **eigenschappen** deelvenster rechts van het canvas te klikken op **Launch column selector**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="ae76e-149">In de **kolommen selecteren** dialoogvenster, selecteer de rijen in **beschikbare kolommen** en klik op > te verplaatsen naar **geselecteerde kolommen**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="ae76e-150">Het dialoogvenster ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="ae76e-150">The dialog should look like this:</span></span>

   ![Kolomkiezer met alle kolommen geselecteerd][2]

6. <span data-ttu-id="ae76e-152">Klik op de **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ae76e-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="ae76e-153">Terug in de **eigenschappen** deelvenster, zoek de **nieuwe kolomnamen** parameter.</span><span class="sxs-lookup"><span data-stu-id="ae76e-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="ae76e-154">Geef een lijst met namen van de 21 kolommen in de gegevensset, gescheiden door komma's en in de volgorde van kolommen in dit veld.</span><span class="sxs-lookup"><span data-stu-id="ae76e-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="ae76e-155">U kunt de namen van kolommen uit de dataset-documentatie op de website UCI verkrijgen of voor uw gemak bedoeld; u kunt kopiëren en plakken van de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="ae76e-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="ae76e-156">Het deelvenster Eigenschappen ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="ae76e-156">The Properties pane looks like this:</span></span>
   
   ![Eigenschappen voor metagegevens bewerken][3]

> [!TIP]
> <span data-ttu-id="ae76e-158">Als u controleren of de kolomkoppen wilt, voer het experiment (Klik op **uitvoeren** onder het experimentcanvas).</span><span class="sxs-lookup"><span data-stu-id="ae76e-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="ae76e-159">Wanneer deze is voltooid (Er verschijnt een groen vinkje op [metagegevens bewerken][edit-metadata]), klikt u op de uitvoerpoort van de [metagegevens bewerken] [ edit-metadata] module en selecteer **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="ae76e-160">U kunt de uitvoer van elke module weergeven op dezelfde manier om de voortgang van de gegevens via het experiment weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ae76e-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="ae76e-161">Training maken en testen van gegevenssets</span><span class="sxs-lookup"><span data-stu-id="ae76e-161">Create training and test datasets</span></span>
<span data-ttu-id="ae76e-162">We moeten sommige gegevens aan het model trainen en sommige te testen.</span><span class="sxs-lookup"><span data-stu-id="ae76e-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="ae76e-163">Dus in de volgende stap van het experiment we de gegevensset in twee afzonderlijke gegevenssets splitsen: één voor het trainen van het model en één voor het testen van het.</span><span class="sxs-lookup"><span data-stu-id="ae76e-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="ae76e-164">Om dit te doen, gebruiken we de [Split Data] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="ae76e-165">Zoek de [Split Data] [ split] module, sleep deze naar het canvas en verbindt deze met de [metagegevens bewerken] [ edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="ae76e-166">Standaard is de verhouding tussen het gesplitste 0,5 en de **Randomized gesplitste** parameter is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ae76e-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="ae76e-167">Dit betekent dat een willekeurige helft van de gegevens uitgevoerd via één poort van wordt de [Split Data] [ split] -module en de helft via de andere.</span><span class="sxs-lookup"><span data-stu-id="ae76e-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="ae76e-168">U kunt deze parameters aanpassen, evenals de **willekeurige seed** parameter wijzigen van de scheiding tussen trainings- en testdoeleinden gegevens.</span><span class="sxs-lookup"><span data-stu-id="ae76e-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="ae76e-169">In dit voorbeeld laat we ze-is.</span><span class="sxs-lookup"><span data-stu-id="ae76e-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ae76e-170">De eigenschap **fractie van rijen in de eerste uitvoergegevensset** bepaalt hoeveel van de gegevens is de uitvoer via de *links* uitvoerpoort.</span><span class="sxs-lookup"><span data-stu-id="ae76e-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="ae76e-171">Bijvoorbeeld als u de verhouding tussen 0,7 instelt, is 70% van de gegevens uitvoer via de poort van de linker- en 30% tot en met de juiste poort.</span><span class="sxs-lookup"><span data-stu-id="ae76e-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="ae76e-172">Dubbelklik op de [Split Data] [ split] module en de opmerking invoeren, ' Training/testen gegevens splitsen 50% '.</span><span class="sxs-lookup"><span data-stu-id="ae76e-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="ae76e-173">Kunnen we gebruiken de uitvoer van de [Split Data] [ split] module echter we graag, maar we Kies moet de uitvoer van de linker trainingsgegevens en het recht uitvoergegevens als testen.</span><span class="sxs-lookup"><span data-stu-id="ae76e-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="ae76e-174">Zoals vermeld in de [vorige stap](machine-learning-walkthrough-2-upload-data.md), de kosten van een hoge kredietrisico als laag onjuiste vijf keer hoger dan de kosten van het onjuiste een lage kredietrisico zo hoog is.</span><span class="sxs-lookup"><span data-stu-id="ae76e-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="ae76e-175">Als u wilt voor dit account, moet er een nieuwe gegevensset die overeenkomt met deze functie kosten gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ae76e-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="ae76e-176">In de nieuwe gegevensset, elk met een hoog risico voorbeeld vijf keer gerepliceerd terwijl elke laag risico voorbeeld niet is gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="ae76e-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="ae76e-177">We kunnen deze replicatie doen met behulp van R-code:</span><span class="sxs-lookup"><span data-stu-id="ae76e-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="ae76e-178">Zoek en sleep de [R-Script uitvoeren] [ execute-r-script] module naar het experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="ae76e-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="ae76e-179">Verbinding maken met de uitvoerpoort links van de [Split Data] [ split] module aan de eerste invoer poort ('Dataset1') van de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="ae76e-180">Dubbelklik op de [R-Script uitvoeren] [ execute-r-script] module en voer de opmerking 'Instellen kosten aanpassing'.</span><span class="sxs-lookup"><span data-stu-id="ae76e-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="ae76e-181">In de **eigenschappen** deelvenster, verwijdert u de standaardtekst in de **R-Script** parameter en voer dit script:</span><span class="sxs-lookup"><span data-stu-id="ae76e-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R-script in de module R-Script uitvoeren][9]

<span data-ttu-id="ae76e-183">We moeten doen deze dezelfde replicatiebewerking voor elke uitvoer van de [Split Data] [ split] module zodat de training en testen gegevens de dezelfde aanpassing van de kosten hebben.</span><span class="sxs-lookup"><span data-stu-id="ae76e-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="ae76e-184">De eenvoudigste manier om dit te doen is door het dupliceren van de [R-Script uitvoeren] [ execute-r-script] module die we zojuist hebt gemaakt en verbinding maken met de andere uitvoerpoort van de [Split Data] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="ae76e-185">Met de rechtermuisknop op de [R-Script uitvoeren] [ execute-r-script] module en selecteer **kopie**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="ae76e-186">Met de rechtermuisknop op het experimentcanvas en selecteer **plakken**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="ae76e-187">De nieuwe module naar positie slepen en sluit vervolgens de juiste uitvoerpoort van de [Split Data] [ split] module die u wilt de eerste invoerpoort van deze nieuwe [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="ae76e-188">Klik aan de onderkant van het canvas op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ae76e-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="ae76e-189">De kopie van de module R-Script uitvoeren bevat hetzelfde script als de oorspronkelijke module.</span><span class="sxs-lookup"><span data-stu-id="ae76e-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="ae76e-190">Wanneer u kopieert en plakt een module op het canvas, behoudt de kopie de eigenschappen van het origineel.</span><span class="sxs-lookup"><span data-stu-id="ae76e-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="ae76e-191">Onze experiment ziet nu er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="ae76e-191">Our experiment now looks something like this:</span></span>

![Split-module en R scripts toe te voegen][4]

<span data-ttu-id="ae76e-193">Zie voor meer informatie over het gebruik van R-scripts in uw experimenten [uw experiment uitbreiden met R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="ae76e-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="ae76e-194">**Volgende stap: [trainen en evalueren van de modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="ae76e-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
