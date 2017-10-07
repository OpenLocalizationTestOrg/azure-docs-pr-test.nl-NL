---
title: Linux-VM-implementatie-RM aaaTroubleshoot | Microsoft Docs
description: Resource Manager implementatieproblemen bij het maken van een nieuwe virtuele Linux-machine in Azure oplossen
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Resource Manager deployment problemen met het maken van een nieuwe virtuele Linux-machine in Azure oplossen
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Meest voorkomende problemen
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Zie voor andere VM-implementatieproblemen en vragen [problemen met implementatie Linux virtuele machine in Azure](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Registreert activiteit verzamelen
het oplossen van problemen toostart verzamelen Hallo activiteit registreert tooidentify Hallo fout die is gekoppeld aan Hallo probleem. Hallo bevatten volgende koppelingen gedetailleerde informatie over Hallo proces toofollow.

[Implementatiebewerkingen bekijken](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Weergeven van de activiteit logboeken toomanage Azure resources](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** als Hallo OS Linux gegeneraliseerd, en deze wordt geüpload en/of vastgelegd Hello gegeneraliseerd instellen, wordt niet eventuele fouten. Op dezelfde manier als Hallo OS Linux speciaal bedoeld is, en deze wordt geüpload en/of vastgelegd met gespecialiseerde Hallo instelling, en eventuele fouten niet.

**Fouten uploaden:**

**N<sup>1</sup>:** als Hallo OS Linux gegeneraliseerd en is geüpload als gespecialiseerde, ontvangt u een inrichting time-outfout omdat Hallo VM is vastgelopen bij Hallo fase inrichten.

**N<sup>2</sup>:** als Hallo OS is Linux gespecialiseerde en als gegeneraliseerd is geüpload, krijgt u een inrichting is mislukt omdat hello nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam hello, gebruikersnaam en wachtwoord.

**Oplossing:**

tooresolve beide deze fouten uploaden Hallo oorspronkelijke VHD, beschikbare on-premises, Hallo met dezelfde instelling als die voor Hallo OS (gegeneraliseerd/specifieke). tooupload zoals gegeneraliseerd, houd er rekening mee toorun-inrichting eerst ervan ongedaan maakt.

**Vastleggen fouten:**

**N<sup>3</sup>:** als Hallo OS Linux gegeneraliseerd en deze wordt vastgelegd als gespecialiseerde, ontvangt u een inrichting time-outfout omdat Hallo oorspronkelijke VM kan niet worden gebruikt als deze is gemarkeerd als gegeneraliseerd.

**N<sup>4</sup>:** als Hallo OS is Linux gespecialiseerde en deze is vastgelegd, zoals gegeneraliseerd, krijgt u een inrichting is mislukt omdat hello nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam hello, gebruikersnaam en wachtwoord. Bovendien Hallo oorspronkelijke VM kan niet worden gebruikt omdat deze is gemarkeerd als gespecialiseerde.

**Oplossing:**

tooresolve beide deze fouten Hallo huidige installatiekopie verwijderen vanuit de portal Hallo en [opnieuw vastleggen van Hallo huidige VHD's](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Hallo met dezelfde instelling als die voor Hallo OS (gegeneraliseerd/specifieke).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Probleem: Aangepaste / galerie / marketplace-installatiekopie; Toewijzingsfout
Deze fout zich voordoet in situaties wanneer Hallo nieuwe VM-aanvraag is vastgemaakt tooa cluster Hallo aangevraagde VM-grootte kan niet worden ondersteund of heeft geen beschikbare vrije ruimte tooaccommodate Hallo aanvraag.

**1 oorzaak:** Hallo cluster ondersteunt geen Hallo aangevraagde VM-grootte.

**Oplossing 1:**

* Probeer Hallo-aanvraag met een kleinere VM.
* Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:
  * Stop alle Hallo-VM's in de beschikbaarheidsset Hallo.
    Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.
  * Nadat alle virtuele machines stoppen hello, maakt u Hallo nieuwe virtuele machine in Hallo gewenst grootte.
  * Start eerst Hallo van nieuwe virtuele machine en vervolgens Selecteer Hallo gestopt VM's en klik op **Start**.

**2 oorzaak:** Hallo cluster heeft geen gratis resources.

**Oplossing 2:**

* Hallo aanvraag opnieuw proberen op een later tijdstip.
* Als hello nieuwe virtuele machine kan deel uitmaken van een andere beschikbaarheidsset instellen
  * Maak een nieuwe virtuele machine in een andere beschikbaarheidsset (in Hallo dezelfde regio).
  * Toevoegen van nieuwe VM-toohello Hallo hetzelfde virtuele netwerk.

## <a name="next-steps"></a>Volgende stappen
Als u problemen ondervindt wanneer u een gestopte Linux VM starten of het formaat van een bestaande Linux VM in Azure, Zie [problemen bij de implementatie met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure Resource Manager oplossen](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

