---
title: aaaDeploy containers met Helm in Azure Kubernetes | Microsoft Docs
description: Hallo Helm verpakking hulpprogramma toodeploy containers gebruiken op een cluster Kubernetes in Azure Container Service
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="079dc-103">Helm toodeploy containers op een cluster Kubernetes gebruiken</span><span class="sxs-lookup"><span data-stu-id="079dc-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="079dc-104">[Helm](https://github.com/kubernetes/helm/) is een open source verpakking hulpprogramma waarmee u kunt installeren en Hallo levenscyclus van Kubernetes toepassingen beheren.</span><span class="sxs-lookup"><span data-stu-id="079dc-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="079dc-105">Vergelijkbare tooLinux pakket managers zoals Apt get- en Yum Helm is gebruikte toomanage Kubernetes grafieken, pakketten van vooraf geconfigureerde Kubernetes resources zijn.</span><span class="sxs-lookup"><span data-stu-id="079dc-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="079dc-106">Dit artikel laat zien hoe toowork met Helm op een cluster Kubernetes geïmplementeerd in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="079dc-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="079dc-107">Helm bestaat uit twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="079dc-107">Helm has two components:</span></span> 
* <span data-ttu-id="079dc-108">Hallo **Helm CLI** een client die wordt uitgevoerd op uw computer, lokaal of in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="079dc-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="079dc-109">**Helmstok** is een server die wordt uitgevoerd op Hallo Kubernetes cluster en beheert Hallo levenscyclus van uw toepassingen Kubernetes</span><span class="sxs-lookup"><span data-stu-id="079dc-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="079dc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="079dc-110">Prerequisites</span></span>

* <span data-ttu-id="079dc-111">[Maak een cluster Kubernetes](container-service-kubernetes-walkthrough.md) in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="079dc-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="079dc-112">[Installeer en configureer `kubectl` ](../container-service-connect.md) op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="079dc-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="079dc-113">[Installeer Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="079dc-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="079dc-114">Helm basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="079dc-114">Helm basics</span></span> 

<span data-ttu-id="079dc-115">tooview informatie over Hallo Kubernetes cluster dat u helmstok installeren en implementeren van uw toepassingen op, typ Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="079dc-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="079dc-117">Nadat u Helm hebt geïnstalleerd, installeert u helmstok op uw cluster Kubernetes door Hallo volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="079dc-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="079dc-118">Wanneer het is voltooid, ziet u uitvoer zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="079dc-118">When it completes successfully, you see output like hello following:</span></span>

![Helmstok installatie](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="079dc-120">tooview alle Hallo Helm grafieken beschikbaar in Hallo-opslagplaats, type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="079dc-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="079dc-121">U weergegeven Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="079dc-121">You see output like hello following:</span></span>

![Helm zoeken](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="079dc-123">tooupdate hello grafieken tooget Hallo meest recente versies, typt u:</span><span class="sxs-lookup"><span data-stu-id="079dc-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="079dc-124">Een grafiek Nginx inkomend domeincontroller implementeren</span><span class="sxs-lookup"><span data-stu-id="079dc-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="079dc-125">toodeploy een grafiek Nginx ingress-controller, typt u een één-opdracht:</span><span class="sxs-lookup"><span data-stu-id="079dc-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Inkomend domeincontroller implementeren](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="079dc-127">Als u typt `kubectl get svc` tooview alle services die worden uitgevoerd op Hallo-cluster, die u ziet dat een IP-adres toohello inkomend controller is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="079dc-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="079dc-128">(Terwijl het Hallo-toewijzing wordt uitgevoerd, ziet u `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="079dc-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="079dc-129">Het duurt een paar minuten toocomplete.)</span><span class="sxs-lookup"><span data-stu-id="079dc-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="079dc-130">Nadat het Hallo IP-adres wordt toegewezen, gaat u toohello waarde van Hallo externe IP-adres toosee hello Nginx back-end uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="079dc-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Inkomend IP-adres](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="079dc-132">toosee een lijst met grafieken geïnstalleerd op uw cluster, type:</span><span class="sxs-lookup"><span data-stu-id="079dc-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="079dc-133">U kunt ook de opdracht hello te opgeven`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="079dc-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="079dc-134">Een grafiek MariaDB en de client implementeren</span><span class="sxs-lookup"><span data-stu-id="079dc-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="079dc-135">Een grafiek MariaDB en een MariaDB client tooconnect toohello database nu implementeren.</span><span class="sxs-lookup"><span data-stu-id="079dc-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="079dc-136">toodeploy hello MariaDB grafiek, type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="079dc-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="079dc-137">waar `--name` een label dat is gebruikt voor versies.</span><span class="sxs-lookup"><span data-stu-id="079dc-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="079dc-138">Als het Hallo-implementatie mislukt, voert u `helm repo update` en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="079dc-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="079dc-139">tooview alle Hallo grafieken geïmplementeerd op het cluster, type:</span><span class="sxs-lookup"><span data-stu-id="079dc-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="079dc-140">tooview alle implementaties die worden uitgevoerd op uw cluster, typt u:</span><span class="sxs-lookup"><span data-stu-id="079dc-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="079dc-141">Ten slotte toorun een schil tooaccess Hallo client, typt u:</span><span class="sxs-lookup"><span data-stu-id="079dc-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="079dc-142">type Hallo de volgende opdracht en vervangt-client toohello tooconnect `v1-mariadb` met Hallo-naam van uw implementatie:</span><span class="sxs-lookup"><span data-stu-id="079dc-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="079dc-143">U kunt nu standaard SQL-opdrachten toocreate databases, tabellen, enzovoort. Bijvoorbeeld: `Create DATABASE testdb1;` maakt een lege database.</span><span class="sxs-lookup"><span data-stu-id="079dc-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="079dc-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="079dc-144">Next steps</span></span>

* <span data-ttu-id="079dc-145">Zie voor meer informatie over het beheren van Kubernetes grafieken Hallo [Helm documentatie](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="079dc-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

