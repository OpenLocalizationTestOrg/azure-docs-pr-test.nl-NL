---
title: aaaUse Docker-Machine toocreate Linux wordt gehost in Azure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Docker-Machine toocreate Docker-hosts in Azure.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a><span data-ttu-id="5279c-103">Hoe toouse Docker-Machine toocreate gehost in Azure</span><span class="sxs-lookup"><span data-stu-id="5279c-103">How toouse Docker Machine toocreate hosts in Azure</span></span>
<span data-ttu-id="5279c-104">Dit artikel details hoe toouse [Docker-Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span><span class="sxs-lookup"><span data-stu-id="5279c-104">This article details how toouse [Docker Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span></span> <span data-ttu-id="5279c-105">Hallo `docker-machine` opdracht maakt u een Linux-virtuele machine (VM) in Azure vervolgens Docker geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5279c-105">hello `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="5279c-106">U kunt uw Docker-hosts in het gebruik van Azure beheren Hallo dezelfde lokale hulpprogramma's en werkstromen.</span><span class="sxs-lookup"><span data-stu-id="5279c-106">You can then manage your Docker hosts in Azure using hello same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="5279c-107">Virtuele machines met Docker-Machine maken</span><span class="sxs-lookup"><span data-stu-id="5279c-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="5279c-108">Eerst moet u uw Azure-abonnement-ID met [az account weergeven](/cli/azure/account#show) als volgt:</span><span class="sxs-lookup"><span data-stu-id="5279c-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="5279c-109">Maken van virtuele machines Docker-host in Azure met `docker-machine create` door te geven *azure* als Hallo-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="5279c-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as hello driver.</span></span> <span data-ttu-id="5279c-110">Zie voor meer informatie, Hallo [Docker Azure stuurprogramma-documentatie](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="5279c-110">For more information, see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="5279c-111">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*, maakt u een gebruikersaccount met de naam *azureuser*, en poort geopend *80* hosten op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="5279c-111">hello following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on hello host VM.</span></span> <span data-ttu-id="5279c-112">Volg alle prompts toolog in tooyour Azure-account en Docker-Machine machtigingen toocreate verlenen en beheren van resources.</span><span class="sxs-lookup"><span data-stu-id="5279c-112">Follow any prompts toolog in tooyour Azure account and grant Docker Machine permissions toocreate and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="5279c-113">Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5279c-113">hello output looks similar toohello following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="5279c-114">De Docker-shell configureren</span><span class="sxs-lookup"><span data-stu-id="5279c-114">Configure your Docker shell</span></span>
<span data-ttu-id="5279c-115">tooconnect tooyour Docker-host in Azure, de juiste verbindingsinstellingen Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="5279c-115">tooconnect tooyour Docker host in Azure, define hello appropriate connection settings.</span></span> <span data-ttu-id="5279c-116">Zoals eerder aan Hallo einde van Hallo uitvoer, als volgt Hallo verbindingsgegevens voor de Docker-host weergeven:</span><span class="sxs-lookup"><span data-stu-id="5279c-116">As noted at hello end of hello output, view hello connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="5279c-117">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5279c-117">hello output is similar toohello following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="5279c-118">Hallo-verbindingsinstellingen voor de toodefine kunt u beide uitvoeren Hallo voorgestelde configuratieopdracht (`eval $(docker-machine env myvmdocker)`), of u kunt de omgevingsvariabelen Hallo handmatig instellen.</span><span class="sxs-lookup"><span data-stu-id="5279c-118">toodefine hello connection settings you can either run hello suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set hello environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="5279c-119">Een container worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5279c-119">Run a container</span></span>
<span data-ttu-id="5279c-120">toosee een container in actie, kunt een eenvoudige NGINX-webserver uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5279c-120">toosee a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="5279c-121">Maken van een container met `docker run` en weer te geven van poort 80 voor internetverkeer als volgt:</span><span class="sxs-lookup"><span data-stu-id="5279c-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="5279c-122">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5279c-122">hello output is similar toohello following example:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="5279c-123">Weergave actieve containers met `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="5279c-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="5279c-124">Hallo volgende voorbeelduitvoer wordt weergegeven Hallo NGINX-container met met poort 80 weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5279c-124">hello following example output shows hello NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a><span data-ttu-id="5279c-125">Test Hallo container</span><span class="sxs-lookup"><span data-stu-id="5279c-125">Test hello container</span></span>
<span data-ttu-id="5279c-126">Hallo openbaar IP-adres van Docker-host als volgt verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="5279c-126">Obtain hello public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="5279c-127">toosee hello container in actie, open een webbrowser en Voer Hallo openbare IP-adres hebt genoteerd in Hallo-uitvoer van de voorgaande opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5279c-127">toosee hello container in action, open a web browser and enter hello public IP address noted in hello output of hello preceding command:</span></span>

![Actieve ngnix container](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="5279c-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5279c-129">Next steps</span></span>
<span data-ttu-id="5279c-130">U kunt ook hosts maken met de Hallo [Docker VM-extensie](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="5279c-130">You can also create hosts with hello [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="5279c-131">Zie voor voorbeelden op met behulp van Docker Compose [aan de slag met Docker en opstellen in Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="5279c-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
