---
title: 'Controleer Hallo D: station van een virtuele machine een gegevensschijf | Microsoft Docs'
description: 'Hierin wordt beschreven hoe toochange stationsletters voor een Windows-VM zodat u Hallo D: station als een gegevensstation gebruiken kunt.'
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Hallo D: station gebruiken als een gegevensstation op een virtuele machine van Windows
Als uw toepassing toouse Hallo D-station toostore gegevens moet, volgt u deze instructies toouse een andere stationsletter voor de tijdelijke schijf Hallo. Gebruik nooit Hallo tijdelijke schijf toostore gegevens dat u nodig hebt tookeep.

Als u de grootte of **stoppen (Deallocate)** een virtuele machine, kan dit de plaatsing van Hallo virtuele machine tooa nieuwe hypervisor activeren. Een gebeurtenis gepland of ongepland onderhoud activeren mogelijk ook deze plaatsing. In dit scenario worden de tijdelijke schijf Hallo opnieuw toegewezen toohello eerste beschikbare letter. Als u een toepassing die specifiek Hallo D: station moet hebt, moet u toofollow deze stappen tootemporarily verplaatsen Hallo pagefile.sys, een nieuwe gegevensschijf koppelen en wijs deze Hallo letter D en verplaatsen Hallo pagefile.sys back-toohello tijdelijke schijf. Hierna kunt Azure niet terug te nemen Hallo D: als Hallo VM tooa andere hypervisor verplaatst.

Zie voor meer informatie over hoe Azure gebruikt voor de tijdelijke schijf Hallo [begrijpen Hallo tijdelijke station op Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Hallo gegevensschijf koppelen
Eerst moet u tooattach Hallo gegevens schijf toohello virtuele machine. toodo deze Hallo portal gebruikt, Zie [hoe tooattach een beheerde gegevens in Azure-portal Hallo schijf](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Tijdelijk verplaatst pagefile.sys tooC station
1. Verbinding maken met toohello virtuele machine. 
2. Klik met de rechtermuisknop Hallo **Start** menu en selecteer **System**.
3. Selecteer in het menu Hallo links, **Geavanceerde systeeminstellingen**.
4. In Hallo **prestaties** sectie **instellingen**.
5. Selecteer Hallo **Geavanceerd** tabblad.
6. In Hallo **virtueel geheugen** sectie **wijziging**.
7. Selecteer Hallo **C** station en klik vervolgens op **systeem beheerde grootte** en klik vervolgens op **ingesteld**.
8. Selecteer Hallo **D** station en klik vervolgens op **geen wisselbestand** en klik vervolgens op **ingesteld**.
9. Klik op toepassen. U ontvangt een waarschuwing dat die Hallo-computer moet opnieuw worden opgestart voor Hallo wijzigingen tootake invloed toobe.
10. Hallo virtuele machine opnieuw opstarten.

## <a name="change-hello-drive-letters"></a>Hallo stationsletters wijzigen
1. Eenmaal Hallo VM opnieuw wordt opgestart, meld u opnieuw aan toohello VM.
2. Klik op Hallo **Start** menu en typ **diskmgmt.msc** en druk op Enter. Schijfbeheer wordt gestart.
3. Met de rechtermuisknop op **D**, Hallo station voor tijdelijke opslag en selecteert u **wijziging stationsletter en paden**.
4. Selecteer onder de stationsletter, een nieuw station, zoals **T** en klik vervolgens op **OK**. 
5. Met de rechtermuisknop op de gegevensschijf Hallo en selecteer **wijziging stationsletter en paden**.
6. Selecteer onder de stationsletter, station **D** en klik vervolgens op **OK**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Pagefile.sys back toohello tijdelijke opslagstation verplaatsen
1. Klik met de rechtermuisknop Hallo **Start** menu en selecteer **systeem**
2. Selecteer in het menu Hallo links, **Geavanceerde systeeminstellingen**.
3. In Hallo **prestaties** sectie **instellingen**.
4. Selecteer Hallo **Geavanceerd** tabblad.
5. In Hallo **virtueel geheugen** sectie **wijziging**.
6. Selecteer Hallo OS station **C** en klik op **geen wisselbestand** en klik vervolgens op **ingesteld**.
7. Selecteer Hallo tijdelijke opslagstation **T** en klik vervolgens op **systeem beheerde grootte** en klik vervolgens op **ingesteld**.
8. Klik op **Toepassen**. U ontvangt een waarschuwing dat die Hallo-computer moet opnieuw worden opgestart voor Hallo wijzigingen tootake invloed toobe.
9. Hallo virtuele machine opnieuw opstarten.

## <a name="next-steps"></a>Volgende stappen
* U kunt verhogen Hallo opslag beschikbaar tooyour virtuele machine door [koppelen van een extra gegevensschijf](attach-managed-disk-portal.md).

