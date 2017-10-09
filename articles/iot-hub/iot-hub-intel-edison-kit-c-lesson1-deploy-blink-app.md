---
title: 'Connect Intel Edison (C) tooAzure IoT - les 1: toepassing implementeren | Microsoft Docs'
description: Hallo C voorbeeldtoepassing vanuit GitHub klonen en voer gulp toodeploy deze toepassing tooyour Intel Edison mededelingenbord. Deze voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino geleid projecten, arduino geleid knipperen, arduino geleid knipperen code, arduino knipperen programma, arduino knipperen voorbeeld
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="bb8e1-105">Hallo knipperen toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="bb8e1-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bb8e1-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bb8e1-106">What you will do</span></span>
<span data-ttu-id="bb8e1-107">Hallo C voorbeeldtoepassing vanuit GitHub klonen en Hallo gulp hulpprogramma toodeploy Hallo voorbeeld toepassing tooIntel Edison gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="bb8e1-108">Hallo-voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="bb8e1-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bb8e1-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bb8e1-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bb8e1-110">What you will learn</span></span>
* <span data-ttu-id="bb8e1-111">Hoe toodeploy en Voer Hallo voorbeeldtoepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb8e1-112">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bb8e1-112">What you need</span></span>
<span data-ttu-id="bb8e1-113">U moet hebben voltooid Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="bb8e1-114">[Uw apparaat configureren][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="bb8e1-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="bb8e1-115">[Hallo-hulpprogramma's ophalen][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="bb8e1-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="bb8e1-116">Open Hallo-voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="bb8e1-116">Open hello sample application</span></span>
<span data-ttu-id="bb8e1-117">tooopen hello voorbeeldtoepassing, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="bb8e1-118">Hallo voorbeeld opslagplaats vanuit GitHub door het uitvoeren van de volgende opdracht Hallo klonen:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="bb8e1-119">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

<span data-ttu-id="bb8e1-121">Hallo-bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toocontrol Hallo LED bevat.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="bb8e1-122">Afhankelijkheden voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="bb8e1-122">Install application dependencies</span></span>
<span data-ttu-id="bb8e1-123">Hallo-bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="bb8e1-124">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="bb8e1-124">Configure hello device connection</span></span>
<span data-ttu-id="bb8e1-125">tooconfigure Hallo apparaatverbinding, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="bb8e1-126">Hallo apparaat configuratiebestand gegenereerd door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="bb8e1-127">Hallo-configuratiebestand `config-edison.json` Hallo gebruikersreferenties u toolog in tooEdison bevat.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="bb8e1-128">Hallo-geheugenlek tooavoid van gebruikersreferenties, Hallo-configuratiebestand wordt gegenereerd in de submap Hallo `.iot-hub-getting-started` van Hallo basismap op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="bb8e1-129">Hallo apparaat configuratiebestand openen in Visual Studio Code door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="bb8e1-130">Vervang Hallo tijdelijke aanduiding voor `[device hostname or IP address]` en `[device password]` met Hallo IP-adres en het wachtwoord die u hebt gemarkeerd omlaag in de vorige les.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="bb8e1-132">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-132">Congratulations!</span></span> <span data-ttu-id="bb8e1-133">Hallo eerste voorbeeldtoepassing voor Edison hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="bb8e1-134">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="bb8e1-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="bb8e1-135">Hello Azure IoT Hub SDK installeren op Edison</span><span class="sxs-lookup"><span data-stu-id="bb8e1-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="bb8e1-136">Hello Azure IoT Hub SDK installeren op Edison door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="bb8e1-137">Deze taak kan duren voordat een toocomplete lange tijd, afhankelijk van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="bb8e1-138">Deze behoeften toobe slechts eenmaal uitvoeren voor één Edison.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="bb8e1-139">Implementeren en Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bb8e1-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="bb8e1-140">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb8e1-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="bb8e1-141">Controleer of de app werkt het Hallo</span><span class="sxs-lookup"><span data-stu-id="bb8e1-141">Verify hello app works</span></span>
<span data-ttu-id="bb8e1-142">Hallo-voorbeeldtoepassing wordt automatisch beëindigd nadat Hallo LED voor 20 keer knippert.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="bb8e1-143">Als er geen Hallo LED knippert, raadpleegt u Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED knippert][led-blinking]

## <a name="summary"></a><span data-ttu-id="bb8e1-145">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bb8e1-145">Summary</span></span>
<span data-ttu-id="bb8e1-146">U hebt geïnstalleerd Hallo vereist extra toowork met Edison en een voorbeeld toepassing tooEdison tooblink Hallo LED geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="bb8e1-147">U kunt nu maken, implementeren, en voer een ander voorbeeld van een toepassing die verbinding Edison tooAzure toosend IoT Hub maakt en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="bb8e1-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb8e1-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb8e1-148">Next steps</span></span>
<span data-ttu-id="bb8e1-149">[Hello Azure-hulpprogramma's ophalen][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="bb8e1-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
