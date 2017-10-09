---
title: Veelgestelde vragen voor virtuele Linux-machines in Azure aaaFrequently | Microsoft Docs
description: Biedt antwoorden toosome van Hallo Veelgestelde vragen over gemaakt met Resource Manager-model Hallo virtuele Linux-machines.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Veelgestelde vragen over virtuele Linux-Machines
In dit artikel komen enkele veelgestelde vragen over virtuele Linux-machines in Azure met Resource Manager-implementatiemodel Hallo gemaakt. Zie voor Hallo Windows-versie van dit onderwerp [Veelgestelde vragen over Windows virtuele Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Wat kan ik uitvoeren op een VM van Azure?
Alle abonnees kunnen serversoftware uitvoeren op een virtuele machine van Azure. Zie voor meer informatie [Linux op Azure-Endorsed distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Hoeveel opslagruimte kan ik gebruiken met een virtuele machine?
Elke gegevensschijf kan zijn van too1 TB. Hallo aantal gegevensschijven die u kunt gebruiken, is afhankelijk van Hallo grootte van Hallo virtuele machine. Zie [Grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.

Een Azure storage-account biedt opslag voor de besturingssysteemschijf hello en eventuele gegevensschijven. Elke schijf is een VHD-bestand dat wordt opgeslagen als een pagina-blob. Zie [deze pagina](https://azure.microsoft.com/pricing/details/storage/) voor prijsinformatie.

## <a name="how-can-i-access-my-virtual-machine"></a>Hoe kan ik toegang tot mijn virtuele machine?
Stel een verbinding met extern toolog toohello voor virtuele machines met behulp van Secure Shell (SSH). Zie Hallo instructies over het tooconnect [vanuit Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [van Linux- en Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). SSH biedt standaard ondersteuning voor maximaal tien gelijktijdige verbindingen. U kunt dit getal verhogen door Hallo-configuratiebestand bewerken.

Als u problemen ondervindt, uitchecken [oplossen Secure Shell (SSH) verbindingen](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>Kan ik Hallo tijdelijke schijf (/ dev/sdb1) toostore gegevens gebruiken?
Gebruik geen Hallo tijdelijke schijf (/ dev/sdb1) toostore gegevens. Het is alleen er voor de tijdelijke opslag. U risico verlies van gegevens die kunnen niet worden hersteld.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Kan ik kopiëren of kloon van een bestaande virtuele machine in Azure?
Ja. Zie voor instructies [hoe toocreate kopie maken van een virtuele Linux-machine in de resourcemanager-implementatiemodel Hallo](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Waarom krijg ik niet zien Canada centraal en Canada Oost regio's via Azure Resource Manager?
Hallo twee nieuwe gebieden van Canada Central en Canada Oost worden niet automatisch geregistreerd voor het maken van de virtuele machine voor bestaande Azure-abonnementen. Deze registratie automatisch uitgevoerd wanneer een virtuele machine wordt geïmplementeerd via Azure portal tooany Hallo andere regio's met Azure Resource Manager. Nadat een virtuele machine is geïmplementeerd tooany andere Azure-regio Hallo nieuwe gebieden moet beschikbaar zijn voor latere virtuele machines.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Kan ik een NIC toomy VM toevoegen nadat deze gemaakt?
Ja, dit is nu mogelijk. Hallo VM eerste behoeften toobe gestopt toewijzing ongedaan is gemaakt. U kunt toevoegen of verwijderen van een NIC (tenzij het Hallo laatste NIC op Hallo VM). 

## <a name="are-there-any-computer-name-requirements"></a>Zijn er naam computervereisten?
Ja. Hallo-computernaam mag maximaal 64 tekens lang zijn. Zie [Naming conventions regels en beperkingen](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over de naamgeving van uw resources.

## <a name="are-there-any-resource-group-name-requirements"></a>Zijn er een resource vereisten voor de naam groep?
Ja. Hallo Resourcegroepnaam mag maximaal 90 tekens lang zijn. Zie [Naming conventions regels en beperkingen](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over resourcegroepen.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Wat zijn Hallo gebruikersnaam vereisten bij het maken van een virtuele machine?
Gebruikersnamen moet 1 tot 64 tekens lang zijn.

Hallo volgende gebruikersnamen zijn niet toegestaan:

<table>
    <tr>
        <td style="text-align:center">Beheerder </td><td style="text-align:center"> Beheerder </td><td style="text-align:center"> Gebruiker </td><td style="text-align:center"> Gebruiker1</td>
    </tr>
    <tr>
        <td style="text-align:center">Test </td><td style="text-align:center"> Gebruiker2 </td><td style="text-align:center"> Test1 </td><td style="text-align:center"> User3</td>
    </tr>
    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> een</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> ASPNET</td>
    </tr>
    <tr>
        <td style="text-align:center">Back-up </td><td style="text-align:center"> Console </td><td style="text-align:center"> David </td><td style="text-align:center"> Gast</td>
    </tr>
    <tr>
        <td style="text-align:center">John </td><td style="text-align:center"> Eigenaar </td><td style="text-align:center"> hoofdmap </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">SQL </td><td style="text-align:center"> Ondersteuning </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">Test2 </td><td style="text-align:center"> Test3 </td><td style="text-align:center"> User4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Wat zijn de wachtwoordvereisten Hallo bij het maken van een virtuele machine?
Wachtwoorden moeten 6-72 tekens lang zijn en voldoen aan 3 buiten Hallo 4 complexiteitsvereisten te volgen:

* Lagere tekens bevatten
* Bovenste tekens bevatten
* Een cijfer zijn
* Hebt u een speciaal teken (Regex overeenkomen met [\W_])

Hallo volgende wachtwoorden zijn niet toegestaan:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$ $word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Wachtwoord!</td>
        <td style="text-align:center">Wachtwoord1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">ILOVEYOU!</td>
    </tr>
</table>
