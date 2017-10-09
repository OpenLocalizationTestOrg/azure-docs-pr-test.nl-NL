---
title: een data schijf tooa Linux VM aaaAttach | Microsoft Docs
description: Hoe Hallo tooattach nieuwe of bestaande gegevens schijf tooa Linux VM in hello Azure portal met behulp van Resource Manager-implementatiemodel.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Hoe tooattach data schijf tooa Linux VM in hello Azure-portal
Dit artikel laat zien hoe tooattach zowel nieuwe als bestaande schijven tooa virtuele Linux-machine via hello Azure-portal. U kunt ook [koppelen van een data schijf tooa virtuele Windows-machine in Azure-portal Hallo](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). U kunt toouse beide schijven Azure beheerd of onbeheerd schijven. Beheerde schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze. Niet-beheerde schijven is een opslagaccount vereist en beschikt over sommige [quota en limieten die van toepassing](../../azure-subscription-service-limits.md#storage-limits). Zie [Overzicht van Azure Managed Disks](../windows/managed-disks-overview.md) voor meer informatie over Azure Managed Disks.

Voordat u schijven tooyour VM koppelt, controleert u de volgende tips:

* Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Premium-opslag toouse, moet u een virtuele machine DS-serie- of GS-serie. U kunt zowel Premium en Standard schijven met deze virtuele machines. Premium-opslag is beschikbaar in bepaalde regio's. Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Schijven gekoppelde toovirtual machines zijn daadwerkelijk .vhd bestanden die zijn opgeslagen in Azure. Zie voor meer informatie [over schijven en virtuele harde schijven voor virtuele machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Hallo virtuele machine gevonden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **virtuele Machines**.
3. Selecteer Hallo virtuele machine uit de lijst Hallo.
4. toohello virtuele machines blade in **Essentials**, klikt u op **schijven**.
   
    ![Instellingen voor de schijf openen](./media/attach-disk-portal/find-disk-settings.png)

Instructies voor het koppelen van een volgende om door te gaan een [beheerde schijven](#use-azure-managed-disks) of [onbeheerde schijf](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Azure-beheerde schijven gebruiken

### <a name="attach-a-new-disk"></a>Een nieuwe schijf koppelen

1. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. Klik op Hallo vervolgkeuzelijst voor **naam** en selecteer **maken-schijf**:

    ![Maken van Azure beheerde schijven](./media/attach-disk-portal/create-new-md.png)

3. Voer een naam voor de beheerde schijf. Controleer Hallo standaardinstellingen, indien nodig bijwerken en klik vervolgens op **maken**.
   
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/create-new-md-settings.png)

4. Klik op **opslaan** toocreate Hallo beheerd schijf en update Hallo VM-configuratie:

   ![Nieuwe Azure beheerd schijf opslaan](./media/attach-disk-portal/confirm-create-new-md.png)

5. Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**. Als beheerde schijven een bron op het hoogste niveau zijn, wordt in de hoofdmap Hallo van resourcegroep Hallo Hallo schijf weergegeven:

   ![Azure-schijf beheerd in de resourcegroep](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Een bestaande schijf koppelen
1. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. Klik op Hallo vervolgkeuzelijst voor **naam** tooview een lijst met bestaande schijven toegankelijk tooyour Azure-abonnement beheerd. Selecteer Hallo beheerd schijf tooattach:

   ![Bestaande Azure beheerd schijf koppelen](./media/attach-disk-portal/select-existing-md.png)

3. Klik op **opslaan** tooattach Hallo bestaande schijf en update Hallo VM-configuratie worden beheerd:
   
   ![Beheerde Azure-schijf updates opslaan](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Nadat Azure wordt hello schijf toohello virtuele machine, wordt deze weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.

## <a name="use-unmanaged-disks"></a>Niet-beheerde schijven gebruiken

### <a name="attach-a-new-disk"></a>Een nieuwe schijf koppelen

1. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. Controleer Hallo standaardinstellingen, indien nodig bijwerken en klik vervolgens op **OK**.
   
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-new.png)
3. Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.

### <a name="attach-an-existing-disk"></a>Een bestaande schijf koppelen
1. Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.
2. Onder **bestaande schijf koppelen**, klikt u op **VHD-bestand**.
   
   ![Bestaande schijf koppelen](./media/attach-disk-portal/attach-existing.png)
3. Onder **opslagaccounts**, Hallo-account en -container met Hallo .vhd-bestand selecteren.
   
   ![Locatie van de VHD vinden](./media/attach-disk-portal/find-storage-container.png)
4. Selecteer Hallo .vhd-bestand.
5. Onder **bestaande schijf koppelen**, Hallo bestand dat u zojuist hebt geselecteerd wordt vermeld onder **VHD-bestand**. Klik op **OK**.
6. Nadat Azure wordt hello schijf toohello virtuele machine, wordt deze weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.


## <a name="next-steps"></a>Volgende stappen
Nadat het Hallo-schijf wordt toegevoegd, moet u tooprepare voor gebruik. Zie voor meer informatie [hoe: initialiseren van een nieuwe gegevensschijf in Linux](add-disk.md).
