---
title: een bestaande voorspellende aaaRetrain webservice | Microsoft Docs
description: Meer informatie over hoe Hallo web service toouse Hallo zojuist getrainde model in Azure Machine Learning tooretrain een model en bij te werken.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="5e67d-103">Een bestaande voorspellende webservice opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="5e67d-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="5e67d-104">Dit document beschrijft Hallo retraining-proces voor Hallo scenario te volgen:</span><span class="sxs-lookup"><span data-stu-id="5e67d-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="5e67d-105">U hebt een trainingsexperiment en een Voorspellend experiment die u hebt geïmplementeerd als een geoperationaliseerd webservice.</span><span class="sxs-lookup"><span data-stu-id="5e67d-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="5e67d-106">U hebt nieuwe gegevens die u uw predictive web service toouse tooperform de score berekenen wilt.</span><span class="sxs-lookup"><span data-stu-id="5e67d-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="5e67d-107">toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="5e67d-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="5e67d-108">Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="5e67d-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="5e67d-109">Beginnen met uw bestaande webservice en experimenten, moet u toofollow deze stappen:</span><span class="sxs-lookup"><span data-stu-id="5e67d-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="5e67d-110">Hallo model bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5e67d-110">Update hello model.</span></span>
   1. <span data-ttu-id="5e67d-111">De training experiment tooallow voor web-service in- en uitgangen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5e67d-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="5e67d-112">Hallo trainingsexperiment implementeren als een retraining-webservice.</span><span class="sxs-lookup"><span data-stu-id="5e67d-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="5e67d-113">Hallo trainingsexperiment Batch uitvoering Service (BES) tooretrain Hallo model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e67d-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="5e67d-114">Gebruik hello Azure Machine Learning PowerShell-cmdlets tooupdate Hallo Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="5e67d-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="5e67d-115">Meld u aan tooyour Azure Resource Manager-account.</span><span class="sxs-lookup"><span data-stu-id="5e67d-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="5e67d-116">Hallo webservicedefinitie ophalen.</span><span class="sxs-lookup"><span data-stu-id="5e67d-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="5e67d-117">Hallo webservicedefinitie als JSON exporteren.</span><span class="sxs-lookup"><span data-stu-id="5e67d-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="5e67d-118">Hallo referentie toohello ilearner-blob in Hallo JSON bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5e67d-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="5e67d-119">Hallo JSON importeren in de definitie van een web-service.</span><span class="sxs-lookup"><span data-stu-id="5e67d-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="5e67d-120">Hallo webservice bijwerken met de definitie van een nieuwe web-service.</span><span class="sxs-lookup"><span data-stu-id="5e67d-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="5e67d-121">Hallo trainingsexperiment implementeren</span><span class="sxs-lookup"><span data-stu-id="5e67d-121">Deploy hello training experiment</span></span>
<span data-ttu-id="5e67d-122">Hallo trainingsexperiment toodeploy als retraining webservice, moet u web service in- en uitgangen toohello model toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5e67d-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="5e67d-123">Door verbinding te maken een *Web Service uitvoer* module toohello experiment  *[Train Model] [ train-model]*  module u Hallo training experiment inschakelen een nieuw getraind model die u in uw Voorspellend experiment gebruiken kunt tooproduce.</span><span class="sxs-lookup"><span data-stu-id="5e67d-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="5e67d-124">Als u hebt een *Evaluate Model* -module, kunt u ook web service uitvoer tooget Hallo evaluatieresultaten koppelen als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="5e67d-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="5e67d-125">tooupdate uw trainingsexperiment:</span><span class="sxs-lookup"><span data-stu-id="5e67d-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="5e67d-126">Verbinding maken met een *Web Service invoer* module tooyour gegevensinvoer (bijvoorbeeld een *Clean Missing Data* module).</span><span class="sxs-lookup"><span data-stu-id="5e67d-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="5e67d-127">Normaal gesproken gewenste tooensure die uw invoergegevens verwerkt in Hallo op dezelfde manier als uw oorspronkelijke trainingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="5e67d-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="5e67d-128">Verbinding maken met een *Web Service uitvoer* module toohello uitvoer van uw *Train Model* module.</span><span class="sxs-lookup"><span data-stu-id="5e67d-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="5e67d-129">Als u hebt een *Evaluate Model* module en u wilt dat toooutput Hallo evaluatieresultaten, verbinding maken met een *Web Service uitvoer* module toohello uitvoer van uw *Evaluate Model* module.</span><span class="sxs-lookup"><span data-stu-id="5e67d-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="5e67d-130">Voer uw experiment.</span><span class="sxs-lookup"><span data-stu-id="5e67d-130">Run your experiment.</span></span>

