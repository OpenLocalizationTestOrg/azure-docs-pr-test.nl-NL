---
title: Ondersteuning voor de Load Balancer van Azure Resource Manager | Microsoft Docs
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
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Ondersteuning van Azure Resource Manager gebruiken met Azure Load Balancer

Azure Resource Manager is het framework voorkeursbeheerpunten voor services in Azure. Azure Load Balancer kunnen worden beheerd met Azure Resource Manager gebaseerde API's en hulpprogramma's.

## <a name="concepts"></a>Concepten

Met Resource Manager Azure Load Balancer bevat de volgende onderliggende bronnen:

* Front-end-IP-configuratie: een Load balancer kan een of meer front-end IP-adressen, ook bekend als een virtueel IP-adressen (VIP's) bevatten. Deze IP-adressen fungeren als ingang voor het verkeer.
* Back-end-adresgroep: dit zijn IP-adressen die zijn gekoppeld met de virtuele machine Network Interface Card (NIC) die load worden gedistribueerd.
* Taakverdelingsregels: een regeleigenschap wordt een opgegeven front-end-IP- en de combinatie van poort aan een set van back-end-IP-adressen en de poort toegewezen. Een enkele load balancer kan meerdere regels voor taakverdeling bevatten. Elke regel is een combinatie van een front-end IP en poort en back-end IP en poort die is gekoppeld aan virtuele machines.
* Tests-tests kunnen u om de status van de VM-exemplaren bij te houden. Als u een health test mislukt, de VM-instantie gaat buiten rotatie automatisch.
* Binnenkomende NAT-regels – NAT-regels definiëren van het binnenkomende verkeer via de voorgrond IP beëindigen en gedistribueerd naar de back-end-IP.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Snelstartsjablonen

Met Azure Resource Manager kunt u uw toepassingen inrichten aan de hand van een declaratieve sjabloon. U kunt in één enkele sjabloon meerdere services plus de bijbehorende afhankelijkheden implementeren. U gebruikt dezelfde sjabloon om uw toepassing herhaaldelijk te implementeren in elke fase van de levenscyclus van de toepassing.

Sjablonen kunnen definities voor virtuele Machines, virtuele netwerken, Beschikbaarheidssets, netwerkinterfaces (NIC's), Opslagaccounts, Load Balancers, Netwerkbeveiligingsgroepen en openbare IP-adressen bevatten. U kunt alles wat die u nodig hebt voor een complexe toepassing maken met behulp van sjablonen. Het sjabloonbestand kan worden gecontroleerd in content management-systeem voor versiebeheer en samenwerking.

[Meer informatie over sjablonen](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Meer informatie over netwerkbronnen](../virtual-network/resource-groups-networking.md)

Met behulp van de Load Balancer van Azure-snelstartsjablonen vindt u in een [GitHub-opslagplaats](https://github.com/Azure/azure-quickstart-templates) die als host fungeert voor een set sjablonen community is gegenereerd.

Voorbeelden van sjablonen:

* [2 virtuele machines in een Load Balancer en taakverdelingsregels](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 virtuele machines in een VNET met een interne Load Balancer en Load Balancer-regels](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 virtuele machines in een Load Balancer en NAT-regels configureren op de Load Balancer](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Azure Load Balancer met een PowerShell of CLI instellen

Aan de slag met Azure Resource Manager-cmdlets, opdrachtregel-hulpprogramma's en REST-API 's

* [Azure-netwerken Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) kan worden gebruikt voor het maken van een Load Balancer.
* [Het maken van een load balancer met Azure Resource Manager](load-balancer-get-started-ilb-arm-ps.md)
* [De Azure CLI gebruiken met Azure Resourcemanagement](../xplat-cli-azure-resource-manager.md)
* [De Load Balancer REST-API 's](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Volgende stappen

U kunt ook [maken van de load balancer van een Internetgericht](load-balancer-get-started-internet-arm-ps.md) en configureren van welk type [distributie modus](load-balancer-distribution-mode.md) voor een specifieke load balancer-netwerk het gedrag van verkeer.

Meer informatie over het beheren van [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md). Dit is belangrijk wanneer uw toepassing moet verbindingen keepalive voor servers achter een load balancer.
