---
title: aaaDifferent manieren toocreate een Windows-VM in Azure | Microsoft Docs
description: Geeft een lijst Hallo verschillende manieren toocreate virtuele Windows-machine met Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="d362a-103">Verschillende manieren toocreate virtuele Windows-machine</span><span class="sxs-lookup"><span data-stu-id="d362a-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="d362a-104">Azure biedt verschillende manieren toocreate een virtuele machine omdat de virtuele machines zijn geschikt voor verschillende gebruikers en doelstellingen.</span><span class="sxs-lookup"><span data-stu-id="d362a-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="d362a-105">Dit betekent dat u toomake enkele mogelijkheden over Hallo virtuele machine moet en hoe toocreate deze.</span><span class="sxs-lookup"><span data-stu-id="d362a-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="d362a-106">In dit artikel krijgt u een overzicht van deze keuzes en tooinstructions koppelingen.</span><span class="sxs-lookup"><span data-stu-id="d362a-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="d362a-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d362a-107">Azure portal</span></span>
<span data-ttu-id="d362a-108">Met behulp van hello Azure-portal is een eenvoudige manier tootry uit een virtuele machine, vooral als u net met Azure begint.</span><span class="sxs-lookup"><span data-stu-id="d362a-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="d362a-109">Maak een virtuele machine met Windows met behulp van Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="d362a-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="d362a-110">Template</span><span class="sxs-lookup"><span data-stu-id="d362a-110">Template</span></span>
<span data-ttu-id="d362a-111">Virtuele machines vereisen een combinatie van resources (zoals een beschikbare sets en storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="d362a-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="d362a-112">In plaats van te implementeren en beheren van elke resource afzonderlijk, kunt u een Azure Resource Manager-sjabloon die u implementeert en richt alle Hallo resources in een enkele, gecoördineerde bewerking.</span><span class="sxs-lookup"><span data-stu-id="d362a-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="d362a-113">Een virtuele Windows-machine maken met een Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="d362a-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="d362a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d362a-114">Azure PowerShell</span></span>
<span data-ttu-id="d362a-115">Als u liever in een opdrachtshell werkt, kunt u Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d362a-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="d362a-116">Een Windows-VM maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d362a-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="d362a-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d362a-117">Visual Studio</span></span>
<span data-ttu-id="d362a-118">Gebruik Visual Studio toobuild, beheren, en implementeren van virtuele machines met hello Azure Tools voor Visual Studio en hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="d362a-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="d362a-119">Azure-hulpprogramma's voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d362a-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

