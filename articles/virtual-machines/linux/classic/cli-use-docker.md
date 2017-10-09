---
title: aaaUsing hello Docker VM-extensie voor Linux op Azure
description: Worden Docker en hello Azure Virtual Machines uitbreidingen beschreven en ziet u hoe tooprogrammatically virtuele Machines maken in Azure die docker-hosts vanaf Hallo-opdrachtregel met behulp van hello Azure CLI.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>Met behulp van Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor meer informatie over het gebruik van Hallo Docker VM-extensie met Resource Manager-model Hallo [hier](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dit onderwerp beschrijft hoe een virtuele machine met Hallo Docker VM-extensie van Hallo toocreate service management (asm)-modus in Azure CLI op elk platform. [Docker](https://www.docker.com/) is een van de Hallo populairste virtualisatie-methoden die gebruikmaakt van [Linux containers](http://en.wikipedia.org/wiki/LXC) in plaats van virtuele machines als een manier om gegevens te isoleren en berekeningen op gedeelde bronnen. U kunt Hallo Docker VM-extensie en Hallo [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate een Docker-virtuele machine die als host fungeert voor een onbeperkt aantal containers voor uw toepassingen in Azure. een hoog niveau bespreking van containers en hun voordelen toosee Zie Hallo [Docker hoog niveau Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Hoe toouse Hallo Docker VM-extensie met Azure
toouse hello Docker VM-extensie met Azure, moet u een versie van Hallo installeren [Azure-opdrachtregelinterface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) hoger is dan 0.8.6 (zoals de huidige versie is van deze Hallo schrijven 0.10.0). U kunt hello Azure CLI voor Mac, Linux en Windows installeren.

Hallo volledig toouse Docker in Azure is eenvoudig:

* Hello Azure CLI en de bijbehorende afhankelijkheden op Hallo computer van waaruit u toocontrol Azure wilt installeren (op Windows, wordt dit een Linux-distributie uitgevoerd als een virtuele machine)
* Hello Azure CLI Docker opdrachten toocreate een Docker VM-host in Azure gebruiken
* Hallo lokale Docker opdrachten toomanage uw Docker-containers in uw Docker-virtuele machine in Azure gebruiken.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Hello Azure-opdrachtregelinterface (Azure CLI) installeren
tooinstall en hello Azure CLI configureren, Zie [hoe tooinstall hello Azure-opdrachtregelinterface](../../../cli-install-nodejs.md). type-installatie Hallo tooconfirm `azure` achter de opdrachtprompt Hallo en na een korte ogenblik ziet u hello Azure CLI ASCII-illustraties waarin Hallo basic opdrachten beschikbaar tooyou. Als installatie Hallo correct werkt, moet u kunnen tootype `azure help vm` en ziet dat een van de opdrachten Hallo vermeld 'docker'.

> [!NOTE]
> Docker bevat hulpprogramma's voor Windows, [Docker-Machine](https://docs.docker.com/installation/windows/), die u kunt ook tooautomate Hallo maken van een docker-client die u toowork kunt gebruiken met Azure Virtual machines als docker-hosts.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Verbinding maken met hello Azure CLI tootooyour Azure-Account
Voordat u kunt hello Azure CLI gebruiken moet u de referenties van uw Azure-account koppelen aan hello Azure CLI op uw platform. sectie Hallo [hoe tooconnect tooyour Azure-abonnement](../../../xplat-cli-connect.md) wordt uitgelegd hoe tooeither downloaden en importeren uw **.publishsettings** bestand of om uw Azure-CLI koppelen aan een organisatie-id.

> [!NOTE]
> Er zijn bepaalde verschillen in het gedrag wanneer met behulp van een of hello andere methoden voor verificatie, dus worden ervoor tooread Hallo document hierboven toounderstand Hallo verschillende functionaliteit.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Docker installeren en gebruiken van Hallo Docker VM-extensie voor Azure
Ga als volgt Hallo [Docker-installatie-instructies](https://docs.docker.com/installation/#installation) tooinstall Docker lokaal op uw computer.

toouse Docker met een virtuele Machine van Azure, Hallo Linux afbeelding gebruikt voor Hallo VM moet beschikken over Hallo [Azure Linux VM-Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) geïnstalleerd. Er zijn momenteel slechts twee typen installatiekopieën die deze:

* De installatiekopie van een Ubuntu vanaf Hallo galerie van Azure-installatiekopie of
* Een aangepaste installatiekopie van Linux die u hebt gemaakt met hello Azure Linux VM-Agent geïnstalleerd en geconfigureerd. Zie [Azure Linux VM-Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over het toobuild een aangepaste Linux VM Hello Azure VM-Agent.

### <a name="using-hello-azure-image-gallery"></a>Met behulp van hello Azure installatiekopie-galerie
Gebruik vanaf een Bash of Terminal-sessie, hello Azure CLI-opdracht toolocate Hallo meest recente Ubuntu-installatiekopie in Hallo VM galerie toouse door in te voeren na

`azure vm image list | grep Ubuntu-14_04`

en selecteer een van de namen van de installatiekopie hello, zoals `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, en gebruik Hallo volgende opdracht toocreate een nieuwe virtuele machine met behulp van de installatiekopie.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

Waarbij:

* *&lt;de naam van de VM-cloudservice&gt;*  heet Hallo Hallo VM die Hallo Docker-container hostcomputer in Azure fungeren zal
* *&lt;gebruikersnaam&gt;*  Hallo-gebruikersnaam van het standaard-hoofdgebruiker Hallo Hallo VM
* *&lt;wachtwoord&gt;*  Hallo wachtwoord Hallo *gebruikersnaam* account dat voldoet aan de normen Hallo van complexiteit voor Azure

> [!NOTE]
> Op dit moment een wachtwoord moet ten minste 8 tekens, één kleine letter en één hoofdletter, een getal en een speciaal teken zoals een Hallo volgende tekens bevatten: `!@#$%^&+=`. Nee, Hallo periode achter Hallo Hallo voorgaande zin is niet een speciaal teken.
> 
> 

Als Hallo-opdracht voltooid is, ziet u dat lijkt op Hallo volgende, afhankelijk van Hallo nauwkeurig argumenten en opties die u gebruikt:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Maken van een virtuele machine, kan een paar minuten duren, maar nadat deze zijn ingericht (Hallo statuswaarde is `ReadyRole`) Hallo Docker-daemon (hello Docker-service) wordt gestart en u verbinding kunt maken met toohello Docker-containerhost.
> 
> 

tootest hello Docker VM die u hebt gemaakt in Azure, type

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

waar  *&lt;vm-naam-u-gebruikt&gt;*  heet Hallo Hallo virtuele machine die u in de aanroep te gebruikt`azure vm docker create`. U ziet iets dergelijks toohello volgende, waarmee wordt aangegeven dat uw virtuele machine Docker-Host actief is en worden uitgevoerd in Azure en wachten op de opdrachten. 

Nu kunt u met behulp van de docker-clientinformatie tooobtain tooconnect proberen (in sommige Docker-client-instellingen, zoals die op de Mac, moet u wellicht toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Alleen toobe zeker weet dat u alle werkende, u kunt Hallo VM voor Hallo Docker-extensie controleren:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Docker-verificatie voor Webtoepassingshost VM
Bovendien toocreating hello Docker-VM Hallo `azure vm docker create` opdracht ook automatisch maakt Hallo benodigde certificaten tooallow uw Docker client computer tooconnect toohello Azure containerhost via HTTPS en op beide Hallo certificaten zijn opgeslagen Hallo-client en host machines, naar gelang van toepassing. Op de daaropvolgende pogingen worden gedaan, worden bestaande certificaten Hallo opnieuw gebruikt en gedeeld met Hallo nieuwe host.

Standaard certificaten zijn geplaatst `~/.docker`, en Docker worden geconfigureerde toorun op poort **2376**. Als u een andere poort toouse of map dat wilt, moet u een van de volgende Hallo `azure vm docker create` opties voor opdrachtregel tooconfigure uw Docker-container host VM toouse een andere poort of verschillende certificaten voor verbindingen met clients:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

Hallo Docker-daemon op Hallo host is geconfigureerde toolisten voor en verifiëren van de client-verbindingen op Hallo opgegeven poort Hallo certificaten gebruikt die zijn gegenereerd door Hallo `azure vm docker create` opdracht. Hallo-clientcomputer moet deze certificaten toogain toegang toohello Docker host hebben.

> [!NOTE]
> Een netwerkhost uitgevoerd zonder deze certificaten zijn kwetsbaar tooanyone kunt tooconnect toohello machine. Voordat u de standaardconfiguratie Hallo wijzigt, zorg ervoor dat u Hallo risico's tooyour computers en toepassingen begrijpt.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* U bent klaar toogo toohello [Docker-gebruikershandleiding] en de Docker-VM te gebruiken. een VM Docker-functionaliteit in de nieuwe portal Hallo toocreate Zie [hoe toouse Docker VM-extensie Hallo Hello Portal].
* ondersteunt Docker Compose dat gebruikmaakt van een declaratieve tootake YAML-bestand een ontwikkelaar gemodelleerd-toepassing in een omgeving tevens Hello Azure Docker VM-extensie en het genereren van een consistente implementatie. Zie [aan de slag met Docker Compose toodefine en een toepassing met meerdere container uitvoert op een virtuele machine van Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[hoe toouse Docker VM-extensie Hallo Hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Docker-gebruikershandleiding]:https://docs.docker.com/userguide/

[aan de slag met Docker Compose toodefine en een toepassing met meerdere container uitvoert op een virtuele machine van Azure]:../docker-compose-quickstart.md
