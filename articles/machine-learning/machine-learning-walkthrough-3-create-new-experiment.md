---
title: 'Stap 3: Maak een nieuwe Machine Learning-experiment | Microsoft Docs'
description: 'Stap 3 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: een nieuw trainingsexperiment maken in Azure Machine Learning Studio.'
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
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="a0853-103">Kennismaken, stap 3: Een nieuw Azure Machine Learning-experiment maken</span><span class="sxs-lookup"><span data-stu-id="a0853-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="a0853-104">Dit is de derde stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a0853-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a0853-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="a0853-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="a0853-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="a0853-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="a0853-107">**Een nieuw experiment maken**</span><span class="sxs-lookup"><span data-stu-id="a0853-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="a0853-108">Trainen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="a0853-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a0853-109">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="a0853-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a0853-110">Toegang tot Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="a0853-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a0853-111">Hallo volgende stap in dit scenario is toocreate een experiment in Machine Learning Studio die gebruikmaakt van Hallo gegevensset die wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="a0853-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="a0853-112">Klik in Studio **+ nieuw** onderaan Hallo Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="a0853-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="a0853-113">Selecteer **EXPERIMENT**, en selecteer vervolgens 'Leeg Experiment'.</span><span class="sxs-lookup"><span data-stu-id="a0853-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Een nieuw experiment maken][0]

2. <span data-ttu-id="a0853-115">Selecteer Hallo standaard naam Hallo boven aan het papier Hallo experiment en wijzig deze toosomething zinvolle.</span><span class="sxs-lookup"><span data-stu-id="a0853-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Wijzig de naam van experiment][5]
   
   > [!TIP]
   > <span data-ttu-id="a0853-117">Het is een goede gewoonte toofill in **samenvatting** en **beschrijving** voor Hallo experiment in Hallo **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="a0853-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="a0853-118">Deze eigenschappen kunt u kans toodocument Hallo experiment hello, zodat iedereen die deze later wordt uw doelen en methodologie begrijpen.</span><span class="sxs-lookup"><span data-stu-id="a0853-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Experiment eigenschappen][6]
   > 
