---
title: Voorbeelden van de CLI aaaAzure | Microsoft Docs
description: Voorbeelden van Azure CLI
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Azure CLI-voorbeelden voor netwerken

Hallo bevat volgende tabel koppelingen toobash scripts gebouwd met behulp van hello Azure CLI.

| | |
|-|-|
|**Connectiviteit tussen Azure-resources**||
| [Een virtueel netwerk voor toepassingen met meerdere lagen maken](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Hiermee maakt een virtueel netwerk met front-end en back-end-subnetten. Verkeer toohello front-end-subnet is beperkt tooHTTP en SSH, tijdens het verkeer toohello back-end-subnet is beperkt tooMySQL, poort 3306. |
| [Peer twee virtuele netwerken](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Maakt en verbinding maakt twee virtuele netwerken in Hallo dezelfde regio. |
| [-Routeverkeer via een virtueel netwerkapparaat](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Maakt een virtueel netwerk met de front-end en back-end-subnetten en een virtuele machine die verkeer tussen Hallo twee subnetten kunnen tooroute is. |
| [Filteren van binnenkomende en uitgaande netwerkverkeer voor VM](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Hiermee maakt een virtueel netwerk met front-end en back-end-subnetten. Binnenkomend netwerkverkeer toohello front-end-subnet is beperkt tooHTTP, HTTPS en SSH. Uitgaand verkeer toohello Internet van Hallo back-end-subnet is niet toegestaan. |
|**Load balancing en verkeer richting**||
| [Laden van saldo verkeer tooVMs voor hoge beschikbaarheid](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Maakt verschillende virtuele machines in een maximaal beschikbare en configuratie van taakverdeling. |
| [Taakverdeling maken voor meerdere websites op virtuele machines](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Hiermee maakt twee virtuele machines met meerdere IP-configuraties, gekoppelde tooan Azure Beschikbaarheidsset, toegankelijk via een Azure Load Balancer. |
| [Directe verkeer over meerdere regio's voor hoge beschikbaarheid](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Hiermee maakt twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten. |
| | |
