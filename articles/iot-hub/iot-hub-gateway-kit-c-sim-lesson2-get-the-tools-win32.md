---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Windows) | Microsoft Docs'
description: Hallo-hulpprogramma's en Hallo software installeren op de hostcomputer waarop Windows wordt uitgevoerd, een iothub maken en Registreer uw apparaat in Hallo IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, installeer git voor windows, gulp uitvoeren, knooppunt js windows installeren, npm in windows te installeren, python op windows installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="2531e-104">Ophalen van Hallo hulpprogramma's (Windows 7 en hoger)</span><span class="sxs-lookup"><span data-stu-id="2531e-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2531e-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="2531e-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="2531e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="2531e-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="2531e-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="2531e-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="2531e-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2531e-108">What you will do</span></span>

- <span data-ttu-id="2531e-109">Installeer Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="2531e-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="2531e-110">Hello Azure-opdrachtregelinterface (Azure CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="2531e-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="2531e-111">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2531e-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2531e-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2531e-112">What you will learn</span></span>

<span data-ttu-id="2531e-113">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="2531e-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="2531e-114">Hoe tooinstall [Git](https://git-scm.com/) en [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="2531e-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="2531e-115">GIT is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="2531e-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="2531e-116">Hallo-voorbeeldtoepassing voor deze les wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="2531e-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="2531e-117">Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="2531e-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="2531e-118">Hoe toouse [NPM](https://www.npmjs.com/) tooinstall Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2531e-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="2531e-119">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="2531e-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="2531e-120">NPM is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="2531e-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="2531e-121">Hoe tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2531e-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="2531e-122">Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="2531e-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2531e-123">Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.</span><span class="sxs-lookup"><span data-stu-id="2531e-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="2531e-124">Hoe tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="2531e-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="2531e-125">Python is een veelgebruikte op hoog niveau, algemeen, geïnterpreteerde en dynamische programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="2531e-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="2531e-126">Hoe tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2531e-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="2531e-127">Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="2531e-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="2531e-128">U werkt rechtstreeks vanaf een opdrachtregel tooprovision en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="2531e-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="2531e-129">Hoe toouse hello Azure CLI toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2531e-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2531e-130">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2531e-130">What you need</span></span>

- <span data-ttu-id="2531e-131">Een Internet verbinding toodownload Hallo hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="2531e-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="2531e-132">Een Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="2531e-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2531e-133">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="2531e-133">Install Git and Node.js</span></span>

<span data-ttu-id="2531e-134">Klik op Hallo toodownload koppelingen volgen en Git en Node.js LTS voor Windows installeren.</span><span class="sxs-lookup"><span data-stu-id="2531e-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="2531e-135">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="2531e-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="2531e-136">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="2531e-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="2531e-137">Node.js ontwikkelingsprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="2531e-137">Install Node.js development tools</span></span>

<span data-ttu-id="2531e-138">U gebruikt [gulp.js](http://gulpjs.com/) tooautomate implementatie en uitvoering van scripts.</span><span class="sxs-lookup"><span data-stu-id="2531e-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="2531e-139">Druk op `Windows + R`, type `cmd` en druk op `Enter` tooopen een opdrachtpromptvenster, en vervolgens uitvoeren Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="2531e-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="2531e-140">Als u problemen met Hallo-installatie ondervindt, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="2531e-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="2531e-141">Knooppunt, NPM en Gulp zijn vereiste toorun automatiseringsscripts ontwikkeld in Node.js.</span><span class="sxs-lookup"><span data-stu-id="2531e-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="2531e-142">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="2531e-142">Install Python</span></span>

<span data-ttu-id="2531e-143">U kunt kiezen uit Python 2.7 3.4 of 3.5.</span><span class="sxs-lookup"><span data-stu-id="2531e-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="2531e-144">In deze zelfstudie gebruiken we Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="2531e-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="2531e-145">Als u python al hebt geïnstalleerd, gaat u de volgende sectie toohello.</span><span class="sxs-lookup"><span data-stu-id="2531e-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="2531e-146">Python ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="2531e-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="2531e-147">U moet ook tooadd Hallo pad Hallo mappen waar systeem geïnstalleerde toohello Python.exe en pip.exe zijn `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="2531e-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="2531e-148">Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="2531e-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="2531e-149">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="2531e-149">Install hello Azure CLI</span></span>

<span data-ttu-id="2531e-150">tooinstall hello Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2531e-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="2531e-151">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="2531e-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="2531e-152">Hello Azure CLI installeren door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="2531e-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="2531e-153">Hallo-installatie kan 5 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="2531e-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="2531e-154">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2531e-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="2531e-155">U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="2531e-155">You should see hello following output if hello installation is successful.</span></span>

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="2531e-157">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="2531e-157">Install Visual Studio Code</span></span>

<span data-ttu-id="2531e-158">Visual Studio Code die u in configuratiebestanden Hallo-zelfstudie tooedit later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2531e-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="2531e-159">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="2531e-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="2531e-160">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2531e-160">Summary</span></span>

<span data-ttu-id="2531e-161">U kunt alle Hallo vereist hulpprogramma's en software hebt geïnstalleerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="2531e-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="2531e-162">Uw volgende taak toouse hello Azure CLI toocreate is een IoT-hub en Registreer uw apparaat bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2531e-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2531e-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2531e-163">Next steps</span></span>
[<span data-ttu-id="2531e-164">Een IoT-hub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="2531e-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
