---
title: aaaUse Docker Compose op een Linux VM in Azure | Microsoft Docs
description: Hoe Hallo toouse Docker en opstellen op Linux virtuele machines met Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="38d3d-103">Ophalen met Docker en opstellen toodefine gestart en het uitvoeren van een toepassing met meerdere container in Azure</span><span class="sxs-lookup"><span data-stu-id="38d3d-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="38d3d-104">Met [opstellen](http://github.com/docker/compose), u een eenvoudige tekst bestand toodefine gebruikt een toepassing die bestaat uit meerdere Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="38d3d-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="38d3d-105">U film van uw toepassing in één opdracht dat alles werkt toodeploy uw gedefinieerde omgeving.</span><span class="sxs-lookup"><span data-stu-id="38d3d-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="38d3d-106">Een voorbeeld: in dit artikel laat zien u hoe tooquickly ingesteld met een back-end een WordPress-blog MariaDB SQL-database op een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="38d3d-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="38d3d-107">U kunt ook tooset opstellen om complexere toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38d3d-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="38d3d-108">Instellen van een Linux-VM als Docker-host</span><span class="sxs-lookup"><span data-stu-id="38d3d-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="38d3d-109">U kunt verschillende Azure procedures en de beschikbare installatiekopieën of de Resource Manager-sjablonen gebruiken in hello Azure Marketplace toocreate een Linux-VM en ingesteld als een Docker-host.</span><span class="sxs-lookup"><span data-stu-id="38d3d-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="38d3d-110">Zie bijvoorbeeld [hello Docker VM-extensie toodeploy met uw omgeving](dockerextension.md) tooquickly een Ubuntu VM Hello Azure Docker VM-extensie maken met behulp van een [snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="38d3d-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="38d3d-111">Wanneer u Hallo Docker VM-extensie, uw virtuele machine is automatisch geconfigureerd als een Docker-host en Compose is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="38d3d-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="38d3d-112">Docker-host te maken met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="38d3d-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="38d3d-113">Meest recente installatie Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="38d3d-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="38d3d-114">Maak eerst een resourcegroep voor uw omgeving Docker met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="38d3d-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="38d3d-115">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie:</span><span class="sxs-lookup"><span data-stu-id="38d3d-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="38d3d-116">Vervolgens implementeert u een virtuele machine met [az implementatie maken](/cli/azure/group/deployment#create) waarin hello Azure Docker VM-extensie van [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="38d3d-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="38d3d-117">Uw eigen waarden opgeven voor *newStorageAccountName*, *adminUsername*, *adminPassword*, en *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="38d3d-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="38d3d-118">Het duurt enkele minuten duren voordat Hallo implementatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="38d3d-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="38d3d-119">Zodra het Hallo-implementatie is voltooid, [toonext stap verplaatsen](#verify-that-compose-is-installed) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="38d3d-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="38d3d-120">Tooinstead return besturingselement toohello-prompt en laat Hallo implementatie blijven op de achtergrond hello, voegt u desgewenst Hallo `--no-wait` toohello opdracht vóór markering.</span><span class="sxs-lookup"><span data-stu-id="38d3d-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="38d3d-121">Dit proces kunt u tooperform doorwerken in Hallo CLI tijdens het Hallo-implementatie blijft gedurende enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="38d3d-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="38d3d-122">Vervolgens kunt u meer informatie over de status van Hallo Docker-host met bekijken [az vm weergeven](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="38d3d-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="38d3d-123">Hallo volgende voorbeeld controleert Hallo status van virtuele machine met de naam Hallo *myDockerVM* (de standaardnaam van de sjabloon Hallo Hallo - deze naam niet wijzigen) in de resourcegroep Hallo met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="38d3d-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="38d3d-124">Wanneer deze opdracht retourneert *geslaagd*, Hallo-implementatie is voltooid en kunt u SSH toohello VM in Hallo volgende stap.</span><span class="sxs-lookup"><span data-stu-id="38d3d-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="38d3d-125">Controleren of Compose is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="38d3d-125">Verify that Compose is installed</span></span>
<span data-ttu-id="38d3d-126">Zodra het Hallo-implementatie is voltooid, SSH tooyour nieuwe Docker host Hallo DNS-naam u hebt opgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="38d3d-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="38d3d-127">U kunt `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details van uw virtuele machine, met inbegrip van Hallo DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="38d3d-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="38d3d-128">toocheck waaruit is geïnstalleerd op Hallo VM, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="38d3d-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="38d3d-129">Ziet u uitvoer ziet te*docker compose 1.6.2, 4d 72027 bouwen*.</span><span class="sxs-lookup"><span data-stu-id="38d3d-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="38d3d-130">Als u een andere methode toocreate een Docker-host gebruikt en tooinstall zelf samenstellen moet, Zie Hallo [documentatie opstellen](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="38d3d-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="38d3d-131">Maak een docker-compose.yml-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="38d3d-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="38d3d-132">Vervolgens maakt u een `docker-compose.yml` bestand, dat slechts een configuratie-tekstbestand, toodefine hello Docker containers toorun op Hallo VM is.</span><span class="sxs-lookup"><span data-stu-id="38d3d-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="38d3d-133">Hallo-bestand bevat Hallo installatiekopie toorun op elke container (of het mogelijk een build van een Dockerfile) nodig omgevingsvariabelen en afhankelijkheden, poorten en Hallo koppelingen tussen containers.</span><span class="sxs-lookup"><span data-stu-id="38d3d-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="38d3d-134">Zie voor meer informatie over yml file-syntaxis, [opstellen bestandsverwijzing](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="38d3d-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="38d3d-135">Hallo maken *docker-compose.yml* als volgt:</span><span class="sxs-lookup"><span data-stu-id="38d3d-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="38d3d-136">Gebruik uw favoriete text editor tooadd sommige toohello gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="38d3d-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="38d3d-137">Hallo volgende voorbeeld wordt Hallo *vi* editor:</span><span class="sxs-lookup"><span data-stu-id="38d3d-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="38d3d-138">Hallo voorbeeld te volgen in het tekstbestand plakken.</span><span class="sxs-lookup"><span data-stu-id="38d3d-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="38d3d-139">Deze configuratie wordt gebruikt voor afbeeldingen van Hallo [DockerHub register](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Hallo open-source weblog en inhoud management system) en een gekoppelde back-end MariaDB SQL-database.</span><span class="sxs-lookup"><span data-stu-id="38d3d-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="38d3d-140">Voer uw eigen *MYSQL_ROOT_PASSWORD* als volgt:</span><span class="sxs-lookup"><span data-stu-id="38d3d-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="38d3d-141">Start Hallo containers met opstellen</span><span class="sxs-lookup"><span data-stu-id="38d3d-141">Start hello containers with Compose</span></span>
<span data-ttu-id="38d3d-142">Hallo in dezelfde map als uw *docker-compose.yml* bestand Hallo volgende opdracht uitvoeren (afhankelijk van uw omgeving, moet u mogelijk toorun `docker-compose` met `sudo`):</span><span class="sxs-lookup"><span data-stu-id="38d3d-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="38d3d-143">Deze opdracht start Hallo Docker-containers opgegeven in *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="38d3d-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="38d3d-144">Het duurt enkele minuten duren voor deze stap toocomplete.</span><span class="sxs-lookup"><span data-stu-id="38d3d-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="38d3d-145">Ziet u uitvoer vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="38d3d-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="38d3d-146">Ervoor toouse Hallo worden **-d** optie op opstarten, zodat Hallo containers worden uitgevoerd op de achtergrond Hallo continu.</span><span class="sxs-lookup"><span data-stu-id="38d3d-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="38d3d-147">tooverify die Hallo containers, type `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="38d3d-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="38d3d-148">U ziet ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="38d3d-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="38d3d-149">U kunt nu verbinding tooWordPress rechtstreeks op Hallo VM op poort 80.</span><span class="sxs-lookup"><span data-stu-id="38d3d-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="38d3d-150">Open een webbrowser en Voer Hallo DNS-naam van uw virtuele machine (zoals `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="38d3d-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="38d3d-151">U ziet nu Hallo die WordPress startscherm, waarin u kunt Hallo installatie voltooien en aan de slag met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="38d3d-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![WordPress startscherm][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="38d3d-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38d3d-153">Next steps</span></span>
* <span data-ttu-id="38d3d-154">Ga toohello [Docker VM-extensie-gebruikershandleiding](https://github.com/Azure/azure-docker-extension/blob/master/README.md) voor meer opties tooconfigure Docker en opstellen in uw Docker-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="38d3d-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="38d3d-155">Bijvoorbeeld, is één optie tooput Hallo opstellen yml bestand (geconverteerde tooJSON) rechtstreeks in de configuratie Hallo Hallo Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="38d3d-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="38d3d-156">Bekijk Hallo [opstellen Naslaggids](http://docs.docker.com/compose/reference/) en [gebruikershandleiding](http://docs.docker.com/compose/) voor meer voorbeelden van het maken en implementeren van meerdere container apps.</span><span class="sxs-lookup"><span data-stu-id="38d3d-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="38d3d-157">Een Azure Resource Manager-sjabloon gebruiken uw eigen of een bijgedragen Hallo [community](https://azure.microsoft.com/documentation/templates/), toodeploy een Azure-VM met Docker en een toepassing die is ingesteld met opstellen.</span><span class="sxs-lookup"><span data-stu-id="38d3d-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="38d3d-158">Bijvoorbeeld, Hallo [implementeren van een WordPress-blog met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) sjabloon worden gebruikt voor Docker en opstellen tooquickly WordPress implementeert met een MySQL-back-end op een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="38d3d-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="38d3d-159">Probeer de integratie van Docker Compose met een Docker Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="38d3d-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="38d3d-160">Zie [met behulp van opstellen met Swarm](https://docs.docker.com/compose/swarm/) voor scenario's.</span><span class="sxs-lookup"><span data-stu-id="38d3d-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
