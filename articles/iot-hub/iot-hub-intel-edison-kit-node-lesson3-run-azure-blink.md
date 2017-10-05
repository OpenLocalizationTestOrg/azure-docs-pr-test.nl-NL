---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 3: berichten verzenden | Microsoft Docs'
description: Implementeren en uitvoeren van een voorbeeld van toepassing op Intel Edison dat berichten verzendt naar uw IoT-hub en de LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden van gegevens naar de cloud
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
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="8de61-104">Voer een voorbeeldtoepassing om apparaat-naar-cloud-berichten te verzenden</span><span class="sxs-lookup"><span data-stu-id="8de61-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8de61-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="8de61-105">What you will do</span></span>
<span data-ttu-id="8de61-106">In dit artikel wordt beschreven hoe u implementeren en uitvoeren van een voorbeeld van toepassing op Intel Edison dat berichten naar uw IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="8de61-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="8de61-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8de61-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8de61-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="8de61-108">What you will learn</span></span>
<span data-ttu-id="8de61-109">U leert hoe u met het hulpprogramma gulp implementeren en uitvoeren van de voorbeeldtoepassing C op Edison.</span><span class="sxs-lookup"><span data-stu-id="8de61-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8de61-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8de61-110">What you need</span></span>
* <span data-ttu-id="8de61-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een opslagaccount om te verwerken en opslaan van IoT hub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="8de61-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="8de61-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="8de61-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="8de61-113">De verbindingsreeks van het apparaat wordt gebruikt voor Edison verbinding met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8de61-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="8de61-114">De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinden van uw IoT-hub met de apparaat-id die Edison in de IoT-hub vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="8de61-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="8de61-115">Een overzicht van uw IoT-hubs in de resourcegroep met de volgende Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="8de61-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="8de61-116">Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8de61-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="8de61-117">De IoT hub-verbindingsreeks ophalen met de volgende opdracht in de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="8de61-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="8de61-118">`{my hub name}`is de naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Edison.</span><span class="sxs-lookup"><span data-stu-id="8de61-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="8de61-119">De apparaat-verbindingsreeks ophalen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8de61-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="8de61-120">Gebruik `myinteledison` als de waarde van `{device id}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8de61-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="8de61-121">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="8de61-121">Configure the device connection</span></span>
1. <span data-ttu-id="8de61-122">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="8de61-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="8de61-123">Open het configuratiebestand van het apparaat `config-edison.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8de61-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="8de61-125">Controleer de volgende vervangingen in de `config-edison.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="8de61-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="8de61-126">Vervang **[apparaat-hostnaam of IP-adres]** met het apparaat IP-adres dat u naar beneden gemarkeerd wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8de61-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="8de61-127">Vervang **[apparaat-verbindingsreeks IoT]** met de `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="8de61-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="8de61-128">Vervang **[IoT hub verbindingsreeks]** met de `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="8de61-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8de61-129">U hoeft niet `azure_storage_connection_string` in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8de61-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="8de61-130">Houd deze zo is.</span><span class="sxs-lookup"><span data-stu-id="8de61-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="8de61-131">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="8de61-131">Deploy and run the sample application</span></span>
<span data-ttu-id="8de61-132">Implementeren en uitvoeren van de voorbeeldtoepassing op Edison met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8de61-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="8de61-133">Controleer of de voorbeeldtoepassing werkt</span><span class="sxs-lookup"><span data-stu-id="8de61-133">Verify that the sample application works</span></span>
<span data-ttu-id="8de61-134">U ziet de LED die is verbonden met Edison knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="8de61-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="8de61-135">Telkens wanneer de LED knippert, wordt de voorbeeldtoepassing verzendt een bericht naar uw IoT-hub en verifieert dat wordt het bericht is verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8de61-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="8de61-136">Bovendien wordt elk bericht ontvangen door de IoT-hub in het consolevenster.</span><span class="sxs-lookup"><span data-stu-id="8de61-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="8de61-137">De voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="8de61-137">The sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="8de61-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8de61-139">Summary</span></span>
<span data-ttu-id="8de61-140">U hebt geïmplementeerd en de nieuwe knipperen voorbeeldtoepassing uitvoeren op Edison apparaat-naar-cloud-berichten verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8de61-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="8de61-141">U nu bewaken uw berichten zoals ze zijn geschreven naar het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8de61-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8de61-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8de61-142">Next steps</span></span>
<span data-ttu-id="8de61-143">[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="8de61-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md