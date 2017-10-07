---
title: aaaSelecting gebruikersnamen voor Linux | Microsoft Docs
description: Meer informatie over hoe de namen van tooselect gebruiker voor een virtuele Linux-machine in Azure.
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
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Gebruikersnamen selecteren voor Linux op Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Wanneer u een virtuele Linux-machine in Azure inricht, kunt u Hallo-naam van een niet-hoofdgebruiker waarmee u later toolog in Hallo VM kunt moet opgeven. U kunt ervoor kiezen de naam van de nieuwe gebruiker Hallo Hallo of als inrichting via Hallo klassieke Azure-portal kunt u accepteren Hallo standaard de naam 'azureuser'.

In de meeste gevallen wordt deze gebruiker op Hallo basisinstallatiekopie won't bestaan en wordt gemaakt tijdens het inrichtingsproces Hallo. Als gebruiker Hallo op Hallo basisinstallatiekopie VM bestaat, configureert hello Azure Linux agent gewoon vervolgens Hallo wachtwoord en/of SSH-sleutel voor die gebruiker op basis van Hallo informatie die u hebt opgegeven bij het maken van Hallo VM.

**Echter**, Linux definieert een set namen van gebruikers die niet worden gebruikt. Hallo inrichting proces wordt **mislukken** als u probeert tooprovision een Linux-VM met behulp van een bestaande systeemgebruiker, die is gedefinieerd als een gebruiker met UID 0 en 99 liggen. Een typisch voorbeeld is Hallo `root` gebruiker UID 0 is.

* Zie ook: [Linux standaard Base - gebruiker-ID bereiken](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Hallo Hieronder volgt een lijst met algemene ingebouwd systeem-gebruikers voor CentOS en Ubuntu dat moet u niet gebruiken bij het inrichten van een virtuele Linux-machine in Azure. Deze lijst is slechts een voorbeeld, raadpleegt u toohello-documentatie voor uw tooensure distributie die u niet in conflict met een bestaande systeemgebruiker Hallo-gebruikersnaam.

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

