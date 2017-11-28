---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 2: Azure-hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) op Ubuntu installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 65248e14d0ea05a44efe76e66e1ef519285982b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="5f179-104">Ophalen van de Azure-hulpprogramma's (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5f179-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5f179-105">[Windows 7 en hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="5f179-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="5f179-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5f179-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5f179-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5f179-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5f179-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5f179-108">What you will do</span></span>
<span data-ttu-id="5f179-109">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="5f179-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5f179-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5f179-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5f179-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5f179-111">What you will learn</span></span>
<span data-ttu-id="5f179-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="5f179-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5f179-113">Klik hier voor meer informatie over het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5f179-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="5f179-114">Het toevoegen van een IoT-subgroep van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5f179-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5f179-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5f179-115">What you need</span></span>
* <span data-ttu-id="5f179-116">Een virtuele Ubuntu-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="5f179-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="5f179-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f179-117">An active Azure subscription.</span></span> <span data-ttu-id="5f179-118">Als u geen account hebt, kunt u een [gratis proefaccount](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="5f179-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="5f179-119">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="5f179-119">Install the Azure CLI</span></span>
<span data-ttu-id="5f179-120">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure, zodat u kunt werken rechtstreeks vanaf de opdrachtregel voor het inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="5f179-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="5f179-121">Volg deze stappen voor het installeren van de nieuwste Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="5f179-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5f179-122">Voer de volgende opdrachten in een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="5f179-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="5f179-123">Het duurt vijf minuten voor het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5f179-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="5f179-124">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="5f179-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5f179-125">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="5f179-125">You should see the following output if the installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="5f179-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5f179-127">Summary</span></span>
<span data-ttu-id="5f179-128">U kunt de Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5f179-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="5f179-129">Uw volgende taak is het maken van uw Azure IoT hub- en apparaatidentiteiten met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5f179-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f179-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f179-130">Next steps</span></span>
<span data-ttu-id="5f179-131">[Het maken van uw IoT-hub en Intel Edison registreren][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="5f179-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
