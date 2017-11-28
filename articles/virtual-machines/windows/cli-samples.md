---
title: aaaAzure CLI voorbeelden Windows | Microsoft Docs
description: Windows Azure CLI-voorbeelden
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="e4e24-103">Virtuele machines van Azure CLI-voorbeelden voor Windows</span><span class="sxs-lookup"><span data-stu-id="e4e24-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="e4e24-104">Hallo bevat volgende tabel koppelingen toobash scripts gebouwd met behulp van Azure CLI Hallo die Windows virtuele machines implementeren.</span><span class="sxs-lookup"><span data-stu-id="e4e24-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="e4e24-105">**Virtuele machines maken**</span><span class="sxs-lookup"><span data-stu-id="e4e24-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="e4e24-106">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="e4e24-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-107">Maakt een virtuele Windows-computer met een minimale configuratie.</span><span class="sxs-lookup"><span data-stu-id="e4e24-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="e4e24-108">Een volledig geconfigureerde virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="e4e24-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-109">Een resourcegroep, virtuele machine en alle gerelateerde resources gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e4e24-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="e4e24-110">Maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="e4e24-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-111">Maakt verschillende virtuele machines in een maximaal beschikbare en configuratie van taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="e4e24-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="e4e24-112">Een virtuele machine maken en voer het script voor configuratie</span><span class="sxs-lookup"><span data-stu-id="e4e24-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-113">Een virtuele machine maakt en hello Azure aangepast Script extensie tooinstall IIS gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e4e24-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="e4e24-114">Een virtuele machine maken en uitvoeren van de DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="e4e24-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-115">Een virtuele machine maakt en hello Azure Desired State Configuration (DSC)-extensie tooinstall IIS gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e4e24-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="e4e24-116">**Virtuele machines**</span><span class="sxs-lookup"><span data-stu-id="e4e24-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="e4e24-117">Beveiligen van netwerkverkeer tussen virtuele machines</span><span class="sxs-lookup"><span data-stu-id="e4e24-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-118">Hiermee maakt twee virtuele machines, alle gerelateerde resources en een interne en externe netwerkbeveiligingsgroepen (NSG).</span><span class="sxs-lookup"><span data-stu-id="e4e24-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="e4e24-119">**Beveiligde virtuele machines**</span><span class="sxs-lookup"><span data-stu-id="e4e24-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="e4e24-120">Versleutelen van een VM- en gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="e4e24-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-121">Een Azure Sleutelkluis, de versleutelingssleutel en de service-principal gemaakt en vervolgens een virtuele machine versleutelt.</span><span class="sxs-lookup"><span data-stu-id="e4e24-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="e4e24-122">**Virtuele machines bewaken**</span><span class="sxs-lookup"><span data-stu-id="e4e24-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="e4e24-123">Monitor voor een virtuele machine bij Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="e4e24-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="e4e24-124">Een virtuele machine maakt, Hallo Operations Management Suite-agent geïnstalleerd en schrijft Hallo VM in een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="e4e24-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
