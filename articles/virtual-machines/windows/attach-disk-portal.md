---
title: Een niet-beheerde gegevensschijf koppelen aan een virtuele machine van Windows - Azure | Microsoft Docs
description: Klik hier voor meer informatie over het nieuwe of bestaande niet-beheerde gegevensschijf koppelen aan een virtuele machine van Windows in de Azure portal met het implementatiemodel van Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: c0886302c82641f8cc1a00d3972870d58ba8afb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-an-unmanaged-data-disk-to-a-windows-vm-in-the-azure-portal"></a>Hoe u een niet-beheerde gegevensschijf koppelen aan een virtuele machine van Windows in de Azure portal

In dit artikel leest u hoe nieuwe en bestaande niet-beheerde schijven koppelen aan Windows virtuele machines via de Azure-portal. U kunt ook [een gegevensschijf met behulp van PowerShell koppelen](./attach-disk-ps.md). Voordat u dit doet, controleert u de volgende tips:

* De omvang van de virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](sizes.md).
* Premium-opslag gebruiken, moet u een virtuele machine DS-serie- of GS-serie. Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts. Premium-opslag is beschikbaar in bepaalde regio's. Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Voor een nieuwe schijf hoeft u niet eerst maken omdat Azure gemaakt wanneer u dit aansluit.


U kunt ook [een gegevensschijf met behulp van Powershell koppelen](attach-disk-ps.md).


## <a name="find-the-virtual-machine"></a>De virtuele machine gevonden
1. Meld u aan bij [Azure Portal](https://portal.azure.com/).
2. Klik in het menu aan de linkerkant op **virtuele Machines**.
3. Selecteer de virtuele machine in de lijst.
4. Klik op de blade virtuele machines **schijven**.
   
Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Optie 1: Koppelen en een nieuwe schijf initialiseren
1. Op de **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. In de **Attach-beheerde schijven** blade, typ een naam voor de schijf in **naam** en selecteer vervolgens **nieuwe (lege schijf)** in **gegevensbrontype**.
3. Onder **opslagcontainer**, klikt u op de **Bladeren** knop en blader naar het opslagaccount en container waarin u wilt dat de nieuwe VHD worden opgeslagen en klik vervolgens op **Selecteer**. 
  
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Wanneer u klaar bent met de instellingen voor de gegevensschijf, klikt u op **OK**.
4. Terug in de **schijven** blade, klikt u op **opslaan** de schijf toevoegen aan de VM-configuratie.


### <a name="initialize-a-new-data-disk"></a>Initialiseer de gegevensschijf van een nieuwe

1. Verbinding maken met de virtuele machine. Zie voor instructies [verbinding maken met en meld u aan een virtuele machine van Azure waarop Windows wordt uitgevoerd bij](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Klik op de **Start** menu binnen de virtuele machine en het type **diskmgmt.msc** en treffers **Enter**. Hiermee start u de module Schijfbeheer.
2. Schijfbeheer herkent dat u een nieuwe, niet-geïnitialiseerde schijf hebt en de schijf initialiseren-venster.
3. Zorg ervoor dat de nieuwe schijf is geselecteerd en klik op **OK** voor het initialiseren.
4. De nieuwe schijf wordt nu weergegeven als **niet-toegewezen**. Klik met de rechtermuisknop op de schijf en selecteer **Nieuw eenvoudig volume**. De **Wizard Nieuw eenvoudig Volume** wordt gestart.
5. Doorloop de wizard, alle standaardinstellingen, houden wanneer u klaar bent Selecteer **voltooien**.
6. Sluit de module Schijfbeheer.
7. Krijgt u een pop-upvenster die u de nieuwe schijf formatteren moet voordat u deze kunt gebruiken. Klik op **schijf formatteren**.
8. In de **nieuwe schijf formatteren** dialoogvenster, Controleer de instellingen en klik vervolgens op **Start**.
9. Krijg een waarschuwing dat de schijven formatteert, worden alle gegevens, klikt u **OK**.
10. Wanneer de indeling voltooid is, klikt u op **OK**.


## <a name="option-2-attach-an-existing-disk"></a>Optie 2: Een bestaande schijf koppelen
1. Op de **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. Op de **onbeheerde schijf koppelen** blade in **gegevensbrontype** Selecteer **bestaande blob**.

    ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Klik op **Bladeren** om te navigeren naar het opslagaccount en container waarin de bestaande VHD zich bevindt. Klik op en de VHD en klik vervolgens op **Selecteer**.
4. Klik op **OK** in de **onbeheerde schijf koppelen** blade.
5. In de **schijven** blade, klikt u op **opslaan** de schijf toevoegen aan de configuratie voor de virtuele machine.
   


## <a name="use-trim-with-standard-storage"></a>Gebruik TRIM met standard-opslag

Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen. TRIM worden niet-gebruikte blokken op de schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt. Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen. 

U kunt deze opdracht om te controleren van de beperkende instelling uitvoeren. Open een opdrachtprompt op de virtuele machine van Windows en typ:

```
fsutil behavior query DisableDeleteNotify
```

Als de opdracht 0 retourneert, wordt ' trim ' correct ingeschakeld. Als deze 1 retourneert, voert u de volgende opdracht voor het vrijmaken van opslagruimte inschakelen:
```
fsutil behavior set DisableDeleteNotify 0
```

Na het verwijderen van gegevens van de schijf, kunt u ervoor zorgen dat de beperkende leegmaken goed door het uitvoeren van bewerkingen met ' trim ' defragmentatie:

```
defrag.exe <volume:> -l
```

U kunt er ook voor zorgen dat het hele volume wordt verkleind door het formatteren van het volume.


## <a name="next-steps"></a>Volgende stappen
Als u een toepassing gebruikt de D: station voor het opslaan van gegevens, kunt u [wijzigen van de stationsletter van de tijdelijke schijf Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

