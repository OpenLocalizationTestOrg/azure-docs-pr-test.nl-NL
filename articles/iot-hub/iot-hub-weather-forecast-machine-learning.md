---
title: aaaWeather prognose met Azure Machine Learning met gegevens uit IoT Hub | Microsoft Docs
description: Azure Machine Learning regen toopredict Hallo kans op basis van Hallo temperatuur en vochtigheid gegevens die uw IoT-hub worden verzameld van een sensor gebruiken.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: prognose weer machine learning
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="55b92-104">Weer voor de prognose met Hallo sensorgegevens uit uw IoT-hub in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="55b92-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="55b92-106">Machine learning is een techniek voor gegevenswetenschap waarmee computers leren van bestaande gegevens tooforecast toekomstig gedrag, resultaten en trends.</span><span class="sxs-lookup"><span data-stu-id="55b92-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="55b92-107">Azure Machine Learning is een cloudservice voor predictive analytics waarmee u mogelijke tooquickly kunt maken en implementeren van voorspellende modellen als analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="55b92-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="55b92-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="55b92-108">What you learn</span></span>

<span data-ttu-id="55b92-109">U leert hoe toouse Azure Machine Learning toodo weer prognose (kans regen) met behulp van Hallo temperatuur en vochtigheid gegevens van uw Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="55b92-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="55b92-110">Hallo kans regen is Hallo-uitvoer van een model van de voorspelling voorbereide weer.</span><span class="sxs-lookup"><span data-stu-id="55b92-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="55b92-111">Hallo-model is gebaseerd op historische gegevens tooforecast kans regen op basis van temperatuur en vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="55b92-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="55b92-112">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="55b92-112">What you do</span></span>

- <span data-ttu-id="55b92-113">Hallo weer voorspellingsmodel implementeren als een webservice.</span><span class="sxs-lookup"><span data-stu-id="55b92-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="55b92-114">Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="55b92-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="55b92-115">Een Stream Analytics-taak maken en Hallo taak te configureren:</span><span class="sxs-lookup"><span data-stu-id="55b92-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="55b92-116">Temperatuur en vochtigheid gegevens lezen uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="55b92-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="55b92-117">Hallo web service tooget Hallo regen kans aanroepen.</span><span class="sxs-lookup"><span data-stu-id="55b92-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="55b92-118">Sla Hallo resultaat tooan Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="55b92-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="55b92-119">Microsoft Azure Storage Explorer tooview Hallo weer prognose gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55b92-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55b92-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="55b92-120">What you need</span></span>