<span data-ttu-id="5e67d-131">Vervolgens moet u Hallo trainingsexperiment implementeren als een webservice die een getraind model en de resultaten van evaluatie van model produceert.</span><span class="sxs-lookup"><span data-stu-id="5e67d-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="5e67d-132">Aan de onderkant van de Hallo van experimentcanvas Hallo, klikt u op **webservice ingesteld**, en selecteer vervolgens **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="5e67d-133">Hello Azure Machine Learning-webservices wordt geopend toohello **webservice implementeren** pagina.</span><span class="sxs-lookup"><span data-stu-id="5e67d-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="5e67d-134">Typ een naam voor uw web-service, kies een betaald abonnement en klik vervolgens op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="5e67d-135">U kunt Hallo Batchuitvoering methode alleen gebruiken voor het maken van modellen getraind.</span><span class="sxs-lookup"><span data-stu-id="5e67d-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="5e67d-136">Hallo-model met nieuwe gegevens met behulp van BES Retrain</span><span class="sxs-lookup"><span data-stu-id="5e67d-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="5e67d-137">In dit voorbeeld we toocreate Hallo C# retraining toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e67d-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="5e67d-138">U kunt deze taak ook Python of R voorbeeld code tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="5e67d-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="5e67d-139">toocall hello retraining API's:</span><span class="sxs-lookup"><span data-stu-id="5e67d-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="5e67d-140">Maak een C#-consoletoepassing in Visual Studio: **nieuw** > **Project** > **Visual C#** > **Classic Windows Desktop** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="5e67d-141">Meld u aan toohello Machine Learning Web Services-portal.</span><span class="sxs-lookup"><span data-stu-id="5e67d-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="5e67d-142">Klik op Hallo webservice waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="5e67d-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="5e67d-143">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-143">Click **Consume**.</span></span>
5. <span data-ttu-id="5e67d-144">Hallo Hallo onderaan in **verbruiken** pagina in Hallo **voorbeeldcode** sectie, klikt u op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="5e67d-145">Hallo C# voorbeeldcode voor Batchuitvoering Kopieer en plak deze in het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e67d-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="5e67d-146">Zorg ervoor dat die naamruimte Hallo blijft intact.</span><span class="sxs-lookup"><span data-stu-id="5e67d-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="5e67d-147">Hallo NuGet-pakket Microsoft.AspNet.WebApi.Client, zoals opgegeven in Hallo opmerkingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5e67d-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="5e67d-148">tooadd hello verwijzing tooMicrosoft.WindowsAzure.Storage.dll mogelijk moet u eerst tooinstall hello [-clientbibliotheek voor Azure Storage-services](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="5e67d-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="5e67d-149">Hallo volgende schermafbeelding ziet u Hallo **verbruiken** pagina in hello Azure Machine Learning-webservices-portal.</span><span class="sxs-lookup"><span data-stu-id="5e67d-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Pagina gebruiken][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="5e67d-151">Hallo apikey declaratie bijwerken</span><span class="sxs-lookup"><span data-stu-id="5e67d-151">Update hello apikey declaration</span></span>
<span data-ttu-id="5e67d-152">Zoek Hallo **apikey** declaratie:</span><span class="sxs-lookup"><span data-stu-id="5e67d-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="5e67d-153">In Hallo **Basic verbruik info** sectie Hallo **verbruiken** pagina, Ga naar de primaire sleutel Hallo en kopieer het toohello **apikey** declaratie.</span><span class="sxs-lookup"><span data-stu-id="5e67d-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="5e67d-154">Hello Azure Storage-gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="5e67d-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="5e67d-155">Hallo BES voorbeeldcode uploadt een bestand van een lokale schijf (bijvoorbeeld ' C:\temp\CensusIpnput.csv') tooAzure opslag, verwerkt en schrijft Hallo resultaten back tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="5e67d-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="5e67d-156">tooupdate hello Azure Storage-gegevens, moet u Hallo naam, de sleutel en de container voor uw opslagaccount van Hallo klassieke Azure-portal en vervolgens update Hallo correspondi na het uitvoeren van uw experiment Hallo resulterende storage-account ophalen de werkstroom moet vergelijkbaar toohello volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="5e67d-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Resulterende werkstroom na het uitvoeren van][4]<span data-ttu-id="5e67d-158">NG waarden in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="5e67d-158">ng values in hello code.</span></span>

