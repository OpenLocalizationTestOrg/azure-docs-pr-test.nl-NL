---
title: aaaReset Linux VM wachtwoord en SSH-sleutel uit Hallo CLI | Microsoft Docs
description: Hoe toouse hello VMAccess-extensie van hello Azure-opdrachtregelinterface (CLI) tooreset een Linux-VM-wachtwoord of SSH-sleutel, herstel Hallo SSH-configuratie en consistentie van de schijf controleren
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Hoe tooreset een Linux-VM-wachtwoord of SSH-sleutel, los Hallo SSH-configuratie en consistentie van de schijf met behulp van Hallo VMAccess-extensie controleren
Als u geen tooa virtuele Linux-machine in Azure verbinding maken vanwege een vergeten wachtwoord, een onjuiste sleutel voor Secure Shell (SSH) of een probleem met de Hallo SSH-configuratie, Hallo VMAccessForLinux-extensie met hello Azure CLI tooreset Hallo wachtwoord of SSH-sleutel, oplossen Hallo SSH-configuratie en controleren van de consistentie van de schijf. 

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Met hello Azure CLI, gebruikt u Hallo **azure vm-extensie set** via de opdrachtregelinterface (Bash, Terminal-opdrachtprompt) tooaccess-opdrachten. Voer **help azure vm-extensie set** voor het gebruik van gedetailleerde extensie.

U kunt doen met Azure CLI hello, Hallo volgende taken:

