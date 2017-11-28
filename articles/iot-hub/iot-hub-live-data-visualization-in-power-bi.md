---
title: "aaaReal tijd gegevensvisualisatie van sensorgegevens uit Azure IoT Hub – Power BI | Microsoft Docs"
description: Gebruik Power BI toovisualize temperatuur en vochtigheid gegevens die worden verzameld van Hallo sensor en tooyour Azure IoT hub wordt verzonden.
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
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="b1eb9-104">Realtime-sensorgegevens uit Azure IoT Hub met Power BI visualiseren</span><span class="sxs-lookup"><span data-stu-id="b1eb9-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="b1eb9-106">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="b1eb9-106">What you learn</span></span>

<span data-ttu-id="b1eb9-107">U leert hoe toovisualize realtime-sensorgegevens die uw Azure-IoT-hub ontvangt door Power BI.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="b1eb9-108">Als u wilt dat tootry Hallo gegevens visualiseren in uw iothub met Web-Apps, Zie [gebruik Azure Web Apps toovisualize realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b1eb9-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b1eb9-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="b1eb9-109">What you do</span></span>

- <span data-ttu-id="b1eb9-110">Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="b1eb9-111">Maken, configureren en uitvoeren van een Stream Analytics-taak voor overdracht van gegevens uit uw IoT hub tooyour Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="b1eb9-112">Maken en publiceren van een Power BI toovisualize Hallo rapportgegevens.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b1eb9-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="b1eb9-113">What you need</span></span>

- <span data-ttu-id="b1eb9-114">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="b1eb9-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="b1eb9-115">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="b1eb9-116">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b1eb9-117">Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="b1eb9-118">Een Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-118">A Power BI account.</span></span> <span data-ttu-id="b1eb9-119">([Probeer Power BI gratis](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="b1eb9-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="b1eb9-120">Maken, configureren en uitvoeren van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="b1eb9-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="b1eb9-121">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="b1eb9-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="b1eb9-122">In Azure-portal Hallo, klikt u op Nieuw > Internet der dingen > Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="b1eb9-123">Voer Hallo informatie voor de taak hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="b1eb9-124">**Taaknaam**: Hallo-naam van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="b1eb9-125">Hallo-naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="b1eb9-126">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="b1eb9-127">**Locatie**: gebruik Hallo dezelfde locatie als de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="b1eb9-128">**Pincode toodashboard**: Schakel deze optie voor eenvoudige toegang tooyour iothub uit het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Een Stream Analytics-taak maken in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="b1eb9-130">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="b1eb9-131">Toevoegen van een invoer toohello Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="b1eb9-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b1eb9-132">Open Hallo Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b1eb9-133">Onder **taak topologie**, klikt u op **invoer**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="b1eb9-134">In Hallo **invoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="b1eb9-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b1eb9-135">**Invoeralias**: Hallo unieke alias voor Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="b1eb9-136">**Bron**: Selecteer **IoT-hub**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="b1eb9-137">**Consumergroep**: Selecteer Hallo consumergroep u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="b1eb9-138">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-138">Click **Create**.</span></span>

   ![Toevoegen van een invoer tooa Stream Analytics-taak in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="b1eb9-140">Toevoegen van een uitvoer toohello Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="b1eb9-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b1eb9-141">Onder **taak topologie**, klikt u op **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="b1eb9-142">In Hallo **uitvoer** deelvenster, klikt u op **toevoegen**, en voer de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="b1eb9-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b1eb9-143">**Uitvoeraliassen**: Hallo unieke alias voor Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="b1eb9-144">**Sink**: Selecteer **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="b1eb9-145">Klik op **autoriseren**, en vervolgens meldt u zich bij uw Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="b1eb9-146">Na autorisatie, Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b1eb9-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="b1eb9-147">**Werkruimte groep**: Selecteer de groep doelwerkruimte.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="b1eb9-148">**Naam van DataSet**: Voer een gegevenssetnaam.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="b1eb9-149">**Tabelnaam**: Voer een tabelnaam.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="b1eb9-150">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-150">Click **Create**.</span></span>

   ![Een uitvoer tooa Stream Analytics-taak toevoegen in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="b1eb9-152">Hallo query van de Stream Analytics-taak Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="b1eb9-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="b1eb9-153">Onder **taak topologie**, klikt u op **Query**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="b1eb9-154">Vervang `[YourInputAlias]` met alias van de taak Hallo Hallo invoer.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="b1eb9-155">Vervang `[YourOutputAlias]` met Hallo uitvoeralias van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="b1eb9-156">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-156">Click **Save**.</span></span>

   ![Een query tooa Stream Analytics-taak niet toevoegen in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="b1eb9-158">Hallo Stream Analytics-taak uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="b1eb9-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="b1eb9-159">Klik in het Hallo-Stream Analytics-taak op **Start** > **nu** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="b1eb9-160">Zodra het Hallo-taak is gestart, Hallo taakstatus verandert van **gestopt** te**met**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Een Stream Analytics-taak uitgevoerd in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="b1eb9-162">Maken en publiceren van een Power BI toovisualize Hallo rapportgegevens</span><span class="sxs-lookup"><span data-stu-id="b1eb9-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="b1eb9-163">Controleer de voorbeeldtoepassing hello wordt uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="b1eb9-164">Als u niet het geval is, raadpleegt u de zelfstudies toohello onder [instellen van uw apparaat](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="b1eb9-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="b1eb9-165">Meld u aan tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="b1eb9-166">Ga toohello groep werkruimte die u hebt ingesteld toen u Hallo uitvoer voor Hallo Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b1eb9-167">Klik op **Streaming gegevenssets**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="b1eb9-168">U ziet de gegevensset Hallo vermeld die u hebt opgegeven toen u Hallo uitvoer voor Hallo Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b1eb9-169">Onder **acties**, klikt u op Hallo eerste pictogram toocreate een rapport.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Een Microsoft Power BI-rapport maken](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="b1eb9-171">Maak een regel grafiek tooshow realtime temperatuur gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="b1eb9-172">Voeg een lijndiagram op Hallo-rapportpagina maken.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="b1eb9-173">Op Hallo **velden** deelvenster Vouw Hallo tabel die u hebt opgegeven toen u Hallo uitvoer voor Hallo Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="b1eb9-174">Sleep **EventEnqueuedUtcTime** te**as** op Hallo **visualisaties** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="b1eb9-175">Sleep **temperatuur** te**waarden**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="b1eb9-176">Nu wordt een lijndiagram gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-176">Now a line chart is created.</span></span> <span data-ttu-id="b1eb9-177">Hallo x-as geeft de datum en tijd in UTC-tijdzone Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="b1eb9-178">Hallo y-as worden temperatuur van Hallo sensor weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Toevoegen van een lijndiagram voor temperatuur tooa Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="b1eb9-180">Maak een andere regel grafiek tooshow realtime vochtigheid gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="b1eb9-181">toodo, volgt u dezelfde hierboven stappen Hallo op en plaats **EventEnqueuedUtcTime** op Hallo x-as en **vochtigheid** op Hallo y-as.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Toevoegen van een lijndiagram voor vochtigheid tooa Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="b1eb9-183">Klik op **opslaan** toosave Hallo rapport.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="b1eb9-184">Klik op **bestand** > **tooweb publiceren**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="b1eb9-185">Klik op **invoegcode maken**, en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="b1eb9-186">U bent Hallo rapportkoppeling die u met iemand voor toegang tot rapporten en een code codefragment toointegrate Hallo rapport in uw blog of website delen kunt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Publiceren van een Microsoft Power BI-rapport](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="b1eb9-188">Microsoft biedt ook Hallo [mobiele apps van Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) voor het weergeven en interactie met uw Power BI-dashboards en rapporten op je mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1eb9-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1eb9-189">Next steps</span></span>

<span data-ttu-id="b1eb9-190">U hebt Power BI toovisualize realtime-sensorgegevens met succes van uw Azure-IoT-hub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="b1eb9-191">Er is een andere manier toovisualize-gegevens van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b1eb9-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="b1eb9-192">Zie [gebruik Azure Web Apps toovisualize realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b1eb9-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
