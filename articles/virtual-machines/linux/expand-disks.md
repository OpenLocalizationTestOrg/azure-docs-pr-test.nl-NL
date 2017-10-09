---
title: aaaExpand virtuele harde schijven op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe tooexpand virtuele harde schijven op een Linux-VM met Azure CLI 2.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Hoe tooexpand virtuele harde schijven op een Linux-VM met Azure CLI Hallo
Hallo standaardgrootte virtuele harde schijf voor Hallo besturingssysteem (OS) is doorgaans 30 GB op een Linux virtuele machine (VM) in Azure. U kunt [gegevensschijven toevoegen](add-disk.md) tooprovide voor extra opslagruimte, maar u kunt ook desgewenst voor tooexpand een bestaande gegevensschijf. Dit artikel wordt uitgelegd hoe tooexpand schijven voor een Linux-VM met hello Azure CLI 2.0 beheerd. U kunt ook de besturingssysteemschijf Hallo zonder begeleiding Hello uitvouwen [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Zorg er altijd dat u maakt u een back-up van uw gegevens voordat u de schijf uitvoert de grootte van bewerkingen. Zie voor meer informatie [Back-up van Linux virtuele machines in Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Schijf uitbreiden
Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In dit artikel is een bestaande virtuele machine in Azure met ten minste één schijf met gegevens die zijn gekoppeld en voorbereid vereist. Als u nog geen een virtuele machine die u kunt gebruiken, raadpleegt u [maken en voorbereiden van een virtuele machine met gegevensschijven](tutorial-manage-disks.md#create-and-attach-disks).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup* en *myVM*.

1. Bewerkingen op virtuele harde schijven kunnen niet worden uitgevoerd met Hallo VM uitgevoerd. Toewijzing van uw virtuele machine met [az vm ongedaan](/cli/azure/vm#deallocate). Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`Geeft de rekenresources Hallo niet vrij. toorelease rekenresources, gebruikt u `az vm deallocate`. Hallo VM moet ongedaan tooexpand Hallo virtuele hardeschijf.

2. Een lijst met beheerde schijven weergeven in een resourcegroep met [az Schijflijst](/cli/azure/disk#list). Hallo volgende voorbeeld wordt een lijst met beheerde schijven in Hallo resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Vouw de benodigde schijfruimte Hallo met [az schijf update](/cli/azure/disk#update). Hallo volgende voorbeeld wordt uitgebreid beheerde Hallo-schijf met de naam *myDataDisk* toobe *200*Gb in grootte:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Wanneer u een beheerde schijf wilt uitbreiden, is bijgewerkt Hallo grootte toegewezen toohello dichtstbijzijnde beheerde schijfgrootte. Zie voor een tabel van Hallo beheerde schijfgrootten beschikbaar en lagen [beheerd schijven overzicht van Azure - prijzen en facturering](../windows/managed-disks-overview.md#pricing-and-billing).

3. Start de virtuele machine met [az vm start](/cli/azure/vm#start). Hallo volgende voorbeeld wordt gestart met de naam VM Hallo *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM met de juiste referenties Hallo. U kunt verkrijgen Hallo openbare IP-adres van uw virtuele machine met [az vm weergeven](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. Hallo toouse schijf uitgebreid, moet u tooexpand Hallo onderliggende partitie en het bestandssysteem.

    a. Als al is gekoppeld, ontkoppelt Hallo schijf:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Gebruik `parted` tooview informatie schijf en het formaat Hallo-partitie:

    ```bash
    sudo parted /dev/sdc
    ```

    Informatie weergeven over Hallo bestaande partitie-indeling met `print`. Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld ziet u de onderliggende schijf Hallo is 215Gb groot:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Vouw Hallo-partitie met `resizepart`. Voer Hallo partitienummer, *1*, en een grootte voor de nieuwe partitie Hallo:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, invoeren`quit`

5. Controleren met Hallo partitie is gewijzigd, Hallo partitie consistentie met `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Nu vergroten of verkleinen Hallo bestandssysteem met `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Koppelpunt Hallo partitie toohello gewenste locatie, zoals `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. tooverify hello OS-schijf is gewijzigd, gebruikt u `df -h`. Hallo volgende voorbeelduitvoer toont Hallo gegevensstation, */dev/sdc1*, is nu 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Volgende stappen
Als u extra opslagruimte, moet u ook [gegevens schijven tooa Linux VM toevoegen](add-disk.md). Zie voor meer informatie over schijfversleuteling [versleutelen schijven op een Linux-VM met behulp van Azure CLI Hallo](encrypt-disks.md).
