---
title: aaaLoad saldo Kubernetes containers in Azure | Microsoft Docs
description: Extern verbinding te maken en verdelen over meerdere containers in een cluster Kubernetes in Azure Container Service.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes containers, Micro-services, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="f1d5a-104">Load balance containers in een cluster Kubernetes in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f1d5a-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="f1d5a-105">Dit artikel bevat taakverdeling in een cluster Kubernetes in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="f1d5a-106">Taakverdeling biedt een extern toegankelijke IP-adres voor het Hallo-service en distribueert netwerkverkeer tussen Hallo gehele product in VM-agent wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="f1d5a-107">U kunt instellen van een service Kubernetes toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage externe netwerk (TCP)-verkeer.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="f1d5a-108">Aanvullende configuratie zijn load balancing en routering van HTTP of HTTPS-verkeer of meer geavanceerde scenario's mogelijk.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1d5a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f1d5a-109">Prerequisites</span></span>
* <span data-ttu-id="f1d5a-110">[Implementeren van een cluster Kubernetes](container-service-kubernetes-walkthrough.md) in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f1d5a-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="f1d5a-111">[Verbinding maken met uw client](../container-service-connect.md) tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="f1d5a-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="f1d5a-112">Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="f1d5a-112">Azure load balancer</span></span>

<span data-ttu-id="f1d5a-113">Een cluster Kubernetes is geïmplementeerd in Azure Container Service bevat standaard een internetgerichte Azure load balancer voor virtuele machines Hallo-agent.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="f1d5a-114">(Een afzonderlijke load balancer-bron is geconfigureerd voor Hallo master VM's). Azure load balancer is een laag 4 load balancer.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="f1d5a-115">Hallo load balancer ondersteunt momenteel alleen TCP-verkeer in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="f1d5a-116">Wanneer u een service Kubernetes maakt, kunt u automatisch hello Azure load balancer tooallow access toohello-service configureren.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="f1d5a-117">tooconfigure hello load balancer set Hallo service `type` te`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="f1d5a-118">Hallo load balancer maakt een regel toomap een openbaar IP-adres en poortnummer van de binnenkomende verkeer toohello persoonlijke IP-adressen en poortnummers van Hallo gehele product in agent virtuele machines (en omgekeerd voor verkeer van antwoord).</span><span class="sxs-lookup"><span data-stu-id="f1d5a-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="f1d5a-119">Hieronder vindt u twee voorbeelden ziet u hoe tooset Kubernetes service Hallo `type` te`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="f1d5a-120">(Na het Hallo-voorbeelden Hallo implementaties verwijderd als u deze niet meer nodig.)</span><span class="sxs-lookup"><span data-stu-id="f1d5a-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="f1d5a-121">Voorbeeld: Gebruik Hallo `kubectl expose` opdracht</span><span class="sxs-lookup"><span data-stu-id="f1d5a-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="f1d5a-122">Hallo [Kubernetes scenario](container-service-kubernetes-walkthrough.md) bevat een voorbeeld van hoe u een service met Hallo tooexpose `kubectl expose` opdracht en de bijbehorende `--type=LoadBalancer` vlag.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="f1d5a-123">Hier volgen Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-123">Here are hello steps :</span></span>

1. <span data-ttu-id="f1d5a-124">Start een nieuwe implementatie van de container.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-124">Start a new container deployment.</span></span> <span data-ttu-id="f1d5a-125">Bijvoorbeeld, Hallo opdracht start een nieuwe implementatie aangeroepen na `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="f1d5a-126">Hallo-implementatie bestaat uit drie containers op basis van Hallo Docker-afbeelding voor Hallo Nginx-webserver.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="f1d5a-127">Controleer of de Hallo containers worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-127">Verify that hello containers are running.</span></span> <span data-ttu-id="f1d5a-128">Bijvoorbeeld, als u een query voor Hallo containers met `kubectl get pods`, ziet u uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Ophalen van Nginx-containers](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="f1d5a-130">tooconfigure hello load balancer tooaccept externe verkeer toohello implementatie uitvoeren `kubectl expose` met `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="f1d5a-131">Hallo beschrijft volgende opdracht Hallo Nginx-server op poort 80:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="f1d5a-132">Type `kubectl get svc` toosee Hallo status van Hallo-services in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="f1d5a-133">Tijdens het Hallo load balancer Hallo regel configureert, Hallo `EXTERNAL-IP` Hallo service wordt weergegeven als `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="f1d5a-134">Na een paar minuten is Hallo externe IP-adres geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Azure load balancer configureren](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="f1d5a-136">Controleer of u toegang hebt tot Hallo-service op Hallo externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="f1d5a-137">Open bijvoorbeeld een web browser toohello IP-adres weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="f1d5a-138">Hallo browser bevat Hallo Nginx-webserver uitgevoerd in een van de containers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="f1d5a-139">Of Voer Hallo `curl` of `wget` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="f1d5a-140">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="f1d5a-141">Dit is het geval als de uitvoer er ongeveer zo uitziet:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-141">You should see output similar to:</span></span>

    ![Toegang Nginx met curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="f1d5a-143">toosee hello configuratie van hello Azure load balancer, Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1d5a-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="f1d5a-144">Zoeken naar Hallo resourcegroep voor de container service-cluster en selecteer Hallo load balancer voor Hallo agent virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="f1d5a-145">De naam moet hetzelfde zijn als de containerservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="f1d5a-146">(Niet Hallo load balancer voor de hoofdknooppunten Hallo kiezen, een waarvan de naam bevat Hallo **master lb**.)</span><span class="sxs-lookup"><span data-stu-id="f1d5a-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![De load balancer in de resourcegroep](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="f1d5a-148">toosee hello details van Hallo load balancer-configuratie, klikt u op **Taakverdelingsregels** en Hallo-naam van het Hallo-regel die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Load balancer-regels](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="f1d5a-150">Voorbeeld: Geef `type: LoadBalancer` in Hallo serviceconfiguratiebestand</span><span class="sxs-lookup"><span data-stu-id="f1d5a-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="f1d5a-151">Als u een app Kubernetes container uit een YAML of JSON implementeren [serviceconfiguratiebestand](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), een externe load balancer opgeven door Hallo na de specificatie van de service toohello regel toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="f1d5a-152">Hallo volgende stappen gebruikt Hallo Kubernetes [gastenboek voorbeeld](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="f1d5a-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="f1d5a-153">In dit voorbeeld is een meerlaagse-web-app op basis van Redis- en PHP Docker-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="f1d5a-154">U kunt opgeven in het serviceconfiguratiebestand Hallo dat Hallo frontend PHP server hello Azure load balancer wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="f1d5a-155">Hallo-bestand downloaden `guestbook-all-in-one.yaml` van [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="f1d5a-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="f1d5a-156">Bladeren naar Hallo `spec` voor Hallo `frontend` service.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="f1d5a-157">Opmerking verwijderen Hallo regel `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![De load balancer in de serviceconfiguratie](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="f1d5a-159">Hallo-bestand opslaan en Hallo-app implementeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="f1d5a-160">Type `kubectl get svc` toosee Hallo status van Hallo-services in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="f1d5a-161">Tijdens het Hallo load balancer Hallo regel configureert, Hallo `EXTERNAL-IP` Hallo `frontend` service wordt weergegeven als `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="f1d5a-162">Na een paar minuten is Hallo externe IP-adres geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="f1d5a-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Azure load balancer configureren](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="f1d5a-164">Controleer of u toegang hebt tot Hallo-service op Hallo externe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="f1d5a-165">U kunt bijvoorbeeld een web browser toohello externe IP-adres van Hallo-service openen.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Extern toegang gastenboek](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="f1d5a-167">U kunt gastenboek vermeldingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="f1d5a-168">toosee hello configuratie van hello Azure load balancer, blader naar Hallo load balancerresource voor Hallo-cluster in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1d5a-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f1d5a-169">Zie Hallo stappen in het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="f1d5a-170">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="f1d5a-170">Considerations</span></span>

* <span data-ttu-id="f1d5a-171">Maken van een regel voor load balancer Hallo verloopt asynchroon en informatie over Hallo ingericht balancer is gepubliceerd in Hallo-service `status.loadBalancer` veld.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="f1d5a-172">Elke service wordt automatisch toegewezen aan een eigen virtuele IP-adres in Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="f1d5a-173">Als u tooreach Hallo load balancer met een DNS-naam wilt, werken met uw toocreate domein serviceprovider een DNS-naam van regel Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="f1d5a-174">HTTP of HTTPS-verkeer</span><span class="sxs-lookup"><span data-stu-id="f1d5a-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="f1d5a-175">tooload saldo HTTP of HTTPS-verkeer toocontainer web-apps en beheren van certificaten voor transport layer security (TLS), kunt u Hallo Kubernetes [inkomend](https://kubernetes.io/docs/user-guide/ingress/) resource.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="f1d5a-176">Een inkomend is een verzameling regels waarmee binnenkomende verbindingen tooreach Hallo-clusterservices.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="f1d5a-177">Voor een inkomend resource-toowork hello Kubernetes cluster moet beschikken over een [inkomend controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="f1d5a-178">Azure Container Service een domeincontroller inkomend Kubernetes niet automatisch geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="f1d5a-179">Implementaties met meerdere domeincontrollers zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-179">Several controller implementations are available.</span></span> <span data-ttu-id="f1d5a-180">Op dit moment Hallo [Nginx inkomend controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) tooconfigure inkomend regels en taakverdeling HTTP en HTTPS-verkeer wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="f1d5a-181">Zie voor meer informatie, Hallo [Nginx inkomend controller documentatie](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="f1d5a-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1d5a-182">Wanneer u Hallo Nginx inkomend controller in Azure Container Service, moet het Hallo domeincontrollers implementeren als een service met zichtbaar `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="f1d5a-183">Hiermee configureert u hello Azure load balancer tooroute verkeer toohello controller.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="f1d5a-184">Zie de vorige sectie Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f1d5a-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f1d5a-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1d5a-185">Next steps</span></span>

* <span data-ttu-id="f1d5a-186">Zie Hallo [Kubernetes LoadBalancer-documentatie](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="f1d5a-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="f1d5a-187">Meer informatie over [Kubernetes Ingress- en Uitgangsclaims domeincontrollers](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="f1d5a-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="f1d5a-188">Zie [Kubernetes-voorbeelden](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="f1d5a-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

