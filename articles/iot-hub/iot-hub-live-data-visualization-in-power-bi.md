---
title: "Realtime gegevensvisualisatie van sensorgegevens uit Azure IoT Hub – Power BI | Microsoft Docs"
description: Gebruik Power BI om temperatuur en vochtigheid gegevens die worden verzameld van de sensor en verzonden naar uw Azure-IoT-hub te visualiseren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: realtime gegevensvisualisatie, live gegevensvisualisatie, sensor gegevensvisualisatie
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="3d89c-104">Realtime-sensorgegevens uit Azure IoT Hub met Power BI visualiseren</span><span class="sxs-lookup"><span data-stu-id="3d89c-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="3d89c-106">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="3d89c-106">What you learn</span></span>

<span data-ttu-id="3d89c-107">U leert hoe voor het visualiseren van realtime-sensorgegevens die uw Azure-IoT-hub ontvangt door Power BI.</span><span class="sxs-lookup"><span data-stu-id="3d89c-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="3d89c-108">Als u proberen de gegevens in uw IoT-hub met Web-Apps wilt, raadpleegt u [gebruik Azure Web Apps voor het visualiseren van realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3d89c-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3d89c-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="3d89c-109">What you do</span></span>

- <span data-ttu-id="3d89c-110">Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3d89c-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="3d89c-111">Maken, configureren en uitvoeren van een Stream Analytics-taak voor overdracht van gegevens uit uw IoT-hub aan uw Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="3d89c-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="3d89c-112">Maken en publiceren van een Power BI-rapport om de gegevens te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="3d89c-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3d89c-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="3d89c-113">What you need</span></span>