1. <span data-ttu-id="5e67d-159">Meld u aan toohello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5e67d-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="5e67d-160">Klik in Hallo linkernavigatievenster kolom op **opslag**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="5e67d-161">Selecteer één toostore hello retrained vanuit Hallo lijst met opslagaccounts, model.</span><span class="sxs-lookup"><span data-stu-id="5e67d-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="5e67d-162">Klik onder aan de pagina Hallo Hallo op **toegangssleutels beheren**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="5e67d-163">Kopiëren en opslaan van Hallo **primaire toegangssleutel** en sluiten Hallo dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5e67d-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="5e67d-164">Bovenaan Hallo Hallo pagina, klikt u op **Containers**.</span><span class="sxs-lookup"><span data-stu-id="5e67d-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="5e67d-165">Selecteer een bestaande container of maak een nieuwe en Hallo naam worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e67d-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="5e67d-166">Zoek Hallo *StorageAccountName*, *StorageAccountKey*, en *StorageContainerName* declaraties en update Hallo waarden die u vanuit de klassieke portal Hallo opgeslagen .</span><span class="sxs-lookup"><span data-stu-id="5e67d-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="5e67d-167">Ook moet u ervoor zorgen dat Hallo-bestand voor invoer is beschikbaar op Hallo locatie die u in het Hallo-code opgeeft.</span><span class="sxs-lookup"><span data-stu-id="5e67d-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="5e67d-168">Hallo uitvoerlocatie opgeven</span><span class="sxs-lookup"><span data-stu-id="5e67d-168">Specify hello output location</span></span>
<span data-ttu-id="5e67d-169">Wanneer u de uitvoerlocatie Hallo in Hallo Request-nettolading opgeeft, uitbreiding van Hallo-bestand dat is opgegeven in Hallo *RelativeLocation* moet worden opgegeven als `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="5e67d-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="5e67d-170">Zie Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5e67d-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="5e67d-171">Hallo Hieronder volgt een voorbeeld van uitvoer retraining: ![Retraining uitvoer][6]</span><span class="sxs-lookup"><span data-stu-id="5e67d-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="5e67d-172">Hallo retraining resultaten evalueren</span><span class="sxs-lookup"><span data-stu-id="5e67d-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="5e67d-173">Wanneer u de toepassing hello uitvoert, omvat Hallo uitvoer Hallo-URL en gedeelde handtekeningen toegangstoken dat nodig tooaccess Hallo evaluatieresultaten zijn.</span><span class="sxs-lookup"><span data-stu-id="5e67d-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="5e67d-174">Ziet u prestatieresultaten Hallo van Hallo retrained model door een combinatie van Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* uit Hallo uitvoer resultaten voor *output2* (zoals weergegeven in de voorgaande afbeelding uitvoer retraining Hallo) en Hallo volledige URL in de adresbalk van de browser Hallo plakken.</span><span class="sxs-lookup"><span data-stu-id="5e67d-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="5e67d-175">Hallo resultaten toodetermine onderzoeken of Hallo zojuist getraind model functioneert goed genoeg tooreplace Hallo een bestaande.</span><span class="sxs-lookup"><span data-stu-id="5e67d-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="5e67d-176">Kopiëren Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken* uit Hallo uitvoer resultaten.</span><span class="sxs-lookup"><span data-stu-id="5e67d-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="5e67d-177">Opnieuw trainen Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="5e67d-177">Retrain hello web service</span></span>
<span data-ttu-id="5e67d-178">Wanneer u een nieuwe webservice opnieuw trainen, werkt u Hallo voorspellende web service definitie tooreference Hallo nieuwe getrainde model.</span><span class="sxs-lookup"><span data-stu-id="5e67d-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="5e67d-179">Hallo webservicedefinitie is een interne representatie van het getrainde model van de webservice Hallo Hallo en kan niet rechtstreeks worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5e67d-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="5e67d-180">Zorg ervoor dat u voor uw Voorspellend experiment en niet uw trainingsexperiment Hallo webservicedefinitie ophaalt.</span><span class="sxs-lookup"><span data-stu-id="5e67d-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="5e67d-181">Meld u aan tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5e67d-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="5e67d-182">U moet zich eerst aanmelden tooyour Azure-account uit binnen Hallo PowerShell-omgeving met behulp van Hallo [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e67d-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="5e67d-183">Hallo webservicedefinitie object ophalen</span><span class="sxs-lookup"><span data-stu-id="5e67d-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="5e67d-184">Haal vervolgens Hallo webservicedefinitie object door aanroepen Hallo [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e67d-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="5e67d-185">toodetermine hello Resourcegroepnaam van een bestaande webservice Hallo Get AzureRmMlWebService cmdlet zonder parameters toodisplay Hallo webservices uitvoeren in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5e67d-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="5e67d-186">Zoek Hallo webservice en zoek vervolgens naar de web service-ID.</span><span class="sxs-lookup"><span data-stu-id="5e67d-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="5e67d-187">Hallo-naam van de resourcegroep Hallo Hallo vierde element in het Hallo-ID is direct na Hallo *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="5e67d-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="5e67d-188">Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="5e67d-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="5e67d-189">U kunt ook toodetermine hello Resourcegroepnaam van een bestaande webservice, toohello Azure Machine Learning-webservices portal aanmelden.</span><span class="sxs-lookup"><span data-stu-id="5e67d-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="5e67d-190">Hallo-webservice selecteren.</span><span class="sxs-lookup"><span data-stu-id="5e67d-190">Select hello web service.</span></span> <span data-ttu-id="5e67d-191">naam resourcegroep Hallo Hallo vijfde element van het Hallo-URL van webservice hello, wordt direct na Hallo *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="5e67d-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="5e67d-192">Hallo Resourcegroepnaam is in Hallo voorbeeld te volgen, standaard-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="5e67d-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="5e67d-193">Hallo webservicedefinitie object exporteren als JSON</span><span class="sxs-lookup"><span data-stu-id="5e67d-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="5e67d-194">Nieuw getraind model toomodify Hallo definitie van Hallo getrainde model toouse hello, moet u eerst hello gebruiken [Export AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport het bestand tooa JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="5e67d-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="5e67d-195">Update Hallo referentie toohello ilearner-blob</span><span class="sxs-lookup"><span data-stu-id="5e67d-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="5e67d-196">Zoek in Hallo activa, Hallo [getraind model] update Hallo *uri* waarde in Hallo *locationInfo* knooppunt met Hallo URI van Hallo ilearner-blob.</span><span class="sxs-lookup"><span data-stu-id="5e67d-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="5e67d-197">Hallo URI gegenereerd door een combinatie van Hallo *BaseLocation* en Hallo *RelativeLocation* van uitvoer Hallo Hallo BES retraining-aanroep.</span><span class="sxs-lookup"><span data-stu-id="5e67d-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="5e67d-198">Hallo JSON importeren in een object van de webservicedefinitie</span><span class="sxs-lookup"><span data-stu-id="5e67d-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="5e67d-199">Moet u Hallo [importeren AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Hallo JSON-bestand weer in een webservicedefinitie-object waarmee u tooupdate hello predicative experiment kunt is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5e67d-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="5e67d-200">Hallo webservice bijwerken</span><span class="sxs-lookup"><span data-stu-id="5e67d-200">Update hello web service</span></span>
<span data-ttu-id="5e67d-201">Gebruik tot slot Hallo [Update AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Hallo Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="5e67d-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
