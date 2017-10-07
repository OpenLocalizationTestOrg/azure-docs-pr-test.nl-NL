---
title: aaaUsing Docker VM-extensie voor Linux | Microsoft Docs
description: Hierin wordt beschreven Docker en hello Azure Virtual Machines bestandsextensies, en hoe toocreate Azure virtuele Machines die zijn docker-hosts met behulp van Azure CLI Hallo klassieke implementatiemodel.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Met behulp van Docker VM-extensie Hallo Hello klassieke Azure-portal
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

[Docker](https://www.docker.com/) is een van de Hallo populairste virtualisatie-methoden die gebruikmaakt van [Linux containers](http://en.wikipedia.org/wiki/LXC) in plaats van virtuele machines als een manier om gegevens te isoleren en berekeningen op gedeelde bronnen. U kunt Hallo Docker VM-extensie beheerd door [Azure Linux Agent] toocreate een Docker-virtuele machine die als host fungeert voor een onbeperkt aantal containers voor uw toepassingen in Azure.

> [!NOTE]
> Dit onderwerp wordt beschreven hoe toocreate een Docker VM van Hallo klassieke Azure-portal. hoe toocreate een Docker-virtuele machine op de opdrachtregel hello, Zie toosee [hoe toouse Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)]. een hoog niveau bespreking van containers en hun voordelen toosee Zie Hallo [Docker hoog niveau Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Een nieuwe virtuele machine maken vanuit Hallo installatiekopie galerie
de eerste stap Hallo vereist een Azure-VM uit een Linux-installatiekopie die ondersteuning biedt voor Hallo Docker VM-extensie, de installatiekopie van een Ubuntu 14.04 TNS vanaf Hallo installatiekopie galerie met als een serverinstallatiekopie voorbeeld en Ubuntu 14.04 bureaublad als een client. Klik in de portal Hallo op **+ nieuw** in Hallo linksonder hoek toocreate een nieuw exemplaar van de virtuele machine en selecteer de installatiekopie van een Ubuntu 14.04 TNS van beschikbare Hallo selecties of van Hallo voltooien installatiekopie galerie, zoals hieronder wordt weergegeven.

> [!NOTE]
> Op dit moment ondersteunen alleen Ubuntu 14.04 TNS afbeeldingen recenter dan juli 2014 Hallo Docker VM-extensie.
> 
> 

![Maak een nieuwe Ubuntu-afbeelding](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Docker-certificaten maken
Zorg ervoor dat de Docker is geïnstalleerd op de clientcomputer na Hallo die VM is gemaakt. (Zie voor meer informatie [Docker-installatie-instructies](https://docs.docker.com/installation/#installation).)

Hallo certificaat en de sleutel-bestanden maken voor Docker-communicatie te volgens[Docker uitgevoerd met https] en plaats deze in Hallo  **`~/.docker`**  map op de clientcomputer.

> [!NOTE]
> Hallo Docker VM-extensie in Hallo-portal op dit moment zijn referenties nodig met base64-gecodeerd zijn.
> 
> 

Op de opdrachtregel hello gebruiken  **`base64`**  of een andere favoriet toocreate base64-gecodeerd onderwerpen met betrekking tot codering. Dit wordt uitgevoerd met een eenvoudige reeks certificaat en de sleutel bestanden eruit vergelijkbare toothis:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Hallo Docker VM-extensie toevoegen
tooadd hello Docker VM-extensie, zoekt u VM-instantie Hallo u hebt gemaakt en schuif naar beneden te**extensies** en klik op de toobring van VM-extensies, zoals hieronder wordt weergegeven.

> [!NOTE]
> Deze functionaliteit wordt ondersteund in alleen Hallo preview-portal: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Toevoegen van een uitbreiding
Klik op Hallo **+ toevoegen** toodisplay Hallo mogelijke VM-extensies kunt u toothis VM toevoegen.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Selecteer Hallo Docker VM-extensie
Kies Hallo Docker VM-extensie, die Hallo Docker beschrijving en belangrijke koppelingen wordt, en klik vervolgens op **maken** op Hallo onder toobegin Hallo-installatieprocedure.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Het certificaat en de sleutelbestanden toevoegen:
Voer in formuliervelden hello, Hallo base64-gecodeerd versies van uw CA-certificaat, het servercertificaat en de sleutel van uw Server, zoals wordt weergegeven in de volgende afbeelding Hallo.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Houd er rekening mee dat (zoals in hello voorafgaand aan de installatiekopie) Hallo 2376 wordt gevuld standaard. Kunt u hier een willekeurig eindpunt Hallo volgende stap worden echter tooopen up Hallo die overeenkomt met eindpunt. Als u Hallo standaard wijzigt, moet u ervoor dat tooopen up Hallo die overeenkomt met het eindpunt in de volgende stap Hallo.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Hallo Docker communicatie-eindpunt toevoegen
Wanneer u bekijkt hello-resourcegroep die u hebt gemaakt, selecteert u Hallo Netwerkbeveiligingsgroep die zijn gekoppeld aan uw virtuele machine en klikt u op **regels voor binnenkomende beveiliging** tooview Hallo regels, zoals hier wordt weergegeven.

![](media/portal-use-docker/AddingEndpoint.png)

Klik op **+ toevoegen** tooadd die een andere regel, en voer een naam voor het Hallo-eindpunt in geval van Hallo-standaard (in dit voorbeeld **Docker**), en 2376 'Doelpoortbereik'. Hallo protocol waarde weer instellen **TCP**, en klik op **OK** toocreate Hallo regel.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Test uw Docker-Client en de Azure Docker-Host
Zoek en kopieer Hallo-naam van uw VM-domein en op de opdrachtregel Hallo van uw clientcomputer, het type `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (waarbij *dockerextension* wordt vervangen door Hallo subdomein voor uw virtuele machine).

Hallo resultaat moet vergelijkbaar toothis weergegeven:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Zodra u Hallo bovenstaande stappen hebt voltooid, hebt u nu een volledig functionele Docker-host waarop een virtuele machine van Azure, geconfigureerd toobe verbonden tooremotely van andere clients.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
U bent klaar toogo toohello [Docker-gebruikershandleiding] en de Docker-VM te gebruiken. Als u tooautomate Docker-hosts maken op Azure VM's via de opdrachtregelinterface wilt, Zie [hoe toouse Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[hoe toouse Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux Agent]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[Docker uitgevoerd met https]:http://docs.docker.com/articles/https/
[Docker-gebruikershandleiding]:https://docs.docker.com/userguide/
