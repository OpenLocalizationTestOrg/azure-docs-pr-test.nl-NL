---
title: Gebruikersnamen voor Linux selecteren | Microsoft Docs
description: Informatie over het selecteren van gebruikersnamen voor een virtuele Linux-machine in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Gebruikersnamen selecteren voor Linux op Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Wanneer u een virtuele Linux-machine in Azure inrichten, moet u de naam van een niet-hoofdgebruiker die u later gebruiken kunt voor aanmelding bij de virtuele machine opgeven. U kunt de naam van de nieuwe gebruiker of als inrichting via de klassieke Azure portal kunt u de standaard de naam 'azureuser' accepteren.

In de meeste gevallen wordt deze gebruiker won't bestaan op de basisinstallatiekopie en tijdens het inrichtingsproces wordt gemaakt. Als de gebruiker op de basisinstallatiekopie van de virtuele machine bestaat, configureert de Azure Linux-agent gewoon vervolgens het wachtwoord en/of de SSH-sleutel voor die gebruiker op basis van de informatie die u hebt opgegeven bij het maken van de virtuele machine.

**Echter**, Linux definieert een set namen van gebruikers die niet worden gebruikt. Tijdens het inrichtingsproces wordt **mislukken** als u probeert te creëren van een Linux-VM met behulp van een bestaande systeemgebruiker, die is gedefinieerd als een gebruiker met UID 0 en 99 liggen. Een typisch voorbeeld is de `root` gebruiker UID 0 is.

* Zie ook: [Linux standaard Base - gebruiker-ID bereiken](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Hier volgt een lijst met algemene ingebouwd systeem-gebruikers voor CentOS en Ubuntu dat moet u niet gebruiken bij het inrichten van een virtuele Linux-machine in Azure. Deze lijst is slechts een voorbeeld, Raadpleeg de documentatie voor uw distributiepunt om ervoor te zorgen dat de gebruikersnaam die u ervoor kiezen geen met een bestaande gebruiker conflict.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* opslaglocatie
* cd-rom
* cgred
* daemon
* dbus
* bellen
* DIP
* schijf
* diskettestations
* FTP
* FTP
* games
* Gopher
* haldaemon
* is gestopt
* kmem
* vergrendelen
* LP
* E-mail
* Man
* geheugentoewijzing
* nfsnobody
* niemand
* NTP
* Operator
* oprofile
* postdrop
* postfix
* qpidd
* hoofdmap
* RPC
* rpcuser
* saslauth
* afsluiten
* slocate
* sshd
* stapdev
* stapusr
* Synchronisatie
* sys
* tape
* Test
* tcpdump
* TTY
* gebruikers
* utempter
* utmp
* uucp
* vcsa
* video
* Wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* Beheerder
* audio
* Back-up
* opslaglocatie
* cd-rom
* crontab
* daemon
* bellen
* DIP
* schijf
* Faxserver
* diskettestations
* integreert
* games
* gnats
* IRC
* kmem
* Liggend
* libuuid
* lijst
* LP
* E-mail
* Man
* MessageBus
* mlocate
* netdev
* Nieuws
* niemand
* nogroup
* Operator
* plugdev
* Proxy
* hoofdmap
* SASL
* Shadow
* src
* SSH
* sshd
* medewerkers
* sudo
* Synchronisatie
* sys
* syslog
* tape
* TTY
* gebruikers
* utmp
* uucp
* video
* Voice-over
* whoopsie
* www-gegevens

