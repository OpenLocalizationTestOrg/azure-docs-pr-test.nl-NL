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
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="a36f2-103">Met behulp van Docker VM-extensie Hallo Hello klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a36f2-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="a36f2-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a36f2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a36f2-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a36f2-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a36f2-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a36f2-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="a36f2-107">[Docker](https://www.docker.com/) is een van de Hallo populairste virtualisatie-methoden die gebruikmaakt van [Linux containers](http://en.wikipedia.org/wiki/LXC) in plaats van virtuele machines als een manier om gegevens te isoleren en berekeningen op gedeelde bronnen.</span><span class="sxs-lookup"><span data-stu-id="a36f2-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="a36f2-108">U kunt Hallo Docker VM-extensie beheerd door [Azure Linux Agent] toocreate een Docker-virtuele machine die als host fungeert voor een onbeperkt aantal containers voor uw toepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="a36f2-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="a36f2-109">Dit onderwerp wordt beschreven hoe toocreate een Docker VM van Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a36f2-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="a36f2-110">hoe toocreate een Docker-virtuele machine op de opdrachtregel hello, Zie toosee [hoe toouse Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)].</span><span class="sxs-lookup"><span data-stu-id="a36f2-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="a36f2-111">een hoog niveau bespreking van containers en hun voordelen toosee Zie Hallo [Docker hoog niveau Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="a36f2-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="a36f2-112">Een nieuwe virtuele machine maken vanuit Hallo installatiekopie galerie</span><span class="sxs-lookup"><span data-stu-id="a36f2-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="a36f2-113">de eerste stap Hallo vereist een Azure-VM uit een Linux-installatiekopie die ondersteuning biedt voor Hallo Docker VM-extensie, de installatiekopie van een Ubuntu 14.04 TNS vanaf Hallo installatiekopie galerie met als een serverinstallatiekopie voorbeeld en Ubuntu 14.04 bureaublad als een client.</span><span class="sxs-lookup"><span data-stu-id="a36f2-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="a36f2-114">Klik in de portal Hallo op **+ nieuw** in Hallo linksonder hoek toocreate een nieuw exemplaar van de virtuele machine en selecteer de installatiekopie van een Ubuntu 14.04 TNS van beschikbare Hallo selecties of van Hallo voltooien installatiekopie galerie, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a36f2-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="a36f2-115">Op dit moment ondersteunen alleen Ubuntu 14.04 TNS afbeeldingen recenter dan juli 2014 Hallo Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="a36f2-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Maak een nieuwe Ubuntu-afbeelding](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="a36f2-117">Docker-certificaten maken</span><span class="sxs-lookup"><span data-stu-id="a36f2-117">Create Docker Certificates</span></span>
<span data-ttu-id="a36f2-118">Zorg ervoor dat de Docker is geïnstalleerd op de clientcomputer na Hallo die VM is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a36f2-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="a36f2-119">(Zie voor meer informatie [Docker-installatie-instructies](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="a36f2-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="a36f2-120">Hallo certificaat en de sleutel-bestanden maken voor Docker-communicatie te volgens[Docker uitgevoerd met https] en plaats deze in Hallo  **`~/.docker`**  map op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="a36f2-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="a36f2-121">Hallo Docker VM-extensie in Hallo-portal op dit moment zijn referenties nodig met base64-gecodeerd zijn.</span><span class="sxs-lookup"><span data-stu-id="a36f2-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="a36f2-122">Op de opdrachtregel hello gebruiken  **`base64`**  of een andere favoriet toocreate base64-gecodeerd onderwerpen met betrekking tot codering.</span><span class="sxs-lookup"><span data-stu-id="a36f2-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="a36f2-123">Dit wordt uitgevoerd met een eenvoudige reeks certificaat en de sleutel bestanden eruit vergelijkbare toothis:</span><span class="sxs-lookup"><span data-stu-id="a36f2-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

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

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="a36f2-124">Hallo Docker VM-extensie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a36f2-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="a36f2-125">tooadd hello Docker VM-extensie, zoekt u VM-instantie Hallo u hebt gemaakt en schuif naar beneden te**extensies** en klik op de toobring van VM-extensies, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a36f2-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="a36f2-126">Deze functionaliteit wordt ondersteund in alleen Hallo preview-portal: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="a36f2-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="a36f2-127">Toevoegen van een uitbreiding</span><span class="sxs-lookup"><span data-stu-id="a36f2-127">Add an Extension</span></span>
<span data-ttu-id="a36f2-128">Klik op Hallo **+ toevoegen** toodisplay Hallo mogelijke VM-extensies kunt u toothis VM toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a36f2-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="a36f2-129">Selecteer Hallo Docker VM-extensie</span><span class="sxs-lookup"><span data-stu-id="a36f2-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="a36f2-130">Kies Hallo Docker VM-extensie, die Hallo Docker beschrijving en belangrijke koppelingen wordt, en klik vervolgens op **maken** op Hallo onder toobegin Hallo-installatieprocedure.</span><span class="sxs-lookup"><span data-stu-id="a36f2-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="a36f2-131">Het certificaat en de sleutelbestanden toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a36f2-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="a36f2-132">Voer in formuliervelden hello, Hallo base64-gecodeerd versies van uw CA-certificaat, het servercertificaat en de sleutel van uw Server, zoals wordt weergegeven in de volgende afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="a36f2-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="a36f2-133">Houd er rekening mee dat (zoals in hello voorafgaand aan de installatiekopie) Hallo 2376 wordt gevuld standaard.</span><span class="sxs-lookup"><span data-stu-id="a36f2-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="a36f2-134">Kunt u hier een willekeurig eindpunt Hallo volgende stap worden echter tooopen up Hallo die overeenkomt met eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a36f2-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="a36f2-135">Als u Hallo standaard wijzigt, moet u ervoor dat tooopen up Hallo die overeenkomt met het eindpunt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="a36f2-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="a36f2-136">Hallo Docker communicatie-eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="a36f2-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="a36f2-137">Wanneer u bekijkt hello-resourcegroep die u hebt gemaakt, selecteert u Hallo Netwerkbeveiligingsgroep die zijn gekoppeld aan uw virtuele machine en klikt u op **regels voor binnenkomende beveiliging** tooview Hallo regels, zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a36f2-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="a36f2-138">Klik op **+ toevoegen** tooadd die een andere regel, en voer een naam voor het Hallo-eindpunt in geval van Hallo-standaard (in dit voorbeeld **Docker**), en 2376 'Doelpoortbereik'.</span><span class="sxs-lookup"><span data-stu-id="a36f2-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="a36f2-139">Hallo protocol waarde weer instellen **TCP**, en klik op **OK** toocreate Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="a36f2-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="a36f2-140">Test uw Docker-Client en de Azure Docker-Host</span><span class="sxs-lookup"><span data-stu-id="a36f2-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="a36f2-141">Zoek en kopieer Hallo-naam van uw VM-domein en op de opdrachtregel Hallo van uw clientcomputer, het type `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (waarbij *dockerextension* wordt vervangen door Hallo subdomein voor uw virtuele machine).</span><span class="sxs-lookup"><span data-stu-id="a36f2-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="a36f2-142">Hallo resultaat moet vergelijkbaar toothis weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a36f2-142">hello result should appear similar toothis:</span></span>

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

<span data-ttu-id="a36f2-143">Zodra u Hallo bovenstaande stappen hebt voltooid, hebt u nu een volledig functionele Docker-host waarop een virtuele machine van Azure, geconfigureerd toobe verbonden tooremotely van andere clients.</span><span class="sxs-lookup"><span data-stu-id="a36f2-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="a36f2-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a36f2-144">Next steps</span></span>
<span data-ttu-id="a36f2-145">U bent klaar toogo toohello [Docker-gebruikershandleiding] en de Docker-VM te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a36f2-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="a36f2-146">Als u tooautomate Docker-hosts maken op Azure VM's via de opdrachtregelinterface wilt, Zie [hoe toouse Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)]</span><span class="sxs-lookup"><span data-stu-id="a36f2-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

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
