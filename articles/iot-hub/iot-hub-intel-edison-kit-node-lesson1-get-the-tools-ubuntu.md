---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 1: download hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Download en installeer Hallo vereiste hulpprogramma's en -software voor de eerste voorbeeldtoepassing voor Edison Hallo op Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino ontwikkelingsprogramma's, iot-ontwikkeling, iot-software, internet van dingen software, git op ubuntu, installatie knooppunt js ubuntu installeren
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="508fc-104">Hallo hulpprogramma's (Ubuntu 16.04) ophalen</span><span class="sxs-lookup"><span data-stu-id="508fc-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="508fc-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="508fc-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="508fc-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="508fc-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="508fc-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="508fc-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="508fc-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="508fc-108">What you will do</span></span>
<span data-ttu-id="508fc-109">Hallo ontwikkelingsprogramma's en software voor eerste voorbeeldtoepassing voor uw Edison Intel Hallo Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="508fc-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="508fc-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="508fc-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="508fc-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="508fc-111">What you will learn</span></span>
<span data-ttu-id="508fc-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="508fc-112">In this article, you will learn:</span></span>

* <span data-ttu-id="508fc-113">Hoe tooinstall Git en Node.js</span><span class="sxs-lookup"><span data-stu-id="508fc-113">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="508fc-114">[GIT](https://git-scm.com) is een open-source gedistribueerd versiebeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="508fc-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="508fc-115">Hallo-voorbeeldtoepassing voor dit artikel wordt opgeslagen op Git.</span><span class="sxs-lookup"><span data-stu-id="508fc-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="508fc-116">[Node.js](https://nodejs.org/en/) is een JavaScript-runtime met een uitgebreide pakket-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="508fc-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="508fc-117">Hoe toouse NPM tooinstall extra Node.js ontwikkelingsprogramma's.</span><span class="sxs-lookup"><span data-stu-id="508fc-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="508fc-118">Hallo minimaal vereiste versie van Node.js is 4.5 TNS.</span><span class="sxs-lookup"><span data-stu-id="508fc-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="508fc-119">[NPM](https://www.npmjs.com) is een van de Hallo pakket managers voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="508fc-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="508fc-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="508fc-120">What you need</span></span>
<span data-ttu-id="508fc-121">toocomplete deze bewerking moet u:</span><span class="sxs-lookup"><span data-stu-id="508fc-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="508fc-122">Een Internet verbinding toodownload Hallo ontwikkelingsprogramma's en software Hallo.</span><span class="sxs-lookup"><span data-stu-id="508fc-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="508fc-123">Een computer die Ubuntu 16.04 of hoger wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="508fc-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="508fc-124">Installeer Git, Node.js en NPM</span><span class="sxs-lookup"><span data-stu-id="508fc-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="508fc-125">Gebruik Hallo sneltoets `Ctrl + Alt + T` tooopen een terminal en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="508fc-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="508fc-126">Extra hulpprogramma's voor Node.js-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="508fc-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="508fc-127">Gebruik [gulp.js](http://gulpjs.com) tooautomate Hallo implementatie van Hallo voorbeeld toepassing tooEdison.</span><span class="sxs-lookup"><span data-stu-id="508fc-127">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="508fc-128">Installeer `gulp` door het uitvoeren van de volgende opdracht in de terminal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="508fc-128">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="508fc-129">Als u problemen hebt met het installeren van Node.js en deze extra ontwikkelprogramma's op Ubuntu, Zie Hallo [probleemoplossingsgids] [ troubleshooting] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="508fc-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="508fc-130">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="508fc-130">Install Visual Studio Code</span></span>
<span data-ttu-id="508fc-131">[Download](https://code.visualstudio.com/docs/setup/linux) en Visual Studio Code installeren.</span><span class="sxs-lookup"><span data-stu-id="508fc-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="508fc-132">Visual Studio Code is een eenvoudige maar krachtige broncode-editor voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="508fc-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="508fc-133">U gebruikt deze editor verderop in Hallo zelfstudie tooedit Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="508fc-133">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="508fc-134">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="508fc-134">Summary</span></span>
<span data-ttu-id="508fc-135">U kunt Hallo vereist ontwikkelingsprogramma's en -software voor het eerste voorbeeldtoepassing hello hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="508fc-135">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="508fc-136">de volgende taak Hallo is toocreate, implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison.</span><span class="sxs-lookup"><span data-stu-id="508fc-136">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="508fc-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="508fc-137">Next steps</span></span>
<span data-ttu-id="508fc-138">[Hallo knipperen voorbeeldtoepassing maken en implementeren][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="508fc-138">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
