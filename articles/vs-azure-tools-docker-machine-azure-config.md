---
title: aaaCreate Docker-hosts in Azure met Docker-Machine | Microsoft Docs
description: Beschrijving van de Docker-Machine toocreate docker-hosts in Azure.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="b8d1e-103">Docker-hosts in Azure maken met Docker-Machine</span><span class="sxs-lookup"><span data-stu-id="b8d1e-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="b8d1e-104">Met [Docker](https://www.docker.com/) containers vereist een host VM actieve Hallo docker-daemon.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="b8d1e-105">Dit onderwerp wordt beschreven hoe toouse hello [docker-machine](https://docs.docker.com/machine/) opdracht toocreate nieuwe Linux-VM's geconfigureerd met Hallo Docker-daemon worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="b8d1e-106">**Opmerking:**</span><span class="sxs-lookup"><span data-stu-id="b8d1e-106">**Note:**</span></span> 

* <span data-ttu-id="b8d1e-107">*In dit artikel hangt samen met docker-machine versie 0.9.0-rc2 of hoger*</span><span class="sxs-lookup"><span data-stu-id="b8d1e-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="b8d1e-108">*Windows-Containers worden ondersteund via de docker-machine in Hallo nabije toekomst*</span><span class="sxs-lookup"><span data-stu-id="b8d1e-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="b8d1e-109">Virtuele machines met Docker-Machine maken</span><span class="sxs-lookup"><span data-stu-id="b8d1e-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="b8d1e-110">Docker host virtuele machines in Azure maken met de Hallo `docker-machine create` opdracht met Hallo `azure` stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="b8d1e-111">Hello Azure stuurprogramma is vereist voor uw abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="b8d1e-112">U kunt Hallo [Azure CLI](cli-install-nodejs.md) of Hallo [Azure Portal](https://portal.azure.com) tooretrieve uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="b8d1e-113">**Met behulp van hello Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="b8d1e-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="b8d1e-114">Selecteer **abonnementen** van Hallo linkernavigatievenster pagina en kopieer Hallo abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="b8d1e-115">**Hello Azure CLI gebruiken**</span><span class="sxs-lookup"><span data-stu-id="b8d1e-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="b8d1e-116">Type ```azure account list``` en kopiëren Hallo abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="b8d1e-117">Type `docker-machine create --driver azure` toosee Hallo opties en hun standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="b8d1e-118">U ziet ook Hallo [Docker Azure stuurprogramma documentatie](https://docs.docker.com/machine/drivers/azure/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="b8d1e-119">Hallo volgende voorbeeld is afhankelijk van Hallo [standaardwaarden](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), maar eventueel deze waarden ingesteld:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="b8d1e-120">Azure dns voor Hallo-naam die is gekoppeld aan de openbare IP-adres Hallo en certificaten die zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="b8d1e-121">Dit is Hallo DNS-naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="b8d1e-122">Hallo VM kan vervolgens veilig stoppen, vrijgeven Hallo dynamische IP en Hallo mogelijkheid tooreconnect nadat Hallo vm wordt opnieuw met een nieuwe IP-adres gestart opgeven.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="b8d1e-123">Hallo-voorvoegsel moet uniek zijn voor deze regio UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="b8d1e-124">Open poort 80 op Hallo VM voor uitgaande internetverbinding</span><span class="sxs-lookup"><span data-stu-id="b8d1e-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="b8d1e-125">grootte van Hallo VM tooutilize sneller premium-opslag</span><span class="sxs-lookup"><span data-stu-id="b8d1e-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="b8d1e-126">Premium-opslag gebruikt voor Hallo vm-schijf</span><span class="sxs-lookup"><span data-stu-id="b8d1e-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="b8d1e-127">Kies een host docker met docker-machine</span><span class="sxs-lookup"><span data-stu-id="b8d1e-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="b8d1e-128">Zodra u een vermelding in de docker-machine voor de host hebt, kunt u Hallo standaardhost kunt instellen wanneer docker opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="b8d1e-129">PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="b8d1e-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="b8d1e-130">Met behulp van Bash</span><span class="sxs-lookup"><span data-stu-id="b8d1e-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="b8d1e-131">U kunt nu docker-opdrachten uitvoeren op de opgegeven host Hallo</span><span class="sxs-lookup"><span data-stu-id="b8d1e-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="b8d1e-132">Een container worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="b8d1e-132">Run a container</span></span>
<span data-ttu-id="b8d1e-133">U kunt nu een eenvoudige web server tootest uitvoeren met een host die is geconfigureerd, of de host correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="b8d1e-134">Hier wordt een installatiekopie van het standaard nginx gebruiken, geeft u het moet luisteren op poort 80, en als Hallo host VM opnieuw wordt opgestart, wordt de container Hallo wordt opnieuw gestart ook (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="b8d1e-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="b8d1e-135">Hallo-uitvoer ziet er ongeveer als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="b8d1e-136">Test Hallo container</span><span class="sxs-lookup"><span data-stu-id="b8d1e-136">Test hello container</span></span>
<span data-ttu-id="b8d1e-137">Bekijk actieve containers met `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="b8d1e-138">En toosee Hallo-container, type uitgevoerd `docker-machine ip <VM name>` toofind Hallo IP-adres tooenter in Hallo browser:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Actieve ngnix container](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="b8d1e-140">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b8d1e-140">Summary</span></span>
<span data-ttu-id="b8d1e-141">U kunt eenvoudig docker-hosts in Azure voor uw afzonderlijke docker host validaties met docker-machine inrichten.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="b8d1e-142">Voor productie Hallo hosting van containers, Zie [Azure Container Service](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="b8d1e-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="b8d1e-143">toodevelop .NET Core-toepassingen met Visual Studio, Zie [Docker-Tools voor Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="b8d1e-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

