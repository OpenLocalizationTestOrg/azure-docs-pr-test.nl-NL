---
title: aaaAzure Linux virtuele Machines richtlijnen | Microsoft Docs
description: Informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van virtuele Linux-machines in Azure
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
ms.openlocfilehash: 0f779f791005441b6b16e106a3dc5a095bb33034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>Richtlijnen voor Linux virtuele machines in Azure
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

In dit artikel is gericht op wat Hallo vereist voor het plannen van stappen voor het maken en beheren van virtuele machines (VM's) binnen uw Azure-omgeving.

## <a name="implementation-guidelines-for-vms"></a>Richtlijnen voor de implementatie voor virtuele machines
Beslissingen te nemen:

* Hoeveel virtuele machines wilt u dat voor uw verschillende toepassingslagen en onderdelen van uw infrastructuur?
* Welke bronnen CPU en geheugen heeft elke VM nodig en wat zijn de opslagvereisten Hallo?

Taken:

* Definieer Hallo werkbelastingen voor uw toepassing en Hallo resources Hallo die VM 's vereisen.
* Hallo resourcebehoeften voor elke virtuele machine met Hallo geschikte VM omvang en opslag type uitlijnen.
* Definieer uw resourcegroepen voor de verschillende lagen Hallo en onderdelen van uw infrastructuur.
* Uw VM-naamgevingsconventie definiëren.
* Uw virtuele machines met behulp van hello Azure CLI, web portal of met Resource Manager-sjablonen maken.

## <a name="virtual-machines"></a>Virtuele machines
Een van de belangrijkste resources binnen uw Azure-omgeving Hallo is waarschijnlijk virtuele machines. Deze resource is waar u uw toepassingen, databases, verificatieservices, enzovoort worden uitgevoerd.

Het is belangrijk toounderstand hello [andere VM-grootten](sizes.md) toocorrectly het formaat van uw omgeving vanuit het oogpunt van prestaties en kosten van. Als uw VM's geen onvoldoende CPU-kernen of geheugen, de prestaties van uw toepassing leidt dit tot slechtere ongeacht hoe goed het is ontworpen en ontwikkeld. Bekijk Hallo voorgesteld werkbelastingen voor elke VM-reeks als uitgangspunt nemen als u welke grootte VM toouse voor elk onderdeel in uw infrastructuur besluit. U kunt [Hallo grootte van een virtuele machine wijzigen](change-vm-size.md) na de implementatie.

Opslag speelt een belangrijke rol in de prestaties van de virtuele machine. U kunt de Standard-opslag, die gebruikmaakt van reguliere draaiende schijven, of Premium-opslag gebruiken voor hoge i/o-werkbelastingen en optimale prestaties, die gebruikmaken van SSD-schijven. Als Hello VM-grootte, er worden kosten verbonden overwegingen tooselecting Hallo opslagmedium. U kunt lezen Hallo [opslag infrastructuur richtlijnen artikel](infrastructure-storage-solutions-guidelines.md) toounderstand hoe toodesign opslag voor optimale prestaties van uw virtuele machines nodig.

## <a name="resource-groups"></a>Resourcegroepen
Onderdelen, zoals virtuele machines logisch zijn gegroepeerd voor eenvoudig beheer en onderhoud met behulp van [Azure-resourcegroepen](../../azure-resource-manager/resource-group-overview.md). Met behulp van resourcegroepen kunt u maken, beheren en bewaken van alle Hallo-resources die gezamenlijk een bepaalde toepassing. U kunt ook implementeren [toegangsbeheer op basis van rollen](../../active-directory/role-based-access-control-what-is.md) toogrant toegang tooothers binnen uw team tooonly Hallo resources ze nodig hebben. Tooplan uit uw resourcegroepen en roltoewijzingen tijd in beslag nemen. Er zijn verschillende benaderingen tooactually ontwerpen en implementeren van resourcegroepen, dus wees zeker tooread hello [resource groepen richtlijnen artikel](infrastructure-resource-groups-guidelines.md) toounderstand hoe best toobuild uit uw virtuele machines.

## <a name="templates"></a>Sjablonen
U kunt sjablonen, gedefinieerd door declaratieve JSON-bestanden, toocreate opbouwen uw virtuele machines. Sjablonen doorgaans bouwen ook Hallo vereist opslag, netwerken, netwerkinterfaces, IP-adressering, enz. samen met de Hallo VM's zelf. U kunt sjablonen toocreate consistente, reproduceerbare omgevingen gebruiken voor ontwikkeling en tests doeleinden tooeasily productieomgevingen repliceren en vice versa. U kunt meer lezen over [opbouwen en met behulp van sjablonen](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand hoe u ze gebruiken kunt voor het maken en implementeren van uw virtuele machines.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

