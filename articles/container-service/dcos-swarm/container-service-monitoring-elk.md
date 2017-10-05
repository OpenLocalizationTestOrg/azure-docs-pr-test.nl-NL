---
title: Een Azure-DC/OS-cluster - stack van ELK bewaken | Microsoft Docs
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
ms.openlocfilehash: fcfa277cdd0f3cebc0fbbb23e771fb23ffbe2ca6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="c8b40-104">Een Azure Container Service-cluster met ELK bewaken</span><span class="sxs-lookup"><span data-stu-id="c8b40-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="c8b40-105">In dit artikel ziet u hoe de stack ELK (Elasticsearch, Logstash, Kibana) op een DC/OS-cluster in Azure Container Service implementeren.</span><span class="sxs-lookup"><span data-stu-id="c8b40-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c8b40-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c8b40-106">Prerequisites</span></span>
<span data-ttu-id="c8b40-107">[Implementeer](container-service-deployment.md) en [verbinding](../container-service-connect.md) een DC/OS-cluster dat is geconfigureerd met Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="c8b40-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="c8b40-108">Bekijk het dashboard in DC/OS en Marathon services [hier](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="c8b40-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="c8b40-109">Installeer ook het [Marathon-taakverdeling](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="c8b40-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="c8b40-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="c8b40-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="c8b40-111">ELK stack is een combinatie van Elasticsearch, Logstash en Kibana waarmee een end-to-end-stack die kan worden gebruikt om te controleren en analyseren van Logboeken in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="c8b40-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="c8b40-112">De stack ELK op een DC/OS-cluster configureren</span><span class="sxs-lookup"><span data-stu-id="c8b40-112">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="c8b40-113">Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/) eenmaal in de DC/OS-gebruikersinterface Navigeer naar **Universe**.</span><span class="sxs-lookup"><span data-stu-id="c8b40-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="c8b40-114">Zoek en installeer Elasticsearch Logstash en Kibana uit de DC/OS-Universe en in die specifieke volgorde.</span><span class="sxs-lookup"><span data-stu-id="c8b40-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="c8b40-115">Voor meer informatie over de configuratie van wanneer u naar de **installatie in de geavanceerde** koppeling.</span><span class="sxs-lookup"><span data-stu-id="c8b40-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="c8b40-119">Zodra de containers voor ELK en weet zetten, u Kibana moet toegankelijk via Marathon-Taakverdeling inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c8b40-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="c8b40-120">Navigeer naar **Services** > **kibana**, en klik op **bewerken** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c8b40-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="c8b40-122">Schakelen naar **JSON-modus** en blader naar de sectie labels.</span><span class="sxs-lookup"><span data-stu-id="c8b40-122">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="c8b40-123">U moet toevoegen een `"HAPROXY_GROUP": "external"` vermelding hier zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="c8b40-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="c8b40-124">Nadat u op **wijzigingen implementeren**, de container wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="c8b40-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="c8b40-126">Als u controleren of Kibana is geregistreerd als een service in het dashboard HAPROXY wilt, moet u poort 9090 op het cluster agent openen als HAPROXY wordt uitgevoerd op poort 9090.</span><span class="sxs-lookup"><span data-stu-id="c8b40-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="c8b40-127">Standaard openen we poorten 80, 8080, en 443 in het cluster DC/OS-agent.</span><span class="sxs-lookup"><span data-stu-id="c8b40-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="c8b40-128">Vindt u instructies voor het openen van een poort en bieden openbare beoordelen [hier](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="c8b40-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="c8b40-129">Voor toegang tot het dashboard HAPROXY, opent u de beheerinterface van de Marathon-Taakverdeling op: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="c8b40-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="c8b40-130">Zodra u naar de URL navigeren, ziet u het dashboard HAPROXY zoals hieronder wordt weergegeven en ziet u een servicevermelding voor Kibana.</span><span class="sxs-lookup"><span data-stu-id="c8b40-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="c8b40-132">Voor toegang tot het dashboard Kibana, dat is geïmplementeerd op poort 5601, moet u poort 5601 openen.</span><span class="sxs-lookup"><span data-stu-id="c8b40-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="c8b40-133">Volg de instructies [hier](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="c8b40-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="c8b40-134">Open het dashboard Kibana op: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="c8b40-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8b40-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8b40-135">Next steps</span></span>

* <span data-ttu-id="c8b40-136">Voor systeem- en logboekbestanden doorsturen en instellingen, Zie [Log-beheer in DC/OS met ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="c8b40-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="c8b40-137">Om te filteren van Logboeken, Zie [Logboeken filteren met ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="c8b40-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

