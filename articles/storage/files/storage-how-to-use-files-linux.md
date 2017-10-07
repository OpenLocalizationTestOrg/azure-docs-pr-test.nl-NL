---
title: Azure File storage met Linux aaaUse | Microsoft Docs
description: Meer informatie over hoe toomount een Azure-bestand delen via SMB op Linux.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Azure File storage gebruiken met Linux
[Azure File storage](../storage-dotnet-how-to-use-files.md) is van Microsoft easy toouse cloud-bestandssysteem. Azure-bestandsshares kunnen worden gekoppeld in Linux-distributies met Hallo [cifs utils pakket](https://wiki.samba.org/index.php/LinuxCIFS_utils) van Hallo [Samba project](https://www.samba.org/). In dit artikel ziet u twee manieren toomount een Azure-bestandsshare: op aanvraag Hello `mount` opdracht en op opstarten door het maken van een vermelding in `/etc/fstab`.

> [!NOTE]  
> In volgorde toomount een Azure-bestandsshare buiten hello moet Azure-regio die deze wordt gehost in, bijvoorbeeld on-premises of in een andere Azure-regio Hallo OS ondersteunen Hallo versleuteling van SMB 3.0. Coderingsfunctie voor SMB 3.0 voor Linux is geïntroduceerd in 4.11 kernel. Deze functie kunt koppelen van de bestandsshare in Azure vanaf on-premises of andere Azure-regio. Deze functionaliteit is op Hallo moment van publicatie, backported tooUbuntu van 16.04 en hoger.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Prerequisities voor het koppelen van een Azure-bestandsshare met Linux en Hallo cifs-utils-pakket
* **Kies een Linux-distributie waarvoor Hallo cifs utils pakket is geïnstalleerd kan**: Microsoft raadt Hallo Linux-distributies in de afbeelding voor Azure-galerie hello te volgen:

    * Ubuntu Server 14.04 +
    * RHEL 7 +
    * CentOS 7 +
    * Debian 8
    * openSUSE 13.2 +
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Hallo cifs utils pakket is geïnstalleerd**: Hallo cifs-utils kan worden geïnstalleerd met behulp van Pakketbeheer Hallo op Hallo Linux-distributie van uw keuze. 

    Op **Ubuntu** en **op basis van Debian** distributies, gebruik Hallo `apt-get` Pakketbeheer:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    Op **RHEL** en **CentOS**, gebruik Hallo `yum` Pakketbeheer:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    Op **openSUSE**, gebruik Hallo `zypper` Pakketbeheer:

    ```
    sudo zypper install samba*
    ```

    Op andere distributies Hallo juiste package manager gebruiken of [compileren van bron](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Besluit op Hallo van map/bestand machtigingen van de gekoppelde share Hallo**: In de onderstaande Hallo voorbeelden, gebruiken we 0777, toogive lezen, schrijven en uitvoeren van machtigingen tooall gebruikers. U kunt het vervangen door andere [type chmod machtigingen](https://en.wikipedia.org/wiki/Chmod) naar wens. 

* **Naam van het opslagaccount**: toomount een Azure-bestand delen, kunt u moet Hallo naam van het opslagaccount Hallo.

* **Opslagaccountsleutel**: toomount een Azure-bestand delen, kunt u moet Hallo primaire (of secundaire)-opslagsleutel. SAS-sleutels worden momenteel niet ondersteund voor koppelen.

* **Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445 - controleren toosee als uw firewall niet wordt geblokkeerd door TCP-poorten 445 van client-computer.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Hello Azure-op-verzoek met de bestandsshare koppelen`mount`
1. **[Hallo cifs utils pakket voor uw Linux-distributie](#install-cifs-utils)**.

2. **Maak een map voor het koppelpunt Hallo**: dit kan overal worden gedaan op Hallo-bestandssysteem.

    ```
    mkdir mymountpoint
    ```

3. **Gebruik Hallo koppelpunt opdracht toomount hello Azure File share**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, en `<storage-account-key>` met de juiste informatie Hallo.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Wanneer u klaar bent met behulp van Azure-bestandsshare Hallo, u kunt gebruiken `sudo umount ./mymountpoint` toounmount Hallo share.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Maken van een permanente koppelpunt voor hello Azure-bestandsshare met`/etc/fstab`
1. **[Hallo cifs utils pakket voor uw Linux-distributie](#install-cifs-utils)**.

2. **Maak een map voor het koppelpunt Hallo**: dit kan overal worden gedaan op Hallo bestandssysteem, maar u moet toonote Hallo absolute pad van Hallo-map. Hallo volgende voorbeeld maakt een map onder de hoofdmap.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Gebruik Hallo volgende opdracht tooappend Hallo volgt regel te`/etc/fstab`**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, en `<storage-account-key>` met de juiste informatie Hallo.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> U kunt `sudo mount -a` toomount Hallo bestandsshare in Azure na het bewerken van `/etc/fstab` in plaats van opnieuw opstarten.

## <a name="feedback"></a>Feedback
Linux-gebruikers, willen we toohear van u!

Hello Azure File storage voor Linux gebruikersgroep biedt een forum voor u tooshare feedback terwijl u evalueren en een bestandsopslag op Linux vast. E-mailadres [Azure File storage Linux gebruikers](mailto:azurefileslinuxusers@microsoft.com) toojoin Hallo gebruikersgroep.

## <a name="next-steps"></a>Volgende stappen
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.
* [Naslaginformatie over REST API voor bestandsservices](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Hoe toouse AzCopy met Microsoft Azure storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI gebruiken met Azure storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Veelgestelde vragen](../storage-files-faq.md)
* [Problemen oplossen](storage-troubleshoot-linux-file-connection-problems.md)
