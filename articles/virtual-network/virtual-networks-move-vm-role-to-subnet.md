---
title: Een VM (klassiek) of een exemplaar van Cloud Services-rol verplaatsen naar een ander subnet - Azure PowerShell | Microsoft Docs
description: Informatie over het verplaatsen van virtuele machines (klassiek) en Cloud Services-rolinstanties naar een ander subnet met behulp van PowerShell.
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
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="605c3-103">Een VM (klassiek) of een exemplaar van Cloud Services-rol verplaatsen naar een ander subnet met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="605c3-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="605c3-104">U kunt PowerShell gebruiken voor het verplaatsen van uw virtuele machines (klassiek) van één subnet naar de andere in hetzelfde virtuele netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="605c3-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="605c3-105">Rolinstanties kunnen worden verplaatst met het bewerken van het CSCFG-bestand in plaats van met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="605c3-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="605c3-106">In dit artikel wordt uitgelegd hoe verplaatsen van virtuele machines te implementeren via het klassieke implementatiemodel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="605c3-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="605c3-107">Waarom virtuele machines verplaatsen naar een ander subnet?</span><span class="sxs-lookup"><span data-stu-id="605c3-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="605c3-108">Migratie van subnet is handig wanneer de oudere subnet te klein is en kan niet worden uitgebreid vanwege bestaande actieve virtuele machines in dat subnet.</span><span class="sxs-lookup"><span data-stu-id="605c3-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="605c3-109">In dat geval kunt u een nieuwe, groter subnet maken en de virtuele machines migreren naar het nieuwe subnet en nadat de migratie is voltooid, kunt u het oude leeg subnet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="605c3-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="605c3-110">Een virtuele machine verplaatsen naar een ander subnet</span><span class="sxs-lookup"><span data-stu-id="605c3-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="605c3-111">Voer de Set AzureSubnet PowerShell-cmdlet met het onderstaande voorbeeld als sjabloon voor het verplaatsen van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="605c3-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="605c3-112">In het onderstaande voorbeeld verplaatst we TestVM van de huidige subnet naar Subnet 2.</span><span class="sxs-lookup"><span data-stu-id="605c3-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="605c3-113">Zorg ervoor dat het voorbeeld naar aanleiding van uw omgeving bewerken.</span><span class="sxs-lookup"><span data-stu-id="605c3-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="605c3-114">Houd er rekening mee dat wanneer u de cmdlet Update-AzureVM als onderdeel van een procedure uitvoert, deze opnieuw wordt opgestart uw virtuele machine als onderdeel van het updateproces.</span><span class="sxs-lookup"><span data-stu-id="605c3-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="605c3-115">Als u een statische interne persoonlijke IP-adres voor de virtuele machine opgegeven, hebt u deze instelling te wissen voordat u de virtuele machine naar een nieuw subnet verplaatsen kunt.</span><span class="sxs-lookup"><span data-stu-id="605c3-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="605c3-116">In dat geval gebruikt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="605c3-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="605c3-117">Een rolinstantie verplaatsen naar een ander subnet</span><span class="sxs-lookup"><span data-stu-id="605c3-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="605c3-118">Bewerk het CSCFG-bestand voor het verplaatsen van een rolexemplaar.</span><span class="sxs-lookup"><span data-stu-id="605c3-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="605c3-119">In het onderstaande voorbeeld verplaatst we 'Role0' in het virtuele netwerk *VNETName* van de aanwezig subnet *Subnet 2*.</span><span class="sxs-lookup"><span data-stu-id="605c3-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="605c3-120">Omdat de rolinstantie al is geïmplementeerd, moet u alleen de subnetnaam wijzigen = Subnet 2.</span><span class="sxs-lookup"><span data-stu-id="605c3-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="605c3-121">Zorg ervoor dat het voorbeeld naar aanleiding van uw omgeving bewerken.</span><span class="sxs-lookup"><span data-stu-id="605c3-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
