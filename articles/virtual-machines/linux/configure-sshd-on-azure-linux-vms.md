---
title: aaaConfigure SSHD op Azure Linux Virtual Machines | Microsoft Docs
description: Configureer SSHD voor aanbevolen beveiligingsprocedures en toolockdown SSH tooAzure virtuele Linux-Machines.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>SSHD op Azure Linux VM's configureren

Dit artikel laat zien hoe toolockdown SSH-Server op Linux-, tooprovide aanbevolen procedures voor beveiliging en ook toospeed up Hallo SSH-aanmelding Hallo met behulp van SSH-sleutels in plaats van wachtwoorden.  toofurther lockdown SSHD gaan we toodisable Hallo hoofdgebruiker kunnen toologin worden Hallo gebruikers beperken die toologin via een groepslijst met goedgekeurde zijn toegestaan voor het uitschakelen van SSH-protocolversie 1, een minimale sleutel bits instellen en configureren van automatische-Meld u af bij niet-actieve gebruikers.  Hallo-vereisten voor dit artikel zijn: een Azure-account ([ophalen van een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)) en [SSH openbare en persoonlijke sleutelbestanden](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Snelle opdrachten

Configureer `/etc/ssh/sshd_config` Hello volgende instellingen:

### <a name="disable-password-logins"></a>Wachtwoord aanmeldingen uitschakelen

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Aanmelding door Hallo hoofdgebruiker uitschakelen

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Groepslijst met toegestane

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Lijst met toegestane gebruikers

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>SSH-protocol versie 1 uitschakelen

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Minimale sleutel bits

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Verbreek de verbinding met niet-actieve gebruikers

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

SSHD is hello SSH-Server die wordt uitgevoerd op Hallo Linux VM.  SSH is een client die wordt uitgevoerd vanuit een shell op uw MacBook, Linux-werkstation of vanuit een Bash op Windows.  SSH is ook Hallo-protocol gebruikt toosecure en coderen Hallo uitgewisseld tussen uw werkstation en het Hallo Linux VM maken SSH ook een VPN (virtueel particulier netwerk).

Voor dit artikel is zeer belangrijk tookeep één aanmelding tooyour Linux-VM voor de volledige procedure Hallo openen.  Wanneer een SSH-verbinding is gemaakt, blijft deze als een geopende sessie, zolang het Hallo-venster niet is gesloten.  Met één terminal aangemeld, kunt u wijzigingen aangebracht toobe toohello SSHD service zonder dat ze worden geblokkeerd als een belangrijke wijziging wordt doorgevoerd.  Als u ophalen vergrendeld buiten uw Linux-VM met een verbroken SSHD configuratie, Azure biedt Hallo mogelijkheid tooreset een verbroken SSHD-configuratie met Hallo [Azure VM-extensie voor toegang tot](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Om deze reden openen we twee aansluitingen en SSH toohello Linux VM vanuit van beide.  We Hallo eerste terminal toomake Hallo wijzigingen tooSSHDs configuratiebestand gebruiken en Hallo SSHD-service opnieuw starten.  We gebruiken Hallo tweede terminal tootest die wordt gewijzigd nadat het Hallo-service opnieuw wordt gestart.  Omdat we bij het uitschakelen van SSH wachtwoorden afhankelijk strikt SSH-sleutels, als uw SSH-sleutels niet juist zijn en sluiten van Hallo verbinding toohello VM, hello VM wordt permanent vergrendeld en kan niemand zich kunnen toologin tooit verplicht stelt toobe verwijderd en opnieuw gemaakt.

## <a name="disable-password-logins"></a>Wachtwoord aanmeldingen uitschakelen

Hallo snelste manier toosecure u Linux VM toodisable wachtwoord aanmeldingen is.  Wanneer wachtwoord aanmeldingen zijn ingeschakeld, afdwingen bots verkennen Hallo web wordt direct gestart probeert toobrute raden Hallo wachtwoord voor uw Linux-VM met behulp van SSH.  Wachtwoord aanmeldingen volledig is uitgeschakeld, kunnen Hallo SSH server tooignore alle wachtwoord aanmeldingspogingen.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Aanmelding door Hallo hoofdgebruiker uitschakelen

Volgende aanbevolen procedures voor Linux hello `root` gebruiker moet nooit worden aangemeld via SSH of met behulp van `sudo su`.  Alle opdrachten die behoefte hebben aan machtigingen voor het niveau van hoofdmap moeten altijd worden uitgevoerd via Hallo `sudo` opdracht alle acties voor toekomstige controle registreert.  Uitschakelen Hallo `root` gebruiker aanmelden via SSH is een best practices beveiligingsstap die ervoor zorgt dat alleen geautoriseerde gebruikers tooSSH zijn toegestaan.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Groepslijst met toegestane

SSH biedt een methode voor het beperken van gebruikers en groepen die worden toegestaan of niet is toegestaan via SSH aanmelden.  Deze functie maakt gebruik van een lijst met tooapprove of specifieke gebruikers en groepen aanmelden weigeren.  Hallo wheel groep toohello instelling `AllowGroups` lijst met goedgekeurde aanmeldingen via SSH toojust gebruikersaccounts die in Hallo wheel groep beperkt.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Lijst met toegestane gebruikers

Beperken van de SSH-aanmeldingen toojust gebruikers is een meer specifiek manier tooaccomplish Hallo dezelfde taak die `AllowGroups` is.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>SSH-protocol versie 1 uitschakelen

SSH-protocolversie 1 is niet veilig en moet zijn uitgeschakeld.  SSH-protocolversie 2 is Hallo huidige versie een veilige manier tooSSH tooyour-server biedt.  Uitschakelen van versie 1 van SSH, weigert SSH-clients die tooestablish probeert een verbinding met de Hallo SSH-server met versie 1 van SSH.  Alleen versie 2-SSH-verbindingen zijn toegestaan toonegotiate een verbinding met de Hallo SSH-server.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Minimale sleutel bits

Aanbevolen beveiligingsprocedures wachtwoord SSH-aanmeldingen zijn uitgeschakeld en SSH-sleutels toobe tooauthenticate gebruikt met Hallo SSH-server zijn toegestaan.  Deze SSH-sleutels kunnen worden gemaakt met behulp van verschillende lengtes sleutels, gemeten in bits.  Aanbevolen procedures statussen dat sleutels van 2048 bits lang Hallo minimale acceptabele sleutelsterkte zijn.  Sleutels van minder dan 2048 bits kunnen theoretisch worden verbroken.  Instelling Hallo `ServerKeyBits` te`2048` staat verbindingen met behulp van de sleutels van 2048 bits of hoger en verbindingen van minder dan 2048 bits.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Verbreek de verbinding met niet-actieve gebruikers

SSH heeft Hallo mogelijkheid toodisconnect gebruikers die open verbinding die meer dan een ingestelde periode van seconden inactief zijn gebleven.  Open sessies tooonly houden die gebruikers die active limieten Hallo blootstelling van Hallo Linux VM zijn.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Opnieuw opstarten SSHD

instellingen voor tooenable Hallo in `/etc/ssh/sshd_config` hello SSHD proces opnieuw Hallo SSH-server opnieuw starten.  Hallo terminalvenster u toorestart Hallo SSH-server gebruiken zonder verlies van Hallo open SSH-sessie geopend blijven.  tootest hello nieuwe SSH-serverinstellingen gebruiken een tweede terminalvenster of tabblad.  Kunt u met behulp van een afzonderlijke terminal tootest Hallo SSH-verbinding toogo terug en controleer aanvullende wijzigingen toohello `/etc/ssh/sshd_config` in de eerste terminal Hallo zonder dat ze worden geblokkeerd door een recente SSHD wijziging.  

### <a name="on-redhat-centos-and-fedora"></a>Op Redhat, Centos en Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Op Debian en Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Opnieuw instellen van SSHD met behulp van Azure reset-toegang

Als u van een recente wijziging toohello SSHD configuratie zijn vergrendeld kunt u hello Azure VM-uitbreiding voor toegang tot tooreset hello SSHD configuratie back toohello oorspronkelijke configuratie.

Alle voorbeeldnamen vervangen door uw eigen.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Fail2ban installeren

Het is raadzaam tooinstall en setup Hallo open-source app Fail2ban, welke blokken herhaalde pogingen toologin tooyour Linux VM via SSH met brute kracht.  Fail2ban logboeken herhaalde pogingen toologin mislukt via SSH en maakt vervolgens firewallregels tooblock Hallo IP-adres dat Hallo pogingen afkomstig zijn uit.

* [Fail2ban startpagina](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Volgende stappen

Nu dat u hebt geconfigureerd en Hallo SSH-server op uw Linux-VM vergrendeld zijn er aanbevolen procedures voor extra beveiliging die kunt u volgen.  

* [Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Versleutelen van schijven op een Linux-VM met hello Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Toegang en beveiliging in Azure Resource Manager-sjablonen](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
