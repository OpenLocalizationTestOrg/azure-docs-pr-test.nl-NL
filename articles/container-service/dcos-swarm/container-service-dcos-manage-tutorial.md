---
title: zelfstudie voor aaaAzure Container Service - DC/OS beheren | Microsoft Docs
description: Zelfstudie voor Azure Container Service - DC/OS beheren
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="e00ab-104">Zelfstudie voor Azure Container Service - DC/OS beheren</span><span class="sxs-lookup"><span data-stu-id="e00ab-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="e00ab-105">DC/OS biedt een gedistribueerde platform voor lopende moderne en beperkte toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e00ab-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="e00ab-106">Met Azure Container Service is het inrichten van een productie gereed DC/OS-cluster snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="e00ab-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="e00ab-107">Deze eenvoudige stappen voor snel starten-informatie nodig toodeploy een DC/OS-cluster en voer basic werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="e00ab-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e00ab-108">Een ACS-DC/OS-cluster maken</span><span class="sxs-lookup"><span data-stu-id="e00ab-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="e00ab-109">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="e00ab-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="e00ab-110">Hallo DC/OS CLI installeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="e00ab-111">Een toepassing toohello-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="e00ab-112">Een toepassing op Hallo cluster schalen</span><span class="sxs-lookup"><span data-stu-id="e00ab-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="e00ab-113">Hallo DC/OS clusterknooppunten schalen</span><span class="sxs-lookup"><span data-stu-id="e00ab-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="e00ab-114">Basic DC/OS-management</span><span class="sxs-lookup"><span data-stu-id="e00ab-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="e00ab-115">Hallo DC/OS-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="e00ab-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="e00ab-116">Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e00ab-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e00ab-117">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="e00ab-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e00ab-118">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e00ab-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="e00ab-119">DC/OS-cluster maken</span><span class="sxs-lookup"><span data-stu-id="e00ab-119">Create DC/OS cluster</span></span>

