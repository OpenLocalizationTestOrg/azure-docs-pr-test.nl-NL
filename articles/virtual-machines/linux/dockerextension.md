---
title: Gebruik de Azure Docker VM-extensie | Microsoft Docs
description: Informatie over het gebruik van de Docker-VM-extensie voor het snel en veilig implementeren van een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen en Azure CLI 2.0
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
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="d11d9-103">Maakt een Docker-omgeving in Azure met behulp van de Docker-VM-extensie</span><span class="sxs-lookup"><span data-stu-id="d11d9-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="d11d9-104">Docker is een populair containerbeheer en installatiekopieën platform waarmee u snel werken met containers op Linux.</span><span class="sxs-lookup"><span data-stu-id="d11d9-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="d11d9-105">In Azure zijn er verschillende manieren waarop u kunt Docker implementeren volgens uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="d11d9-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="d11d9-106">Dit artikel is gericht op het gebruik van de Docker-VM-extensie en Azure Resource Manager-sjablonen met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="d11d9-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="d11d9-107">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d11d9-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="d11d9-108">Overzicht van Azure Docker VM-extensie</span><span class="sxs-lookup"><span data-stu-id="d11d9-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="d11d9-109">De virtuele machine in Azure Docker-extensie installeert en configureert u de Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="d11d9-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="d11d9-110">U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van de Docker-host met behulp van de virtuele machine in Azure Docker-extensie.</span><span class="sxs-lookup"><span data-stu-id="d11d9-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="d11d9-111">Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg dat de virtuele machine in Azure Docker-extensie is geschikt voor krachtiger developer- of productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="d11d9-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="d11d9-112">Zie voor meer informatie over de verschillende implementatiemethoden, met behulp van Docker-Machine en Services van Azure-Container, inclusief de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="d11d9-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="d11d9-113">Snel prototype een app kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="d11d9-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="d11d9-114">Gereed voor productie, schaalbare omgevingen die aanvullende plannings- en hulpprogramma's bieden bouwen, kunt u implementeren een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d11d9-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="d11d9-115">Een sjabloon met de extensie Azure Docker VM implementeren</span><span class="sxs-lookup"><span data-stu-id="d11d9-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="d11d9-116">We gebruiken een bestaande sjabloon voor de Quick Start voor het maken van een Ubuntu VM die gebruikmaakt van de virtuele machine in Azure Docker-uitbreiding installeren en configureren van de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="d11d9-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="d11d9-117">U kunt de sjabloon hier weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d11d9-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="d11d9-118">U moet de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d11d9-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d11d9-119">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d11d9-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d11d9-120">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *westus* locatie:</span><span class="sxs-lookup"><span data-stu-id="d11d9-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="d11d9-121">Vervolgens implementeert u een virtuele machine met [az implementatie maken](/cli/azure/group/deployment#create) waarin de Azure Docker VM-extensie van [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d11d9-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="d11d9-122">Uw eigen waarden opgeven voor *newStorageAccountName*, *adminUsername*, *adminPassword*, en *dnsNameForPublicIP* als volgt:</span><span class="sxs-lookup"><span data-stu-id="d11d9-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="d11d9-123">Het duurt enkele minuten duren voordat de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d11d9-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="d11d9-124">Zodra de implementatie is voltooid, [verplaatsen naar de volgende stap](#deploy-your-first-nginx-container) naar SSH met uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d11d9-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="d11d9-125">Voeg desgewenst in plaats daarvan om terug te beheren op de vraag en kunt de implementatie op de achtergrond voortgezet, de `--no-wait` vlag naar de voorgaande opdracht.</span><span class="sxs-lookup"><span data-stu-id="d11d9-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="d11d9-126">Dit proces kunt u andere taken uitvoeren in de CLI tijdens de implementatie gedurende enkele minuten blijft.</span><span class="sxs-lookup"><span data-stu-id="d11d9-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="d11d9-127">Vervolgens kunt u meer informatie over de hoststatus Docker met bekijken [az vm weergeven](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="d11d9-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="d11d9-128">Het volgende voorbeeld controleert de status van de virtuele machine met de naam *myDockerVM* (de standaardnaam van de sjabloon - geen deze naam niet wijzigen) in de resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d11d9-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="d11d9-129">Wanneer deze opdracht retourneert *geslaagd*, de implementatie is voltooid en kunt u SSH naar de virtuele machine in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="d11d9-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="d11d9-130">Uw eerste nginx-container implementeren</span><span class="sxs-lookup"><span data-stu-id="d11d9-130">Deploy your first nginx container</span></span>
<span data-ttu-id="d11d9-131">Gebruiken om de details van uw virtuele machine, met inbegrip van de DNS-naam te geven `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="d11d9-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="d11d9-132">SSH kunt uitvoeren naar uw nieuwe Docker hosten van uw lokale computer als volgt:</span><span class="sxs-lookup"><span data-stu-id="d11d9-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="d11d9-133">Wanneer aangemeld bij de Docker-host, gaan we een nginx-container te uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d11d9-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="d11d9-134">De uitvoer is vergelijkbaar met het volgende voorbeeld wordt de nginx-installatiekopie gedownload en een container gestart:</span><span class="sxs-lookup"><span data-stu-id="d11d9-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="d11d9-135">Controleer de status van de containers die wordt uitgevoerd op uw host Docker als volgt:</span><span class="sxs-lookup"><span data-stu-id="d11d9-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="d11d9-136">De uitvoer is vergelijkbaar met het volgende voorbeeld, waaruit blijkt dat de nginx-container actief is en TCP-poorten 80 en 443 en ernaar worden doorgestuurd:</span><span class="sxs-lookup"><span data-stu-id="d11d9-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="d11d9-137">De container in actie zien, opent u een webbrowser en voer de DNS-naam van de Docker-host:</span><span class="sxs-lookup"><span data-stu-id="d11d9-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="d11d9-139">Azure Docker VM-sjabloon uitbreidingsverwijzing</span><span class="sxs-lookup"><span data-stu-id="d11d9-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="d11d9-140">Het vorige voorbeeld maakt gebruik van een bestaande Quick Start-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d11d9-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="d11d9-141">U kunt ook de Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="d11d9-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="d11d9-142">Om dit te doen, kunt u het volgende toevoegen aan de Resource Manager-sjablonen, definiëren de `vmName` van uw virtuele machine op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="d11d9-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="d11d9-143">U vindt meer gedetailleerde stapsgewijze instructies over het gebruik van Resource Manager-sjablonen door te lezen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d11d9-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d11d9-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d11d9-144">Next steps</span></span>
<span data-ttu-id="d11d9-145">U kunt desgewenst [de Docker-daemon TCP-poort configureren](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), begrijpen [Docker-beveiliging](https://docs.docker.com/engine/security/security/), of met behulp van containers implementeren [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="d11d9-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="d11d9-146">Zie voor meer informatie over de Azure Docker VM-extensie zichzelf, het [GitHub project](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="d11d9-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="d11d9-147">Lees meer informatie over de extra Docker implementatie-opties in Azure:</span><span class="sxs-lookup"><span data-stu-id="d11d9-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="d11d9-148">Docker-Machine met het Azure-stuurprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="d11d9-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="d11d9-149">[Aan de slag met Docker en opstellen om te definiëren en een toepassing met meerdere container uitvoert op een virtuele machine van Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="d11d9-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="d11d9-150">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="d11d9-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

