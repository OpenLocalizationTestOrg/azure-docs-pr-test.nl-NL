---
title: aaaSave tooAzure gegevensopslag met berichten voor uw iothub | Microsoft Docs
description: Gebruik een Azure-functie app-toosave uw IoT hub berichten tooyour Azure-tabelopslag. Hallo IoT hub berichten bevatten informatie, zoals sensorgegevens dat wordt verzonden door uw IoT-apparaat.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-gegevensopslag, gegevensopslag iot-temperatuursensor
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="42afa-105">Opslaan van IoT hub berichten met sensor gegevens tooyour Azure-tabelopslag</span><span class="sxs-lookup"><span data-stu-id="42afa-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="42afa-107">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="42afa-107">What you learn</span></span>

<span data-ttu-id="42afa-108">U leert hoe werken app toostore IoT hub berichten in uw tabelopslag toocreate Azure storage-account en een Azure.</span><span class="sxs-lookup"><span data-stu-id="42afa-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="42afa-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="42afa-109">What you do</span></span>

- <span data-ttu-id="42afa-110">Een Azure-opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="42afa-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="42afa-111">Bereid uw IoT-hub verbindingsberichten tooread.</span><span class="sxs-lookup"><span data-stu-id="42afa-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="42afa-112">Maken en implementeren van een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="42afa-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="42afa-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="42afa-113">What you need</span></span>

