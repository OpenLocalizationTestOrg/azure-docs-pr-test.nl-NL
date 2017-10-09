---
title: aaaLoad saldo containers in Azure DC/OS-cluster | Microsoft Docs
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
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="52846-104">Load balance containers in een Azure Container Service DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="52846-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="52846-105">In dit artikel wordt besproken hoe toocreate een interne load balancer in een DC/OS beheerd Azure Container Service met behulp van Marathon-Taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="52846-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="52846-106">Deze configuratie kunt u tooscale uw toepassingen horizontaal.</span><span class="sxs-lookup"><span data-stu-id="52846-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="52846-107">U kunt er ook tootake profiteren van Hallo openbare en persoonlijke agent clusters door het plaatsen van uw netwerktaakverdelers op Hallo openbare als uw toepassingscontainers op Hallo persoonlijke cluster.</span><span class="sxs-lookup"><span data-stu-id="52846-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="52846-108">In deze zelfstudie hebt u:</span><span class="sxs-lookup"><span data-stu-id="52846-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52846-109">Een Load Balancer van Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="52846-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="52846-110">Implementeer een toepassing met Hallo load balancer</span><span class="sxs-lookup"><span data-stu-id="52846-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="52846-111">Configureren en de Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="52846-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="52846-112">U moet een ACS DC/OS cluster toocomplete Hallo in deze zelfstudie stappen.</span><span class="sxs-lookup"><span data-stu-id="52846-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="52846-113">Indien nodig, [dit voorbeeldscript](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="52846-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="52846-114">Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="52846-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="52846-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="52846-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="52846-116">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52846-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="52846-117">Overzicht van netwerktaakverdeling</span><span class="sxs-lookup"><span data-stu-id="52846-117">Load balancing overview</span></span>

<span data-ttu-id="52846-118">Er zijn twee lagen voor taakverdeling in een Azure Container Service DC/OS-cluster:</span><span class="sxs-lookup"><span data-stu-id="52846-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="52846-119">**Azure Load Balancer** biedt openbare invoerpunten (hello toepassingsgroepen dat eindgebruikers toegang).</span><span class="sxs-lookup"><span data-stu-id="52846-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="52846-120">Een Azure LB automatisch wordt geleverd met Azure Container Service en is standaard geconfigureerd tooexpose poort 80 en 443 van 8080.</span><span class="sxs-lookup"><span data-stu-id="52846-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="52846-121">**Hallo Marathon-taakverdeling (marathon-taakverdeling)** routes inkomende aanvragen toocontainer instanties die deze aanvragen.</span><span class="sxs-lookup"><span data-stu-id="52846-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="52846-122">Hallo marathon-taakverdeling wordt dynamisch aangepast geschaald Hallo containers bieden onze webservice.</span><span class="sxs-lookup"><span data-stu-id="52846-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="52846-123">Deze load balancer is niet opgegeven in uw Containerservice standaard, maar het is gemakkelijk tooinstall.</span><span class="sxs-lookup"><span data-stu-id="52846-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="52846-124">Marathon-taakverdeling configureren</span><span class="sxs-lookup"><span data-stu-id="52846-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="52846-125">Marathon-taakverdeling opnieuw dynamisch geconfigureerd op basis van de Hallo-containers die u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="52846-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="52846-126">Het is ook robuuste toohello verlies van een container of agent - als dit het geval is, Apache Mesos elders Hallo container opnieuw is opgestart en marathon-taakverdeling past zich.</span><span class="sxs-lookup"><span data-stu-id="52846-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="52846-127">Hallo opdracht tooinstall Hallo marathon-taakverdeling te volgen op Hallo openbare agent cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="52846-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="52846-128">Taakverdeling toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="52846-128">Deploy load balanced application</span></span>

<span data-ttu-id="52846-129">Nu dat we Hallo marathon-taakverdeling pakket hebben, kunnen we een toepassingscontainer dat we tooload saldo wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="52846-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="52846-130">Eerst ophalen Hallo FQDN-naam van de agents Hallo openbaar beschikbaar gesteld.</span><span class="sxs-lookup"><span data-stu-id="52846-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="52846-131">Maak vervolgens een bestand met de naam *hello web.json* en de kopie in Hallo de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="52846-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="52846-132">Hallo `HAPROXY_0_VHOST` label moet toobe bijgewerkt met de FQDN-naam van de DC/OS-agents Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="52846-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

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

<span data-ttu-id="52846-133">Hallo DC/OS CLI toorun Hallo toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="52846-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="52846-134">Standaard implementeert Marathon Hallo Hallo toepassing toohello persoonlijke cluster.</span><span class="sxs-lookup"><span data-stu-id="52846-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="52846-135">Dit betekent dat Hallo hierboven implementatie is alleen toegankelijk via de load balancer, meestal Hallo gewenst gedrag.</span><span class="sxs-lookup"><span data-stu-id="52846-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="52846-136">Zodra het Hallo-toepassing is geïmplementeerd, blader toohello FQDN-naam van Hallo agent cluster tooview taakverdeling toepassing.</span><span class="sxs-lookup"><span data-stu-id="52846-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Afbeelding van taakverdeling toepassing](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="52846-138">Azure Load Balancer configureren</span><span class="sxs-lookup"><span data-stu-id="52846-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="52846-139">Standaard stelt de Azure Load Balancer poorten 80, 8080 en 443 open.</span><span class="sxs-lookup"><span data-stu-id="52846-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="52846-140">Als u een van deze drie poorten (zoals in Hallo bovenstaande voorbeeld) en er is niets moet u toodo op.</span><span class="sxs-lookup"><span data-stu-id="52846-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="52846-141">U kunt toohit moet de agent load balancer FQDN en telkens wanneer u vernieuwt u een van de drie webservers op een wijze round robin hebt bereikt.</span><span class="sxs-lookup"><span data-stu-id="52846-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="52846-142">Als u een andere poort gebruikt, moet u een round-robin tooadd regel en een test op Hallo load balancer voor Hallo-poort die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="52846-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="52846-143">U kunt dit doen vanuit Hallo [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), met Hallo opdrachten `azure network lb rule create` en `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="52846-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52846-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52846-144">Next steps</span></span>

<span data-ttu-id="52846-145">In deze zelfstudie hebt u geleerd over taakverdeling in ACS met zowel Hallo Marathon en Azure load balancers met inbegrip van Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="52846-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52846-146">Een Load Balancer van Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="52846-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="52846-147">Implementeer een toepassing met Hallo load balancer</span><span class="sxs-lookup"><span data-stu-id="52846-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="52846-148">Configureren en de Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="52846-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="52846-149">Ga toohello volgende zelfstudie toolearn over de integratie van Azure-opslag met DC/OS in Azure.</span><span class="sxs-lookup"><span data-stu-id="52846-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52846-150">De bestandsshare koppelen Azure in DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="52846-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)