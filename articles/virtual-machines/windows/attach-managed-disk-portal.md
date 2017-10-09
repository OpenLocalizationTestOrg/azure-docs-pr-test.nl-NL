---
title: een beheerde gegevens schijf tooa Windows VM - Azure aaaAttach | Microsoft Docs
description: De wijze waarop tooattach nieuwe gegevens schijf tooa beheerd Hallo Windows virtuele machine in Azure portal met behulp van Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Hoe een beheerde gegevens tooattach schijf tooa Windows VM in hello Azure-portal

Dit artikel laat zien hoe een nieuwe beheerde gegevens tooattach schijf tooWindows virtuele machines via hello Azure-portal. Voordat u dit doet, controleert u de volgende tips:

* Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](sizes.md).
* Voor een nieuwe schijf, hoeft u niet toocreate het eerste omdat Azure gemaakt wanneer u dit aansluit.

U kunt ook [een gegevensschijf met behulp van Powershell koppelen](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Een gegevensschijf toevoegen
1. Klik in het menu aan de linkerkant Hallo Hallo op **virtuele Machines**.
2. Selecteer Hallo virtuele machine uit de lijst Hallo.
3. Klik op Hallo virtuele machineblade **schijven**.
   4. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
5. Selecteer in de vervolgkeuzelijst voor de nieuwe schijf Hallo Hallo, **maken leeg**.
6. In Hallo **-beheerde schijven maken** blade, typ een naam voor Hallo schijf en pas Hallo van andere instellingen zo nodig. Wanneer u klaar bent, klikt u op **maken**.
7. In Hallo **schijven** blade, klik op Opslaan toosave Hallo nieuwe schijf-configuratie voor Hallo VM.
6. Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.


## <a name="initialize-a-new-data-disk"></a>Initialiseer de gegevensschijf van een nieuwe

1. Verbinding maken met toohello VM.
1. Klik op Hallo startmenu binnen Hallo VM en typ **diskmgmt.msc** en treffers **Enter**. Hiermee start u Hallo schijf-beheermodule.
2. Schijfbeheer constateert dat er een nieuwe, niet-geïnitialiseerde schijf en Hallo schijf initialiseren-venster.
3. Zorg ervoor dat de nieuwe schijf Hallo is geselecteerd en klik op **OK** tooinitialize deze.
4. Hallo nieuwe schijf wordt nu weergegeven als **niet-toegewezen**. Klik met de rechtermuisknop op Hallo schijf en selecteer **Nieuw eenvoudig volume**. Hallo **Wizard Nieuw eenvoudig Volume** wordt gestart.
5. Ga in de wizard hello, alle standaardinstellingen hello, houden wanneer u klaar bent Selecteer **voltooien**.
6. Sluit de module Schijfbeheer.
7. U ontvangt een pop-upvenster die u moet tooformat Hallo nieuwe schijf voordat u deze kunt gebruiken. Klik op **schijf formatteren**.
8. In Hallo **nieuwe schijf formatteren** dialoogvenster, selectievakje Hallo instellingen en klik vervolgens op **Start**.
9. U ontvangt een waarschuwing dat Hallo schijven formatteren worden gewist door alle Hallo gegevens, klikt u op **OK**.
10. Wanneer het Hallo-indeling is voltooid, klikt u op **OK**.

## <a name="use-trim-with-standard-storage"></a>Gebruik TRIM met standard-opslag

Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen. TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt. Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen. 

U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren. Open een opdrachtprompt op de virtuele machine van Windows en typ:

```
fsutil behavior query DisableDeleteNotify
```

Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld. Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:
```
fsutil behavior set DisableDeleteNotify 0
```

Na het verwijderen van gegevens van de schijf, kunt u ervoor zorgen dat Hallo TRIM operations leegmaken goed door het uitvoeren van defragmentatiefase met ' trim ':

```
defrag.exe <volume:> -l
```

U kunt er ook voor zorgen Hallo hele volume wordt door het Hallo-volume formatteren bijgesneden.

## <a name="next-steps"></a>Volgende stappen
Als u een toepassing toouse Hallo D: station toostore gegevens nodig zijn, kunt u [stationsletter op Hallo van Hallo Windows tijdelijke schijf wijzigen](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
