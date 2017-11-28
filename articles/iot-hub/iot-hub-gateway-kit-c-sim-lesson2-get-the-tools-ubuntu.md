---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 2: ophalen van de hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: De hulpprogramma's en de software installeren op de hostcomputer Ubuntu uitgevoerd, een iothub maken en Registreer uw apparaat in de IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, iot-cloudservice, internet der dingen software, azure cli, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 349daf5c3206f7fc20662beebd16928624142a56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="aafcb-104">De hulpprogramma's downloaden (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="aafcb-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aafcb-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="aafcb-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="aafcb-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="aafcb-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="aafcb-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="aafcb-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="aafcb-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="aafcb-108">What you will do</span></span>

- <span data-ttu-id="aafcb-109">Installeer Git, Node.js, Gulp, Python.</span><span class="sxs-lookup"><span data-stu-id="aafcb-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="aafcb-110">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="aafcb-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="aafcb-111">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="aafcb-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="aafcb-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="aafcb-112">What you will learn</span></span>

<span data-ttu-id="aafcb-113">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="aafcb-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="aafcb-114">Klik hier voor meer informatie over het installeren van Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="aafcb-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="aafcb-115">GIT is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="aafcb-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="aafcb-116">De voorbeeldtoepassing voor deze les wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="aafcb-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="aafcb-117">Node.js is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="aafcb-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="aafcb-118">Hoe Node.js ontwikkelingsprogramma's installeren met NPM.</span><span class="sxs-lookup"><span data-stu-id="aafcb-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="aafcb-119">De minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="aafcb-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="aafcb-120">NPM is een van de pakket-managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="aafcb-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="aafcb-121">Klik hier voor meer informatie over het installeren van Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="aafcb-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="aafcb-122">Visual Studio Code is een platformoverschrijdende, eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="aafcb-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="aafcb-123">Het biedt uitstekende ondersteuning voor foutopsporing, ingesloten Git besturingselement syntaxismarkering, intelligent code is voltooid, fragmenten en code refactoring ook.</span><span class="sxs-lookup"><span data-stu-id="aafcb-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="aafcb-124">Het installeren van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aafcb-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="aafcb-125">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure.</span><span class="sxs-lookup"><span data-stu-id="aafcb-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="aafcb-126">U werkt rechtstreeks vanaf een opdrachtregel inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="aafcb-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="aafcb-127">Het gebruik van de Azure CLI voor het maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aafcb-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aafcb-128">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="aafcb-128">What you need</span></span>

- <span data-ttu-id="aafcb-129">Een internetverbinding beschikken om het downloaden van de hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="aafcb-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="aafcb-130">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aafcb-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="aafcb-131">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="aafcb-131">Install Git and Node.js</span></span>

<span data-ttu-id="aafcb-132">Volg deze stappen voor het installeren van de Git- en Node.js:</span><span class="sxs-lookup"><span data-stu-id="aafcb-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="aafcb-133">Druk op `Ctrl + Alt + T` een terminal openen.</span><span class="sxs-lookup"><span data-stu-id="aafcb-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="aafcb-134">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="aafcb-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="aafcb-135">Node.js ontwikkelingsprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="aafcb-135">Install Node.js development tools</span></span>

<span data-ttu-id="aafcb-136">U gebruikt [gulp.js](http://gulpjs.com/) te automatiseren, implementatie en uitvoering van scripts.</span><span class="sxs-lookup"><span data-stu-id="aafcb-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="aafcb-137">Als u wilt installeren gulp, voer de volgende opdracht in de terminal:</span><span class="sxs-lookup"><span data-stu-id="aafcb-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="aafcb-138">Als u problemen bij de installatie ondervindt, raadpleegt u de [probleemoplossingsgids](iot-hub-gateway-kit-c-sim-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="aafcb-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="aafcb-139">Knooppunt, NPM en Gulp zijn vereist om uit te voeren automatiseringsscripts ontwikkeld in Node.js.</span><span class="sxs-lookup"><span data-stu-id="aafcb-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="aafcb-140">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="aafcb-140">Install the Azure CLI</span></span>

<span data-ttu-id="aafcb-141">Volg deze stappen voor het installeren van de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="aafcb-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="aafcb-142">Voer de volgende opdrachten in de terminal:</span><span class="sxs-lookup"><span data-stu-id="aafcb-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="aafcb-143">De installatie kan 5 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="aafcb-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="aafcb-144">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="aafcb-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="aafcb-145">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="aafcb-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="aafcb-146">![Controleer of de installatie van de Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="aafcb-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="aafcb-147">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="aafcb-147">Install Visual Studio Code</span></span>

<span data-ttu-id="aafcb-148">U kunt Visual Studio Code verderop in de zelfstudie configuratiebestanden bewerken.</span><span class="sxs-lookup"><span data-stu-id="aafcb-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="aafcb-149">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="aafcb-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="aafcb-150">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="aafcb-150">Summary</span></span>

<span data-ttu-id="aafcb-151">U hebt de vereiste hulpprogramma's en software op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="aafcb-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="aafcb-152">Uw volgende taak is het gebruik van de Azure CLI voor het maken van een IoT-hub en Registreer uw apparaat bij uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aafcb-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aafcb-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aafcb-153">Next steps</span></span>
[<span data-ttu-id="aafcb-154">Een IoT-hub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="aafcb-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
