---
title: Hoofdmap bevoegdheden gebruiken op virtuele Linux-machines | Microsoft Docs
description: Informatie over het gebruik van root-bevoegdheden op een virtuele Linux-machine in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Bevoegdheden op hoofdniveau gebruiken op virtuele Linux-machines in Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Standaard de `root` gebruiker is uitgeschakeld op Linux virtuele machines in Azure. Gebruikers kunnen opdrachten uitvoeren met verhoogde bevoegdheden met behulp van de `sudo` opdracht. De ervaring kan echter variëren afhankelijk van hoe het systeem is ingericht.

1. **SSH-sleutel en het wachtwoord of wachtwoord alleen** -de virtuele machine is ingericht met ofwel een certificaat (`.CER` bestand) of SSH-sleutel, evenals een wachtwoord, of alleen een gebruikersnaam en wachtwoord. In dit geval `sudo` voor het wachtwoord van de gebruiker wordt gevraagd voordat de opdracht wordt uitgevoerd.
2. **SSH-sleutel** -de virtuele machine is ingericht met een certificaat (`.cer`, `.pem`, of `.pub` bestand) of SSH-sleutel, maar er is geen wachtwoord.  In dit geval `sudo` **niet** vragen om het wachtwoord van de gebruiker voordat de opdracht wordt uitgevoerd.

## <a name="ssh-key-and-password-or-password-only"></a>SSH-sleutel en wachtwoord of alleen wachtwoord
Meld u aan bij de virtuele Linux-machine met behulp van SSH-sleutel of het wachtwoord verificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:

    # sudo <command>
    [sudo] password for azureuser:

In dit geval wordt de gebruiker wordt gevraagd om een wachtwoord. Na het invoeren van het wachtwoord `sudo` wordt uitgevoerd de opdracht met `root` bevoegdheden.

U kunt ook passwordless sudo inschakelen door het bewerken van de `/etc/sudoers.d/waagent` bestand, bijvoorbeeld:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Deze wijziging kunt voor passwordless sudo door de gebruiker 'azureuser'.

## <a name="ssh-key-only"></a>SSH alleen sleutel
Meld u aan bij de virtuele Linux-machine met behulp van SSH-sleutelverificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:

    # sudo <command>

In dit geval de gebruiker wordt **niet** worden gevraagd om een wachtwoord. Na zwaarwegende `<enter>`, `sudo` wordt uitgevoerd de opdracht met `root` bevoegdheden.

