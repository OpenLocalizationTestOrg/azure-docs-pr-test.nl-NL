---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Hulpprogramma's installeren op uw Mac-computer, een iothub maken en uw apparaat registreren in de IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, install python mac, installeer git op mac gulp uitvoert, installatie knooppunt js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d86332816130de7a6951a74ceb215c8ce476d5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="74b81-104">Download de hulpprogramma's (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="74b81-104">Get the tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74b81-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="74b81-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="74b81-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="74b81-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="74b81-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="74b81-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="74b81-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="74b81-108">What you will do</span></span>

- <span data-ttu-id="74b81-109">Installeer Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="74b81-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="74b81-110">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="74b81-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="74b81-111">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="74b81-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="74b81-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="74b81-112">What you will learn</span></span>

<span data-ttu-id="74b81-113">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="74b81-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="74b81-114">Het installeren van [Git](https://git-scm.com/) en [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="74b81-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="74b81-115">GIT is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="74b81-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="74b81-116">De voorbeeldtoepassing voor deze les wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="74b81-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="74b81-117">Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="74b81-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="74b81-118">Het gebruik van [NPM](https://www.npmjs.com/) Node.js ontwikkelingsprogramma's te installeren.</span><span class="sxs-lookup"><span data-stu-id="74b81-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="74b81-119">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="74b81-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="74b81-120">NPM is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="74b81-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="74b81-121">Klik hier voor meer informatie over het installeren van Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="74b81-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="74b81-122">Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="74b81-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="74b81-123">Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.</span><span class="sxs-lookup"><span data-stu-id="74b81-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="74b81-124">Klik hier voor meer informatie over het installeren van Python.</span><span class="sxs-lookup"><span data-stu-id="74b81-124">How to install Python.</span></span>
  - <span data-ttu-id="74b81-125">Python is een veelgebruikte op hoog niveau, algemeen, geïnterpreteerde en dynamische programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="74b81-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="74b81-126">Klik hier voor meer informatie over het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="74b81-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="74b81-127">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="74b81-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="74b81-128">U werkt rechtstreeks vanaf een opdrachtregel inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="74b81-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="74b81-129">Het gebruik van de Azure CLI voor het maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="74b81-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="74b81-130">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="74b81-130">What you need</span></span>

- <span data-ttu-id="74b81-131">Een internetverbinding beschikken om het downloaden van de hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="74b81-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="74b81-132">Een Mac-computer met OS X Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="74b81-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="74b81-133">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="74b81-133">Install Git and Node.js</span></span>

<span data-ttu-id="74b81-134">Wilt installeren Git en Node.js, gebruikt u het hulpprogramma voor het Homebrew pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="74b81-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="74b81-135">[Download](http://brew.sh/) en Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="74b81-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="74b81-136">Als u Homebrew al hebt geïnstalleerd, gaat u naar stap 2.</span><span class="sxs-lookup"><span data-stu-id="74b81-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="74b81-137">Druk op `Cmd + Space` en voer `Terminal` een terminal openen.</span><span class="sxs-lookup"><span data-stu-id="74b81-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="74b81-138">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="74b81-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="74b81-139">Git en Node.js installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="74b81-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="74b81-140">Node.js ontwikkelingsprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="74b81-140">Install Node.js development tools</span></span>

<span data-ttu-id="74b81-141">U gebruikt [gulp.js](http://gulpjs.com/) te automatiseren, implementatie en uitvoering van scripts.</span><span class="sxs-lookup"><span data-stu-id="74b81-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="74b81-142">Als u wilt installeren gulp, voer de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="74b81-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="74b81-143">Als u problemen bij de installatie ondervindt, raadpleegt u de [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="74b81-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="74b81-144">Knooppunt, NPM en Gulp zijn vereist om uit te voeren automatiseringsscripts ontwikkeld in Node.js.</span><span class="sxs-lookup"><span data-stu-id="74b81-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="74b81-145">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="74b81-145">Install Python</span></span>

<span data-ttu-id="74b81-146">Hoewel Mac OS X wordt geleverd met Python 2.7, raden we u Python via Homebrew te installeren.</span><span class="sxs-lookup"><span data-stu-id="74b81-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="74b81-147">Zie [Python installeren op Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="74b81-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="74b81-148">Python en pip installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="74b81-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="74b81-149">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="74b81-149">Install the Azure CLI</span></span>

<span data-ttu-id="74b81-150">Volg deze stappen voor het installeren van de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="74b81-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="74b81-151">Voer de volgende opdrachten in de terminal:</span><span class="sxs-lookup"><span data-stu-id="74b81-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="74b81-152">De installatie kan 5 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="74b81-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="74b81-153">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="74b81-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="74b81-154">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="74b81-154">You should see the following output if the installation is successful.</span></span>

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="74b81-156">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="74b81-156">Install Visual Studio Code</span></span>

<span data-ttu-id="74b81-157">U kunt Visual Studio Code verderop in de zelfstudie configuratiebestanden bewerken.</span><span class="sxs-lookup"><span data-stu-id="74b81-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="74b81-158">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="74b81-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="74b81-159">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="74b81-159">Summary</span></span>

<span data-ttu-id="74b81-160">U hebt de vereiste hulpprogramma's en software op uw Mac-computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="74b81-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="74b81-161">Uw volgende taak is het gebruik van de Azure CLI voor het maken van een IoT-hub en Registreer uw apparaat bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="74b81-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74b81-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74b81-162">Next steps</span></span>
[<span data-ttu-id="74b81-163">Een iothub maken en registreren van apparaat</span><span class="sxs-lookup"><span data-stu-id="74b81-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
