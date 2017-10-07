---
title: aaaEnable access tooAzure DC/OS-container app | Microsoft Docs
description: Hoe tooenable openbare toegang krijgen tot tooDC/OS-containers in Azure Container Service.
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Openbare toegang tooan Azure Container Service-toepassing inschakelen
Elke DC/OS-container in Hallo ACS [openbare agent groep](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatisch blootgestelde toohello internet. Standaard-poorten **80**, **443**, **8080** zijn geopend en luistert op deze poorten (openbare) containers toegankelijk zijn. Dit artikel laat zien hoe tooopen meer poorten voor uw toepassingen in Azure Container Service.

## <a name="open-a-port-portal"></a>Open een poort (portal)
We moeten eerst tooopen Hallo poort die we willen.

1. Meld u bij toohello-portal.
2. Zoeken naar Hallo resourcegroep die u hebt geïmplementeerd hello Azure Container Service.
3. Hallo agent load balancer selecteren (die de naam vergelijkbaar te**XXXX-agent-lb-XXXX**).
   
    ![Azure container service load balancer](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Klik op **Probes** en vervolgens **toevoegen**.
   
    ![Azure container service load balancer-tests](./media/container-service-enable-public-access/add-probe.png)
5. Hallo test formulier invullen en klik op **OK**.
   
   | Veld | Beschrijving |
   | --- | --- |
   | Naam |Een beschrijvende naam van het Hallo-test. |
   | Poort |Hallo-poort van Hallo container tootest. |
   | Pad |(Wanneer in de HTTP-modus) Hallo website relatieve pad tooprobe. HTTPS wordt niet ondersteund. |
   | Interval |Hallo hoeveelheid tijd tussen test probeert, in seconden. |
   | Drempelwaarde voor onjuiste status |Het aantal opeenvolgende test probeert voordat Hallo container niet in orde. |
6. Terug op het Hallo-eigenschappen van Hallo agent load balancer, klikt u op **Taakverdelingsregels** en vervolgens **toevoegen**.
   
    ![Azure container service load balancer-regels](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Hallo load balancer formulier invullen en klik op **OK**.
   
   | Veld | Beschrijving |
   | --- | --- |
   | Naam |Een beschrijvende naam Hallo load balancer. |
   | Poort |Hallo openbare binnenkomende poort. |
   | Back-endpoort |Hallo interne openbare poort van Hallo container tooroute verkeer naar. |
   | Back-endpool |Hallo-containers in deze groep worden Hallo doel voor deze load balancer. |
   | Test |Hallo toodetermine test die wordt gebruikt als een doel in Hallo **back-endpool** in orde is. |
   | Sessiepersistentie |Hiermee wordt bepaald hoe het verkeer van een client voor Hallo duur van Hallo sessie moet worden verwerkt.<br><br>**Geen**: opeenvolgende aanvragen van Hallo dezelfde client door elke container kan worden verwerkt.<br>**Client IP**: opeenvolgende aanvragen van hetzelfde client-IP-worden afgehandeld door Hallo Hallo dezelfde container.<br>**Client IP en -protocol**: opeenvolgende aanvragen van dezelfde combinatie van client en het IP-protocol worden afgehandeld door Hallo Hallo dezelfde container. |
   | Time-out voor inactiviteit |(Alleen TCP) Hallo in minuten, tijd tookeep een TCP/HTTP-client openen zonder afhankelijk te zijn van *keepalive-* berichten. |

## <a name="add-a-security-rule-portal"></a>Toevoegen van een beveiligingsregel (portal)
Vervolgens moet een regel waarmee verkeer van onze poort is geopend via de firewall Hallo tooadd.

1. Meld u bij toohello-portal.
2. Zoeken naar Hallo resourcegroep die u hebt geïmplementeerd hello Azure Container Service.
3. Selecteer Hallo **openbare** netwerkbeveiligingsgroep agent (die de naam vergelijkbaar te**XXXX-agent-openbare-nsg-XXXX**).
   
    ![Azure container service-netwerkbeveiligingsgroep](./media/container-service-enable-public-access/agent-nsg.png)
4. Selecteer **inkomende beveiligingsregels** en vervolgens **toevoegen**.
   
    ![Azure container service netwerkbeveiligingsgroepen](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Hallo firewall regel tooallow vullen met de openbare poort en klik op **OK**.
   
   | Veld | Beschrijving |
   | --- | --- |
   | Naam |Een beschrijvende naam van de firewallregel Hallo. |
   | Prioriteit |De positie van de prioriteit voor Hallo regel. Hallo lagere Hallo nummer Hallo hogere Hallo prioriteit. |
   | Bron |Hallo binnenkomende IP-adresbereik toobe toegestaan of geweigerd door deze regel beperken. Gebruik **eventuele** toonot beperking opgeven. |
   | Service |Selecteer een set vooraf gedefinieerde services is bedoeld voor deze regel. Gebruik anders **aangepaste** toocreate zelf. |
   | Protocol |Op basis van verkeer te beperken **TCP** of **UDP**. Gebruik **eventuele** toonot beperking opgeven. |
   | Poortbereik |Wanneer **Service** is **aangepaste**, bepaalt Hallo bereik van de poorten die door deze regel is van invloed op. U kunt een losse poort zijn, zoals **80**, of een bereik, zoals **1024 1500**. |
   | Actie |Verkeer toestaan of weigeren die voldoen aan de criteria Hallo. |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over het verschil tussen Hallo [openbare en persoonlijke DC/OS-agents](container-service-dcos-agents.md).

Meer informatie lezen over [beheer van uw DC/OS-containers](container-service-mesos-marathon-ui.md).

