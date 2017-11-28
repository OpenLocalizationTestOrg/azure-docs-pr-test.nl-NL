---
title: Verbinding maken met Raspberry Pi (C) naar Azure IoT - oplossen | Microsoft Docs
description: Pagina voor de frambozen Pi Node.js-ervaring voor probleemoplossing
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="33301-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="33301-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="33301-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="33301-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="33301-106">De toepassing goed wordt uitgevoerd, maar niet de LED knippert</span><span class="sxs-lookup"><span data-stu-id="33301-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="33301-107">Dit probleem is altijd gerelateerd aan hardware circuit connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="33301-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="33301-108">Gebruik de volgende stappen om problemen te identificeren:</span><span class="sxs-lookup"><span data-stu-id="33301-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="33301-109">Controleer dat u hebt ervoor de juiste gekozen **GPIO** op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="33301-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="33301-110">De twee poorten moet **GPIO GND (pincode 6)** en **GPIO 04 (7 pincode)**.</span><span class="sxs-lookup"><span data-stu-id="33301-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="33301-111">Controleer of de polariteit van uw LED juist is.</span><span class="sxs-lookup"><span data-stu-id="33301-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="33301-112">De langer arm zou moeten aangeven waarom de **positief**, gebruikte pincodes.</span><span class="sxs-lookup"><span data-stu-id="33301-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="33301-113">Gebruik de **3, 3v vastmaken** en **GND pincode** op frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="33301-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="33301-114">De DC-macht Pi behandeld.</span><span class="sxs-lookup"><span data-stu-id="33301-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="33301-115">Controleer of de LED prima werkt.</span><span class="sxs-lookup"><span data-stu-id="33301-115">Check that the LED works fine.</span></span>

