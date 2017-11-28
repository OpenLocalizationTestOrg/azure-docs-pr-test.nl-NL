---
title: Weer prognose met Azure Machine Learning met gegevens uit IoT Hub | Microsoft Docs
description: Gebruik Azure Machine Learning de kans op regen voorspellen op basis van de temperatuur en vochtigheid die uw IoT-hub uit een sensor verzamelt.
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
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="8a421-104">Weer voorspellen met behulp van de sensorgegevens uit uw IoT-hub in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8a421-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="8a421-106">Machine learning is een techniek voor gegevenswetenschap waarmee computers leren van bestaande gegevens te voorspellen van toekomstige gedrag, resultaten en trends.</span><span class="sxs-lookup"><span data-stu-id="8a421-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="8a421-107">Azure Machine Learning is een cloudservice voor predictive analytics waarmee u snel voorspellende modellen kunt maken en implementeren als analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="8a421-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="8a421-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="8a421-108">What you learn</span></span>

<span data-ttu-id="8a421-109">U leert hoe u met Azure Machine Learning weerbericht prognose (kans regen) met behulp van de temperatuur en vochtigheid gegevens van uw Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a421-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="8a421-110">De kans op regen is de uitvoer van een model van de voorspelling voorbereide weer.</span><span class="sxs-lookup"><span data-stu-id="8a421-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="8a421-111">Het model is gebaseerd op historische gegevens te voorspellen op basis van temperatuur en vochtigheid regen kans.</span><span class="sxs-lookup"><span data-stu-id="8a421-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8a421-112">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="8a421-112">What you do</span></span>

- <span data-ttu-id="8a421-113">Het model van de voorspelling weer als een webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="8a421-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="8a421-114">Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8a421-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="8a421-115">Een Stream Analytics-taak maken en configureren van de taak is:</span><span class="sxs-lookup"><span data-stu-id="8a421-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="8a421-116">Temperatuur en vochtigheid gegevens lezen uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a421-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="8a421-117">De webservice om de kans op regen aanroept.</span><span class="sxs-lookup"><span data-stu-id="8a421-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="8a421-118">Het resultaat opslaan naar een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="8a421-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="8a421-119">Microsoft Azure Storage Explorer gebruiken om weer te geven van de prognose weer.</span><span class="sxs-lookup"><span data-stu-id="8a421-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8a421-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8a421-120">What you need</span></span>