* [Hallo-wachtwoord opnieuw instellen](#pwresetcli)
* [Hallo SSH-sleutel opnieuw instellen](#sshkeyresetcli)
* [Hallo wachtwoord en Hallo SSH-sleutel opnieuw instellen](#resetbothcli)
* [Een nieuw sudo-gebruikersaccount maken](#createnewsudocli)
* [Hallo SSH-configuratie opnieuw instellen](#sshconfigresetcli)
* [Een gebruiker verwijderen](#deletecli)
* [Hallo-status van Hallo VMAccess-extensie weergeven](#statuscli)
* [Controleer de consistentie van toegevoegde schijven](#checkdisk)
* [Herstellen van toegevoegde schijven op uw Linux-VM](#repairdisk)

## <a name="prerequisites"></a>Vereisten
Hiervoor hebt u toodo Hallo volgende nodig:

* U moet te[hello Azure CLI installeren](../../../cli-install-nodejs.md) en [tooyour abonnement verbinding](../../../xplat-cli-connect.md) toouse Azure resources zijn gekoppeld aan uw account.
* Juiste modus voor het klassieke implementatiemodel Hallo HALLO hallo door volgende te typen bij de opdrachtprompt Hallo instellen:
    ``` 
        azure config mode asm
    ```
* Een nieuw wachtwoord of SSH-sleutels hebben als u wilt dat tooreset een. U kunt deze niet nodig als u wilt dat tooreset Hallo SSH-configuratie.

## <a name="pwresetcli"></a>Hallo-wachtwoord opnieuw instellen
1. Maak een bestand op uw lokale computer met de naam PrivateConf.json met deze regels. Vervang **gebruik met Windows** en  **myP@ssW0rd**  met uw eigen gebruikersnaam en wachtwoord en stel uw eigen datum voor verlopen.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Hallo SSH-sleutel opnieuw instellen
1. Maak een bestand met de naam PrivateConf.json met deze inhoud. Vervang Hallo **gebruik met Windows** en **mySSHKey** waarden door uw eigen waarden.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Zowel Hallo wachtwoord en Hallo SSH-sleutel opnieuw instellen
1. Maak een bestand met de naam PrivateConf.json met deze inhoud. Vervang Hallo **gebruik met Windows**, **mySSHKey** en  **myP@ssW0rd**  waarden door uw eigen waarden.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Een nieuw sudo-gebruikersaccount maken

Als u uw gebruikersnaam vergeet, kunt u VMAccess toocreate een nieuw bestand met de Hallo sudo-instantie. In dit geval Hallo bestaande gebruikersnaam en wachtwoord worden niet gewijzigd.

een nieuwe sudo-gebruiker met wachtwoord toegang, gebruik Hallo script in toocreate [Hallo-wachtwoord opnieuw instellen](#pwresetcli) en Hallo nieuwe gebruikersnaam opgeven.

een nieuwe gebruiker met sudo met SSH toegang tot de sleutel, gebruik Hallo script in toocreate [Hallo SSH-sleutel opnieuw instellen](#sshkeyresetcli) en geeft u de nieuwe gebruikersnaam Hallo.

U kunt ook [Hallo wachtwoord en het Hallo SSH-sleutel opnieuw ingesteld](#resetbothcli) toocreate een nieuwe gebruiker met wachtwoord en toegang tot de sleutel van SSH.

## <a name="sshconfigresetcli"></a>Hallo SSH-configuratie opnieuw instellen
Als SSH-configuratie Hallo zich in een ongewenste status, kunt u ook toegang toohello VM verliezen. U kunt Hallo VMAccess-extensie tooreset hello tooits standaard configuratiestatus gebruiken. toodo dus u hoeft alleen maar tooset Hallo 'reset_ssh' sleutel te 'True'. Hallo-extensie wordt Hallo SSH-server opnieuw opstarten en opent u Hallo SSH-poort op de virtuele machine Hallo SSH configuratiewaarden toodefault opnieuw instellen. Hallo gebruikersaccount (naam, wachtwoord of SSH-sleutels) worden niet gewijzigd.

> [!NOTE]
> /etc/ssh/sshd_config bevindt Hallo SSH-configuratiebestand die opnieuw wordt ingesteld.
> 
> 

1. Maak een bestand met de naam PrivateConf.json met deze inhoud.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Een gebruiker verwijderen
Als u een gebruikersaccount zonder aan te melden bij toohello VM rechtstreeks toodelete wilt, kunt u dit script gebruiken.

1. Maak een bestand met de naam PrivateConf.json met deze inhoud, vervangen door Hallo gebruiker naam tooremove voor **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Hallo-status van Hallo VMAccess-extensie weergeven
status van de toodisplay Hallo Hallo VMAccess-extensie, wordt deze opdracht uitvoeren.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Controleer de consistentie van toegevoegde schijven
toorun fsck op alle schijven in uw virtuele Linux-machine, moet u toodo Hallo volgende:

1. Maak een bestand met de naam PublicConf.json met deze inhoud. Controleer de dat schijf duurt voordat een Booleaanse waarde of toocheck schijven tooyour virtuele machine gekoppeld. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Voer deze opdracht tooexecute, vervangen door de naam van uw virtuele machine voor Hallo **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Herstellen van schijven
toorepair-schijven die u niet wilt koppelen of koppelpunt configuratiefouten hebt, gebruikt u Hallo VMAccess-extensie tooreset Hallo koppelpunt configuratie op uw virtuele Linux-machine. Hallo-naam van de schijf vervangen door **myDisk**.

1. Maak een bestand met de naam PublicConf.json met deze inhoud. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Voer deze opdracht tooexecute, vervangen door de naam van uw virtuele machine voor Hallo **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Volgende stappen
* Als u toouse Azure PowerShell-cmdlets of Azure Resource Manager sjablonen tooreset Hallo wachtwoord of SSH-sleutel wilt, los Hallo SSH-configuratie, en controleren van de consistentie van de schijf, Zie Hallo [VMAccess-extensie-documentatie op GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* U kunt ook Hallo [Azure-portal](https://portal.azure.com) tooreset Hallo wachtwoord of SSH-sleutel van een Linux-VM in het klassieke implementatiemodel Hallo geïmplementeerd. U kunt momenteel Hallo portal wilt toothis gebruiken voor een Linux-VM is geïmplementeerd in Hallo Resource Manager-implementatiemodel.
* Zie [over functies en uitbreidingen van de virtuele machine](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over het gebruik van VM-extensies voor Azure virtual machines.

