---
title: aaaDeploy containers met Helm in Azure Kubernetes | Microsoft Docs
description: Hallo Helm verpakking hulpprogramma toodeploy containers gebruiken op een cluster Kubernetes in Azure Container Service
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Helm toodeploy containers op een cluster Kubernetes gebruiken 

[Helm](https://github.com/kubernetes/helm/) is een open source verpakking hulpprogramma waarmee u kunt installeren en Hallo levenscyclus van Kubernetes toepassingen beheren. Vergelijkbare tooLinux pakket managers zoals Apt get- en Yum Helm is gebruikte toomanage Kubernetes grafieken, pakketten van vooraf geconfigureerde Kubernetes resources zijn. Dit artikel laat zien hoe toowork met Helm op een cluster Kubernetes geïmplementeerd in Azure Container Service.

Helm bestaat uit twee onderdelen: 
* Hallo **Helm CLI** een client die wordt uitgevoerd op uw computer, lokaal of in de cloud Hallo  

* **Helmstok** is een server die wordt uitgevoerd op Hallo Kubernetes cluster en beheert Hallo levenscyclus van uw toepassingen Kubernetes 
 
## <a name="prerequisites"></a>Vereisten

* [Maak een cluster Kubernetes](container-service-kubernetes-walkthrough.md) in Azure Container Service

* [Installeer en configureer `kubectl` ](../container-service-connect.md) op een lokale computer

* [Installeer Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) op een lokale computer

## <a name="helm-basics"></a>Helm basisbeginselen 

tooview informatie over Hallo Kubernetes cluster dat u helmstok installeren en implementeren van uw toepassingen op, typ Hallo volgende opdracht:

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Nadat u Helm hebt geïnstalleerd, installeert u helmstok op uw cluster Kubernetes door Hallo volgende opdracht te typen:

```bash
helm init --upgrade
```
Wanneer het is voltooid, ziet u uitvoer zoals Hallo volgende:

![Helmstok installatie](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview alle Hallo Helm grafieken beschikbaar in Hallo-opslagplaats, type Hallo volgende opdracht:

```bash 
helm search 
```

U weergegeven Hallo volgende uitvoer:

![Helm zoeken](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello grafieken tooget Hallo meest recente versies, typt u:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Een grafiek Nginx inkomend domeincontroller implementeren 
 
toodeploy een grafiek Nginx ingress-controller, typt u een één-opdracht:

```bash
helm install stable/nginx-ingress 
```
![Inkomend domeincontroller implementeren](./media/container-service-kubernetes-helm/nginx-ingress.png)

Als u typt `kubectl get svc` tooview alle services die worden uitgevoerd op Hallo-cluster, die u ziet dat een IP-adres toohello inkomend controller is toegewezen. (Terwijl het Hallo-toewijzing wordt uitgevoerd, ziet u `<pending>`. Het duurt een paar minuten toocomplete.) 

Nadat het Hallo IP-adres wordt toegewezen, gaat u toohello waarde van Hallo externe IP-adres toosee hello Nginx back-end uitgevoerd. 
 
![Inkomend IP-adres](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee een lijst met grafieken geïnstalleerd op uw cluster, type:

```bash
helm list 
```

U kunt ook de opdracht hello te opgeven`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Een grafiek MariaDB en de client implementeren

Een grafiek MariaDB en een MariaDB client tooconnect toohello database nu implementeren.

toodeploy hello MariaDB grafiek, type Hallo volgende opdracht:

```bash
helm install --name v1 stable/mariadb
```

waar `--name` een label dat is gebruikt voor versies.

> [!TIP]
> Als het Hallo-implementatie mislukt, voert u `helm repo update` en probeer het opnieuw.
>
 
 
tooview alle Hallo grafieken geïmplementeerd op het cluster, type:

```bash 
helm list
```
 
tooview alle implementaties die worden uitgevoerd op uw cluster, typt u:

```bash
kubectl get deployments 
``` 
 
 
Ten slotte toorun een schil tooaccess Hallo client, typt u:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
type Hallo de volgende opdracht en vervangt-client toohello tooconnect `v1-mariadb` met Hallo-naam van uw implementatie:

```bash
sudo mysql –h v1-mariadb
```
 
 
U kunt nu standaard SQL-opdrachten toocreate databases, tabellen, enzovoort. Bijvoorbeeld: `Create DATABASE testdb1;` maakt een lege database. 
 
 
 
## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over het beheren van Kubernetes grafieken Hallo [Helm documentatie](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

