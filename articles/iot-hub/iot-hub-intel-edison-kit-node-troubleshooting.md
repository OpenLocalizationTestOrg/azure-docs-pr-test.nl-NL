---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 4: probleemoplossing | Microsoft Docs'
description: Pagina voor probleemoplossing voor Intel Edison Node.js-ervaring
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino probleemoplossing
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="3f44d-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="3f44d-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="3f44d-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="3f44d-105">Hardware issues</span></span>
<span data-ttu-id="3f44d-106">Zie voor meer informatie over het oplossen van veelvoorkomende problemen op Intel Edison de [officiële pagina voor probleemoplossing](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="3f44d-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="3f44d-107">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="3f44d-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="3f44d-108">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="3f44d-108">No response during gulp tasks</span></span>
<span data-ttu-id="3f44d-109">Als u met taken gulp problemen, kunt u toevoegen de `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="3f44d-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="3f44d-110">Probeer het huidige gulp taken beëindigd met behulp van `Ctrl + C`, en voer de volgende in het consolevenster opdracht om te zien foutopsporingsberichten.</span><span class="sxs-lookup"><span data-stu-id="3f44d-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="3f44d-111">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3f44d-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="3f44d-112">NPM problemen</span><span class="sxs-lookup"><span data-stu-id="3f44d-112">NPM issues</span></span>
<span data-ttu-id="3f44d-113">Voer de NPM-pakket bijwerken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3f44d-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="3f44d-114">Als het probleem blijft optreden, laat u hierop een toelichting aan het einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="3f44d-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="3f44d-115">Foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="3f44d-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="3f44d-116">De voorbeeldtoepassing in de foutopsporingsmodus uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3f44d-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="3f44d-117">Zodra de engine voor foutopsporing gereed is, moet u kunnen zien ```Debugger listening on port 5858``` van de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3f44d-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="3f44d-118">VS-Code voor het verbinding maken met het externe apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="3f44d-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="3f44d-119">Open de **Debug** Configuratiescherm vanaf de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="3f44d-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="3f44d-120">Klik op de groene **foutopsporing starten** knop (F5).</span><span class="sxs-lookup"><span data-stu-id="3f44d-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="3f44d-121">VS Code opent een **launch.json** bestand, dat u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3f44d-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="3f44d-122">Update de **launch.json** bestand met de volgende inhoud, Vervang `[device hostname or IP address]` met het daadwerkelijk apparaat IP-adres of de hostnaam.</span><span class="sxs-lookup"><span data-stu-id="3f44d-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

![Configuratie van extern foutopsporing](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="3f44d-124">Koppelen aan de externe toepassing</span><span class="sxs-lookup"><span data-stu-id="3f44d-124">Attach to the remote application</span></span>

<span data-ttu-id="3f44d-125">Klik op de groene **foutopsporing starten** (F5) knop en profiteer van foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="3f44d-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="3f44d-126">U kunt lezen [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) voor meer informatie over het foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="3f44d-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Externe interactieve foutopsporing](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="3f44d-128">Azure CLI-problemen</span><span class="sxs-lookup"><span data-stu-id="3f44d-128">Azure-CLI issues</span></span>
<span data-ttu-id="3f44d-129">De Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="3f44d-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="3f44d-130">Zoek naar de oplossing in de [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) te zoeken naar oplossingen.</span><span class="sxs-lookup"><span data-stu-id="3f44d-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="3f44d-131">Probeer Azure cli naar de nieuwste versie om bij te werken opdrachten werken niet zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="3f44d-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="3f44d-132">Als u met het hulpprogramma fouten optreden, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in de **problemen** sectie van de GitHub-repo.</span><span class="sxs-lookup"><span data-stu-id="3f44d-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="3f44d-133">Voor hulp bij het oplossen van veelvoorkomende problemen, Controleer de [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="3f44d-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="3f44d-134">Als u 'Kan een versie die voldoet aan de vereiste niet vinden' aan, voert u de volgende opdracht om te werken van pip naar de laatste versie.</span><span class="sxs-lookup"><span data-stu-id="3f44d-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="3f44d-135">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="3f44d-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="3f44d-136">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="3f44d-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="3f44d-137">Wanneer u installeert **pip**, een machtigingsfout wordt gegenereerd wanneer de oudere pakketten die zijn geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="3f44d-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="3f44d-138">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3f44d-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="3f44d-139">Sommige **pip** pakketten van een eerdere installatie zijn gemaakt door root, waardoor de machtiging fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="3f44d-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="3f44d-140">De oplossing is om te verwijderen die pakketten geïnstalleerd door de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="3f44d-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="3f44d-141">Gebruik de volgende stappen uit om deze taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="3f44d-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="3f44d-142">Ga naar: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="3f44d-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="3f44d-143">Lijst met pakketten maken door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="3f44d-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="3f44d-144">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="3f44d-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="3f44d-145">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="3f44d-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="3f44d-146">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3f44d-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="3f44d-147">Als u uw Azure IoT hub met succes hebt ingericht `azure-cli`, en moet u een hulpprogramma voor het beheren van de apparaten die zijn verbonden met uw IoT-hub, probeert u de volgende hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="3f44d-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="3f44d-148">Apparaat Explorer</span><span class="sxs-lookup"><span data-stu-id="3f44d-148">Device Explorer</span></span>
<span data-ttu-id="3f44d-149">[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt met uw IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f44d-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="3f44d-150">Er wordt gecommuniceerd met de volgende [IoT-hubeindpunten](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="3f44d-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="3f44d-151">_Identiteiten Apparaatbeheer_ inrichten en beheren van apparaten die zijn geregistreerd met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3f44d-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="3f44d-152">_Apparaat-naar-cloud ontvangen_ zodat u berichten van uw apparaat voor uw IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="3f44d-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="3f44d-153">_Cloud naar apparaat verzenden_ zodat u berichten naar uw apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="3f44d-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="3f44d-154">Configureer uw `IoT hub connection string` vanuit dit hulpprogramma te gebruiken van de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="3f44d-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="3f44d-155">IoT-hub Explorer</span><span class="sxs-lookup"><span data-stu-id="3f44d-155">IoT hub Explorer</span></span>
<span data-ttu-id="3f44d-156">[IoT-hub Explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld meerdere platforms CLI-hulpprogramma om apparaatclients te beheren.</span><span class="sxs-lookup"><span data-stu-id="3f44d-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="3f44d-157">Het hulpprogramma kunt u de apparaten in het identiteitenregister beheren, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.</span><span class="sxs-lookup"><span data-stu-id="3f44d-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="3f44d-158">Voer de volgende opdracht in uw omgeving opdrachtregelprogramma voor het installeren van de meest recente (voorlopige) versie van het hulpprogramma iothub explorer:</span><span class="sxs-lookup"><span data-stu-id="3f44d-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="3f44d-159">De volgende opdracht kunt u extra hulp vragen over alle iothub explorer-opdrachten en de bijbehorende parameters:</span><span class="sxs-lookup"><span data-stu-id="3f44d-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="3f44d-160">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3f44d-160">Azure portal</span></span>
<span data-ttu-id="3f44d-161">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3f44d-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="3f44d-162">U kunt ook gebruik van de [Azure-portal](../azure-portal-overview.md) kunt inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3f44d-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="3f44d-163">Problemen met de Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="3f44d-163">Azure storage issues</span></span>
<span data-ttu-id="3f44d-164">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u gebruiken kunt voor het werken met [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="3f44d-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="3f44d-165">Met dit hulpprogramma kunt u verbinding maken met uw tabel en de gegevens weergegeven in het.</span><span class="sxs-lookup"><span data-stu-id="3f44d-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="3f44d-166">U kunt dit hulpprogramma om problemen met uw Azure Storage te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f44d-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f44d-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f44d-167">Next steps</span></span>
<span data-ttu-id="3f44d-168">Deze pagina bevat alleen de meest voorkomende problemen van Intel Edison kit.</span><span class="sxs-lookup"><span data-stu-id="3f44d-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="3f44d-169">U kunt ook de opmerkingen onder laten problemen rapporteren voor meer informatie over.</span><span class="sxs-lookup"><span data-stu-id="3f44d-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="3f44d-170">Ga terug naar [aan de slag met Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3f44d-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started