---
title: aaaQuickstart - cluster voor Windows Azure Kubernetes | Microsoft Docs
description: Snel meer toocreate een cluster Kubernetes voor Windows-containers in Azure Container Service met hello Azure CLI.
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="406eb-103">Kubernetes-cluster voor Windows-containers implementeren</span><span class="sxs-lookup"><span data-stu-id="406eb-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="406eb-104">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="406eb-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="406eb-105">De details van deze handleiding hello Azure CLI toodeploy met een [Kubernetes](https://kubernetes.io/docs/home/) -cluster in [Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="406eb-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="406eb-106">Zodra Hallo-cluster is geïmplementeerd, u verbinding maakt tooit Hello Kubernetes `kubectl` opdrachtregelprogramma en u uw eerste Windows-container te implementeren.</span><span class="sxs-lookup"><span data-stu-id="406eb-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="406eb-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="406eb-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="406eb-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="406eb-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="406eb-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="406eb-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="406eb-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="406eb-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="406eb-111">De ondersteuning voor Windows-containers in Kubernetes in Azure Container Service is momenteel beschikbaar als preview.</span><span class="sxs-lookup"><span data-stu-id="406eb-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="406eb-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="406eb-112">Create a resource group</span></span>

<span data-ttu-id="406eb-113">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="406eb-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="406eb-114">Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="406eb-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="406eb-115">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="406eb-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="406eb-116">Een Kubernetes-cluster maken</span><span class="sxs-lookup"><span data-stu-id="406eb-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="406eb-117">Een cluster Kubernetes maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="406eb-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="406eb-118">Hallo volgende voorbeeld wordt een cluster met de naam *myK8sCluster* hoofdsleutel met een Linux-knooppunt en twee knooppunten van de Windows-agent.</span><span class="sxs-lookup"><span data-stu-id="406eb-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="406eb-119">In dit voorbeeld maakt SSH-sleutels nodig tooconnect toohello Linux master.</span><span class="sxs-lookup"><span data-stu-id="406eb-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="406eb-120">In dit voorbeeld wordt *azureuser* voor de naam van een gebruiker met beheerdersrechten en *myPassword12* Hallo-wachtwoord op Hallo Windows knooppunten.</span><span class="sxs-lookup"><span data-stu-id="406eb-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="406eb-121">Deze waarden toosomething juiste tooyour omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="406eb-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="406eb-122">Na enkele minuten Hallo-opdracht is voltooid en ziet u informatie over uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="406eb-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="406eb-123">Kubectl installeren</span><span class="sxs-lookup"><span data-stu-id="406eb-123">Install kubectl</span></span>

<span data-ttu-id="406eb-124">tooconnect toohello Kubernetes-cluster van de clientcomputer gebruik [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), Hallo Kubernetes opdrachtregelprogramma client.</span><span class="sxs-lookup"><span data-stu-id="406eb-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="406eb-125">Als u Azure CloudShell gebruikt, is `kubectl` al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="406eb-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="406eb-126">Als u wilt dat tooinstall deze lokaal, kunt u Hallo [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) opdracht.</span><span class="sxs-lookup"><span data-stu-id="406eb-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="406eb-127">Hallo Azure CLI voorbeeld installeert na `kubectl` tooyour system.</span><span class="sxs-lookup"><span data-stu-id="406eb-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="406eb-128">In Windows moet u deze opdracht uitvoeren als beheerder.</span><span class="sxs-lookup"><span data-stu-id="406eb-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="406eb-129">Verbinden met kubectl</span><span class="sxs-lookup"><span data-stu-id="406eb-129">Connect with kubectl</span></span>

<span data-ttu-id="406eb-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster uitvoeren Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht.</span><span class="sxs-lookup"><span data-stu-id="406eb-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="406eb-131">Hallo downloadt volgende voorbeeld Hallo clusterconfiguratie voor uw cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="406eb-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="406eb-132">tooverify hello verbinding tooyour cluster van uw computer, probeer uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="406eb-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="406eb-133">`kubectl`Geeft een lijst Hallo hoofd- en agent knooppunten.</span><span class="sxs-lookup"><span data-stu-id="406eb-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="406eb-134">Een Windows IIS-container implementeren</span><span class="sxs-lookup"><span data-stu-id="406eb-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="406eb-135">U kunt een Docker-container uitvoeren binnen een Kubernetes-*schil*, die een of meer containers bevat.</span><span class="sxs-lookup"><span data-stu-id="406eb-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="406eb-136">Dit eenvoudige voorbeeld maakt gebruik van een JSON-bestand toospecify een container Microsoft Internet Information Server (IIS) en maakt vervolgens Hallo schil Hallo met `kubctl apply` opdracht.</span><span class="sxs-lookup"><span data-stu-id="406eb-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="406eb-137">Maken van een lokaal bestand met de naam `iis.json` en kopiëren Hallo tekst.</span><span class="sxs-lookup"><span data-stu-id="406eb-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="406eb-138">Dit bestand vertelt Kubernetes toorun IIS op Windows Server 2016 Nano Server met de installatiekopie van een openbare container van [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="406eb-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="406eb-139">Hallo-container gebruikt poort 80, maar in eerste instantie is alleen toegankelijk vanuit Hallo clusternetwerk.</span><span class="sxs-lookup"><span data-stu-id="406eb-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="406eb-140">toostart hello schil type:</span><span class="sxs-lookup"><span data-stu-id="406eb-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="406eb-141">implementatie van tootrack hello, type:</span><span class="sxs-lookup"><span data-stu-id="406eb-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="406eb-142">Hoewel Hallo schil implementeert, is het Hallo-status `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="406eb-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="406eb-143">Het kan enkele minuten duren voordat Hallo container tooenter hello `Running` status.</span><span class="sxs-lookup"><span data-stu-id="406eb-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="406eb-144">Weergave Hallo IIS-welkomstpagina</span><span class="sxs-lookup"><span data-stu-id="406eb-144">View hello IIS welcome page</span></span>

<span data-ttu-id="406eb-145">tooexpose Hallo schil toohello wereld met een openbaar IP-adres, type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="406eb-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="406eb-146">Met deze opdracht maakt Kubernetes een service en een [Azure load balancer-regel](container-service-kubernetes-load-balancing.md) met een openbaar IP-adres voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="406eb-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="406eb-147">Hallo na de opdracht toosee Hallo status van Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="406eb-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="406eb-148">In eerste instantie Hallo IP-adres wordt weergegeven als `pending`.</span><span class="sxs-lookup"><span data-stu-id="406eb-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="406eb-149">Na een paar minuten Hallo externe IP-adres van Hallo `iis` schil is ingesteld:</span><span class="sxs-lookup"><span data-stu-id="406eb-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="406eb-150">U kunt een webbrowser van uw keuze toosee Hallo IIS standaardwelkomstpagina op Hallo externe IP-adres gebruiken:</span><span class="sxs-lookup"><span data-stu-id="406eb-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Afbeelding van tooIIS bladeren](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="406eb-152">Cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="406eb-152">Delete cluster</span></span>
<span data-ttu-id="406eb-153">Wanneer Hallo cluster niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, containerservice en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="406eb-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="406eb-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="406eb-154">Next steps</span></span>

<span data-ttu-id="406eb-155">In deze snelstartgids hebt u een Kubernetes-cluster geïmplementeerd, het verbonden met `kubectl` en een schil met een IIS-container geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="406eb-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="406eb-156">toolearn meer informatie over Azure Container Service blijven toohello Kubernetes zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="406eb-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="406eb-157">Een ACS Kubernetes-cluster beheren</span><span class="sxs-lookup"><span data-stu-id="406eb-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
