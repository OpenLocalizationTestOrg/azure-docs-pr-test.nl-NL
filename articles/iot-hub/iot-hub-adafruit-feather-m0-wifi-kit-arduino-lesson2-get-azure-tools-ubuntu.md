---
title: 'Verbinding maken met Arduino tooAzure IoT - les 2: Azure-hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) op Ubuntu installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="ff6d1-104">Ophalen van de Azure-hulpprogramma's (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="ff6d1-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="ff6d1-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="ff6d1-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="ff6d1-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ff6d1-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ff6d1-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ff6d1-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ff6d1-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="ff6d1-108">What you will do</span></span>

<span data-ttu-id="ff6d1-109">Hello Azure-opdrachtregelinterface (Azure CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="ff6d1-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ff6d1-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="ff6d1-111">What you will learn</span></span>
<span data-ttu-id="ff6d1-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="ff6d1-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ff6d1-113">Hoe tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="ff6d1-114">Hoe tooadd een subgroep IoT Hallo Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ff6d1-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="ff6d1-115">What you need</span></span>
* <span data-ttu-id="ff6d1-116">Een virtuele Ubuntu-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="ff6d1-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-117">An active Azure subscription.</span></span> <span data-ttu-id="ff6d1-118">Als u geen account hebt, kunt u een [gratis proefaccount](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="ff6d1-119">Hello Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="ff6d1-119">Install hello Azure CLI</span></span>
<span data-ttu-id="ff6d1-120">Hello Azure CLI biedt meerdere platforms opdrachtregelprogramma voor Azure, zodat u toowork rechtstreeks vanuit uw tooprovision vanaf de opdrachtregel en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="ff6d1-121">tooinstall Hallo nieuwste Azure CLI, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="ff6d1-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="ff6d1-122">Hallo volgende opdrachten in een terminalvenster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="ff6d1-123">Vijf minuten tooinstall hello Azure CLI kan duren.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="ff6d1-124">Hallo installatie controleren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ff6d1-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="ff6d1-125">U ziet de volgende Hallo uitvoer als Hallo-installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-125">You should see hello following output if hello installation is successful.</span></span>

![Uitvoer die slagen aangeeft][output]

## <a name="summary"></a><span data-ttu-id="ff6d1-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ff6d1-127">Summary</span></span>
<span data-ttu-id="ff6d1-128">U kunt hello Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="ff6d1-129">Het is uw volgende taak toocreate uw Azure-IoT-hub en apparaten identiteit met hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ff6d1-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff6d1-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff6d1-130">Next steps</span></span>
<span data-ttu-id="ff6d1-131">[Het maken van uw IoT-hub en het mededelingenbord Arduino registreren][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="ff6d1-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md