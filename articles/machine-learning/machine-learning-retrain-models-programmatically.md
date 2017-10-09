---
title: aaaRetrain Machine Learning-modellen programmatisch | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically opnieuw trainen model en update Hallo web service toouse Hallo nieuw model is getraind in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="defb0-103">Machine Learning modellen programmatisch opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="defb0-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="defb0-104">In dit scenario leert u hoe een Azure Machine Learning-webservice met C# en Hallo Machine Learning-batchuitvoeringsservice in tooprogrammatically opnieuw trainen.</span><span class="sxs-lookup"><span data-stu-id="defb0-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="defb0-105">Zodra u hebt Hallo model retrained, tonen Hallo volgen scenario's hoe tooupdate Hallo-model in uw predictive webservice:</span><span class="sxs-lookup"><span data-stu-id="defb0-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="defb0-106">Als u een webservice klassieke in Hallo Machine Learning-webservices-portal hebt geïmplementeerd, Zie [opnieuw trainen van een webservice klassieke](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="defb0-107">Als u een nieuwe webservice hebt geïmplementeerd, Zie [opnieuw trainen Hallo Machine Learning Management cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="defb0-108">Zie voor een overzicht van Hallo proces retraining [opnieuw een Machine Learning-Model te trainen](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="defb0-109">Als u wilt dat toostart met uw bestaande web-service op basis van nieuwe Azure Resource Manager, Zie [opnieuw trainen van een bestaande voorspellende webservice](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="defb0-110">Een trainingsexperiment maken</span><span class="sxs-lookup"><span data-stu-id="defb0-110">Create a training experiment</span></span>
<span data-ttu-id="defb0-111">In dit voorbeeld gebruikt u ' voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset ' van Hallo Microsoft Azure Machine Learning-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="defb0-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="defb0-112">Hallo-experiment toocreate:</span><span class="sxs-lookup"><span data-stu-id="defb0-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="defb0-113">Aanmelden bij tooMicrosoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="defb0-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="defb0-114">Klik op Hallo rechterbenedenhoek van Hallo dashboard **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="defb0-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="defb0-115">Selecteer in de Microsoft Samples hello, voorbeeld 5.</span><span class="sxs-lookup"><span data-stu-id="defb0-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="defb0-116">toorename hello experiment Hallo boven aan het experimentcanvas hello, selecteert u de naam van de Hallo-experiment "voorbeeld 5: trein, Test evalueren voor binaire classificatie: volwassenen gegevensset '.</span><span class="sxs-lookup"><span data-stu-id="defb0-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="defb0-117">Type telling Model.</span><span class="sxs-lookup"><span data-stu-id="defb0-117">Type Census Model.</span></span>
6. <span data-ttu-id="defb0-118">Klik onder Hallo van Hallo experimentencanvas op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="defb0-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="defb0-119">Klik op **instellen webservice** en selecteer **Retraining webservice**.</span><span class="sxs-lookup"><span data-stu-id="defb0-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="defb0-120">Hallo hieronder vindt u de eerste experiment Hallo.</span><span class="sxs-lookup"><span data-stu-id="defb0-120">hello following shows hello initial experiment.</span></span>
   
   ![Eerste experiment.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="defb0-122">Een Voorspellend experiment maken en publiceren als een webservice</span><span class="sxs-lookup"><span data-stu-id="defb0-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="defb0-123">Vervolgens maakt u een Experiment Predicative.</span><span class="sxs-lookup"><span data-stu-id="defb0-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="defb0-124">Hallo onder aan het experimentcanvas hello, klikt u op **webservice ingesteld** en selecteer **voorspellende webservice**.</span><span class="sxs-lookup"><span data-stu-id="defb0-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="defb0-125">Hallo model opgeslagen als een getraind Model en web service invoer en uitvoer modules worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="defb0-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="defb0-126">Klik op **Run**.</span><span class="sxs-lookup"><span data-stu-id="defb0-126">Click **Run**.</span></span> 
3. <span data-ttu-id="defb0-127">Nadat het Hallo-experiment is voltooid, klikt u op **webservice implementeren [klassieke]** of **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="defb0-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="defb0-128">toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="defb0-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="defb0-129">Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="defb0-130">Hallo trainingsexperiment implementeren als een webservice Training</span><span class="sxs-lookup"><span data-stu-id="defb0-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="defb0-131">tooretrain hello getrainde model, moet u Hallo trainingsexperiment die u hebt gemaakt als een webservice Retraining implementeren.</span><span class="sxs-lookup"><span data-stu-id="defb0-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="defb0-132">Deze webservice moet een *Web Service uitvoer* module verbonden toohello  *[Train Model] [ train-model]*  module, toobe kunnen tooproduce nieuwe modellen zijn opgeleid.</span><span class="sxs-lookup"><span data-stu-id="defb0-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="defb0-133">tooreturn toohello trainingsexperiment Hallo experimenten pictogram in het linkerdeelvenster hello, klik op Hallo experiment telling Model met de naam.</span><span class="sxs-lookup"><span data-stu-id="defb0-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="defb0-134">Typ in Experiment zoekitems zoekvak Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="defb0-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="defb0-135">Sleep een *Web Service invoer* module op Hallo canvas experimenteren en verbinding maken met de uitvoer toohello *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="defb0-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="defb0-136">Dit zorgt ervoor dat uw retraining gegevens worden verwerkt Hallo op dezelfde manier als uw oorspronkelijke trainingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="defb0-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="defb0-137">Sleep twee *webservice uitvoer* modules op Hallo experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="defb0-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="defb0-138">Verbinding maken met uitvoer Hallo Hallo *Train Model* module tooone Hallo uitvoer en Hallo *Evaluate Model* module toohello andere.</span><span class="sxs-lookup"><span data-stu-id="defb0-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="defb0-139">Hallo web service uitvoer voor **Train Model** biedt ons Hallo nieuwe getrainde model.</span><span class="sxs-lookup"><span data-stu-id="defb0-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="defb0-140">Hallo uitvoer te gekoppeld**Evaluate Model** retourneert die module-uitvoer, namelijk Hallo prestatieresultaten.</span><span class="sxs-lookup"><span data-stu-id="defb0-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="defb0-141">Klik op **Run**.</span><span class="sxs-lookup"><span data-stu-id="defb0-141">Click **Run**.</span></span> 

<span data-ttu-id="defb0-142">Vervolgens moet u Hallo trainingsexperiment implementeren als een webservice die een getraind model en de resultaten van evaluatie van model produceert.</span><span class="sxs-lookup"><span data-stu-id="defb0-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="defb0-143">tooaccomplish dit de volgende reeks acties zijn afhankelijk van of u werkt met een webservice klassieke of een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="defb0-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="defb0-144">**Klassieke webservice**</span><span class="sxs-lookup"><span data-stu-id="defb0-144">**Classic web service**</span></span>

<span data-ttu-id="defb0-145">Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld** en selecteer **webservice implementeren [klassieke]**.</span><span class="sxs-lookup"><span data-stu-id="defb0-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="defb0-146">Hallo-webservice **Dashboard** voor Batchuitvoering met Hallo API-sleutel en Hallo API help-pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="defb0-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="defb0-147">Alleen Hallo Batchuitvoering methode kan worden gebruikt voor het maken van de Trained Models.</span><span class="sxs-lookup"><span data-stu-id="defb0-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="defb0-148">**Nieuwe webservice**</span><span class="sxs-lookup"><span data-stu-id="defb0-148">**New web service**</span></span>

<span data-ttu-id="defb0-149">Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld** en selecteer **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="defb0-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="defb0-150">Web Service Azure Machine Learning-webservices Hello wordt toohello implementeren service webpagina geopend.</span><span class="sxs-lookup"><span data-stu-id="defb0-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="defb0-151">Typ een naam voor uw web-service en kies een betaald abonnement en klik vervolgens op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="defb0-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="defb0-152">Alleen Hallo Batchuitvoering methode kan worden gebruikt voor het maken van de Trained Models</span><span class="sxs-lookup"><span data-stu-id="defb0-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="defb0-153">In beide gevallen nadat experiment voltooide uitgevoerd heeft ziet Hallo resulterende werkstroom er als volgt:</span><span class="sxs-lookup"><span data-stu-id="defb0-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Resulterende workflow nadat uitgevoerd.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="defb0-155">Hallo-model met nieuwe gegevens met behulp van BES Retrain</span><span class="sxs-lookup"><span data-stu-id="defb0-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="defb0-156">Bijvoorbeeld, u toocreate Hallo C# retraining toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="defb0-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="defb0-157">U kunt ook gebruiken Hallo Python of R voorbeeld code tooaccomplish deze taak.</span><span class="sxs-lookup"><span data-stu-id="defb0-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="defb0-158">toocall hello Retraining API's:</span><span class="sxs-lookup"><span data-stu-id="defb0-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="defb0-159">Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Classic Windows Desktop** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="defb0-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="defb0-160">Meld u aan toohello Machine Learning-webservice-portal.</span><span class="sxs-lookup"><span data-stu-id="defb0-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="defb0-161">Als u met een klassiek-webservice werkt, klikt u op **klassieke webservices**.</span><span class="sxs-lookup"><span data-stu-id="defb0-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="defb0-162">Klik op Hallo met werken web-service.</span><span class="sxs-lookup"><span data-stu-id="defb0-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="defb0-163">Klik op het standaardeindpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="defb0-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="defb0-164">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="defb0-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="defb0-165">Hallo Hallo onderaan in **verbruiken** pagina in Hallo **voorbeeldcode** sectie, klikt u op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="defb0-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="defb0-166">Toostep 5 van deze procedure blijven.</span><span class="sxs-lookup"><span data-stu-id="defb0-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="defb0-167">Als u met een nieuwe webservice werkt, klikt u op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="defb0-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="defb0-168">Klik op Hallo met werken web-service.</span><span class="sxs-lookup"><span data-stu-id="defb0-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="defb0-169">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="defb0-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="defb0-170">Hallo Hallo verbruiken pagina in Hallo onderaan in **voorbeeldcode** sectie, klikt u op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="defb0-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="defb0-171">Hallo C# voorbeeldcode voor Batchuitvoering Kopieer en plak deze in het bestand Program.cs hello om ervoor te zorgen Hallo naamruimte blijft intact.</span><span class="sxs-lookup"><span data-stu-id="defb0-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="defb0-172">Hallo Nuget-pakket Microsoft.AspNet.WebApi.Client zoals opgegeven in Hallo opmerkingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="defb0-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="defb0-173">tooadd hello verwijzing tooMicrosoft.WindowsAzure.Storage.dll mogelijk moet u eerst tooinstall Hallo-clientbibliotheek voor Microsoft Azure storage-services.</span><span class="sxs-lookup"><span data-stu-id="defb0-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="defb0-174">Zie voor meer informatie [Windows Storage-Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="defb0-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="defb0-175">Hallo apikey declaratie bijwerken</span><span class="sxs-lookup"><span data-stu-id="defb0-175">Update hello apikey declaration</span></span>
<span data-ttu-id="defb0-176">Zoek Hallo **apikey** declaratie.</span><span class="sxs-lookup"><span data-stu-id="defb0-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="defb0-177">In Hallo **Basic verbruik info** sectie Hallo **verbruiken** pagina, Ga naar de primaire sleutel Hallo en kopieer het toohello **apikey** declaratie.</span><span class="sxs-lookup"><span data-stu-id="defb0-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="defb0-178">Hello Azure Storage-gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="defb0-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="defb0-179">Hallo BES voorbeeldcode uploadt een bestand van een lokale schijf (bijvoorbeeld 'C:\temp\CensusIpnput.csv') tooAzure opslag, verwerkt en schrijft Hallo resultaten back tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="defb0-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="defb0-180">tooaccomplish deze taak moet u Hallo Storage account name, -sleutel en container-gegevens ophalen voor uw opslagaccount van Hallo klassieke Azure-portal en bijbehorende waarden in de code Hallo Hallo-update.</span><span class="sxs-lookup"><span data-stu-id="defb0-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="defb0-181">Meld u aan toohello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="defb0-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="defb0-182">Klik in Hallo linkernavigatievenster kolom op **opslag**.</span><span class="sxs-lookup"><span data-stu-id="defb0-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="defb0-183">Selecteer één toostore hello retrained vanuit Hallo lijst met opslagaccounts, model.</span><span class="sxs-lookup"><span data-stu-id="defb0-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="defb0-184">Klik onder aan de pagina Hallo Hallo op **toegangssleutels beheren**.</span><span class="sxs-lookup"><span data-stu-id="defb0-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="defb0-185">Kopiëren en opslaan van Hallo **primaire toegangssleutel** en sluiten Hallo dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="defb0-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="defb0-186">Bovenaan Hallo Hallo pagina, klikt u op **Containers**.</span><span class="sxs-lookup"><span data-stu-id="defb0-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="defb0-187">Selecteer een bestaande container of maak een nieuwe en Hallo naam worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="defb0-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="defb0-188">Zoek Hallo *StorageAccountName*, *StorageAccountKey*, en *StorageContainerName* declaraties en update Hallo waarden die u hebt genoteerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="defb0-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="defb0-189">Ook moet u ervoor zorgen Hallo-bestand voor invoer is beschikbaar op Hallo-locatie die u in het Hallo-code opgeeft.</span><span class="sxs-lookup"><span data-stu-id="defb0-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="defb0-190">Hallo uitvoerlocatie opgeven</span><span class="sxs-lookup"><span data-stu-id="defb0-190">Specify hello output location</span></span>
<span data-ttu-id="defb0-191">Bij het Hallo-uitvoerlocatie opgeven in Hallo Request-nettolading, uitbreiding van Hallo dat is opgegeven in Hallo *RelativeLocation* moet worden opgegeven als ilearner.</span><span class="sxs-lookup"><span data-stu-id="defb0-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="defb0-192">Zie Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="defb0-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="defb0-193">Hallo-namen van de uitvoerlocaties afwijken van Hallo uitzonderingen in deze stapsgewijze kennismaking op basis van Hallo volgorde waarin u Hallo web service uitvoer modules hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="defb0-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="defb0-194">Omdat u dit trainingsexperiment met twee uitvoer hebt ingesteld, opnemen Hallo resultaten locatiegegevens van opslag voor beide parameters.</span><span class="sxs-lookup"><span data-stu-id="defb0-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Uitvoer retraining][6]

