---
title: aaaUse hoofdmap bevoegdheden op de virtuele Linux-machines | Microsoft Docs
description: Meer informatie over hoe toouse hoofdmap bevoegdheden hebben op een virtuele Linux-machine in Azure.
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
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Bevoegdheden op hoofdniveau gebruiken op virtuele Linux-machines in Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Standaard Hallo `root` gebruiker is uitgeschakeld op Linux virtuele machines in Azure. Gebruikers kunnen opdrachten uitvoeren met verhoogde bevoegdheden via Hallo `sudo` opdracht. Hallo-ervaring kan echter variëren afhankelijk van hoe Hallo system is ingericht.

1. **SSH-sleutel en het wachtwoord of wachtwoord alleen** -Hallo virtuele machine is ingericht met ofwel een certificaat (`.CER` bestand) of SSH-sleutel, evenals een wachtwoord, of alleen een gebruikersnaam en wachtwoord. In dit geval `sudo` voor Hallo gebruikerswachtwoord wordt gevraagd voordat het Hallo-opdracht wordt uitgevoerd.
2. **SSH-sleutel** -Hallo virtuele machine is ingericht met een certificaat (`.cer`, `.pem`, of `.pub` bestand) of SSH-sleutel, maar er is geen wachtwoord.  In dit geval `sudo` **niet** vragen om het wachtwoord van de gebruiker van de Hallo voordat Hallo-opdracht wordt uitgevoerd.

## <a name="ssh-key-and-password-or-password-only"></a>SSH-sleutel en wachtwoord of alleen wachtwoord
Meld u aan bij Hallo Linux virtuele machine met behulp van SSH-sleutel of het wachtwoord verificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:

    # sudo <command>
    [sudo] password for azureuser:

In dit geval wordt Hallo gebruiker gevraagd om een wachtwoord. Na het invoeren van Hallo wachtwoord `sudo` wordt uitgevoerd Hallo-opdracht met `root` bevoegdheden.

U kunt ook passwordless sudo inschakelen door het bewerken van Hallo `/etc/sudoers.d/waagent` bestand, bijvoorbeeld:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Deze wijziging kunt voor passwordless sudo door gebruiker Hallo 'azureuser'.

## <a name="ssh-key-only"></a>SSH alleen sleutel
Meld u aan bij Hallo Linux virtuele machine met behulp van SSH-sleutelverificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:

    # sudo <command>

In dit geval Hallo gebruiker wordt **niet** worden gevraagd om een wachtwoord. Na zwaarwegende `<enter>`, `sudo` wordt uitgevoerd Hallo-opdracht met `root` bevoegdheden.

