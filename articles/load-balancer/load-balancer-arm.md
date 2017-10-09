---
title: Resource Manager-ondersteuning voor de Load Balancer aaaAzure | Microsoft Docs
description: Met behulp van powershell voor de Load Balancer met Azure Resource Manager. Met behulp van sjablonen voor de load balancer
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Ondersteuning van Azure Resource Manager gebruiken met Azure Load Balancer

Azure Resource Manager is Hallo voorkeursbeheerpunten framework voor services in Azure. Azure Load Balancer kunnen worden beheerd met Azure Resource Manager gebaseerde API's en hulpprogramma's.

## <a name="concepts"></a>Concepten

Met Resource Manager Azure Load Balancer bevat Hallo onderliggende resources te volgen:

* Front-end-IP-configuratie: een Load balancer kan een of meer front-end IP-adressen, ook bekend als een virtueel IP-adressen (VIP's) bevatten. Deze IP-adressen fungeren als inkomend voor Hallo-verkeer.
* Back-end-adresgroep: dit zijn IP-adressen die zijn gekoppeld aan virtuele machine voor Hallo Network Interface Card (NIC) toowhich load worden gedistribueerd.
* Taakverdeling regels: een regeleigenschap toegewezen een front-end opgegeven IP-adres en poort combinatie tooa set back-end-IP-adressen en combinatie van poort. Een enkele load balancer kan meerdere regels voor taakverdeling bevatten. Elke regel is een combinatie van een front-end IP en poort en back-end IP en poort die is gekoppeld aan virtuele machines.
* Tests – tests schakelt u tookeep bijhouden van Hallo status van de VM-exemplaren. Als u een health test mislukt, Hallo VM-instantie gaat buiten rotatie automatisch.
* Binnenkomende NAT regels – NAT-regels definiëren Hallo binnenkomend verkeer via Hallo-front-end-IP en gedistribueerde toohello terug IP eindigen.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Snelstartsjablonen

Azure Resource Manager kunt u tooprovision uw toepassingen met behulp van een declaratief sjabloon. U kunt in één enkele sjabloon meerdere services plus de bijbehorende afhankelijkheden implementeren. U hello gebruiken dezelfde sjabloon toorepeatedly uw toepassing tijdens elke fase van de levenscyclus van de toepassing hello implementeren.

Sjablonen kunnen definities voor virtuele Machines, virtuele netwerken, Beschikbaarheidssets, netwerkinterfaces (NIC's), Opslagaccounts, Load Balancers, Netwerkbeveiligingsgroepen en openbare IP-adressen bevatten. U kunt alles wat die u nodig hebt voor een complexe toepassing maken met behulp van sjablonen. Hallo-sjabloonbestand kan worden gecontroleerd in content management-systeem voor versiebeheer en samenwerking.

[Meer informatie over sjablonen](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Meer informatie over netwerkbronnen](../virtual-network/resource-groups-networking.md)

Met behulp van de Load Balancer van Azure-snelstartsjablonen vindt u in een [GitHub-opslagplaats](https://github.com/Azure/azure-quickstart-templates) die als host fungeert voor een set sjablonen community is gegenereerd.

Voorbeelden van sjablonen:

* [2 virtuele machines in een Load Balancer en taakverdelingsregels](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 virtuele machines in een VNET met een interne Load Balancer en Load Balancer-regels](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 virtuele machines in een Load Balancer en NAT-regels configureren op Hallo LB](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Azure Load Balancer met een PowerShell of CLI instellen

Aan de slag met Azure Resource Manager-cmdlets, opdrachtregel-hulpprogramma's en REST-API 's

* [Azure-netwerken Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) gebruikte toocreate een Load Balancer kunt worden.
* [Hoe toocreate een load balancer met Azure Resource Manager](load-balancer-get-started-ilb-arm-ps.md)
* [Hello Azure CLI gebruiken met Azure Resource Management](../xplat-cli-azure-resource-manager.md)
* [De Load Balancer REST-API 's](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Volgende stappen

U kunt ook [maken van de load balancer van een Internetgericht](load-balancer-get-started-internet-arm-ps.md) en configureren van welk type [distributie modus](load-balancer-distribution-mode.md) voor een specifieke load balancer-netwerk het gedrag van verkeer.

Meer informatie over hoe toomanage [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md). Dit is belangrijk wanneer uw toepassing tookeep verbindingen actief voor servers achter een load balancer moet.