<span data-ttu-id="defb0-196">Diagram 4: Retraining uitvoer.</span><span class="sxs-lookup"><span data-stu-id="defb0-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="defb0-197">Hallo Retraining resultaten evalueren</span><span class="sxs-lookup"><span data-stu-id="defb0-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="defb0-198">Wanneer u de toepassing hello uitvoert, Hallo uitvoer bevat de URL van de Hallo en SAS-token nodig tooaccess Hallo resultaten van evaluatie.</span><span class="sxs-lookup"><span data-stu-id="defb0-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="defb0-199">Ziet u prestatieresultaten Hallo van Hallo retrained model door een combinatie van Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* uit Hallo uitvoer resultaten voor *output2* (zoals weergegeven in de voorgaande afbeelding uitvoer retraining Hallo) en Hallo volledige URL in de adresbalk van Hallo browser te plakken.</span><span class="sxs-lookup"><span data-stu-id="defb0-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="defb0-200">Hallo resultaten toodetermine onderzoeken of Hallo zojuist getraind model functioneert goed genoeg tooreplace Hallo een bestaande.</span><span class="sxs-lookup"><span data-stu-id="defb0-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="defb0-201">Kopiëren Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* van resultaten van de uitvoer hello, wordt u ze gebruiken tijdens Hallo retraining proces.</span><span class="sxs-lookup"><span data-stu-id="defb0-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="defb0-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="defb0-202">Next steps</span></span>
<span data-ttu-id="defb0-203">Als u voorspellende Hallo-webservice geïmplementeerd door te klikken op **webservice implementeren [klassieke]**, Zie [opnieuw trainen van een webservice klassieke](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="defb0-204">Als u voorspellende Hallo-webservice geïmplementeerd door te klikken op **Web Service implementeren [New]**, Zie [opnieuw trainen Hallo Machine Learning Management cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="defb0-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
