---
title: aaaUse hello Azure Docker VM-extensie Hello Azure CLI 1.0 | Microsoft Docs
description: Informatie over hoe toouse Hallo Docker VM-extensie tooquickly en veilig implementeert een Docker-omgeving in Azure met behulp van Resource Manager-sjablonen.
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
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="e8553-103">Maakt een Docker-omgeving in Azure met behulp van Docker VM-extensie voor Hallo Hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e8553-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="e8553-104">Docker is een populair containerbeheer en installatiekopieën platform waarmee u tooquickly werken met containers op Linux (en ook Windows).</span><span class="sxs-lookup"><span data-stu-id="e8553-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="e8553-105">In Azure zijn er verschillende manieren waarop u Docker volgens tooyour behoeften kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="e8553-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="e8553-106">Dit artikel is gericht op het gebruik van Hallo Docker VM-extensie en Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e8553-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="e8553-107">Zie voor meer informatie over Hallo verschillende implementatiemethoden, inclusief het gebruik van Docker-Machine en de Azure-Container Services Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e8553-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="e8553-108">tooquickly prototype een app, kunt u één Docker-host met behulp van [Docker-Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="e8553-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="e8553-109">Voor grotere, stabiele omgevingen, kunt u hello Azure Docker VM-extensie, dat ook wordt ondersteund [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistente containerimplementaties.</span><span class="sxs-lookup"><span data-stu-id="e8553-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="e8553-110">Dit artikel gegevens met behulp van hello Azure Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="e8553-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="e8553-111">toobuild gereed is voor productie, schaalbare omgevingen die extra hulpprogramma's voor planning en beheer bieden, u kunt een [Docker Swarm-cluster op Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e8553-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e8553-112">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="e8553-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e8553-113">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e8553-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e8553-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="e8553-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e8553-115">[Azure CLI 2.0](dockerextension.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="e8553-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="e8553-116">Overzicht van Azure Docker VM-extensie</span><span class="sxs-lookup"><span data-stu-id="e8553-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="e8553-117">Hello Azure Docker VM-extensie installeert en configureert u het Hallo Docker-daemon, Docker-client en Docker Compose in uw virtuele Linux-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="e8553-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="e8553-118">U hebt meer controle en functies dan gewoon met behulp van Docker-Machine of maken van Hallo Docker-host met behulp van hello Azure Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="e8553-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="e8553-119">Deze aanvullende functies, zoals [Docker Compose](https://docs.docker.com/compose/overview/), zorg hello Azure Docker VM-extensie is geschikt voor krachtiger developer- of productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="e8553-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="e8553-120">Azure Resource Manager-sjablonen definiëren Hallo volledige structuur van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="e8553-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="e8553-121">Sjablonen kunnen u toocreate en bronnen zoals Hallo Docker host virtuele machines, opslag, op rollen gebaseerde toegangsbeheer (RBAC) en diagnostische gegevens configureren.</span><span class="sxs-lookup"><span data-stu-id="e8553-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="e8553-122">U kunt deze sjablonen toocreate extra implementaties op een consistente manier hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="e8553-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="e8553-123">Zie voor meer informatie over Azure Resource Manager en sjablonen [overzicht van Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8553-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="e8553-124">Een sjabloon met hello Azure Docker VM-extensie implementeren</span><span class="sxs-lookup"><span data-stu-id="e8553-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="e8553-125">Laten we gebruik van een bestaande sjabloon Quick Start-toocreate een Ubuntu VM die gebruikmaakt van hello Azure Docker VM-extensie tooinstall en Hallo Docker host configureren.</span><span class="sxs-lookup"><span data-stu-id="e8553-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="e8553-126">U kunt hier Hallo sjabloon weergeven: [eenvoudige implementatie van een VM Ubuntu met Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="e8553-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="e8553-127">U moet Hallo [nieuwste Azure CLI](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in het Hallo-Resource Manager-modus als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e8553-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e8553-128">Hallo-sjabloon met gebruik van Azure CLI, geven Hallo sjabloon URI Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="e8553-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="e8553-129">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie.</span><span class="sxs-lookup"><span data-stu-id="e8553-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="e8553-130">Uw eigen Resourcegroepnaam en locatie als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e8553-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="e8553-131">Hallo prompts tooname beantwoord uw storage-account, een gebruikersnaam en wachtwoord, en bieden een DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="e8553-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="e8553-132">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e8553-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="e8553-133">Hello Azure CLI retourneert u toohello prompt na slechts enkele seconden, maar de Docker-host wordt nog steeds gemaakt en geconfigureerd door hello Azure Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="e8553-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="e8553-134">Het duurt enkele minuten duren voordat Hallo implementatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="e8553-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="e8553-135">U kunt details zien over Hallo Docker host de status van Hallo `azure vm show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e8553-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="e8553-136">Hallo volgende voorbeeld controleert Hallo status van virtuele machine met de naam Hallo *myDockerVM* (de standaardnaam van de sjabloon Hallo Hallo - deze naam niet wijzigen) in de resourcegroep Hallo met de naam *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e8553-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="e8553-137">Geef de naam Hallo van Hallo-resourcegroep die u hebt gemaakt in de voorgaande stap Hallo:</span><span class="sxs-lookup"><span data-stu-id="e8553-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="e8553-138">uitvoer van Hallo Hallo `azure vm show` is vergelijkbaar toohello voorbeeld van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e8553-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
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

<span data-ttu-id="e8553-139">Aan de bovenkant van de Hallo van Hallo uitvoer, ziet u Hallo **ProvisioningState** Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e8553-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="e8553-140">Wanneer u ziet nu *geslaagd*, Hallo-implementatie is voltooid en kunt u SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="e8553-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="e8553-141">Naar einde van Hallo-uitvoer, Hallo *FQDN* Hallo volledig gekwalificeerde domeinnaam van uw Docker-host wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8553-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="e8553-142">Deze FDQN-naam is die u gebruikt tooSSH tooyour Docker-host in de resterende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8553-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="e8553-143">Uw eerste nginx-container implementeren</span><span class="sxs-lookup"><span data-stu-id="e8553-143">Deploy your first nginx container</span></span>
<span data-ttu-id="e8553-144">Eenmaal Hallo-implementatie is voltooid, SSH tooyour nieuwe Docker-host van de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e8553-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="e8553-145">Voer uw eigen gebruikersnaam en de FQDN-naam als volgt:</span><span class="sxs-lookup"><span data-stu-id="e8553-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="e8553-146">Wanneer toohello aangemeld met Docker-host, gaan we een nginx-container te uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e8553-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="e8553-147">Hallo-uitvoer is vergelijkbaar toohello na voorbeeld Hallo nginx installatiekopie gedownload en een container gestart:</span><span class="sxs-lookup"><span data-stu-id="e8553-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="e8553-148">Controleer de status Hallo van Hallo-containers die zijn uitgevoerd op uw host Docker als volgt:</span><span class="sxs-lookup"><span data-stu-id="e8553-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="e8553-149">Hallo-uitvoer is vergelijkbaar toohello voorbeeld te volgen, die Hallo nginx-container met actief is en TCP-poorten 80 en 443 en ernaar worden doorgestuurd:</span><span class="sxs-lookup"><span data-stu-id="e8553-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="e8553-150">toosee uw container in actie, open een webbrowser omhoog en Voer Hallo FQDN-naam van de Docker-host:</span><span class="sxs-lookup"><span data-stu-id="e8553-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Actieve ngnix container](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="e8553-152">Azure Docker VM-sjabloon uitbreidingsverwijzing</span><span class="sxs-lookup"><span data-stu-id="e8553-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="e8553-153">het vorige voorbeeld Hallo maakt gebruik van een bestaande Quick Start-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8553-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="e8553-154">U kunt ook hello Azure Docker VM-extensie implementeren met uw eigen Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e8553-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="e8553-155">toodo toevoegen dus Hallo tooyour Resource Manager-sjablonen te volgen, Hallo definiëren *vmName* van uw virtuele machine op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="e8553-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

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

<span data-ttu-id="e8553-156">U vindt meer gedetailleerde stapsgewijze instructies over het gebruik van Resource Manager-sjablonen door te lezen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8553-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8553-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8553-157">Next steps</span></span>
<span data-ttu-id="e8553-158">U kunt desgewenst te[hello Docker-daemon TCP-poort configureren](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), begrijpen [Docker beveiliging](https://docs.docker.com/engine/security/security/), of met behulp van containers implementeren [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="e8553-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="e8553-159">Zie voor meer informatie over hello Azure Docker VM-extensie zichzelf Hallo [GitHub project](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="e8553-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="e8553-160">Lees meer informatie over Hallo aanvullende Docker implementatieopties in Azure:</span><span class="sxs-lookup"><span data-stu-id="e8553-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="e8553-161">Docker-Machine Hello Azure stuurprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="e8553-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="e8553-162">[Aan de slag met Docker Compose toodefine en een toepassing met meerdere container uitvoert op een virtuele machine van Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e8553-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="e8553-163">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="e8553-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

