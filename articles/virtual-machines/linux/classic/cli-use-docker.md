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
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="235cb-103">Met behulp van Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="235cb-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="235cb-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="235cb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="235cb-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="235cb-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="235cb-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="235cb-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="235cb-107">Zie voor meer informatie over het gebruik van Hallo Docker VM-extensie met Resource Manager-model Hallo [hier](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="235cb-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="235cb-108">Dit onderwerp beschrijft hoe een virtuele machine met Hallo Docker VM-extensie van Hallo toocreate service management (asm)-modus in Azure CLI op elk platform.</span><span class="sxs-lookup"><span data-stu-id="235cb-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="235cb-109">[Docker](https://www.docker.com/) is een van de Hallo populairste virtualisatie-methoden die gebruikmaakt van [Linux containers](http://en.wikipedia.org/wiki/LXC) in plaats van virtuele machines als een manier om gegevens te isoleren en berekeningen op gedeelde bronnen.</span><span class="sxs-lookup"><span data-stu-id="235cb-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="235cb-110">U kunt Hallo Docker VM-extensie en Hallo [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate een Docker-virtuele machine die als host fungeert voor een onbeperkt aantal containers voor uw toepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="235cb-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="235cb-111">een hoog niveau bespreking van containers en hun voordelen toosee Zie Hallo [Docker hoog niveau Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="235cb-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="235cb-112">Hoe toouse Hallo Docker VM-extensie met Azure</span><span class="sxs-lookup"><span data-stu-id="235cb-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="235cb-113">toouse hello Docker VM-extensie met Azure, moet u een versie van Hallo installeren [Azure-opdrachtregelinterface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) hoger is dan 0.8.6 (zoals de huidige versie is van deze Hallo schrijven 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="235cb-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="235cb-114">U kunt hello Azure CLI voor Mac, Linux en Windows installeren.</span><span class="sxs-lookup"><span data-stu-id="235cb-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="235cb-115">Hallo volledig toouse Docker in Azure is eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="235cb-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="235cb-116">Hello Azure CLI en de bijbehorende afhankelijkheden op Hallo computer van waaruit u toocontrol Azure wilt installeren (op Windows, wordt dit een Linux-distributie uitgevoerd als een virtuele machine)</span><span class="sxs-lookup"><span data-stu-id="235cb-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="235cb-117">Hello Azure CLI Docker opdrachten toocreate een Docker VM-host in Azure gebruiken</span><span class="sxs-lookup"><span data-stu-id="235cb-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="235cb-118">Hallo lokale Docker opdrachten toomanage uw Docker-containers in uw Docker-virtuele machine in Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="235cb-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="235cb-119">Hello Azure-opdrachtregelinterface (Azure CLI) installeren</span><span class="sxs-lookup"><span data-stu-id="235cb-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="235cb-120">tooinstall en hello Azure CLI configureren, Zie [hoe tooinstall hello Azure-opdrachtregelinterface](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="235cb-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="235cb-121">type-installatie Hallo tooconfirm `azure` achter de opdrachtprompt Hallo en na een korte ogenblik ziet u hello Azure CLI ASCII-illustraties waarin Hallo basic opdrachten beschikbaar tooyou.</span><span class="sxs-lookup"><span data-stu-id="235cb-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="235cb-122">Als installatie Hallo correct werkt, moet u kunnen tootype `azure help vm` en ziet dat een van de opdrachten Hallo vermeld 'docker'.</span><span class="sxs-lookup"><span data-stu-id="235cb-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="235cb-123">Docker bevat hulpprogramma's voor Windows, [Docker-Machine](https://docs.docker.com/installation/windows/), die u kunt ook tooautomate Hallo maken van een docker-client die u toowork kunt gebruiken met Azure Virtual machines als docker-hosts.</span><span class="sxs-lookup"><span data-stu-id="235cb-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="235cb-124">Verbinding maken met hello Azure CLI tootooyour Azure-Account</span><span class="sxs-lookup"><span data-stu-id="235cb-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="235cb-125">Voordat u kunt hello Azure CLI gebruiken moet u de referenties van uw Azure-account koppelen aan hello Azure CLI op uw platform.</span><span class="sxs-lookup"><span data-stu-id="235cb-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="235cb-126">sectie Hallo [hoe tooconnect tooyour Azure-abonnement](../../../xplat-cli-connect.md) wordt uitgelegd hoe tooeither downloaden en importeren uw **.publishsettings** bestand of om uw Azure-CLI koppelen aan een organisatie-id.</span><span class="sxs-lookup"><span data-stu-id="235cb-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="235cb-127">Er zijn bepaalde verschillen in het gedrag wanneer met behulp van een of hello andere methoden voor verificatie, dus worden ervoor tooread Hallo document hierboven toounderstand Hallo verschillende functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="235cb-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="235cb-128">Docker installeren en gebruiken van Hallo Docker VM-extensie voor Azure</span><span class="sxs-lookup"><span data-stu-id="235cb-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="235cb-129">Ga als volgt Hallo [Docker-installatie-instructies](https://docs.docker.com/installation/#installation) tooinstall Docker lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="235cb-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="235cb-130">toouse Docker met een virtuele Machine van Azure, Hallo Linux afbeelding gebruikt voor Hallo VM moet beschikken over Hallo [Azure Linux VM-Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="235cb-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="235cb-131">Er zijn momenteel slechts twee typen installatiekopieën die deze:</span><span class="sxs-lookup"><span data-stu-id="235cb-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="235cb-132">De installatiekopie van een Ubuntu vanaf Hallo galerie van Azure-installatiekopie of</span><span class="sxs-lookup"><span data-stu-id="235cb-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="235cb-133">Een aangepaste installatiekopie van Linux die u hebt gemaakt met hello Azure Linux VM-Agent geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="235cb-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="235cb-134">Zie [Azure Linux VM-Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over het toobuild een aangepaste Linux VM Hello Azure VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="235cb-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="235cb-135">Met behulp van hello Azure installatiekopie-galerie</span><span class="sxs-lookup"><span data-stu-id="235cb-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="235cb-136">Gebruik vanaf een Bash of Terminal-sessie, hello Azure CLI-opdracht toolocate Hallo meest recente Ubuntu-installatiekopie in Hallo VM galerie toouse door in te voeren na</span><span class="sxs-lookup"><span data-stu-id="235cb-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="235cb-137">en selecteer een van de namen van de installatiekopie hello, zoals `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, en gebruik Hallo volgende opdracht toocreate een nieuwe virtuele machine met behulp van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="235cb-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="235cb-138">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="235cb-138">where:</span></span>

* <span data-ttu-id="235cb-139">*&lt;de naam van de VM-cloudservice&gt;*  heet Hallo Hallo VM die Hallo Docker-container hostcomputer in Azure fungeren zal</span><span class="sxs-lookup"><span data-stu-id="235cb-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="235cb-140">*&lt;gebruikersnaam&gt;*  Hallo-gebruikersnaam van het standaard-hoofdgebruiker Hallo Hallo VM</span><span class="sxs-lookup"><span data-stu-id="235cb-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="235cb-141">*&lt;wachtwoord&gt;*  Hallo wachtwoord Hallo *gebruikersnaam* account dat voldoet aan de normen Hallo van complexiteit voor Azure</span><span class="sxs-lookup"><span data-stu-id="235cb-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="235cb-142">Op dit moment een wachtwoord moet ten minste 8 tekens, één kleine letter en één hoofdletter, een getal en een speciaal teken zoals een Hallo volgende tekens bevatten: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="235cb-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="235cb-143">Nee, Hallo periode achter Hallo Hallo voorgaande zin is niet een speciaal teken.</span><span class="sxs-lookup"><span data-stu-id="235cb-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="235cb-144">Als Hallo-opdracht voltooid is, ziet u dat lijkt op Hallo volgende, afhankelijk van Hallo nauwkeurig argumenten en opties die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="235cb-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="235cb-145">Maken van een virtuele machine, kan een paar minuten duren, maar nadat deze zijn ingericht (Hallo statuswaarde is `ReadyRole`) Hallo Docker-daemon (hello Docker-service) wordt gestart en u verbinding kunt maken met toohello Docker-containerhost.</span><span class="sxs-lookup"><span data-stu-id="235cb-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="235cb-146">tootest hello Docker VM die u hebt gemaakt in Azure, type</span><span class="sxs-lookup"><span data-stu-id="235cb-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="235cb-147">waar  *&lt;vm-naam-u-gebruikt&gt;*  heet Hallo Hallo virtuele machine die u in de aanroep te gebruikt`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="235cb-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="235cb-148">U ziet iets dergelijks toohello volgende, waarmee wordt aangegeven dat uw virtuele machine Docker-Host actief is en worden uitgevoerd in Azure en wachten op de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="235cb-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="235cb-149">Nu kunt u met behulp van de docker-clientinformatie tooobtain tooconnect proberen (in sommige Docker-client-instellingen, zoals die op de Mac, moet u wellicht toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="235cb-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

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

<span data-ttu-id="235cb-150">Alleen toobe zeker weet dat u alle werkende, u kunt Hallo VM voor Hallo Docker-extensie controleren:</span><span class="sxs-lookup"><span data-stu-id="235cb-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="235cb-151">Docker-verificatie voor Webtoepassingshost VM</span><span class="sxs-lookup"><span data-stu-id="235cb-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="235cb-152">Bovendien toocreating hello Docker-VM Hallo `azure vm docker create` opdracht ook automatisch maakt Hallo benodigde certificaten tooallow uw Docker client computer tooconnect toohello Azure containerhost via HTTPS en op beide Hallo certificaten zijn opgeslagen Hallo-client en host machines, naar gelang van toepassing.</span><span class="sxs-lookup"><span data-stu-id="235cb-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="235cb-153">Op de daaropvolgende pogingen worden gedaan, worden bestaande certificaten Hallo opnieuw gebruikt en gedeeld met Hallo nieuwe host.</span><span class="sxs-lookup"><span data-stu-id="235cb-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="235cb-154">Standaard certificaten zijn geplaatst `~/.docker`, en Docker worden geconfigureerde toorun op poort **2376**.</span><span class="sxs-lookup"><span data-stu-id="235cb-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="235cb-155">Als u een andere poort toouse of map dat wilt, moet u een van de volgende Hallo `azure vm docker create` opties voor opdrachtregel tooconfigure uw Docker-container host VM toouse een andere poort of verschillende certificaten voor verbindingen met clients:</span><span class="sxs-lookup"><span data-stu-id="235cb-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="235cb-156">Hallo Docker-daemon op Hallo host is geconfigureerde toolisten voor en verifiëren van de client-verbindingen op Hallo opgegeven poort Hallo certificaten gebruikt die zijn gegenereerd door Hallo `azure vm docker create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="235cb-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="235cb-157">Hallo-clientcomputer moet deze certificaten toogain toegang toohello Docker host hebben.</span><span class="sxs-lookup"><span data-stu-id="235cb-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="235cb-158">Een netwerkhost uitgevoerd zonder deze certificaten zijn kwetsbaar tooanyone kunt tooconnect toohello machine.</span><span class="sxs-lookup"><span data-stu-id="235cb-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="235cb-159">Voordat u de standaardconfiguratie Hallo wijzigt, zorg ervoor dat u Hallo risico's tooyour computers en toepassingen begrijpt.</span><span class="sxs-lookup"><span data-stu-id="235cb-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="235cb-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="235cb-160">Next steps</span></span>
* <span data-ttu-id="235cb-161">U bent klaar toogo toohello [Docker-gebruikershandleiding] en de Docker-VM te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="235cb-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="235cb-162">een VM Docker-functionaliteit in de nieuwe portal Hallo toocreate Zie [hoe toouse Docker VM-extensie Hallo Hello Portal].</span><span class="sxs-lookup"><span data-stu-id="235cb-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="235cb-163">ondersteunt Docker Compose dat gebruikmaakt van een declaratieve tootake YAML-bestand een ontwikkelaar gemodelleerd-toepassing in een omgeving tevens Hello Azure Docker VM-extensie en het genereren van een consistente implementatie.</span><span class="sxs-lookup"><span data-stu-id="235cb-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="235cb-164">Zie [aan de slag met Docker Compose toodefine en een toepassing met meerdere container uitvoert op een virtuele machine van Azure].</span><span class="sxs-lookup"><span data-stu-id="235cb-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

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
