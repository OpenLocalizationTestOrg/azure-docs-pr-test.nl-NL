---
title: Azure Linux virtuele Machines richtlijnen | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor het implementeren van virtuele Linux-machines in Azure
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 2d886795b301ab79272cae10a53831fd44c18f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>Richtlijnen voor Linux virtuele machines in Azure
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht in de vereiste stappen van de planning voor het maken en beheren van virtuele machines (VM's) binnen uw Azure-omgeving.

## <a name="implementation-guidelines-for-vms"></a>Richtlijnen voor de implementatie voor virtuele machines
Beslissingen te nemen:

* Hoeveel virtuele machines wilt u dat voor uw verschillende toepassingslagen en onderdelen van uw infrastructuur?
* Welke bronnen CPU en geheugen heeft elke VM nodig en wat zijn de opslagvereisten?

Taken:

* Definieer de werkbelastingen voor uw toepassing en de resources die zijn vereist voor de virtuele machines.
* De resource-eisen voor elke virtuele machine met het juiste VM-grootte en opslag type uitlijnen.
* Definieer uw resourcegroepen voor de verschillende lagen en de onderdelen van uw infrastructuur.
* Uw VM-naamgevingsconventie definiëren.
* Uw virtuele machines met de Azure CLI, web portal of met Resource Manager-sjablonen maken.

## <a name="virtual-machines"></a>Virtuele machines
Een van de belangrijkste resources in uw Azure-omgeving is waarschijnlijk virtuele machines. Deze resource is waar u uw toepassingen, databases, verificatieservices, enzovoort worden uitgevoerd.

Het is belangrijk dat u begrijpt de [andere VM-grootten](sizes.md) correct grootte van uw omgeving vanuit het oogpunt van prestaties en kosten van. Als uw VM's geen onvoldoende CPU-kernen of geheugen, de prestaties van uw toepassing leidt dit tot slechtere ongeacht hoe goed het is ontworpen en ontwikkeld. Bekijk de voorgestelde werkbelastingen voor elke VM-reeks als uitgangspunt nemen als u besluit welke grootte VM moet worden gebruikt voor elk onderdeel in uw infrastructuur. U kunt [de grootte van een virtuele machine wijzigen](change-vm-size.md) na de implementatie.

Opslag speelt een belangrijke rol in de prestaties van de virtuele machine. U kunt de Standard-opslag, die gebruikmaakt van reguliere draaiende schijven, of Premium-opslag gebruiken voor hoge i/o-werkbelastingen en optimale prestaties, die gebruikmaken van SSD-schijven. Als met de VM-grootte, er worden kosten verbonden overwegingen bij het selecteren van het opslagmedium. U vindt de [opslag infrastructuur richtlijnen artikel](infrastructure-storage-solutions-guidelines.md) om te begrijpen hoe ontwerp voor optimale prestaties van uw virtuele machines de juiste opslag.

## <a name="resource-groups"></a>Resourcegroepen
Onderdelen, zoals virtuele machines logisch zijn gegroepeerd voor eenvoudig beheer en onderhoud met behulp van [Azure-resourcegroepen](../../azure-resource-manager/resource-group-overview.md). Met behulp van resourcegroepen kunt u maken, beheren en bewaken van alle resources die gezamenlijk een bepaalde toepassing. U kunt ook implementeren [toegangsbeheer op basis van rollen](../../active-directory/role-based-access-control-what-is.md) toegang wilt verlenen aan andere gebruikers binnen uw team tot alleen de resources die ze nodig hebben. Tijd voor het plannen van uw resourcegroepen en roltoewijzingen in beslag nemen. Er zijn verschillende manieren daadwerkelijk ontwerpen en implementeren van resourcegroepen, dus Lees de [resource groepen richtlijnen artikel](infrastructure-resource-groups-guidelines.md) om te begrijpen hoe het beste naar het bouwen van uw virtuele machines.

## <a name="templates"></a>Sjablonen
U kunt sjablonen, gedefinieerd door declaratieve JSON-bestanden voor het maken van uw virtuele machines maken. Sjablonen doorgaans maken ook de vereiste opslag, netwerken, netwerkinterfaces, IP-adressering, enz. samen met de virtuele machines zelf. U kunt sjablonen maken consistent, reproduceerbare omgevingen voor ontwikkeling en testen doeleinden eenvoudig repliceren productieomgevingen en vice versa. U kunt meer lezen over [opbouwen en met behulp van sjablonen](../../azure-resource-manager/resource-group-overview.md#template-deployment) om te begrijpen hoe u ze kunt gebruiken voor het maken en implementeren van uw virtuele machines.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