- <span data-ttu-id="8a421-121">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die wordt ingegaan op de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="8a421-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="8a421-122">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a421-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="8a421-123">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a421-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="8a421-124">Een clienttoepassing dat berichten naar uw Azure-IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="8a421-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="8a421-125">Een Azure Machine Learning Studio-account.</span><span class="sxs-lookup"><span data-stu-id="8a421-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="8a421-126">([Machine Learning Studio gratis proberen](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="8a421-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="8a421-127">Het model van de voorspelling weer als een webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="8a421-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="8a421-128">Ga naar de [weer voorspelling modelpagina](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="8a421-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="8a421-129">Klik op **openen in Studio** in Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8a421-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="8a421-130">![Open de weer voorspelling modelpagina in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="8a421-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="8a421-131">Klik op **uitvoeren** valideren van de stappen in het model.</span><span class="sxs-lookup"><span data-stu-id="8a421-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="8a421-132">Deze stap kan twee minuten duren.</span><span class="sxs-lookup"><span data-stu-id="8a421-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="8a421-133">![Open het model van de voorspelling weer in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="8a421-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="8a421-134">Klik op **instellen van WEBSERVICE** > **voorspellende webservice**.</span><span class="sxs-lookup"><span data-stu-id="8a421-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="8a421-135">![Het model van de voorspelling weer in Azure Machine Learning Studio implementeren](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="8a421-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="8a421-136">In het diagram, sleept u de **Web service invoer** module ergens in de buurt van de **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="8a421-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="8a421-137">Verbinding maken met de **Web service invoer** module die u wilt de **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="8a421-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="8a421-138">![Verbinding maken met twee modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="8a421-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="8a421-139">Klik op **uitvoeren** valideren van de stappen in het model.</span><span class="sxs-lookup"><span data-stu-id="8a421-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="8a421-140">Klik op **WEBSERVICE implementeren** voor het implementeren van het model als een webservice.</span><span class="sxs-lookup"><span data-stu-id="8a421-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="8a421-141">Op het dashboard van het model, downloaden de **Excel 2010 of ouder werkmap** voor **aanvraag/antwoord**.</span><span class="sxs-lookup"><span data-stu-id="8a421-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="8a421-142">Zorg ervoor dat u downloadt de **Excel 2010 of ouder werkmap** zelfs als u een nieuwere versie van Excel worden uitgevoerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8a421-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![De Excel voor het eindpunt REQUEST RESPONSE downloaden](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="8a421-144">Open de Excel-werkmap, noteert u de **URL van WEBSERVICE** en **TOEGANGSSLEUTEL**.</span><span class="sxs-lookup"><span data-stu-id="8a421-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="8a421-145">Maken, configureren en uitvoeren van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="8a421-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="8a421-146">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="8a421-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="8a421-147">In de [Azure-portal](https://ms.portal.azure.com/), klikt u op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.</span><span class="sxs-lookup"><span data-stu-id="8a421-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="8a421-148">Voer de volgende informatie voor de taak.</span><span class="sxs-lookup"><span data-stu-id="8a421-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="8a421-149">**Taaknaam**: de naam van de taak.</span><span class="sxs-lookup"><span data-stu-id="8a421-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="8a421-150">De naam moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="8a421-150">The name must be globally unique.</span></span>

   <span data-ttu-id="8a421-151">**Resourcegroep**: gebruik dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a421-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="8a421-152">**Locatie**: gebruik dezelfde locatie als uw resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8a421-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="8a421-153">**Vastmaken aan dashboard**: Schakel deze optie voor eenvoudige toegang naar uw IoT-hub vanuit het dashboard.</span><span class="sxs-lookup"><span data-stu-id="8a421-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Een Stream Analytics-taak maken in Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="8a421-155">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a421-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="8a421-156">Invoer voor de Stream Analytics-taak toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a421-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="8a421-157">Open de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="8a421-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="8a421-158">Onder **taak topologie**, klikt u op **invoer**.</span><span class="sxs-lookup"><span data-stu-id="8a421-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="8a421-159">In de **invoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8a421-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="8a421-160">**Invoeralias**: de alias die uniek zijn voor de invoer.</span><span class="sxs-lookup"><span data-stu-id="8a421-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="8a421-161">**Bron**: Selecteer **IoT-hub**.</span><span class="sxs-lookup"><span data-stu-id="8a421-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="8a421-162">**Consumergroep**: Selecteer de consumergroep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8a421-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Invoer voor de Stream Analytics-taak toevoegen in Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="8a421-164">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a421-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="8a421-165">Uitvoer toevoegen aan Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="8a421-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="8a421-166">Onder **taak topologie**, klikt u op **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="8a421-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="8a421-167">In de **uitvoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8a421-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="8a421-168">**Uitvoeraliassen**: de alias die uniek zijn voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="8a421-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="8a421-169">**Sink**: Selecteer **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="8a421-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="8a421-170">**Storage-account**: het storage-account voor de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8a421-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="8a421-171">U kunt een opslagaccount maken of een bestaande gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a421-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="8a421-172">**Container**: de container waarin de blob is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8a421-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="8a421-173">U kunt een container maken of een bestaande gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a421-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="8a421-174">**Gebeurtenis serialisatie-indeling**: Selecteer **CSV**.</span><span class="sxs-lookup"><span data-stu-id="8a421-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Uitvoer toevoegen aan Stream Analytics-taak in Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="8a421-176">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a421-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="8a421-177">Een functie toevoegen aan de Stream Analytics-taak voor het aanroepen van de webservice die u hebt geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="8a421-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="8a421-178">Onder **taak topologie**, klikt u op **functies** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8a421-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="8a421-179">Voer de volgende informatie in:</span><span class="sxs-lookup"><span data-stu-id="8a421-179">Enter the following information:</span></span>

   <span data-ttu-id="8a421-180">**Functie Alias**: Voer `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="8a421-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="8a421-181">**Type functie**: Selecteer **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="8a421-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="8a421-182">**Optie importeren**: Selecteer **importeren uit een ander abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8a421-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="8a421-183">**URL**: Voer de URL van de WEBSERVICE die u hebt genoteerd omlaag uit de Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="8a421-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="8a421-184">**Sleutel**: Voer de TOEGANGSSLEUTEL die u hebt genoteerd af van de Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="8a421-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Een functie toevoegen aan Stream Analytics-taak in Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="8a421-186">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a421-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="8a421-187">De query van de Stream Analytics-taak configureren</span><span class="sxs-lookup"><span data-stu-id="8a421-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="8a421-188">Onder **taak topologie**, klikt u op **Query**.</span><span class="sxs-lookup"><span data-stu-id="8a421-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="8a421-189">Vervang de bestaande code door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="8a421-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="8a421-190">Vervang `[YourInputAlias]` met de ingevoerde alias van de taak.</span><span class="sxs-lookup"><span data-stu-id="8a421-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="8a421-191">Vervang `[YourOutputAlias]` met de uitvoeralias van de taak.</span><span class="sxs-lookup"><span data-stu-id="8a421-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="8a421-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8a421-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="8a421-193">De Stream Analytics-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8a421-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="8a421-194">Klik in de Stream Analytics-taak op **Start** > **nu** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="8a421-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="8a421-195">Zodra de taak kan worden gestart, wordt de taakstatus verandert van **gestopt** naar **met**.</span><span class="sxs-lookup"><span data-stu-id="8a421-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![De Stream Analytics-taak uitvoeren](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="8a421-197">Microsoft Azure Storage Explorer gebruiken om weer te geven van de prognose weer</span><span class="sxs-lookup"><span data-stu-id="8a421-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="8a421-198">Voer de clienttoepassing om te beginnen met het verzamelen en verzenden van temperatuur en vochtigheid gegevens naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a421-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="8a421-199">Voor elk bericht dat uw IoT-hub ontvangt, roept de Stream Analytics-taak de webservice voor de prognose weer om de kans op regen produceren.</span><span class="sxs-lookup"><span data-stu-id="8a421-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="8a421-200">Het resultaat wordt vervolgens opgeslagen in de Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8a421-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="8a421-201">Azure Storage Explorer is een hulpprogramma dat u gebruiken kunt om het resultaat weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8a421-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="8a421-202">[Download en installeer Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8a421-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="8a421-203">Open Azure Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="8a421-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="8a421-204">Aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8a421-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="8a421-205">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a421-205">Select your subscription.</span></span>
1. <span data-ttu-id="8a421-206">Klik op uw abonnement > **Opslagaccounts** > uw storage-account > **Blob-Containers** > uw container.</span><span class="sxs-lookup"><span data-stu-id="8a421-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="8a421-207">Open een CSV-bestand om het resultaat te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8a421-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="8a421-208">De laatste kolom registreert de kans op regen.</span><span class="sxs-lookup"><span data-stu-id="8a421-208">The last column records the chance of rain.</span></span>

   ![Resultaat van de prognose weer met Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="8a421-210">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8a421-210">Summary</span></span>

<span data-ttu-id="8a421-211">U hebt Azure Machine Learning is gebruikt voor het produceren van de kans op regen op basis van de temperatuur en vochtigheid gegevens die uw IoT-hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="8a421-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]