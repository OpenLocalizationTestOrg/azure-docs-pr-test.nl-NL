---
title: aaaSet van MySQL op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall Hallo MySQL stack is op een virtuele Linux-machine (Ubuntu of RedHat familie OS) in Azure
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Hoe tooinstall MySQL in Azure
In dit artikel leert u hoe tooinstall en MySQL configureren op een virtuele machine van Azure waarop Linux wordt uitgevoerd.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>MySQL installeren op de virtuele machine
> [!NOTE]
> U moet al een Microsoft Azure virtuele machine waarop Linux wordt uitgevoerd in de volgorde toocomplete in deze zelfstudie hebben. Zie de [Azure Linux VM-zelfstudie](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate en instellen van een Linux-VM met `mysqlnode` als Hallo VM-naam en `azureuser` als gebruiker voordat u doorgaat.
> 
> 

In dit geval 3306 poort gebruiken als Hallo MySQL-poort.  

Verbinding maken met toohello Linux VM u via de putty hebt gemaakt. Als dit Hallo eerste keer dat u Azure Linux VM gebruikt, Zie hoe toouse putty verbinding tooa Linux VM [hier](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

We gebruiken opslagplaats pakket tooinstall MySQL5.6 als voorbeeld in dit artikel. MySQL5.6 heeft eigenlijk meer verbetering in prestaties dan MySQL5.5.  Meer informatie [hier](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Hoe tooinstall MySQL5.6 op Ubuntu
We gebruiken Linux VM hier met Ubuntu van Azure.

* Stap 1: Installeer MySQL Server 5.6 te schakelen`root` gebruiker:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Mysql-server 5.6 installeren:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Tijdens de installatie, ziet u een dialoogvenster venster poping up tooask u tooset MySQL hoofdwachtwoord hieronder, en u moet Hallo hier wachtwoord instelt.
  
    ![Afbeelding](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Invoer Hallo wachtwoord opnieuw tooconfirm.

    ![Afbeelding](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Stap 2: Aanmelding MySQL-Server
  
    Wanneer de installatie van de MySQL-server is voltooid, wordt MySQL-service automatisch gestart. U kunt zich aanmelden MySQL-Server met `root` gebruiker.
    Hallo onderstaande opdracht toologin en invoer wachtwoord gebruiken.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Stap 3: Beheren Hallo MySQL-service wordt uitgevoerd
  
    (a) de status van MySQL-service ophalen
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) MySQL-Service starten
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) MySQL-service stoppen
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) Hallo MySQL-service opnieuw starten
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Hoe tooinstall MySQL op Red Hat OS-familie, zoals CentOS, Oracle Linux
We gebruiken Linux VM hier met de CentOS, Oracle Linux.

* Stap 1: Toevoegen Hallo MySQL Yum opslagplaats Switch te`root` gebruiker:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Download en installeer Hallo MySQL releasepakket:
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Stap 2: Hieronder bestand tooenable Hallo MySQL opslagplaats voor het downloaden van het Hallo MySQL5.6 pakket bewerken
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Elke waarde van dit bestand toobelow bijwerken:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Stap 3: Installatie MySQL van MySQL-opslagplaats MySQL installeren:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    MySQL-RPM-pakket en alle gerelateerde pakketten worden geïnstalleerd.
* Stap 4: Beheren Hallo MySQL-service wordt uitgevoerd
  
    (a) Controleer de servicestatus Hallo van Hallo MySQL-server:
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) Controleer of de poort van MySQL standaardserver Hallo actief is:
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) Hallo MySQL-server niet starten:

           #[root@mysqlnode ~]#service mysqld start

    (d) stoppen Hallo MySQL-server:

           #[root@mysqlnode ~]#service mysqld stop

    (e) MySQL toostart instellen als Hallo system boot-up:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Hoe tooinstall MySQL in SUSE Linux
We gebruiken Linux VM hier met OpenSUSE.

* Stap 1: Download en installeer MySQL-Server
  
    Switch te`root` gebruiker via de onderstaande opdracht:  
  
           #sudo su -
  
    Download en installeer MySQL pakket:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Stap 2: Beheren Hallo MySQL-service wordt uitgevoerd
  
    (a) Hallo status controleren van Hallo MySQL-server:
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) Controleer of Hallo standaardpoort Hallo MySQL-server:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) Hallo MySQL-server niet starten:

           #[root@mysqlnode ~]# rcmysql start

    (d) stoppen Hallo MySQL-server:

           #[root@mysqlnode ~]# rcmysql stop

    (e) MySQL toostart instellen als Hallo system boot-up:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Volgende stap
Meer informatie over het gebruik en informatie met betrekking tot MySQL vinden [hier](https://www.mysql.com/).