![LED specificatie](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="33301-117">Andere hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="33301-117">Other hardware issues</span></span>
<span data-ttu-id="33301-118">Zie voor meer informatie over het oplossen van veelvoorkomende problemen bij frambozen Pi 3 de [officiële pagina voor probleemoplossing](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="33301-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="33301-119">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="33301-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="33301-120">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="33301-120">No response during gulp tasks</span></span>
<span data-ttu-id="33301-121">Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen de `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="33301-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="33301-122">Huidige gulp taken beëindigd met behulp van Ctrl + C, en voer de volgende opdracht in het consolevenster om te zien foutopsporingsberichten.</span><span class="sxs-lookup"><span data-stu-id="33301-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="33301-123">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="33301-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="33301-124">Problemen met detectie van apparaat</span><span class="sxs-lookup"><span data-stu-id="33301-124">Device discovery issues</span></span>
<span data-ttu-id="33301-125">Voor hulp bij het oplossen van veelvoorkomende problemen met de `devdisco` opdracht, Controleer de [Leesmij](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="33301-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="33301-126">npm problemen</span><span class="sxs-lookup"><span data-stu-id="33301-126">npm issues</span></span>
<span data-ttu-id="33301-127">Voer uw npm pakket bijwerken met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="33301-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="33301-128">Als het probleem blijft optreden, laat u hierop een toelichting aan het einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="33301-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="33301-129">Foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="33301-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="33301-130">De voorbeeldtoepassing in de foutopsporingsmodus uitvoeren</span><span class="sxs-lookup"><span data-stu-id="33301-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="33301-131">Wanneer de engine voor foutopsporing klaar is, ziet u ```Debugger listening on port 5858``` in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="33301-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="33301-132">Visual Studio Code verbinding maken met het externe apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="33301-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="33301-133">Open de **Debug** deelvenster aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="33301-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="33301-134">Klik op de groene **foutopsporing starten** knop (F5).</span><span class="sxs-lookup"><span data-stu-id="33301-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="33301-135">Visual Studio Code een launch.json-bestand wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="33301-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="33301-136">Het bestand launch.json bijwerken met de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="33301-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="33301-137">Vervang `[device hostname or IP address]` met de werkelijke IP-adres of de hostnaam apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="33301-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="33301-138">Voor meer informatie over de foutopsporing Visual Studio, Raadpleeg [foutopsporing in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="33301-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="33301-140">Koppelen aan de externe toepassing</span><span class="sxs-lookup"><span data-stu-id="33301-140">Attach to the remote application</span></span>
<span data-ttu-id="33301-141">Klik op de groene **foutopsporing starten** (F5) knop foutopsporing te starten.</span><span class="sxs-lookup"><span data-stu-id="33301-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="33301-142">Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) voor meer informatie over het foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="33301-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Externe interactieve foutopsporing](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="33301-144">Problemen met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33301-144">Azure CLI issues</span></span>
<span data-ttu-id="33301-145">De Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="33301-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="33301-146">Als u wilt zoeken naar oplossingen, kunt u de [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="33301-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="33301-147">Als u met het hulpprogramma fouten optreden, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in de **problemen** sectie van de GitHub-repo.</span><span class="sxs-lookup"><span data-stu-id="33301-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="33301-148">Als u hulp nodig hebt bij het oplossen van veelvoorkomende problemen, Controleer de [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="33301-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="33301-149">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="33301-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="33301-150">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="33301-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="33301-151">Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="33301-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="33301-152">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="33301-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="33301-153">Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor de machtiging fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="33301-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="33301-154">De oplossing is om te verwijderen die pakketten geïnstalleerd door de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="33301-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="33301-155">Gebruik de volgende stappen uit om deze taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="33301-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="33301-156">Ga naar: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="33301-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="33301-157">Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="33301-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="33301-158">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="33301-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="33301-159">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="33301-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="33301-160">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="33301-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="33301-161">Als u uw Azure-IoT-hub met Azure CLI met succes hebt ingericht en u een hulpprogramma moet voor het beheren van de apparaten die zijn verbonden met uw IoT-hub, kunt u de volgende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="33301-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="33301-162">Apparaat explorer</span><span class="sxs-lookup"><span data-stu-id="33301-162">Device explorer</span></span>
<span data-ttu-id="33301-163">De [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) hulpprogramma wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt met uw IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="33301-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="33301-164">Er wordt gecommuniceerd met de volgende [IoT-hubeindpunten](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="33301-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="33301-165">*Identiteiten Apparaatbeheer* inrichten en beheren van apparaten die zijn geregistreerd met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="33301-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="33301-166">*Apparaat-naar-cloud ontvangen* zodat u berichten van uw apparaat voor uw IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="33301-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="33301-167">*Cloud naar apparaat verzenden* zodat u berichten naar uw apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="33301-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="33301-168">Configureer uw IoT hub-verbindingsreeks vanuit dit hulpprogramma te gebruiken van de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="33301-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="33301-169">iothub explorer</span><span class="sxs-lookup"><span data-stu-id="33301-169">iothub-explorer</span></span>
<span data-ttu-id="33301-170">[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld meerdere platforms CLI-hulpprogramma om apparaten te beheren.</span><span class="sxs-lookup"><span data-stu-id="33301-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="33301-171">Het hulpprogramma kunt u de apparaten in het identiteitenregister beheren, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaat-berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="33301-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="33301-172">Voer de volgende opdracht in uw omgeving opdrachtregelprogramma voor het installeren van de meest recente (voorlopige) versie van het hulpprogramma iothub explorer:</span><span class="sxs-lookup"><span data-stu-id="33301-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="33301-173">De volgende opdracht kunt u extra hulp vragen over alle iothub explorer-opdrachten en de bijbehorende parameters:</span><span class="sxs-lookup"><span data-stu-id="33301-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="33301-174">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33301-174">Azure portal</span></span>
<span data-ttu-id="33301-175">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="33301-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="33301-176">U kunt ook gebruik van de [Azure-portal](../azure-portal-overview.md) kunt inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="33301-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="33301-177">Azure Storage-problemen</span><span class="sxs-lookup"><span data-stu-id="33301-177">Azure Storage issues</span></span>
<span data-ttu-id="33301-178">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u gebruiken kunt voor het werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="33301-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="33301-179">Met dit hulpprogramma kunt u verbinding maken met uw tabel en de gegevens weergegeven in het.</span><span class="sxs-lookup"><span data-stu-id="33301-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="33301-180">U kunt dit hulpprogramma om problemen met uw Azure Storage te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33301-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

