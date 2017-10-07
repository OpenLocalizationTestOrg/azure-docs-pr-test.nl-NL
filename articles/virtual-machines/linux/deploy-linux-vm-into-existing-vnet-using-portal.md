---
title: aaaDeploy virtuele Linux-machines in bestaande netwerk met Azure portal | Microsoft Docs
description: Linux-VM implementeren in een bestaand Azure virtueel netwerk met behulp van Hallo-portal.
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
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Hoe toodeploy virtuele Linux-machine in Azure een bestaand virtueel netwerk met hello Azure-portal

Dit artikel ziet u hoe toodeploy een virtuele machine (VM) in een bestaand virtueel netwerk (VNet). Azure activa zoals beveiligingsgroepen vnet's en het netwerk moeten statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven. Zodra een VNet is geïmplementeerd, kan opnieuw door constante nieuwe distributies zonder een nadelige invloed toohello infrastructuur worden gebruikt. Rekening houdt met een VNet dat deze een traditioneel netwerkswitch hardware - u hoeft dan niet een geheel nieuwe hardware overschakelen met elke implementatie tooconfigure.  

Met een juist geconfigureerde VNet, kunt u blijven toodeploy nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen gedurende de levensduur Hallo Hallo VNet vereist.

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Maak eerst een groep resource tooorganize alles wat die u in dit scenario maakt. Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Hallo VNet maken

Bouw een VNet toolaunch Hallo vervolgens, virtuele machines in. Hallo VNet bevat één subnet en is gekoppeld aan netwerkbeveiligingsgroep Hallo met dit subnet in een later stadium.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Een VNic toohello subnet toevoegen

Virtueel-netwerkkaarten (VNics) zijn belangrijk als u verbinding ze toodifferent virtuele machines maken kunt. Deze aanpak houdt Hallo VNic als statische resource Hallo VMs tijdelijke kan zijn. Een VNic maken en deze koppelen aan Hallo subnet in de vorige stap Hallo gemaakt.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Hallo netwerkbeveiligingsgroep maken

Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag. Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Regel voor geven van een binnenkomende SSH toevoegen

Hallo VM moet toegang vanaf Hallo internet, zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 doorgegeven op Hallo virtuele machine wordt gemaakt.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Hallo NSG koppelen aan Hallo subnet

Hallo subnet koppelen Hallo netwerkbeveiligingsgroep met Hallo VNet en Hallo subnet gemaakt. Netwerkbeveiligingsgroepen kunnen worden gekoppeld aan een hele subnet of een afzonderlijke VNic. Hallo Firewall voor het filteren van verkeer op Hallo subnetniveau, worden alle VNics en Hallo virtuele machines binnen Hallo subnet beveiligd door Hallo netwerkbeveiligingsgroep. Hallo is andere benadering Hallo network security groep wordt slechts een enkele VNic gekoppeld en slechts één virtuele machine te beveiligen.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Hallo VM in Hallo VNet en NSG implementeren

Gebruik hello Azure-portal, is Hallo Linux VM geïmplementeerde toohello bestaande Azure-resourcegroep, VNet Subnet en VNic.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Met behulp van bestaande resources van Hallo portal toochoose vertelt u Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo. Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.  

## <a name="next-steps"></a>Volgende stappen

* [Een Azure Resource Manager-sjabloon toocreate een specifieke implementatie gebruiken](../windows/cli-deploy-templates.md)
* [Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten](create-cli-complete.md)
* [Linux-VM in Azure met behulp van sjablonen maken](create-ssh-secured-vm-from-template.md)
