---
title: Connect Raspberry PI (C) tooAzure IoT - oplossen | Microsoft Docs
description: Het oplossen van de pagina voor Hallo frambozen Pi Node.js-ervaring
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-problemen, internet der dingen problemen
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="a5ba0-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="a5ba0-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="a5ba0-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="a5ba0-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="a5ba0-106">Hallo-toepassing wordt uitgevoerd en maar Hallo LED knippert niet</span><span class="sxs-lookup"><span data-stu-id="a5ba0-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="a5ba0-107">Dit probleem is altijd gerelateerde toohardware circuit netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="a5ba0-108">Na de stappen tooidentify problemen hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a5ba0-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="a5ba0-109">Controleer dat u hebt gekozen Hallo juist **GPIO** op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="a5ba0-110">Hallo twee poorten moet **GPIO GND (pincode 6)** en **GPIO 04 (7 pincode)**.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="a5ba0-111">Controleer of de polariteit Hallo van uw LED juist is.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="a5ba0-112">Hallo langer arm zou moeten aangeven waarom Hallo **positief**, gebruikte pincodes.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="a5ba0-113">Gebruik Hallo **3, 3v vastmaken** en **GND pincode** op frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="a5ba0-114">Hallo DC power Pi behandeld.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="a5ba0-115">Controleer dat Hallo LED werkt prima.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-115">Check that hello LED works fine.</span></span>

![LED specificatie](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="a5ba0-117">Andere hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="a5ba0-117">Other hardware issues</span></span>
<span data-ttu-id="a5ba0-118">Zie voor informatie over het oplossen van veelvoorkomende problemen bij frambozen Pi 3 Hallo [officiële pagina voor probleemoplossing](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="a5ba0-119">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="a5ba0-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="a5ba0-120">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="a5ba0-120">No response during gulp tasks</span></span>
<span data-ttu-id="a5ba0-121">Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="a5ba0-122">Probeer tooterminate huidige gulp taken met behulp van Ctrl + c drukken en voer de volgende opdracht in uw foutopsporingsberichten console venster toosee Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="a5ba0-123">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="a5ba0-124">Problemen met detectie van apparaat</span><span class="sxs-lookup"><span data-stu-id="a5ba0-124">Device discovery issues</span></span>
<span data-ttu-id="a5ba0-125">Voor hulp bij het oplossen van veelvoorkomende problemen met Hallo `devdisco` opdracht, controleert u Hallo [Leesmij](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="a5ba0-126">npm problemen</span><span class="sxs-lookup"><span data-stu-id="a5ba0-126">npm issues</span></span>
<span data-ttu-id="a5ba0-127">Probeer tooupdate de npm-pakket met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5ba0-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="a5ba0-128">Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="a5ba0-129">Foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="a5ba0-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="a5ba0-130">Hallo-voorbeeldtoepassing in de foutopsporingsmodus uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a5ba0-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="a5ba0-131">Wanneer foutopsporing-engine Hallo klaar is, ziet u ```Debugger listening on port 5858``` in Hallo console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="a5ba0-132">Visual Studio Code tooconnect toohello externe apparaten configureren</span><span class="sxs-lookup"><span data-stu-id="a5ba0-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="a5ba0-133">Open Hallo **Debug** Configuratiescherm op Hallo linkerkant.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="a5ba0-134">Klik op Hallo groen **foutopsporing starten** knop (F5).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="a5ba0-135">Visual Studio Code een launch.json-bestand wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="a5ba0-136">Hallo launch.json updatebestand Hello inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="a5ba0-137">Vervang `[device hostname or IP address]` met Hallo werkelijke IP-adres of de hostnaam apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="a5ba0-138">toolearn meer informatie over Hallo Visual Studio foutopsporing Raadpleeg te[foutopsporing in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Configuratie van extern foutopsporing](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="a5ba0-140">De externe toepassing toohello koppelen</span><span class="sxs-lookup"><span data-stu-id="a5ba0-140">Attach toohello remote application</span></span>
<span data-ttu-id="a5ba0-141">Klik op Hallo groen **foutopsporing starten** (F5) knop toostart foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="a5ba0-142">Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn meer informatie over Hallo foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Externe interactieve foutopsporing](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="a5ba0-144">Problemen met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5ba0-144">Azure CLI issues</span></span>
<span data-ttu-id="a5ba0-145">Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="a5ba0-146">oplossingen voor tooseek, kunt u Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="a5ba0-147">Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="a5ba0-148">Controleer voor hulp bij het oplossen van veelvoorkomende problemen Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="a5ba0-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="a5ba0-149">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="a5ba0-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="a5ba0-150">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="a5ba0-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="a5ba0-151">Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="a5ba0-152">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="a5ba0-153">Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="a5ba0-154">Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="a5ba0-155">Hallo toocomplete stappen te volgen met deze taak gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a5ba0-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="a5ba0-156">Ga naar: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="a5ba0-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="a5ba0-157">Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="a5ba0-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="a5ba0-158">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="a5ba0-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="a5ba0-159">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="a5ba0-160">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a5ba0-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="a5ba0-161">Als u uw Azure-IoT-hub met Azure CLI met succes hebt ingericht en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="a5ba0-162">Apparaat explorer</span><span class="sxs-lookup"><span data-stu-id="a5ba0-162">Device explorer</span></span>
<span data-ttu-id="a5ba0-163">Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) hulpprogramma wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt tooyour IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="a5ba0-164">Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="a5ba0-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="a5ba0-165">*Identiteiten Apparaatbeheer* tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="a5ba0-166">*Apparaat-naar-cloud ontvangen* zodat u berichten van uw apparaat tooyour IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="a5ba0-167">*Cloud naar apparaat verzenden* zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="a5ba0-168">Configureer uw IoT hub-verbindingsreeks binnen dit hulpprogramma toouse de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="a5ba0-169">iothub explorer</span><span class="sxs-lookup"><span data-stu-id="a5ba0-169">iothub-explorer</span></span>
<span data-ttu-id="a5ba0-170">[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage apparaten.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="a5ba0-171">U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaat-berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="a5ba0-172">tooinstall Hallo nieuwste (prerelease) versie van Hallo iothub explorer hulpprogramma, Hallo volgende opdracht in uw omgeving opdrachtregel uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a5ba0-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="a5ba0-173">U kunt Hallo opdracht tooget meer informatie over alle Hallo iothub explorer opdrachten en hun parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5ba0-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="a5ba0-174">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a5ba0-174">Azure portal</span></span>
<span data-ttu-id="a5ba0-175">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="a5ba0-176">U kunt ook toouse hello [Azure-portal](../azure-portal-overview.md) toohelp inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="a5ba0-177">Azure Storage-problemen</span><span class="sxs-lookup"><span data-stu-id="a5ba0-177">Azure Storage issues</span></span>
<span data-ttu-id="a5ba0-178">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="a5ba0-179">Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="a5ba0-180">U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.</span><span class="sxs-lookup"><span data-stu-id="a5ba0-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

