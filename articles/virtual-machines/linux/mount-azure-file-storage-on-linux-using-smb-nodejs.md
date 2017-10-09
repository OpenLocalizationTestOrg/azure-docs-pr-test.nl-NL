---
title: Azure File storage in Linux VM's met behulp van SMB met Azure CLI 1.0 aaaMount | Microsoft Docs
description: Hoe toomount Azure File storage in Linux VM's via SMB
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Koppelpunt Azure File storage in Linux VM's met behulp van SMB met Azure CLI 1.0

Dit artikel laat zien hoe toomount Azure File storage in een Linux-VM met behulp van Server Message Block (SMB)-protocol Hallo. File storage biedt bestandsshares in de cloud Hallo via Hallo standaard SMB-protocol. Hallo-vereisten zijn:

* Een [Azure-account](https://azure.microsoft.com/pricing/free-trial/)
* [Secure Shell (SSH) openbare en persoonlijke sleutelbestanden](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>CLI-versies toouse
U kunt Hallo taak uitvoeren met behulp van een van de volgende versies van de opdrachtregelinterface (CLI) Hallo:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten
tooaccomplish hello taak snel stappen Hallo in deze sectie. Voor meer informatie en context gedetailleerde, beginnen op Hallo ['Gedetailleerd overzicht'](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sectie.

### <a name="prerequisites"></a>Vereisten
* Een resourcegroep
* Een Azure-netwerk
* Een netwerkbeveiligingsgroep met een SSH inkomende
* Een subnet
* Een Azure storage-account
* Sleutels voor Azure-opslagaccount
* Een Azure File storage-share
* Een virtuele Linux-machine

Geen voorbeelden vervangen door uw eigen instellingen.

### <a name="create-a-directory-for-hello-local-mount"></a>Maak een map voor lokale koppeling Hallo

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Hallo bestand opslag toohello koppelpunt wordt gehost SMB-share koppelen

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Hallo koppelpunt behouden na opnieuw opstarten
Hallo volgt regel te toevoegen`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

File storage biedt bestandsshares in de cloud Hallo Hallo standaard SMB-protocol gebruiken. Met de meest recente release van File storage Hallo kunt u ook een bestandsshare koppelen vanuit elk besturingssysteem dat ondersteuning biedt voor SMB 3.0. Als u een SMB-koppelen op Linux gebruikt, krijgt u eenvoudig back-ups tooa robuuste, permanente archiveren locatie voor de opslag die wordt ondersteund door een SLA.

Verplaatsen van bestanden in een VM tooan SMB koppelpunt wordt gehost op File storage is dat een uitstekende manier toodebug registreert. Dat komt doordat Hallo dezelfde SMB-share worden gekoppeld, lokaal tooyour Mac, Linux of Windows-werkstation. SMB niet Hallo beste oplossing voor het streamen van Linux of toepassingslogboeken in real-time, omdat Hallo SMB-protocol niet is ingebouwd toohandle deze rechten zware logboekregistratie. Een speciale, uniforme logboekregistratie laag hulpprogramma zoals Fluentd zou een betere keuze dan SMB zijn voor het verzamelen van Linux- en uitvoer logboekregistratie toepassing.

Voor deze gedetailleerde procedure maken we Hallo vereisten nodig toofirst Hallo File storage-share maken en klik vervolgens op een Linux-VM via SMB koppelen.

1. Een Azure storage-account maken met behulp van de volgende code Hallo:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Hallo-toegangscodes voor opslag weergeven.

    Wanneer u een opslagaccount maakt, worden de Hallo toegangscodes zodat ze kunnen worden gedraaid zonder onderbreking van de service in paren worden gemaakt. Wanneer u de tweede sleutel toohello Hallo paar overschakelt, maakt u een nieuw sleutelpaar. Nieuwe toegangscodes voor opslag worden altijd paarsgewijs ervoor te zorgen dat u altijd ten minste één niet-gebruikte opslag sleutel gereed tooswitch te hebben gemaakt. tooshow-opslagaccountsleutels voor Hallo Hallo volgende code gebruiken:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Hallo File storage-share maken.

    Hallo File storage-share bevat Hallo SMB-share. Hallo quotum wordt altijd uitgedrukt in gigabytes (GB). toocreate Hallo File storage-share, Hallo volgende code gebruiken:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Hallo koppelpunt map maken.

    U moet een lokale map maken in Hallo Linux bestand system toomount Hallo naar de SMB-share. Geschreven of gelezen uit de lokale Koppelmap Hallo wordt toohello SMB-share die wordt gehost op de opslag van bestanden doorgestuurd. toocreate hello directory gebruik Hallo code te volgen:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. SMB-share met behulp van de volgende code Hallo Hallo koppelen:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Bewaren Hallo SMB koppelen via opnieuw wordt opgestart.

    Wanneer u de computer opnieuw Hallo Linux VM opstart, is hello gekoppelde SMB-share ontkoppeld tijdens het afsluiten. tooremount hello SMB-share op opstarten, moet u een regel toohello Linux /etc/fstab toevoegen. Hallo fstab-bestand toolist Hallo bestandssystemen toomount moet tijdens het opstartproces Hallo maakt gebruik van Linux. Toe te voegen Hallo SMB-share zorgt ervoor dat Hallo File storage-share is een permanent gekoppelde bestandssysteem voor Hallo Linux VM. Hallo bestand opslag SMB-share tooa toe te voegen is nieuwe virtuele machine mogelijk wanneer u cloud-init gebruiken.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Volgende stappen

- [Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Voeg een schijf tooa Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Versleutelen van schijven op een Linux-VM met behulp van hello Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
