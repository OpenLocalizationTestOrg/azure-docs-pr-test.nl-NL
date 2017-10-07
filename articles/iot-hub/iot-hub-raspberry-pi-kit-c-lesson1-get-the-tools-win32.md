---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi Hallo op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, knooppunt js windows installeren, npm installeren op windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="022bb-104">Ophalen van Hallo hulpprogramma's (Windows 7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="022bb-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="022bb-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="022bb-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="022bb-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="022bb-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="022bb-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="022bb-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="022bb-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="022bb-108">What you will do</span></span>
<span data-ttu-id="022bb-109">Hallo-software voor Hallo eerste voorbeeldtoepassing voor frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden.</span><span class="sxs-lookup"><span data-stu-id="022bb-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="022bb-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="022bb-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="022bb-111">Hoewel Hallo programmeertaal van logische Hallo C, Node.js-hulpprogramma's worden gebruikt in Hallo uitkomsten toodiscover apparaten en voorbeeldtoepassingen maken en distribueren.</span><span class="sxs-lookup"><span data-stu-id="022bb-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="022bb-112">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="022bb-112">What you will learn</span></span>
<span data-ttu-id="022bb-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="022bb-113">In this article, you will learn:</span></span>

* <span data-ttu-id="022bb-114">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="022bb-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="022bb-115">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="022bb-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="022bb-116">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="022bb-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="022bb-117">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="022bb-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="022bb-118">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="022bb-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="022bb-119">Hallo minimum versievereisten voor Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="022bb-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="022bb-120">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="022bb-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="022bb-121">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="022bb-121">What you need</span></span>

<span data-ttu-id="022bb-122">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="022bb-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="022bb-123">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="022bb-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="022bb-124">Een computer waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="022bb-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="022bb-125">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="022bb-125">Install Git and Node.js</span></span>

<span data-ttu-id="022bb-126">Klik op onderstaande toodownload Hallo koppelingen en installeer Git en Node.js LTS voor Windows.</span><span class="sxs-lookup"><span data-stu-id="022bb-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="022bb-127">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="022bb-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="022bb-128">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="022bb-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="022bb-129">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="022bb-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="022bb-130">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooPi.</span><span class="sxs-lookup"><span data-stu-id="022bb-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="022bb-131">Gebruik Hallo [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="022bb-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="022bb-132">Start een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="022bb-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="022bb-133">Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="022bb-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="022bb-134">Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="022bb-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="022bb-135">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="022bb-135">Install Visual Studio Code</span></span>

<span data-ttu-id="022bb-136">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="022bb-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="022bb-137">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="022bb-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="022bb-138">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="022bb-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="022bb-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="022bb-139">Summary</span></span>

<span data-ttu-id="022bb-140">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="022bb-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="022bb-141">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.</span><span class="sxs-lookup"><span data-stu-id="022bb-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="022bb-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="022bb-142">Next steps</span></span>

[<span data-ttu-id="022bb-143">Hallo knipperen toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="022bb-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
