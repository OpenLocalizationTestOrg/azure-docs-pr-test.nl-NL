---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooRaspberry Pi 3 dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: knipperen cloud pi geleid, knipperen geleid vanuit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="63a94-104">Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="63a94-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="63a94-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="63a94-105">What you will do</span></span>
<span data-ttu-id="63a94-106">Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op frambozen Pi 3 dat verzendt berichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="63a94-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="63a94-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="63a94-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="63a94-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="63a94-108">What you will learn</span></span>
<span data-ttu-id="63a94-109">U leert hoe toouse hello gulp hulpprogramma toodeploy en Hallo voorbeeld Node.js-toepassing uitvoeren op Pi.</span><span class="sxs-lookup"><span data-stu-id="63a94-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="63a94-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="63a94-110">What you need</span></span>
* <span data-ttu-id="63a94-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="63a94-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="63a94-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="63a94-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="63a94-113">Hallo apparaat verbindingsreeks wordt gebruikt door uw Pi tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="63a94-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="63a94-114">Hallo IoT hub-verbindingsreeks is gebruikte tooconnect toohello-identiteitenregister van uw IoT hub toomanage Hallo-apparaten die zijn toegestaan tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="63a94-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="63a94-115">Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="63a94-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="63a94-116">Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="63a94-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="63a94-117">Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="63a94-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="63a94-118">`{my hub name}`Hallo-naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Pi is.</span><span class="sxs-lookup"><span data-stu-id="63a94-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="63a94-119">Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="63a94-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="63a94-120">Gebruik `myraspberrypi` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="63a94-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="63a94-121">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="63a94-121">Configure hello device connection</span></span>
1. <span data-ttu-id="63a94-122">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="63a94-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="63a94-123">Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.</span><span class="sxs-lookup"><span data-stu-id="63a94-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="63a94-124">Open Hallo apparaat configuratiebestand `config-raspberrypi.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="63a94-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="63a94-126">Zorg Hallo vervangingen in Hallo na `config-raspberrypi.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="63a94-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="63a94-127">Vervang **[apparaat-hostnaam of IP-adres]** met Hallo IP-adres of de hostnaam apparaatnaam u gekregen `device-discovery-cli` of Hallo waarde overgenomen wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="63a94-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="63a94-128">Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="63a94-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="63a94-129">Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="63a94-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="63a94-130">U hoeft niet `azure_storage_connection_string` in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="63a94-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="63a94-131">Houd deze zo is.</span><span class="sxs-lookup"><span data-stu-id="63a94-131">Keep it as is.</span></span>

<span data-ttu-id="63a94-132">Update Hallo `config-raspberrypi.json` bestand zodat u de voorbeeldtoepassing Hallo van uw computer kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="63a94-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="63a94-133">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="63a94-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="63a94-134">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="63a94-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="63a94-135">Controleer of de voorbeeldtoepassing Hallo werkt</span><span class="sxs-lookup"><span data-stu-id="63a94-135">Verify that hello sample application works</span></span>
<span data-ttu-id="63a94-136">U ziet Hallo LED die is verbonden tooPi knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="63a94-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="63a94-137">Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="63a94-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="63a94-138">Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="63a94-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="63a94-139">Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="63a94-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="63a94-141">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="63a94-141">Summary</span></span>
<span data-ttu-id="63a94-142">U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op Pi toosend apparaat-naar-cloudberichten tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="63a94-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="63a94-143">U nu bewaken uw berichten zoals ze zijn toohello storage-account geschreven.</span><span class="sxs-lookup"><span data-stu-id="63a94-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63a94-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63a94-144">Next steps</span></span>
[<span data-ttu-id="63a94-145">Alleen berichten permanent in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="63a94-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

