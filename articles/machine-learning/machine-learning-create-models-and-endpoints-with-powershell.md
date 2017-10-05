---
title: Meerdere modellen maken op basis van een experiment | Microsoft Docs
description: PowerShell gebruiken voor het maken van meerdere Machine Learning-modellen en web-service-eindpunten met dezelfde algoritme, maar met verschillende training gegevenssets.
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 21d8c1ee0877df8d317d5a14131dc574fa5303c4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="e8224-103">Veel Machine Learning-modellen en webservice-eindpunten maken van een experiment met PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8224-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="e8224-104">Hier volgt een veelvoorkomend probleem van machine learning: U wilt maken van veel modellen die dezelfde werkstroom training hebben en dezelfde algoritme gebruiken, maar verschillende training gegevenssets als invoer.</span><span class="sxs-lookup"><span data-stu-id="e8224-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="e8224-105">In dit artikel leest u hoe u dit doet op grote schaal in Azure Machine Learning Studio met behulp van slechts een enkele experiment.</span><span class="sxs-lookup"><span data-stu-id="e8224-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="e8224-106">Stel dat u een globale fiets verhuur franchiseonderneming bedrijf bezit.</span><span class="sxs-lookup"><span data-stu-id="e8224-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="e8224-107">U wilt maken van een regressiemodel om te voorspellen van de vraag verhuur is gebaseerd op historische gegevens.</span><span class="sxs-lookup"><span data-stu-id="e8224-107">You want to build a regression model to predict the rental demand based on historic data.</span></span> <span data-ttu-id="e8224-108">Hebt u 1000 verhuur locaties overal ter wereld en u een gegevensset voor elke locatie met belangrijke functies zoals datum, tijd, weer en verkeer die specifiek zijn voor elke locatie hebt verzameld.</span><span class="sxs-lookup"><span data-stu-id="e8224-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span></span>

<span data-ttu-id="e8224-109">U kunt het model met één keer een samengevoegde versie van alle gegevenssets op alle locaties kan trainen.</span><span class="sxs-lookup"><span data-stu-id="e8224-109">You could train your model once using a merged version of all the datasets across all locations.</span></span> <span data-ttu-id="e8224-110">Maar omdat elk van de locaties van een unieke omgeving heeft, wordt een betere benadering voor het trainen van uw regressiemodel afzonderlijk met behulp van de gegevensset voor elke locatie.</span><span class="sxs-lookup"><span data-stu-id="e8224-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span></span> <span data-ttu-id="e8224-111">Op die manier elk getraind model kan rekening gehouden met de grootte van andere archieven, volume, Geografie, populatie, fiets-vriendelijk verkeer-omgeving, *enzovoort*.</span><span class="sxs-lookup"><span data-stu-id="e8224-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="e8224-112">Die de aanbevolen aanpak mogelijk, maar u niet wilt 1000 training experimenten maken in Azure Machine Learning met elkaar die een unieke locatie voorstelt.</span><span class="sxs-lookup"><span data-stu-id="e8224-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="e8224-113">Behalve dat een enigszins overweldigend taak, het is ook heel inefficiënt lijkt omdat elk experiment allemaal dezelfde onderdelen, met uitzondering van de gegevensset training hebben zou.</span><span class="sxs-lookup"><span data-stu-id="e8224-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span></span>

