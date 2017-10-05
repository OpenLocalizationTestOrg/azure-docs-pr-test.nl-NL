---
title: SSH-wachtwoorden op uw Linux-VM uitschakelen door het configureren van SSHD | Microsoft Docs
description: Beveilig uw Linux-VM op Azure door wachtwoord aanmeldingen voor SSH uit te schakelen.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>SSH-wachtwoorden op uw Linux-VM uitschakelen door SSHD configureren
In dit artikel is gericht op het vergrendelen van de beveiliging van de aanmelding van de Linux-VM.  Zodra de SSH-poort 22 wordt geopend op het world bots begin probeert door te raden wachtwoorden aanmelden.  Wat gebeurt in dit artikel is wachtwoord aanmeldingen via SSH uitschakelen.  Door het volledig verwijderen van de mogelijkheid om wachtwoorden te gebruiken beveiligen we de Linux-VM van dit type beveiligingsaanval.  Bijkomend voordeel is dat we Linux SSHD zodat alleen aanmeldingen via SSH openbare en persoonlijke sleutels voor aanmelding bij Linux veel de veiligste manier configureert.  De mogelijke combinaties van deze vereist te raden de persoonlijke sleutel is enorme en daarom raadt af bots van zelfs proberen alles uit te proberen te beveiligingsaanvallen SSH-sleutels.

## <a name="goals"></a>Doelstellingen
* Configureer SSHD om te blokkeren:
  * Wachtwoord aanmeldingen
  * Hoofdmap gebruikersaanmelding
  * Vraag en antwoord-verificatie
* Configureer SSHD om toe te staan:
  * alleen sleutel SSH aanmeldingen
* Opnieuw opstarten SSHD terwijl u nog steeds bent aangemeld
* De configuratie van de nieuwe SSHD testen

## <a name="introduction"></a>Inleiding
[SSH gedefinieerd](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD is de SSH-Server die wordt uitgevoerd op de Linux-VM.  SSH is een client die op een shell op uw werkstation MacBook- of Linux wordt uitgevoerd.  SSH is ook het protocol dat wordt gebruikt voor het beveiligen en de communicatie tussen uw werkstation en de Linux-VM te versleutelen.

Voor dit artikel is zeer belangrijk dat openen één aanmelding bij uw Linux-VM voor de hele doorlopen.  Om deze reden wordt we twee aansluitingen en SSH voor Linux VM openen vanuit een van beide.  De eerste terminal zullen worden gebruikt voor de wijzigingen aanbrengen in het configuratiebestand SSHDs en start de service SSHD.  De tweede terminal zullen worden gebruikt voor het testen van deze wijzigingen zodra de service is gestart.  Omdat we bij het uitschakelen van SSH wachtwoorden afhankelijk strikt SSH-sleutels, als uw SSH-sleutels niet juist zijn en sluiten van de verbinding met de virtuele machine, de virtuele machine wordt permanent vergrendeld en kan niemand zich kunnen aanmelden bij deze verplicht stelt worden verwijderd en opnieuw gemaakt.

## <a name="prerequisites"></a>Vereisten
* [SSH-sleutels maken in Linux en Mac voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Azure-account
  * [gratis proefversie te registreren](https://azure.microsoft.com/pricing/free-trial/)
  * [Azure Portal](http://portal.azure.com)
* Linux-VM uitgevoerd op azure
* SSH openbare sleutelpaar in`~/.ssh/`
* Openbare SSH-sleutel in `~/.ssh/authorized_keys` op de Linux-VM
* Sudo-rechten op de virtuele machine
* Poort 22 openen

## <a name="quick-commands"></a>Snelle opdrachten
*Doorgewinterde Linux Admins die de versie TLDR begint u hier.  Voor alle andere wil de gedetailleerde uitleg en doorloop deze sectie met overslaan.*

```bash
sudo vim /etc/ssh/sshd_config
```

Bewerk het configuratiebestand wordt als volgt:

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

Start de service SSHD. Op op basis van Debian distributies:

```bash
sudo service ssh restart
```

Op op basis van Red Hat distributies:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Gedetailleerde Doorloop
Meld u aan de Linux-VM op terminal 1 (T1).  Meld u aan de Linux-VM op terminal 2 (T2).

Op tijdstip T2 gaan we het configuratiebestand SSHD bewerken.  

```bash
sudo vim /etc/ssh/sshd_config
```

Hier bewerken we alleen de instellingen voor het uitschakelen van wachtwoorden en SSH-sleutel aanmeldingen inschakelen.  Er zijn veel instellingen in dit bestand waarin u moet onderzoeken en wijzigt u Linux & SSH als beveiligen als u nodig hebt.

#### <a name="disable-password-logins"></a>Wachtwoord aanmeldingen uitschakelen

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Verificatie van openbare sleutels inschakelen

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Hoofdmap aanmelding uitschakelen

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Vraag en antwoord-verificatie uit te schakelen
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Opnieuw opstarten SSHD
Op de shell T1 controleren dat u nog steeds bent aangemeld.  Dit is essentieel zodat u bent niet toegang buiten uw virtuele machine als uw SSH-sleutels niet correct zijn omdat wachtwoorden zijn nu uitgeschakeld.  Als u alle instellingen zijn onjuist op uw Linux-VM kunt u T1 om op te lossen sshd_config als u nog steeds wordt vastgelegd in en SSH de verbinding actief tijdens de service SSHD houden wordt start opnieuw op.

Van T2 uitvoeren:

##### <a name="on-the-debian-family"></a>Op de Debian-familie
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a>Op de familie RedHat
```bash
sudo service sshd restart
```

Wachtwoorden zijn nu uitgeschakeld op de virtuele machine die beschermt tegen beveiligingsaanvallen wachtwoord aanmeldingspogingen.  Toegestaan dat kunt u zich aanmelden sneller en veel veiligere met alleen de SSH-sleutels.

