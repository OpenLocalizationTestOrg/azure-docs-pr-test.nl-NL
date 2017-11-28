---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Windows) | Microsoft Docs'
description: De hulpprogramma's en de software installeren op de hostcomputer waarop Windows wordt uitgevoerd, een iothub maken en Registreer uw apparaat in de IoT-hub.
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
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="54702-104">Download de hulpprogramma's (Windows 7 en hoger)</span><span class="sxs-lookup"><span data-stu-id="54702-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54702-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="54702-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="54702-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="54702-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="54702-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="54702-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="54702-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="54702-108">What you will do</span></span>

- <span data-ttu-id="54702-109">Installeer Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="54702-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="54702-110">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="54702-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="54702-111">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="54702-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="54702-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="54702-112">What you will learn</span></span>

<span data-ttu-id="54702-113">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="54702-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="54702-114">Het installeren van [Git](https://git-scm.com/) en [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="54702-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="54702-115">GIT is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="54702-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="54702-116">De voorbeeldtoepassing voor deze les wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="54702-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="54702-117">Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="54702-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="54702-118">Het gebruik van [NPM](https://www.npmjs.com/) Node.js ontwikkelingsprogramma's te installeren.</span><span class="sxs-lookup"><span data-stu-id="54702-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="54702-119">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="54702-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="54702-120">NPM is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="54702-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="54702-121">Klik hier voor meer informatie over het installeren van Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="54702-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="54702-122">Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="54702-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="54702-123">Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.</span><span class="sxs-lookup"><span data-stu-id="54702-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="54702-124">Klik hier voor meer informatie over het installeren van Python.</span><span class="sxs-lookup"><span data-stu-id="54702-124">How to install Python.</span></span>
  - <span data-ttu-id="54702-125">Python is een veelgebruikte op hoog niveau, algemeen, geïnterpreteerde en dynamische programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="54702-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="54702-126">Klik hier voor meer informatie over het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="54702-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="54702-127">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="54702-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="54702-128">U werkt rechtstreeks vanaf een opdrachtregel inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="54702-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="54702-129">Het gebruik van de Azure CLI voor het maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="54702-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="54702-130">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="54702-130">What you need</span></span>

- <span data-ttu-id="54702-131">Een internetverbinding beschikken om het downloaden van de hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="54702-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="54702-132">Een Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="54702-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="54702-133">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="54702-133">Install Git and Node.js</span></span>

<span data-ttu-id="54702-134">Klik op de volgende koppelingen wilt downloaden en installeren van Git en Node.js LTS voor Windows.</span><span class="sxs-lookup"><span data-stu-id="54702-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="54702-135">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="54702-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="54702-136">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="54702-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="54702-137">Node.js ontwikkelingsprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="54702-137">Install Node.js development tools</span></span>

<span data-ttu-id="54702-138">U gebruikt [gulp.js](http://gulpjs.com/) te automatiseren, implementatie en uitvoering van scripts.</span><span class="sxs-lookup"><span data-stu-id="54702-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="54702-139">Druk op `Windows + R`, type `cmd` en druk op `Enter` open een opdrachtpromptvenster en voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="54702-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="54702-140">Als u problemen bij de installatie ondervindt, raadpleegt u de [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="54702-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="54702-141">Knooppunt, NPM en Gulp zijn vereist om uit te voeren automatiseringsscripts ontwikkeld in Node.js.</span><span class="sxs-lookup"><span data-stu-id="54702-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="54702-142">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="54702-142">Install Python</span></span>

<span data-ttu-id="54702-143">U kunt kiezen uit Python 2.7 3.4 of 3.5.</span><span class="sxs-lookup"><span data-stu-id="54702-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="54702-144">In deze zelfstudie gebruiken we Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="54702-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="54702-145">Als u python al hebt geïnstalleerd, gaat u naar de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="54702-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="54702-146">Python ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="54702-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="54702-147">Ook moet u het pad van de mappen waar Python.exe en pip.exe zijn geïnstalleerd op het systeem toevoegen `PATH` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="54702-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="54702-148">Python.exe worden standaard geïnstalleerd `C:\Python27` en pip.exe is geïnstalleerd in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="54702-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="54702-149">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="54702-149">Install the Azure CLI</span></span>

<span data-ttu-id="54702-150">Volg deze stappen voor het installeren van de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="54702-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="54702-151">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="54702-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="54702-152">Azure CLI installeren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="54702-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="54702-153">De installatie kan 5 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="54702-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="54702-154">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="54702-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="54702-155">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="54702-155">You should see the following output if the installation is successful.</span></span>

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="54702-157">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="54702-157">Install Visual Studio Code</span></span>

<span data-ttu-id="54702-158">U kunt Visual Studio Code verderop in de zelfstudie configuratiebestanden bewerken.</span><span class="sxs-lookup"><span data-stu-id="54702-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="54702-159">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="54702-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="54702-160">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="54702-160">Summary</span></span>

<span data-ttu-id="54702-161">U hebt de vereiste hulpprogramma's en software op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="54702-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="54702-162">Uw volgende taak is het gebruik van de Azure CLI voor het maken van een IoT-hub en Registreer uw apparaat bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="54702-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54702-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54702-163">Next steps</span></span>
[<span data-ttu-id="54702-164">Een IoT-hub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="54702-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
