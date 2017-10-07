---
title: aaaAbout schijven en VHD's voor Microsoft Azure VM's van Windows | Microsoft Docs
description: Meer informatie over de basisprincipes van Hallo van schijven en virtuele harde schijven voor Windows virtuele machines in Azure.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Over schijven en VHD's voor VM's van Windows Azure
Net als een andere computer gebruik virtuele machines in Azure schijven als een plaats toostore een besturingssysteem, toepassingen en gegevens. Alle virtuele machines in Azure hebt ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf. Hallo besturingssysteemschijf wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn virtuele harde schijven (VHD's) opgeslagen in Azure storage-account. Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen. 

In dit artikel wordt bespreken Hallo verschillende manieren worden gebruikt voor Hallo schijven, en vervolgens bespreken Hallo verschillende typen schijven kunt u maken en gebruiken. In dit artikel is ook beschikbaar voor [virtuele Linux-machines](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Schijven die worden gebruikt door virtuele machines

Eens kijken hoe Hallo schijven door Hallo VM's worden gebruikt.

### <a name="operating-system-disk"></a>Besturingssysteemschijf
Elke virtuele machine heeft een gekoppelde besturingssysteemschijf. Het is geregistreerd als een SATA harde schijf en gelabeld als Hallo tekstknooppunt standaard. Deze schijf heeft een maximale capaciteit van 2048 gigabyte (GB). 

### <a name="temporary-disk"></a>Tijdelijke schijf
Elke virtuele machine bevat een tijdelijke schijf. Hallo tijdelijke schijf opslag op korte termijn voor toepassingen en processen en gegevens van de beoogde tooonly opslaan zoals pagina of het swap-bestanden is. Gegevens op de tijdelijke schijf Hallo zijn mogelijk verloren gegaan tijdens een [onderhoud](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) of wanneer u [opnieuw implementeren van een virtuele machine](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Tijdens een standaard herstart Hallo VM moet Hallo-gegevens op de tijdelijke schijf Hallo handhaven.

Hallo tijdelijke schijf wordt aangeduid als Hallo station D: standaard en het wordt gebruikt voor het opslaan van pagefile.sys. tooremap deze schijf tooa andere stationsletter, Zie [wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](../virtual-machines/windows/change-drive-letter.md). Hallo-grootte van de tijdelijke schijf Hallo varieert, afhankelijk van de grootte van de Hallo van Hallo virtuele machine. Zie voor meer informatie [grootten voor Windows virtuele machines](../virtual-machines/windows/sizes.md).

Zie voor meer informatie over hoe Azure gebruikt voor de tijdelijke schijf Hallo [begrijpen Hallo tijdelijke station op Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Gegevensschijf
Een gegevensschijf is een VHD die is aangesloten tooa virtuele machine toostore toepassingsgegevens of andere gegevens die u nodig hebt tookeep. Gegevensschijven worden geregistreerd als SCSI-stations en zijn gelabeld met een letter die u kiest. Elke gegevensschijf heeft een maximale capaciteit van 4095 GB. Hallo grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunt u tooit en Hallo type opslag kunt u koppelen toohost Hallo schijven.

> [!NOTE]
> Zie voor meer informatie over de capaciteit van virtuele machines, [grootten voor Windows virtuele machines](../virtual-machines/windows/sizes.md).
> 

Azure maakt een besturingssysteemschijf wanneer u een virtuele machine van een installatiekopie maakt. Als u een afbeelding met gegevensschijven, maakt Azure ook Hallo gegevensschijven bij het maken van Hallo virtuele machine. Anders toevoegen u gegevensschijven nadat u Hallo virtuele machine hebt gemaakt.

U kunt gegevens schijven tooa virtuele machine door op elk gewenst moment toevoegen **koppelen** Hallo schijf toohello virtuele machine. U kunt een VHD die u hebt geüpload of gekopieerd tooyour storage-account of een die Azure voor u gemaakt. Koppelen van een gegevensschijf koppelt Hallo VHD-bestand aan Hallo VM door het plaatsen van een 'lease' op Hallo VHD zodat deze kan niet worden verwijderd uit de opslag terwijl er nog steeds gekoppeld.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Een laatste aanbeveling: gebruik TRIM met niet-beheerde standaardschijven 

Als u niet-beheerde standaard schijven (HDD) gebruikt, moet u TRIM inschakelen. TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt. Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen. 

U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren. Open een opdrachtprompt op de virtuele machine van Windows en typ:


```
fsutil behavior query DisableDeleteNotify
```

Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld. Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Opmerking: Ondersteuning begint met Windows Server 2012 / Windows 8 en hoger, Zie Zie [nieuwe API-apps toestaan toosend 'TRIM en ontkoppelen' hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Volgende stappen
* [Een schijf koppelen](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd extra opslagruimte voor uw virtuele machine.
* [Wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) zodat uw toepassing hello D: station voor gegevens gebruiken kunt.

