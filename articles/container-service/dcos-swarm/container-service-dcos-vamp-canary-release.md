---
title: Kokospalm release met Vamp op Azure DC/OS-cluster | Microsoft Docs
description: Het gebruik van Vamp kokospalm release Services en toepassen van slimme verkeer filteren op een Azure Container Service DC/OS-cluster
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: 4a20091b59f2643ea71cce99c159a5075706e35d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="63c3d-103">Kokospalm release microservices met Vamp in een Azure Container Service DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="63c3d-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="63c3d-104">In dit scenario stelt Vamp op Azure Container Service met een DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="63c3d-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="63c3d-105">We kokospalm release van de Vamp demoservice 'sava' en vervolgens incompatibiliteit van de service met Firefox oplossen door toe te passen smart verkeer gefilterd.</span><span class="sxs-lookup"><span data-stu-id="63c3d-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="63c3d-106">In dit overzicht Vamp wordt uitgevoerd op een DC/OS-cluster, maar u kunt ook Vamp met Kubernetes gebruiken als de orchestrator.</span><span class="sxs-lookup"><span data-stu-id="63c3d-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="63c3d-107">Over Canarische vrijgegeven en Vamp</span><span class="sxs-lookup"><span data-stu-id="63c3d-107">About canary releases and Vamp</span></span>


