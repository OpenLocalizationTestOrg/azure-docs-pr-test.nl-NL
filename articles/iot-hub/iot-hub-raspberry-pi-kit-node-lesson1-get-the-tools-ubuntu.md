---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi Hallo op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git op ubuntu, gulp uitvoeren, knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="a9ca5-104">Hallo hulpprogramma's (Ubuntu 16.04) ophalen</span><span class="sxs-lookup"><span data-stu-id="a9ca5-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9ca5-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="a9ca5-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="a9ca5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a9ca5-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="a9ca5-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="a9ca5-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="a9ca5-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a9ca5-108">What you will do</span></span>
<span data-ttu-id="a9ca5-109">Hallo-software voor Hallo eerste voorbeeldtoepassing voor frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="a9ca5-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a9ca5-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a9ca5-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a9ca5-111">What you will learn</span></span>
<span data-ttu-id="a9ca5-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="a9ca5-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a9ca5-113">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="a9ca5-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a9ca5-115">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a9ca5-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a9ca5-117">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a9ca5-118">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a9ca5-119">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="a9ca5-120">Wat moet u</span><span class="sxs-lookup"><span data-stu-id="a9ca5-120">What do you need</span></span>
<span data-ttu-id="a9ca5-121">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="a9ca5-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="a9ca5-122">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a9ca5-123">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="a9ca5-124">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="a9ca5-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="a9ca5-125">Gebruik Hallo sneltoets `Ctrl + Alt + T` tooopen een terminal en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a9ca5-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a9ca5-126">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="a9ca5-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="a9ca5-127">U gebruikt [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooPi.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="a9ca5-128">U ook hello gebruiken [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="a9ca5-129">Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="a9ca5-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="a9ca5-130">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a9ca5-131">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="a9ca5-131">Install Visual Studio Code</span></span>
<span data-ttu-id="a9ca5-132">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="a9ca5-133">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a9ca5-134">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a9ca5-135">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a9ca5-135">Summary</span></span>
<span data-ttu-id="a9ca5-136">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a9ca5-137">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.</span><span class="sxs-lookup"><span data-stu-id="a9ca5-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9ca5-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9ca5-138">Next steps</span></span>
[<span data-ttu-id="a9ca5-139">Hallo knipperen voorbeeldtoepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="a9ca5-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