<span data-ttu-id="e00ab-120">Maak eerst een resourcegroep met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e00ab-121">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="e00ab-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="e00ab-122">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.</span><span class="sxs-lookup"><span data-stu-id="e00ab-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="e00ab-123">Maak vervolgens een DC/OS-cluster met Hallo [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="e00ab-124">Hallo volgende voorbeeld maakt u een DC/OS-cluster met de naam *myDCOSCluster* en SSH-sleutels gemaakt als deze niet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="e00ab-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="e00ab-125">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="e00ab-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="e00ab-126">Hallo-opdracht is voltooid en retourneert informatie over de implementatie van Hallo na enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="e00ab-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="e00ab-127">Verbinding maken met tooDC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="e00ab-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="e00ab-128">Zodra een DC/OS-cluster is gemaakt, kan het zijn toegang tot en met een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="e00ab-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="e00ab-129">Hallo volgende opdracht tooreturn Hallo openbare IP-adres van de DC/OS-master Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e00ab-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="e00ab-130">Dit IP-adres is opgeslagen in een variabele en gebruikt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="e00ab-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="e00ab-131">toocreate Hallo SSH-tunnel, Hallo volgende opdracht uitvoeren en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="e00ab-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="e00ab-132">Als poort 80 al in gebruik is is, mislukt de Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="e00ab-133">Update Hallo via een tunnel tooone poort niet in gebruik, zoals `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="e00ab-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="e00ab-134">DC/OS CLI installeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-134">Install DC/OS CLI</span></span>

<span data-ttu-id="e00ab-135">Hallo DC/OS cli met Hallo installeren [az acs dcos install-cli](/azure/acs/dcos#install-cli) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="e00ab-136">Als u Azure CloudShell, Hallo DC/OS CLI is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e00ab-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="e00ab-137">Als u hello Azure CLI voor Mac OS- of Linux uitvoert, moet u mogelijk toorun Hallo opdracht met sudo.</span><span class="sxs-lookup"><span data-stu-id="e00ab-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="e00ab-138">Voordat u Hallo die CLI kan worden gebruikt met Hallo-cluster, moet dit geconfigureerde toouse Hallo SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="e00ab-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="e00ab-139">toodo uitgevoerd dus Hallo de volgende opdracht, Hallo-poort aan te passen, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="e00ab-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="e00ab-140">Een toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-140">Run an application</span></span>

<span data-ttu-id="e00ab-141">Hallo-standaardwaarde planning mechanisme voor een ACS-DC/OS-cluster is Marathon.</span><span class="sxs-lookup"><span data-stu-id="e00ab-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="e00ab-142">Marathon gebruikte toostart is een toepassing en status van toepassing op de DC/OS-cluster Hallo HALLO hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="e00ab-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="e00ab-143">tooschedule een toepassing via Marathon, maak een bestand met de naam **marathon app.json**, en kopiëren Hallo inhoud in de App.</span><span class="sxs-lookup"><span data-stu-id="e00ab-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="e00ab-144">Hallo opdracht tooschedule Hallo toepassing toorun volgen op Hallo DC/OS-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e00ab-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="e00ab-145">Hallo Implementatiestatus toosee voor Hallo-app Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e00ab-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="e00ab-146">Wanneer Hallo **taken** kolomwaarde verandert van *0/1* te*1/1*, implementatie van toepassing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e00ab-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="e00ab-147">Marathon-toepassing schalen</span><span class="sxs-lookup"><span data-stu-id="e00ab-147">Scale Marathon application</span></span>

<span data-ttu-id="e00ab-148">In het vorige voorbeeld hello, is een toepassing met één exemplaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e00ab-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="e00ab-149">Deze implementatie dat drie exemplaren van Hallo toepassing beschikbaar is, zijn geopend Hallo tooupdate **marathon app.json** bestand en Hallo exemplaar eigenschap too3 bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e00ab-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="e00ab-150">Hallo-toepassing hello met bijwerken `dcos marathon app update` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="e00ab-151">Hallo Implementatiestatus toosee voor Hallo-app Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e00ab-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="e00ab-152">Wanneer Hallo **taken** kolomwaarde verandert van *1/3* te*31/*, implementatie van toepassing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e00ab-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="e00ab-153">Internet toegankelijk app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-153">Run internet accessible app</span></span>

<span data-ttu-id="e00ab-154">Hallo ACS DC/OS-cluster bestaat uit twee sets knooppunt, een openbare die toegankelijk is op internet Hallo en een particuliere dat niet toegankelijk op Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="e00ab-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="e00ab-155">Hallo standaardset is Hallo persoonlijke knooppunten, die is gebruikt in het laatste voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="e00ab-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="e00ab-156">een toepassing toegankelijk toomake op Hallo van internet, deze toohello openbare knooppuntset implementeren.</span><span class="sxs-lookup"><span data-stu-id="e00ab-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="e00ab-157">toodo geven dus Hallo `acceptedResourceRoles` een waarde van het object `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="e00ab-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="e00ab-158">Maak een bestand met de naam **nginx public.json** en kopiëren Hallo inhoud in de App.</span><span class="sxs-lookup"><span data-stu-id="e00ab-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="e00ab-159">Hallo opdracht tooschedule Hallo toepassing toorun volgen op Hallo DC/OS-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e00ab-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="e00ab-160">Hallo openbaar IP-adres van Hallo DC/OS-cluster openbare agents worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="e00ab-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="e00ab-161">Bladeren door toothis adres retourneert Hallo standaard NGINX-site.</span><span class="sxs-lookup"><span data-stu-id="e00ab-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="e00ab-163">Schaal DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="e00ab-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="e00ab-164">In de voorgaande voorbeelden hello is een toepassing geschaald toomultiple exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e00ab-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="e00ab-165">Hallo DC/OS-infrastructuur kan ook worden uitgebreid tooprovide meer of minder rekencapaciteit.</span><span class="sxs-lookup"><span data-stu-id="e00ab-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="e00ab-166">Dit wordt gedaan met Hallo [az acs schalen]() opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="e00ab-167">toosee hello Huidig aantal van de DC/OS-agents gebruiken Hallo [az acs weergeven](/cli/azure/acs#show) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="e00ab-168">tooincrease aantal too5 hello, gebruikt u Hallo [az acs schalen](/cli/azure/acs#scale) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e00ab-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="e00ab-169">DC/OS-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="e00ab-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="e00ab-170">Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, DC/OS-cluster en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="e00ab-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="e00ab-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e00ab-171">Next steps</span></span>

<span data-ttu-id="e00ab-172">In deze zelfstudie hebt u geleerd over basic DC/OS-beheertaak, waaronder de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="e00ab-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e00ab-173">Een ACS-DC/OS-cluster maken</span><span class="sxs-lookup"><span data-stu-id="e00ab-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="e00ab-174">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="e00ab-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="e00ab-175">Hallo DC/OS CLI installeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="e00ab-176">Een toepassing toohello-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="e00ab-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="e00ab-177">Een toepassing op Hallo cluster schalen</span><span class="sxs-lookup"><span data-stu-id="e00ab-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="e00ab-178">Hallo DC/OS clusterknooppunten schalen</span><span class="sxs-lookup"><span data-stu-id="e00ab-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="e00ab-179">Hallo DC/OS-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="e00ab-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="e00ab-180">Geavanceerde toohello volgende zelfstudie toolearn over laden taakverdeling toepassing in DC/OS op Azure.</span><span class="sxs-lookup"><span data-stu-id="e00ab-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e00ab-181">Load balancing gebruiken voor toepassingen</span><span class="sxs-lookup"><span data-stu-id="e00ab-181">Load balance applications</span></span>](container-service-load-balancing.md)