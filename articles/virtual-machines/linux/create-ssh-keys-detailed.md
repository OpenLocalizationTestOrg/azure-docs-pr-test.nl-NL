---
title: aaaDetailed stappen toocreate een SSH-sleutelpaar voor virtuele Linux-machines in Azure | Microsoft Docs
description: Informatie over extra stappen toocreate de openbare en persoonlijke sleutelpaar voor een SSH voor virtuele Linux-machines in Azure, samen met specifieke certificaten voor verschillende gebruiksscenario.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Gedetailleerde doorloop toocreate een SSH-sleutelpaar en extra certificaten voor een Linux-VM in Azure
U kunt virtuele Machines in Azure die standaard toousing SSH-sleutels voor verificatie, hoeft u Hallo wachtwoorden toolog in maken met een SSH-sleutelpaar. Wachtwoorden kunnen worden geraden en uw wachtwoord voor uw virtuele machines van toorelentless brute kracht aanvallen tooguess openen. Virtuele machines die zijn gemaakt met hello Azure CLI of Resource Manager-sjablonen kunnen uw openbare SSH-sleutel als onderdeel van Hallo-implementatie, het verwijderen van een post-implementatie stap in de configuratie van het wachtwoord aanmeldingen uitschakelen voor SSH bevatten. Dit artikel vindt gedetailleerde stappen en aanvullende voorbeelden gegeven van certificaten genereren, zoals voor gebruik met de virtuele Linux-machines. Als u tooquickly wilt maken en gebruiken van een SSH-sleutelpaar, Zie [hoe toocreate een SSH-sleutel voor openbare en persoonlijke koppelen voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md).

## <a name="understanding-ssh-keys"></a>Inzicht in SSH-sleutels

