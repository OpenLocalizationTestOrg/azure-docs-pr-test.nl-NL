---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Mac OS) | Microsoft Docs'
description: Hulpprogramma's installeren op uw Mac-computer, een iothub maken en Registreer uw apparaat in Hallo IoT-hub.
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
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="07556-104">Hallo hulpprogramma's (Mac OS) ophalen</span><span class="sxs-lookup"><span data-stu-id="07556-104">Get hello tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07556-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="07556-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="07556-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="07556-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="07556-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="07556-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="07556-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="07556-108">What you will do</span></span>

- <span data-ttu-id="07556-109">Installeer Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="07556-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="07556-110">Hello Azure-opdrachtregelinterface (Azure CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="07556-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="07556-111">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="07556-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="07556-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="07556-112">What you will learn</span></span>

<span data-ttu-id="07556-113">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="07556-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="07556-114">Hoe tooinstall [Git](https://git-scm.com/) en [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="07556-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="07556-115">GIT is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="07556-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="07556-116">Hallo-voorbeeldtoepassing voor deze les wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="07556-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="07556-117">Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="07556-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="07556-118">Hoe toouse [NPM](https://www.npmjs.com/) tooinstall Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="07556-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="07556-119">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="07556-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="07556-120">NPM is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="07556-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="07556-121">Hoe tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="07556-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="07556-122">Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="07556-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="07556-123">Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.</span><span class="sxs-lookup"><span data-stu-id="07556-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="07556-124">Hoe tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="07556-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="07556-125">Python is een veelgebruikte op hoog niveau, algemeen, geïnterpreteerde en dynamische programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="07556-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="07556-126">Hoe tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="07556-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="07556-127">Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="07556-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="07556-128">U werkt rechtstreeks vanaf een opdrachtregel tooprovision en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="07556-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="07556-129">Hoe toouse hello Azure CLI toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="07556-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="07556-130">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="07556-130">What you need</span></span>

- <span data-ttu-id="07556-131">Een Internet verbinding toodownload Hallo hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="07556-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="07556-132">Een Mac-computer met OS X Yosemite (10.10) of hoger.</span><span class="sxs-lookup"><span data-stu-id="07556-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="07556-133">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="07556-133">Install Git and Node.js</span></span>

<span data-ttu-id="07556-134">tooinstall Git en Node.js, gebruikt hulpprogramma voor Hallo Homebrew pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="07556-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="07556-135">[Download](http://brew.sh/) en Homebrew installeren.</span><span class="sxs-lookup"><span data-stu-id="07556-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="07556-136">Als u Homebrew al hebt geïnstalleerd, gaat u toostep 2.</span><span class="sxs-lookup"><span data-stu-id="07556-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="07556-137">Druk op `Cmd + Space` en voer `Terminal` tooopen een terminal.</span><span class="sxs-lookup"><span data-stu-id="07556-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="07556-138">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="07556-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="07556-139">Installeer Git en Node.js Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="07556-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="07556-140">Node.js ontwikkelingsprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="07556-140">Install Node.js development tools</span></span>

<span data-ttu-id="07556-141">U gebruikt [gulp.js](http://gulpjs.com/) tooautomate implementatie en uitvoering van scripts.</span><span class="sxs-lookup"><span data-stu-id="07556-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="07556-142">tooinstall gulp uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="07556-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="07556-143">Als u problemen met Hallo-installatie ondervindt, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="07556-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="07556-144">Knooppunt, NPM en Gulp zijn vereiste toorun automatiseringsscripts ontwikkeld in Node.js.</span><span class="sxs-lookup"><span data-stu-id="07556-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="07556-145">Installeren van Python</span><span class="sxs-lookup"><span data-stu-id="07556-145">Install Python</span></span>

<span data-ttu-id="07556-146">Hoewel Mac OS X wordt geleverd met Python 2.7, raden we u Python via Homebrew te installeren.</span><span class="sxs-lookup"><span data-stu-id="07556-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="07556-147">Zie [Python installeren op Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="07556-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="07556-148">Python en pip door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="07556-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="07556-149">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="07556-149">Install hello Azure CLI</span></span>

<span data-ttu-id="07556-150">tooinstall hello Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="07556-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="07556-151">Voer Hallo opdrachten in de terminal hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="07556-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="07556-152">Hallo-installatie kan 5 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="07556-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="07556-153">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="07556-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="07556-154">U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="07556-154">You should see hello following output if hello installation is successful.</span></span>

   ![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="07556-156">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="07556-156">Install Visual Studio Code</span></span>

<span data-ttu-id="07556-157">Visual Studio Code die u in configuratiebestanden Hallo-zelfstudie tooedit later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="07556-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="07556-158">[Download](https://code.visualstudio.com/docs/setup/osx) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="07556-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="07556-159">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="07556-159">Summary</span></span>

<span data-ttu-id="07556-160">U kunt alle Hallo vereist hulpprogramma's en software hebt geïnstalleerd op uw Mac-computer.</span><span class="sxs-lookup"><span data-stu-id="07556-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="07556-161">Uw volgende taak toouse hello Azure CLI toocreate is een IoT-hub en Registreer uw apparaat bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="07556-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07556-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07556-162">Next steps</span></span>
[<span data-ttu-id="07556-163">Een iothub maken en registreren van apparaat</span><span class="sxs-lookup"><span data-stu-id="07556-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
