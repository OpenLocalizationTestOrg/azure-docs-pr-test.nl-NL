---
title: aaaUpdate hello Azure Linux Agent vanuit GitHub | Microsoft Docs
description: Meer informatie over hoe tooupdate Azure Linux Agent voor uw Linux-VM in Azure toohello meest recente versie van GitHub
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Hoe tooupdate hello Azure Linux Agent op een virtuele machine

tooupdate uw [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) op een Linux-VM in Azure, moet u al hebben:

- Een actieve Linux VM in Azure.
- Een verbinding toothat Linux VM via SSH.

U moet altijd eerst in voor een pakket in Hallo Linux distro opslagplaats. Het is mogelijk Hallo pakket beschikbaar mogelijk niet de nieuwste versie Hallo, echter inschakelen autoupdate waarborgt Hallo Linux-Agent altijd de meest recente update Hallo krijgen. Hebt u problemen met het installeren van Hallo pakket managers, moet u ondersteuning van Hallo distro leverancier zoeken.

## <a name="updating-hello-azure-linux-agent"></a>Hello Azure Linux Agent bijwerken

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Update-pakket-cache

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hallo waagent-service opnieuw starten

#### <a name="restart-agent-for-1404"></a>Agent opnieuw starten om 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Agent opnieuw starten om 16.04 / 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 'Wheezy'

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Update-pakket-cache

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Agent automatisch bijwerken inschakelen
Deze versie van Debian beschikt niet over een versie > = 2.0.16, automatisch bijwerken is daarom niet beschikbaar. Hallo-uitvoer van Hallo hierboven opdracht ziet u als Hallo-pakket bijgewerkt is.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 'Jessie' / Debian 9 'Stretch'

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Update-pakket-cache

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld 

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hallo waagent-service opnieuw starten

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>RedHat / CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Beschikbare updates controleren

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld 

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hallo waagent-service opnieuw starten

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Beschikbare updates controleren

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld 

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hallo waagent-service opnieuw starten

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Beschikbare updates controleren

Hallo bovenstaande uitvoer ziet u als toodate Hallo-pakket is.

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld 

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hallo waagent-service opnieuw starten

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Controleer uw huidige Pakketversie

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Beschikbare updates controleren

In de uitvoer van de bovenstaande Hallo Hallo ziet hier u als Hallo pakket maximaal datum is.

#### <a name="install-hello-latest-package-version"></a>Installeer de meest recente Pakketversie Hallo

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld 

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hallo waagent-service opnieuw starten

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 en 7

Oracle Linux, zorg ervoor dat Hallo `Addons` opslagplaats is ingeschakeld. Kies tooedit Hallo bestand `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) of `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), en wijzig Hallo regel `enabled=0` te`enabled=1` onder **[ol6_addons]** of **[ol7_addons]** in dit bestand.

Vervolgens tooinstall Hallo meest recente versie van hello Azure Linux Agent, type:

```bash
sudo yum install WALinuxAgent
```

Als u niet kunt Hallo invoegtoepassing opslagplaats vinden kunt u deze regels kunt gewoon op Hallo einde van uw .repo bestand volgens tooyour Oracle Linux release toevoegen:

Voor Oracle Linux 6 virtuele machines:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Voor Oracle Linux 7 virtuele machines:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Typ vervolgens:

```bash
sudo yum update WALinuxAgent
```

Dit is normaal alles wat die u nodig hebt, maar als voor een bepaalde reden moet u tooinstall uit https://github.com rechtstreeks gebruik hello te volgen stappen.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Hallo Linux-Agent bijwerken wanneer er geen agentpakket voor distributie bestaat

Wget (Er zijn een aantal distributies dat niet het standaard, zoals Redhat en CentOS, Oracle Linux versies, 6.4 en 6.5) installeren door te typen `sudo yum install wget` op Hallo-opdrachtregel.

### <a name="1-download-hello-latest-version"></a>1. Download de nieuwste versie Hallo
Open [Hallo release van Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in een webpagina en uitzoeken Hallo-nummer voor meest recente versie. (U kunt uw huidige versie vinden door te typen `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Voor versie 2.2.x of hoger, typ:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Hallo wordt volgende regel versie 2.2.0 als voorbeeld gebruikt:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Hello Azure Linux Agent installeren

#### <a name="for-version-22x-use"></a>Voor versie 2.2.x, gebruiken:
Mogelijk moet u tooinstall Hallo pakket `setuptools` eerst--Zie [hier](https://pypi.python.org/pypi/setuptools). Voer vervolgens:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Zorg ervoor dat automatische updates is ingeschakeld

Controleer eerst toosee als deze is ingeschakeld:

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled' vinden. Als u deze uitvoer ziet, is het ingeschakeld:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable uitvoeren:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Hallo waagent-service opnieuw starten
Voor het merendeel van Linux-distributies:

```bash
sudo service waagent restart
```

Ubuntu, gebruikt u in:

```bash
sudo service walinuxagent restart
```

Voor virtuele CoreOS, gebruiken:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Hello Azure Linux Agent versie bevestigen
    
```bash
waagent -version
```

Voor virtuele CoreOS, Hallo hierboven opdracht werkt mogelijk niet.

U ziet dat hello Azure Linux Agent versie is bijgewerkt toohello nieuwe versie.

Zie voor meer informatie over hello Azure Linux Agent [Azure Linux Agent Leesmij](https://github.com/Azure/WALinuxAgent).
