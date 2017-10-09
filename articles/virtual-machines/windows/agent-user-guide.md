---
title: Overzicht van virtuele machines Agent aaaAzure | Microsoft Docs
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
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="70d9e-103">Overzicht van Azure VM-Agent</span><span class="sxs-lookup"><span data-stu-id="70d9e-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="70d9e-104">Hallo Microsoft Azure-Agent voor virtuele Machine (AM Agent) is een beveiligde, lichtgewicht proces die VM interactie met hello Azure-Infrastructuurcontroller beheert.</span><span class="sxs-lookup"><span data-stu-id="70d9e-104">hello Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="70d9e-105">Hallo VM-Agent heeft een primaire rol als inschakelen en het uitvoeren van de virtuele machine van Azure-extensies.</span><span class="sxs-lookup"><span data-stu-id="70d9e-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="70d9e-106">VM-extensies inschakelen na de implementatieconfiguratie van virtuele machines, zoals het installeren en configureren van software.</span><span class="sxs-lookup"><span data-stu-id="70d9e-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="70d9e-107">Uitbreidingen van de virtuele machine ook inschakelen herstelfuncties zoals het opnieuw instellen van Hallo beheerderswachtwoord van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="70d9e-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="70d9e-108">Zonder hello Azure VM-Agent, de uitbreidingen van de virtuele machine kunnen niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70d9e-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="70d9e-109">In dit document worden de installatie, detectie en verwijdering van hello Azure VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="70d9e-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="70d9e-110">Hallo VM-Agent installeren</span><span class="sxs-lookup"><span data-stu-id="70d9e-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="70d9e-111">Afbeelding van de Azure-galerie</span><span class="sxs-lookup"><span data-stu-id="70d9e-111">Azure gallery image</span></span>

<span data-ttu-id="70d9e-112">Hello Azure VM-Agent wordt standaard geïnstalleerd op een Windows-virtuele machine op basis van een installatiekopie van een Azure-galerie geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="70d9e-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="70d9e-113">Bij het implementeren van een installatiekopie van een Azure-galerie van Hallo Portal, PowerShell, opdrachtregelinterface of een Azure Resource Manager-sjabloon worden hello die Azure VM-Agent ook is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="70d9e-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="70d9e-114">Handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="70d9e-114">Manual installation</span></span>

<span data-ttu-id="70d9e-115">Hallo Windows VM-agent kan handmatig worden geïnstalleerd met behulp van een Windows installer-pakket.</span><span class="sxs-lookup"><span data-stu-id="70d9e-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="70d9e-116">Handmatige installatie kan nodig zijn bij het maken van de installatiekopie van een aangepaste virtuele machine die wordt geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="70d9e-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="70d9e-117">toomanually installatie Hallo Windows VM-Agent, Hallo VM-Agent-installatieprogramma downloaden vanaf deze locatie [Windows Azure VM-Agent downloaden](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="70d9e-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="70d9e-118">Hallo VM-Agent kan worden geïnstalleerd door te dubbelklikken op Hallo windows installer-bestand.</span><span class="sxs-lookup"><span data-stu-id="70d9e-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="70d9e-119">Voor een automatisch of zonder toezicht-installatie van de VM-agent Hallo Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70d9e-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="70d9e-120">Hallo VM-Agent detecteren</span><span class="sxs-lookup"><span data-stu-id="70d9e-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="70d9e-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70d9e-121">PowerShell</span></span>

<span data-ttu-id="70d9e-122">Hello Azure Resource Manager PowerShell-module kan worden gebruikt tooretrieve informatie over Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="70d9e-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="70d9e-123">Met `Get-AzureRmVM` retourneert behoorlijk een stukje informatie, met inbegrip van Hallo Inrichtingsstatus voor hello Azure VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="70d9e-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="70d9e-124">Hallo volgende is slechts een subset van Hallo `Get-AzureRmVM` uitvoer.</span><span class="sxs-lookup"><span data-stu-id="70d9e-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="70d9e-125">Kennisgeving Hallo `ProvisionVMAgent` eigenschap genest in `OSProfile`, is deze eigenschap de gebruikte toodetermine als Hallo VM-agent toohello geïmplementeerde virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="70d9e-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="70d9e-126">Hallo na script kan worden gebruikt tooreturn een beknopte lijst met namen van de virtuele machine en status Hallo Hallo VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="70d9e-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="70d9e-127">Handmatige detectie</span><span class="sxs-lookup"><span data-stu-id="70d9e-127">Manual Detection</span></span>

<span data-ttu-id="70d9e-128">Als Windows Azure VM tooa aangemeld, worden Taakbeheer gebruikte tooexamine actieve processen.</span><span class="sxs-lookup"><span data-stu-id="70d9e-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="70d9e-129">toocheck voor hello Azure VM-Agent, opent u Taakbeheer > Hallo tabblad met details op en zoek naar een procesnaam `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="70d9e-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="70d9e-130">Hallo aanwezigheid van dit proces geeft dat die Hallo VM-agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="70d9e-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="70d9e-131">Hallo VM-Agent bijwerken</span><span class="sxs-lookup"><span data-stu-id="70d9e-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="70d9e-132">Hello Azure VM-Agent voor Windows, wordt automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="70d9e-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="70d9e-133">Als u nieuwe virtuele machines zijn geïmplementeerd tooAzure, krijgen ze Hallo nieuwste VM-agent.</span><span class="sxs-lookup"><span data-stu-id="70d9e-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="70d9e-134">Aangepaste installatiekopieën voor virtuele machine moet de handmatig bijgewerkte tooinclude Hallo nieuwe VM-agent.</span><span class="sxs-lookup"><span data-stu-id="70d9e-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
