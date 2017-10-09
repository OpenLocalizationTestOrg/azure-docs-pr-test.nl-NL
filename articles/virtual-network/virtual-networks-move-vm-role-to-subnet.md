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
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Verplaatsen van een virtuele machine (klassiek) of Cloud Services-rol exemplaar tooa ander subnet met behulp van PowerShell
U kunt PowerShell toomove uw virtuele machines (klassiek) van één subnet tooanother Hallo hetzelfde virtuele netwerk (VNet). Rolinstanties kunnen worden verplaatst met het bewerken van Hallo CSCFG-bestand in plaats van met behulp van PowerShell.

> [!NOTE]
> Dit artikel wordt uitgelegd hoe toomove virtuele machines worden geïmplementeerd via Hallo klassieke implementatiemodel alleen.
> 
> 

Waarom virtuele machines tooanother subnet verplaatsen? Migratie van subnet is nuttig wanneer Hallo oudere subnet te klein is en kan niet worden uitgebreid vanwege tooexisting VM's worden uitgevoerd in dat subnet. In dat geval kunt u een nieuwe, groter subnet maken en migreren Hallo VMs toohello nieuw subnet en nadat de migratie is voltooid, kunt u oude leeg subnet Hallo verwijderen.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Hoe een VM-subnet tooanother toomove
toomove een virtuele machine, Voer Hallo Set AzureSubnet PowerShell-cmdlet Hallo onderstaand voorbeeld als sjabloon gebruiken. In onderstaande Hallo voorbeeld, we TestVM verplaatst van de huidige subnet tooSubnet 2. Niet zeker tooedit Hallo voorbeeld tooreflect uw omgeving. Houd er rekening mee dat wanneer u Hallo Update-AzureVM cmdlet als onderdeel van een procedure uitvoert, deze opnieuw wordt opgestart uw virtuele machine als onderdeel van het updateproces Hallo.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Als u een statische interne persoonlijke IP-adres voor de virtuele machine opgegeven, hebt u tooclear die instelling voordat u Hallo VM tooa nieuw subnet kunt verplaatsen. In dat geval gebruikt u Hallo volgende:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove een rol exemplaar tooanother subnet
toomove een rolinstantie hello CSCFG-bestand bewerken. In onderstaande Hallo voorbeeld, verplaatst we 'Role0' in het virtuele netwerk *VNETName* van de huidige subnet te*Subnet 2*. Omdat de rolinstantie Hallo al is geïmplementeerd, wijzigt u zojuist hebt Hallo subnetnaam = Subnet 2. Niet zeker tooedit Hallo voorbeeld tooreflect uw omgeving.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
