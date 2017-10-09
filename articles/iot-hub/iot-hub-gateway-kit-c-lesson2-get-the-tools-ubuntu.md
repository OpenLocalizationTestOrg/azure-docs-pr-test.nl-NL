---
title: 'SensorTag apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Hallo-hulpprogramma's en Hallo software installeren op de hostcomputer Ubuntu uitgevoerd, een iothub maken en Registreer uw apparaat in Hallo IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="bb63b-104">Hallo hulpprogramma's (Ubuntu 16.04) ophalen</span><span class="sxs-lookup"><span data-stu-id="bb63b-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb63b-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="bb63b-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="bb63b-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="bb63b-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="bb63b-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="bb63b-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="bb63b-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bb63b-108">What you will do</span></span>

- <span data-ttu-id="bb63b-109">Installeer Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="bb63b-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="bb63b-110">Hello Azure-opdrachtregelinterface (Azure CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="bb63b-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="bb63b-111">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bb63b-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="bb63b-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bb63b-112">What you will learn</span></span>

<span data-ttu-id="bb63b-113">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="bb63b-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="bb63b-114">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb63b-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="bb63b-115">GIT is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="bb63b-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="bb63b-116">Hallo-voorbeeldtoepassing voor deze les wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="bb63b-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="bb63b-117">Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="bb63b-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="bb63b-118">Hoe toouse NPM tooinstall Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="bb63b-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="bb63b-119">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="bb63b-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="bb63b-120">NPM is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb63b-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="bb63b-121">Hoe tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bb63b-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="bb63b-122">Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="bb63b-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bb63b-123">Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.</span><span class="sxs-lookup"><span data-stu-id="bb63b-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="bb63b-124">Hoe tooinstall hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb63b-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="bb63b-125">Hello Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="bb63b-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="bb63b-126">U werkt rechtstreeks vanaf een opdrachtregel tooprovision en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="bb63b-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="bb63b-127">Hoe toouse hello Azure CLI toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bb63b-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb63b-128">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bb63b-128">What you need</span></span>

- <span data-ttu-id="bb63b-129">Een Internet verbinding toodownload Hallo hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="bb63b-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="bb63b-130">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb63b-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="bb63b-131">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="bb63b-131">Install Git and Node.js</span></span>

<span data-ttu-id="bb63b-132">tooinstall Git- en Node.js, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="bb63b-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="bb63b-133">Druk op `Ctrl + Alt + T` tooopen een terminal.</span><span class="sxs-lookup"><span data-stu-id="bb63b-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="bb63b-134">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="bb63b-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="bb63b-135">Node.js ontwikkelingsprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="bb63b-135">Install Node.js development tools</span></span>

<span data-ttu-id="bb63b-136">U gebruikt [gulp.js](http://gulpjs.com/) tooautomate implementatie en uitvoering van scripts.</span><span class="sxs-lookup"><span data-stu-id="bb63b-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="bb63b-137">tooinstall gulp uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb63b-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="bb63b-138">Als u problemen met Hallo-installatie ondervindt, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-gateway-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="bb63b-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="bb63b-139">Knooppunt, NPM en Gulp zijn vereiste toorun automatiseringsscripts ontwikkeld in Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb63b-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="bb63b-140">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="bb63b-140">Install hello Azure CLI</span></span>

<span data-ttu-id="bb63b-141">tooinstall hello Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="bb63b-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="bb63b-142">Voer Hallo opdrachten in de terminal hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="bb63b-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="bb63b-143">Hallo-installatie kan 5 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="bb63b-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="bb63b-144">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb63b-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="bb63b-145">U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="bb63b-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="bb63b-146">![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="bb63b-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="bb63b-147">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="bb63b-147">Install Visual Studio Code</span></span>

<span data-ttu-id="bb63b-148">Visual Studio Code die u in configuratiebestanden Hallo-zelfstudie tooedit later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bb63b-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="bb63b-149">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="bb63b-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="bb63b-150">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bb63b-150">Summary</span></span>

<span data-ttu-id="bb63b-151">U kunt alle Hallo vereist hulpprogramma's en software hebt geïnstalleerd op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="bb63b-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="bb63b-152">Uw volgende taak toouse hello Azure CLI toocreate is een IoT-hub en Registreer uw apparaat bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bb63b-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb63b-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb63b-153">Next steps</span></span>
[<span data-ttu-id="bb63b-154">Een IoT-hub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="bb63b-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
