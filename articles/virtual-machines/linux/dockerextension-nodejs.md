---
title: De virtuele machine in Azure Docker-uitbreiding gebruiken met de Azure CLI 1.0 | Microsoft Docs
description: Informatie over het gebruik van de Docker-VM-extensie voor het snel en veilig implementeren van een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a3cbcf63533f4042dcd695e141655c5814bd7068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension-with-the-azure-cli-10"></a><span data-ttu-id="79824-103">Maakt een Docker-omgeving in Azure met behulp van de Docker-VM-extensie met de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="79824-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="79824-104">Docker is een populair containerbeheer en installatiekopieën platform waarmee u snel werken met containers op Linux (en ook Windows).</span><span class="sxs-lookup"><span data-stu-id="79824-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="79824-105">In Azure zijn er verschillende manieren waarop u kunt Docker implementeren volgens uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="79824-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="79824-106">Dit artikel is gericht op het gebruik van de Docker-VM-extensie en Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="79824-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="79824-107">Zie voor meer informatie over de verschillende implementatiemethoden, met behulp van Docker-Machine en Services van Azure-Container, inclusief de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="79824-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="79824-108">Snel prototype een app kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="79824-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="79824-109">Voor grotere, stabiele omgevingen, kunt u de virtuele machine in Azure Docker-uitbreiding biedt ook ondersteuning voor [Docker Compose](https://docs.docker.com/compose/overview/) consistente containerimplementaties te genereren.</span><span class="sxs-lookup"><span data-stu-id="79824-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span></span> <span data-ttu-id="79824-110">Dit artikel gegevens met behulp van de virtuele machine in Azure Docker-extensie.</span><span class="sxs-lookup"><span data-stu-id="79824-110">This article details using the Azure Docker VM extension.</span></span>
* <span data-ttu-id="79824-111">Gereed voor productie, schaalbare omgevingen die aanvullende plannings- en hulpprogramma's bieden bouwen, kunt u implementeren een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="79824-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="79824-112">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="79824-112">CLI versions to complete the task</span></span>
<span data-ttu-id="79824-113">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="79824-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="79824-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="79824-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="79824-115">[Azure CLI 2.0](dockerextension.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="79824-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for the resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="79824-116">Overzicht van Azure Docker VM-extensie</span><span class="sxs-lookup"><span data-stu-id="79824-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="79824-117">De virtuele machine in Azure Docker-extensie installeert en configureert u de Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="79824-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="79824-118">U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van de Docker-host met behulp van de virtuele machine in Azure Docker-extensie.</span><span class="sxs-lookup"><span data-stu-id="79824-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="79824-119">Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg dat de virtuele machine in Azure Docker-extensie is geschikt voor krachtiger developer- of productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="79824-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="79824-120">Azure Resource Manager-sjablonen definiëren de volledige structuur van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="79824-120">Azure Resource Manager templates define the entire structure of your environment.</span></span> <span data-ttu-id="79824-121">Sjablonen kunt u maken en configureren van resources, zoals de Docker-host virtuele machines, opslag, op rollen gebaseerde toegangsbeheer (RBAC) en diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="79824-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="79824-122">U kunt deze sjablonen voor het maken van aanvullende implementaties op een consistente manier hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="79824-122">You can reuse these templates to create additional deployments in a consistent manner.</span></span> <span data-ttu-id="79824-123">Zie voor meer informatie over Azure Resource Manager en sjablonen [overzicht van Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79824-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="79824-124">Een sjabloon met de extensie Azure Docker VM implementeren</span><span class="sxs-lookup"><span data-stu-id="79824-124">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="79824-125">We gebruiken een bestaande sjabloon voor de Quick Start voor het maken van een Ubuntu VM die gebruikmaakt van de virtuele machine in Azure Docker-uitbreiding installeren en configureren van de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="79824-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="79824-126">U kunt de sjabloon hier weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="79824-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="79824-127">U moet de [nieuwste Azure CLI](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in de modus Resource Manager als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="79824-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="79824-128">De sjabloon met de Azure CLI, geven de URI van de sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="79824-128">Deploy the template using the Azure CLI, specifying the template URI.</span></span> <span data-ttu-id="79824-129">In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *westus*.</span><span class="sxs-lookup"><span data-stu-id="79824-129">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span> <span data-ttu-id="79824-130">Uw eigen Resourcegroepnaam en locatie als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="79824-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="79824-131">Beantwoord de wordt u gevraagd uw storage-account een naam, een gebruikersnaam en wachtwoord, en bieden een DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="79824-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="79824-132">De uitvoer lijkt op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="79824-132">The output is similar to the following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for the following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="79824-133">De Azure CLI geeft u op de vraag nadat slechts enkele seconden, maar de Docker-host is wel wordt gemaakt en geconfigureerd voor de virtuele machine in Azure Docker-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="79824-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span></span> <span data-ttu-id="79824-134">Het duurt enkele minuten duren voordat de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="79824-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="79824-135">U kunt details over het gebruik van Docker host status zien de `azure vm show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="79824-135">You can view details about the Docker host status using the `azure vm show` command.</span></span>

<span data-ttu-id="79824-136">Het volgende voorbeeld controleert de status van de virtuele machine met de naam *myDockerVM* (de standaardnaam van de sjabloon - geen deze naam niet wijzigen) in de resourcegroep met de naam *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="79824-136">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*.</span></span> <span data-ttu-id="79824-137">Voer de naam van de resourcegroep die u in de vorige stap hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="79824-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="79824-138">De uitvoer van de `azure vm show` opdracht is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="79824-138">The output of the `azure vm show` command is similar to the following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myDockerVM"
+ Looking up the NIC "myVMNicD"
+ Looking up the public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="79824-139">Aan de bovenkant van de uitvoer ziet u de **ProvisioningState** van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79824-139">Near the top of the output, you see the **ProvisioningState** of the VM.</span></span> <span data-ttu-id="79824-140">Wanneer u ziet nu *geslaagd*, de implementatie is voltooid en kunt u SSH naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79824-140">When this displays *Succeeded*, the deployment has finished and you can SSH to the VM.</span></span>

<span data-ttu-id="79824-141">Aan het einde van de uitvoer van de *FQDN* geeft de volledig gekwalificeerde domeinnaam van uw Docker-host.</span><span class="sxs-lookup"><span data-stu-id="79824-141">Towards the end of the output, *FQDN* displays the fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="79824-142">Deze FDQN-naam is die u gebruikt om SSH voor uw Docker-hosts in de resterende stappen.</span><span class="sxs-lookup"><span data-stu-id="79824-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="79824-143">Uw eerste nginx-container implementeren</span><span class="sxs-lookup"><span data-stu-id="79824-143">Deploy your first nginx container</span></span>
<span data-ttu-id="79824-144">Zodra de implementatie is voltooid, SSH naar uw nieuwe Docker-host van de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="79824-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span></span> <span data-ttu-id="79824-145">Voer uw eigen gebruikersnaam en de FQDN-naam als volgt:</span><span class="sxs-lookup"><span data-stu-id="79824-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="79824-146">Wanneer aangemeld bij de Docker-host, gaan we een nginx-container te uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="79824-146">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="79824-147">De uitvoer is vergelijkbaar met het volgende voorbeeld wordt de nginx-installatiekopie gedownload en een container gestart:</span><span class="sxs-lookup"><span data-stu-id="79824-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="79824-148">Controleer de status van de containers die wordt uitgevoerd op uw host Docker als volgt:</span><span class="sxs-lookup"><span data-stu-id="79824-148">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="79824-149">De uitvoer is vergelijkbaar met het volgende voorbeeld, waaruit blijkt dat de nginx-container actief is en TCP-poorten 80 en 443 en ernaar worden doorgestuurd:</span><span class="sxs-lookup"><span data-stu-id="79824-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="79824-150">De container in actie zien, opent u een webbrowser en voer de FQDN-naam van uw Docker-host:</span><span class="sxs-lookup"><span data-stu-id="79824-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span></span>

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="79824-152">Azure Docker VM-sjabloon uitbreidingsverwijzing</span><span class="sxs-lookup"><span data-stu-id="79824-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="79824-153">Het vorige voorbeeld maakt gebruik van een bestaande Quick Start-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="79824-153">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="79824-154">U kunt ook de Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="79824-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="79824-155">Om dit te doen, kunt u het volgende toevoegen aan de Resource Manager-sjablonen, definiëren de *vmName* van uw virtuele machine op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="79824-155">To do so, add the following to your Resource Manager templates, defining the *vmName* of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="79824-156">U vindt meer gedetailleerde stapsgewijze instructies over het gebruik van Resource Manager-sjablonen door te lezen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79824-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="79824-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79824-157">Next steps</span></span>
<span data-ttu-id="79824-158">U kunt desgewenst [de Docker-daemon TCP-poort configureren](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), begrijpen [Docker-beveiliging](https://docs.docker.com/engine/security/security/), of met behulp van containers implementeren [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="79824-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="79824-159">Zie voor meer informatie over de Azure Docker VM-extensie zichzelf, het [GitHub project](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="79824-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="79824-160">Lees meer informatie over de extra Docker implementatie-opties in Azure:</span><span class="sxs-lookup"><span data-stu-id="79824-160">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="79824-161">Docker-Machine met het Azure-stuurprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="79824-161">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="79824-162">[Aan de slag met Docker en opstellen om te definiëren en een toepassing met meerdere container uitvoert op een virtuele machine van Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="79824-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="79824-163">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="79824-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

