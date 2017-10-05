---
title: Azure Container Service Quick Start - DC/OS-Cluster implementeren | Microsoft Docs
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
ms.openlocfilehash: a31170369de9bc1ddcddb97171281b0014af95f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="3215c-104">Een DC/OS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="3215c-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="3215c-105">DC/OS biedt een gedistribueerde platform voor lopende moderne en beperkte toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3215c-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="3215c-106">Met Azure Container Service is het inrichten van een productie gereed DC/OS-cluster snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="3215c-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="3215c-107">Deze informatie snel starten de eenvoudige stappen die nodig zijn voor het implementeren van een DC/OS-cluster en basic werkbelasting uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3215c-107">This quick start details the basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="3215c-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="3215c-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="3215c-109">Voor deze zelfstudie is versie 2.0.4 of hoger van de Azure CLI vereist.</span><span class="sxs-lookup"><span data-stu-id="3215c-109">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3215c-110">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="3215c-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="3215c-111">Als u Azure CLI 2.0 wilt upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3215c-111">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="3215c-112">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="3215c-112">Log in to Azure</span></span> 

<span data-ttu-id="3215c-113">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="3215c-113">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3215c-114">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="3215c-114">Create a resource group</span></span>

<span data-ttu-id="3215c-115">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3215c-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3215c-116">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="3215c-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="3215c-117">In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *VS Oost*.</span><span class="sxs-lookup"><span data-stu-id="3215c-117">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="3215c-118">DC/OS-cluster maken</span><span class="sxs-lookup"><span data-stu-id="3215c-118">Create DC/OS cluster</span></span>

<span data-ttu-id="3215c-119">Maken van een DC/OS-cluster met de [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3215c-119">Create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="3215c-120">Het volgende voorbeeld wordt een DC/OS-cluster met de naam *myDCOSCluster* en SSH-sleutels gemaakt als deze niet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="3215c-120">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="3215c-121">Als u een specifieke set sleutels wilt gebruiken, gebruikt u de optie `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="3215c-121">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="3215c-122">Na enkele minuten, de opdracht is voltooid en retourneert informatie over de implementatie.</span><span class="sxs-lookup"><span data-stu-id="3215c-122">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="3215c-123">Verbinding maken met DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="3215c-123">Connect to DC/OS cluster</span></span>

<span data-ttu-id="3215c-124">Zodra een DC/OS-cluster is gemaakt, kan het zijn toegang tot en met een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="3215c-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="3215c-125">Voer de volgende opdracht om te retourneren van het openbare IP-adres van de DC/OS-master.</span><span class="sxs-lookup"><span data-stu-id="3215c-125">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="3215c-126">Dit IP-adres is opgeslagen in een variabele en gebruikt in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3215c-126">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="3215c-127">De SSH-tunnel maken, voert de volgende opdracht uit en volg de aanwijzingen op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="3215c-127">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="3215c-128">Als poort 80 al in gebruik is is, mislukt de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3215c-128">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="3215c-129">De via een tunnel poort naar een niet in gebruik, zoals bijwerken `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="3215c-129">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="3215c-130">De SSH-tunnel kan worden getest door te bladeren naar `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="3215c-130">The SSH tunnel can be tested by browsing to `http://localhost`.</span></span> <span data-ttu-id="3215c-131">Als een poort andere 80 is bereikt, de locatie moet worden gezocht aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3215c-131">If a port other that 80 has been used, adjust the location to match.</span></span> 

<span data-ttu-id="3215c-132">Als de SSH-tunnel is gemaakt, wordt de DC/OS-portal geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3215c-132">If the SSH tunnel was successfully created, the DC/OS portal is returned.</span></span>

![DCOS GEBRUIKERSINTERFACE](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="3215c-134">DC/OS CLI installeren</span><span class="sxs-lookup"><span data-stu-id="3215c-134">Install DC/OS CLI</span></span>

<span data-ttu-id="3215c-135">De DC/OS-opdrachtregelinterface wordt gebruikt voor het beheren van een DC/OS-cluster vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3215c-135">The DC/OS command line interface is used to manage a DC/OS cluster from the command-line.</span></span> <span data-ttu-id="3215c-136">Installeer de DC/OS cli met de [az acs dcos install-cli](/azure/acs/dcos#install-cli) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3215c-136">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="3215c-137">Als u Azure CloudShell gebruikt, wordt de DC/OS CLI is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3215c-137">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="3215c-138">Als u de Azure CLI voor Mac OS- of Linux uitvoert, moet u mogelijk de opdracht uitvoert met sudo.</span><span class="sxs-lookup"><span data-stu-id="3215c-138">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="3215c-139">Voordat de CLI kan worden gebruikt met het cluster, moet deze worden geconfigureerd voor het gebruik van de SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="3215c-139">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="3215c-140">Voer de volgende opdracht, de poort aan te passen, indien nodig om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="3215c-140">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="3215c-141">Een toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3215c-141">Run an application</span></span>

<span data-ttu-id="3215c-142">De standaardwaarde planning mechanisme voor een ACS-DC/OS-cluster is Marathon.</span><span class="sxs-lookup"><span data-stu-id="3215c-142">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="3215c-143">Marathon wordt gebruikt om een toepassing starten en beheren van de status van de toepassing op de DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="3215c-143">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="3215c-144">Als u een toepassing via Marathon plannen, maakt u een bestand met de naam *marathon app.json*, en kopieer de volgende inhoud in de App.</span><span class="sxs-lookup"><span data-stu-id="3215c-144">To schedule an application through Marathon, create a file named *marathon-app.json*, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="3215c-145">Voer de volgende opdracht om te plannen van de toepassing uit te voeren op de DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="3215c-145">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="3215c-146">Overzicht van de implementatiestatus voor de app, voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="3215c-146">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="3215c-147">Wanneer de **WACHTEN** kolomwaarde verandert van *True* naar *False*, implementatie van toepassing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3215c-147">When the **WAITING** column value switches from *True* to *False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="3215c-148">Haal het openbare IP-adres van de agents DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="3215c-148">Get the public IP address of the DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="3215c-149">Bladeren naar dit adres retourneert de standaard NGINX-site.</span><span class="sxs-lookup"><span data-stu-id="3215c-149">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="3215c-151">DC/OS-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="3215c-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="3215c-152">Wanneer deze niet langer nodig is, kunt u de [az groep verwijderen](/cli/azure/group#delete) opdracht voor het verwijderen van de resourcegroep, DC/OS-cluster, en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="3215c-152">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="3215c-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3215c-153">Next steps</span></span>

<span data-ttu-id="3215c-154">In deze snel starten moet u een DC/OS-cluster hebt geïmplementeerd en een eenvoudige Docker-container hebt uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="3215c-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on the cluster.</span></span> <span data-ttu-id="3215c-155">Blijven de ACS-zelfstudies voor meer informatie over Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3215c-155">To learn more about Azure Container Service, continue to the ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3215c-156">Een ACS-DC/OS-Cluster beheren</span><span class="sxs-lookup"><span data-stu-id="3215c-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)