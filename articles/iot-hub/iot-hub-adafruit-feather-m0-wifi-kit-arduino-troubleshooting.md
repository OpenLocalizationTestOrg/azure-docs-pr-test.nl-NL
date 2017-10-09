---
title: Connect Arduino (C) tooAzure IoT - oplossen | Microsoft Docs
description: Pagina voor probleemoplossing voor Adafruit Doezelaar M0 Wi-Fi Arduino ervaring
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino probleemoplossing
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="57ad8-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="57ad8-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="57ad8-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="57ad8-105">Hardware issues</span></span>
<span data-ttu-id="57ad8-106">Zie voor informatie over het oplossen van veelvoorkomende problemen op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino hello [officiële pagina voor probleemoplossing](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="57ad8-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="57ad8-107">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="57ad8-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="57ad8-108">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="57ad8-108">No response during gulp tasks</span></span>
<span data-ttu-id="57ad8-109">Als u problemen hebt met het actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="57ad8-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="57ad8-110">Probeer tooterminate huidige gulp taken met behulp van `Ctrl + C`, en vervolgens uitvoeren Hallo-opdracht in uw foutopsporingsberichten console venster toosee.</span><span class="sxs-lookup"><span data-stu-id="57ad8-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="57ad8-111">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="57ad8-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="57ad8-112">Of u kunt toevoegen `--listen` tooopen seriële poort toooutput apparaatgegevens-logboek.</span><span class="sxs-lookup"><span data-stu-id="57ad8-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="57ad8-113">NPM problemen</span><span class="sxs-lookup"><span data-stu-id="57ad8-113">NPM issues</span></span>
<span data-ttu-id="57ad8-114">Probeer tooupdate uw pakket NPM Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="57ad8-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="57ad8-115">Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="57ad8-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="57ad8-116">Azure CLI-problemen</span><span class="sxs-lookup"><span data-stu-id="57ad8-116">Azure-CLI issues</span></span>
<span data-ttu-id="57ad8-117">Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="57ad8-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="57ad8-118">Zoek naar de oplossing in Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek oplossingen.</span><span class="sxs-lookup"><span data-stu-id="57ad8-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="57ad8-119">Probeer tooupgrade Azure cli toolatest versie wanneer opdrachten niet werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="57ad8-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="57ad8-120">Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.</span><span class="sxs-lookup"><span data-stu-id="57ad8-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="57ad8-121">Voor hulp bij het oplossen van veelvoorkomende problemen, Controleer Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="57ad8-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="57ad8-122">Als u aan 'Kan een versie die voldoet aan de vereiste Hallo niet vinden', neem opdracht uitvoeren Hallo volgende tooupgrade pip toolastest versie.</span><span class="sxs-lookup"><span data-stu-id="57ad8-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="57ad8-123">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="57ad8-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="57ad8-124">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="57ad8-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="57ad8-125">Wanneer u installeert **pip**, een machtigingsfout wordt gegenereerd wanneer de oudere pakketten die zijn geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="57ad8-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="57ad8-126">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="57ad8-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="57ad8-127">Sommige **pip** pakketten van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout.</span><span class="sxs-lookup"><span data-stu-id="57ad8-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="57ad8-128">Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="57ad8-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="57ad8-129">Hallo toocomplete stappen te volgen met deze taak gebruiken:</span><span class="sxs-lookup"><span data-stu-id="57ad8-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="57ad8-130">Ga naar: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="57ad8-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="57ad8-131">Lijst met pakketten maken door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="57ad8-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="57ad8-132">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="57ad8-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="57ad8-133">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="57ad8-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="57ad8-134">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="57ad8-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="57ad8-135">Als u uw Azure IoT hub met succes hebt ingericht `azure-cli`, en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen:</span><span class="sxs-lookup"><span data-stu-id="57ad8-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="57ad8-136">Apparaat Explorer</span><span class="sxs-lookup"><span data-stu-id="57ad8-136">Device Explorer</span></span>
<span data-ttu-id="57ad8-137">[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbindt tooyour IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="57ad8-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="57ad8-138">Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="57ad8-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="57ad8-139">*Identiteiten Apparaatbeheer* tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="57ad8-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="57ad8-140">*Apparaat-naar-cloud ontvangen* zodat u berichten van uw apparaat tooyour IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="57ad8-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="57ad8-141">*Cloud naar apparaat verzenden* zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="57ad8-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="57ad8-142">Configureer uw `IoT hub connection string` binnen dit hulpprogramma toouse de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="57ad8-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="57ad8-143">IoT-hub Explorer</span><span class="sxs-lookup"><span data-stu-id="57ad8-143">IoT hub Explorer</span></span>
<span data-ttu-id="57ad8-144">[IoT-hub Explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage-apparaatclients.</span><span class="sxs-lookup"><span data-stu-id="57ad8-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="57ad8-145">U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.</span><span class="sxs-lookup"><span data-stu-id="57ad8-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="57ad8-146">tooinstall Hallo nieuwste (prerelease) versie van Hallo iothub explorer hulpprogramma, Hallo volgende opdracht in uw omgeving opdrachtregel uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="57ad8-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="57ad8-147">U kunt Hallo opdracht tooget meer informatie over alle Hallo iothub explorer opdrachten en hun parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="57ad8-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="57ad8-148">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="57ad8-148">Azure portal</span></span>
<span data-ttu-id="57ad8-149">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="57ad8-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="57ad8-150">U kunt ook toouse hello [Azure-portal](../azure-portal-overview.md) toohelp inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="57ad8-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="57ad8-151">Problemen met de Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="57ad8-151">Azure storage issues</span></span>
<span data-ttu-id="57ad8-152">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="57ad8-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="57ad8-153">Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien.</span><span class="sxs-lookup"><span data-stu-id="57ad8-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="57ad8-154">U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.</span><span class="sxs-lookup"><span data-stu-id="57ad8-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md