- <span data-ttu-id="55b92-121">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="55b92-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="55b92-122">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="55b92-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="55b92-123">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="55b92-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="55b92-124">Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="55b92-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="55b92-125">Een Azure Machine Learning Studio-account.</span><span class="sxs-lookup"><span data-stu-id="55b92-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="55b92-126">([Machine Learning Studio gratis proberen](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="55b92-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="55b92-127">Hallo weer voorspellingsmodel als een webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="55b92-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="55b92-128">Ga toohello [weer voorspelling modelpagina](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="55b92-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="55b92-129">Klik op **openen in Studio** in Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="55b92-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="55b92-130">![Open Hallo weer voorspelling modelpagina in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="55b92-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="55b92-131">Klik op **uitvoeren** toovalidate Hallo stappen voor het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="55b92-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="55b92-132">Deze stap kan toocomplete 2 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="55b92-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="55b92-133">![Open Hallo weer voorspellingsmodel in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="55b92-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="55b92-134">Klik op **instellen van WEBSERVICE** > **voorspellende webservice**.</span><span class="sxs-lookup"><span data-stu-id="55b92-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="55b92-135">![Hallo weer voorspellingsmodel in Azure Machine Learning Studio implementeren](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="55b92-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="55b92-136">Sleep in Hallo diagram Hallo **Web service invoer** module ergens in de buurt van Hallo **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="55b92-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="55b92-137">Verbinding maken met de Hallo **Web service invoer** module toohello **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="55b92-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="55b92-138">![Verbinding maken met twee modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="55b92-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="55b92-139">Klik op **uitvoeren** toovalidate Hallo stappen voor het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="55b92-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="55b92-140">Klik op **WEBSERVICE implementeren** toodeploy Hallo model als een webservice.</span><span class="sxs-lookup"><span data-stu-id="55b92-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="55b92-141">Op Hallo dashboard van Hallo-model downloaden Hallo **Excel 2010 of ouder werkmap** voor **aanvraag/antwoord**.</span><span class="sxs-lookup"><span data-stu-id="55b92-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="55b92-142">Zorg ervoor dat u Hallo downloaden **Excel 2010 of ouder werkmap** zelfs als u een nieuwere versie van Excel worden uitgevoerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="55b92-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Hallo Excel voor Hallo REQUEST RESPONSE-eindpunt downloaden](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="55b92-144">Hallo Excel-werkmap opent, noteer Hallo **URL van WEBSERVICE** en **TOEGANGSSLEUTEL**.</span><span class="sxs-lookup"><span data-stu-id="55b92-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="55b92-145">Maken, configureren en uitvoeren van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="55b92-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="55b92-146">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="55b92-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="55b92-147">In Hallo [Azure-portal](https://ms.portal.azure.com/), klikt u op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.</span><span class="sxs-lookup"><span data-stu-id="55b92-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="55b92-148">Voer Hallo informatie voor de taak hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="55b92-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="55b92-149">**Taaknaam**: Hallo-naam van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="55b92-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="55b92-150">Hallo-naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="55b92-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="55b92-151">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="55b92-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="55b92-152">**Locatie**: gebruik Hallo dezelfde locatie als de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="55b92-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="55b92-153">**Pincode toodashboard**: Schakel deze optie voor eenvoudige toegang tooyour iothub uit het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="55b92-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Een Stream Analytics-taak maken in Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="55b92-155">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="55b92-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="55b92-156">Toevoegen van een invoer toohello Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="55b92-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="55b92-157">Open Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="55b92-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="55b92-158">Onder **taak topologie**, klikt u op **invoer**.</span><span class="sxs-lookup"><span data-stu-id="55b92-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="55b92-159">In Hallo **invoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="55b92-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="55b92-160">**Invoeralias**: Hallo unieke alias voor Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="55b92-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="55b92-161">**Bron**: Selecteer **IoT-hub**.</span><span class="sxs-lookup"><span data-stu-id="55b92-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="55b92-162">**Consumergroep**: Selecteer Hallo consumergroep u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="55b92-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Toevoegen van een invoer toohello Stream Analytics-taak in Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="55b92-164">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="55b92-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="55b92-165">Toevoegen van een uitvoer toohello Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="55b92-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="55b92-166">Onder **taak topologie**, klikt u op **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="55b92-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="55b92-167">In Hallo **uitvoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="55b92-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="55b92-168">**Uitvoeraliassen**: Hallo unieke alias voor Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="55b92-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="55b92-169">**Sink**: Selecteer **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="55b92-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="55b92-170">**Storage-account**: Hallo storage-account voor de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="55b92-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="55b92-171">U kunt een opslagaccount maken of een bestaande gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55b92-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="55b92-172">**Container**: Hallo container waarin Hallo blob is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="55b92-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="55b92-173">U kunt een container maken of een bestaande gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55b92-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="55b92-174">**Gebeurtenis serialisatie-indeling**: Selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="55b92-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Een uitvoer toohello Stream Analytics-taak toevoegen in Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="55b92-176">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="55b92-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="55b92-177">Een functie toohello Stream Analytics-taak toocall Hallo u geïmplementeerde webservice toevoegen</span><span class="sxs-lookup"><span data-stu-id="55b92-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="55b92-178">Onder **taak topologie**, klikt u op **functies** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="55b92-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="55b92-179">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="55b92-179">Enter hello following information:</span></span>

   <span data-ttu-id="55b92-180">**Functie Alias**: Voer `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="55b92-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="55b92-181">**Type functie**: Selecteer **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="55b92-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="55b92-182">**Optie importeren**: Selecteer **importeren uit een ander abonnement**.</span><span class="sxs-lookup"><span data-stu-id="55b92-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="55b92-183">**URL**: Voer Hallo WEBSERVICE-URL die u hebt genoteerd omlaag van Hallo Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="55b92-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="55b92-184">**Sleutel**: Voer Hallo TOEGANGSSLEUTEL die u hebt genoteerd omlaag van Hallo Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="55b92-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Een functie toohello Stream Analytics-taak niet toevoegen in Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="55b92-186">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="55b92-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="55b92-187">Hallo query van de Stream Analytics-taak Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="55b92-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="55b92-188">Onder **taak topologie**, klikt u op **Query**.</span><span class="sxs-lookup"><span data-stu-id="55b92-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="55b92-189">De bestaande code Hallo vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="55b92-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="55b92-190">Vervang `[YourInputAlias]` met alias van de taak Hallo Hallo invoer.</span><span class="sxs-lookup"><span data-stu-id="55b92-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="55b92-191">Vervang `[YourOutputAlias]` met Hallo uitvoeralias van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="55b92-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="55b92-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="55b92-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="55b92-193">Hallo Stream Analytics-taak uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="55b92-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="55b92-194">Klik in het Hallo-Stream Analytics-taak op **Start** > **nu** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="55b92-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="55b92-195">Zodra het Hallo-taak is gestart, Hallo taakstatus verandert van **gestopt** te**met**.</span><span class="sxs-lookup"><span data-stu-id="55b92-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Hallo Stream Analytics-taak uitgevoerd](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="55b92-197">Microsoft Azure Storage Explorer tooview Hallo weer prognose gebruiken</span><span class="sxs-lookup"><span data-stu-id="55b92-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="55b92-198">Voer Hallo client toepassing toostart verzamelen en verzenden van temperatuur en vochtigheid gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="55b92-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="55b92-199">Voor elk bericht dat uw IoT-hub ontvangt, roept Hallo Stream Analytics-taak Hallo weer prognose web service tooproduce Hallo kans regen.</span><span class="sxs-lookup"><span data-stu-id="55b92-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="55b92-200">Hallo resultaat wordt vervolgens opgeslagen tooyour Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="55b92-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="55b92-201">Azure Storage Explorer is een hulpprogramma waarmee u tooview Hallo resultaat kunt.</span><span class="sxs-lookup"><span data-stu-id="55b92-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="55b92-202">[Download en installeer Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="55b92-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="55b92-203">Open Azure Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="55b92-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="55b92-204">Meld u aan tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="55b92-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="55b92-205">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="55b92-205">Select your subscription.</span></span>
1. <span data-ttu-id="55b92-206">Klik op uw abonnement > **Opslagaccounts** > uw storage-account > **Blob-Containers** > uw container.</span><span class="sxs-lookup"><span data-stu-id="55b92-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="55b92-207">Open een .csv-bestand toosee Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="55b92-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="55b92-208">de laatste kolom records Hallo Hallo kans regen.</span><span class="sxs-lookup"><span data-stu-id="55b92-208">hello last column records hello chance of rain.</span></span>

   ![Resultaat van de prognose weer met Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="55b92-210">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="55b92-210">Summary</span></span>

<span data-ttu-id="55b92-211">U hebt Azure Machine Learning tooproduce Hallo kans op basis van Hallo temperatuur en vochtigheid gegevens die uw IoT-hub ontvangt regen is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="55b92-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]