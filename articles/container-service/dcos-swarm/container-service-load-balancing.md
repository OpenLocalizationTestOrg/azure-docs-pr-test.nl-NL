---
title: Laden van saldo containers in Azure DC/OS-cluster | Microsoft Docs
description: Verdelen over meerdere containers in een Azure Container Service DC/OS-cluster.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, Micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="473f0-104">Load balance containers in een Azure Container Service DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="473f0-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="473f0-105">In dit artikel wordt besproken voor het maken van een interne load balancer in een DC/OS beheerd-Azure Containerservice met behulp van Marathon-Taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="473f0-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="473f0-106">Deze configuratie kunt u uw toepassingen horizontaal schalen.</span><span class="sxs-lookup"><span data-stu-id="473f0-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="473f0-107">Ook kunt u profiteren van de openbare en persoonlijke agent clusters door het plaatsen van uw netwerktaakverdelers op het openbare als uw toepassingscontainers op het persoonlijke cluster.</span><span class="sxs-lookup"><span data-stu-id="473f0-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="473f0-108">In deze zelfstudie hebt u:</span><span class="sxs-lookup"><span data-stu-id="473f0-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="473f0-109">Een Load Balancer van Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="473f0-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="473f0-110">Implementeer een toepassing met behulp van de load balancer</span><span class="sxs-lookup"><span data-stu-id="473f0-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="473f0-111">Configureren en de Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="473f0-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="473f0-112">U moet een ACS-DC/OS-cluster de stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="473f0-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="473f0-113">Indien nodig, [dit voorbeeldscript](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="473f0-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="473f0-114">Voor deze zelfstudie is versie 2.0.4 of hoger van de Azure CLI vereist.</span><span class="sxs-lookup"><span data-stu-id="473f0-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="473f0-115">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="473f0-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="473f0-116">Als u Azure CLI 2.0 wilt upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="473f0-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="473f0-117">Overzicht van netwerktaakverdeling</span><span class="sxs-lookup"><span data-stu-id="473f0-117">Load balancing overview</span></span>

<span data-ttu-id="473f0-118">Er zijn twee lagen voor taakverdeling in een Azure Container Service DC/OS-cluster:</span><span class="sxs-lookup"><span data-stu-id="473f0-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="473f0-119">**Azure Load Balancer** biedt openbare invoerpunten (de waarden die eindgebruikers toegang).</span><span class="sxs-lookup"><span data-stu-id="473f0-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="473f0-120">Een Azure LB automatisch wordt geleverd met Azure Container Service en is standaard geconfigureerd om poort 80 en 443 van 8080 weer te geven.</span><span class="sxs-lookup"><span data-stu-id="473f0-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="473f0-121">**De Marathon-taakverdeling (marathon-taakverdeling)** routes binnenkomende aanvragen naar containerexemplaren die aanvragen voor deze service.</span><span class="sxs-lookup"><span data-stu-id="473f0-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="473f0-122">De marathon-taakverdeling wordt dynamisch aangepast geschaald de containers bieden onze webservice.</span><span class="sxs-lookup"><span data-stu-id="473f0-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="473f0-123">Deze load balancer is niet opgegeven in uw Containerservice standaard, maar het is eenvoudig te installeren.</span><span class="sxs-lookup"><span data-stu-id="473f0-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="473f0-124">Marathon-taakverdeling configureren</span><span class="sxs-lookup"><span data-stu-id="473f0-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="473f0-125">Marathon Load Balancer herconfigureert zichzelf dynamisch op basis van de containers die u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="473f0-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="473f0-126">Het is ook aan het verlies van een container of agent - als dit het geval is, Apache Mesos elders in de container opnieuw is opgestart en marathon-taakverdeling past zich.</span><span class="sxs-lookup"><span data-stu-id="473f0-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="473f0-127">Voer de volgende opdracht voor het installeren van de marathon-taakverdeling op de openbare agent-cluster.</span><span class="sxs-lookup"><span data-stu-id="473f0-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="473f0-128">Taakverdeling toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="473f0-128">Deploy load balanced application</span></span>

<span data-ttu-id="473f0-129">Nu we het Marathon-LB-pakket hebben, kunnen we een toepassingscontainer implementeren waarvan we de taken willen verdelen.</span><span class="sxs-lookup"><span data-stu-id="473f0-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="473f0-130">De FQDN-naam van de agents die openbaar blootgestelde eerst worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="473f0-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="473f0-131">Maak vervolgens een bestand met de naam *hello web.json* en kopieer de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="473f0-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="473f0-132">De `HAPROXY_0_VHOST` label moet worden bijgewerkt met de FQDN van de DC/OS-agents.</span><span class="sxs-lookup"><span data-stu-id="473f0-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
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
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="473f0-133">Gebruik de DC/OS CLI de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="473f0-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="473f0-134">Standaard Marathon implementeert het de toepassing naar de persoonlijke cluster.</span><span class="sxs-lookup"><span data-stu-id="473f0-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="473f0-135">Dit betekent dat de bovenstaande implementatie alleen toegankelijk via de load balancer is, dit is meestal het gewenste gedrag.</span><span class="sxs-lookup"><span data-stu-id="473f0-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="473f0-136">Zodra de toepassing is geïmplementeerd, blader naar de FQDN-naam van het cluster agent taakverdeling toepassing weergeven.</span><span class="sxs-lookup"><span data-stu-id="473f0-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Afbeelding van taakverdeling toepassing](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="473f0-138">Azure Load Balancer configureren</span><span class="sxs-lookup"><span data-stu-id="473f0-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="473f0-139">Standaard stelt de Azure Load Balancer poorten 80, 8080 en 443 open.</span><span class="sxs-lookup"><span data-stu-id="473f0-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="473f0-140">Als u een van deze drie poorten gebruikt (zoals we dit in het bovenstaande voorbeeld doen), dan hoeft u niets te doen.</span><span class="sxs-lookup"><span data-stu-id="473f0-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="473f0-141">U moet kunnen om de load balancer-uw agent FQDN en telkens wanneer die u vernieuwt u een van de drie webservers op een wijze round robin hebt bereikt.</span><span class="sxs-lookup"><span data-stu-id="473f0-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="473f0-142">Als u een andere poort gebruikt, moet u een round-robinregel en een test toevoegen op de load balancer voor de poort die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="473f0-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="473f0-143">Dit kan vanuit de [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), met de opdrachten `azure network lb rule create` en `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="473f0-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="473f0-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="473f0-144">Next steps</span></span>

<span data-ttu-id="473f0-145">In deze zelfstudie hebt u geleerd over taakverdeling in ACS aan het Marathon- en Azure load balancers met inbegrip van de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="473f0-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="473f0-146">Een Load Balancer van Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="473f0-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="473f0-147">Implementeer een toepassing met behulp van de load balancer</span><span class="sxs-lookup"><span data-stu-id="473f0-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="473f0-148">Configureren en de Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="473f0-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="473f0-149">Ga naar de volgende zelfstudie voor meer informatie over de integratie van Azure-opslag met DC/OS in Azure.</span><span class="sxs-lookup"><span data-stu-id="473f0-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="473f0-150">De bestandsshare koppelen Azure in DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="473f0-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)