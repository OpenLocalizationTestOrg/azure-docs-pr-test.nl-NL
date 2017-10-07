---
title: virtuele machine van Windows deployment-klassieke aaaTroubleshoot | Microsoft Docs
description: Klassieke implementatieproblemen bij het maken van een nieuwe Windows virtuele machine in Azure oplossen
services: virtual-machines-windows
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f01d237-ba39-4c32-b72d-18f5f505d43a
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cjiang
ms.openlocfilehash: aa12cb013a18e0572fbef8b7ea69106dd47c1fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a>Klassieke implementatieproblemen met het maken van een nieuwe Windows virtuele machine in Azure oplossen
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor Hallo Resource Manager-versie van dit artikel [hier](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>De auditlogboeken verzamelen
het oplossen van problemen toostart verzamelen Hallo audit registreert tooidentify Hallo fout Hallo probleem gekoppeld.

Klik in hello Azure-portal, op **Bladeren** > **virtuele machines** > *uw Windows-machine*  >   **Instellingen** > **controlelogboeken**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** als Hallo OS Windows gegeneraliseerd, en deze wordt geüpload en/of vastgelegd Hello gegeneraliseerd instellen, wordt niet eventuele fouten. Op dezelfde manier als Hallo OS Windows speciaal bedoeld is, en deze wordt geüpload en/of vastgelegd met gespecialiseerde Hallo instelling, en eventuele fouten niet.

**Fouten uploaden:**

**N<sup>1</sup>:** als Hallo OS Windows gegeneraliseerd en is geüpload als gespecialiseerde, ontvangt u een inrichting time-outfout Hello VM bij OOBE-welkomstscherm vastgelopen.

**N<sup>2</sup>:** als Hallo OS is Windows gespecialiseerde en als gegeneraliseerd is geüpload, krijgt u een inrichting is mislukt met de Hallo VM bij OOBE-welkomstscherm vastgelopen omdat hello nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computer Hallo naam, gebruikersnaam en wachtwoord.

**Oplossing:**

tooresolve beide deze fouten uploaden Hallo oorspronkelijke VHD, beschikbare on-premises, Hallo met dezelfde instelling als die voor Hallo OS (gegeneraliseerd/specifieke). tooupload zoals gegeneraliseerd, moet u eerst toorun sysprep. Zie [maken en uploaden van een Windows Server-VHD tooAzure](createupload-vhd.md) voor meer informatie.

**Vastleggen fouten:**

**N<sup>3</sup>:** als Hallo OS Windows gegeneraliseerd en deze wordt vastgelegd als gespecialiseerde, ontvangt u een inrichting time-outfout omdat Hallo oorspronkelijke VM kan niet worden gebruikt als deze is gemarkeerd als gegeneraliseerd.

**N<sup>4</sup>:** als Hallo OS is Windows gespecialiseerde en deze is vastgelegd, zoals gegeneraliseerd, krijgt u een inrichting is mislukt omdat hello nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam hello, gebruikersnaam en wachtwoord. Bovendien Hallo oorspronkelijke VM kan niet worden gebruikt omdat deze is gemarkeerd als gespecialiseerde.

**Oplossing:**

tooresolve beide deze fouten Hallo huidige installatiekopie verwijderen vanuit de portal Hallo en [opnieuw vastleggen van Hallo huidige VHD's](capture-image.md) Hallo met dezelfde instelling als die voor Hallo OS (gegeneraliseerd/specifieke).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Probleem: Aangepaste / galerie / marketplace-installatiekopie; Toewijzingsfout
Deze fout in situaties zich voordoet wanneer de nieuwe VM-aanvraag Hallo tooa-cluster dat ofwel geen beschikbare vrije ruimte tooaccommodate Hallo aanvraag heeft wordt verzonden of Hallo aangevraagde VM-grootte kan niet worden ondersteund. Het is niet mogelijk toomix andere reeks van virtuele machines in Hallo dezelfde cloudservice. Dus als u wilt dat toocreate een nieuwe virtuele machine van een ander formaat dan wat uw cloudservice kan ondersteunen, mislukt Hallo compute aanvraag.

Afhankelijk van de beperkingen van de cloudservice Hallo Hallo u toocreate Hallo van nieuwe virtuele machine, een fout is veroorzaakt door een van twee situaties kunnen optreden.

**1 oorzaak:** Hallo-cloudservice is vastgemaakt tooa specifieke cluster of gekoppelde tooan affiniteitsgroep en daarom vastgemaakt tooa specifieke cluster standaard is. Zodat nieuwe compute resource in die groep affiniteit aanvragen worden geprobeerd in Hallo dezelfde cluster waar Hallo bestaande bronnen worden gehost. Echter hello hetzelfde cluster mogelijk geen ondersteuning Hallo aangevraagd VM-grootte of hebt u onvoldoende beschikbare ruimte, wat resulteert in een toewijzingsfout. Dit geldt of Hallo nieuwe resources zijn gemaakt via een nieuwe cloudservice of een bestaande cloudservice.

**Oplossing 1:**

* Een nieuwe cloudservice maken en deze koppelen aan een regio of een regio op basis van een virtueel netwerk.
* Maak een nieuwe virtuele machine in Hallo nieuwe cloudservice.
  Als u een fout opgetreden krijgt bij een poging een nieuwe cloudservice toocreate, probeer op een later tijdstip of regio voor de cloudservice Hallo Hallo wijzigen.

> [!IMPORTANT]
> Als u een nieuwe virtuele machine in een bestaande cloudservice toocreate probeert maar kan niet en toocreate een nieuwe cloudservice voor uw nieuwe virtuele machine was, kunt u tooconsolidate alle virtuele machines in Hallo dezelfde cloudservice. toodo dus Hallo virtuele machines in de bestaande cloudservice Hallo verwijderen en opnieuw ze van hun schijven in de nieuwe cloudservice Hallo vastleggen. Het is echter belangrijk tooremember dat nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, dus u tooupdate moet deze voor alle Hallo afhankelijkheden die momenteel gebruikmaken van deze informatie voor een bestaande cloudservice Hallo.
> 
> 

**2 oorzaak:** Hallo-cloudservice is gekoppeld aan een virtueel netwerk dat is gekoppeld tooan affiniteitsgroep, dus is het specifieke cluster tooa vastgemaakt aan het ontwerp. Alle nieuwe compute resource aanvragen in die groep affiniteit worden daarom heeft geprobeerd in Hallo dezelfde cluster waar Hallo bestaande bronnen worden gehost. Echter hello hetzelfde cluster mogelijk geen ondersteuning Hallo aangevraagd VM-grootte of hebt u onvoldoende beschikbare ruimte, wat resulteert in een toewijzingsfout. Dit geldt of Hallo nieuwe resources zijn gemaakt via een nieuwe cloudservice of een bestaande cloudservice.

**Oplossing 2:**

* Maak een nieuw regionaal virtueel netwerk.
* Maken van nieuwe virtuele machine in een nieuw virtueel netwerk Hallo Hallo.
* [Verbinding maken met uw bestaande virtuele netwerk](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello nieuw virtueel netwerk. Zie voor meer informatie over [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). U kunt ook [migreren van uw virtuele netwerk op basis van affiniteit-groep tooa regionaal virtueel netwerk](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), en maak vervolgens Hallo van nieuwe virtuele machine.

## <a name="next-steps"></a>Volgende stappen
Als u problemen ondervindt wanneer u een gestopte virtuele machine van Windows te starten of het formaat van een bestaande Windows-machines in Azure, Zie [klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande Windows virtuele Machine in Azure](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md).

