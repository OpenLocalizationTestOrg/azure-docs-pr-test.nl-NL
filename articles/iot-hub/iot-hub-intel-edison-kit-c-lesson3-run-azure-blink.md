---
title: 'Connect Intel Edison (C) tooAzure IoT - les 3: berichten verzenden | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooIntel Edison dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="d4207-104">Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="d4207-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d4207-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="d4207-105">What you will do</span></span>
<span data-ttu-id="d4207-106">Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op Intel Edison die verzendt berichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d4207-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="d4207-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d4207-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d4207-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="d4207-108">What you will learn</span></span>
<span data-ttu-id="d4207-109">U leert hoe toouse Hallo hulpprogramma toodeploy gulp en Hallo C voorbeeldtoepassing uitvoeren op Edison.</span><span class="sxs-lookup"><span data-stu-id="d4207-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d4207-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="d4207-110">What you need</span></span>
* <span data-ttu-id="d4207-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="d4207-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="d4207-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="d4207-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="d4207-113">Hallo apparaat-verbindingsreeks is gebruikte tooconnect Edison tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d4207-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="d4207-114">Hallo IoT hub-verbindingsreeks is gebruikte tooconnect uw IoT hub toohello apparaat-id die Edison in Hallo IoT-hub aangeeft.</span><span class="sxs-lookup"><span data-stu-id="d4207-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="d4207-115">Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="d4207-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="d4207-116">Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="d4207-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="d4207-117">Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="d4207-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="d4207-118">`{my hub name}`Hallo-naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Edison is.</span><span class="sxs-lookup"><span data-stu-id="d4207-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="d4207-119">Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4207-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="d4207-120">Gebruik `myinteledison` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="d4207-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="d4207-121">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="d4207-121">Configure hello device connection</span></span>
1. <span data-ttu-id="d4207-122">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="d4207-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="d4207-123">Voer **gulp install-hulpprogramma's** en, als u dit nog niet hebt gedaan in les 1.</span><span class="sxs-lookup"><span data-stu-id="d4207-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="d4207-124">Open Hallo apparaat configuratiebestand `config-edison.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4207-124">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="d4207-126">Zorg Hallo vervangingen in Hallo na `config-edison.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="d4207-126">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="d4207-127">Vervang **[apparaat-hostnaam of IP-adres]** met Hallo apparaat IP-adres u omlaag gemarkeerd wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d4207-127">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="d4207-128">Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="d4207-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="d4207-129">Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="d4207-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d4207-130">U hoeft niet `azure_storage_connection_string` in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d4207-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="d4207-131">Houd deze zo is.</span><span class="sxs-lookup"><span data-stu-id="d4207-131">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="d4207-132">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="d4207-132">Deploy and run hello sample application</span></span>
<span data-ttu-id="d4207-133">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="d4207-133">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="d4207-134">Controleer of de voorbeeldtoepassing Hallo werkt</span><span class="sxs-lookup"><span data-stu-id="d4207-134">Verify that hello sample application works</span></span>
<span data-ttu-id="d4207-135">U ziet Hallo LED die is verbonden tooEdison knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="d4207-135">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="d4207-136">Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d4207-136">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="d4207-137">Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4207-137">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="d4207-138">Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="d4207-138">hello sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="d4207-140">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d4207-140">Summary</span></span>
<span data-ttu-id="d4207-141">U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op Edison toosend apparaat-naar-cloudberichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d4207-141">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="d4207-142">U nu bewaken uw berichten zoals ze zijn toohello storage-account geschreven.</span><span class="sxs-lookup"><span data-stu-id="d4207-142">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4207-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4207-143">Next steps</span></span>
<span data-ttu-id="d4207-144">[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="d4207-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md