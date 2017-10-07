---
title: "aaaHow toocreate Linux Azure VM-installatiekopieën met verpakker | Microsoft Docs"
description: Meer informatie over hoe toouse verpakker toocreate afbeeldingen van Linux virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="44cb7-103">Hoe installatiekopieën van toouse verpakker toocreate virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="44cb7-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="44cb7-104">Elke virtuele machine (VM) in Azure wordt gemaakt van een installatiekopie die Hallo Linux-distributie en versie van het besturingssysteem definieert.</span><span class="sxs-lookup"><span data-stu-id="44cb7-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="44cb7-105">Voorbeelden van afbeeldingen zijn vooraf geïnstalleerde toepassingen en configuraties.</span><span class="sxs-lookup"><span data-stu-id="44cb7-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="44cb7-106">Hello Azure Marketplace bevat veel installatiekopieën van het eerste en derde partij voor het meest voorkomende distributies en omgevingen met toepassingen, of kunt u uw eigen aangepaste installatiekopieën die zijn afgestemd tooyour behoeften.</span><span class="sxs-lookup"><span data-stu-id="44cb7-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="44cb7-107">Dit artikel wordt uitgelegd hoe de bron-hulpprogramma voor het openen van toouse Hallo [verpakker](https://www.packer.io/) toodefine en build aangepaste installatiekopieën in Azure.</span><span class="sxs-lookup"><span data-stu-id="44cb7-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="44cb7-108">Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="44cb7-108">Create Azure resource group</span></span>
<span data-ttu-id="44cb7-109">Tijdens Hallo maken maakt verpakker tijdelijke Azure-resources als builds Hallo bron-VM.</span><span class="sxs-lookup"><span data-stu-id="44cb7-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="44cb7-110">toocapture die VM voor gebruik als een installatiekopie van een gegevensbron, moet u een resourcegroep definiëren.</span><span class="sxs-lookup"><span data-stu-id="44cb7-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="44cb7-111">Hallo wordt uitvoer van Hallo verpakker buildproces opgeslagen in deze resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="44cb7-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="44cb7-112">Maak een resourcegroep maken met [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="44cb7-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="44cb7-113">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="44cb7-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="44cb7-114">Azure-referenties maken</span><span class="sxs-lookup"><span data-stu-id="44cb7-114">Create Azure credentials</span></span>
<span data-ttu-id="44cb7-115">Verpakker verifieert met Azure met behulp van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="44cb7-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="44cb7-116">Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals verpakker kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44cb7-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="44cb7-117">U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="44cb7-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="44cb7-118">Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en uitvoer Hallo de referenties die verpakker moet:</span><span class="sxs-lookup"><span data-stu-id="44cb7-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="44cb7-119">Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:</span><span class="sxs-lookup"><span data-stu-id="44cb7-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="44cb7-120">tooauthenticate tooAzure, moet u ook uw Azure-abonnement-ID met tooobtain [az account weergeven](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="44cb7-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="44cb7-121">U Hallo-uitvoer van deze twee opdrachten in de volgende stap hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44cb7-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="44cb7-122">Verpakker sjabloon definiëren</span><span class="sxs-lookup"><span data-stu-id="44cb7-122">Define Packer template</span></span>
<span data-ttu-id="44cb7-123">toobuild afbeeldingen, maakt u een sjabloon als een JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="44cb7-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="44cb7-124">In de sjabloon hello, definieert u opbouwfuncties en buildproces provisioners die Hallo werkelijke uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="44cb7-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="44cb7-125">Verpakker heeft een [provisioner voor Azure](https://www.packer.io/docs/builders/azure.html) waarmee u toodefine Azure resources, zoals Hallo principal Servicereferenties in Hallo voorgaande stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44cb7-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="44cb7-126">Maak een bestand met de naam *ubuntu.json* en inhoud te plakken Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="44cb7-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="44cb7-127">Geef uw eigen waarden voor Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="44cb7-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="44cb7-128">Parameter</span><span class="sxs-lookup"><span data-stu-id="44cb7-128">Parameter</span></span>                           | <span data-ttu-id="44cb7-129">Waar tooobtain</span><span class="sxs-lookup"><span data-stu-id="44cb7-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="44cb7-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="44cb7-130">*client_id*</span></span>                         | <span data-ttu-id="44cb7-131">Eerste regel van de uitvoer van `az ad sp` maken command - *appId*</span><span class="sxs-lookup"><span data-stu-id="44cb7-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="44cb7-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="44cb7-132">*client_secret*</span></span>                     | <span data-ttu-id="44cb7-133">Lijn van uitvoer van de tweede `az ad sp` maken command - *wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="44cb7-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="44cb7-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="44cb7-134">*tenant_id*</span></span>                         | <span data-ttu-id="44cb7-135">Derde regel van uitvoer van `az ad sp` maken command - *tenant*</span><span class="sxs-lookup"><span data-stu-id="44cb7-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="44cb7-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="44cb7-136">*subscription_id*</span></span>                   | <span data-ttu-id="44cb7-137">De uitvoer van `az account show` opdracht</span><span class="sxs-lookup"><span data-stu-id="44cb7-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="44cb7-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="44cb7-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="44cb7-139">Naam van resourcegroep die u hebt gemaakt in de eerste stap Hallo</span><span class="sxs-lookup"><span data-stu-id="44cb7-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="44cb7-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="44cb7-140">*managed_image_name*</span></span>                | <span data-ttu-id="44cb7-141">Naam voor Hallo beheerde installatiekopie die is gemaakt</span><span class="sxs-lookup"><span data-stu-id="44cb7-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="44cb7-142">Deze sjabloon maakt een installatiekopie van een virtuele Ubuntu 16.04 TNS, NGINX installeert en deprovisions Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="44cb7-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="44cb7-143">Als u deze sjabloon tooprovision gebruikersreferenties uitbreiden, aanpassen Hallo provisioner opdracht dat deprovisions hello Azure-agent tooread `-deprovision` plaats `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="44cb7-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="44cb7-144">Hallo `+user` vlag verwijdert alle gebruikersaccounts uit Hallo bron-VM.</span><span class="sxs-lookup"><span data-stu-id="44cb7-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="44cb7-145">Verpakker installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="44cb7-145">Build Packer image</span></span>
<span data-ttu-id="44cb7-146">Als u nog niet geïnstalleerd op uw lokale machine verpakker hebt [Volg Hallo verpakker installatie-instructies](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="44cb7-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="44cb7-147">Hallo image samenstellen door te geven van uw verpakker sjabloonbestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="44cb7-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="44cb7-148">Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:</span><span class="sxs-lookup"><span data-stu-id="44cb7-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="44cb7-149">Virtuele machine van de afbeelding voor Azure maken</span><span class="sxs-lookup"><span data-stu-id="44cb7-149">Create VM from Azure Image</span></span>
<span data-ttu-id="44cb7-150">U kunt nu een virtuele machine maken van de installatiekopie met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="44cb7-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="44cb7-151">Geef Hallo installatiekopie die u hebt gemaakt met de Hallo `--image` parameter.</span><span class="sxs-lookup"><span data-stu-id="44cb7-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="44cb7-152">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* van *myPackerImage* en SSH-sleutels genereert als deze niet al bestaan:</span><span class="sxs-lookup"><span data-stu-id="44cb7-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="44cb7-153">Het duurt enkele minuten toocreate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="44cb7-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="44cb7-154">Zodra Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="44cb7-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="44cb7-155">Dit adres is gebruikte tooaccess hello NGINX site via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="44cb7-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="44cb7-156">virtuele machine, open poort 80 van Hallo Internet met het web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="44cb7-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="44cb7-157">Virtuele machine en NGINX testen</span><span class="sxs-lookup"><span data-stu-id="44cb7-157">Test VM and NGINX</span></span>
<span data-ttu-id="44cb7-158">Nu kunt u een webbrowser openen en voer `http://publicIpAddress` in de adresbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="44cb7-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="44cb7-159">Geef uw eigen openbare IP-adres uit Hallo VM proces maken.</span><span class="sxs-lookup"><span data-stu-id="44cb7-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="44cb7-160">Hallo standaard NGINX-pagina wordt weergegeven zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="44cb7-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Standaardsite van NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="44cb7-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44cb7-162">Next steps</span></span>
<span data-ttu-id="44cb7-163">In dit voorbeeld gebruikt u verpakker toocreate een VM-installatiekopie met NGINX al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="44cb7-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="44cb7-164">U kunt deze VM-installatiekopie samen met de bestaande implementatiewerkstromen, zoals uw app tooVMs van de installatiekopie met Ansible, Chef of Puppet hello gemaakt toodeploy gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44cb7-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="44cb7-165">Zie voor aanvullende voorbeeld verpakker sjablonen voor andere Linux-distributies, [deze GitHub-repo-](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="44cb7-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>