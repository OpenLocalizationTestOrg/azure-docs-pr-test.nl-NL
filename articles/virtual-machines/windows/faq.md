---
title: aaaFAQ over Windows virtuele machines in Azure | Microsoft Docs
description: Biedt antwoorden toosome van Hallo Veelgestelde vragen over Windows virtuele machines is gemaakt met de Hallo Resource Manager-model.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Veelgestelde vragen over virtuele Windows-Machines
In dit artikel komen enkele veelgestelde vragen over Windows virtuele machines in Azure met Resource Manager-implementatiemodel Hallo gemaakt. Zie voor Hallo Linux-versie van dit onderwerp [Veelgestelde vragen over virtuele Linux-Machines](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Wat kan ik uitvoeren op een VM van Azure?
Alle abonnees kunnen serversoftware uitvoeren op een virtuele machine van Azure. Zie voor meer informatie over Hallo ondersteuningsbeleid voor Microsoft-serversoftware uitgevoerd in Azure [Microsoft server softwareondersteuning voor Azure Virtual Machines](https://support.microsoft.com/kb/2721672)

Bepaalde versies van Windows 7, Windows 8.1 en Windows 10 zijn beschikbaar tooMSDN Azure voordeel abonnees en abonnees van een MSDN ontwikkelen en testen betalen naar gebruik voor ontwikkel- en taken. Zie het Engelstalige blogbericht [Windows Client images for MSDN subscribers](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/) voor meer informatie, zoals instructies en beperkingen. 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Hoeveel opslagruimte kan ik gebruiken met een virtuele machine?
Elke gegevensschijf kan zijn van too1 TB. Hallo aantal gegevensschijven die u kunt gebruiken, is afhankelijk van Hallo grootte van Hallo virtuele machine. Zie [Grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie.

Azure-beheerde schijven zijn Hallo nieuwe en aanbevolen schijf opslag voor gebruik met Azure Virtual Machines voor permanente opslag van gegevens. U kunt voor elke virtuele machine Managed Disks gebruiken. Azure Managed Disks biedt twee typen duurzame opslag: Premium en Standard Managed Disks. Zie voor informatie over prijzen, [beheerd schijven prijzen](https://azure.microsoft.com/pricing/details/managed-disks).

Azure storage-accounts kunnen ook opslag bieden voor de besturingssysteemschijf hello en eventuele gegevensschijven. Elke schijf is een VHD-bestand dat wordt opgeslagen als een pagina-blob. Zie [deze pagina](https://azure.microsoft.com/pricing/details/storage/) voor prijsinformatie.

## <a name="how-can-i-access-my-virtual-machine"></a>Hoe kan ik toegang tot mijn virtuele machine?
Stel een externe verbinding verbinding met extern bureaublad (RDP) voor een virtuele machine van Windows. Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Maximaal twee gelijktijdige verbindingen worden ondersteund, tenzij het Hallo-server is geconfigureerd als een extern bureaublad-Services sessiehost.  

Als u problemen met extern bureaublad ondervindt, Zie [tooa van problemen met extern bureaublad-verbindingen op basis van Windows Azure virtuele Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Als u bekend met Hyper-V bent, kijkt u misschien voor een vergelijkbaar tooVMConnect hulpprogramma. Azure biedt geen een vergelijkbaar hulpprogramma bieden omdat console toegang tooa virtuele machine wordt niet ondersteund.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Kan ik Hallo tijdelijke schijf (hello station standaard D:) toostore gegevens gebruiken?
Gebruik geen Hallo tijdelijke schijf toostore gegevens. Het is alleen tijdelijke opslag, zodat u zou risico verlies van gegevens die kunnen niet worden hersteld. Verlies van gegevens kan optreden wanneer Hallo virtuele machine wordt verplaatst tooa andere host. Grootte wijzigen van een virtuele machine, zijn Hallo host of een hardwarefout op Hallo host bijwerken Hallo redenen die een virtuele machine mogelijk verplaatsen.

Als u een toepassing die toouse Hallo D: stationsletter nodig hebt, kunt u stationsletters kunt toewijzen, zodat hello tijdelijke schijf gebruikmaakt van iets anders dan D:. Zie voor instructies [wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Hoe kan ik de stationsletter op Hallo van de tijdelijke schijf Hallo wijzigen?
U kunt wijzigen Hallo stationsletter door bewegende Hallo wisselbestand en stations opnieuw toewijzen, maar moet u zeker dat u de stappen in een bepaalde volgorde Hallo toomake. Zie voor instructies [wijziging stationsletter op Hallo van Hallo Windows tijdelijke schijf](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>Kan ik een bestaande VM tooan beschikbaarheidsset toevoegen?
Nee. Als u wilt dat uw VM toobe een deel van een beschikbaarheidsset, moet u toocreate Hallo VM binnen Hallo set. Er is momenteel niet een tooadd manier een VM tooan beschikbaarheid instellen nadat deze is gemaakt.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Kan ik een virtuele machine tooAzure uploaden?
Ja. Zie voor instructies [migreren lokale VMs tooAzure](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Kan ik het formaat van de besturingssysteemschijf Hallo?
Ja. Zie voor instructies [hoe tooexpand OS-schijf van een virtuele Machine in een Azure-resourcegroep Hallo](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Kan ik kopiëren of kloon van een bestaande virtuele machine in Azure?
Ja. Beheerde installatiekopieën gebruikt, kunt u een installatiekopie van een virtuele machine maken en gebruik vervolgens Hallo installatiekopie toobuild meerdere nieuwe virtuele machines. Zie voor instructies [een aangepaste installatiekopie van een VM maken](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Waarom krijg ik niet zien Canada centraal en Canada Oost regio's via Azure Resource Manager?

Hallo twee nieuwe gebieden van Canada Central en Canada Oost worden niet automatisch geregistreerd voor het maken van de virtuele machine voor bestaande Azure-abonnementen. Deze registratie automatisch uitgevoerd wanneer een virtuele machine wordt geïmplementeerd via Azure portal tooany Hallo andere regio's met Azure Resource Manager. Nadat een virtuele machine is geïmplementeerd tooany andere Azure-regio Hallo nieuwe gebieden moet beschikbaar zijn voor latere virtuele machines.

## <a name="does-azure-support-linux-vms"></a>Azure biedt ondersteuning voor virtuele Linux-machines?
Ja. tooquickly maken een tootry Linux-VM uit, Zie [maken van een Linux-VM op Azure met behulp van Hallo Portal](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Kan ik een NIC toomy VM toevoegen nadat deze gemaakt?
Ja, dit is nu mogelijk. Hallo VM eerste behoeften toobe gestopt toewijzing ongedaan is gemaakt. U kunt toevoegen of verwijderen van een NIC (tenzij het Hallo laatste NIC op Hallo VM). 

## <a name="are-there-any-computer-name-requirements"></a>Zijn er naam computervereisten?
Ja. Hallo-computernaam mag maximaal 15 tekens lang zijn. Zie [Naming conventions regels en beperkingen](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie over de naamgeving van uw resources.

## <a name="are-there-any-resource-group-name-requirements"></a>Zijn er een resource vereisten voor de naam groep?
Ja. Hallo Resourcegroepnaam mag maximaal 90 tekens lang zijn. Zie [Naming conventions regels en beperkingen](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie over resourcegroepen.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Wat zijn Hallo gebruikersnaam vereisten bij het maken van een virtuele machine?

Gebruikersnamen mag maximaal 20 tekens lang zijn en mag niet eindigen op een punt ('. '). 


Hallo volgende gebruikersnamen zijn niet toegestaan:
<table>
    <tr>
        <td style="text-align:center">Beheerder </td><td style="text-align:center"> Beheerder </td><td style="text-align:center"> Gebruiker </td><td style="text-align:center"> Gebruiker1</td>
    </tr>
    <tr>
        <td style="text-align:center">Test </td><td style="text-align:center"> Gebruiker2 </td><td style="text-align:center"> Test1 </td><td style="text-align:center"> User3</td>
    </tr>    <tr>
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
Wachtwoorden moeten 12 123 tekens lang zijn en 3 buiten Hallo na 4 complexiteitsvereisten voldoen:

* Lagere tekens bevatten
* Bovenste tekens bevatten
* Een cijfer zijn
* Hebt u een speciaal teken (Regex overeenkomen met [\W_])

Hallo volgende wachtwoorden zijn niet toegestaan:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$ $word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Wachtwoord! </td>
        <td>Wachtwoord1 </td>
        <td>Password22 </td>
        <td>ILOVEYOU! </td>
    </tr>
</table>
