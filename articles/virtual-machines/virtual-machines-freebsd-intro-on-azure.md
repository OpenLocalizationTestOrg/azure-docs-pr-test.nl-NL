---
title: aaaIntroduction tooFreeBSD in Azure | Microsoft Docs
description: Meer informatie over het gebruik van FreeBSD virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>TooFreeBSD inleiding op Azure
Dit onderwerp bevat een overzicht van een FreeBSD virtuele machine in Azure wordt uitgevoerd.

## <a name="overview"></a>Overzicht
FreeBSD voor Microsoft Azure is dat een geavanceerde computerbesturingssysteem gebruikt toopower moderne servers, desktops en ingesloten platforms.

Microsoft Corporation is afbeeldingen van FreeBSD beschikbaar maken op Azure Hello [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) vooraf is geconfigureerd. Op dit moment wordt hello volgende FreeBSD versies aangeboden als afbeeldingen door Microsoft:

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

Hallo-agent is verantwoordelijk voor de communicatie tussen Hallo FreeBSD VM en hello Azure-infrastructuur voor bewerkingen, zoals inrichten Hallo VM op het eerste gebruik (gebruikersnaam, wachtwoord of SSH-sleutel, hostnaam, enz.) en het inschakelen van de functionaliteit voor selectief VM-extensies.

Als voor toekomstige versies van FreeBSD Hallo-strategie is de huidige toostay en Hallo meest recente versies beschikbaar kort nadat deze zijn gepubliceerd door Hallo FreeBSD release engineering team.

## <a name="deploying-a-freebsd-virtual-machine"></a>Een FreeBSD virtuele machine implementeren
Een FreeBSD virtuele machine implementeert, is een eenvoudig proces met behulp van een installatiekopie van hello Azure Marketplace van hello Azure-portal:

- [FreeBSD 10.3 op Hallo Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [FreeBSD 11.0 op Hallo Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Een FreeBSD virtuele machine via Azure CLI 2.0 in FreeBSD maken
U moet eerst tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Hoewel de volgende opdracht op een machine FreeBSD.

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

Als bash niet is geïnstalleerd op uw machine FreeBSD, voert u de volgende opdracht voorafgaand aan installatie Hallo. 

```
    sudo pkg install bash
```

Als python niet is geïnstalleerd op uw machine FreeBSD, voert u de volgende opdrachten voorafgaand aan installatie Hallo. 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

U wordt gevraagd tijdens de installatie van Hallo `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Als u beantwoorden `y` en voer `/etc/rc.conf` als `a path tooan rc file tooupdate`, u wellicht voldoen aan de Hallo probleem `ERROR: [Errno 13] Permission denied`. tooresolve dit probleem, moet u Hallo schrijven rechts toocurrent gebruiker tegen Hallo bestand toekennen `etc/rc.conf`.

U kunt nu aanmelden met Azure en uw FreeBSD VM maken. Hieronder volgt een voorbeeld toocreate een FreeBSD 11.0 VM. U kunt ook de parameter Hallo toevoegen `--public-ip-address-dns-name` met een globaal unieke DNS-naam voor een nieuwe openbare IP-adres. 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

U kunt vervolgens tooyour FreeBSD VM via Hallo IP-adres dat in de uitvoer Hallo van hierboven implementatie afgedrukt aanmelden. 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>VM-extensies voor FreeBSD
Hieronder vindt u ondersteunde VM-extensies in FreeBSD.

### <a name="vmaccess"></a>VMAccess
Hallo [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) uitbreiding kunt:

* Hallo-wachtwoord opnieuw instellen van Hallo oorspronkelijke sudo-gebruiker.
* Maak een nieuwe gebruiker van de sudo met Hallo wachtwoord opgegeven.
* Stel Hallo van de openbare hostsleutel met Hallo sleutel opgegeven.
* Opnieuw instellen Hallo van de openbare hostsleutel opgegeven tijdens de VM-inrichting als Hallo host-sleutel is niet opgegeven.
* Open Hallo SSH-poort (22) en Hallo sshd_config herstellen als reset_ssh tootrue is ingesteld.
* Verwijder bestaande Hallo-gebruiker.
* Controleer de schijven.
* Een extra schijf repareren.

### <a name="customscript"></a>CustomScript
Hallo [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) uitbreiding kunt:

* Indien opgegeven, download u Hallo aangepaste scripts van Azure Storage of een externe openbare opslag (bijvoorbeeld GitHub).
* Hallo vermelding punt script uitvoeren.
* Ondersteuning voor inline-opdrachten.
* Windows-stijl nieuwe regel in de schaal en Python-scripts automatisch converteren.
* Verwijder BOM automatisch in de shell- en Python-scripts.
* Gevoelige gegevens in CommandToExecute beveiligd.

> [!NOTE]
> FreeBSD VM ondersteunt alleen CustomScript versie 1.x nu.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Verificatie: gebruikersnamen, wachtwoorden en SSH-sleutels
Wanneer u een FreeBSD virtuele machine met behulp van hello Azure-portal maakt, moet u een gebruikersnaam, wachtwoord of openbare SSH-sleutel opgeven.
Gebruikersnamen voor het implementeren van een FreeBSD virtuele machine in Azure mag niet overeenkomen met de namen van systeemaccounts (UID < 100) al aanwezig in Hallo virtuele machine ('root', bijvoorbeeld).
Alleen Hallo RSA SSH-sleutel wordt momenteel ondersteund. Een SSH-sleutel met meerdere regels moet beginnen met `---- BEGIN SSH2 PUBLIC KEY ----` en eindigen met `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Het verkrijgen van supergebruiker bevoegdheden
Hallo-gebruikersaccount dat is opgegeven tijdens de implementatie van de virtuele machine-exemplaar in Azure is een bevoegd account. Hallo pakket van sudo is geïnstalleerd Hallo gepubliceerd FreeBSD installatiekopie.
Nadat u bent aangemeld via dit gebruikersaccount, kunt u opdrachten uitvoeren als hoofdmap door Hallo opdrachtsyntaxis.

```
    $ sudo <COMMAND>
```

U kunt desgewenst een shell basis verkrijgen via `sudo -s`.

## <a name="known-issues"></a>Bekende problemen
Hallo [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) versie 2.2.2 heeft een [bekend probleem] (https://github.com/Azure/WALinuxAgent/pull/517) die ervoor zorgt dat Hallo inrichten fout voor FreeBSD VM op Azure. Hallo werd fix vastgelegd door [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) versie 2.2.3 en latere versies. 

## <a name="next-steps"></a>Volgende stappen
* Ga te[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate een FreeBSD VM.
* Als u uw eigen tooAzure FreeBSD toobring wilt, Raadpleeg te[maken en uploaden een tooAzure FreeBSD VHD](linux/classic/freebsd-create-upload-vhd.md).
