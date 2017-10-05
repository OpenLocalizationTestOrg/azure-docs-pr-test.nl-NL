---
title: 'Connect Intel Edison (C) naar Azure IoT - les 2: Azure-hulpprogramma''s (Ubuntu) | Microsoft Docs'
description: Python en Azure-opdrachtregelinterface (Azure CLI) op Ubuntu installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure cli, iot-cloudservice, arduino cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 897ab63af85a1f830ed49084ce7c3e74c84a4cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="a0541-104">Ophalen van de Azure-hulpprogramma's (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="a0541-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a0541-105">[Windows 7 en hoger][windows]</span><span class="sxs-lookup"><span data-stu-id="a0541-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="a0541-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a0541-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a0541-107">[Mac OS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a0541-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a0541-108">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a0541-108">What you will do</span></span>
<span data-ttu-id="a0541-109">Installeer de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="a0541-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="a0541-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a0541-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0541-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a0541-111">What you will learn</span></span>
<span data-ttu-id="a0541-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="a0541-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a0541-113">Klik hier voor meer informatie over het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a0541-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="a0541-114">Het toevoegen van een IoT-subgroep van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a0541-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0541-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a0541-115">What you need</span></span>
* <span data-ttu-id="a0541-116">Een virtuele Ubuntu-computer met een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="a0541-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="a0541-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0541-117">An active Azure subscription.</span></span> <span data-ttu-id="a0541-118">Als u geen account hebt, kunt u een [gratis proefaccount](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="a0541-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="a0541-119">Azure-CLI installeren</span><span class="sxs-lookup"><span data-stu-id="a0541-119">Install the Azure CLI</span></span>
<span data-ttu-id="a0541-120">De Azure CLI biedt een meerdere platforms opdrachtregelprogramma ervaring voor Azure, zodat u kunt werken rechtstreeks vanaf de opdrachtregel voor het inrichten en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="a0541-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="a0541-121">Volg deze stappen voor het installeren van de nieuwste Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="a0541-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a0541-122">Voer de volgende opdrachten in een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="a0541-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="a0541-123">Het duurt vijf minuten voor het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a0541-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="a0541-124">De installatie controleren door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a0541-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="a0541-125">U ziet de volgende uitvoer als de installatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="a0541-125">You should see the following output if the installation is successful.</span></span>

![Uitvoer die slagen aangeeft](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="a0541-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a0541-127">Summary</span></span>
<span data-ttu-id="a0541-128">U kunt de Azure CLI hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a0541-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="a0541-129">Uw volgende taak is het maken van uw Azure IoT hub- en apparaatidentiteiten met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a0541-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0541-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0541-130">Next steps</span></span>
<span data-ttu-id="a0541-131">[Het maken van uw IoT-hub en Intel Edison registreren][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="a0541-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
