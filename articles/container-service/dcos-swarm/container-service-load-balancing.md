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
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Load balance containers in een Azure Container Service DC/OS-cluster
In dit artikel wordt besproken hoe toocreate een interne load balancer in een DC/OS beheerd Azure Container Service met behulp van Marathon-Taakverdeling. Deze configuratie kunt u tooscale uw toepassingen horizontaal. U kunt er ook tootake profiteren van Hallo openbare en persoonlijke agent clusters door het plaatsen van uw netwerktaakverdelers op Hallo openbare als uw toepassingscontainers op Hallo persoonlijke cluster. In deze zelfstudie hebt u:

> [!div class="checklist"]
> * Een Load Balancer van Marathon configureren
> * Implementeer een toepassing met Hallo load balancer
> * Configureren en de Azure load balancer

U moet een ACS DC/OS cluster toocomplete Hallo in deze zelfstudie stappen. Indien nodig, [dit voorbeeldscript](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) kunt maken voor u.

Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Overzicht van netwerktaakverdeling

Er zijn twee lagen voor taakverdeling in een Azure Container Service DC/OS-cluster: 

**Azure Load Balancer** biedt openbare invoerpunten (hello toepassingsgroepen dat eindgebruikers toegang). Een Azure LB automatisch wordt geleverd met Azure Container Service en is standaard geconfigureerd tooexpose poort 80 en 443 van 8080.

**Hallo Marathon-taakverdeling (marathon-taakverdeling)** routes inkomende aanvragen toocontainer instanties die deze aanvragen. Hallo marathon-taakverdeling wordt dynamisch aangepast geschaald Hallo containers bieden onze webservice. Deze load balancer is niet opgegeven in uw Containerservice standaard, maar het is gemakkelijk tooinstall.

## <a name="configure-marathon-load-balancer"></a>Marathon-taakverdeling configureren

Marathon-taakverdeling opnieuw dynamisch geconfigureerd op basis van de Hallo-containers die u hebt geïmplementeerd. Het is ook robuuste toohello verlies van een container of agent - als dit het geval is, Apache Mesos elders Hallo container opnieuw is opgestart en marathon-taakverdeling past zich.

Hallo opdracht tooinstall Hallo marathon-taakverdeling te volgen op Hallo openbare agent cluster worden uitgevoerd.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Taakverdeling toepassing implementeren

Nu dat we Hallo marathon-taakverdeling pakket hebben, kunnen we een toepassingscontainer dat we tooload saldo wilt implementeren. 

Eerst ophalen Hallo FQDN-naam van de agents Hallo openbaar beschikbaar gesteld.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Maak vervolgens een bestand met de naam *hello web.json* en de kopie in Hallo de volgende inhoud. Hallo `HAPROXY_0_VHOST` label moet toobe bijgewerkt met de FQDN-naam van de DC/OS-agents Hallo Hallo. 

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

Hallo DC/OS CLI toorun Hallo toepassing gebruiken. Standaard implementeert Marathon Hallo Hallo toepassing toohello persoonlijke cluster. Dit betekent dat Hallo hierboven implementatie is alleen toegankelijk via de load balancer, meestal Hallo gewenst gedrag.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Zodra het Hallo-toepassing is geïmplementeerd, blader toohello FQDN-naam van Hallo agent cluster tooview taakverdeling toepassing.

![Afbeelding van taakverdeling toepassing](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Azure Load Balancer configureren

Standaard stelt de Azure Load Balancer poorten 80, 8080 en 443 open. Als u een van deze drie poorten (zoals in Hallo bovenstaande voorbeeld) en er is niets moet u toodo op. U kunt toohit moet de agent load balancer FQDN en telkens wanneer u vernieuwt u een van de drie webservers op een wijze round robin hebt bereikt. 

Als u een andere poort gebruikt, moet u een round-robin tooadd regel en een test op Hallo load balancer voor Hallo-poort die u gebruikt. U kunt dit doen vanuit Hallo [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), met Hallo opdrachten `azure network lb rule create` en `azure network lb probe create`.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd over taakverdeling in ACS met zowel Hallo Marathon en Azure load balancers met inbegrip van Hallo van de volgende activiteiten:

> [!div class="checklist"]
> * Een Load Balancer van Marathon configureren
> * Implementeer een toepassing met Hallo load balancer
> * Configureren en de Azure load balancer

Ga toohello volgende zelfstudie toolearn over de integratie van Azure-opslag met DC/OS in Azure.

> [!div class="nextstepaction"]
> [De bestandsshare koppelen Azure in DC/OS-cluster](container-service-dcos-fileshare.md)