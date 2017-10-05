---
title: 'Arduino verbinden met Azure IoT - les 2: Azure-hulpprogramma''s (Ubuntu) | Microsoft Docs'
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
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="f8243-104">Ophalen van de Azure-hulpprogramma's (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f8243-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="f8243-105">[Windows 7 of hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="f8243-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="f8243-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="f8243-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="f8243-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="f8243-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f8243-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="f8243-108">What you will do</span></span>

<span data-ttu-id="f8243-109">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f8243-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="f8243-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="f8243-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f8243-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="f8243-111">What you will learn</span></span>
<span data-ttu-id="f8243-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="f8243-112">In this article, you will learn:</span></span>
* <span data-ttu-id="f8243-113">Klik hier voor meer informatie over het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f8243-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="f8243-114">Het toevoegen van een IoT-subgroep van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f8243-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f8243-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="f8243-115">What you need</span></span>
* <span data-ttu-id="f8243-116">Een virtuele Ubuntu-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="f8243-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="f8243-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8243-117">An active Azure subscription.</span></span> <span data-ttu-id="f8243-118">Als u geen account hebt, kunt u een [gratis proefaccount](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="f8243-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="f8243-119">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="f8243-119">Install the Azure CLI</span></span>
<span data-ttu-id="f8243-120">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure, zodat u kunt werken rechtstreeks vanaf de opdrachtregel voor het inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="f8243-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="f8243-121">Volg deze stappen voor het installeren van de nieuwste Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="f8243-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f8243-122">Voer de volgende opdrachten in een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="f8243-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="f8243-123">Het duurt vijf minuten voor het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f8243-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="f8243-124">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f8243-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="f8243-125">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="f8243-125">You should see the following output if the installation is successful.</span></span>

![Uitvoer die slagen aangeeft][output]

## <a name="summary"></a><span data-ttu-id="f8243-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f8243-127">Summary</span></span>
<span data-ttu-id="f8243-128">U kunt de Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f8243-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="f8243-129">Uw volgende taak is het maken van uw Azure IoT hub- en apparaatidentiteiten met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f8243-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8243-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8243-130">Next steps</span></span>
<span data-ttu-id="f8243-131">[Het maken van uw IoT-hub en het mededelingenbord Arduino registreren][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="f8243-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md