- <span data-ttu-id="3d89c-114">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die wordt ingegaan op de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="3d89c-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="3d89c-115">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3d89c-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="3d89c-116">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="3d89c-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="3d89c-117">Een clienttoepassing dat berichten naar uw Azure-IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="3d89c-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="3d89c-118">Een Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="3d89c-118">A Power BI account.</span></span> <span data-ttu-id="3d89c-119">([Probeer Power BI gratis](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="3d89c-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="3d89c-120">Maken, configureren en uitvoeren van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="3d89c-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="3d89c-121">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="3d89c-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="3d89c-122">Klik in de Azure-portal op Nieuw > Internet der dingen > Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="3d89c-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="3d89c-123">Voer de volgende informatie voor de taak.</span><span class="sxs-lookup"><span data-stu-id="3d89c-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="3d89c-124">**Taaknaam**: de naam van de taak.</span><span class="sxs-lookup"><span data-stu-id="3d89c-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="3d89c-125">De naam moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="3d89c-125">The name must be globally unique.</span></span>

   <span data-ttu-id="3d89c-126">**Resourcegroep**: gebruik dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d89c-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="3d89c-127">**Locatie**: gebruik dezelfde locatie als uw resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3d89c-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="3d89c-128">**Vastmaken aan dashboard**: Schakel deze optie voor eenvoudige toegang naar uw IoT-hub vanuit het dashboard.</span><span class="sxs-lookup"><span data-stu-id="3d89c-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Een Stream Analytics-taak maken in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="3d89c-130">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="3d89c-131">Invoer voor de Stream Analytics-taak toevoegen</span><span class="sxs-lookup"><span data-stu-id="3d89c-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="3d89c-132">Open de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="3d89c-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="3d89c-133">Onder **taak topologie**, klikt u op **invoer**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="3d89c-134">In de **invoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="3d89c-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="3d89c-135">**Invoeralias**: de alias die uniek zijn voor de invoer.</span><span class="sxs-lookup"><span data-stu-id="3d89c-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="3d89c-136">**Bron**: Selecteer **IoT-hub**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="3d89c-137">**Consumergroep**: Selecteer de consumergroep die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d89c-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="3d89c-138">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-138">Click **Create**.</span></span>

   ![Een invoer toevoegen aan Stream Analytics-taak in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="3d89c-140">Uitvoer toevoegen aan Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="3d89c-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="3d89c-141">Onder **taak topologie**, klikt u op **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="3d89c-142">In de **uitvoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="3d89c-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="3d89c-143">**Uitvoeraliassen**: de alias die uniek zijn voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3d89c-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="3d89c-144">**Sink**: Selecteer **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="3d89c-145">Klik op **autoriseren**, en vervolgens meldt u zich bij uw Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="3d89c-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="3d89c-146">Na autorisatie, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="3d89c-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="3d89c-147">**Werkruimte groep**: Selecteer de groep doelwerkruimte.</span><span class="sxs-lookup"><span data-stu-id="3d89c-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="3d89c-148">**Naam van DataSet**: Voer een gegevenssetnaam.</span><span class="sxs-lookup"><span data-stu-id="3d89c-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="3d89c-149">**Tabelnaam**: Voer een tabelnaam.</span><span class="sxs-lookup"><span data-stu-id="3d89c-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="3d89c-150">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-150">Click **Create**.</span></span>

   ![Uitvoer toevoegen aan een Stream Analytics-taak in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="3d89c-152">De query van de Stream Analytics-taak configureren</span><span class="sxs-lookup"><span data-stu-id="3d89c-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="3d89c-153">Onder **taak topologie**, klikt u op **Query**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="3d89c-154">Vervang `[YourInputAlias]` met de ingevoerde alias van de taak.</span><span class="sxs-lookup"><span data-stu-id="3d89c-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="3d89c-155">Vervang `[YourOutputAlias]` met de uitvoeralias van de taak.</span><span class="sxs-lookup"><span data-stu-id="3d89c-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="3d89c-156">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-156">Click **Save**.</span></span>

   ![Een query toevoegen aan een Stream Analytics-taak in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="3d89c-158">De Stream Analytics-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3d89c-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="3d89c-159">Klik in de Stream Analytics-taak op **Start** > **nu** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="3d89c-160">Zodra de taak kan worden gestart, wordt de taakstatus verandert van **gestopt** naar **met**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Een Stream Analytics-taak uitgevoerd in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="3d89c-162">Maken en publiceren van een Power BI-rapport om de gegevens te visualiseren</span><span class="sxs-lookup"><span data-stu-id="3d89c-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="3d89c-163">Controleer dat de voorbeeldtoepassing op uw apparaat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d89c-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="3d89c-164">Als u niet het geval is, raadpleegt u de zelfstudies onder [instellen van uw apparaat](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="3d89c-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="3d89c-165">Aanmelden bij uw [Power BI](https://powerbi.microsoft.com/en-us/) account.</span><span class="sxs-lookup"><span data-stu-id="3d89c-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="3d89c-166">Ga naar de werkruimte voor groep die u hebt ingesteld toen u de uitvoer voor de Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d89c-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="3d89c-167">Klik op **Streaming gegevenssets**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="3d89c-168">U ziet de vermelde gegevensset die u hebt opgegeven toen u de uitvoer voor de Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d89c-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="3d89c-169">Onder **acties**, klikt u op het eerste pictogram om een rapport te maken.</span><span class="sxs-lookup"><span data-stu-id="3d89c-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Een Microsoft Power BI-rapport maken](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="3d89c-171">Maak een lijndiagram om weer te geven van realtime temperatuur gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="3d89c-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="3d89c-172">Voeg een lijndiagram op de pagina rapport maken.</span><span class="sxs-lookup"><span data-stu-id="3d89c-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="3d89c-173">Op de **velden** deelvenster, vouw de tabel die u hebt opgegeven toen u de uitvoer voor de Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d89c-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="3d89c-174">Sleep **EventEnqueuedUtcTime** naar **as** op de **visualisaties** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="3d89c-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="3d89c-175">Sleep **temperatuur** naar **waarden**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="3d89c-176">Nu wordt een lijndiagram gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d89c-176">Now a line chart is created.</span></span> <span data-ttu-id="3d89c-177">De x-as geeft de datum en tijd in UTC-tijdzone.</span><span class="sxs-lookup"><span data-stu-id="3d89c-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="3d89c-178">De y-as worden temperatuur van de sensor weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3d89c-178">The y-axis displays temperature from the sensor.</span></span>

      ![Een lijndiagram voor temperatuur toevoegen aan een Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="3d89c-180">Maak een andere lijndiagram om weer te geven van realtime vochtigheid gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="3d89c-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="3d89c-181">U doet dit door dezelfde stappen hierboven en plaats **EventEnqueuedUtcTime** op de x-as en **vochtigheid** op de y-as.</span><span class="sxs-lookup"><span data-stu-id="3d89c-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Een lijndiagram voor vochtigheid toevoegen aan een Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="3d89c-183">Klik op **opslaan** het rapport wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="3d89c-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="3d89c-184">Klik op **bestand** > **publiceren op web**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="3d89c-185">Klik op **invoegcode maken**, en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="3d89c-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="3d89c-186">U hebt de rapportkoppeling hebt opgegeven dat u met iedereen voor toegang tot rapporten en een codefragment delen kunt aan het rapport integreren in uw blog of website.</span><span class="sxs-lookup"><span data-stu-id="3d89c-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Publiceren van een Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="3d89c-188">Microsoft biedt ook de [mobiele apps van Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) voor het weergeven en interactie met uw Power BI-dashboards en rapporten op je mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="3d89c-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d89c-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d89c-189">Next steps</span></span>

<span data-ttu-id="3d89c-190">U hebt Power BI is gebruikt voor het visualiseren van realtime-sensorgegevens uit uw Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d89c-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="3d89c-191">Er is een andere manier om gegevens uit Azure IoT Hub te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="3d89c-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="3d89c-192">Zie [gebruik Azure Web Apps voor het visualiseren van realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3d89c-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
