---
title: Implementeer containers met Helm in Azure Kubernetes | Microsoft Docs
description: Het Helm verpakking-hulpprogramma gebruiken om de containers op een cluster Kubernetes in Azure Container Service implementeren
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
ms.openlocfilehash: 3cfcc5abbee03ca8fbbec4e4eae711e7c2d9deae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="64d1b-103">Helm gebruiken voor het implementeren van containers op een cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="64d1b-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="64d1b-104">[Helm](https://github.com/kubernetes/helm/) is een open source verpakking hulpprogramma waarmee u kunt installeren en beheren van de levenscyclus van Kubernetes toepassingen.</span><span class="sxs-lookup"><span data-stu-id="64d1b-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="64d1b-105">Net als bij Linux pakket managers zoals Apt get- en Yum, Helm wordt gebruikt voor het beheren van Kubernetes grafieken die pakketten van vooraf geconfigureerde Kubernetes resources zijn.</span><span class="sxs-lookup"><span data-stu-id="64d1b-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="64d1b-106">In dit artikel leest u hoe werken met Helm op een cluster Kubernetes is geïmplementeerd in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="64d1b-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="64d1b-107">Helm bestaat uit twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="64d1b-107">Helm has two components:</span></span> 
* <span data-ttu-id="64d1b-108">De **Helm CLI** een client die lokaal of in de cloud wordt uitgevoerd op uw computer</span><span class="sxs-lookup"><span data-stu-id="64d1b-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="64d1b-109">**Helmstok** is een server die wordt uitgevoerd op het cluster Kubernetes en beheert de levenscyclus van uw toepassingen Kubernetes</span><span class="sxs-lookup"><span data-stu-id="64d1b-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="64d1b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64d1b-110">Prerequisites</span></span>

* <span data-ttu-id="64d1b-111">[Maak een cluster Kubernetes](container-service-kubernetes-walkthrough.md) in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="64d1b-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="64d1b-112">[Installeer en configureer `kubectl` ](../container-service-connect.md) op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="64d1b-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="64d1b-113">[Installeer Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="64d1b-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="64d1b-114">Helm basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="64d1b-114">Helm basics</span></span> 

<span data-ttu-id="64d1b-115">Als u informatie over het Kubernetes-cluster dat u helmstok installeren en implementeren van uw toepassingen op, typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="64d1b-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="64d1b-117">Nadat u Helm hebt geïnstalleerd, installeert u helmstok op uw cluster Kubernetes door de volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="64d1b-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="64d1b-118">Wanneer het is voltooid, ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="64d1b-118">When it completes successfully, you see output like the following:</span></span>

![Helmstok installatie](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="64d1b-120">Als u wilt weergeven van alle Helm grafieken die beschikbaar is in de opslagplaats, typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="64d1b-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="64d1b-121">Ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="64d1b-121">You see output like the following:</span></span>

![Helm zoeken](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="64d1b-123">Voor het bijwerken van de grafieken om op te halen van de meest recente versies, typt u:</span><span class="sxs-lookup"><span data-stu-id="64d1b-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="64d1b-124">Een grafiek Nginx inkomend domeincontroller implementeren</span><span class="sxs-lookup"><span data-stu-id="64d1b-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="64d1b-125">Typ één opdracht voor het implementeren van een grafiek Nginx inkomend domeincontroller:</span><span class="sxs-lookup"><span data-stu-id="64d1b-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Inkomend domeincontroller implementeren](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="64d1b-127">Als u typt `kubectl get svc` om weer te geven van alle services die worden uitgevoerd op het cluster, u zien dat een IP-adres aan de domeincontroller inkomend is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="64d1b-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="64d1b-128">(Terwijl de toewijzing uitgevoerd wordt, ziet u `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="64d1b-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="64d1b-129">Het duurt een paar minuten duren.)</span><span class="sxs-lookup"><span data-stu-id="64d1b-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="64d1b-130">Na het IP-adres wordt toegewezen, gaat u naar de waarde van het externe IP-adres voor een overzicht van de Nginx back-end uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64d1b-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![Inkomend IP-adres](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="64d1b-132">Een lijst van grafieken geïnstalleerd op het cluster wilt bekijken, typt u:</span><span class="sxs-lookup"><span data-stu-id="64d1b-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="64d1b-133">U kunt ook de opdracht voor het opgeven `helm ls`.</span><span class="sxs-lookup"><span data-stu-id="64d1b-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="64d1b-134">Een grafiek MariaDB en de client implementeren</span><span class="sxs-lookup"><span data-stu-id="64d1b-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="64d1b-135">Een grafiek MariaDB en een client MariaDB verbinding maken met de database nu implementeren.</span><span class="sxs-lookup"><span data-stu-id="64d1b-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="64d1b-136">Typ de volgende opdracht voor het implementeren van de grafiek MariaDB:</span><span class="sxs-lookup"><span data-stu-id="64d1b-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="64d1b-137">waar `--name` een label dat is gebruikt voor versies.</span><span class="sxs-lookup"><span data-stu-id="64d1b-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="64d1b-138">Als de implementatie mislukt, voert u `helm repo update` en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="64d1b-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="64d1b-139">Als u wilt de diagrammen die zijn geïmplementeerd op het cluster weergeven, typt u:</span><span class="sxs-lookup"><span data-stu-id="64d1b-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="64d1b-140">Als u wilt weergeven van alle implementaties die worden uitgevoerd op uw cluster, typt u:</span><span class="sxs-lookup"><span data-stu-id="64d1b-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="64d1b-141">Ten slotte voor het uitvoeren van een schil om toegang tot de client, typt u:</span><span class="sxs-lookup"><span data-stu-id="64d1b-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="64d1b-142">Voor verbinding met de client, typt u de volgende opdracht, vervangen `v1-mariadb` met de naam van uw implementatie:</span><span class="sxs-lookup"><span data-stu-id="64d1b-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="64d1b-143">U kunt de standaard SQL-opdrachten nu gebruiken voor het maken van databases, tabellen, enzovoort. Bijvoorbeeld: `Create DATABASE testdb1;` maakt een lege database.</span><span class="sxs-lookup"><span data-stu-id="64d1b-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="64d1b-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64d1b-144">Next steps</span></span>

* <span data-ttu-id="64d1b-145">Zie voor meer informatie over het beheren van Kubernetes grafieken de [Helm documentatie](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="64d1b-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

