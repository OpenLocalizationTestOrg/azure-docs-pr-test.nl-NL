---
title: "Realtime gegevensvisualisatie van sensorgegevens uit uw Azure-IoT-hub – Web-Apps | Microsoft Docs"
description: Gebruik de functie Web Apps van Microsoft Azure App Service voor het visualiseren van temperatuur en vochtigheid gegevens die worden verzameld van de sensor en verzonden naar uw Iot-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: realtime gegevensvisualisatie, live gegevensvisualisatie, sensor gegevensvisualisatie
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="8a502-104">Realtime-sensorgegevens uit uw Azure-IoT-hub visualiseren met behulp van de functie Web Apps van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8a502-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="8a502-106">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="8a502-106">What you learn</span></span>

<span data-ttu-id="8a502-107">In deze zelfstudie leert u hoe voor het visualiseren van realtime-sensorgegevens die uw IoT-hub ontvangt door het uitvoeren van een webtoepassing die wordt gehost op een web-app.</span><span class="sxs-lookup"><span data-stu-id="8a502-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="8a502-108">Als u wilt proberen de gegevens in uw IoT-hub visualiseren met behulp van Power BI, Zie [gebruik Power BI voor het visualiseren van realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="8a502-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8a502-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="8a502-109">What you do</span></span>

- <span data-ttu-id="8a502-110">Een web-app maken in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8a502-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="8a502-111">Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8a502-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="8a502-112">Configureer de web-app voor het lezen van sensorgegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a502-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="8a502-113">Upload een webtoepassing worden gehost door de web-app.</span><span class="sxs-lookup"><span data-stu-id="8a502-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="8a502-114">Open de web-app om realtime temperatuur en vochtigheid gegevens uit uw IoT-hub te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8a502-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8a502-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8a502-115">What you need</span></span>

- <span data-ttu-id="8a502-116">[Instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md), die wordt ingegaan op de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="8a502-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="8a502-117">Een actief Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="8a502-117">An active Azure subscription</span></span>
  - <span data-ttu-id="8a502-118">Een Iot-hub in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="8a502-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="8a502-119">Een clienttoepassing die berichten naar uw Iot-hub verzendt</span><span class="sxs-lookup"><span data-stu-id="8a502-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="8a502-120">Git downloaden</span><span class="sxs-lookup"><span data-stu-id="8a502-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="8a502-121">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="8a502-121">Create a web app</span></span>

1. <span data-ttu-id="8a502-122">In de [Azure-portal](https://ms.portal.azure.com/), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.</span><span class="sxs-lookup"><span data-stu-id="8a502-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="8a502-123">Voer een unieke naam, Controleer of het abonnement, geeft u een resourcegroep en een locatie, selecteer **vastmaken aan dashboard**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8a502-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="8a502-124">Het is raadzaam dat u dezelfde locatie als die van de resourcegroep selecteren.</span><span class="sxs-lookup"><span data-stu-id="8a502-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="8a502-125">In dat geval helpt bij het verwerken van de snelheid en beperkt de kosten van de gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="8a502-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![Een webtoepassing maken](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="8a502-127">De web-app voor het lezen van gegevens uit uw IoT-hub configureren</span><span class="sxs-lookup"><span data-stu-id="8a502-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="8a502-128">Open de web-app die u zojuist hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="8a502-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="8a502-129">Klik op **toepassingsinstellingen**, en klik vervolgens onder **appinstellingen**, voeg de volgende sleutel-waardeparen:</span><span class="sxs-lookup"><span data-stu-id="8a502-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="8a502-130">Sleutel</span><span class="sxs-lookup"><span data-stu-id="8a502-130">Key</span></span>                                   | <span data-ttu-id="8a502-131">Waarde</span><span class="sxs-lookup"><span data-stu-id="8a502-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="8a502-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="8a502-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="8a502-133">Verkregen van iothub explorer</span><span class="sxs-lookup"><span data-stu-id="8a502-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="8a502-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="8a502-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="8a502-135">De naam van de consumergroep die u aan uw IoT-hub toevoegt</span><span class="sxs-lookup"><span data-stu-id="8a502-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![Instellingen toevoegen aan uw web-app met sleutel-waardeparen](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="8a502-137">Klik op **toepassingsinstellingen**onder **algemene instellingen**, schakelen tussen de **Web-sockets** optie en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8a502-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![Stel de optie Web-sockets](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="8a502-139">Een webtoepassing worden gehost door de web-app uploaden</span><span class="sxs-lookup"><span data-stu-id="8a502-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="8a502-140">Op GitHub, hebben we aangebracht beschikbaar een webtoepassing die wordt weergegeven van realtime-sensorgegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a502-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="8a502-141">U hoeft alleen is de web-app voor het werken met een Git-opslagplaats, de webtoepassing vanuit GitHub downloaden en vervolgens uploaden naar Azure voor de web-app naar host configureren.</span><span class="sxs-lookup"><span data-stu-id="8a502-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="8a502-142">Klik in de web-app op **implementatieopties** > **bron kiezen** > **lokale Git-opslagplaats**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a502-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configureren van uw web-app-implementatie voor het gebruik van de lokale Git-opslagplaats](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="8a502-144">Klik op **Implementatiereferenties**, maak een gebruikersnaam en wachtwoord om verbinding maken met de Git-opslagplaats in Azure, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8a502-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="8a502-145">Klik op **overzicht**, en noteer de waarde van **Git kloon-url**.</span><span class="sxs-lookup"><span data-stu-id="8a502-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![Ophalen van de Git-kloon-URL van uw web-app](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="8a502-147">Open een opdracht of een terminalvenster op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8a502-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="8a502-148">De web-app vanuit GitHub downloaden en dit uploaden naar Azure voor de web-app naar host.</span><span class="sxs-lookup"><span data-stu-id="8a502-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="8a502-149">Voer de volgende opdrachten om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="8a502-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="8a502-150">\<GIT kloon-URL\> is de URL van de Git-opslagplaats gevonden op de **overzicht** pagina van de web-app.</span><span class="sxs-lookup"><span data-stu-id="8a502-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="8a502-151">Open de web-app om realtime temperatuur en vochtigheid gegevens uit uw IoT-hub te bekijken</span><span class="sxs-lookup"><span data-stu-id="8a502-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="8a502-152">Op de **overzicht** pagina van uw web-app klikt u op de URL voor het openen van de web-app.</span><span class="sxs-lookup"><span data-stu-id="8a502-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![Ophalen van de URL van uw web-app](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="8a502-154">U ziet de real-time temperatuur en vochtigheid gegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a502-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![Web-app-pagina met realtime temperatuur en vochtigheid](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="8a502-156">Controleer dat de voorbeeldtoepassing op uw apparaat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8a502-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="8a502-157">Als u niet het geval is, ontvangt u een lege grafiek, raadpleegt u de zelfstudies onder [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a502-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a502-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a502-158">Next steps</span></span>
<span data-ttu-id="8a502-159">U hebt uw web-app is gebruikt voor het visualiseren van realtime-sensorgegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8a502-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="8a502-160">Zie voor een andere manier om gegevens uit Azure IoT Hub te visualiseren [gebruik Power BI voor het visualiseren van realtime-sensorgegevens uit uw IoT-hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="8a502-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