<span data-ttu-id="e8224-114">Gelukkig kan dit worden bereikt met behulp van de [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) en het automatiseren van de taak met [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="e8224-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e8224-115">Als u ons voorbeeld sneller worden uitgevoerd, verlagen we het aantal locaties van 1000 tot en met 10.</span><span class="sxs-lookup"><span data-stu-id="e8224-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span></span> <span data-ttu-id="e8224-116">Maar de beginselen en de procedures van toepassing op 1000 locaties.</span><span class="sxs-lookup"><span data-stu-id="e8224-116">But the same principles and procedures apply to 1,000 locations.</span></span> <span data-ttu-id="e8224-117">Het enige verschil is dat als u wilt trainen van 1000 gegevenssets u waarschijnlijk zien wilt met de volgende PowerShell-scripts in parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8224-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span></span> <span data-ttu-id="e8224-118">Hoe dat valt buiten het bereik van dit artikel, maar u voorbeelden van PowerShell multithreading kunt vinden op het Internet.</span><span class="sxs-lookup"><span data-stu-id="e8224-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span></span>  
> 
> 

## <a name="set-up-the-training-experiment"></a><span data-ttu-id="e8224-119">Het trainingsexperiment instellen</span><span class="sxs-lookup"><span data-stu-id="e8224-119">Set up the training experiment</span></span>
<span data-ttu-id="e8224-120">We gaan een voorbeeld gebruiken [trainingsexperiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) die we al hebt gemaakt in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="e8224-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="e8224-121">Open dit experiment in uw [Azure Machine Learning Studio](https://studio.azureml.net) werkruimte.</span><span class="sxs-lookup"><span data-stu-id="e8224-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="e8224-122">Om te kunnen volgen samen met het volgende voorbeeld, kan u wilt gebruiken in een standaard werkruimte in plaats van een gratis werkruimte.</span><span class="sxs-lookup"><span data-stu-id="e8224-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="e8224-123">We één eindpunt maakt voor elke klant - voor een totaal van 10 eindpunten - en waarvoor u een standaard werkruimte omdat een gratis werkruimte beperkt tot 3-eindpunten is.</span><span class="sxs-lookup"><span data-stu-id="e8224-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span></span> <span data-ttu-id="e8224-124">Als u alleen een gratis werkruimte hebt, alleen de onderstaande om toe te staan voor slechts 3 locaties scripts te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e8224-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="e8224-125">Het experiment wordt gebruikgemaakt van een **gegevens importeren** module voor het importeren van de gegevensset training *customer001.csv* van een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8224-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="e8224-126">Stel hebben we training gegevenssets van alle fiets verhuur locaties verzameld en opgeslagen in dezelfde locatie voor de blob-opslag met bestandsnamen, variërend van *rentalloc001.csv* naar *rentalloc10.csv*.</span><span class="sxs-lookup"><span data-stu-id="e8224-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span></span>

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="e8224-128">Houd er rekening mee dat een **Web Service uitvoer** module is toegevoegd aan de **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="e8224-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span></span>
<span data-ttu-id="e8224-129">Wanneer dit experiment wordt geïmplementeerd als een webservice, het eindpunt gekoppeld dat uitvoer het getrainde model wordt geretourneerd in de indeling van een bestand .ilearner.</span><span class="sxs-lookup"><span data-stu-id="e8224-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span></span>

<span data-ttu-id="e8224-130">Ook de opmerking die we een web service-parameter voor de URL ingesteld die de **importgegevens** module wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e8224-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span></span> <span data-ttu-id="e8224-131">Deze manier kunnen wij gebruiken de parameter om op te geven van individuele training gegevenssets trainen van het model voor elke locatie.</span><span class="sxs-lookup"><span data-stu-id="e8224-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span></span>
<span data-ttu-id="e8224-132">Er zijn andere manieren we kunnen dit hebt gedaan, zoals een SQL-query om gegevens te verkrijgen uit een Azure SQL database met de parameter voor een web-service of te gebruiken om een **Web Service invoer** module die u wilt doorgeven in een gegevensset met de webservice.</span><span class="sxs-lookup"><span data-stu-id="e8224-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span></span>

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="e8224-134">Nu gaan we deze trainingsexperiment met behulp van de standaardwaarde uitvoeren *rental001.csv* als de training-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e8224-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span></span> <span data-ttu-id="e8224-135">Als u de uitvoer van de **Evaluate** module (Klik op de uitvoer en selecteer **Visualize**), kunt u zien krijgen we een goede prestaties van *AUC* 0.91 =.</span><span class="sxs-lookup"><span data-stu-id="e8224-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="e8224-136">Op dit moment kunt u een webservice buiten dit trainingsexperiment implementeren.</span><span class="sxs-lookup"><span data-stu-id="e8224-136">At this point, we're ready to deploy a web service out of this training experiment.</span></span>

## <a name="deploy-the-training-and-scoring-web-services"></a><span data-ttu-id="e8224-137">De training en score berekenen voor webservices implementeren</span><span class="sxs-lookup"><span data-stu-id="e8224-137">Deploy the training and scoring web services</span></span>
<span data-ttu-id="e8224-138">Voor het implementeren van de webservice voor training, klikt u op de **webservice ingesteld** onder het experimentcanvas en selecteer **webservice implementeren**.</span><span class="sxs-lookup"><span data-stu-id="e8224-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="e8224-139">Roep deze webservice '' fiets verhuur Training'.</span><span class="sxs-lookup"><span data-stu-id="e8224-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="e8224-140">Nu moet de score webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="e8224-140">Now we need to deploy the scoring web service.</span></span>
<span data-ttu-id="e8224-141">Hiertoe klikt raadzaam **webservice ingesteld** onder het canvas en selecteer **voorspellende webservice**.</span><span class="sxs-lookup"><span data-stu-id="e8224-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="e8224-142">Hiermee maakt u een score experiment.</span><span class="sxs-lookup"><span data-stu-id="e8224-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="e8224-143">We hebben enkele kleine wijzigingen aanbrengen in deze werken als een webservice, zoals het verwijderen van het label kolom "cnt' van de invoergegevens nodig en beperken van de uitvoer naar alleen de exemplaar-id en de bijbehorende voorspelde waarde.</span><span class="sxs-lookup"><span data-stu-id="e8224-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span></span>

<span data-ttu-id="e8224-144">Als u wilt opslaan zelf die werken, kunt u gewoon openen de [Voorspellend experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in de galerie die al is voorbereid.</span><span class="sxs-lookup"><span data-stu-id="e8224-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span></span>

<span data-ttu-id="e8224-145">Voor het implementeren van de webservice Voorspellend experiment uitvoeren en klik op de **webservice implementeren** knop onder het canvas.</span><span class="sxs-lookup"><span data-stu-id="e8224-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span></span> <span data-ttu-id="e8224-146">De score webservice 'Fiets verhuur score berekenen voor' name '.</span><span class="sxs-lookup"><span data-stu-id="e8224-146">Name the scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="e8224-147">10 identiek webservice-eindpunten maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8224-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="e8224-148">Deze webservice wordt geleverd met een standaardeindpunt.</span><span class="sxs-lookup"><span data-stu-id="e8224-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="e8224-149">Maar dit is nog niet als geïnteresseerd zijn in het standaardeindpunt omdat deze niet worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e8224-149">But we're not as interested in the default endpoint since it can't be updated.</span></span> <span data-ttu-id="e8224-150">Wat we moeten doen is het maken van 10 extra eindpunten, één voor elke locatie.</span><span class="sxs-lookup"><span data-stu-id="e8224-150">What we need to do is to create 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="e8224-151">We doen dit met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8224-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="e8224-152">Eerst we onze PowerShell-omgeving hebt ingesteld:</span><span class="sxs-lookup"><span data-stu-id="e8224-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and is properly set to point to the valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="e8224-153">Voer de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e8224-153">Then, run the following PowerShell command:</span></span>

    # Create 10 endpoints on the scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="e8224-154">Nu we 10 eindpunten hebt gemaakt en alle bevatten getraind op hetzelfde getraind model *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="e8224-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="e8224-155">U kunt ze weergeven in de Azure-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="e8224-155">You can view them in the Azure Management Portal.</span></span>

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-the-endpoints-to-use-separate-training-datasets-using-powershell"></a><span data-ttu-id="e8224-157">De eindpunten voor het gebruik van twee afzonderlijke trainings-gegevenssets met behulp van PowerShell bijwerken</span><span class="sxs-lookup"><span data-stu-id="e8224-157">Update the endpoints to use separate training datasets using PowerShell</span></span>
<span data-ttu-id="e8224-158">De volgende stap is de eindpunten bijwerken met een unieke getraind voor elke afzonderlijke klantgegevens modellen.</span><span class="sxs-lookup"><span data-stu-id="e8224-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="e8224-159">Maar eerst moet u voor het produceren van deze modellen uit de **fiets verhuur Training** webservice.</span><span class="sxs-lookup"><span data-stu-id="e8224-159">But first we need to produce these models from the **Bike Rental Training** web service.</span></span> <span data-ttu-id="e8224-160">Daarvoor gaat u terug naar de **fiets verhuur Training** webservice.</span><span class="sxs-lookup"><span data-stu-id="e8224-160">Let's go back to the **Bike Rental Training** web service.</span></span> <span data-ttu-id="e8224-161">We moeten het eindpunt BES 10 keer met 10 andere training gegevenssets aanroepen om het produceren van 10 verschillende modellen.</span><span class="sxs-lookup"><span data-stu-id="e8224-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span></span> <span data-ttu-id="e8224-162">We gebruiken de **InovkeAmlWebServiceBESEndpoint** PowerShell-cmdlet om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="e8224-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span></span>

<span data-ttu-id="e8224-163">U moet ook referenties opgeven voor blob storage-account in `$configContent`, dat wil zeggen de velden `AccountName`, `AccountKey` en `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="e8224-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="e8224-164">De `AccountName` kan bestaan uit een van de accountnamen van uw, zoals in de **klassieke Azure-beheerportal** (*opslag* tabblad).</span><span class="sxs-lookup"><span data-stu-id="e8224-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="e8224-165">Nadat u op een opslagaccount op de `AccountKey` kunt u vinden door te drukken de **toegangssleutels beheren** knop onderaan en kopiëren van de *primaire toegangssleutel*.</span><span class="sxs-lookup"><span data-stu-id="e8224-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span></span> <span data-ttu-id="e8224-166">De `RelativeLocation` is het pad ten opzichte van uw opslag waarin u een nieuw model wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e8224-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span></span> <span data-ttu-id="e8224-167">Bijvoorbeeld: het pad `hai/retrain/bike_rental/` in het script onder verwijst naar een container met de naam `hai`, en `/retrain/bike_rental/` zijn submappen.</span><span class="sxs-lookup"><span data-stu-id="e8224-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="e8224-168">Op dit moment kunt u geen submappen via de gebruikersinterface van de portal maken, maar er zijn [verschillende Azure Storage Explorers](../storage/common/storage-explorers.md) waarmee u kunt doen.</span><span class="sxs-lookup"><span data-stu-id="e8224-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you to do so.</span></span> <span data-ttu-id="e8224-169">Het wordt aanbevolen dat u een nieuwe container in uw opslag maken voor het opslaan van de nieuwe getraind modellen (.ilearner-bestanden) als volgt: van uw opslagpagina, klikt u op de **toevoegen** knop onderaan en noem deze `retrain`.</span><span class="sxs-lookup"><span data-stu-id="e8224-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span></span> <span data-ttu-id="e8224-170">Kortom, de benodigde wijzigingen in het onderstaande script hebben betrekking op `AccountName`, `AccountKey` en `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="e8224-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke the retraining API 10 times
    # This is the default (and the only) endpoint on the training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="e8224-171">Het eindpunt BES is de enige ondersteunde modus voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="e8224-171">The BES endpoint is the only supported mode for this operation.</span></span> <span data-ttu-id="e8224-172">RRS kan niet worden gebruikt voor het produceren van getraind modellen.</span><span class="sxs-lookup"><span data-stu-id="e8224-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="e8224-173">Zoals u ziet, in plaats van 10 andere BES taak json configuratiebestanden, maken we dynamisch in plaats daarvan de configuratietekenreeks maken en voer deze naar de *jobConfigString* parameter van de  **InvokeAmlWebServceBESEndpoint** cmdlet, omdat het is helaas niet hoeft te bewaren van een kopie op schijf.</span><span class="sxs-lookup"><span data-stu-id="e8224-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span></span>

<span data-ttu-id="e8224-174">Als alles goed gaat, na enige tijd ziet u 10 .ilearner bestanden van *model001.ilearner* naar *model010.ilearner*, in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8224-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="e8224-175">Nu we klaar zijn om bij te werken van onze 10 batchscoreberekening webservice-eindpunten met deze modellen met behulp van de **Patch AmlWebServiceEndpoint** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e8224-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="e8224-176">Vergeet niet opnieuw kunt dat we alleen patch de niet-standaard-eindpunten die we programmatisch eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8224-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span></span>

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="e8224-177">Dit moet vrij snel uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8224-177">This should run fairly quickly.</span></span> <span data-ttu-id="e8224-178">Wanneer de uitvoering is voltooid, je we hebt gemaakt 10 voorspellende webservice-eindpunten, elk met een unieke getraind op de specifieke gegevensset naar een locatie verhuur, via een trainingsexperiment één model is getraind.</span><span class="sxs-lookup"><span data-stu-id="e8224-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span></span> <span data-ttu-id="e8224-179">U kunt dit controleren, kunt u proberen het aanroepen van deze eindpunten met behulp van de **InvokeAmlWebServiceRRSEndpoint** cmdlet, met dezelfde gegevens en andere voorspelling resultaten weergegeven omdat de modellen worden getraind verwachte met andere training sets.</span><span class="sxs-lookup"><span data-stu-id="e8224-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="e8224-180">Volledige PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="e8224-180">Full PowerShell script</span></span>
<span data-ttu-id="e8224-181">Dit is de vermelding van de volledige broncode:</span><span class="sxs-lookup"><span data-stu-id="e8224-181">Here's the listing of the full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and properly set to point to the valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on the scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke the retraining API 10 times to produce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