<span data-ttu-id="63c3d-108">[Vrijgeven van kokospalm](https://martinfowler.com/bliki/CanaryRelease.html) is een strategie voor slimme implementatie door innovatieve organisaties zoals Netflix, Facebook en Spotify vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="63c3d-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="63c3d-109">Het is een benadering die logisch, klinkt omdat deze problemen vermindert veiligheid netten introduceert en verhoogt de vernieuwing.</span><span class="sxs-lookup"><span data-stu-id="63c3d-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="63c3d-110">Waarom worden niet alle bedrijven met behulp van deze?</span><span class="sxs-lookup"><span data-stu-id="63c3d-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="63c3d-111">Uitbreiden van een pijplijn CI/CD om op te nemen kokospalm strategieën voegt complexiteit en uitgebreide devops kennis en ervaring vereist.</span><span class="sxs-lookup"><span data-stu-id="63c3d-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="63c3d-112">Dit is voldoende is voor het blokkeren van kleinere bedrijfs- en ondernemingsbeheer zowel voordat ze ook aan de slag.</span><span class="sxs-lookup"><span data-stu-id="63c3d-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="63c3d-113">[Vamp](http://vamp.io/) brengt een open source-systeem ontworpen voor het vereenvoudigen van deze overgang en brengt Canarische functies aan uw voorkeur container scheduler.</span><span class="sxs-lookup"><span data-stu-id="63c3d-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span></span> <span data-ttu-id="63c3d-114">De vamp kokospalm functionaliteit zich verder uitstrekt dan implementaties op basis van een percentage.</span><span class="sxs-lookup"><span data-stu-id="63c3d-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="63c3d-115">Verkeer kan worden gefilterd en splitst bij een breed scala aan de voorwaarden, bijvoorbeeld voor het doel specifieke gebruikers, IP-adresbereiken of apparaten.</span><span class="sxs-lookup"><span data-stu-id="63c3d-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="63c3d-116">Vamp houdt en maatstaven voor prestaties, zodat voor automatisering op basis van echte gegevens analyseert.</span><span class="sxs-lookup"><span data-stu-id="63c3d-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="63c3d-117">U kunt instellen op automatisch herstel op fouten of afzonderlijke service varianten op basis van load of latentie schalen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="63c3d-118">Azure Container Service met DC/OS instellen</span><span class="sxs-lookup"><span data-stu-id="63c3d-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="63c3d-119">[Een DC/OS-cluster implementeren](container-service-deployment.md) met één master en twee agents van standaardgrootte.</span><span class="sxs-lookup"><span data-stu-id="63c3d-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="63c3d-120">[Maken van een SSH-tunnel](../container-service-connect.md) verbinding maken met de DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="63c3d-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span></span> <span data-ttu-id="63c3d-121">In dit artikel wordt ervan uitgegaan dat u tunnel aan het cluster op de lokale poort 80.</span><span class="sxs-lookup"><span data-stu-id="63c3d-121">This article assumes that you tunnel to the cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="63c3d-122">Vamp instellen</span><span class="sxs-lookup"><span data-stu-id="63c3d-122">Set up Vamp</span></span>

<span data-ttu-id="63c3d-123">Nu dat u een actieve DC/OS-cluster hebt, kunt u Vamp installeren vanaf de DC/OS-gebruikersinterface (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="63c3d-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span></span> 

![DC/OS-webgebruikersinterface](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="63c3d-125">De installatie wordt uitgevoerd in twee fasen:</span><span class="sxs-lookup"><span data-stu-id="63c3d-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="63c3d-126">**Implementeer Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="63c3d-127">Vervolgens **Vamp implementeren** door de DC/OS Vamp universe pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="63c3d-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="63c3d-128">Elasticsearch implementeren</span><span class="sxs-lookup"><span data-stu-id="63c3d-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="63c3d-129">Elasticsearch vereist vamp voor het verzamelen van de metrische gegevens en aggregatie.</span><span class="sxs-lookup"><span data-stu-id="63c3d-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="63c3d-130">U kunt de [magneticio Docker installatiekopieën](https://hub.docker.com/r/magneticio/elastic/) voor het implementeren van een compatibel Vamp Elasticsearch-stack.</span><span class="sxs-lookup"><span data-stu-id="63c3d-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="63c3d-131">Ga in de DC/OS-gebruikersinterface naar **Services** en klik op **Service implementeren**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="63c3d-132">Selecteer **JSON-modus** van de **nieuwe Service implementeren** pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="63c3d-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span></span>

  ![Selecteer JSON-modus](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="63c3d-134">In de volgende JSON plakken.</span><span class="sxs-lookup"><span data-stu-id="63c3d-134">Paste in the following JSON.</span></span> <span data-ttu-id="63c3d-135">Deze configuratie wordt de container met 1 GB RAM-geheugen en een eenvoudige statuscontrole op de poort Elasticsearch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63c3d-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="63c3d-136">Klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-136">Click **Deploy**.</span></span>

  <span data-ttu-id="63c3d-137">DC/OS implementeert de Elasticsearch-container.</span><span class="sxs-lookup"><span data-stu-id="63c3d-137">DC/OS deploys the Elasticsearch container.</span></span> <span data-ttu-id="63c3d-138">U kunt de voortgang volgen op de **Services** pagina.</span><span class="sxs-lookup"><span data-stu-id="63c3d-138">You can track progress on the **Services** page.</span></span>  

  ![e implementeren? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="63c3d-140">Vamp implementeren</span><span class="sxs-lookup"><span data-stu-id="63c3d-140">Deploy Vamp</span></span>

<span data-ttu-id="63c3d-141">Zodra Elasticsearch als rapporteert **met**, kunt u het pakket Vamp DC/OS Universe toevoegen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="63c3d-142">Ga naar **Universe** en zoek naar **vamp**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-142">Go to **Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="63c3d-143">![Vamp op DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="63c3d-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="63c3d-144">Klik op **installeren** naast de vamp van het pakket en kies **installatie in de geavanceerde**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="63c3d-145">Schuif naar beneden en voer de volgende elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="63c3d-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Voer de URL Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="63c3d-147">Klik op **Bekijk en installeer**, klikt u vervolgens op **installeren** implementatie te starten.</span><span class="sxs-lookup"><span data-stu-id="63c3d-147">Click **Review and Install**, then click **Install** to start the deployment.</span></span>  

  <span data-ttu-id="63c3d-148">DC/OS implementeert alle vereiste Vamp onderdelen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="63c3d-149">U kunt de voortgang volgen op de **Services** pagina.</span><span class="sxs-lookup"><span data-stu-id="63c3d-149">You can track progress on the **Services** page.</span></span>
  
  ![Vamp als universe pakket implementeren](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="63c3d-151">Zodra de implementatie is voltooid, kunt u toegang tot de gebruikersinterface Vamp:</span><span class="sxs-lookup"><span data-stu-id="63c3d-151">Once deployment has completed, you can access the Vamp UI:</span></span>

  ![-Service op de DC/OS vamp](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp gebruikersinterface](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="63c3d-154">Uw eerste service implementeren</span><span class="sxs-lookup"><span data-stu-id="63c3d-154">Deploy your first service</span></span>

<span data-ttu-id="63c3d-155">Nu dat Vamp actief en werkend is, een service implementeren vanuit een blauwdruk.</span><span class="sxs-lookup"><span data-stu-id="63c3d-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="63c3d-156">In de meest eenvoudige vorm een [Vamp blauwdruk](http://vamp.io/documentation/using-vamp/blueprints/) beschrijft de eindpunten (gateways), clusters en services te implementeren.</span><span class="sxs-lookup"><span data-stu-id="63c3d-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span></span> <span data-ttu-id="63c3d-157">Vamp clusters gebruikt om verschillende varianten van dezelfde service te groeperen in logische groepen voor kokospalm vrijgeven of A / B-tests.</span><span class="sxs-lookup"><span data-stu-id="63c3d-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="63c3d-158">Dit scenario wordt gebruikt voor een voorbeeldtoepassing monolithische aangeroepen [ **sava**](https://github.com/magneticio/sava), die is op versie 1.0.</span><span class="sxs-lookup"><span data-stu-id="63c3d-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="63c3d-159">De monoliet wordt verpakt in een Docker-container in Docker-Hub onder de magneticio/sava:1.0.0 ligt.</span><span class="sxs-lookup"><span data-stu-id="63c3d-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="63c3d-160">De app wordt normaal uitgevoerd op poort 8080, maar u wilt in dit geval onder poort 9050 weergeven.</span><span class="sxs-lookup"><span data-stu-id="63c3d-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span></span> <span data-ttu-id="63c3d-161">Implementeer de app via Vamp met behulp van een eenvoudige blauwdruk.</span><span class="sxs-lookup"><span data-stu-id="63c3d-161">Deploy the app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="63c3d-162">Ga naar **implementaties**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-162">Go to **Deployments**.</span></span>

2. <span data-ttu-id="63c3d-163">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-163">Click **Add**.</span></span>

3. <span data-ttu-id="63c3d-164">In de volgende blauwdruk YAML te plakken.</span><span class="sxs-lookup"><span data-stu-id="63c3d-164">Paste in the following blueprint YAML.</span></span> <span data-ttu-id="63c3d-165">Deze blauwdruk bevat één cluster met slechts één service-variant, die we in een latere stap wijzigen:</span><span class="sxs-lookup"><span data-stu-id="63c3d-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster to create
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="63c3d-166">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-166">Click **Save**.</span></span> <span data-ttu-id="63c3d-167">Vamp initieert de implementatie.</span><span class="sxs-lookup"><span data-stu-id="63c3d-167">Vamp initiates the deployment.</span></span>

<span data-ttu-id="63c3d-168">De implementatie wordt weergegeven op de **implementaties** pagina.</span><span class="sxs-lookup"><span data-stu-id="63c3d-168">The deployment is listed on the **Deployments** page.</span></span> <span data-ttu-id="63c3d-169">Klik op de implementatie als de status wilt controleren.</span><span class="sxs-lookup"><span data-stu-id="63c3d-169">Click the deployment to monitor its status.</span></span>

![UI - sava implementeren vamp](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![de service Sava in Vamp gebruikersinterface](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="63c3d-172">Twee gateways worden gemaakt, die worden vermeld op de **Gateways** pagina:</span><span class="sxs-lookup"><span data-stu-id="63c3d-172">Two gateways are created, which are listed on the **Gateways** page:</span></span>

* <span data-ttu-id="63c3d-173">een stabiele eindpunt voor toegang tot de service (poort 9050)</span><span class="sxs-lookup"><span data-stu-id="63c3d-173">a stable endpoint to access the running service (port 9050)</span></span> 
* <span data-ttu-id="63c3d-174">een beheerde Vamp interne gateway (meer informatie over deze gateway later).</span><span class="sxs-lookup"><span data-stu-id="63c3d-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![UI - sava gateways vamp](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="63c3d-176">De service sava is nu geïmplementeerd, maar u geen toegang tot deze extern omdat de Load Balancer van Azure voor het doorsturen van verkeer naar deze nog niet weet.</span><span class="sxs-lookup"><span data-stu-id="63c3d-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span></span> <span data-ttu-id="63c3d-177">Voor toegang tot de service, werk de netwerkconfiguratie van Azure.</span><span class="sxs-lookup"><span data-stu-id="63c3d-177">To access the service, update the Azure networking configuration.</span></span>


## <a name="update-the-azure-network-configuration"></a><span data-ttu-id="63c3d-178">Werk de configuratie van de Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="63c3d-178">Update the Azure network configuration</span></span>

<span data-ttu-id="63c3d-179">Vamp de sava-service op de DC/OS-agent knooppunten, die een stabiele eindpunt op poort 9050 geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="63c3d-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="63c3d-180">Voor toegang tot de service van buiten het DC/OS-cluster, moet u de volgende wijzigingen aanbrengen aan de configuratie van de Azure-netwerk in uw implementatie van het cluster:</span><span class="sxs-lookup"><span data-stu-id="63c3d-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="63c3d-181">**Configureren van de Azure Load Balancer** voor de agents (de resource met de naam **dcos-agent-lb-xxxx**) met een health test en een regel voor het doorsturen van verkeer op poort 9050 naar de sava-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="63c3d-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span></span> 

2. <span data-ttu-id="63c3d-182">**Bijwerken van de netwerkbeveiligingsgroep** voor de openbare agents (de resource met de naam **XXXX-agent-openbare-nsg-XXXX**)-verkeer op poort 9050 toestaan.</span><span class="sxs-lookup"><span data-stu-id="63c3d-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span></span>

<span data-ttu-id="63c3d-183">Zie voor gedetailleerde stappen voor het voltooien van deze taken met de Azure portal [openbare toegang tot een Azure Container Service-toepassing](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="63c3d-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="63c3d-184">Poort 9050 voor alle poortinstellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="63c3d-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="63c3d-185">Zodra u alles is gemaakt, gaat u naar de **overzicht** blade van de load balancer voor DC/OS-agent (de resource met de naam **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="63c3d-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="63c3d-186">Zoek de **openbaar IP-adres**, en het gebruik van het adres voor toegang tot sava op poort 9050.</span><span class="sxs-lookup"><span data-stu-id="63c3d-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span></span>

![Azure portal - get openbaar IP-adres](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![Sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="63c3d-189">Voer een kokospalm release</span><span class="sxs-lookup"><span data-stu-id="63c3d-189">Run a canary release</span></span>

<span data-ttu-id="63c3d-190">Stel dat u hebt een nieuwe versie van deze toepassing die u wilt kokospalm release in productie.</span><span class="sxs-lookup"><span data-stu-id="63c3d-190">Suppose you have a new version of this application that you want to canary release into production.</span></span> <span data-ttu-id="63c3d-191">U hebt het beperkte als magneticio/sava:1.1.0 en klaar bent om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="63c3d-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span></span> <span data-ttu-id="63c3d-192">Vamp kunt u eenvoudig nieuwe services toegevoegd aan de actieve implementatie.</span><span class="sxs-lookup"><span data-stu-id="63c3d-192">Vamp lets you easily add new services to the running deployment.</span></span> <span data-ttu-id="63c3d-193">Deze 'samengevoegde' services worden geïmplementeerd naast de bestaande services in het cluster en een gewicht van 0% wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="63c3d-194">Er is geen verkeer wordt doorgestuurd naar een nieuwe, samengevoegde service totdat u de distributie van verkeer aanpassen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span></span> <span data-ttu-id="63c3d-195">De schuifregelaar gewicht in de gebruikersinterface Vamp biedt u volledige controle over de distributie, waardoor het incrementele aanpassingen (kokospalm release) of een directe terugdraaien.</span><span class="sxs-lookup"><span data-stu-id="63c3d-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="63c3d-196">Een nieuwe service-variant samenvoegen</span><span class="sxs-lookup"><span data-stu-id="63c3d-196">Merge a new service variant</span></span>

<span data-ttu-id="63c3d-197">Samenvoegen van de nieuwe sava 1.1-service met de actieve implementatie:</span><span class="sxs-lookup"><span data-stu-id="63c3d-197">To merge the new sava 1.1 service with the running deployment:</span></span>

1. <span data-ttu-id="63c3d-198">Klik in de gebruikersinterface Vamp **blauwdrukken**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-198">In the Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="63c3d-199">Klik op **toevoegen** en plak in de volgende blauwdruk YAML: deze blauwdruk wordt een nieuwe service-variant (sava: 1.1.0) te implementeren binnen het bestaande cluster (sava_cluster) beschreven.</span><span class="sxs-lookup"><span data-stu-id="63c3d-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster to update
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint to update
  ```
  
3. <span data-ttu-id="63c3d-200">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-200">Click **Save**.</span></span> <span data-ttu-id="63c3d-201">De blauwdruk wordt opgeslagen en weergegeven op de **blauwdrukken** pagina.</span><span class="sxs-lookup"><span data-stu-id="63c3d-201">The blueprint is stored and listed on the **Blueprints** page.</span></span>

4. <span data-ttu-id="63c3d-202">Open het actiemenu op de blauwdruk sava: 1.1 en klik op **samenvoegen naar**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span></span>

  ![UI - blauwdrukken vamp](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="63c3d-204">Selecteer de **sava** implementatie en klik op **samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-204">Select the **sava** deployment and click **Merge**.</span></span>

  ![UI - samenvoegen blauwdruk aan implementatie vamp](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="63c3d-206">Vamp implementeert de nieuwe service-variant voor sava: 1.1.0 is beschreven in de blauwdruk naast sava: 1.0.0 in de **sava_cluster** van de actieve implementatie.</span><span class="sxs-lookup"><span data-stu-id="63c3d-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span></span> 

![UI - bijgewerkte sava implementatie vamp](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="63c3d-208">De **sava_cluster-sava/webport** gateway (de clustereindpunt) wordt ook bijgewerkt, een route toe te voegen aan de zojuist geïmplementeerde sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="63c3d-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span></span> <span data-ttu-id="63c3d-209">Op dit moment geen verkeer wordt gerouteerd hier (de **gewicht** is ingesteld op 0%).</span><span class="sxs-lookup"><span data-stu-id="63c3d-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span></span>

![UI - cluster gateway vamp](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="63c3d-211">Kokospalm release</span><span class="sxs-lookup"><span data-stu-id="63c3d-211">Canary release</span></span>

<span data-ttu-id="63c3d-212">Met beide versies van sava in hetzelfde cluster wordt geïmplementeerd, past u de distributie van verkeer tussen hen worden verplaatst de **gewicht** schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="63c3d-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span></span>

1. <span data-ttu-id="63c3d-213">Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) naast **gewicht**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span></span>

2. <span data-ttu-id="63c3d-214">De gewichtsdistributie ingesteld op 50% / 50% en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="63c3d-214">Set the weight distribution to 50%/50% and click **Save**.</span></span>

  ![UI - gateway gewicht schuifregelaar vamp](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="63c3d-216">Ga terug naar uw browser en vernieuw de pagina sava een paar keer.</span><span class="sxs-lookup"><span data-stu-id="63c3d-216">Go back to your browser and refresh the sava page a few more times.</span></span> <span data-ttu-id="63c3d-217">De toepassing sava nu schakelt u tussen een sava: 1.0 en een pagina sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="63c3d-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![wisselende sava1.0 en sava1.1 services](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="63c3d-219">Deze alternatieven van de pagina geschikt is voor de 'Incognito' of 'Anonymous' modus van uw browser vanwege de caching van statische elementen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="63c3d-220">Filteren van verkeer</span><span class="sxs-lookup"><span data-stu-id="63c3d-220">Filter traffic</span></span>

<span data-ttu-id="63c3d-221">Stel dat na implementatie dat u een incompatibiliteit in sava: 1.1.0 dat oorzaken problemen worden weergegeven in browsers Firefox gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="63c3d-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="63c3d-222">U kunt Vamp binnenkomend verkeer filteren en omleiden dat alle Firefox gebruikers terug naar de bekende stabiele sava: 1.0.0 instellen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span></span> <span data-ttu-id="63c3d-223">Dit filter herstelt direct de onderbreking voor Firefox gebruikers, terwijl alle andere nog steeds profiteren van de voordelen van het verbeterde sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="63c3d-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span></span>

<span data-ttu-id="63c3d-224">Maakt gebruik van vamp **voorwaarden** op het filter-verkeer tussen routes in een gateway.</span><span class="sxs-lookup"><span data-stu-id="63c3d-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span></span> <span data-ttu-id="63c3d-225">Het verkeer wordt eerst gefilterd en omgeleid op basis van de voorwaarden die bij elke route.</span><span class="sxs-lookup"><span data-stu-id="63c3d-225">Traffic is first filtered and directed according to the conditions applied to each route.</span></span> <span data-ttu-id="63c3d-226">Alle resterende verkeer wordt verdeeld volgens de instelling voor het gewicht van gateway.</span><span class="sxs-lookup"><span data-stu-id="63c3d-226">All remaining traffic is distributed according to the gateway weight setting.</span></span>

<span data-ttu-id="63c3d-227">U kunt een voorwaarde voor het filteren van alle Firefox gebruikers en ze rechtstreeks naar de oude sava: 1.0.0 maken:</span><span class="sxs-lookup"><span data-stu-id="63c3d-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span></span>

1. <span data-ttu-id="63c3d-228">Op sava/sava_cluster/webport **Gateways** pagina, klikt u op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) om toe te voegen een **voorwaarde** naar de sava/sava_cluster/sava:1.0.0/webport route.</span><span class="sxs-lookup"><span data-stu-id="63c3d-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="63c3d-229">Voer de voorwaarde **gebruikersagent Firefox ==** en klik op ![Vamp UI - opslaan](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="63c3d-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="63c3d-230">Vamp voegt de voorwaarde van een standaardwaarde van 0%.</span><span class="sxs-lookup"><span data-stu-id="63c3d-230">Vamp adds the condition with a default strength of 0%.</span></span> <span data-ttu-id="63c3d-231">Als u wilt filteren van verkeer, moet u de voorwaarde sterkte aanpassen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-231">To start filtering traffic, you need to adjust the condition strength.</span></span>

3. <span data-ttu-id="63c3d-232">Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) wijzigen de **sterkte** aan de voorwaarde wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="63c3d-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span></span>
 
4. <span data-ttu-id="63c3d-233">Stel de **sterkte** naar 100%, klik op ![Vamp UI - opslaan](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) om op te slaan.</span><span class="sxs-lookup"><span data-stu-id="63c3d-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span></span>

  <span data-ttu-id="63c3d-234">Vamp verzendt nu al het verkeer die overeenkomt met de voorwaarde (alle Firefox gebruikers) voor het sava: 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="63c3d-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span></span>

  ![Vamp UI - voorwaarde van toepassing op gateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="63c3d-236">Ten slotte het gewicht van de gateway voor het verzenden van alle resterende verkeer (alle gebruikers voor niet-Firefox) naar de nieuwe sava: 1.1.0 aanpassen.</span><span class="sxs-lookup"><span data-stu-id="63c3d-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span></span> <span data-ttu-id="63c3d-237">Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) naast **gewicht** en stel de gewichtsdistributie zodat 100% is omgeleid naar de sava/sava_cluster/sava:1.1.0/webport route.</span><span class="sxs-lookup"><span data-stu-id="63c3d-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="63c3d-238">Al het verkeer niet door de voorwaarde worden gefilterd nu doorgestuurd naar de nieuwe sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="63c3d-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span></span>

6. <span data-ttu-id="63c3d-239">Het filter in te grijpen bekijken, opent u twee verschillende browsers (één Firefox en een andere browser) en toegang tot de service sava van beide.</span><span class="sxs-lookup"><span data-stu-id="63c3d-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span></span> <span data-ttu-id="63c3d-240">Alle Firefox aanvragen worden verzonden naar sava: 1.0.0, terwijl alle andere browsers worden doorgestuurd naar sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="63c3d-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span></span>

  ![UI - filter verkeer vamp](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="63c3d-242">Berekening van het</span><span class="sxs-lookup"><span data-stu-id="63c3d-242">Summing up</span></span>

<span data-ttu-id="63c3d-243">Dit artikel is een korte inleiding in Vamp op een DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="63c3d-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span></span> <span data-ttu-id="63c3d-244">Om te beginnen u Vamp up verkregen en uitgevoerd op uw Azure Container Service DC/OS-cluster, een service met een blauwdruk Vamp geïmplementeerd en het heeft geopend op de blootgestelde eindpunt (gateway).</span><span class="sxs-lookup"><span data-stu-id="63c3d-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span></span>

<span data-ttu-id="63c3d-245">We ook op sommige andere van krachtige functies van Vamp aangeraakt: samenvoegen van een nieuwe service-variant aan de actieve implementatie en filteren van verkeer om op te lossen een bekend incompatibiliteitsprobleem incrementeel introduceren.</span><span class="sxs-lookup"><span data-stu-id="63c3d-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="63c3d-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63c3d-246">Next steps</span></span>

* <span data-ttu-id="63c3d-247">Meer informatie over het beheren van Vamp acties via de [Vamp REST-API](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="63c3d-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="63c3d-248">Vamp automatiseringsscripts in Node.js bouwen en uitvoeren als [Vamp werkstromen](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="63c3d-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="63c3d-249">Zie aanvullende [VAMP zelfstudies](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="63c3d-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

