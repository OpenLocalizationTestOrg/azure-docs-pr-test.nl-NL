---
title: een niet-beheerde gegevens schijf tooa Windows VM - Azure aaaAttach | Microsoft Docs
description: Hoe tooattach nieuwe of bestaande niet-beheerde gegevens schijf tooa virtuele Windows-machine in Azure portal met behulp van Hallo Hallo Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Hoe gegevens in een niet-beheerde tooattach schijf tooa Windows VM in hello Azure-portal

Dit artikel ziet u hoe tooattach zowel nieuwe als bestaande zonder begeleiding schijven tooWindows virtuele machines via hello Azure-portal. U kunt ook [een gegevensschijf met behulp van PowerShell koppelen](./attach-disk-ps.md). Voordat u dit doet, controleert u de volgende tips:

* Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](sizes.md).
* Premium-opslag toouse, moet u een virtuele machine DS-serie- of GS-serie. Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts. Premium-opslag is beschikbaar in bepaalde regio's. Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Voor een nieuwe schijf, hoeft u niet toocreate het eerste omdat Azure gemaakt wanneer u dit aansluit.


U kunt ook [een gegevensschijf met behulp van Powershell koppelen](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Hallo virtuele machine gevonden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik in het menu aan de linkerkant Hallo Hallo op **virtuele Machines**.
3. Selecteer Hallo virtuele machine uit de lijst Hallo.
4. Klik op Hallo virtuele machines blade **schijven**.
   
Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Optie 1: Koppelen en een nieuwe schijf initialiseren
1. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. In Hallo **Attach-beheerde schijven** blade een naam voor de schijf Hallo in **naam** en selecteer vervolgens **nieuwe (lege schijf)** in **gegevensbrontype**.
3. Onder **opslagcontainer**, klikt u op Hallo **Bladeren** knop en blader toohello opslagaccount en container waar u Hallo nieuwe VHD toobe opgeslagen, zoals en klik vervolgens op **Selecteer**. 
  
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Wanneer u klaar bent met instellingen voor de gegevensschijf Hallo Hallo, klikt u op **OK**.
4. Terug in Hallo **schijven** blade, klikt u op **opslaan** tooadd Hallo schijf toohello VM-configuratie.


### <a name="initialize-a-new-data-disk"></a>Initialiseer de gegevensschijf van een nieuwe

1. Verbinding maken met toohello virtuele machine. Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Klik op Hallo **Start** menu binnen Hallo VM en het type **diskmgmt.msc** en treffers **Enter**. Hiermee start u Hallo schijf-beheermodule.
2. Schijfbeheer herkent dat u een nieuwe, niet-geïnitialiseerde schijf hebt en Hallo schijf initialiseren-venster.
3. Zorg ervoor dat de nieuwe schijf Hallo is geselecteerd en klik op **OK** tooinitialize deze.
4. Hallo nieuwe schijf wordt nu weergegeven als **niet-toegewezen**. Klik met de rechtermuisknop op Hallo schijf en selecteer **Nieuw eenvoudig volume**. Hallo **Wizard Nieuw eenvoudig Volume** wordt gestart.
5. Ga in de wizard hello, alle standaardinstellingen hello, houden wanneer u klaar bent Selecteer **voltooien**.
6. Sluit de module Schijfbeheer.
7. U krijgt een pop-upvenster dat u moet tooformat Hallo nieuwe schijf voordat u deze kunt gebruiken. Klik op **schijf formatteren**.
8. In Hallo **nieuwe schijf formatteren** dialoogvenster, selectievakje Hallo instellingen en klik vervolgens op **Start**.
9. Krijg een waarschuwing dat Hallo schijven formatteert, worden alle gegevens hello, klikt u **OK**.
10. Wanneer het Hallo-indeling is voltooid, klikt u op **OK**.


## <a name="option-2-attach-an-existing-disk"></a>Optie 2: Een bestaande schijf koppelen
1. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. Op Hallo **onbeheerde schijf koppelen** blade in **gegevensbrontype** Selecteer **bestaande blob**.

    ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Klik op **Bladeren** toonavigate toohello opslagaccount en container waar hello bestaande VHD zich bevindt. Klik op en Hallo VHD en klik vervolgens op **Selecteer**.
4. Klik op **OK** in Hallo **onbeheerde schijf koppelen** blade.
5. In Hallo **schijven** blade, klikt u op **opslaan** tooadd hello toohello schijfconfiguratie voor Hallo VM.
   


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

