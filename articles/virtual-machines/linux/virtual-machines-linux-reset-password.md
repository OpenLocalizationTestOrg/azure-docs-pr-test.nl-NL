---
title: aaaHow tooreset lokale Linux-wachtwoord op Azure Virtual machines | Microsoft Docs
description: Introduceren Hallo stappen tooreset Hallo lokale Linux-wachtwoord op Azure VM
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Hoe tooreset lokale Linux-wachtwoord op Azure Virtual machines

Dit artikel bevat verschillende methoden tooreset lokale Linux-virtuele Machine (VM) wachtwoorden. Als Hallo-gebruikersaccount is verlopen of als u alleen toocreate een nieuw account wilt, kunt u deze kunt gebruiken Hallo na methoden toocreate een nieuwe lokale beheerdersaccount en opnieuw krijgen toegang toohello VM.

## <a name="symptoms"></a>Symptomen

U kunt zich niet aanmelden toohello VM en u ontvangt een bericht weergegeven dat aangeeft dat Hallo wachtwoord die u hebt gebruikt, is onjuist. Bovendien u niet gebruiken VMAgent tooreset uw wachtwoord op Hallo Azure-Portal. 

## <a name="manual-password-reset-procedure"></a>Handmatige procedure voor wachtwoord opnieuw instellen

1.  Hallo VM verwijderen en schijven Hallo gekoppeld houden.

2.  Hallo OS station als een schijf gegevens tooanother koppelen tijdelijke virtuele machine in Hallo dezelfde locatie.

3.  Hallo SSH-opdracht op Hallo tijdelijke VM toobecome volgen supergebruiker uitgevoerd.


    ~~~~
    sudo su
    ~~~~

4.  Voer **fdisk -l** of kijken system logboeken toofind Hallo nieuwe schijf is gekoppeld. Hallo station naam toomount vinden. Klik op Hallo tijdelijke virtuele machine, zoeken in de relevante Hallo logbestand.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Hallo volgt voorbeelduitvoer van Hallo grep-opdracht:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Maken van een koppelpunt aangeroepen **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Hallo OS-schijf koppelen op Hallo-koppelpunt. U hoeft meestal toomount sdc1 of sdc2. Dit hangt af van Hallo partitie in de map/etc van Hallo verbroken machineschijf die als host fungeert.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Een back-up uitvoeren voordat u wijzigingen aanbrengt:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Het wachtwoord opnieuw instellen van Hallo gebruiker die u nodig hebt:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Verplaatsing Hallo gewijzigd bestanden toohello juiste locatie op Hallo van machine schijf verbroken.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
