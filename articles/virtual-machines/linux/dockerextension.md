---
title: aaaUse hello Azure Docker VM-extensie | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Docker VM-extensie tooquickly en veilig implementeert een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen en hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="dc89c-103">Maakt een Docker-omgeving in Azure met behulp van Hallo Docker VM-extensie</span><span class="sxs-lookup"><span data-stu-id="dc89c-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="dc89c-104">Docker is een populair containerbeheer en installatiekopieën platform waarmee u tooquickly werken met containers op Linux.</span><span class="sxs-lookup"><span data-stu-id="dc89c-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="dc89c-105">In Azure zijn er verschillende manieren waarop u Docker volgens tooyour behoeften kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="dc89c-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="dc89c-106">Dit artikel is gericht op het gebruik van Hallo Docker VM-extensie en Azure Resource Manager-sjablonen met hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="dc89c-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="dc89c-107">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dc89c-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="dc89c-108">Overzicht van Azure Docker VM-extensie</span><span class="sxs-lookup"><span data-stu-id="dc89c-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="dc89c-109">Hello Azure Docker VM-extensie installeert en configureert u het Hallo Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="dc89c-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="dc89c-110">U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van Hallo Docker-host met behulp van hello Azure Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="dc89c-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="dc89c-111">Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg hello Azure Docker VM-extensie is geschikt voor krachtiger developer- of productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="dc89c-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="dc89c-112">Zie voor meer informatie over Hallo verschillende implementatiemethoden, inclusief het gebruik van Docker-Machine en de Azure-Container Services Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dc89c-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="dc89c-113">tooquickly prototype een app, kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="dc89c-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="dc89c-114">toobuild gereed is voor productie, schaalbare omgevingen die extra hulpprogramma's voor planning en beheer bieden, u kunt een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="dc89c-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="dc89c-115">Een sjabloon met hello Azure Docker VM-extensie implementeren</span><span class="sxs-lookup"><span data-stu-id="dc89c-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="dc89c-116">Laten we gebruik van een bestaande sjabloon Quick Start-toocreate een Ubuntu VM die gebruikmaakt van hello Azure Docker VM-extensie tooinstall en Hallo Docker host configureren.</span><span class="sxs-lookup"><span data-stu-id="dc89c-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="dc89c-117">U kunt hier Hallo sjabloon weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="dc89c-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="dc89c-118">Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="dc89c-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="dc89c-119">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="dc89c-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="dc89c-120">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie:</span><span class="sxs-lookup"><span data-stu-id="dc89c-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="dc89c-121">Vervolgens implementeert u een virtuele machine met [az implementatie maken](/cli/azure/group/deployment#create) waarin hello Azure Docker VM-extensie van [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="dc89c-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="dc89c-122">Uw eigen waarden opgeven voor *newStorageAccountName*, *adminUsername*, *adminPassword*, en *dnsNameForPublicIP* als volgt:</span><span class="sxs-lookup"><span data-stu-id="dc89c-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="dc89c-123">Het duurt enkele minuten duren voordat Hallo implementatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="dc89c-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="dc89c-124">Zodra het Hallo-implementatie is voltooid, [toonext stap verplaatsen](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="dc89c-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="dc89c-125">Tooinstead return besturingselement toohello-prompt en laat Hallo implementatie blijven op de achtergrond hello, voegt u desgewenst Hallo `--no-wait` toohello opdracht vóór markering.</span><span class="sxs-lookup"><span data-stu-id="dc89c-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="dc89c-126">Dit proces kunt u tooperform doorwerken in Hallo CLI tijdens het Hallo-implementatie blijft gedurende enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="dc89c-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="dc89c-127">Vervolgens kunt u meer informatie over de status van Hallo Docker-host met bekijken [az vm weergeven](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="dc89c-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="dc89c-128">Hallo volgende voorbeeld controleert Hallo status van virtuele machine met de naam Hallo *myDockerVM* (de standaardnaam van de sjabloon Hallo Hallo - deze naam niet wijzigen) in de resourcegroep Hallo met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="dc89c-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="dc89c-129">Wanneer deze opdracht retourneert *geslaagd*, Hallo-implementatie is voltooid en kunt u SSH toohello VM in Hallo volgende stap.</span><span class="sxs-lookup"><span data-stu-id="dc89c-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="dc89c-130">Uw eerste nginx-container implementeren</span><span class="sxs-lookup"><span data-stu-id="dc89c-130">Deploy your first nginx container</span></span>
<span data-ttu-id="dc89c-131">tooview details van uw virtuele machine, inclusief Hallo DNS-naam gebruiken `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="dc89c-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="dc89c-132">SSH tooyour nieuwe Docker hosten van uw lokale computer als volgt:</span><span class="sxs-lookup"><span data-stu-id="dc89c-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="dc89c-133">Wanneer toohello aangemeld met Docker-host, gaan we een nginx-container te uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="dc89c-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="dc89c-134">Hallo-uitvoer is vergelijkbaar toohello na voorbeeld Hallo nginx installatiekopie gedownload en een container gestart:</span><span class="sxs-lookup"><span data-stu-id="dc89c-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="dc89c-135">Controleer de status Hallo van Hallo-containers die zijn uitgevoerd op uw host Docker als volgt:</span><span class="sxs-lookup"><span data-stu-id="dc89c-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="dc89c-136">Hallo-uitvoer is vergelijkbaar toohello voorbeeld te volgen, die Hallo nginx-container met actief is en TCP-poorten 80 en 443 en ernaar worden doorgestuurd:</span><span class="sxs-lookup"><span data-stu-id="dc89c-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="dc89c-137">toosee uw container in actie, open een webbrowser boven en Voer Hallo DNS-naam van de Docker-host:</span><span class="sxs-lookup"><span data-stu-id="dc89c-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="dc89c-139">Azure Docker VM-sjabloon uitbreidingsverwijzing</span><span class="sxs-lookup"><span data-stu-id="dc89c-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="dc89c-140">het vorige voorbeeld Hallo maakt gebruik van een bestaande Quick Start-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="dc89c-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="dc89c-141">U kunt ook hello Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="dc89c-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="dc89c-142">toodo toevoegen dus Hallo tooyour Resource Manager-sjablonen te volgen, Hallo definiëren `vmName` van uw virtuele machine op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="dc89c-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="dc89c-143">U vindt meer gedetailleerde stapsgewijze instructies over het gebruik van Resource Manager-sjablonen door te lezen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc89c-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc89c-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc89c-144">Next steps</span></span>
<span data-ttu-id="dc89c-145">U kunt desgewenst te[hello Docker-daemon TCP-poort configureren](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), begrijpen [Docker beveiliging](https://docs.docker.com/engine/security/security/), of met behulp van containers implementeren [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="dc89c-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="dc89c-146">Zie voor meer informatie over hello Azure Docker VM-extensie zichzelf Hallo [GitHub project](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="dc89c-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="dc89c-147">Lees meer informatie over Hallo aanvullende Docker implementatieopties in Azure:</span><span class="sxs-lookup"><span data-stu-id="dc89c-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="dc89c-148">Docker-Machine Hello Azure stuurprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc89c-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="dc89c-149">[Aan de slag met Docker Compose toodefine en een toepassing met meerdere container uitvoert op een virtuele machine van Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="dc89c-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="dc89c-150">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="dc89c-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

