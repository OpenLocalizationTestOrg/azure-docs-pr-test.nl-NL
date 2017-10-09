---
title: Gesimuleerde apparaat & Azure IoT Gateway - probleemoplossing | Microsoft Docs
description: Pagina voor probleemoplossing voor Intel NUC gateway
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-problemen, internet der dingen problemen
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="4d1eb-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4d1eb-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="4d1eb-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="4d1eb-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="4d1eb-106">TI SensorTag kan niet worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="4d1eb-107">verbindingsproblemen tootroubleshoot SensorTag, gebruik Hallo [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="4d1eb-108">Een probleem met de Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4d1eb-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="4d1eb-109">opstartproblemen tootroubleshoot, te verwijzen[problemen met het niet opstarten op Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="4d1eb-110">problemen met de besturingssystemen van tootroubleshoot te verwijzen[problemen met het besturingssysteem op Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="4d1eb-111">tootroubleshoot andere problemen te verwijzen[knipperen Codes en een piepgeluid laat horen Codes voor Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="4d1eb-112">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="4d1eb-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="4d1eb-113">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="4d1eb-113">No response during gulp tasks</span></span>

<span data-ttu-id="4d1eb-114">Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="4d1eb-115">Probeer tooterminate huidige gulp taken met behulp van `Ctrl + C`, en vervolgens uitvoeren Hallo-opdracht in uw foutopsporingsberichten console venster toosee.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="4d1eb-116">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="4d1eb-117">Problemen met detectie van apparaat</span><span class="sxs-lookup"><span data-stu-id="4d1eb-117">Device discovery issues</span></span>

<span data-ttu-id="4d1eb-118">Voor hulp bij het oplossen van veelvoorkomende problemen met Hallo `discover-sensortag` opdracht, controleert u Hallo [wiki-pagina](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="4d1eb-119">npm problemen</span><span class="sxs-lookup"><span data-stu-id="4d1eb-119">npm issues</span></span>

<span data-ttu-id="4d1eb-120">Probeer tooupdate de npm-pakket door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="4d1eb-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="4d1eb-121">Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="4d1eb-122">Foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="4d1eb-122">Remote Debugging</span></span>
> <span data-ttu-id="4d1eb-123">Onderstaande instructies zijn bedoeld voor het opsporen van node.js-scripts die worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="4d1eb-124">Hallo-voorbeeldtoepassing in de foutopsporingsmodus uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4d1eb-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="4d1eb-125">Hallo-voorbeeldtoepassing in de foutopsporingsmodus uitvoeren door te voeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4d1eb-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="4d1eb-126">Wanneer foutopsporing-engine Hallo klaar is, ziet u `Debugger listening on port 5858` in Hallo console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="4d1eb-127">Visual Studio Code tooconnect toohello externe apparaten configureren</span><span class="sxs-lookup"><span data-stu-id="4d1eb-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="4d1eb-128">Open Hallo **Debug** Configuratiescherm op Hallo linkerkant.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="4d1eb-129">Klik op Hallo groen **foutopsporing starten** knop (F5).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="4d1eb-130">Hiermee opent u Visual Studio Code een `launch.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="4d1eb-131">Update Hallo `launch.json` bestand met de Hallo inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="4d1eb-132">Vervang `[device hostname or IP address]` met Hallo werkelijke IP-adres of de hostnaam apparaatnaam.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

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

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="4d1eb-134">De externe toepassing toohello koppelen</span><span class="sxs-lookup"><span data-stu-id="4d1eb-134">Attach toohello remote application</span></span>

<span data-ttu-id="4d1eb-135">Klik op Hallo groen **foutopsporing starten** (F5) knop toostart foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="4d1eb-136">Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn meer informatie over Hallo foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Voorbeeld van foutopsporing uitschakelen](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="4d1eb-138">Problemen met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4d1eb-138">Azure CLI issues</span></span>

<span data-ttu-id="4d1eb-139">Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="4d1eb-140">oplossingen voor tooseek, kunt u Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="4d1eb-141">Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="4d1eb-142">Controleer voor hulp bij het oplossen van veelvoorkomende problemen Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="4d1eb-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="4d1eb-143">Als u aan 'Kan een versie die voldoet aan de vereiste Hallo niet vinden', neem opdracht uitvoeren Hallo volgende tooupgrade pip toolastest versie.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="4d1eb-144">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="4d1eb-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="4d1eb-145">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="4d1eb-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="4d1eb-146">Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="4d1eb-147">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="4d1eb-148">Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="4d1eb-149">Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="4d1eb-150">Hallo toocomplete stappen te volgen met deze taak gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4d1eb-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="4d1eb-151">Te gaan`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="4d1eb-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="4d1eb-152">Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="4d1eb-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="4d1eb-153">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="4d1eb-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="4d1eb-154">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="4d1eb-155">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4d1eb-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="4d1eb-156">Als u uw Azure-IoT-hub Hello Azure CLI met succes hebt ingericht en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="4d1eb-157">Apparaat Explorer</span><span class="sxs-lookup"><span data-stu-id="4d1eb-157">Device Explorer</span></span>

<span data-ttu-id="4d1eb-158">[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbindt tooyour IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="4d1eb-159">Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="4d1eb-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="4d1eb-160">Apparaat identity management tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="4d1eb-161">Apparaat-naar-cloud ontvangen u berichten van uw apparaat tooyour IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="4d1eb-162">Cloud naar apparaat verzenden zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="4d1eb-163">Configureer uw IoT hub-verbindingsreeks binnen dit hulpprogramma toouse de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="4d1eb-164">iothub explorer</span><span class="sxs-lookup"><span data-stu-id="4d1eb-164">iothub-explorer</span></span>

<span data-ttu-id="4d1eb-165">[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage-apparaatclients.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="4d1eb-166">U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="4d1eb-167">tooinstall hello nieuwste (prerelease) versie van Hallo iothub explorer hulpprogramma, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4d1eb-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="4d1eb-168">meer informatie over alle tooget Hallo iothub explorer opdrachten en de bijbehorende parameters, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4d1eb-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="4d1eb-169">Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4d1eb-169">hello Azure portal</span></span>

<span data-ttu-id="4d1eb-170">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="4d1eb-171">U kunt ook toouse hello [Azure-portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="4d1eb-172">Azure Storage-problemen</span><span class="sxs-lookup"><span data-stu-id="4d1eb-172">Azure Storage issues</span></span>

<span data-ttu-id="4d1eb-173">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com/) is een zelfstandige app van Microsoft die u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="4d1eb-174">Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="4d1eb-175">U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.</span><span class="sxs-lookup"><span data-stu-id="4d1eb-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