Met behulp van SSH openbare en persoonlijke sleutels is Hallo gemakkelijkste manier toolog in tooyour Linux-servers. [Cryptografie met openbare sleutels](https://en.wikipedia.org/wiki/Public-key_cryptography) biedt een veel veiligere manier toolog in tooyour Linux- of BSD VM in Azure dan wachtwoorden, die brute-geforceerde aanzienlijk eenvoudiger worden kunnen.

Uw openbare sleutel kan worden gedeeld met iedereen, maar alleen u (of uw lokale beveiligingsinfrastructuur) beschikt over uw persoonlijke sleutel.  persoonlijke Hallo SSH-sleutel moet een [zeer beveiligd wachtwoord](https://www.xkcd.com/936/) (bron:[xkcd.com](https://xkcd.com)) toosafeguard deze.  Dit wachtwoord wordt alleen tooaccess Hallo persoonlijke SSH-sleutelbestand en **is niet** Hallo het wachtwoord voor gebruikersaccount.  Wanneer u een wachtwoord tooyour SSH-sleutel toevoegt, gecodeerd Hallo persoonlijke sleutel met AES 128-bits, zodat hello persoonlijke sleutel zonder Hallo wachtwoord toodecrypt onbruikbaar is wordt.  Als een aanvaller stelen van uw persoonlijke sleutel en dat sleutel heeft geen een wachtwoord, is ze zou kunnen toouse dat persoonlijke sleutel toolog in tooany servers waarop de bijbehorende openbare sleutel Hallo.  Als een persoonlijke sleutel is beveiligd met een wachtwoord, kan deze niet worden gebruikt door de aanvaller. Zo beschikt u over een extra beveiligingslaag voor uw infrastructuur in Azure.

In dit artikel maakt een SSH-protocolversie 2 RSA openbare en persoonlijke sleutelbestand paar (ook waarnaar wordt verwezen tooas 'ssh-rsa' sleutels), wordt aanbevolen voor implementaties met Azure Resource Manager. *SSH-rsa* sleutels zijn vereist op Hallo [portal](https://portal.azure.com) voor zowel klassieke implementaties van Resource Manager.

## <a name="ssh-keys-use-and-benefits"></a>Gebruik en voordelen van SSH-sleutels

Azure vereist ten minste 2048 bits SSH-protocol versie 2 RSA-indeling openbare en persoonlijke sleutels; Hallo-bestand met openbare sleutel heeft Hallo `.pub` containerindeling. Hallo toocreate sleutels gebruik `ssh-keygen`, die een reeks vragen en schrijft u een persoonlijke sleutel en een overeenkomende openbare sleutel. Wanneer een Azure VM is gemaakt, Azure kopieën openbare sleutel toohello Hallo `~/.ssh/authorized_keys` map op Hallo VM. SSH-sleutels in `~/.ssh/authorized_keys` gebruikte toochallenge Hallo client toomatch Hallo bijbehorende persoonlijke sleutel van een SSH-aanmelding verbinding zijn.  Wanneer een virtuele machine van Azure Linux is gemaakt met behulp van SSH-sleutels voor verificatie, Azure Hallo SSHD configureert server toonot toestaan wachtwoord aanmeldingen, SSH-sleutels.  Daarom maakt Azure Linux VM's met SSH-sleutels, kunt u helpen beveiligen Hallo VM-implementatie en besparen Hallo standaardconfiguratie na de implementatie stap van het uitschakelen van wachtwoorden in Hallo **sshd_config** bestand.

## <a name="using-ssh-keygen"></a>ssh-keygen gebruiken

Deze opdracht maakt u een wachtwoord beveiligd (versleuteld) SSH-sleutelpaar met 2048-bits RSA en deze opmerkingen tooeasily worden geïdentificeerd.  

SSH sleutels zijn standaard bewaard in Hallo `~/.ssh` directory.  Als u nog geen een `~/.ssh` directory, Hallo `ssh-keygen` opdracht maakt het voor u Hello juiste machtigingen.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*Uitleg van de opdracht*

`ssh-keygen`Hallo programma gebruikt toocreate Hallo sleutels =

`-t rsa`= type sleutel toocreate Hallo RSA-indeling [wikipedia][parens aan einde](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = aantal bits van Hallo-sleutel

`-C "azureuser@myserver"`= een opmerking toegevoegde toohello einde van Hallo openbaar-sleutelbestand tooeasily worden geïdentificeerd.  Normaal gesproken een e-mailbericht wordt gebruikt als Hallo Opmerking maar kunt u wat het beste werkt voor uw infrastructuur.

## <a name="classic-deploy-using-asm"></a>Klassieke implementatie met behulp van`asm`

Als u van het klassieke implementatiemodel hello gebruikmaakt (`asm` modus in Hallo CLI), kunt u een openbare SSH-RSA-sleutel of een RFC4716 geformatteerd sleutel in een pem-container.  openbare sleutel voor SSH-RSA Hallo is wat eerder in dit artikel met behulp van is gemaakt `ssh-keygen`.

een RFC4716 toocreate ingedeeld sleutel van een bestaande openbare SSH-sleutel:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Voorbeeld van ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Opgeslagen sleutelbestanden:

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

Hallo sleutelpaar naam voor dit artikel.  Een sleutelpaar met de naam **id_rsa** is Hallo standaard en een aantal hulpprogramma's verwachten mogelijk Hallo **id_rsa** persoonlijke sleutelbestand naam dus is het een goed idee. Hallo directory `~/.ssh/` is de standaardlocatie Hallo voor SSH-sleutelparen en Hallo SSH-configuratiebestand.  Als niet wordt opgegeven met een volledig pad `ssh-keygen` Hallo sleutels maakt in Hallo huidige werkmap, niet de standaard Hallo `~/.ssh`.

Een lijst met Hallo `~/.ssh` directory.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

Sleutelwachtwoord:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`tooa wachtwoord verwezen voor persoonlijke sleutelbestand Hallo als 'een wachtwoordzin.'  Het is *sterk* tooadd aanbevolen een wachtwoord tooyour persoonlijke sleutel. Zonder een wachtwoord beschermen Hallo sleutelbestand, kunt iedereen met Hallo bestand gebruiken toolog in tooany-server die de bijbehorende openbare sleutel Hallo heeft. Toevoegen van een wachtwoord (wachtwoordzin) biedt meer beveiliging voor het geval iemand kunnen toogain toegang tooyour persoonlijke sleutelbestand is, krijgt u tijd toochange Hallo sleutels gebruikt tooauthenticate u.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Het wachtwoord van uw persoonlijke sleutel met behulp van ssh-agent toostore

Typ uw wachtwoord persoonlijke sleutelbestand bij elke SSH-aanmelding tooavoid kunt u `ssh-agent` toocache uw persoonlijke sleutelbestand wachtwoord. Als u een Mac OSX-sleutelketen Hallo Hallo persoonlijke sleutels, wachtwoorden veilig opslaat wanneer u aanroept `ssh-agent`.

Controleren en gebruiken van ssh-agent en ssh-toevoegen tooinform Hallo SSH systeem over Hallo sleutelbestanden zodat Hallo wachtwoordzin niet toobe interactief gebruikt hoeven.

```bash
eval "$(ssh-agent -s)"
```

Nu de persoonlijke sleutel hello te toevoegen`ssh-agent` met Hallo opdracht `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Hallo-wachtwoord voor persoonlijke sleutel wordt nu opgeslagen in `ssh-agent`.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>Met behulp van `ssh-copy-id` toocopy Hallo sleutel tooan bestaande VM
Als u al een virtuele machine hebt gemaakt kunt u Hallo nieuwe SSH openbare sleutel tooyour Linux VM installeren met:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Een SSH-configuratiebestand maken en configureren

Het is een aanbevolen best practice toocreate en configureer een `~/.ssh/config` bestand toospeed up aanmeldingen en voor het optimaliseren van het gedrag van uw SSH-client.

Hallo volgende voorbeeld wordt een standaardconfiguratie getoond.

### <a name="create-hello-file"></a>Hallo-bestand maken

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Hallo bestand tooadd Hallo nieuwe SSH-configuratie bewerken:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Voorbeeld van `~/.ssh/config`-bestand:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Deze SSH-configuratie kunt u secties voor elke server tooenable elke toohave zijn eigen toegewezen sleutelpaar. Hallo standaardinstellingen (`Host *`) zijn voor alle hosts die niet overeenkomen met de Hallo specifieke hosts hoger staan in het Hallo-configuratiebestand.

### <a name="config-file-explained"></a>Uitleg van configuratiebestand

`Host`= Hallo-naam van Hallo-host wordt aangeroepen op Hallo terminal.  `ssh fedora22`vertelt `SSH` toouse Hallo waarden in Hallo instellingenblok met het label `Host fedora22` Opmerking: Host mag een label dat logisch is voor uw gebruik en vertegenwoordigt geen Hallo werkelijke hostnaam van een server.

`Hostname 102.160.203.241`= Hallo IP-adres of de DNS-naam voor het Hallo-server die wordt geopend.

`User ahmet`Hallo externe gebruiker account toouse = bij het aanmelden toohello-server.

`PubKeyAuthentication yes`= vertelt SSH in de gewenste toouse een SSH-sleutel toolog.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= persoonlijke Hallo SSH-sleutel en de bijbehorende openbare sleutel toouse voor verificatie.

## <a name="ssh-into-linux-without-a-password"></a>SSH in Linux zonder een wachtwoord

Nu u een SSH-sleutelpaar en een geconfigureerd SSH-configuratiebestand hebt, bent u kunnen toolog in tooyour Linux VM snel en veilig. Hallo eerste keer dat u zich aanmelden met behulp van de opdrachtprompts van een SSH-sleutel Hallo tooa-server u voor Hallo wachtwoordzin voor dat sleutelbestand.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Uitleg van de opdracht

Wanneer `ssh fedora22` wordt uitgevoerd SSH eerst zoekt en laadt u de instellingen van Hallo `Host fedora22` blok en laadt het vervolgens alle resterende instellingen van het laatste blok, Hallo Hallo `Host *`.

## <a name="next-steps"></a>Volgende stappen

Naast up toocreate Azure Linux VM's gebruikt Hallo nieuwe openbare SSH-sleutel.  Azure virtuele machines die zijn gemaakt met een openbare SSH-sleutel als Hallo aanmelding zijn beter beveiligd dan virtuele machines die zijn gemaakt met de Hallo aanmelding standaardmethode wachtwoorden.  Virtuele Azure-machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden uitgeschakeld, waarmee brute force-aanvallen om wachtwoorden te raden worden voorkomen.

* [Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Maak een beveiligde Linux-VM met hello Azure-portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Maak een beveiligde Linux VM hello Azure CLI gebruiken](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
