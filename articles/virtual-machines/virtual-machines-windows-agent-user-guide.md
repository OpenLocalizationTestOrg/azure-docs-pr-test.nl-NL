---
title: Overzicht van de virtuele Machine van Azure-Agent | Microsoft Docs
description: Overzicht van de virtuele Machine van Azure-Agent
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="196c3-103">Overzicht van Azure VM-Agent</span><span class="sxs-lookup"><span data-stu-id="196c3-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="196c3-104">De Agent in Microsoft Azure virtuele Machine (VM-Agent) is een beveiligde, lichtgewicht proces die VM interactie met de Azure-Infrastructuurcontroller beheert.</span><span class="sxs-lookup"><span data-stu-id="196c3-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="196c3-105">De VM-Agent heeft een primaire rol als inschakelen en het uitvoeren van de virtuele machine van Azure-extensies.</span><span class="sxs-lookup"><span data-stu-id="196c3-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="196c3-106">VM-extensies inschakelen na de implementatieconfiguratie van virtuele machines, zoals het installeren en configureren van software.</span><span class="sxs-lookup"><span data-stu-id="196c3-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="196c3-107">Uitbreidingen van de virtuele machine ook inschakelen herstelfuncties zoals het opnieuw instellen van het beheerderswachtwoord van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="196c3-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="196c3-108">Zonder de Azure VM-Agent kunnen niet uitbreidingen van de virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="196c3-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="196c3-109">In dit document worden de installatie, detectie en verwijdering van de Azure VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="196c3-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="196c3-110">De VM-Agent installeren</span><span class="sxs-lookup"><span data-stu-id="196c3-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="196c3-111">Afbeelding van de Azure-galerie</span><span class="sxs-lookup"><span data-stu-id="196c3-111">Azure gallery image</span></span>

<span data-ttu-id="196c3-112">De Azure VM-Agent is standaard geïnstalleerd op een Windows-virtuele machine op basis van een installatiekopie van een Azure-galerie geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="196c3-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="196c3-113">Bij het implementeren van een installatiekopie van een Azure-galerie van de Portal, PowerShell, opdrachtregelinterface of een Azure Resource Manager-sjabloon is de Azure VM-Agent ook worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="196c3-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="196c3-114">Handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="196c3-114">Manual installation</span></span>

<span data-ttu-id="196c3-115">De virtuele machine van Windows-agent kan handmatig worden geïnstalleerd met behulp van een Windows installer-pakket.</span><span class="sxs-lookup"><span data-stu-id="196c3-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="196c3-116">Handmatige installatie kan nodig zijn bij het maken van de installatiekopie van een aangepaste virtuele machine die wordt geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="196c3-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="196c3-117">Voor handmatige installatie van de VM-Agent van Windows, kunt u het VM-Agent-installatieprogramma downloaden vanaf deze locatie [Windows Azure VM-Agent downloaden](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="196c3-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="196c3-118">De VM-Agent kan worden geïnstalleerd door te dubbelklikken op het windows installer-bestand.</span><span class="sxs-lookup"><span data-stu-id="196c3-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="196c3-119">Voer de volgende opdracht voor een automatisch of zonder toezicht-installatie van de VM-agent.</span><span class="sxs-lookup"><span data-stu-id="196c3-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="196c3-120">Detecteren van de VM-Agent</span><span class="sxs-lookup"><span data-stu-id="196c3-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="196c3-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="196c3-121">PowerShell</span></span>

<span data-ttu-id="196c3-122">De Azure Resource Manager PowerShell-module kan worden gebruikt voor het ophalen van informatie over Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="196c3-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="196c3-123">Met `Get-AzureRmVM` retourneert behoorlijk een stukje informatie, inclusief de Inrichtingsstatus voor de Azure VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="196c3-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="196c3-124">Het volgende is slechts een subset van de `Get-AzureRmVM` uitvoer.</span><span class="sxs-lookup"><span data-stu-id="196c3-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="196c3-125">U ziet de `ProvisionVMAgent` eigenschap genest in `OSProfile`, deze eigenschap kan worden gebruikt om te bepalen of de VM-agent is geïmplementeerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="196c3-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="196c3-126">Het volgende script kan worden gebruikt om te retourneren van een beknopte lijst met namen van de virtuele machine en de status van de VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="196c3-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="196c3-127">Handmatige detectie</span><span class="sxs-lookup"><span data-stu-id="196c3-127">Manual Detection</span></span>

<span data-ttu-id="196c3-128">Wanneer u aangemeld bij een virtuele machine van Windows Azure, kan Taakbeheer om te onderzoeken actieve processen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="196c3-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="196c3-129">Om te controleren of de Azure VM-Agent, opent u Taakbeheer > Klik op het tabblad met details en zoekt u naar een procesnaam `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="196c3-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="196c3-130">De aanwezigheid van dit proces geeft aan dat de VM-agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="196c3-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="196c3-131">Upgrade van de VM-Agent</span><span class="sxs-lookup"><span data-stu-id="196c3-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="196c3-132">De Azure VM-Agent voor Windows, wordt automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="196c3-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="196c3-133">Als u nieuwe virtuele machines worden geïmplementeerd in Azure, krijgen ze de meest recente VM-agent.</span><span class="sxs-lookup"><span data-stu-id="196c3-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="196c3-134">Aangepaste VM-installatiekopieën moeten handmatig worden bijgewerkt zodat de nieuwe VM-agent.</span><span class="sxs-lookup"><span data-stu-id="196c3-134">Custom VM images should be manually updated to include the new VM agent.</span></span>