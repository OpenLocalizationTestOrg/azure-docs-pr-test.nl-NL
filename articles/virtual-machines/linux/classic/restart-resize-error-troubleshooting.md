---
title: Virtuele machine opnieuw te starten of het formaat problemen | Microsoft Docs
description: Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: troubleshooting
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 7f5718a7e1ab2b14902fa61ffb3053910e584ac6
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/21/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a>Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure
> [!div class="op_single_selector"]
> * [Klassiek](restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

Wanneer u een gestopte Azure virtuele Machine (VM) start of het formaat van een bestaande virtuele machine in Azure, is de algemene fout die u tegenkomt een geheugentoewijzing is mislukt. Deze fout treedt op wanneer het cluster of de regio geen bronnen beschikbaar heeft of het aangevraagde VM-grootte kan niet worden ondersteund.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel. U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken. Zie voor de versie van het Resource Manager, [hier](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>De auditlogboeken verzamelen
U start het oplossen van problemen door de controlelogboeken om te identificeren van de fout die is gekoppeld aan het probleem te verzamelen.

Klik in de Azure-portal op **Bladeren** > **virtuele machines** > *uw virtuele Linux-machine* > **instellingen** > **controlelogboeken**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Probleem: Fout bij het starten van een gestopte VM
U probeert te starten van een gestopte VM maar een toewijzingsfout ophalen.

### <a name="cause"></a>Oorzaak
De aanvraag voor het starten van de gestopte virtuele machine moet worden uitgevoerd op het oorspronkelijke cluster die als host fungeert voor de cloudservice. Het cluster heeft echter geen vrije schijfruimte om de aanvraag te voldoen.

### <a name="resolution"></a>Oplossing
* Een nieuwe cloudservice maken en deze koppelen aan ofwel een regio of een virtueel netwerk met op basis van regio, maar niet in een affiniteitsgroep.
* Verwijder de gestopte virtuele machine.
* Maak de virtuele machine in de nieuwe cloudservice opnieuw met behulp van de schijven.
* Start de VM opnieuw worden gemaakt.

Als u een fout opgetreden krijgt bij het maken van een nieuwe cloudservice, probeer op een later tijdstip of de regio voor de cloudservice wijzigen.

> [!IMPORTANT]
> De nieuwe cloudservice heeft een nieuwe naam en het VIP, dus moet u die gegevens voor de afhankelijkheden die gebruikmaken van die gegevens voor de bestaande cloudservice wijzigen.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Probleem: Fout wanneer het formaat van een bestaande virtuele machine
U probeert te vergroten of verkleinen van een bestaande virtuele machine, maar een toewijzingsfout ophalen.

### <a name="cause"></a>Oorzaak
De aanvraag voor het formaat van de virtuele machine moet worden uitgevoerd op het oorspronkelijke cluster die als host fungeert voor de cloudservice. Het cluster biedt echter geen ondersteuning voor de aangevraagde VM-grootte.

### <a name="resolution"></a>Oplossing
De aangevraagde VM-grootte te beperken en probeer de aanvraag formaat.

* Klik op **door alle Bladeren** > **virtuele machines (klassiek)** > *uw virtuele machine* > **instellingen** > **grootte**. Zie voor gedetailleerde stappen [vergroten of verkleinen van de virtuele machine](https://msdn.microsoft.com/library/dn168976.aspx).

Als het niet mogelijk om de VM-grootte te beperken, volg deze stappen:

* Maak een nieuwe cloudservice, zodat deze is niet gekoppeld aan een affiniteitsgroep en niet zijn gekoppeld aan een virtueel netwerk dat is gekoppeld aan een affiniteitsgroep.
* Maak een nieuwe, groter formaat VM in het.

U kunt alle virtuele machines in dezelfde cloudservice consolideren. Als uw bestaande cloudservice gekoppeld aan een regio op basis van een virtueel netwerk is, kunt u de nieuwe cloudservice met de bestaande virtuele netwerk.

Als de bestaande cloudservice niet gekoppeld aan een virtueel netwerk met op basis van regio is, hebt u voor het verwijderen van de virtuele machines in de bestaande cloudservice en ze opnieuw maken in de nieuwe service in de cloud van de schijven. Het is echter belangrijk dat u weet dat de nieuwe cloudservice heeft een nieuwe naam en het VIP, dus moet u deze voor de afhankelijkheden die momenteel gebruikmaken van deze informatie voor de bestaande cloudservice bijwerken.

## <a name="next-steps"></a>Volgende stappen
Als u problemen ondervindt bij het maken van een nieuwe Linux VM in Azure, Zie [implementatieproblemen oplossen met het maken van een nieuwe virtuele Linux-machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

