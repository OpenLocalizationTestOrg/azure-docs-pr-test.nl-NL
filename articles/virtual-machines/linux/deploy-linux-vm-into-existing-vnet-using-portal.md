---
title: Implementeren van virtuele Linux-machines in bestaande netwerk met Azure portal | Microsoft Docs
description: Implementeer een Linux-VM naar een bestaande Azure-netwerk met behulp van de portal.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a>Het implementeren van een virtuele Linux-machine in Azure een bestaand virtueel netwerk met de Azure-portal

In dit artikel laat zien hoe een virtuele machine (VM) implementeren in een bestaand virtueel netwerk (VNet). Azure activa zoals beveiligingsgroepen vnet's en het netwerk moeten statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven. Zodra een VNet is geïmplementeerd, kan dit opnieuw gebruikt door constante nieuwe distributies zonder een ongewenst is van invloed op de infrastructuur. Rekening houdt met een VNet dat deze een traditioneel netwerkswitch hardware - u niet moet een geheel nieuwe hardwareswitch configureren met elke implementatie.  

U kunt blijven implementeren nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen die zijn vereist tijdens de levensduur van het VNet met een juist geconfigureerde VNet.

## <a name="create-the-resource-group"></a>De resourcegroep maken

Maak eerst een resourcegroep te organiseren alles wat die u in dit scenario maakt. Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a>Het VNet maken

Vervolgens start de virtuele machines in een VNet maken. Het VNet bevat één subnet en is gekoppeld aan de netwerkbeveiligingsgroep met dit subnet in een later stadium.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a>Een VNic toevoegen aan het subnet

Virtueel-netwerkkaarten (VNics) zijn belangrijk omdat u ze met andere virtuele machines verbinden kunt. Deze aanpak houdt de VNic als statische resource terwijl de virtuele machines kunnen tijdelijk zijn. Een VNic maken en deze koppelen aan het subnet in de vorige stap hebt gemaakt.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a>De netwerkbeveiligingsgroep maken

Beveiligingsgroepen voor Azure-netwerk zijn equivalent aan een firewall op de netwerklaag. Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Regel voor geven van een binnenkomende SSH toevoegen

De virtuele machine moet toegang via het internet, zodat een regel binnenkomende poort 22-verkeer via het netwerk worden doorgegeven aan poort 22 op de virtuele machine wordt gemaakt.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a>Het NSG koppelen aan het subnet

Met het VNet en het subnet dat is gemaakt door de netwerkbeveiligingsgroep te koppelen aan het subnet. Netwerkbeveiligingsgroepen kunnen worden gekoppeld aan een hele subnet of een afzonderlijke VNic. Alle VNics en de virtuele machines binnen het subnet met de firewall verkeer op subnetniveau filteren, worden beveiligd door de netwerkbeveiligingsgroep. De andere benadering is de netwerkbeveiligingsgroep kan met slechts een enkele VNic en beveiligende slechts één virtuele machine worden gekoppeld.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a>Implementeer de virtuele machine in het VNet en het NSG

Met de Azure portal, wordt de Linux-VM geïmplementeerd op de bestaande Azure-resourcegroep, VNet, Subnet en VNic.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Via de portal om te kiezen bestaande resources vertelt u Azure voor het implementeren van de virtuele machine binnen de bestaande netwerk. Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.  

## <a name="next-steps"></a>Volgende stappen

* [Een Azure Resource Manager-sjabloon gebruiken om een specifieke implementatie te maken](../windows/cli-deploy-templates.md)
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md)
