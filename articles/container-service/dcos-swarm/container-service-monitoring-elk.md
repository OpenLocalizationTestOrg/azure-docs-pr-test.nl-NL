---
title: een Azure-DC/OS-cluster - stack van ELK aaaMonitor | Microsoft Docs
description: Bewaken van een DC/OS-cluster in Azure Container Service-cluster met ELK (Elasticsearch, Logstash en Kibana).
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure, bewaking, elk
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="38dee-104">Een Azure Container Service-cluster met ELK bewaken</span><span class="sxs-lookup"><span data-stu-id="38dee-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="38dee-105">In dit artikel wordt gedemonstreerd hoe toodeploy Hallo ELK (Elasticsearch, Logstash, Kibana) stack is op een DC/OS-cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="38dee-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="38dee-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="38dee-106">Prerequisites</span></span>
<span data-ttu-id="38dee-107">[Implementeer](container-service-deployment.md) en [verbinding](../container-service-connect.md) een DC/OS-cluster dat is geconfigureerd met Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="38dee-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="38dee-108">Dashboard voor Hallo DC/OS en Marathon services verkennen [hier](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="38dee-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="38dee-109">Installeer ook Hallo [Marathon-taakverdeling](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="38dee-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="38dee-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="38dee-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="38dee-111">ELK stack is een combinatie van Elasticsearch, Logstash, en Kibana waarmee een end tooend stack die kan worden gebruikt toomonitor en analyseren van Logboeken in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="38dee-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="38dee-112">Hallo ELK stack configureren op een DC/OS-cluster</span><span class="sxs-lookup"><span data-stu-id="38dee-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="38dee-113">Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/) eenmaal in de DC/OS-Webgebruikersinterface te navigeren Hallo**Universe**.</span><span class="sxs-lookup"><span data-stu-id="38dee-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="38dee-114">Zoek en installeer Elasticsearch Logstash en Kibana van DC/OS Universe hello en in die specifieke volgorde.</span><span class="sxs-lookup"><span data-stu-id="38dee-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="38dee-115">Voor meer informatie over de configuratie van wanneer u toohello gaat **installatie in de geavanceerde** koppeling.</span><span class="sxs-lookup"><span data-stu-id="38dee-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="38dee-119">Eenmaal Hallo ELK containers en zijn zetten, moet u tooenable Kibana toobe toegankelijk via Marathon-Taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="38dee-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="38dee-120">Navigeer te **Services** > **kibana**, en klik op **bewerken** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="38dee-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="38dee-122">Te schakelen**JSON-modus** en schuif omlaag toohello labels sectie.</span><span class="sxs-lookup"><span data-stu-id="38dee-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="38dee-123">U moet tooadd een `"HAPROXY_GROUP": "external"` vermelding hier zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="38dee-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="38dee-124">Nadat u op **wijzigingen implementeren**, de container wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="38dee-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="38dee-126">Als u wilt dat tooverify die Kibana is geregistreerd als een service in Hallo HAPROXY dashboard, moet u tooopen poort 9090 op Hallo agent cluster als HAPROXY wordt uitgevoerd op poort 9090.</span><span class="sxs-lookup"><span data-stu-id="38dee-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="38dee-127">Standaard we openen van poorten 80, 8080 en 443 in Hallo DC/OS-agent-cluster.</span><span class="sxs-lookup"><span data-stu-id="38dee-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="38dee-128">Instructies tooopen een poort en geef openbare beoordelen vindt [hier](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="38dee-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="38dee-129">tooaccess HAPROXY dashboard, open Hallo Marathon-Taakverdeling-beheerinterface op Hallo: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="38dee-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="38dee-130">Zodra u toohello URL navigeert, ziet u Hallo HAPROXY dashboard zoals hieronder wordt weergegeven en ziet u een servicevermelding voor Kibana.</span><span class="sxs-lookup"><span data-stu-id="38dee-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="38dee-132">tooaccess hello Kibana dashboard, dat is geïmplementeerd op poort 5601, moet u poort tooopen 5601.</span><span class="sxs-lookup"><span data-stu-id="38dee-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="38dee-133">Volg de instructies [hier](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="38dee-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="38dee-134">Open vervolgens Hallo Kibana-dashboard: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="38dee-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38dee-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38dee-135">Next steps</span></span>

* <span data-ttu-id="38dee-136">Voor systeem- en logboekbestanden doorsturen en instellingen, Zie [Log-beheer in DC/OS met ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="38dee-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="38dee-137">toofilter Logboeken, Zie [Logboeken filteren met ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="38dee-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

