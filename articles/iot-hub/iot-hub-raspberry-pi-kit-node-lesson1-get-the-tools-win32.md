---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Windows) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Pi Hallo op Windows 7 en hoger.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-ontwikkeling, iot-software, internet van dingen software, installeer git voor windows, gulp uitvoeren, knooppunt js windows installeren, npm installeren op windows, python installeren op windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="bb78e-104">Ophalen van Hallo hulpprogramma's (Windows 7 of hoger)</span><span class="sxs-lookup"><span data-stu-id="bb78e-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb78e-105">Windows 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="bb78e-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="bb78e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="bb78e-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="bb78e-107">Mac OS 10.10</span><span class="sxs-lookup"><span data-stu-id="bb78e-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="bb78e-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bb78e-108">What you will do</span></span>
<span data-ttu-id="bb78e-109">Hallo-software voor Hallo eerste voorbeeldtoepassing voor frambozen Pi 3 en Hallo ontwikkelingsprogramma's downloaden.</span><span class="sxs-lookup"><span data-stu-id="bb78e-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="bb78e-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bb78e-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bb78e-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bb78e-111">What you will learn</span></span>
<span data-ttu-id="bb78e-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="bb78e-112">In this article, you will learn:</span></span>

* <span data-ttu-id="bb78e-113">Hoe tooinstall Git en Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb78e-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="bb78e-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="bb78e-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="bb78e-115">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="bb78e-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="bb78e-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="bb78e-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="bb78e-117">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="bb78e-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="bb78e-118">Hallo minimum versievereisten voor Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="bb78e-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="bb78e-119">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="bb78e-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb78e-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bb78e-120">What you need</span></span>
<span data-ttu-id="bb78e-121">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="bb78e-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="bb78e-122">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="bb78e-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="bb78e-123">Een computer waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb78e-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="bb78e-124">Installeer Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="bb78e-124">Install Git and Node.js</span></span>
<span data-ttu-id="bb78e-125">Klik op Hallo toodownload koppelingen volgen en Git en Node.js LTS voor Windows installeren.</span><span class="sxs-lookup"><span data-stu-id="bb78e-125">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="bb78e-126">Ophalen van Git voor Windows</span><span class="sxs-lookup"><span data-stu-id="bb78e-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="bb78e-127">Node.js TNS ophalen voor Windows</span><span class="sxs-lookup"><span data-stu-id="bb78e-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="bb78e-128">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="bb78e-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="bb78e-129">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooPi.</span><span class="sxs-lookup"><span data-stu-id="bb78e-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="bb78e-130">U ook hello gebruiken [apparaat detectie cli](https://github.com/Azure/device-discovery-cli) tooretrieve netwerkinformatie over uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="bb78e-130">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="bb78e-131">Start een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bb78e-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="bb78e-132">Installeer `gulp` en `device-discovery-cli` door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb78e-132">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="bb78e-133">Als u problemen hebt met het installeren van Node.js en deze extra Node.js ontwikkelprogramma's op uw computer, Zie Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="bb78e-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="bb78e-134">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="bb78e-134">Install Visual Studio Code</span></span>
<span data-ttu-id="bb78e-135">[Download](https://code.visualstudio.com/docs/setup/windows) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="bb78e-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="bb78e-136">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="bb78e-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bb78e-137">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="bb78e-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="bb78e-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bb78e-138">Summary</span></span>
<span data-ttu-id="bb78e-139">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bb78e-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="bb78e-140">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi.</span><span class="sxs-lookup"><span data-stu-id="bb78e-140">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb78e-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb78e-141">Next steps</span></span>
[<span data-ttu-id="bb78e-142">Hallo knipperen voorbeeldtoepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="bb78e-142">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

