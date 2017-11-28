---
title: Connect Raspberry PI (C) tooAzure IoT - oplossen | Microsoft Docs
description: Pagina voor probleemoplossing voor frambozen Pi Node.js-ervaring
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-problemen, internet der dingen problemen
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="29d13-104">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="29d13-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="29d13-105">Hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="29d13-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="29d13-106">Hallo-toepassing wordt uitgevoerd en maar Hallo LED knippert niet</span><span class="sxs-lookup"><span data-stu-id="29d13-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="29d13-107">Dit probleem is altijd gerelateerde toohello hardware circuit netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="29d13-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="29d13-108">Volgende stappen tooidentify problemen Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29d13-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="29d13-109">Controleer dat u hebt gekozen Hallo juist **GPIO** op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="29d13-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="29d13-110">Hallo twee poorten moet **GPIO GND (pincode 6)** en **GPIO 04 (7 pincode)**.</span><span class="sxs-lookup"><span data-stu-id="29d13-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="29d13-111">Controleer of de polariteit Hallo van uw LED juist is.</span><span class="sxs-lookup"><span data-stu-id="29d13-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="29d13-112">Hallo langer arm zou moeten aangeven waarom Hallo **positief**, gebruikte pincodes.</span><span class="sxs-lookup"><span data-stu-id="29d13-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="29d13-113">Gebruik Hallo **3, 3v vastmaken** en **GND pincode** op frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="29d13-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="29d13-114">Hallo DC power Pi behandeld.</span><span class="sxs-lookup"><span data-stu-id="29d13-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="29d13-115">Controleer dat Hallo LED werkt prima.</span><span class="sxs-lookup"><span data-stu-id="29d13-115">Check that hello LED works fine.</span></span>

