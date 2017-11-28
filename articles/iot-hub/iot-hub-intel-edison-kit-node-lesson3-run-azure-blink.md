---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 3: berichten verzenden | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooIntel Edison dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="daec2-104">Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="daec2-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="daec2-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="daec2-105">What you will do</span></span>
<span data-ttu-id="daec2-106">Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op Intel Edison die verzendt berichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="daec2-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="daec2-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="daec2-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="daec2-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="daec2-108">What you will learn</span></span>
<span data-ttu-id="daec2-109">U leert hoe toouse Hallo hulpprogramma toodeploy gulp en Hallo C voorbeeldtoepassing uitvoeren op Edison.</span><span class="sxs-lookup"><span data-stu-id="daec2-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="daec2-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="daec2-110">What you need</span></span>
* <span data-ttu-id="daec2-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="daec2-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="daec2-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="daec2-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="daec2-113">Hallo apparaat-verbindingsreeks is gebruikte tooconnect Edison tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="daec2-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="daec2-114">Hallo IoT hub-verbindingsreeks is gebruikte tooconnect uw IoT hub toohello apparaat-id die Edison in Hallo IoT-hub aangeeft.</span><span class="sxs-lookup"><span data-stu-id="daec2-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="daec2-115">Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="daec2-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="daec2-116">Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="daec2-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="daec2-117">Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="daec2-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="daec2-118">`{my hub name}`Hallo-naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Edison is.</span><span class="sxs-lookup"><span data-stu-id="daec2-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="daec2-119">Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="daec2-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="daec2-120">Gebruik `myinteledison` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="daec2-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="daec2-121">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="daec2-121">Configure hello device connection</span></span>
1. <span data-ttu-id="daec2-122">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="daec2-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="daec2-123">Open Hallo apparaat configuratiebestand `config-edison.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="daec2-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="daec2-125">Zorg Hallo vervangingen in Hallo na `config-edison.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="daec2-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="daec2-126">Vervang **[apparaat-hostnaam of IP-adres]** met Hallo apparaat IP-adres u omlaag gemarkeerd wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="daec2-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="daec2-127">Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="daec2-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="daec2-128">Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="daec2-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="daec2-129">U hoeft niet `azure_storage_connection_string` in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="daec2-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="daec2-130">Houd deze zo is.</span><span class="sxs-lookup"><span data-stu-id="daec2-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="daec2-131">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="daec2-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="daec2-132">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="daec2-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="daec2-133">Controleer of de voorbeeldtoepassing Hallo werkt</span><span class="sxs-lookup"><span data-stu-id="daec2-133">Verify that hello sample application works</span></span>
<span data-ttu-id="daec2-134">U ziet Hallo LED die is verbonden tooEdison knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="daec2-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="daec2-135">Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="daec2-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="daec2-136">Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="daec2-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="daec2-137">Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="daec2-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="daec2-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="daec2-139">Summary</span></span>
<span data-ttu-id="daec2-140">U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op Edison toosend apparaat-naar-cloudberichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="daec2-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="daec2-141">U nu bewaken uw berichten zoals ze zijn toohello storage-account geschreven.</span><span class="sxs-lookup"><span data-stu-id="daec2-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daec2-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="daec2-142">Next steps</span></span>
<span data-ttu-id="daec2-143">[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="daec2-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md