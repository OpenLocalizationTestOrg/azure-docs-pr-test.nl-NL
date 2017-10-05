---
title: SensorTag apparaat & Azure IoT Gateway - probleemoplossing | Microsoft Docs
description: Pagina voor probleemoplossing voor Intel NUC gateway
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-problemen, internet der dingen problemen
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7e80951de55ade6b5140608dcff8ebb064f942ca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="4f4c5-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4f4c5-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="4f4c5-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="4f4c5-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="4f4c5-106">TI SensorTag kan niet worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="4f4c5-107">Gebruik voor het oplossen van problemen met de netwerkverbinding SensorTag de [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="4f4c5-108">Een probleem met de Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4f4c5-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="4f4c5-109">Raadpleeg voor het oplossen van problemen met opstarten [problemen met het niet opstarten op Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="4f4c5-110">Raadpleeg voor het oplossen van problemen met besturingssystemen [problemen met het besturingssysteem op Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="4f4c5-111">Om andere problemen te verwijzen naar [knipperen Codes en een piepgeluid laat horen Codes voor Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="4f4c5-112">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="4f4c5-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="4f4c5-113">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="4f4c5-113">No response during gulp tasks</span></span>

<span data-ttu-id="4f4c5-114">Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen de `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="4f4c5-115">Probeer het huidige gulp taken beëindigd met behulp van `Ctrl + C`, en voer de volgende in het consolevenster opdracht om te zien foutopsporingsberichten.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="4f4c5-116">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="4f4c5-117">Problemen met detectie van apparaat</span><span class="sxs-lookup"><span data-stu-id="4f4c5-117">Device discovery issues</span></span>

<span data-ttu-id="4f4c5-118">Voor hulp bij het oplossen van veelvoorkomende problemen met de `discover-sensortag` opdracht, Controleer de [wiki-pagina](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="4f4c5-119">npm problemen</span><span class="sxs-lookup"><span data-stu-id="4f4c5-119">npm issues</span></span>

<span data-ttu-id="4f4c5-120">Voer de npm-pakket bijwerken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4f4c5-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="4f4c5-121">Als het probleem blijft optreden, laat u hierop een toelichting aan het einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="4f4c5-122">Foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="4f4c5-122">Remote Debugging</span></span>
> <span data-ttu-id="4f4c5-123">Onderstaande instructies zijn bedoeld voor het opsporen van node.js-scripts die worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="4f4c5-124">De voorbeeldtoepassing in de foutopsporingsmodus uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4f4c5-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="4f4c5-125">De voorbeeldtoepassing in de foutopsporingsmodus uitvoeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4f4c5-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="4f4c5-126">Wanneer de engine voor foutopsporing klaar is, ziet u `Debugger listening on port 5858` in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="4f4c5-127">Visual Studio Code verbinding maken met het externe apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="4f4c5-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="4f4c5-128">Open de **Debug** deelvenster aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="4f4c5-129">Klik op de groene **foutopsporing starten** knop (F5).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="4f4c5-130">Hiermee opent u Visual Studio Code een `launch.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="4f4c5-131">Update de `launch.json` bestand met de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="4f4c5-132">Vervang `[device hostname or IP address]` met de werkelijke IP-adres of de hostnaam apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuratie van extern foutopsporing](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="4f4c5-134">Koppelen aan de externe toepassing</span><span class="sxs-lookup"><span data-stu-id="4f4c5-134">Attach to the remote application</span></span>

<span data-ttu-id="4f4c5-135">Klik op de groene **foutopsporing starten** (F5) knop foutopsporing te starten.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="4f4c5-136">Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) voor meer informatie over het foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Voorbeeld van foutopsporing uitschakelen](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="4f4c5-138">Problemen met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f4c5-138">Azure CLI issues</span></span>

<span data-ttu-id="4f4c5-139">De Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="4f4c5-140">Als u wilt zoeken naar oplossingen, kunt u de [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="4f4c5-141">Als u met het hulpprogramma fouten optreden, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in de **problemen** sectie van de GitHub-repo.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="4f4c5-142">Als u hulp nodig hebt bij het oplossen van veelvoorkomende problemen, Controleer de [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="4f4c5-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="4f4c5-143">Als u 'Kan een versie die voldoet aan de vereiste niet vinden' aan, voert u de volgende opdracht om te werken van pip naar de laatste versie.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="4f4c5-144">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="4f4c5-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="4f4c5-145">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="4f4c5-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="4f4c5-146">Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="4f4c5-147">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="4f4c5-148">Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor de machtiging fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="4f4c5-149">De oplossing is om te verwijderen die pakketten geïnstalleerd door de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="4f4c5-150">Gebruik de volgende stappen uit om deze taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="4f4c5-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="4f4c5-151">Ga naar `/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="4f4c5-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="4f4c5-152">Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="4f4c5-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="4f4c5-153">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="4f4c5-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="4f4c5-154">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="4f4c5-155">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4f4c5-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="4f4c5-156">Als u uw Azure-IoT-hub met de Azure CLI met succes hebt ingericht en u een hulpprogramma moet voor het beheren van de apparaten die zijn verbonden met uw IoT-hub, kunt u de volgende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="4f4c5-157">Apparaat Explorer</span><span class="sxs-lookup"><span data-stu-id="4f4c5-157">Device Explorer</span></span>

<span data-ttu-id="4f4c5-158">[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt met uw IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="4f4c5-159">Er wordt gecommuniceerd met de volgende [IoT-hubeindpunten](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="4f4c5-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="4f4c5-160">Identiteiten Apparaatbeheer voor het inrichten en beheren van apparaten geregistreerd bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="4f4c5-161">Apparaat-naar-cloud ontvangen u berichten van uw apparaat voor uw IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="4f4c5-162">Cloud naar apparaat verzenden zodat u berichten naar uw apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="4f4c5-163">Configureer uw IoT hub-verbindingsreeks vanuit dit hulpprogramma te gebruiken van de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="4f4c5-164">iothub explorer</span><span class="sxs-lookup"><span data-stu-id="4f4c5-164">iothub-explorer</span></span>

<span data-ttu-id="4f4c5-165">[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld meerdere platforms CLI-hulpprogramma om apparaatclients te beheren.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="4f4c5-166">Het hulpprogramma kunt u de apparaten in het identiteitenregister beheren, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="4f4c5-167">Voer de volgende opdracht voor het installeren van de meest recente (voorlopige) versie van het hulpprogramma iothub explorer:</span><span class="sxs-lookup"><span data-stu-id="4f4c5-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="4f4c5-168">Als u meer informatie over alle iothub explorer-opdrachten en de bijbehorende parameters, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4f4c5-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="4f4c5-169">De Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4f4c5-169">The Azure portal</span></span>

<span data-ttu-id="4f4c5-170">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="4f4c5-171">U kunt ook gebruik van de [Azure-portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) kunt inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="4f4c5-172">Azure Storage-problemen</span><span class="sxs-lookup"><span data-stu-id="4f4c5-172">Azure Storage issues</span></span>

<span data-ttu-id="4f4c5-173">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com/) is een zelfstandige app van Microsoft die u gebruiken kunt voor het werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="4f4c5-174">Met dit hulpprogramma kunt u verbinding maken met uw tabel en de gegevens weergegeven in het.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="4f4c5-175">U kunt dit hulpprogramma om problemen met uw Azure Storage te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4f4c5-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
