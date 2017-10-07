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
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Load balance containers in een cluster Kubernetes in Azure Container Service 
Dit artikel bevat taakverdeling in een cluster Kubernetes in Azure Container Service. Taakverdeling biedt een extern toegankelijke IP-adres voor het Hallo-service en distribueert netwerkverkeer tussen Hallo gehele product in VM-agent wordt uitgevoerd.

U kunt instellen van een service Kubernetes toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage externe netwerk (TCP)-verkeer. Aanvullende configuratie zijn load balancing en routering van HTTP of HTTPS-verkeer of meer geavanceerde scenario's mogelijk.

## <a name="prerequisites"></a>Vereisten
* [Implementeren van een cluster Kubernetes](container-service-kubernetes-walkthrough.md) in Azure Container Service
* [Verbinding maken met uw client](../container-service-connect.md) tooyour cluster

## <a name="azure-load-balancer"></a>Azure load balancer

Een cluster Kubernetes is geïmplementeerd in Azure Container Service bevat standaard een internetgerichte Azure load balancer voor virtuele machines Hallo-agent. (Een afzonderlijke load balancer-bron is geconfigureerd voor Hallo master VM's). Azure load balancer is een laag 4 load balancer. Hallo load balancer ondersteunt momenteel alleen TCP-verkeer in Kubernetes.

Wanneer u een service Kubernetes maakt, kunt u automatisch hello Azure load balancer tooallow access toohello-service configureren. tooconfigure hello load balancer set Hallo service `type` te`LoadBalancer`. Hallo load balancer maakt een regel toomap een openbaar IP-adres en poortnummer van de binnenkomende verkeer toohello persoonlijke IP-adressen en poortnummers van Hallo gehele product in agent virtuele machines (en omgekeerd voor verkeer van antwoord). 

 Hieronder vindt u twee voorbeelden ziet u hoe tooset Kubernetes service Hallo `type` te`LoadBalancer`. (Na het Hallo-voorbeelden Hallo implementaties verwijderd als u deze niet meer nodig.)

### <a name="example-use-hello-kubectl-expose-command"></a>Voorbeeld: Gebruik Hallo `kubectl expose` opdracht 
Hallo [Kubernetes scenario](container-service-kubernetes-walkthrough.md) bevat een voorbeeld van hoe u een service met Hallo tooexpose `kubectl expose` opdracht en de bijbehorende `--type=LoadBalancer` vlag. Hier volgen Hallo stappen:

1. Start een nieuwe implementatie van de container. Bijvoorbeeld, Hallo opdracht start een nieuwe implementatie aangeroepen na `mynginx`. Hallo-implementatie bestaat uit drie containers op basis van Hallo Docker-afbeelding voor Hallo Nginx-webserver.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Controleer of de Hallo containers worden uitgevoerd. Bijvoorbeeld, als u een query voor Hallo containers met `kubectl get pods`, ziet u uitvoer vergelijkbare toohello volgende:

    ![Ophalen van Nginx-containers](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure hello load balancer tooaccept externe verkeer toohello implementatie uitvoeren `kubectl expose` met `--type=LoadBalancer`. Hallo beschrijft volgende opdracht Hallo Nginx-server op poort 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Type `kubectl get svc` toosee Hallo status van Hallo-services in Hallo-cluster. Tijdens het Hallo load balancer Hallo regel configureert, Hallo `EXTERNAL-IP` Hallo service wordt weergegeven als `<pending>`. Na een paar minuten is Hallo externe IP-adres geconfigureerd: 

    ![Azure load balancer configureren](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Controleer of u toegang hebt tot Hallo-service op Hallo externe IP-adres. Open bijvoorbeeld een web browser toohello IP-adres weergegeven. Hallo browser bevat Hallo Nginx-webserver uitgevoerd in een van de containers Hallo. Of Voer Hallo `curl` of `wget` opdracht. Bijvoorbeeld:

    ```
    curl 13.82.93.130
    ```

    Dit is het geval als de uitvoer er ongeveer zo uitziet:

    ![Toegang Nginx met curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. toosee hello configuratie van hello Azure load balancer, Ga toohello [Azure-portal](https://portal.azure.com).

7. Zoeken naar Hallo resourcegroep voor de container service-cluster en selecteer Hallo load balancer voor Hallo agent virtuele machines. De naam moet hetzelfde zijn als de containerservice Hallo Hallo. (Niet Hallo load balancer voor de hoofdknooppunten Hallo kiezen, een waarvan de naam bevat Hallo **master lb**.) 

    ![De load balancer in de resourcegroep](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. toosee hello details van Hallo load balancer-configuratie, klikt u op **Taakverdelingsregels** en Hallo-naam van het Hallo-regel die is geconfigureerd.

    ![Load balancer-regels](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Voorbeeld: Geef `type: LoadBalancer` in Hallo serviceconfiguratiebestand

Als u een app Kubernetes container uit een YAML of JSON implementeren [serviceconfiguratiebestand](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), een externe load balancer opgeven door Hallo na de specificatie van de service toohello regel toe te voegen:

```YAML
 "type": "LoadBalancer"
``` 



Hallo volgende stappen gebruikt Hallo Kubernetes [gastenboek voorbeeld](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). In dit voorbeeld is een meerlaagse-web-app op basis van Redis- en PHP Docker-installatiekopieën. U kunt opgeven in het serviceconfiguratiebestand Hallo dat Hallo frontend PHP server hello Azure load balancer wordt gebruikt.

1. Hallo-bestand downloaden `guestbook-all-in-one.yaml` van [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Bladeren naar Hallo `spec` voor Hallo `frontend` service.
3. Opmerking verwijderen Hallo regel `type: LoadBalancer`.

    ![De load balancer in de serviceconfiguratie](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Hallo-bestand opslaan en Hallo-app implementeren door het uitvoeren van de volgende opdracht Hallo:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Type `kubectl get svc` toosee Hallo status van Hallo-services in Hallo-cluster. Tijdens het Hallo load balancer Hallo regel configureert, Hallo `EXTERNAL-IP` Hallo `frontend` service wordt weergegeven als `<pending>`. Na een paar minuten is Hallo externe IP-adres geconfigureerd: 

    ![Azure load balancer configureren](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Controleer of u toegang hebt tot Hallo-service op Hallo externe IP-adres. U kunt bijvoorbeeld een web browser toohello externe IP-adres van Hallo-service openen.

    ![Extern toegang gastenboek](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    U kunt gastenboek vermeldingen toevoegen.

7. toosee hello configuratie van hello Azure load balancer, blader naar Hallo load balancerresource voor Hallo-cluster in Hallo [Azure-portal](https://portal.azure.com). Zie Hallo stappen in het vorige voorbeeld Hallo.

### <a name="considerations"></a>Overwegingen

* Maken van een regel voor load balancer Hallo verloopt asynchroon en informatie over Hallo ingericht balancer is gepubliceerd in Hallo-service `status.loadBalancer` veld.
* Elke service wordt automatisch toegewezen aan een eigen virtuele IP-adres in Hallo load balancer.
* Als u tooreach Hallo load balancer met een DNS-naam wilt, werken met uw toocreate domein serviceprovider een DNS-naam van regel Hallo IP-adres.

## <a name="http-or-https-traffic"></a>HTTP of HTTPS-verkeer

tooload saldo HTTP of HTTPS-verkeer toocontainer web-apps en beheren van certificaten voor transport layer security (TLS), kunt u Hallo Kubernetes [inkomend](https://kubernetes.io/docs/user-guide/ingress/) resource. Een inkomend is een verzameling regels waarmee binnenkomende verbindingen tooreach Hallo-clusterservices. Voor een inkomend resource-toowork hello Kubernetes cluster moet beschikken over een [inkomend controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) uitgevoerd.

Azure Container Service een domeincontroller inkomend Kubernetes niet automatisch geïmplementeerd. Implementaties met meerdere domeincontrollers zijn beschikbaar. Op dit moment Hallo [Nginx inkomend controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) tooconfigure inkomend regels en taakverdeling HTTP en HTTPS-verkeer wordt aanbevolen. 

Zie voor meer informatie, Hallo [Nginx inkomend controller documentatie](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Wanneer u Hallo Nginx inkomend controller in Azure Container Service, moet het Hallo domeincontrollers implementeren als een service met zichtbaar `type: LoadBalancer`. Hiermee configureert u hello Azure load balancer tooroute verkeer toohello controller. Zie de vorige sectie Hallo voor meer informatie.


## <a name="next-steps"></a>Volgende stappen

* Zie Hallo [Kubernetes LoadBalancer-documentatie](https://kubernetes.io/docs/user-guide/load-balancer/)
* Meer informatie over [Kubernetes Ingress- en Uitgangsclaims domeincontrollers](https://kubernetes.io/docs/user-guide/ingress/)
* Zie [Kubernetes-voorbeelden](https://github.com/kubernetes/kubernetes/tree/master/examples)

