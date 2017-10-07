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
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Een Azure Container Service-cluster met ELK bewaken
In dit artikel wordt gedemonstreerd hoe toodeploy Hallo ELK (Elasticsearch, Logstash, Kibana) stack is op een DC/OS-cluster in Azure Container Service. 

## <a name="prerequisites"></a>Vereisten
[Implementeer](container-service-deployment.md) en [verbinding](../container-service-connect.md) een DC/OS-cluster dat is geconfigureerd met Azure Container Service. Dashboard voor Hallo DC/OS en Marathon services verkennen [hier](container-service-mesos-marathon-ui.md). Installeer ook Hallo [Marathon-taakverdeling](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
ELK stack is een combinatie van Elasticsearch, Logstash, en Kibana waarmee een end tooend stack die kan worden gebruikt toomonitor en analyseren van Logboeken in uw cluster.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Hallo ELK stack configureren op een DC/OS-cluster
Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/) eenmaal in de DC/OS-Webgebruikersinterface te navigeren Hallo**Universe**. Zoek en installeer Elasticsearch Logstash en Kibana van DC/OS Universe hello en in die specifieke volgorde. Voor meer informatie over de configuratie van wanneer u toohello gaat **installatie in de geavanceerde** koppeling.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Eenmaal Hallo ELK containers en zijn zetten, moet u tooenable Kibana toobe toegankelijk via Marathon-Taakverdeling. Navigeer te **Services** > **kibana**, en klik op **bewerken** zoals hieronder wordt weergegeven.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Te schakelen**JSON-modus** en schuif omlaag toohello labels sectie.
U moet tooadd een `"HAPROXY_GROUP": "external"` vermelding hier zoals hieronder.
Nadat u op **wijzigingen implementeren**, de container wordt opnieuw opgestart.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Als u wilt dat tooverify die Kibana is geregistreerd als een service in Hallo HAPROXY dashboard, moet u tooopen poort 9090 op Hallo agent cluster als HAPROXY wordt uitgevoerd op poort 9090.
Standaard we openen van poorten 80, 8080 en 443 in Hallo DC/OS-agent-cluster.
Instructies tooopen een poort en geef openbare beoordelen vindt [hier](container-service-enable-public-access.md).

tooaccess HAPROXY dashboard, open Hallo Marathon-Taakverdeling-beheerinterface op Hallo: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Zodra u toohello URL navigeert, ziet u Hallo HAPROXY dashboard zoals hieronder wordt weergegeven en ziet u een servicevermelding voor Kibana.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


tooaccess hello Kibana dashboard, dat is geïmplementeerd op poort 5601, moet u poort tooopen 5601. Volg de instructies [hier](container-service-enable-public-access.md). Open vervolgens Hallo Kibana-dashboard: `http://localhost:5601`.

## <a name="next-steps"></a>Volgende stappen

* Voor systeem- en logboekbestanden doorsturen en instellingen, Zie [Log-beheer in DC/OS met ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).

* toofilter Logboeken, Zie [Logboeken filteren met ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

