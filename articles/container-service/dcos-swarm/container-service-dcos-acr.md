---
title: aaaUsing ACR met een Azure-DC/OS-cluster | Microsoft Docs
description: Een Azure Container Registry gebruiken met een DC/OS-cluster in Azure Container Service
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, Containers Micro-services, Mesos, Azure, bestandsshare, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="b95f6-104">ACR gebruiken met een DC/OS-cluster toodeploy uw toepassing</span><span class="sxs-lookup"><span data-stu-id="b95f6-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="b95f6-105">In dit artikel wordt besproken hoe toouse Azure Container register met een DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="b95f6-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="b95f6-106">ACR kunt u tooprivately store en beheren van installatiekopieën van de container.</span><span class="sxs-lookup"><span data-stu-id="b95f6-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="b95f6-107">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="b95f6-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b95f6-108">Azure Container register implementeren (indien nodig)</span><span class="sxs-lookup"><span data-stu-id="b95f6-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="b95f6-109">ACR-verificatie configureren op een DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="b95f6-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="b95f6-110">Een installatiekopie toohello Azure Container register geüpload</span><span class="sxs-lookup"><span data-stu-id="b95f6-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="b95f6-111">Uitvoeren van een installatiekopie van een container vanaf hello Azure Container register</span><span class="sxs-lookup"><span data-stu-id="b95f6-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="b95f6-112">U moet een ACS DC/OS cluster toocomplete Hallo in deze zelfstudie stappen.</span><span class="sxs-lookup"><span data-stu-id="b95f6-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="b95f6-113">Indien nodig, [dit voorbeeldscript](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="b95f6-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="b95f6-114">Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b95f6-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b95f6-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="b95f6-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b95f6-116">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b95f6-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="b95f6-117">Register met Azure Container implementeren</span><span class="sxs-lookup"><span data-stu-id="b95f6-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="b95f6-118">Maak indien nodig een Azure-Container registry Hello [az acr maken](/cli/azure/acr#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="b95f6-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="b95f6-119">Hallo volgende voorbeeld wordt een register met een willekeurige naam moet worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b95f6-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="b95f6-120">Hallo-register wordt ook geconfigureerd met een beheerdersaccount met Hallo `--admin-enabled` argument.</span><span class="sxs-lookup"><span data-stu-id="b95f6-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="b95f6-121">Zodra het Hallo-register is gemaakt, levert hello Azure CLI gegevens vergelijkbaar toohello volgt.</span><span class="sxs-lookup"><span data-stu-id="b95f6-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="b95f6-122">Let op Hallo `name` en `loginServer`, deze worden gebruikt in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="b95f6-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="b95f6-123">Hallo container register referenties met Hallo [az acr referentie weergeven](/cli/azure/acr/credential) opdracht.</span><span class="sxs-lookup"><span data-stu-id="b95f6-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="b95f6-124">Vervang Hallo `--name` Hello een vermeld in de laatste stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="b95f6-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="b95f6-125">Let op van een wachtwoord is vereist in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="b95f6-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="b95f6-126">Zie voor meer informatie over Azure-Container register [inleiding tooprivate Docker-container registers](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b95f6-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="b95f6-127">ACR-verificatie beheren</span><span class="sxs-lookup"><span data-stu-id="b95f6-127">Manage ACR authentication</span></span>

<span data-ttu-id="b95f6-128">Hallo conventionele wijze toopush en pull-installatiekopie van een persoonlijke register toofirst verifiëren met Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="b95f6-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="b95f6-129">toodo geval is, gebruikt u Hallo `docker login` opdracht op elke client die tooaccess Hallo persoonlijke register nodig.</span><span class="sxs-lookup"><span data-stu-id="b95f6-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="b95f6-130">Omdat een DC/OS-cluster veel knooppunten bevatten kan, die allemaal toobe geverifieerd met Hallo ACR nodig hebt, is het handig tooautomate dit proces voor elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b95f6-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="b95f6-131">Gedeelde opslag maken</span><span class="sxs-lookup"><span data-stu-id="b95f6-131">Create shared storage</span></span>

<span data-ttu-id="b95f6-132">Dit proces maakt gebruik van een Azure-bestandsshare die is gekoppeld op elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b95f6-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="b95f6-133">Als u al geen gedeelde opslag hebt ingesteld, Zie [instellen van een bestandsshare in een DC/OS-cluster](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="b95f6-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="b95f6-134">ACR-verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="b95f6-134">Configure ACR authentication</span></span>

<span data-ttu-id="b95f6-135">Eerst ophalen Hallo FQDN-naam van Hallo DC/OS-master en op te slaan in een variabele.</span><span class="sxs-lookup"><span data-stu-id="b95f6-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="b95f6-136">Een SSH-verbinding maken met Hallo master (of het eerste model Hallo) van uw DC/OS gebaseerde cluster.</span><span class="sxs-lookup"><span data-stu-id="b95f6-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="b95f6-137">Hallo-gebruikersnaam bijwerken als een niet-standaard-waarde is gebruikt bij het maken van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b95f6-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="b95f6-138">Na de opdracht toologin toohello Azure Container register Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b95f6-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="b95f6-139">Vervang Hallo `--username` met de naam van Hallo container register en Hallo Hallo `--password` met een van de opgegeven Hallo wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="b95f6-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="b95f6-140">Vervang het laatste argument Hallo *mycontainerregistry.azurecr.io* in Hallo voorbeeld met de naam van Hallo loginServer van Hallo container register.</span><span class="sxs-lookup"><span data-stu-id="b95f6-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="b95f6-141">Deze opdracht worden opgeslagen Hallo verificatie waarden lokaal onder Hallo `~/.docker` pad.</span><span class="sxs-lookup"><span data-stu-id="b95f6-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="b95f6-142">Maak een gecomprimeerd bestand met Hallo container registerwaarden verificatie.</span><span class="sxs-lookup"><span data-stu-id="b95f6-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="b95f6-143">Kopieer dit bestand toohello gedeelde clusteropslag.</span><span class="sxs-lookup"><span data-stu-id="b95f6-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="b95f6-144">Deze stap maakt beschikbaar zijn op alle knooppunten van de DC/OS-cluster Hallo Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="b95f6-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="b95f6-145">Afbeelding tooACR uploaden</span><span class="sxs-lookup"><span data-stu-id="b95f6-145">Upload image tooACR</span></span>

<span data-ttu-id="b95f6-146">Nu vanuit een ontwikkelcomputer of elk ander systeem met Docker geïnstalleerd, een installatiekopie maken en upload het toohello Azure Container register.</span><span class="sxs-lookup"><span data-stu-id="b95f6-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="b95f6-147">Een container van Hallo Ubuntu installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="b95f6-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="b95f6-148">Nu Hallo container vastleggen in een nieuwe installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b95f6-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="b95f6-149">Hallo installatiekopie met de naam moet tooinclude hello `loginServer` naam van het Hallo-container registrywith een indeling van `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="b95f6-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="b95f6-150">Meld u aan bij hello Azure Container register.</span><span class="sxs-lookup"><span data-stu-id="b95f6-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="b95f6-151">Hallo naam vervangen door Hallo loginServer naam, Hallo--gebruikersnaam met de naam van de Hallo van Hallo container register en Hallo--wachtwoord met een van de opgegeven Hallo wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="b95f6-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="b95f6-152">Ten slotte uploaden Hallo installatiekopie toohello ACR register.</span><span class="sxs-lookup"><span data-stu-id="b95f6-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="b95f6-153">In dit voorbeeld wordt een afbeelding met de naam dcos demo geüpload.</span><span class="sxs-lookup"><span data-stu-id="b95f6-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="b95f6-154">Uitvoeren van een installatiekopie vanaf ACR</span><span class="sxs-lookup"><span data-stu-id="b95f6-154">Run an image from ACR</span></span>

<span data-ttu-id="b95f6-155">toouse een afbeelding uit Hallo ACR register, maakt u een bestand namen *acrDemo.json* en kopiëren Hallo tekst in de App.</span><span class="sxs-lookup"><span data-stu-id="b95f6-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="b95f6-156">Vervangen door de naam van de installatiekopie Hallo Hallo container register loginServer naam en de naam van de installatiekopie, bijvoorbeeld `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="b95f6-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="b95f6-157">Let op Hallo `uris` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b95f6-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="b95f6-158">Deze eigenschap bevat Hallo-locatie van Hallo container verificatie registerbestand, die in dit geval hello Azure-bestandsshare die is gekoppeld op elk knooppunt in Hallo DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="b95f6-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="b95f6-159">Hallo-toepassing Hello CLI DC/Overheadkosten implementeren.</span><span class="sxs-lookup"><span data-stu-id="b95f6-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="b95f6-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b95f6-160">Next steps</span></span>

<span data-ttu-id="b95f6-161">In deze zelfstudie hebt u DC/OS toouse Azure Container register met inbegrip van de volgende Hallo taken configureren:</span><span class="sxs-lookup"><span data-stu-id="b95f6-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b95f6-162">Azure Container register implementeren (indien nodig)</span><span class="sxs-lookup"><span data-stu-id="b95f6-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="b95f6-163">ACR-verificatie configureren op een DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="b95f6-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="b95f6-164">Een installatiekopie toohello Azure Container register geüpload</span><span class="sxs-lookup"><span data-stu-id="b95f6-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="b95f6-165">Uitvoeren van een installatiekopie van een container vanaf hello Azure Container register</span><span class="sxs-lookup"><span data-stu-id="b95f6-165">Run a container image from hello Azure Container Registry</span></span>
