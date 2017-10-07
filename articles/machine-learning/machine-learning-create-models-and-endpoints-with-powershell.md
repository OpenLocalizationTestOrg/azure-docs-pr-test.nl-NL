---
title: aaaCreate meerdere modellen van een experiment | Microsoft Docs
description: Gebruik PowerShell toocreate meerdere Machine Learning-modellen en web service-eindpunten met Hallo dezelfde algoritme maar verschillende training gegevenssets.
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
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="acd87-103">Veel Machine Learning-modellen en webservice-eindpunten maken van een experiment met PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd87-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="acd87-104">Hier volgt een veelvoorkomend probleem van machine learning: gewenste toocreate veel modellen die Hallo hebben dezelfde werkstroom training en gebruik dezelfde algoritme hello, maar hebben verschillende training gegevenssets als invoer.</span><span class="sxs-lookup"><span data-stu-id="acd87-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="acd87-105">Dit artikel ziet u hoe toodo dit op grote schaal in Azure Machine Learning Studio met behulp van slechts een enkele experiment.</span><span class="sxs-lookup"><span data-stu-id="acd87-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="acd87-106">Stel dat u een globale fiets verhuur franchiseonderneming bedrijf bezit.</span><span class="sxs-lookup"><span data-stu-id="acd87-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="acd87-107">Wilt u toobuild regressie model toopredict Hallo verhuur vraag op basis van historische gegevens.</span><span class="sxs-lookup"><span data-stu-id="acd87-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="acd87-108">U 1000 verhuur locaties via Hallo wereld hebt en u hebt een gegevensset voor elke locatie met belangrijke functies zoals datum, tijd, weer en verkeer dat specifieke tooeach locatie worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="acd87-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="acd87-109">U kunt het model met één keer een samengevoegde versie van alle Hallo gegevenssets op alle locaties kan trainen.</span><span class="sxs-lookup"><span data-stu-id="acd87-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="acd87-110">Maar omdat elk van de locaties van een unieke omgeving heeft, een betere benadering zou worden tootrain uw regressiemodel met afzonderlijk Hallo gegevensset voor elke locatie.</span><span class="sxs-lookup"><span data-stu-id="acd87-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="acd87-111">Op die manier elk getraind model kon worden in de grootte van de andere archieven Hallo account, volume, Geografie, populatie, fiets-vriendelijk verkeer-omgeving, *enzovoort*.</span><span class="sxs-lookup"><span data-stu-id="acd87-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="acd87-112">Die mogelijk de beste aanpak hello, maar u niet wilt dat toocreate 1.000 training experimenten in Azure Machine Learning met elkaar die een unieke locatie voorstelt.</span><span class="sxs-lookup"><span data-stu-id="acd87-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="acd87-113">Behalve dat een enigszins overweldigend taak, het is ook heel inefficiënt lijkt omdat elk experiment alle dezelfde onderdelen, met uitzondering van Hallo training gegevensset Hallo zou hebben.</span><span class="sxs-lookup"><span data-stu-id="acd87-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="acd87-114">Gelukkig we dit kunt doen met behulp van Hallo [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) en automatiseren Hallo-taak met [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="acd87-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="acd87-115">toomake ons voorbeeld sneller worden uitgevoerd, verlagen we het aantal locaties van 1000 too10 Hallo.</span><span class="sxs-lookup"><span data-stu-id="acd87-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="acd87-116">Maar hello dezelfde beginselen en procedures toepassen too1, 000 locaties.</span><span class="sxs-lookup"><span data-stu-id="acd87-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="acd87-117">Hallo enige verschil is dat als u wilt dat tootrain van 1000 gegevenssets u waarschijnlijk toothink wilt van het uitvoeren van de volgende PowerShell-scripts parallel Hallo.</span><span class="sxs-lookup"><span data-stu-id="acd87-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="acd87-118">Hoe toodo die valt buiten bereik Hallo van dit artikel, maar u kunt vinden voorbeelden van PowerShell multithreading op Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="acd87-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="acd87-119">Hallo trainingsexperiment instellen</span><span class="sxs-lookup"><span data-stu-id="acd87-119">Set up hello training experiment</span></span>
<span data-ttu-id="acd87-120">We gaan een voorbeeld toouse [trainingsexperiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) die we al hebt gemaakt in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="acd87-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="acd87-121">Open dit experiment in uw [Azure Machine Learning Studio](https://studio.azureml.net) werkruimte.</span><span class="sxs-lookup"><span data-stu-id="acd87-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="acd87-122">In de volgorde toofollow samen met het volgende voorbeeld kunt u toouse een standard-werkruimte in plaats van een gratis werkruimte.</span><span class="sxs-lookup"><span data-stu-id="acd87-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="acd87-123">We één eindpunt maakt voor elke klant - voor een totaal van 10 eindpunten - en waarvoor u een standaard werkruimte omdat een gratis werkruimte beperkt too3 eindpunten is.</span><span class="sxs-lookup"><span data-stu-id="acd87-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="acd87-124">Als u alleen een gratis werkruimte hebt, net Hallo scripts hieronder tooallow voor slechts 3 locaties te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="acd87-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="acd87-125">Hallo-experiment wordt gebruikgemaakt van een **importgegevens** module tooimport Hallo training gegevensset *customer001.csv* van een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="acd87-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="acd87-126">Stel hebben we training gegevenssets van alle fiets verhuur locaties verzameld en opgeslagen in dezelfde locatie voor de opslag-blob met bestandsnamen, variërend van Hallo *rentalloc001.csv* te*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="acd87-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="acd87-128">Houd er rekening mee dat een **Web Service uitvoer** module is toegevoegd toohello **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="acd87-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="acd87-129">Wanneer dit experiment wordt geïmplementeerd als een webservice, retourneren die zijn gekoppeld aan die uitvoer Hallo-eindpunt Hallo getrainde model in Hallo-indeling van een bestand .ilearner.</span><span class="sxs-lookup"><span data-stu-id="acd87-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="acd87-130">Let ook op dat u een web service-parameter voor Hallo-URL die Hallo stelt **importgegevens** module wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="acd87-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="acd87-131">Deze manier kunnen wij toouse Hallo parameter toospecify individuele training gegevenssets tootrain Hallo model voor elke locatie.</span><span class="sxs-lookup"><span data-stu-id="acd87-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="acd87-132">Er zijn andere manieren we kunnen dit hebt gedaan, zoals met behulp van een SQL-query met een web service parameter tooget gegevens uit een Azure SQL database of te gebruiken om een **Web Service invoer** module toopass in een gegevensset toohello-webservice.</span><span class="sxs-lookup"><span data-stu-id="acd87-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="acd87-134">Nu gaan we deze trainingsexperiment met de standaardwaarde Hallo uitvoeren *rental001.csv* zoals Hallo training gegevensset.</span><span class="sxs-lookup"><span data-stu-id="acd87-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="acd87-135">Als u hello uitvoer Hallo bekijkt **Evaluate** module (Hallo uitvoer op en selecteer **Visualize**), kunt u zien krijgen we een goede prestaties van *AUC* = 0.91.</span><span class="sxs-lookup"><span data-stu-id="acd87-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="acd87-136">Op dit moment we klaar toodeploy een webservice buiten dit trainingsexperiment.</span><span class="sxs-lookup"><span data-stu-id="acd87-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="acd87-137">Hallo training en score berekenen voor webservices implementeren</span><span class="sxs-lookup"><span data-stu-id="acd87-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="acd87-138">Hallo toodeploy training webservice, klikt u op Hallo **webservice ingesteld** onder het experimentcanvas hello en selecteer **webservice implementeren**.</span><span class="sxs-lookup"><span data-stu-id="acd87-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="acd87-139">Roep deze webservice '' fiets verhuur Training'.</span><span class="sxs-lookup"><span data-stu-id="acd87-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="acd87-140">Er moet nu toodeploy Hallo score-webservice.</span><span class="sxs-lookup"><span data-stu-id="acd87-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="acd87-141">toodo, we kunt klikken op **webservice ingesteld** hieronder Hallo canvas en selecteer **voorspellende webservice**.</span><span class="sxs-lookup"><span data-stu-id="acd87-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="acd87-142">Hiermee maakt u een score experiment.</span><span class="sxs-lookup"><span data-stu-id="acd87-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="acd87-143">Er moet een paar kleine aanpassingen toomake deze werken als een webservice, zoals het Hallo labelkolom 'cnt' verwijderen uit de Hallo invoergegevens en beperken Hallo uitvoer tooonly Hallo exemplaar-id en de bijbehorende van Hallo voorspelde waarde toomake.</span><span class="sxs-lookup"><span data-stu-id="acd87-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="acd87-144">toosave zelf die werken, kunt u eenvoudig hello openen [Voorspellend experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in Hallo galerie die al is voorbereid.</span><span class="sxs-lookup"><span data-stu-id="acd87-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="acd87-145">Klik vervolgens op Hallo toodeploy Hallo-webservice, Hallo Voorspellend experiment uitvoeren **webservice implementeren** knop onder Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="acd87-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="acd87-146">Naam Hallo score berekenen voor webservice 'Fiets verhuur score berekenen' '.</span><span class="sxs-lookup"><span data-stu-id="acd87-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="acd87-147">10 identiek webservice-eindpunten maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd87-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="acd87-148">Deze webservice wordt geleverd met een standaardeindpunt.</span><span class="sxs-lookup"><span data-stu-id="acd87-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="acd87-149">Maar dit is nog niet belangstelling Hallo standaardeindpunt omdat deze niet worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="acd87-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="acd87-150">Wat er moet toodo is toocreate 10 extra eindpunten, één voor elke locatie.</span><span class="sxs-lookup"><span data-stu-id="acd87-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="acd87-151">We doen dit met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="acd87-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="acd87-152">Eerst we onze PowerShell-omgeving hebt ingesteld:</span><span class="sxs-lookup"><span data-stu-id="acd87-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="acd87-153">Voer Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="acd87-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="acd87-154">Nu er 10 eindpunten is gemaakt en ze allemaal dezelfde getrainde model wordt getraind op Hallo bevatten *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="acd87-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="acd87-155">U kunt ze weergeven in hello Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="acd87-155">You can view them in hello Azure Management Portal.</span></span>

![Afbeelding](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="acd87-157">Hallo eindpunten toouse twee afzonderlijke trainings gegevenssets met behulp van PowerShell bijwerken</span><span class="sxs-lookup"><span data-stu-id="acd87-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="acd87-158">de volgende stap Hallo is tooupdate Hallo eindpunten met een unieke getraind voor elke afzonderlijke klantgegevens modellen.</span><span class="sxs-lookup"><span data-stu-id="acd87-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="acd87-159">Maar eerst moet u tooproduce deze modellen van Hallo **fiets verhuur Training** webservice.</span><span class="sxs-lookup"><span data-stu-id="acd87-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="acd87-160">Daarvoor gaat u terug toohello **fiets verhuur Training** webservice.</span><span class="sxs-lookup"><span data-stu-id="acd87-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="acd87-161">Toocall moet het eindpunt BES 10 keer met 10 andere training gegevenssets in volgorde tooproduce 10 verschillende modellen.</span><span class="sxs-lookup"><span data-stu-id="acd87-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="acd87-162">We gebruiken Hallo **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo dit.</span><span class="sxs-lookup"><span data-stu-id="acd87-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="acd87-163">U moet ook tooprovide referenties voor blob storage-account in `$configContent`, dat wil zeggen op Hallo velden `AccountName`, `AccountKey` en `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="acd87-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="acd87-164">Hallo `AccountName` kan bestaan uit een van de accountnamen van uw, zoals in Hallo **klassieke Azure-beheerportal** (*opslag* tabblad).</span><span class="sxs-lookup"><span data-stu-id="acd87-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="acd87-165">Nadat u op een opslagaccount op de `AccountKey` vindt u door te drukken Hallo **toegangssleutels beheren** knop op Hallo onder en kopiëren Hallo *primaire toegangssleutel*.</span><span class="sxs-lookup"><span data-stu-id="acd87-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="acd87-166">Hallo `RelativeLocation` Hallo pad relatief tooyour opslag is waarin u een nieuw model wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="acd87-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="acd87-167">Bijvoorbeeld: Hallo pad `hai/retrain/bike_rental/` in de volgende punten tooa container met de naam Hallo script `hai`, en `/retrain/bike_rental/` zijn submappen.</span><span class="sxs-lookup"><span data-stu-id="acd87-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="acd87-168">Op dit moment kunt u geen submappen via de gebruikersinterface voor het Hallo-portal maken, maar er zijn [verschillende Azure Storage Explorers](../storage/common/storage-explorers.md) waarmee u toodo dus.</span><span class="sxs-lookup"><span data-stu-id="acd87-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="acd87-169">Het wordt aanbevolen dat u een nieuwe container maken in uw opslag toostore Hallo nieuwe getraind modellen (.ilearner-bestanden) als volgt: van uw opslagpagina, klikt u op Hallo **toevoegen** knop Hallo onderin en noem deze `retrain`.</span><span class="sxs-lookup"><span data-stu-id="acd87-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="acd87-170">Kortom, onderstaande Hallo noodzakelijke wijzigingen toohello-script te horen`AccountName`, `AccountKey` en `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="acd87-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
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
> <span data-ttu-id="acd87-171">Hallo BES-eindpunt is modus Hallo alleen ondersteund voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="acd87-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="acd87-172">RRS kan niet worden gebruikt voor het produceren van getraind modellen.</span><span class="sxs-lookup"><span data-stu-id="acd87-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="acd87-173">Zoals u ziet, in plaats van 10 andere BES taak json configuratiebestanden, maken we dynamisch Hallo configuratietekenreeks in plaats daarvan maakt en voer deze toohello *jobConfigString* parameter Hallo  **InvokeAmlWebServceBESEndpoint** cmdlet, omdat er een kopie echt geen tookeep nodig op schijf is.</span><span class="sxs-lookup"><span data-stu-id="acd87-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="acd87-174">Als alles goed gaat, na enige tijd ziet u 10 .ilearner bestanden van *model001.ilearner* te*model010.ilearner*, in uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="acd87-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="acd87-175">Nu we klaar tooupdate onze 10 score berekenen voor web service-eindpunten met deze modellen met Hallo **Patch AmlWebServiceEndpoint** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acd87-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="acd87-176">Vergeet niet opnieuw kunt dat we alleen patch Hallo niet-standaard eindpunten die we programmatisch eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="acd87-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="acd87-177">Dit moet vrij snel uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="acd87-177">This should run fairly quickly.</span></span> <span data-ttu-id="acd87-178">Wanneer het Hallo-uitvoering is voltooid, hebt we hebt gemaakt 10 voorspellende webservice-eindpunten, elk met een unieke op Hallo gegevensset specifieke tooa verhuur locatie, via een trainingsexperiment één getraind model is getraind.</span><span class="sxs-lookup"><span data-stu-id="acd87-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="acd87-179">tooverify, kunt u proberen het aanroepen van deze eindpunten met Hallo **InvokeAmlWebServiceRRSEndpoint** cmdlet meeleveren Hello dezelfde gegevens en u kunt verwachten toosee verschillende voorspelling resultaten aangezien Hallo modellen zijn getraind met verschillende training sets.</span><span class="sxs-lookup"><span data-stu-id="acd87-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="acd87-180">Volledige PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="acd87-180">Full PowerShell script</span></span>
<span data-ttu-id="acd87-181">Hallo-overzicht van de volledige broncode Hallo Ga als volgt:</span><span class="sxs-lookup"><span data-stu-id="acd87-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
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

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
