---
title: Hiermee stelt u aaaAvailability voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van Beschikbaarheidssets in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78e4da5c8fd9eb186cafacb46454444b73a9439c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a>Azure beschikbaarheidssets richtlijnen voor virtuele Linux-machines

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

In dit artikel is gericht op wat Hallo vereist planningsstappen voor tooensure van beschikbaarheidssets uw toepassingen bij gepland of ongepland gebeurtenissen toegankelijk blijft.

## <a name="implementation-guidelines-for-availability-sets"></a>Richtlijnen voor de implementatie van beschikbaarheidsset instellen
Beslissingen te nemen:

* Hoeveel beschikbaarheidssets hebt u nodig voor Hallo verschillende functies en lagen in de infrastructuur van uw toepassingen?

Taken:

* Definieer Hallo aantal virtuele machines in elke toepassingslaag die u nodig hebt.
* Bepaal of u tooadjust Hallo aantal fout- of update domeinen toobe gebruikt voor uw toepassing moet.
* Hallo vereist beschikbaarheidssets met uw naamgevingsconventie en wat definiëren virtuele machines zich bevinden. Een virtuele machine kan alleen worden opgenomen in een beschikbaarheidsset. 

## <a name="availability-sets"></a>Beschikbaarheidssets
In Azure, kunnen virtuele machines (VM's) worden geplaatst in logische groepering van tooa aangeroepen van een beschikbaarheidsset. Wanneer u virtuele machines binnen een beschikbaarheidsset maakt, distribueert hello Azure-platform Hallo plaatsing van deze VMs over Hallo onderliggende infrastructuur. Moet er een gebeurtenis toohello voor gepland onderhoud Azure-platform of een onderliggende hardware-infrastructuur fault, Hallo gebruik van beschikbaarheidssets zorgt ervoor dat er ten minste één virtuele machine actief blijft.

Als een best practice toepassingen moeten bevindt zich niet op een enkele virtuele machine. Een beschikbaarheidsset die een enkele virtuele machine bevat krijgen geen beveiliging bij gebeurtenissen voor gepland of ongepland binnen hello Azure-platform. Hallo [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines) twee of meer virtuele machines binnen een beschikbaarheid set tooallow Hallo verdeling van virtuele machines over Hallo onderliggende infrastructuur vereist. Als u [Azure Premium-opslag](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello Azure SLA van toepassing is tooa enkele VM.

Hallo onderliggende infrastructuur in Azure is onderverdeeld in toomultiple hardware clusters. Elk cluster hardware kan een bereik van VM-grootten ondersteunen. Een beschikbaarheidsset kan alleen worden gehost op een cluster met één hardware op elk punt in tijd. Hallo bereik van VM-grootten die kunnen optreden in een beschikbaarheidsset één is daarom beperkt toohello bereik van VM-grootten ondersteund door Hallo hardware cluster. Hallo hardware cluster voor de beschikbaarheidsset hello wordt geselecteerd wanneer hello eerste VM in de beschikbaarheidsset hello wordt geïmplementeerd of wanneer starten Hallo eerste VM in een beschikbaarheidsset waar alle VM's momenteel gestopt ongedaan Hallo-status zijn. Hallo na CLI-opdracht kan worden beschikbaar voor een beschikbaarheidsset gebruikte toodetermine Hallo bereik van VM-grootten: ' az vm lijst-grootten--locatie \<tekenreeks\>'

Elk cluster hardware is onderverdeeld in toomultiple update domeinen en domeinen met fouten. Deze domeinen zijn gedefinieerd door welke hosts delen een gemeenschappelijke Updatefase of share vergelijkbare fysieke infrastructuur zoals stroom en netwerken. Azure distribueert automatisch uw virtuele machines binnen een beschikbaarheidsset tussen domeinen toomaintain beschikbaarheid en fouttolerantie. Afhankelijk van de grootte van de Hallo van uw toepassing en het Hallo aantal virtuele machines binnen een beschikbaarheidsset, kunt u aanpassen Hallo-nummer van de domeinen die u wenst toouse. U kunt meer lezen over [beschikbaarheid en het gebruik van de update en fouttolerantie domeinen beheren](manage-availability.md).

Bij het ontwerpen van uw toepassing-infrastructuur hebt gepland Hallo toepassing lagen toouse. Groep virtuele machines die Hallo dienen hetzelfde doel in tooavailability sets, zoals een beschikbaarheidsset voor de front-virtuele machines met nginx of Apache. Maak een afzonderlijke beschikbaarheidsset voor uw back-end-VM's met MongoDB of MySQL. Hallo-doel is tooensure dat elk onderdeel van uw toepassing wordt beveiligd door een beschikbaarheidsset en ten minste eenmaal exemplaar altijd actief blijft.

Load balancers kunnen worden gebruikt voor elke toepassing laag toowork naast een beschikbaarheidsset en zorg ervoor dat verkeer kan altijd worden gerouteerde tooa met een exemplaar. Uw virtuele machines mogelijk blijven in bedrijf tijdens geplande en ongeplande onderhoud gebeurtenissen zonder een load balancer, maar de eindgebruiker mogelijk niet kunnen tooresolve indien hello primaire virtuele machine is niet beschikbaar.

Ontwerp uw toepassing voor hoge beschikbaarheid in de opslaglaag. Hallo aanbevolen procedure is te[gebruik beheerd de schijven voor virtuele machines in een Beschikbaarheidsset](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Als u momenteel niet-beheerde schijven gebruikt, raden wij ten zeerste aan u te[converteren van virtuele machines in de Beschikbaarheidsset toouse beheerd schijven](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

