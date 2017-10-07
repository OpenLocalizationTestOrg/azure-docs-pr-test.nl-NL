---
title: een gebruiker tooa Linux VM op Azure aaaAdd | Microsoft Docs
description: Een gebruiker tooa Linux VM op Azure toevoegen.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Toevoegen van een gebruiker tooan Azure VM
Een eerste taken op een nieuwe Linux-VM Hallo is toocreate een nieuwe gebruiker.  In dit artikel we helpt bij het maken van een sudo-gebruikersaccount en wachtwoord instellen hello, toe te voegen SSH openbare sleutels, en ten slotte gebruiken `visudo` tooallow sudo zonder wachtwoord.

Vereisten zijn: [een Azure-account](https://azure.microsoft.com/pricing/free-trial/), [SSH openbare en persoonlijke sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), een Azure-resourcegroep en hello Azure CLI geïnstalleerd en gewijzigd tooAzure Resource Manager modus gebruiken `azure config mode arm`.

## <a name="quick-commands"></a>Snelle opdrachten
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
### <a name="introduction"></a>Inleiding
Een van de eerste en de meest voorkomende taak Hallo met een nieuwe server is tooadd een gebruikersaccount.  Hoofdmap aanmeldingen moeten zijn uitgeschakeld en Hallo root-account zelf mag niet worden gebruikt met uw Linux-server alleen sudo.  Geeft een gebruiker hoofdmap escalatie bevoegdheden met ' sudo ' het juiste manier tooadminister Hallo samen met Linux.

Met de opdracht Hallo `useradd` we gebruiker accounts toohello Linux VM toevoegen.  Met `useradd` wijzigt `/etc/passwd`, `/etc/shadow`, `/etc/group`, en `/etc/gshadow`.  We een opdrachtregelprogramma vlag toohello toevoegen `useradd` opdracht tooalso Hallo nieuwe toohello juiste sudo gebruikersgroep toevoegen op Linux.  Zelfs als u `useradd` maakt u een vermelding in de `/etc/passwd` deze geeft geen nieuwe gebruikersaccount Hallo een wachtwoord.  Maakt een initiële wachtwoord voor de nieuwe gebruiker Hallo Hallo eenvoudig met `passwd` opdracht.  de laatste stap Hallo is toomodify hello sudo regels tooallow die gebruiker tooexecute opdrachten met bevoegdheden voor sudo zonder tooenter een wachtwoord op voor elke opdracht.  Aanmelden met behulp van de persoonlijke sleutel hello wordt uitgegaan van een gebruikersaccount is beschermd tegen ongewenste actoren en gaat tooallow sudo toegang zonder een wachtwoord.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Toevoegen van een sudo met één gebruiker tooan Azure VM
Meld u bij toohello Azure VM SSH-sleutels gebruiken.  Als er geen installatie SSH openbare toegang tot de sleutel, eerst te voltooien in dit artikel [verificatie van openbare sleutel met Azure met behulp van](http://link.to/article).  

Hallo `useradd` opdracht is voltooid Hallo taken te volgen:

* een nieuw gebruikersaccount maken
* Maak een nieuwe gebruikersgroep met de Hallo dezelfde naam
* een lege waarde te toevoegen`/etc/passwd`
* een lege waarde te toevoegen`/etc/gpasswd`

Hallo `-G` opdrachtregelprogramma vlag Hallo nieuwe gebruiker account toohello juiste Linux groep toegevoegd zodat nieuwe gebruikersaccount Hallo hoofdmap uitbreiding van bevoegdheden.

#### <a name="add-hello-user"></a>Hallo-gebruiker toevoegen
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Een wachtwoord instellen
Hallo `useradd` opdracht Hallo gebruiker maakt en voegt u een vermelding tooboth `/etc/passwd` en `/etc/gpasswd` maar niet daadwerkelijk Hallo wachtwoord ingesteld.  Hallo wachtwoord wordt toegevoegd toohello vermelding met Hallo `passwd` opdracht.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

We nu hebben een gebruiker met sudo-machtigingen op Hallo-server.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Uw openbare SSH-sleutel toohello nieuwe gebruikersaccount toevoegen
Gebruik van uw computer, Hallo `ssh-copy-id` opdracht met Hallo nieuwe wachtwoord.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Met behulp van visudo tooallow sudo gebruik zonder wachtwoord
Met behulp van `visudo` tooedit hello `/etc/sudoers` bestand enkele lagen van bescherming tegen onjuist wijzigen van deze belangrijk bestand toegevoegd.  Bij het uitvoeren van `visudo`, Hallo `/etc/sudoers` bestand is vergrendeld tooensure andere gebruikers geen wijzigingen kunt aanbrengen, terwijl deze actief wordt bewerkt.  Hallo `/etc/sudoers` bestand ook gecontroleerd op fouten door `visudo` wanneer u probeert toosave of sluiten zodat u een verbroken sudoers-bestand niet opslaan.

Er bestaat reeds gebruikers in de juiste standaardgroep Hallo voor sudo-toegang.  Nu gaan we tooenable die groepen toouse sudo zonder wachtwoord.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Controleer of gebruiker hello, ssh-sleutels en sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
