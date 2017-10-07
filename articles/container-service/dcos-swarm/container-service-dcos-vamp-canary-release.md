---
title: aaaCanary release met Vamp op Azure DC/OS-cluster | Microsoft Docs
description: Hoe toouse Vamp toocanary release services en slimme verkeer filteren op een Azure Container Service DC/OS-cluster toe te passen
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
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="c16b6-103">Kokospalm release microservices met Vamp in een Azure Container Service DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="c16b6-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="c16b6-104">In dit scenario stelt Vamp op Azure Container Service met een DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="c16b6-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="c16b6-105">We kokospalm hello Vamp demoservice 'sava' release en vervolgens incompatibiliteit van Hallo-service met Firefox oplossen door toe te passen smart verkeer gefilterd.</span><span class="sxs-lookup"><span data-stu-id="c16b6-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="c16b6-106">In dit overzicht Vamp wordt uitgevoerd op een DC/OS-cluster, maar u kunt ook Vamp met Kubernetes gebruiken als Hallo orchestrator.</span><span class="sxs-lookup"><span data-stu-id="c16b6-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="c16b6-107">Over Canarische vrijgegeven en Vamp</span><span class="sxs-lookup"><span data-stu-id="c16b6-107">About canary releases and Vamp</span></span>


<span data-ttu-id="c16b6-108">[Vrijgeven van kokospalm](https://martinfowler.com/bliki/CanaryRelease.html) is een strategie voor slimme implementatie door innovatieve organisaties zoals Netflix, Facebook en Spotify vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="c16b6-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="c16b6-109">Het is een benadering die logisch, klinkt omdat deze problemen vermindert veiligheid netten introduceert en verhoogt de vernieuwing.</span><span class="sxs-lookup"><span data-stu-id="c16b6-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="c16b6-110">Waarom worden niet alle bedrijven met behulp van deze?</span><span class="sxs-lookup"><span data-stu-id="c16b6-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="c16b6-111">Uitbreiden van een pijplijn CI/CD tooinclude kokospalm strategieën voegt complexiteit en uitgebreide devops kennis en ervaring vereist.</span><span class="sxs-lookup"><span data-stu-id="c16b6-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="c16b6-112">Dat is voldoende tooblock kleinere bedrijfs- en ondernemingsbeheer zowel voordat ze ook aan de slag.</span><span class="sxs-lookup"><span data-stu-id="c16b6-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="c16b6-113">[Vamp](http://vamp.io/) een open source-systeem tooease deze overgang is en kokospalm geven functies tooyour voorkeur container scheduler te brengen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="c16b6-114">De vamp kokospalm functionaliteit zich verder uitstrekt dan implementaties op basis van een percentage.</span><span class="sxs-lookup"><span data-stu-id="c16b6-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="c16b6-115">Verkeer kan worden gefilterd en splitst bij een breed scala aan de voorwaarden, bijvoorbeeld tootarget specifieke gebruikers, IP-adresbereiken of apparaten.</span><span class="sxs-lookup"><span data-stu-id="c16b6-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="c16b6-116">Vamp houdt en maatstaven voor prestaties, zodat voor automatisering op basis van echte gegevens analyseert.</span><span class="sxs-lookup"><span data-stu-id="c16b6-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="c16b6-117">U kunt instellen op automatisch herstel op fouten of afzonderlijke service varianten op basis van load of latentie schalen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="c16b6-118">Azure Container Service met DC/OS instellen</span><span class="sxs-lookup"><span data-stu-id="c16b6-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="c16b6-119">[Een DC/OS-cluster implementeren](container-service-deployment.md) met één master en twee agents van standaardgrootte.</span><span class="sxs-lookup"><span data-stu-id="c16b6-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="c16b6-120">[Maken van een SSH-tunnel](../container-service-connect.md) tooconnect toohello DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="c16b6-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="c16b6-121">In dit artikel wordt ervan uitgegaan dat u een tunnel toohello cluster op de lokale poort 80.</span><span class="sxs-lookup"><span data-stu-id="c16b6-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="c16b6-122">Vamp instellen</span><span class="sxs-lookup"><span data-stu-id="c16b6-122">Set up Vamp</span></span>

<span data-ttu-id="c16b6-123">Nu dat u een actieve DC/OS-cluster hebt, kunt u Vamp installeren vanaf Hallo DC/OS-Webgebruikersinterface (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="c16b6-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![DC/OS-webgebruikersinterface](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="c16b6-125">De installatie wordt uitgevoerd in twee fasen:</span><span class="sxs-lookup"><span data-stu-id="c16b6-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="c16b6-126">**Implementeer Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="c16b6-127">Vervolgens **Vamp implementeren** door Hallo Vamp DC/OS universe pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="c16b6-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="c16b6-128">Elasticsearch implementeren</span><span class="sxs-lookup"><span data-stu-id="c16b6-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="c16b6-129">Elasticsearch vereist vamp voor het verzamelen van de metrische gegevens en aggregatie.</span><span class="sxs-lookup"><span data-stu-id="c16b6-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="c16b6-130">U kunt Hallo [magneticio Docker installatiekopieën](https://hub.docker.com/r/magneticio/elastic/) toodeploy een compatibel Vamp Elasticsearch-stack.</span><span class="sxs-lookup"><span data-stu-id="c16b6-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="c16b6-131">Ga te in Hallo DC/OS-Webgebruikersinterface,**Services** en klik op **Service implementeren**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="c16b6-132">Selecteer **JSON-modus** van Hallo **nieuwe Service implementeren** pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="c16b6-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Selecteer JSON-modus](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="c16b6-134">In de volgende JSON hello te plakken.</span><span class="sxs-lookup"><span data-stu-id="c16b6-134">Paste in hello following JSON.</span></span> <span data-ttu-id="c16b6-135">Deze configuratie wordt uitgevoerd Hallo-container met 1 GB RAM-geheugen en een eenvoudige statuscontrole op Hallo Elasticsearch poort.</span><span class="sxs-lookup"><span data-stu-id="c16b6-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
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
  

3. <span data-ttu-id="c16b6-136">Klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-136">Click **Deploy**.</span></span>

  <span data-ttu-id="c16b6-137">DC/OS implementeert Hallo Elasticsearch container.</span><span class="sxs-lookup"><span data-stu-id="c16b6-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="c16b6-138">U kunt de voortgang volgen op Hallo **Services** pagina.</span><span class="sxs-lookup"><span data-stu-id="c16b6-138">You can track progress on hello **Services** page.</span></span>  

  ![e implementeren? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="c16b6-140">Vamp implementeren</span><span class="sxs-lookup"><span data-stu-id="c16b6-140">Deploy Vamp</span></span>

<span data-ttu-id="c16b6-141">Zodra Elasticsearch als rapporteert **met**, kunt u Hallo Vamp DC/OS Universe pakket toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="c16b6-142">Ga te**Universe** en zoek naar **vamp**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="c16b6-143">![Vamp op DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="c16b6-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="c16b6-144">Klik op **installeren** volgende toohello vamp pakket en kies **installatie in de geavanceerde**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="c16b6-145">Schuif naar beneden en Voer Hallo elasticsearch-url te volgen: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="c16b6-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Voer de URL Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="c16b6-147">Klik op **Bekijk en installeer**, klikt u vervolgens op **installeren** toostart Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c16b6-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="c16b6-148">DC/OS implementeert alle vereiste Vamp onderdelen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="c16b6-149">U kunt de voortgang volgen op Hallo **Services** pagina.</span><span class="sxs-lookup"><span data-stu-id="c16b6-149">You can track progress on hello **Services** page.</span></span>
  
  ![Vamp als universe pakket implementeren](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="c16b6-151">Zodra de implementatie is voltooid, kunt u toegang tot Hallo Vamp gebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="c16b6-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![-Service op de DC/OS vamp](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp gebruikersinterface](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="c16b6-154">Uw eerste service implementeren</span><span class="sxs-lookup"><span data-stu-id="c16b6-154">Deploy your first service</span></span>

<span data-ttu-id="c16b6-155">Nu dat Vamp actief en werkend is, een service implementeren vanuit een blauwdruk.</span><span class="sxs-lookup"><span data-stu-id="c16b6-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="c16b6-156">In de meest eenvoudige vorm een [Vamp blauwdruk](http://vamp.io/documentation/using-vamp/blueprints/) Hallo eindpunten (gateways), clusters en services toodeploy beschrijft.</span><span class="sxs-lookup"><span data-stu-id="c16b6-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="c16b6-157">Vamp maakt gebruik van clusters toogroup verschillende varianten van Hallo dezelfde service in logische groepen voor kokospalm vrijgeven of A / B-tests.</span><span class="sxs-lookup"><span data-stu-id="c16b6-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="c16b6-158">Dit scenario wordt gebruikt voor een voorbeeldtoepassing monolithische aangeroepen [ **sava**](https://github.com/magneticio/sava), die is op versie 1.0.</span><span class="sxs-lookup"><span data-stu-id="c16b6-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="c16b6-159">Hallo monoliet wordt verpakt in een Docker-container in Docker-Hub onder de magneticio/sava:1.0.0 ligt.</span><span class="sxs-lookup"><span data-stu-id="c16b6-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="c16b6-160">Hallo-app wordt normaal uitgevoerd op poort 8080, maar u wilt dat tooexpose in 9050 in dit geval poort.</span><span class="sxs-lookup"><span data-stu-id="c16b6-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="c16b6-161">Hallo-app via Vamp met behulp van een eenvoudige blauwdruk implementeren.</span><span class="sxs-lookup"><span data-stu-id="c16b6-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="c16b6-162">Ga te**implementaties**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="c16b6-163">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-163">Click **Add**.</span></span>

3. <span data-ttu-id="c16b6-164">Plakken in de volgende Hallo blauwdruk YAML.</span><span class="sxs-lookup"><span data-stu-id="c16b6-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="c16b6-165">Deze blauwdruk bevat één cluster met slechts één service-variant, die we in een latere stap wijzigen:</span><span class="sxs-lookup"><span data-stu-id="c16b6-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="c16b6-166">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-166">Click **Save**.</span></span> <span data-ttu-id="c16b6-167">Vamp initieert Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c16b6-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="c16b6-168">Hallo-implementatie wordt vermeld op Hallo **implementaties** pagina.</span><span class="sxs-lookup"><span data-stu-id="c16b6-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="c16b6-169">Klik op Hallo implementatie toomonitor de status ervan.</span><span class="sxs-lookup"><span data-stu-id="c16b6-169">Click hello deployment toomonitor its status.</span></span>

![UI - sava implementeren vamp](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![de service Sava in Vamp gebruikersinterface](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="c16b6-172">Twee gateways worden gemaakt, die worden vermeld op Hallo **Gateways** pagina:</span><span class="sxs-lookup"><span data-stu-id="c16b6-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="c16b6-173">een stabiele eindpunt tooaccess Hallo-service (poort 9050) uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="c16b6-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="c16b6-174">een beheerde Vamp interne gateway (meer informatie over deze gateway later).</span><span class="sxs-lookup"><span data-stu-id="c16b6-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![UI - sava gateways vamp](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="c16b6-176">Hallo sava service is nu geïmplementeerd, maar u geen toegang tot deze extern omdat hello Azure Load Balancer tooforward verkeer tooit nog niet weet.</span><span class="sxs-lookup"><span data-stu-id="c16b6-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="c16b6-177">tooaccess hello service update hello Azure netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="c16b6-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="c16b6-178">Werk de configuratie van hello Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="c16b6-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="c16b6-179">Hallo sava service vamp geïmplementeerd op Hallo DC/OS-agent knooppunten, een stabiele eindpunt op poort 9050 blootstellen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="c16b6-180">tooaccess Hallo-service van het buitenste Hallo DC/OS-cluster, moet u Hallo wijzigingen toohello Azure netwerkconfiguratie in uw implementatie van het cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="c16b6-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="c16b6-181">**Hello Azure Load Balancer configureren** voor Hallo-agents (Hallo resource met de naam **dcos-agent-lb-xxxx**) met een health test en een regel tooforward-verkeer op poort 9050 toohello sava exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c16b6-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="c16b6-182">**Update Hallo netwerkbeveiligingsgroep** voor openbare agents hello (Hallo resource met de naam **XXXX-agent-openbare-nsg-XXXX**) tooallow verkeer op poort 9050.</span><span class="sxs-lookup"><span data-stu-id="c16b6-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="c16b6-183">Voor gedetailleerde stappen toocomplete Hallo deze taken met behulp van Azure portal, Zie [openbare toegang tooan Azure Container Service-toepassing inschakelen](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="c16b6-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="c16b6-184">Poort 9050 voor alle poortinstellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="c16b6-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="c16b6-185">Zodra u alles is gemaakt, gaat u toohello **overzicht** blade Hallo DC/OS-agent load balancer (Hallo resource met de naam **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="c16b6-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="c16b6-186">Hallo zoeken **openbaar IP-adres**, en Hallo adres tooaccess sava op poort 9050 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c16b6-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Azure portal - get openbaar IP-adres](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![Sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="c16b6-189">Voer een kokospalm release</span><span class="sxs-lookup"><span data-stu-id="c16b6-189">Run a canary release</span></span>

<span data-ttu-id="c16b6-190">Stel dat u hebt een nieuwe versie van deze toepassing die u wilt dat toocanary release in productie.</span><span class="sxs-lookup"><span data-stu-id="c16b6-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="c16b6-191">U hebt het beperkte als magneticio/sava:1.1.0 en toogo gereed zijn.</span><span class="sxs-lookup"><span data-stu-id="c16b6-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="c16b6-192">Vamp kunt u eenvoudig toevoegen van nieuwe services toohello waarop implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c16b6-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="c16b6-193">Deze 'samengevoegde' services worden geïmplementeerd naast Hallo bestaande services in Hallo-cluster en een gewicht van 0% toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="c16b6-194">Er is geen verkeer is gerouteerde tooa zojuist samengevoegd service totdat u de distributie van verkeer Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="c16b6-195">Hallo gewicht schuifregelaar in Hallo Vamp gebruikersinterface biedt u volledige controle over Hallo distributie, waardoor het incrementele aanpassingen (kokospalm release) of een directe terugdraaien.</span><span class="sxs-lookup"><span data-stu-id="c16b6-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="c16b6-196">Een nieuwe service-variant samenvoegen</span><span class="sxs-lookup"><span data-stu-id="c16b6-196">Merge a new service variant</span></span>

<span data-ttu-id="c16b6-197">toomerge hello nieuwe sava 1.1-service met Hallo waarop implementatie wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="c16b6-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="c16b6-198">Klik in de gebruikersinterface Vamp hello, op **blauwdrukken**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="c16b6-199">Klik op **toevoegen** en plakken in de volgende Hallo blauwdruk YAML: deze blauwdruk wordt een nieuwe service variant (sava: 1.1.0) toodeploy binnen Hallo bestaand cluster (sava_cluster) beschreven.</span><span class="sxs-lookup"><span data-stu-id="c16b6-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="c16b6-200">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-200">Click **Save**.</span></span> <span data-ttu-id="c16b6-201">Hallo blauwdruk wordt opgeslagen en weergegeven op Hallo **blauwdrukken** pagina.</span><span class="sxs-lookup"><span data-stu-id="c16b6-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="c16b6-202">Open Hallo actiemenu op Hallo sava: 1.1 blauwdruk en klikt u op **samenvoegen naar**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![UI - blauwdrukken vamp](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="c16b6-204">Selecteer Hallo **sava** implementatie en klik op **samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp UI - blauwdruk toodeployment samenvoegen](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="c16b6-206">Vamp implementeert Hallo nieuwe sava: 1.1.0 service variant beschreven in Hallo blauwdruk naast sava: 1.0.0 in Hallo **sava_cluster** Hallo waarop implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c16b6-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![UI - bijgewerkte sava implementatie vamp](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="c16b6-208">Hallo **sava_cluster-sava/webport** gateway (Hallo clustereindpunt) wordt ook bijgewerkt, sava: 1.1.0 toevoegen van een route toohello zojuist geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c16b6-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="c16b6-209">Op dit moment geen verkeer wordt gerouteerd hier (Hallo **gewicht** too0% is ingesteld).</span><span class="sxs-lookup"><span data-stu-id="c16b6-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![UI - cluster gateway vamp](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="c16b6-211">Kokospalm release</span><span class="sxs-lookup"><span data-stu-id="c16b6-211">Canary release</span></span>

<span data-ttu-id="c16b6-212">Met beide versies van sava geïmplementeerd in Hallo dezelfde cluster, het Hallo-distributie van verkeer tussen hen door Hallo verplaatsen aanpassen **gewicht** schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="c16b6-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="c16b6-213">Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) volgende te**gewicht**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="c16b6-214">Stel Hallo gewicht distributie too50%/50% en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c16b6-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![UI - gateway gewicht schuifregelaar vamp](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="c16b6-216">Ga terug tooyour browser en vernieuw Hallo sava pagina een paar keer.</span><span class="sxs-lookup"><span data-stu-id="c16b6-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="c16b6-217">Hallo sava toepassing nu schakelt u tussen een sava: 1.0 en een pagina sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="c16b6-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![wisselende sava1.0 en sava1.1 services](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="c16b6-219">Deze alternatieven van Hallo pagina werkt het beste met Hallo 'Incognito' of 'Anoniem'-modus van uw browser vanwege Hallo van statische elementen in de cache.</span><span class="sxs-lookup"><span data-stu-id="c16b6-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="c16b6-220">Filteren van verkeer</span><span class="sxs-lookup"><span data-stu-id="c16b6-220">Filter traffic</span></span>

<span data-ttu-id="c16b6-221">Stel dat na implementatie dat u een incompatibiliteit in sava: 1.1.0 dat oorzaken problemen worden weergegeven in browsers Firefox gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c16b6-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="c16b6-222">U kunt Vamp toofilter binnenkomend verkeer en directe back-alle gebruikers van Firefox toohello stabiele sava: 1.0.0 bekend.</span><span class="sxs-lookup"><span data-stu-id="c16b6-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="c16b6-223">Dit filter verbeterd direct wordt omgezet Hallo onderbreking voor Firefox gebruikers, terwijl alle andere tooenjoy Hallo voordelen van Hallo blijft sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="c16b6-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="c16b6-224">Maakt gebruik van vamp **voorwaarden** toofilter verkeer tussen routes in een gateway.</span><span class="sxs-lookup"><span data-stu-id="c16b6-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="c16b6-225">Het verkeer wordt eerst gefilterd en omgeleid volgens toohello voorwaarden toegepast tooeach route.</span><span class="sxs-lookup"><span data-stu-id="c16b6-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="c16b6-226">Alle resterende verkeer wordt verdeeld volgens toohello gateway gewicht-instelling.</span><span class="sxs-lookup"><span data-stu-id="c16b6-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="c16b6-227">U kunt een voorwaarde toofilter alle Firefox gebruikers maken en hen te instrueren toohello oude sava: 1.0.0:</span><span class="sxs-lookup"><span data-stu-id="c16b6-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="c16b6-228">Op Hallo sava_cluster-sava/webport **Gateways** pagina, klikt u op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd een **voorwaarde** toohello route sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="c16b6-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="c16b6-229">Voer Hallo voorwaarde **gebruikersagent Firefox ==** en klik op ![Vamp UI - opslaan](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="c16b6-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="c16b6-230">Vamp voegt Hallo voorwaarde van een standaard sterkte van 0%.</span><span class="sxs-lookup"><span data-stu-id="c16b6-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="c16b6-231">toostart het filteren van het verkeer, moet u tooadjust Hallo voorwaarde sterkte.</span><span class="sxs-lookup"><span data-stu-id="c16b6-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="c16b6-232">Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **sterkte** toohello voorwaarde wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="c16b6-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="c16b6-233">Set Hallo **sterkte** too100% en klik op ![Vamp UI - opslaan](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="c16b6-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="c16b6-234">Vamp verzendt nu al het verkeer die overeenkomt met de Hallo voorwaarde (alle gebruikers voor de Firefox) toosava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="c16b6-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp UI - voorwaarde toogateway toepassen](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="c16b6-236">Ten slotte aanpassen Hallo gateway gewicht toosend alle resterende verkeer (alle gebruikers voor de niet-Firefox) toohello nieuwe sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="c16b6-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="c16b6-237">Klik op ![Vamp UI - bewerken](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) volgende te**gewicht** en stel de gewichtsverdeling Hallo zodat 100% gerichte toohello route sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="c16b6-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="c16b6-238">Al het verkeer niet gefilterd door het Hallo-voorwaarde is nu gerichte toohello nieuwe sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="c16b6-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="c16b6-239">toosee hello filter in actie, twee verschillende browsers (één Firefox en een andere browser) en openen Hallo sava service van beide.</span><span class="sxs-lookup"><span data-stu-id="c16b6-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="c16b6-240">Alle Firefox aanvragen verzonden toosava:1.0.0, terwijl alle andere browsers gerichte toosava:1.1.0 zijn.</span><span class="sxs-lookup"><span data-stu-id="c16b6-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![UI - filter verkeer vamp](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="c16b6-242">Berekening van het</span><span class="sxs-lookup"><span data-stu-id="c16b6-242">Summing up</span></span>

<span data-ttu-id="c16b6-243">Dit artikel is een korte inleiding tooVamp op een DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="c16b6-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="c16b6-244">Om te beginnen u Vamp up verkregen en uitgevoerd op uw Azure Container Service DC/OS-cluster, een service met een blauwdruk Vamp geïmplementeerd en het heeft geopend op Hallo blootgesteld eindpunt (gateway).</span><span class="sxs-lookup"><span data-stu-id="c16b6-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="c16b6-245">We ook op sommige andere van krachtige functies van Vamp aangeraakt: een nieuwe service variant toohello waarop implementatie wordt uitgevoerd en voor het filteren van verkeer tooresolve een bekend incompatibiliteitsprobleem incrementeel introducing samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="c16b6-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c16b6-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c16b6-246">Next steps</span></span>

* <span data-ttu-id="c16b6-247">Meer informatie over het beheren van Vamp acties via Hallo [Vamp REST-API](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="c16b6-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="c16b6-248">Vamp automatiseringsscripts in Node.js bouwen en uitvoeren als [Vamp werkstromen](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="c16b6-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="c16b6-249">Zie aanvullende [VAMP zelfstudies](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="c16b6-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

