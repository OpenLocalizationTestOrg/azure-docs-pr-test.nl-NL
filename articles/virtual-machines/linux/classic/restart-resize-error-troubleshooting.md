---
title: aaaVM opnieuw te starten of het formaat problemen | Microsoft Docs
description: Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a>Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure
> [!div class="op_single_selector"]
> * [Klassiek](restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

Wanneer u een gestopte Azure virtuele Machine (VM) toostart probeert of vergroten of verkleinen van een bestaande virtuele machine in Azure, is Hallo veelvoorkomende fout die u tegenkomt een geheugentoewijzing is mislukt. Deze fout treedt op wanneer het Hallo-cluster of de regio ofwel geen beschikbare bronnen heeft of kan niet aangevraagd ondersteuning Hallo VM-grootte.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor de Resource Manager-versie Hallo [hier](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>De auditlogboeken verzamelen
het oplossen van problemen toostart verzamelen Hallo audit registreert tooidentify Hallo fout Hallo probleem gekoppeld.

Klik in hello Azure-portal, op **Bladeren** > **virtuele machines** > *uw virtuele Linux-machine*  >   **Instellingen** > **controlelogboeken**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Probleem: Fout bij het starten van een gestopte VM
U probeert een gestopte VM toostart maar een toewijzingsfout ophalen.

### <a name="cause"></a>Oorzaak
Hallo-aanvraag toostart Hallo gestopt VM heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de cloudservice hello toobe. Hallo-cluster heeft echter geen vrije ruimte beschikbaar toofulfill Hallo aanvraag.

### <a name="resolution"></a>Oplossing
* Een nieuwe cloudservice maken en deze koppelen aan ofwel een regio of een virtueel netwerk met op basis van regio, maar niet in een affiniteitsgroep.
* Verwijder Hallo VM gestopt.
* Maak opnieuw Hallo VM in de nieuwe cloudservice Hallo Hallo-schijven.
* Start Hallo VM opnieuw wordt gemaakt.

Als u een fout opgetreden krijgt bij een poging een nieuwe cloudservice toocreate, probeer op een later tijdstip of regio voor de cloudservice Hallo Hallo wijzigen.

> [!IMPORTANT]
> nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, zodat u toochange die informatie nodig voor alle Hallo afhankelijkheden die deze informatie voor een bestaande cloudservice Hallo gebruiken.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Probleem: Fout wanneer het formaat van een bestaande virtuele machine
U probeert een bestaande VM tooresize maar een toewijzingsfout ophalen.

### <a name="cause"></a>Oorzaak
Hallo-aanvraag tooresize Hallo VM toobe heeft geprobeerd op het oorspronkelijke cluster Hallo hosts Hallo cloudservice. Hallo-cluster biedt echter geen ondersteuning Hallo aangevraagde VM-grootte.

### <a name="resolution"></a>Oplossing
Verminderen Hallo aangevraagde VM-grootte en probeer het opnieuw Hallo vergroten of verkleinen van de aanvraag.

* Klik op **door alle Bladeren** > **virtuele machines (klassiek)** > *uw virtuele machine* > **instellingen** > **grootte**. Zie voor gedetailleerde stappen [Hallo virtuele machine vergroten of verkleinen](https://msdn.microsoft.com/library/dn168976.aspx).

Als dit niet mogelijk tooreduce Hallo VM-grootte is, volg deze stappen:

* Maak een nieuwe cloudservice, zodat het is niet gekoppeld tooan affiniteitsgroep en niet zijn gekoppeld aan een virtueel netwerk dat is gekoppeld tooan affiniteitsgroep.
* Maak een nieuwe, groter formaat VM in het.

U kunt uw virtuele machines consolideren Hallo moeten dezelfde cloudservice. Als uw bestaande cloudservice gekoppeld aan een regio op basis van een virtueel netwerk is, kunt u Hallo nieuwe cloud service toohello bestaand virtueel netwerk verbinden.

Als de bestaande cloudservice Hallo niet gekoppeld aan een regio op basis van een virtueel netwerk is, vervolgens u hebt toodelete hello, virtuele machines in een bestaande cloudservice hello, en ze opnieuw maken in een nieuwe cloudservice Hallo van hun schijven. Het is echter belangrijk tooremember dat nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, dus u tooupdate moet deze voor alle Hallo afhankelijkheden die momenteel gebruikmaken van deze informatie voor een bestaande cloudservice Hallo.

## <a name="next-steps"></a>Volgende stappen
Als u problemen ondervindt bij het maken van een nieuwe Linux VM in Azure, Zie [implementatieproblemen oplossen met het maken van een nieuwe virtuele Linux-machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

