---
title: een schijf tooa aaaAttach klassieke virtuele machine in Azure | Microsoft Docs
description: Een data schijf tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel Hallo koppelen en het initialiseren.
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Een data schijf tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel Hallo koppelen
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

Dit artikel laat zien hoe tooattach nieuwe en bestaande schijven gemaakt met de Hallo Classic deployment model tooa Windows virtuele machine met behulp van hello Azure-portal.

U kunt ook [koppelen van een data schijf tooa Linux VM in hello Azure-portal](../../linux/attach-disk-portal.md).

Voordat u een schijf koppelen, controleert u de volgende tips:

* Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Premium-opslag toouse, moet u een virtuele machine DS-serie- of GS-serie. Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts. Premium-opslag is beschikbaar in bepaalde regio's. Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Voor een nieuwe schijf, hoeft u niet toocreate het eerste omdat Azure gemaakt wanneer u dit aansluit.

U kunt ook [een gegevensschijf met behulp van Powershell koppelen](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Hallo virtuele machine gevonden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer Hallo virtuele machine van Hallo resource in de lijst op Hallo-dashboard.
3. In het linkerdeelvenster onder Hallo **instellingen**, klikt u op **schijven**.

    ![Instellingen voor de schijf openen](./media/attach-disk/virtualmachinedisks.png)

Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Optie 1: Koppelen en een nieuwe schijf initialiseren

1. Op Hallo **schijven** blade, klikt u op **Attach nieuwe**.
2. Controleer Hallo standaardinstellingen, indien nodig bijwerken en klik vervolgens op **OK**.

   ![Controleer de Schijfinstellingen](./media/attach-disk/attach-new.png)

3. Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.

### <a name="initialize-a-new-data-disk"></a>Initialiseer de gegevensschijf van een nieuwe

1. Verbinding maken met toohello virtuele machine. Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Nadat u zich aanmeldt toohello virtuele machine, opent u **Serverbeheer**. Selecteer in het linkerdeelvenster Hallo **File and Storage Services**.

    ![Open Serverbeheer](../media/attach-disk-portal/fileandstorageservices.png)

3. Selecteer **schijven**.
4. Hallo **schijven** sectie vindt u Hallo-schijven. De meeste gevallen heeft een virtuele machine schijf 0, schijf van 1 en 2 schijf. Schijf 0 besturingssysteemschijf hello, schijf 1 Hallo tijdelijke schijf en schijf 2 is Hallo gegevensschijf gekoppeld zojuist toohello virtuele machine. Hallo gegevens schijf lijsten Hallo partitie als **onbekende**.

 Met de rechtermuisknop op Hallo schijf en selecteer **initialiseren**.

5. U wordt gewaarschuwd dat alle gegevens worden gewist wanneer het Hallo-schijf is geïnitialiseerd. Klik op **Ja** tooacknowledge Hallo waarschuwings- en initialisatie Hallo schijf. Hierna kunt Hallo partitie wordt weergegeven als **GPT**. Opnieuw met de rechtermuisknop op Hallo schijf en selecteer **NieuwVolume**.

6. Met de standaardwaarden Hallo Hallo-wizard te voltooien. Als het Hallo-wizard is voltooid, Hallo **Volumes** sectie vindt u Hallo nieuw volume. Hallo-schijf is nu online en gereed toostore gegevens.

    ![Volume is geïnitialiseerd](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Optie 2: Een bestaande schijf koppelen
1. Op Hallo **schijven** blade, klikt u op **Attach bestaande**.
2. Onder **bestaande schijf koppelen**, klikt u op **locatie**.

   ![Bestaande schijf koppelen](./media/attach-disk/attachexistingdisksettings.png)
3. Onder **opslagaccounts**, Hallo-account en -container met Hallo .vhd-bestand selecteren.

   ![Locatie van de VHD vinden](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Selecteer Hallo .vhd-bestand.
5. Onder **bestaande schijf koppelen**, Hallo bestand dat u zojuist hebt geselecteerd wordt vermeld onder **VHD-bestand**. Klik op **OK**.
6. Nadat Azure wordt hello schijf toohello virtuele machine, wordt deze weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.

## <a name="use-trim-with-standard-storage"></a>Gebruik TRIM met standard-opslag

Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen. TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt. Met ' trim ', kun kosten, met inbegrip van niet-gebruikte blokken die het gevolg zijn van grote bestanden worden verwijderd.

U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren. Open een opdrachtprompt op de virtuele machine van Windows en typ:

```
fsutil behavior query DisableDeleteNotify
```

Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld. Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Volgende stappen
Als uw toepassing toouse Hallo D: station toostore gegevens nodig zijn, kunt u [stationsletter op Hallo van Hallo Windows tijdelijke schijf wijzigen](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Aanvullende bronnen
[Over schijven en virtuele harde schijven voor virtuele machines](../../virtual-machines-linux-about-disks-vhds.md)
