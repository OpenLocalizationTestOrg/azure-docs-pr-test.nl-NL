---
title: "aaaReal tijd gegevensvisualisatie van sensorgegevens uit uw Azure-IoT-hub – Web-Apps | Microsoft Docs"
description: Hallo-Web-Apps van Microsoft Azure App Service toovisualize temperatuur en vochtigheid gegevens die worden verzameld van Hallo sensor en verzonden tooyour Iot-hub gebruiken.
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
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="51985-104">Realtime-sensorgegevens uit uw Azure-IoT-hub visualiseren met behulp van de functie voor Hallo-Web-Apps van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="51985-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="51985-106">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="51985-106">What you learn</span></span>

<span data-ttu-id="51985-107">In deze zelfstudie leert u hoe toovisualize realtime-sensorgegevens die uw IoT-hub ontvangt door het uitvoeren van een webtoepassing die wordt gehost op een web-app.</span><span class="sxs-lookup"><span data-stu-id="51985-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="51985-108">Als u tootry toovisualize Hallo gegevens in uw iothub wilt met behulp van Power BI, Zie [gebruik Power BI toovisualize realtime-sensorgegevens uit Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="51985-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="51985-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="51985-109">What you do</span></span>

- <span data-ttu-id="51985-110">Een web-app maken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="51985-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="51985-111">Bereid uw IoT-hub voor toegang tot gegevens door een consumergroep toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="51985-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="51985-112">Configureer Hallo web app tooread sensor-gegevens van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="51985-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="51985-113">Een web application toobe gehost door Hallo web-app uploaden.</span><span class="sxs-lookup"><span data-stu-id="51985-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="51985-114">Open Hallo web app toosee realtime temperatuur en vochtigheid gegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="51985-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="51985-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="51985-115">What you need</span></span>

- <span data-ttu-id="51985-116">[Instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md), die wordt ingegaan op Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="51985-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="51985-117">Een actief Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="51985-117">An active Azure subscription</span></span>
  - <span data-ttu-id="51985-118">Een Iot-hub in uw abonnement</span><span class="sxs-lookup"><span data-stu-id="51985-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="51985-119">Een clienttoepassing die berichten tooyour Iot-hub verzendt</span><span class="sxs-lookup"><span data-stu-id="51985-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="51985-120">Git downloaden</span><span class="sxs-lookup"><span data-stu-id="51985-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="51985-121">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="51985-121">Create a web app</span></span>

1. <span data-ttu-id="51985-122">In Hallo [Azure-portal](https://ms.portal.azure.com/), klikt u op **nieuw** > **Web en mobiel** > **Web-App**.</span><span class="sxs-lookup"><span data-stu-id="51985-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="51985-123">Voer een unieke Taaknaam, Hallo abonnement controleren, Geef een resourcegroep en een locatie, selecteer **pincode toodashboard**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="51985-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="51985-124">Het is raadzaam dat u Hallo selecteert dezelfde locatie bevinden als die van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="51985-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="51985-125">In dat geval helpt bij het verwerken van de snelheid en vermindert Hallo kosten voor gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="51985-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Een webtoepassing maken](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="51985-127">Hallo web app tooread-gegevens van uw IoT-hub configureren</span><span class="sxs-lookup"><span data-stu-id="51985-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="51985-128">Open Hallo-webtoepassing die u zojuist hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="51985-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="51985-129">Klik op **toepassingsinstellingen**, en klik vervolgens onder **appinstellingen**, toevoegen Hallo sleutel/waarde-paren te volgen:</span><span class="sxs-lookup"><span data-stu-id="51985-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="51985-130">Sleutel</span><span class="sxs-lookup"><span data-stu-id="51985-130">Key</span></span>                                   | <span data-ttu-id="51985-131">Waarde</span><span class="sxs-lookup"><span data-stu-id="51985-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="51985-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="51985-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="51985-133">Verkregen van iothub explorer</span><span class="sxs-lookup"><span data-stu-id="51985-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="51985-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="51985-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="51985-135">Hallo-naam van consumentengroep hello tooyour IoT-hub toe te voegen</span><span class="sxs-lookup"><span data-stu-id="51985-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Instellingen tooyour web-app met sleutel-waardeparen toevoegen](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="51985-137">Klik op **toepassingsinstellingen**onder **algemene instellingen**, in-/ uitschakelen Hallo **Web-sockets** optie en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="51985-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Stel Hallo Web sockets optie](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="51985-139">Een web application toobe gehost door Hallo web-app uploaden</span><span class="sxs-lookup"><span data-stu-id="51985-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="51985-140">Op GitHub, hebben we aangebracht beschikbaar een webtoepassing die wordt weergegeven van realtime-sensorgegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="51985-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="51985-141">Toodo hoeft u Hallo web app toowork configureren met een Git-opslagplaats en upload het tooAzure voor Hallo web app toohost Hallo webtoepassing vanuit GitHub downloaden.</span><span class="sxs-lookup"><span data-stu-id="51985-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="51985-142">Klik in het Hallo-web-app op **implementatieopties** > **bron kiezen** > **lokale Git-opslagplaats**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="51985-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Configureren van uw web-app-implementatie toouse Hallo lokale Git-opslagplaats](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="51985-144">Klik op **Implementatiereferenties**, een gebruiker en het wachtwoord toouse tooconnect toohello Git-opslagplaats in Azure maken en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="51985-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="51985-145">Klik op **overzicht**, en bekijkt hello waarde **Git kloon-url**.</span><span class="sxs-lookup"><span data-stu-id="51985-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Hallo Git kloon-URL van uw web-app ophalen](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="51985-147">Open een opdracht of een terminalvenster op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="51985-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="51985-148">Hallo-web-app downloaden vanuit GitHub en upload het tooAzure voor Hallo web app toohost.</span><span class="sxs-lookup"><span data-stu-id="51985-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="51985-149">toodo Voer dus Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="51985-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="51985-150">\<GIT kloon-URL\> Hallo-URL van Hallo Git-opslagplaats gevonden op Hallo **overzicht** pagina van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="51985-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="51985-151">Hallo web app toosee realtime temperatuur en vochtigheid gegevens openen vanuit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="51985-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="51985-152">Op Hallo **overzicht** pagina van uw web-app klikt u op Hallo URL tooopen Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="51985-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Hallo-URL van uw web-app ophalen](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="51985-154">U ziet Hallo realtime temperatuur en vochtigheid gegevens uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="51985-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Web-app-pagina met realtime temperatuur en vochtigheid](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="51985-156">Controleer de voorbeeldtoepassing hello wordt uitgevoerd op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="51985-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="51985-157">Als dat niet zo is, ontvangt u een lege grafiek, raadpleegt u de zelfstudies toohello onder [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="51985-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51985-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51985-158">Next steps</span></span>
<span data-ttu-id="51985-159">U hebt uw web-app toovisualize realtime-sensorgegevens met succes van uw IoT-hub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="51985-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="51985-160">Zie voor een andere manier toovisualize gegevens uit Azure IoT Hub, [gebruik Power BI toovisualize realtime-sensorgegevens uit uw IoT-hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="51985-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