- <span data-ttu-id="42afa-114">[Instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) toocover Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="42afa-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="42afa-115">Een actief Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="42afa-115">An active Azure subscription</span></span>
  - <span data-ttu-id="42afa-116">Een IoT-hub in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="42afa-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="42afa-117">Een actieve toepassing waarmee berichten tooyour iothub worden verzonden</span><span class="sxs-lookup"><span data-stu-id="42afa-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="42afa-118">Een Azure-opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="42afa-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="42afa-119">In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **opslag** > **opslagaccount**  >   **Maak**.</span><span class="sxs-lookup"><span data-stu-id="42afa-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="42afa-120">Voer Hallo benodigde gegevens voor het Hallo-opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="42afa-120">Enter hello necessary information for hello storage account:</span></span>

   ![Een opslagaccount maken in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="42afa-122">**Naam**: Hallo-naam van Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="42afa-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="42afa-123">Hallo-naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="42afa-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="42afa-124">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42afa-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="42afa-125">**Pincode toodashboard**: Selecteer deze optie voor eenvoudige toegang tooyour iothub uit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="42afa-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="42afa-126">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="42afa-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="42afa-127">Voorbereiden van uw IoT-hub tooread verbindingsberichten</span><span class="sxs-lookup"><span data-stu-id="42afa-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="42afa-128">IoT-hub toont een ingebouwde event hub-compatibele eindpunt tooenable toepassingen tooread IoT hub-berichten.</span><span class="sxs-lookup"><span data-stu-id="42afa-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="42afa-129">Ondertussen toepassingen groepen tooread consumentgegevens uit uw IoT-hub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42afa-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="42afa-130">Voordat u een Azure-functie app-tooread gegevens uit uw IoT-hub maakt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="42afa-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="42afa-131">De verbindingsreeks Hallo van uw IoT-hubeindpunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="42afa-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="42afa-132">Maak een consumergroep voor uw iothub.</span><span class="sxs-lookup"><span data-stu-id="42afa-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="42afa-133">De verbindingsreeks Hallo van uw IoT-hubeindpunt ophalen</span><span class="sxs-lookup"><span data-stu-id="42afa-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="42afa-134">Open uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42afa-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="42afa-135">Op Hallo **IoT Hub** deelvenster onder **Messaging**, klikt u op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="42afa-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="42afa-136">In Hallo rechtermuisknop deelvenster onder **ingebouwde eindpunten**, klikt u op **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="42afa-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="42afa-137">In Hallo **eigenschappen** deelvenster, opmerking Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="42afa-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="42afa-138">Event hub-compatibele eindpunt</span><span class="sxs-lookup"><span data-stu-id="42afa-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="42afa-139">Event hub-compatibele naam</span><span class="sxs-lookup"><span data-stu-id="42afa-139">Event hub-compatible name</span></span>

   ![Ophalen van de verbindingsreeks Hallo van uw IoT-hubeindpunt in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="42afa-141">In Hallo **IoT Hub** deelvenster onder **instellingen**, klikt u op **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="42afa-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="42afa-142">Klik op **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="42afa-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="42afa-143">Opmerking Hallo **primaire sleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="42afa-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="42afa-144">De verbindingsreeks Hallo van uw IoT-hubeindpunt als volgt maken:</span><span class="sxs-lookup"><span data-stu-id="42afa-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="42afa-145">Vervang `<Event Hub-compatible endpoint>` en `<Primary key>` met Hallo-waarden die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="42afa-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="42afa-146">Een consumergroep voor uw iothub maken</span><span class="sxs-lookup"><span data-stu-id="42afa-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="42afa-147">Open uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42afa-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="42afa-148">In Hallo **IoT Hub** deelvenster onder **Messaging**, klikt u op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="42afa-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="42afa-149">In Hallo rechtermuisknop deelvenster onder **ingebouwde eindpunten**, klikt u op **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="42afa-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="42afa-150">In Hallo **eigenschappen** deelvenster onder **consumergroepen**, voer een naam en maak een notitie ervan.</span><span class="sxs-lookup"><span data-stu-id="42afa-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="42afa-151">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42afa-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="42afa-152">Een Azure-functie-app maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="42afa-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="42afa-153">In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Compute** > **functie-App**  >   **Maak**.</span><span class="sxs-lookup"><span data-stu-id="42afa-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="42afa-154">Voer de vereiste gegevens Hallo voor Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="42afa-154">Enter hello necessary information for hello function app.</span></span>

   ![Een functie-app maken in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="42afa-156">**App-naam**: Hallo-naam van Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="42afa-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="42afa-157">Hallo-naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="42afa-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="42afa-158">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42afa-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="42afa-159">**Storage-Account**: Hallo storage-account dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="42afa-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="42afa-160">**Pincode toodashboard**: Schakel deze optie voor eenvoudige toegang toohello functie-app vanuit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="42afa-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="42afa-161">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="42afa-161">Click **Create**.</span></span>

4. <span data-ttu-id="42afa-162">Na de Hallo functie-app is gemaakt, opent u het.</span><span class="sxs-lookup"><span data-stu-id="42afa-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="42afa-163">Maak een nieuwe functie door Hallo volgende te doen in Hallo-functie-app:</span><span class="sxs-lookup"><span data-stu-id="42afa-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="42afa-164">a.</span><span class="sxs-lookup"><span data-stu-id="42afa-164">a.</span></span> <span data-ttu-id="42afa-165">Klik op **nieuwe functie**.</span><span class="sxs-lookup"><span data-stu-id="42afa-165">Click **New Function**.</span></span>

   <span data-ttu-id="42afa-166">b.</span><span class="sxs-lookup"><span data-stu-id="42afa-166">b.</span></span> <span data-ttu-id="42afa-167">Selecteer **JavaScript** voor **taal**, en **gegevensverwerking** voor **Scenario**.</span><span class="sxs-lookup"><span data-stu-id="42afa-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="42afa-168">c.</span><span class="sxs-lookup"><span data-stu-id="42afa-168">c.</span></span> <span data-ttu-id="42afa-169">Klik op **maken van deze functie**, en klik vervolgens op **nieuwe functie**.</span><span class="sxs-lookup"><span data-stu-id="42afa-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="42afa-170">d.</span><span class="sxs-lookup"><span data-stu-id="42afa-170">d.</span></span> <span data-ttu-id="42afa-171">Selecteer **JavaScript** voor Hallo-taal en **gegevensverwerking** voor Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="42afa-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="42afa-172">e.</span><span class="sxs-lookup"><span data-stu-id="42afa-172">e.</span></span> <span data-ttu-id="42afa-173">Klik op Hallo **EventHubTrigger JavaScript** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="42afa-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="42afa-174">f.</span><span class="sxs-lookup"><span data-stu-id="42afa-174">f.</span></span> <span data-ttu-id="42afa-175">Voer de vereiste gegevens Hallo voor Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="42afa-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="42afa-176">**Naam van de functie**: naam van de functie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="42afa-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="42afa-177">**Naam Event Hub**: Hallo event hub-compatibele naam die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="42afa-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="42afa-178">**Gebeurtenis-hubverbinding**: tooadd Hallo-verbindingsreeks van Hallo IoT-hubeindpunt die u hebt gemaakt, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="42afa-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="42afa-179">g.</span><span class="sxs-lookup"><span data-stu-id="42afa-179">g.</span></span> <span data-ttu-id="42afa-180">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="42afa-180">Click **Create**.</span></span>

6. <span data-ttu-id="42afa-181">Uitvoer van de functie Hallo configureren door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="42afa-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="42afa-182">a.</span><span class="sxs-lookup"><span data-stu-id="42afa-182">a.</span></span> <span data-ttu-id="42afa-183">Klik op **integreren** > **nieuwe uitvoer** > **Azure Table Storage** > **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="42afa-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Table storage tooyour functie-app toevoegen in hello Azure-portal](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="42afa-185">b.</span><span class="sxs-lookup"><span data-stu-id="42afa-185">b.</span></span> <span data-ttu-id="42afa-186">Voer de vereiste gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="42afa-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="42afa-187">**Parameter tabelnaam**: Gebruik `outputTable`, die wordt gebruikt in hello Azure van functie-code.</span><span class="sxs-lookup"><span data-stu-id="42afa-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="42afa-188">**Tabelnaam**: Gebruik `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="42afa-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="42afa-189">**Storage-account verbinding**: klik op **nieuw**, en selecteer of Voer uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="42afa-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="42afa-190">Als het Hallo-storage-account niet wordt weergegeven, raadpleegt u [account opslagvereisten](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="42afa-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="42afa-191">c.</span><span class="sxs-lookup"><span data-stu-id="42afa-191">c.</span></span> <span data-ttu-id="42afa-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42afa-192">Click **Save**.</span></span>

7. <span data-ttu-id="42afa-193">Onder **Triggers**, klikt u op **Azure Event Hub (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="42afa-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="42afa-194">Onder **Event Hub consumergroep**, voer de naam Hallo van consumentengroep Hallo dat u maakte en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42afa-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="42afa-195">Hallo-functie die u hebt gemaakt op Hallo links op en klik op **bestanden weergeven** op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="42afa-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="42afa-196">Vervang de code Hallo in `index.js` door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="42afa-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="42afa-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="42afa-197">Click **Save**.</span></span>

<span data-ttu-id="42afa-198">U hebt nu Hallo functie-app gemaakt.</span><span class="sxs-lookup"><span data-stu-id="42afa-198">You have now created hello function app.</span></span> <span data-ttu-id="42afa-199">Berichten die uw IoT-hub in tabelopslag ontvangt worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="42afa-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="42afa-200">U kunt Hallo **uitvoeren** knop tootest Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="42afa-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="42afa-201">Wanneer u klikt op **uitvoeren**, test het Hallo-bericht tooyour iothub wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="42afa-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="42afa-202">Hallo aankomst van het Hallo-bericht moet Hallo functie app toostart activeren en sla vervolgens Hallo-bericht tooyour tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="42afa-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="42afa-203">Hallo **logboeken** deelvenster Hallo details van Hallo proces vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="42afa-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="42afa-204">Controleer of het bericht in de tabelopslag</span><span class="sxs-lookup"><span data-stu-id="42afa-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="42afa-205">Hallo-voorbeeldtoepassing uitvoeren op uw apparaat toosend berichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42afa-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="42afa-206">[Download en installeer Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="42afa-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="42afa-207">Open Opslagverkenner, klik op **een Azure-Account toevoegen** > **aanmelden**, en vervolgens weer aanmelden tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="42afa-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="42afa-208">Klik op uw Azure-abonnement > **Opslagaccounts** > uw storage-account > **tabellen** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="42afa-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="42afa-209">U ziet dat berichten worden verzonden van uw apparaat tooyour IoT-hub Hallo aangemeld `deviceData` tabel.</span><span class="sxs-lookup"><span data-stu-id="42afa-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42afa-210">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42afa-210">Next steps</span></span>

<span data-ttu-id="42afa-211">U hebt gemaakt uw Azure storage-account en de Azure-functie-app, dat berichten worden opgeslagen die uw IoT-hub in de tabelopslag van uw ontvangt.</span><span class="sxs-lookup"><span data-stu-id="42afa-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
