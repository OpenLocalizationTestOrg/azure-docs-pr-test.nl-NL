---
title: Een gebruiker toevoegen aan een Linux-VM op Azure | Microsoft Docs
description: Een gebruiker toevoegen aan een Linux-VM op Azure.
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
ms.openlocfilehash: a95157f57c0cbd1f2a9ed68a0fe83140d7c9ec40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-user-to-an-azure-vm"></a>Een gebruiker toevoegen aan een Azure VM
Een van de eerste taken op een nieuwe Linux-VM is het maken van een nieuwe gebruiker.  In dit artikel we doorlopen een sudo-gebruikersaccount maken voor het instellen van het wachtwoord toe te voegen SSH openbare sleutels, en ten slotte gebruiken `visudo` om toe te staan sudo zonder wachtwoord.

Vereisten zijn: [een Azure-account](https://azure.microsoft.com/pricing/free-trial/), [SSH openbare en persoonlijke sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), een Azure-resourcegroep en Azure CLI geïnstalleerd en wordt overgeschakeld naar het gebruik van Azure Resource Manager-modus `azure config mode arm`.

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

# Copy the SSH Public Key to the new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers to allow no password
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify the SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht
### <a name="introduction"></a>Inleiding
Een van de eerste en de meest voorkomende taak met een nieuwe server is het toevoegen van een gebruikersaccount.  Hoofdmap aanmeldingen moeten zijn uitgeschakeld en het hoofdaccount zelf mag niet worden gebruikt met uw Linux-server alleen sudo.  Uitbreiding van bevoegdheden met ' sudo ' voor de hoofdmap van een gebruiker zodat deze de juiste manier te beheren en gebruiken van Linux.

Met de opdracht `useradd` we gebruikersaccounts toevoegen aan de Linux-VM.  Met `useradd` wijzigt `/etc/passwd`, `/etc/shadow`, `/etc/group`, en `/etc/gshadow`.  We een opdrachtregelprogramma vlag wilt toevoegen de `useradd` opdracht ook de nieuwe gebruiker toevoegen aan de juiste sudo-groep op Linux.  Zelfs als u `useradd` maakt u een vermelding in de `/etc/passwd` deze geeft geen nieuwe gebruikersaccount een wachtwoord.  Maakt u een eerste wachtwoord voor de nieuwe gebruiker met behulp van de eenvoudige `passwd` opdracht.  De laatste stap is het wijzigen van de sudo-regels voor het toestaan van die gebruiker met bevoegdheden voor sudo-opdrachten uitvoeren zonder een wachtwoord opgeven voor elke opdracht.  Aanmelden met behulp van de persoonlijke sleutel wordt uitgegaan van een gebruikersaccount is beschermd tegen ongewenste actoren en gaan sudo toegang zonder wachtwoord toestaan.  

### <a name="adding-a-single-sudo-user-to-an-azure-vm"></a>Een gebruiker één sudo toe te voegen aan een Azure VM
Aanmelden bij de virtuele machine in Azure met behulp van SSH-sleutels.  Als er geen installatie SSH openbare toegang tot de sleutel, eerst te voltooien in dit artikel [verificatie van openbare sleutel met Azure met behulp van](http://link.to/article).  

De `useradd` opdracht is voltooid de volgende taken:

* een nieuw gebruikersaccount maken
* Maak een nieuwe groep met dezelfde naam
* een lege vermelding toevoegen`/etc/passwd`
* een lege vermelding toevoegen`/etc/gpasswd`

De `-G` opdrachtregelprogramma vlag wordt het nieuwe gebruikersaccount toegevoegd aan de juiste Linux-groep geeft het nieuwe gebruikersaccount hoofdmap uitbreiding van bevoegdheden.

#### <a name="add-the-user"></a>De gebruiker toevoegen
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Een wachtwoord instellen
De `useradd` opdracht maakt u de gebruiker en wordt een vermelding toegevoegd aan beide `/etc/passwd` en `/etc/gpasswd` , maar het wachtwoord niet daadwerkelijk ingesteld.  Het wachtwoord wordt toegevoegd aan de vermelding met behulp van de `passwd` opdracht.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

We hebben nu een gebruiker met sudo-machtigingen op de server.

### <a name="add-your-ssh-public-key-to-the-new-user-account"></a>Uw openbare SSH-sleutel aan het nieuwe gebruikersaccount toevoegen
Gebruik van uw computer, de `ssh-copy-id` opdracht met het nieuwe wachtwoord.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-to-allow-sudo-usage-without-a-password"></a>Met behulp van visudo voor het gebruik van sudo zonder wachtwoord toestaan
Met behulp van `visudo` bewerken de `/etc/sudoers` bestand enkele lagen van bescherming tegen onjuist wijzigen van deze belangrijk bestand toegevoegd.  Bij het uitvoeren van `visudo`, wordt de `/etc/sudoers` bestand is vergrendeld zodat andere gebruikers geen wijzigingen kunt aanbrengen, terwijl deze actief wordt bewerkt.  De `/etc/sudoers` bestand ook gecontroleerd op fouten door `visudo` wanneer u probeert op te slaan of te sluiten, zodat u een verbroken sudoers-bestand niet opslaan.

Er bestaat reeds gebruikers in de juiste standaardgroep voor sudo-toegang.  Nu gaan we om in te schakelen die groepen sudo gebruiken zonder wachtwoord.

```bash
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-the-user-ssh-keys-and-sudo"></a>Controleer of de gebruiker de ssh-sleutels en sudo
```bash
# Verify the SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
