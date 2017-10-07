---
title: aaaDisable SSH wachtwoorden op uw Linux-VM configureren SSHD | Microsoft Docs
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
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>SSH-wachtwoorden op uw Linux-VM uitschakelen door SSHD configureren
In dit artikel is gericht op het toolock omlaag Hallo aanmeldingsbeveiliging van uw Linux-VM.  Zodra de Hallo SSH-poort 22 wordt geopend start toohello world bots toologin probeert door te raden wachtwoorden.  Wat gebeurt in dit artikel is wachtwoord aanmeldingen via SSH uitschakelen.  Door het verwijderen van volledig Hallo mogelijkheid forceren toouse wachtwoorden we Hallo Linux VM beschermen tegen brute dit type aanval.  Hallo toegevoegd extra is we Linux SSHD tooonly toestaan configureert veel Hallo veiligste manier toologin tooLinux aanmeldingen via SSH openbare en persoonlijke sleutels.  Hallo mogelijke combinaties van deze vereist tooguess Hallo persoonlijke sleutel is enorme en daarom raadt af bots van zelfs proberen alles tootry toobrute force SSH-sleutels.

## <a name="goals"></a>Doelstellingen
* SSHD toodisallow configureren:
  * Wachtwoord aanmeldingen
  * Hoofdmap gebruikersaanmelding
  * Vraag en antwoord-verificatie
* SSHD tooallow configureren:
  * alleen sleutel SSH aanmeldingen
* Opnieuw opstarten SSHD terwijl u nog steeds bent aangemeld
* Test Hallo nieuwe SSHD configuratie

## <a name="introduction"></a>Inleiding
[SSH gedefinieerd](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD is hello SSH-Server die wordt uitgevoerd op Hallo Linux VM.  SSH is een client die op een shell op uw werkstation MacBook- of Linux wordt uitgevoerd.  SSH is ook Hallo-protocol gebruikt toosecure en Hallo uitgewisseld tussen uw werkstation en het Hallo Linux VM versleutelen.

Voor dit artikel is zeer belangrijk tookeep één aanmelding tooyour Linux VM geopend voor de hele Hallo doorlopen.  Om deze reden wordt we twee aansluitingen en SSH toohello Linux VM openen vanuit van beide.  We Hallo eerste terminal toomake Hallo wijzigingen tooSSHDs configuratiebestand gebruiken en Hallo SSHD-service opnieuw starten.  We gebruiken Hallo tweede terminal tootest die wordt gewijzigd nadat het Hallo-service opnieuw wordt gestart.  Omdat we bij het uitschakelen van SSH wachtwoorden afhankelijk strikt SSH-sleutels, als uw SSH-sleutels niet juist zijn en sluiten van Hallo verbinding toohello VM, hello VM wordt permanent vergrendeld en kan niemand zich kunnen toologin tooit verplicht stelt toobe verwijderd en opnieuw gemaakt.

## <a name="prerequisites"></a>Vereisten
* [SSH-sleutels maken in Linux en Mac voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Azure-account
  * [gratis proefversie te registreren](https://azure.microsoft.com/pricing/free-trial/)
  * [Azure Portal](http://portal.azure.com)
* Linux-VM uitgevoerd op azure
* SSH openbare sleutelpaar in`~/.ssh/`
* Openbare SSH-sleutel in `~/.ssh/authorized_keys` op Hallo Linux VM
* Sudo-rechten op Hallo VM
* Poort 22 openen

## <a name="quick-commands"></a>Snelle opdrachten
*Doorgewinterde Linux-beheerders die Hallo TLDR versie begint u hier.  Voor alle andere Hallo wil overslaan gedetailleerde uitleg en doorloop in deze sectie.*

```bash
sudo vim /etc/ssh/sshd_config
```

Hallo-configuratiebestand als volgt bewerken:

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Hallo SSHD service opnieuw starten. Op op basis van Debian distributies:

```bash
sudo service ssh restart
```

Op op basis van Red Hat distributies:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Gedetailleerde Doorloop
Aanmelding toohello Linux VM op terminal 1 (T1).  Aanmelding toohello Linux VM op terminal 2 (T2).

Op tijdstip T2 gaan we tooedit hello SSHD-configuratiebestand.  

```bash
sudo vim /etc/ssh/sshd_config
```

Hier wordt alleen Hallo instellingen toodisable wachtwoorden bewerken en SSH-sleutel aanmeldingen inschakelen.  Er zijn veel instellingen in dit bestand dat u moet onderzoeken en toomake Linux & SSH zo veilig naar wens wijzigen.

#### <a name="disable-password-logins"></a>Wachtwoord aanmeldingen uitschakelen

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Verificatie van openbare sleutels inschakelen

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Hoofdmap aanmelding uitschakelen

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Vraag en antwoord-verificatie uit te schakelen
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Opnieuw opstarten SSHD
Controleer of dat u nog steeds bent aangemeld vanuit Hallo T1-shell.  Dit is essentieel zodat u bent niet toegang buiten uw virtuele machine als uw SSH-sleutels niet correct zijn omdat wachtwoorden zijn nu uitgeschakeld.  Als u alle instellingen zijn onjuist op uw Linux-VM kunt u T1 toofix sshd_config als u nog steeds wordt vastgelegd in en SSH Hallo verbinding actief tijdens Hallo SSHD-service houden wordt opnieuw starten.

Van T2 uitvoeren:

##### <a name="on-hello-debian-family"></a>Op Hallo Debian-familie
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>Op Hallo RedHat familie
```bash
sudo service sshd restart
```

Wachtwoorden zijn nu uitgeschakeld op de virtuele machine die beschermt tegen beveiligingsaanvallen wachtwoord aanmeldingspogingen.  U kunt toologin sneller en veel veiligere worden met alleen de SSH-sleutels toegestaan.