3. <span data-ttu-id="a0853-120">Vouw in het Hallo-module palet toohello links van het experimentcanvas hello **gegevenssets opgeslagen**.</span><span class="sxs-lookup"><span data-stu-id="a0853-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="a0853-121">Zoeken naar Hallo gegevensset die u hebt gemaakt onder **mijn gegevenssets** en sleep deze naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="a0853-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="a0853-122">U vindt ook Hallo gegevensset Hallo naam door in te voeren Hallo **Search** vak boven Hallo palet.</span><span class="sxs-lookup"><span data-stu-id="a0853-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Hallo gegevensset toohello experiment toevoegen][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="a0853-124">Hallo gegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a0853-124">Prepare hello data</span></span>
<span data-ttu-id="a0853-125">U kunt weergeven eerste 100 rijen Hallo gegevens en enkele statische gegevens voor de volledige gegevensset Hallo Hallo: klik op de uitvoerpoort Hallo van Hallo gegevensset (Hallo kleine cirkel Hallo onderin) en selecteer **visualiseren**.</span><span class="sxs-lookup"><span data-stu-id="a0853-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="a0853-126">Omdat het gegevensbestand Hallo niet meegeleverd met kolomkoppen, Studio algemene koppen is opgegeven (Col1, Col2, *enzovoort*).</span><span class="sxs-lookup"><span data-stu-id="a0853-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="a0853-127">Goede koppen niet essentieel toocreating een model, maar ze eenvoudiger eenvoudiger toowork met Hallo gegevens in Hallo-experiment.</span><span class="sxs-lookup"><span data-stu-id="a0853-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="a0853-128">Ook wanneer we dit model uiteindelijk in een webservice publiceren, Hallo koppen te identificeren Hallo kolommen toohello gebruiker van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="a0853-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="a0853-129">We kunt toevoegen met behulp van Hallo kolomkoppen [metagegevens bewerken] [ edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="a0853-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="a0853-130">Gebruik van Hallo [metagegevens bewerken] [ edit-metadata] module toochange metagegevens gekoppeld aan een dataset.</span><span class="sxs-lookup"><span data-stu-id="a0853-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="a0853-131">In dit geval we gebruiken deze tooprovide meer beschrijvende namen voor kolomkoppen.</span><span class="sxs-lookup"><span data-stu-id="a0853-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="a0853-132">toouse [metagegevens bewerken][edit-metadata], u eerst een opgeven welke kolommen toomodify (in dit geval ze allemaal.) Geef vervolgens Hallo actie toobe uitgevoerd op deze kolommen (in dit geval kolomkoppen te wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="a0853-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="a0853-133">Typ in het modulepalet hello, 'metagegevens' in hello **Search** vak.</span><span class="sxs-lookup"><span data-stu-id="a0853-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="a0853-134">Hallo [metagegevens bewerken] [ edit-metadata] wordt weergegeven in de modulelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0853-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="a0853-135">Klik en sleep Hallo [metagegevens bewerken] [ edit-metadata] module op Hallo canvas en zet deze neer hieronder Hallo gegevensset we die eerder is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a0853-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="a0853-136">Verbinding maken met de Hallo gegevensset toohello [metagegevens bewerken][edit-metadata]: klikt u op de uitvoerpoort Hallo Hallo gegevensset (Hallo kleine cirkel onderaan Hallo Hallo gegevensset), sleep toohello invoerpoort van [metagegevens bewerken ] [ edit-metadata] (Hallo kleine cirkel Hallo boven aan het Hallo-module), laat u Hallo muisknop los.</span><span class="sxs-lookup"><span data-stu-id="a0853-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="a0853-137">Hallo gegevensset en module blijven verbonden, zelfs als u ofwel op Hallo canvas verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="a0853-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="a0853-138">Hallo-experiment moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="a0853-138">hello experiment should now look something like this:</span></span>  
   
   ![Metagegevens bewerken][1]
   
   <span data-ttu-id="a0853-140">Hallo rood uitroepteken geeft aan we Hallo-eigenschappen voor deze module nog niet hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a0853-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="a0853-141">We doen om het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0853-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a0853-142">U kunt een opmerking tooa module door te dubbelklikken op Hallo-module en tekstinvoer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0853-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="a0853-143">Hiermee kunt u in één oogopslag zien welke Hallo-module in uw experiment doet.</span><span class="sxs-lookup"><span data-stu-id="a0853-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="a0853-144">Dubbelklik in dit geval op Hallo [metagegevens bewerken] [ edit-metadata] module en type Hallo Opmerking 'Add kolomkoppen'.</span><span class="sxs-lookup"><span data-stu-id="a0853-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="a0853-145">Klik ergens anders op Hallo canvas tooclose Hallo-tekstvak.</span><span class="sxs-lookup"><span data-stu-id="a0853-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="a0853-146">toodisplay Opmerking hello, klikt u op Hallo pijl-omlaag op het Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="a0853-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Metagegevens module bewerken met opmerkingen toegevoegd][8]
   > 
4. <span data-ttu-id="a0853-148">Selecteer [metagegevens bewerken][edit-metadata], en in Hallo **eigenschappen** deelvenster toohello rechts van het canvas hello, klikt u op **Launch column selector**.</span><span class="sxs-lookup"><span data-stu-id="a0853-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="a0853-149">In Hallo **kolommen selecteren** dialoogvenster, selecteer alle rijen in Hallo **beschikbare kolommen** en klik op > toomove ze te**geselecteerde kolommen**.</span><span class="sxs-lookup"><span data-stu-id="a0853-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="a0853-150">Hallo dialoogvenster ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="a0853-150">hello dialog should look like this:</span></span>

   ![Kolomkiezer met alle kolommen geselecteerd][2]

6. <span data-ttu-id="a0853-152">Klik op Hallo **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a0853-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="a0853-153">Terug in Hallo **eigenschappen** deelvenster, zoek Hallo **nieuwe kolomnamen** parameter.</span><span class="sxs-lookup"><span data-stu-id="a0853-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="a0853-154">Geef een lijst met namen voor Hallo 21 kolommen in de gegevensset hello, gescheiden door komma's en in de volgorde van kolommen in dit veld.</span><span class="sxs-lookup"><span data-stu-id="a0853-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="a0853-155">U kunt Hallo kolommen namen ophalen Hallo gegevensset documentatie op Hallo UCI website of voor het gemak kunt u kopiëren en plakken Hallo lijst na:</span><span class="sxs-lookup"><span data-stu-id="a0853-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="a0853-156">Hallo eigenschappendeelvenster ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="a0853-156">hello Properties pane looks like this:</span></span>
   
   ![Eigenschappen voor metagegevens bewerken][3]

> [!TIP]
> <span data-ttu-id="a0853-158">Als u tooverify Hallo kolomkoppen wilt, Hallo experiment uitvoeren (Klik op **uitvoeren** onder het experimentcanvas Hallo).</span><span class="sxs-lookup"><span data-stu-id="a0853-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="a0853-159">Wanneer deze is voltooid (Er verschijnt een groen vinkje op [metagegevens bewerken][edit-metadata]), klikt u op de uitvoerpoort Hallo Hallo [metagegevens bewerken] [ edit-metadata] module en selecteer **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="a0853-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="a0853-160">U kunt Hallo-uitvoer van elke module weergeven in Hallo dezelfde manier tooview Hallo voortgang van Hallo gegevens via Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="a0853-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="a0853-161">Training maken en testen van gegevenssets</span><span class="sxs-lookup"><span data-stu-id="a0853-161">Create training and test datasets</span></span>
<span data-ttu-id="a0853-162">Sommige gegevens tootrain Hallo-model en sommige tootest moet het.</span><span class="sxs-lookup"><span data-stu-id="a0853-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="a0853-163">Dus in de volgende stap Hallo van Hallo experiment, we Hallo gegevensset in twee afzonderlijke gegevenssets splitsen: één voor het trainen van het model en één voor het testen van het.</span><span class="sxs-lookup"><span data-stu-id="a0853-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="a0853-164">toodo, gebruiken we Hallo [Split Data] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="a0853-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="a0853-165">Hallo zoeken [Split Data] [ split] -module, sleep deze naar Hallo canvas en verbindt u deze toohello [metagegevens bewerken] [ edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="a0853-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="a0853-166">Hallo gesplitste verhouding is standaard 0,5 en Hallo **Randomized gesplitste** parameter is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a0853-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="a0853-167">Dit betekent dat een willekeurige helft van Hallo gegevens uitgevoerd via één poort Hallo wordt [Split Data] [ split] -module en de helft via Hallo andere.</span><span class="sxs-lookup"><span data-stu-id="a0853-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="a0853-168">U kunt deze parameters aanpassen, evenals Hallo **willekeurige seed** parameter toochange Hallo verdeeld over de trainings- en testdoeleinden gegevens.</span><span class="sxs-lookup"><span data-stu-id="a0853-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="a0853-169">In dit voorbeeld laat we ze-is.</span><span class="sxs-lookup"><span data-stu-id="a0853-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a0853-170">eigenschap Hallo **fractie van rijen in Hallo eerst uitvoergegevensset** bepaalt hoeveel gegevens Hallo uitvoer via Hallo *links* uitvoerpoort.</span><span class="sxs-lookup"><span data-stu-id="a0853-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="a0853-171">Bijvoorbeeld als u Hallo verhouding too0.7 instelt, wordt vervolgens 70% van Hallo gegevens uitgevoerd via de poort en 30% links via de juiste poort Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0853-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="a0853-172">Dubbelklik op Hallo [Split Data] [ split] module en Hallo opmerking invoeren, ' Training/testen gegevens splitsen 50% '.</span><span class="sxs-lookup"><span data-stu-id="a0853-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="a0853-173">We kunnen Hallo uitvoerwaarden van hello gebruiken [Split Data] [ split] module echter we graag, maar we kiezen toouse Hallo links uitvoer als trainingsgegevens en Hallo rechts als testen uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="a0853-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="a0853-174">Zoals vermeld in Hallo [vorige stap](machine-learning-walkthrough-2-upload-data.md), Hallo kosten van een hoge kredietrisico als laag onjuiste vijf keer hoger is dan Hallo kosten van het onjuiste een lage kredietrisico zo hoog.</span><span class="sxs-lookup"><span data-stu-id="a0853-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="a0853-175">tooaccount voor dit dat er een nieuwe gegevensset die overeenkomt met deze functie kosten gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a0853-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="a0853-176">In de nieuwe gegevensset Hallo, elk met een hoog risico voorbeeld vijf keer gerepliceerd terwijl elke laag risico voorbeeld niet is gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="a0853-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="a0853-177">We kunnen deze replicatie doen met behulp van R-code:</span><span class="sxs-lookup"><span data-stu-id="a0853-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="a0853-178">Zoek en sleep Hallo [R-Script uitvoeren] [ execute-r-script] module naar het experimentcanvas Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0853-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="a0853-179">Hallo links uitvoerpoort Hallo verbinding [Split Data] [ split] poort ('Dataset1') module toohello eerste invoer Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="a0853-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="a0853-180">Dubbelklik op Hallo [R-Script uitvoeren] [ execute-r-script] module en Voer Hallo-Opmerking 'Instellen kosten aanpassing'.</span><span class="sxs-lookup"><span data-stu-id="a0853-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="a0853-181">In Hallo **eigenschappen** deelvenster verwijderen Hallo standaardtekst in Hallo **R-Script** parameter en voer dit script:</span><span class="sxs-lookup"><span data-stu-id="a0853-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R-script module Hallo R-Script uitvoeren][9]

<span data-ttu-id="a0853-183">Deze dezelfde replicatiebewerking voor elke uitvoer Hallo toodo moet [Split Data] [ split] module zodat deze Hallo trainings- en testdoeleinden gegevens hebben dezelfde Hallo kosten aanpassing.</span><span class="sxs-lookup"><span data-stu-id="a0853-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="a0853-184">Hallo gemakkelijkste manier toodo dit is de Hallo dupliceren [R-Script uitvoeren] [ execute-r-script] module we zojuist hebt gemaakt en dit toohello verbindt ander uitvoer poort Hallo [Split Data] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="a0853-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="a0853-185">Klik met de rechtermuisknop Hallo [R-Script uitvoeren] [ execute-r-script] module en selecteer **kopie**.</span><span class="sxs-lookup"><span data-stu-id="a0853-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="a0853-186">Met de rechtermuisknop op het experimentcanvas hello en selecteer **plakken**.</span><span class="sxs-lookup"><span data-stu-id="a0853-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="a0853-187">Hallo nieuwe module naar positie slepen en sluit vervolgens de juiste uitvoerpoort Hallo Hallo [Split Data] [ split] eerste invoer-poort van dit nieuwe module toohello [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="a0853-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="a0853-188">Klik onder Hallo Hallo canvas op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="a0853-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="a0853-189">Hallo-exemplaar van Hallo R-Script niet uitvoeren-module bevat Hallo dezelfde als de oorspronkelijke module Hallo script.</span><span class="sxs-lookup"><span data-stu-id="a0853-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="a0853-190">Wanneer u kopieert en plakt een module op Hallo canvas, behoudt Hallo kopiëren alle Hallo-eigenschappen van het oorspronkelijke Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0853-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="a0853-191">Onze experiment ziet nu er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="a0853-191">Our experiment now looks something like this:</span></span>

![Split-module en R scripts toe te voegen][4]

<span data-ttu-id="a0853-193">Zie voor meer informatie over het gebruik van R-scripts in uw experimenten [uw experiment uitbreiden met R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="a0853-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="a0853-194">**Volgende stap: [trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="a0853-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