![LED specificatie](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="29d13-117">Andere hardwareproblemen</span><span class="sxs-lookup"><span data-stu-id="29d13-117">Other hardware issues</span></span>
<span data-ttu-id="29d13-118">Zie voor informatie over het oplossen van veelvoorkomende problemen bij frambozen Pi 3 Hallo [officiële pagina voor probleemoplossing](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="29d13-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="29d13-119">Problemen met node.js-pakket</span><span class="sxs-lookup"><span data-stu-id="29d13-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="29d13-120">Geen reactie tijdens gulp taken</span><span class="sxs-lookup"><span data-stu-id="29d13-120">No response during gulp tasks</span></span>
<span data-ttu-id="29d13-121">Als u problemen hebt met het actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="29d13-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="29d13-122">Probeer tooterminate huidige gulp taken met behulp van `Ctrl + C`, en vervolgens uitvoeren Hallo-opdracht in uw foutopsporingsberichten console venster toosee.</span><span class="sxs-lookup"><span data-stu-id="29d13-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="29d13-123">Gedetailleerde foutberichten ziet u in de console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="29d13-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="29d13-124">Problemen met detectie van apparaat</span><span class="sxs-lookup"><span data-stu-id="29d13-124">Device discovery issues</span></span>
<span data-ttu-id="29d13-125">Voor hulp bij het oplossen van veelvoorkomende problemen met Hallo `devdisco` opdracht, controleert u Hallo [Leesmij](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="29d13-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="29d13-126">NPM problemen</span><span class="sxs-lookup"><span data-stu-id="29d13-126">NPM issues</span></span>
<span data-ttu-id="29d13-127">Probeer tooupdate uw pakket NPM Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="29d13-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="29d13-128">Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="29d13-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="29d13-129">Foutopsporing op afstand</span><span class="sxs-lookup"><span data-stu-id="29d13-129">Remote debugging</span></span>

<span data-ttu-id="29d13-130">Extern ondersteuning voor foutopsporing worden binnenkort in Visual Studio Code C/C++-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="29d13-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="29d13-131">U kunt in een ondertussen GDB gebruiken via uw favoriete terminal voor SSH:</span><span class="sxs-lookup"><span data-stu-id="29d13-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="29d13-132">Azure CLI-problemen</span><span class="sxs-lookup"><span data-stu-id="29d13-132">Azure-CLI issues</span></span>
<span data-ttu-id="29d13-133">Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie.</span><span class="sxs-lookup"><span data-stu-id="29d13-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="29d13-134">Zoek naar de oplossing in Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek oplossingen.</span><span class="sxs-lookup"><span data-stu-id="29d13-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="29d13-135">Probeer tooupgrade Azure cli toolatest versie wanneer opdrachten niet werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="29d13-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="29d13-136">Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.</span><span class="sxs-lookup"><span data-stu-id="29d13-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="29d13-137">Voor hulp bij het oplossen van veelvoorkomende problemen, Controleer Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="29d13-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="29d13-138">Als u aan 'Kan een versie die voldoet aan de vereiste Hallo niet vinden', neem opdracht uitvoeren Hallo volgende tooupgrade pip toolastest versie.</span><span class="sxs-lookup"><span data-stu-id="29d13-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="29d13-139">Problemen met de installatie van Python</span><span class="sxs-lookup"><span data-stu-id="29d13-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="29d13-140">Verouderde installatieproblemen (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="29d13-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="29d13-141">Wanneer u installeert **pip**, een machtigingsfout wordt gegenereerd wanneer de oudere pakketten die zijn geïnstalleerd met **su** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="29d13-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="29d13-142">Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd.</span><span class="sxs-lookup"><span data-stu-id="29d13-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="29d13-143">Sommige **pip** pakketten van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout.</span><span class="sxs-lookup"><span data-stu-id="29d13-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="29d13-144">Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="29d13-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="29d13-145">Hallo toocomplete stappen te volgen met deze taak gebruiken:</span><span class="sxs-lookup"><span data-stu-id="29d13-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="29d13-146">Ga naar: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="29d13-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="29d13-147">Lijst met pakketten maken door hoofdmap:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="29d13-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="29d13-148">Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="29d13-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="29d13-149">Installeer Python.</span><span class="sxs-lookup"><span data-stu-id="29d13-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="29d13-150">Problemen met Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="29d13-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="29d13-151">Als u uw Azure IoT hub met succes hebt ingericht `azure-cli`, en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen:</span><span class="sxs-lookup"><span data-stu-id="29d13-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="29d13-152">Apparaat Explorer</span><span class="sxs-lookup"><span data-stu-id="29d13-152">Device Explorer</span></span>
<span data-ttu-id="29d13-153">[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbindt tooyour IoT-hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="29d13-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="29d13-154">Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="29d13-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="29d13-155">*Identiteiten Apparaatbeheer* tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="29d13-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="29d13-156">*Apparaat-naar-cloud ontvangen* zodat u berichten van uw apparaat tooyour IoT-hub kunt bewaken.</span><span class="sxs-lookup"><span data-stu-id="29d13-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="29d13-157">*Cloud naar apparaat verzenden* zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="29d13-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="29d13-158">Configureer uw `IoT hub connection string` binnen dit hulpprogramma toouse de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="29d13-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="29d13-159">IoT-hub Explorer</span><span class="sxs-lookup"><span data-stu-id="29d13-159">IoT hub Explorer</span></span>
<span data-ttu-id="29d13-160">[IoT-hub Explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage-apparaatclients.</span><span class="sxs-lookup"><span data-stu-id="29d13-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="29d13-161">U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.</span><span class="sxs-lookup"><span data-stu-id="29d13-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="29d13-162">tooinstall Hallo nieuwste (prerelease) versie van Hallo iothub explorer hulpprogramma, Hallo volgende opdracht in uw omgeving opdrachtregel uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="29d13-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="29d13-163">U kunt Hallo opdracht tooget meer informatie over alle Hallo iothub explorer opdrachten en hun parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="29d13-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="29d13-164">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="29d13-164">Azure portal</span></span>
<span data-ttu-id="29d13-165">Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="29d13-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="29d13-166">U kunt ook toouse hello [Azure-portal](../azure-portal-overview.md) toohelp inrichten, beheren en fouten opsporen in uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="29d13-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="29d13-167">Problemen met de Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="29d13-167">Azure storage issues</span></span>
<span data-ttu-id="29d13-168">[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="29d13-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="29d13-169">Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien.</span><span class="sxs-lookup"><span data-stu-id="29d13-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="29d13-170">U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.</span><span class="sxs-lookup"><span data-stu-id="29d13-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
