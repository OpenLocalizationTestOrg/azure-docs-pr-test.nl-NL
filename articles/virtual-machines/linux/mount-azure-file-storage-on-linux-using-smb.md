---
title: Azure File storage in virtuele Linux-machines met SMB aaaMount | Microsoft Docs
description: Hoe toomount Azure File storage in virtuele Linux-machines met SMB met Azure CLI 2.0 Hallo
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Koppelpunt Azure File storage in virtuele Linux-machines met SMB

Dit artikel laat zien hoe tooutilize hello Azure File storage-service op een Linux-VM met behulp van SMB Hello Azure CLI 2.0 koppelen. Azure File storage biedt bestandsshares in de cloud van Hallo Hallo standaard SMB-protocol gebruiken. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hallo-vereisten zijn:

- [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)
- [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Snelle opdrachten

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
toodo toevoegen dus Hallo regel toohello na `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

File storage biedt bestandsshares in de cloud Hallo Hallo standaard SMB-protocol gebruiken. Met de meest recente release van File storage Hallo kunt u ook een bestandsshare koppelen vanuit elk besturingssysteem dat ondersteuning biedt voor SMB 3.0. Als u een SMB-koppelen op Linux gebruikt, krijgt u eenvoudig back-ups tooa robuuste, permanente archiveren locatie voor de opslag die wordt ondersteund door een SLA.

Verplaatsen van bestanden in een VM tooan SMB koppelpunt wordt gehost op File storage is dat een uitstekende manier toodebug registreert. Dat komt doordat Hallo dezelfde SMB-share worden gekoppeld, lokaal tooyour Mac, Linux of Windows-werkstation. SMB niet Hallo beste oplossing voor het streamen van Linux of toepassingslogboeken in real-time, omdat Hallo SMB-protocol niet is ingebouwd toohandle deze rechten zware logboekregistratie. Een speciale, uniforme logboekregistratie laag hulpprogramma zoals Fluentd zou een betere keuze dan SMB zijn voor het verzamelen van Linux- en uitvoer logboekregistratie toepassing.

Voor deze gedetailleerde procedure maken we Hallo vereisten nodig toofirst Hallo File storage-share maken en klik vervolgens op een Linux-VM via SMB koppelen.

1. Maak een resourcegroep met [az groep maken](/cli/azure/group#create) toohold Hallo-bestandsshare.

    een resourcegroep met de naam toocreate `myResourceGroup` in Hallo 'VS-West' locatie, gebruikt u Hallo voorbeeld te volgen:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Maken van een Azure storage-account met [az storage-account maken](/cli/azure/storage/account#create) toostore Hallo bestanden.

    toocreate een opslagaccount met de naam mystorageaccount hello Standard_LRS opslag SKU, gebruik Hallo voorbeeld te volgen:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Hallo-toegangscodes voor opslag weergeven.

    Wanneer u een opslagaccount maakt, worden de Hallo toegangscodes zodat ze kunnen worden gedraaid zonder onderbreking van de service in paren worden gemaakt. Wanneer u de tweede sleutel toohello Hallo paar overschakelt, maakt u een nieuw sleutelpaar. Nieuwe toegangscodes voor opslag worden altijd paarsgewijs ervoor te zorgen dat u altijd ten minste één niet-gebruikte opslag account key gereed tooswitch te hebben gemaakt.

    Hallo opslagaccountsleutels Hello weergeven [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list). Hallo toegangscodes voor opslag voor Hallo met de naam `mystorageaccount` worden vermeld in Hallo voorbeeld te volgen:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract één sleutel gebruiken Hallo `--query` vlag. Hallo volgende voorbeeld worden de eerste sleutel hello (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Hallo File storage-share maken.

    Hallo File storage-share bevat met de SMB-share Hallo [az storage-share maken](/cli/azure/storage/share#create). Hallo quotum wordt altijd uitgedrukt in gigabytes (GB). Doorgeven in een Hallo sleutels uit voorgaande Hallo `az storage account keys list` opdracht. Maak een share met de naam mystorageshare met een target 10 GB met behulp van Hallo voorbeeld te volgen:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Maak een map koppelpunt.

    Een lokale map maken in Hallo Linux bestand system toomount Hallo naar de SMB-share. Geschreven of gelezen uit de lokale Koppelmap Hallo wordt toohello SMB-share die wordt gehost op de opslag van bestanden doorgestuurd. toocreate een lokale map op/mnt/mymountdirectory, gebruik Hallo voorbeeld te volgen:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Hallo SMB-share toohello lokale directory te koppelen.

    Geef uw eigen storage account gebruikersnaam en het opslagaccountsleutel voor Hallo koppelpunt referenties als volgt:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Bewaren Hallo SMB koppelen via opnieuw wordt opgestart.

    Wanneer u de computer opnieuw Hallo Linux VM opstart, is hello gekoppelde SMB-share ontkoppeld tijdens het afsluiten. tooremount hello SMB-share opstart, een regel toohello Linux /etc/fstab toevoegen. Hallo fstab-bestand toolist Hallo bestandssystemen toomount moet tijdens het opstartproces Hallo maakt gebruik van Linux. Toe te voegen Hallo SMB-share zorgt ervoor dat Hallo File storage-share is een permanent gekoppelde bestandssysteem voor Hallo Linux VM. Hallo bestand opslag SMB-share tooa toe te voegen is nieuwe virtuele machine mogelijk wanneer u cloud-init gebruiken.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Volgende stappen

- [Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Voeg een schijf tooa Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Versleutelen van schijven op een Linux-VM met behulp van hello Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
