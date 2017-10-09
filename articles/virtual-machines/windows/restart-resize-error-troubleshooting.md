---
title: aaaVM opnieuw te starten of het formaat problemen in Azure | Microsoft Docs
description: Oplossen van problemen bij de implementatie met opnieuw te starten of het formaat van een bestaande Windows virtuele Machine in Azure Resource Manager
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a>Problemen oplossen implementatie met opnieuw te starten of het formaat van een bestaande Windows-machines in Azure
Wanneer u een gestopte Azure virtuele Machine (VM) toostart probeert of vergroten of verkleinen van een bestaande virtuele machine in Azure, is Hallo veelvoorkomende fout die u tegenkomt een geheugentoewijzing is mislukt. Deze fout treedt op wanneer het Hallo-cluster of de regio ofwel geen beschikbare bronnen heeft of kan niet aangevraagd ondersteuning Hallo VM-grootte.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Registreert activiteit verzamelen
het oplossen van problemen toostart verzamelen Hallo activiteit registreert tooidentify Hallo fout die is gekoppeld aan Hallo probleem. Hallo koppelingen volgen bevatten gedetailleerde informatie over het Hallo-proces:

[Implementatiebewerkingen bekijken](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Weergeven van de activiteit logboeken toomanage Azure resources](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Probleem: Fout bij het starten van een gestopte VM
U probeert een gestopte VM toostart maar een toewijzingsfout ophalen.

### <a name="cause"></a>Oorzaak
Hallo-aanvraag toostart Hallo gestopt VM heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de cloudservice hello toobe. Hallo-cluster heeft echter geen vrije ruimte beschikbaar toofulfill Hallo aanvraag.

### <a name="resolution"></a>Oplossing
* Stop alle Hallo VM's in Hallo beschikbaarheid ingesteld en elke VM start opnieuw op.
  
  1. Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.
  2. Nadat alle Hallo van virtuele machines stoppen, selecteert u elk Hallo gestopt VM's en klik op Start.
* Hallo herstart aanvraag opnieuw proberen op een later tijdstip.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Probleem: Fout wanneer het formaat van een bestaande virtuele machine
U probeert een bestaande VM tooresize maar een toewijzingsfout ophalen.

### <a name="cause"></a>Oorzaak
Hallo-aanvraag tooresize Hallo VM toobe heeft geprobeerd op het oorspronkelijke cluster Hallo hosts Hallo cloudservice. Hallo-cluster biedt echter geen ondersteuning Hallo aangevraagde VM-grootte.

### <a name="resolution"></a>Oplossing
* Probeer Hallo-aanvraag met een kleinere VM.
* Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:
  
  1. Stop alle Hallo-VM's in de beschikbaarheidsset Hallo.
     
     * Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.
  2. Nadat alle virtuele machines stoppen hello, Hallo gewenst VM tooa groter formaat.
  3. Selecteer Hallo gewijzigd VM en klikt u op **Start**, en vervolgens start Hallo VM's gestopt.

## <a name="next-steps"></a>Volgende stappen
Als u problemen ondervindt bij het maken van een nieuwe Windows VM in Azure, Zie [implementatieproblemen oplossen met een nieuwe virtuele machine voor Windows maken in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

