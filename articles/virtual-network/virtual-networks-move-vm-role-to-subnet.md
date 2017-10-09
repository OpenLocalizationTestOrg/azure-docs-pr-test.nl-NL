---
title: aaaMove een virtuele machine (klassiek) of Cloud Services-rol exemplaar tooa ander subnet - Azure PowerShell | Microsoft Docs
description: Meer informatie over hoe toomove VMs (klassiek) en Cloud Services-rol exemplaren tooa ander subnet met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="c30df-103">Verplaatsen van een virtuele machine (klassiek) of Cloud Services-rol exemplaar tooa ander subnet met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c30df-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="c30df-104">U kunt PowerShell toomove uw virtuele machines (klassiek) van één subnet tooanother Hallo hetzelfde virtuele netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="c30df-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="c30df-105">Rolinstanties kunnen worden verplaatst met het bewerken van Hallo CSCFG-bestand in plaats van met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c30df-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="c30df-106">Dit artikel wordt uitgelegd hoe toomove virtuele machines worden geïmplementeerd via Hallo klassieke implementatiemodel alleen.</span><span class="sxs-lookup"><span data-stu-id="c30df-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="c30df-107">Waarom virtuele machines tooanother subnet verplaatsen?</span><span class="sxs-lookup"><span data-stu-id="c30df-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="c30df-108">Migratie van subnet is nuttig wanneer Hallo oudere subnet te klein is en kan niet worden uitgebreid vanwege tooexisting VM's worden uitgevoerd in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="c30df-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="c30df-109">In dat geval kunt u een nieuwe, groter subnet maken en migreren Hallo VMs toohello nieuw subnet en nadat de migratie is voltooid, kunt u oude leeg subnet Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c30df-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="c30df-110">Hoe een VM-subnet tooanother toomove</span><span class="sxs-lookup"><span data-stu-id="c30df-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="c30df-111">toomove een virtuele machine, Voer Hallo Set AzureSubnet PowerShell-cmdlet Hallo onderstaand voorbeeld als sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c30df-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="c30df-112">In onderstaande Hallo voorbeeld, we TestVM verplaatst van de huidige subnet tooSubnet 2.</span><span class="sxs-lookup"><span data-stu-id="c30df-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="c30df-113">Niet zeker tooedit Hallo voorbeeld tooreflect uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="c30df-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="c30df-114">Houd er rekening mee dat wanneer u Hallo Update-AzureVM cmdlet als onderdeel van een procedure uitvoert, deze opnieuw wordt opgestart uw virtuele machine als onderdeel van het updateproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="c30df-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="c30df-115">Als u een statische interne persoonlijke IP-adres voor de virtuele machine opgegeven, hebt u tooclear die instelling voordat u Hallo VM tooa nieuw subnet kunt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c30df-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="c30df-116">In dat geval gebruikt u Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="c30df-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="c30df-117">toomove een rol exemplaar tooanother subnet</span><span class="sxs-lookup"><span data-stu-id="c30df-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="c30df-118">toomove een rolinstantie hello CSCFG-bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="c30df-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="c30df-119">In onderstaande Hallo voorbeeld, verplaatst we 'Role0' in het virtuele netwerk *VNETName* van de huidige subnet te*Subnet 2*.</span><span class="sxs-lookup"><span data-stu-id="c30df-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="c30df-120">Omdat de rolinstantie Hallo al is geïmplementeerd, wijzigt u zojuist hebt Hallo subnetnaam = Subnet 2.</span><span class="sxs-lookup"><span data-stu-id="c30df-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="c30df-121">Niet zeker tooedit Hallo voorbeeld tooreflect uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="c30df-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
