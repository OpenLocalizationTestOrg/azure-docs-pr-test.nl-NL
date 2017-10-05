---
title: Het oplossen van veelvoorkomende problemen tijdens het maken van de VHD | Microsoft Docs
description: Antwoorden op veelgestelde vragen voor het oplossen van problemen en problemen tijdens het maken van de VHD.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="d2f1f-103">Het oplossen van veelvoorkomende problemen aangetroffen tijdens het maken van de VHD</span><span class="sxs-lookup"><span data-stu-id="d2f1f-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="d2f1f-104">In dit artikel is bedoeld om een Azure Marketplace-uitgever en/of medebeheerder die mogelijk problemen ervaren of Veelgestelde vragen hebben bij het publiceren en beheren van hun oplossing(en) virtuele machine te geven.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="d2f1f-105">Hoe wijzig ik de naam van de host</span><span class="sxs-lookup"><span data-stu-id="d2f1f-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="d2f1f-106">Zodra VM is gemaakt, kunnen gebruikers de naam van de host kunnen niet bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="d2f1f-107">Hoe de extern bureaublad-service of de aanmeldings-wachtwoord opnieuw instellen?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="d2f1f-108">Naslaginformatie voor Windows VM</span><span class="sxs-lookup"><span data-stu-id="d2f1f-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="d2f1f-109">Naslaginformatie voor virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="d2f1f-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="d2f1f-110">Het genereren van nieuwe ssh certificaten?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="d2f1f-111">Raadpleeg de koppeling: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="d2f1f-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="d2f1f-112">Het configureren van een VPN-certificaat voor openen?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="d2f1f-113">Raadpleeg de koppeling: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="d2f1f-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="d2f1f-114">Wat is het ondersteuningsbeleid voor Microsoft-serversoftware uitgevoerd in de Microsoft Azure-virtuele machine-omgeving (infrastructure-as-a-service)?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="d2f1f-115">Raadpleeg de koppeling: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="d2f1f-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="d2f1f-116">Virtuele Machines is beschikt over een unieke id?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="d2f1f-117">Azure codeert Azure VM unieke ID in elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="d2f1f-118">Zie de informatie in deze documentatie en blog.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="d2f1f-119">In een virtuele machine beheren de extensie voor aangepaste scripts in de taak starten?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="d2f1f-120">Raadpleeg de koppeling: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="d2f1f-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="d2f1f-121">Hoe kan ik een virtuele machine maken vanuit de Azure-portal met behulp van de VHD die is geüpload naar de premium-opslag?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="d2f1f-122">We bieden deze functie nog geen ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="d2f1f-123">Is een 32-bits app in Azure Marketplace ondersteund?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="d2f1f-124">Raadpleeg de koppeling voor meer informatie over het ondersteuningsbeleid: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="d2f1f-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="d2f1f-125">Elke keer dat ik wil een installatiekopie maken van mijn VHD's, verschijnt het foutbericht '. VHD is al geregistreerd bij de installatiekopieopslagplaats als resource' in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="d2f1f-126">Geen afbeelding voordat ik niet hebt gemaakt, noch heeft ik een afbeelding met deze naam vinden in Azure.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="d2f1f-127">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="d2f1f-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="d2f1f-128">Dit gebeurt meestal als de gebruiker een virtuele machine uit deze VHD ingericht en er is een vergrendeling op deze VHD.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="d2f1f-129">Controleer of er geen virtuele machine vanuit deze VHD toegewezen is.</span><span class="sxs-lookup"><span data-stu-id="d2f1f-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="d2f1f-130">Als de fout nog steeds blijft bestaan, klikt u vervolgens Verhoog een ondersteuningsticket via deze koppeling of van de publicatie portal met betrekking tot dit (details worden gegeven in het antwoord van vraag 11).</span><span class="sxs-lookup"><span data-stu-id="d2f1f-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>