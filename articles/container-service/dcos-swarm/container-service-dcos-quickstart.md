---
title: aaaAzure Container Service Quick Start - DC/OS-Cluster implementeren | Microsoft Docs
description: Azure Container Service Quick Start - DC/OS-Cluster implementeren
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="30d6f-104">Een DC/OS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="30d6f-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="30d6f-105">DC/OS biedt een gedistribueerde platform voor lopende moderne en beperkte toepassingen.</span><span class="sxs-lookup"><span data-stu-id="30d6f-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="30d6f-106">Met Azure Container Service is het inrichten van een productie gereed DC/OS-cluster snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="30d6f-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="30d6f-107">Deze eenvoudige stappen voor snel starten details Hallo nodig toodeploy een DC/OS-cluster en voer basic werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="30d6f-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="30d6f-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="30d6f-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="30d6f-109">Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="30d6f-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="30d6f-110">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="30d6f-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="30d6f-111">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30d6f-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="30d6f-112">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="30d6f-112">Log in tooAzure</span></span> 

<span data-ttu-id="30d6f-113">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="30d6f-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="30d6f-114">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="30d6f-114">Create a resource group</span></span>

<span data-ttu-id="30d6f-115">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="30d6f-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="30d6f-116">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="30d6f-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="30d6f-117">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="30d6f-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="30d6f-118">DC/OS-cluster maken</span><span class="sxs-lookup"><span data-stu-id="30d6f-118">Create DC/OS cluster</span></span>

<span data-ttu-id="30d6f-119">Maken van een DC/OS-cluster met Hallo [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="30d6f-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="30d6f-120">Hallo volgende voorbeeld maakt u een DC/OS-cluster met de naam *myDCOSCluster* en SSH-sleutels gemaakt als deze niet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="30d6f-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="30d6f-121">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="30d6f-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="30d6f-122">Hallo-opdracht is voltooid en retourneert informatie over de implementatie van Hallo na enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="30d6f-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="30d6f-123">Verbinding maken met tooDC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="30d6f-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="30d6f-124">Zodra een DC/OS-cluster is gemaakt, kan het zijn toegang tot en met een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="30d6f-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="30d6f-125">Hallo volgende opdracht tooreturn Hallo openbare IP-adres van de DC/OS-master Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="30d6f-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="30d6f-126">Dit IP-adres is opgeslagen in een variabele en gebruikt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="30d6f-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="30d6f-127">toocreate Hallo SSH-tunnel, Hallo volgende opdracht uitvoeren en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="30d6f-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="30d6f-128">Als poort 80 al in gebruik is is, mislukt de Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="30d6f-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="30d6f-129">Update Hallo via een tunnel tooone poort niet in gebruik, zoals `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="30d6f-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="30d6f-130">Hallo SSH-tunnel kan worden getest door te bladeren`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="30d6f-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="30d6f-131">Als een poort andere 80 is bereikt, Hallo locatie toomatch aanpassen.</span><span class="sxs-lookup"><span data-stu-id="30d6f-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="30d6f-132">Als de SSH-tunnel Hallo is gemaakt, wordt Hallo DC/OS-portal geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="30d6f-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![DCOS GEBRUIKERSINTERFACE](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="30d6f-134">DC/OS CLI installeren</span><span class="sxs-lookup"><span data-stu-id="30d6f-134">Install DC/OS CLI</span></span>

<span data-ttu-id="30d6f-135">Hallo-opdrachtregelinterface voor DC/OS is gebruikte toomanage een DC/OS-cluster met Hallo vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="30d6f-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="30d6f-136">Hallo DC/OS cli met Hallo installeren [az acs dcos install-cli](/azure/acs/dcos#install-cli) opdracht.</span><span class="sxs-lookup"><span data-stu-id="30d6f-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="30d6f-137">Als u Azure CloudShell, Hallo DC/OS CLI is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="30d6f-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="30d6f-138">Als u hello Azure CLI voor Mac OS- of Linux uitvoert, moet u mogelijk toorun Hallo opdracht met sudo.</span><span class="sxs-lookup"><span data-stu-id="30d6f-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="30d6f-139">Voordat u Hallo die CLI kan worden gebruikt met Hallo-cluster, moet dit geconfigureerde toouse Hallo SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="30d6f-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="30d6f-140">toodo uitgevoerd dus Hallo de volgende opdracht, Hallo-poort aan te passen, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="30d6f-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="30d6f-141">Een toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="30d6f-141">Run an application</span></span>

<span data-ttu-id="30d6f-142">Hallo-standaardwaarde planning mechanisme voor een ACS-DC/OS-cluster is Marathon.</span><span class="sxs-lookup"><span data-stu-id="30d6f-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="30d6f-143">Marathon gebruikte toostart is een toepassing en status van toepassing op de DC/OS-cluster Hallo HALLO hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="30d6f-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="30d6f-144">tooschedule een toepassing via Marathon, maak een bestand met de naam *marathon app.json*, en kopiëren Hallo inhoud in de App.</span><span class="sxs-lookup"><span data-stu-id="30d6f-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="30d6f-145">Hallo opdracht tooschedule Hallo toepassing toorun volgen op Hallo DC/OS-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="30d6f-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="30d6f-146">Hallo Implementatiestatus toosee voor Hallo-app Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="30d6f-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="30d6f-147">Wanneer Hallo **WACHTEN** kolomwaarde verandert van *True* te*False*, implementatie van toepassing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="30d6f-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="30d6f-148">Hallo openbare IP-adres van Hallo DC/OS-cluster agents worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="30d6f-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="30d6f-149">Bladeren door toothis adres retourneert Hallo standaard NGINX-site.</span><span class="sxs-lookup"><span data-stu-id="30d6f-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="30d6f-151">DC/OS-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="30d6f-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="30d6f-152">Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, DC/OS-cluster en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="30d6f-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="30d6f-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30d6f-153">Next steps</span></span>

<span data-ttu-id="30d6f-154">In deze snel starten een DC/OS-cluster hebt geïmplementeerd en een eenvoudige Docker-container op Hallo cluster hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="30d6f-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="30d6f-155">toolearn meer informatie over Azure Container Service blijven toohello ACS zelfstudies.</span><span class="sxs-lookup"><span data-stu-id="30d6f-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30d6f-156">Een ACS-DC/OS-Cluster beheren</span><span class="sxs-lookup"><span data-stu-id="30d6f-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)