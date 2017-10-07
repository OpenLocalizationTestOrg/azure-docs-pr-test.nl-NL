---
title: aaaQuickstart - cluster voor Linux Azure Kubernetes | Microsoft Docs
description: Snel meer toocreate een cluster Kubernetes voor Linux-containers in Azure Container Service met hello Azure CLI.
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a>Kubernetes-cluster voor Linux-containers implementeren

Een cluster Kubernetes wordt geïmplementeerd met behulp van hello Azure CLI in deze snel starten. Een container voor meerdere-toepassing die bestaan uit een webfront-end en een Redis-exemplaar wordt vervolgens geïmplementeerd en uitgevoerd op Hallo-cluster. Zodra de voltooid, Hallo-toepassing is toegankelijk via internet Hallo. 

Hallo-voorbeeldtoepassing die is gebruikt in dit document is geschreven in Python. Hallo-concepten en hier beschreven stappen kunnen worden gebruikt toodeploy elke container installatiekopie in een cluster met Kubernetes. Hallo code, Dockerfile en vooraf gemaakte Kubernetes manifestbestanden gerelateerde toothis project zijn beschikbaar op [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).

![Afbeelding van tooAzure stem bladeren](media/container-service-kubernetes-walkthrough/azure-vote.png)

Deze snel starten, wordt ervan uitgegaan dat een basiskennis van Kubernetes concepten, Zie voor gedetailleerde informatie over Kubernetes hello [Kubernetes documentatie]( https://kubernetes.io/docs/home/).

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

Uitvoer:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a>Een Kubernetes-cluster maken

Een cluster Kubernetes maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht. Hallo volgende voorbeeld wordt een cluster met de naam *myK8sCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

Na enkele minuten Hallo-opdracht is voltooid en retourneert informatie over de json-indeling over Hallo-cluster. 

## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello

Gebruik een cluster Kubernetes toomanage [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), Hallo Kubernetes opdrachtregelprogramma client. 

Als u Azure CloudShell gebruikt, is kubectl al geïnstalleerd. Als u wilt dat tooinstall deze lokaal, kunt u Hallo [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) opdracht.

tooconfigure kubectl tooconnect tooyour Kubernetes cluster uitvoeren Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht. Deze stap referenties downloadt en configureert u Hallo Kubernetes CLI toouse ze.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello verbinding tooyour cluster, gebruik Hallo [kubectl ophalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht tooreturn een lijst met clusterknooppunten Hallo.

```azurecli-interactive
kubectl get nodes
```

Uitvoer:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Een manifestbestand Kubernetes definieert een gewenste status voor Hallo-cluster, inclusief wat de installatiekopieën van de container moeten worden uitgevoerd. In dit voorbeeld is een manifest gebruikte toocreate alle objecten die nodig zijn toorun hello Azure stem toepassing. 

Maak een bestand met de naam `azure-vote.yml` en kopiëren naar het volgende YAML Hallo. Als u werkt in Azure Cloud Shell, kan dit bestand worden gemaakt met behulp van vi of Nano, zoals bij een virtueel of fysiek systeem.

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

Gebruik Hallo [kubectl maken](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) opdracht toorun Hallo-toepassing.

```azurecli-interactive
kubectl create -f azure-vote.yml
```

Uitvoer:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a>Hallo toepassing testen

Als de toepassing hello wordt uitgevoerd, een [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) wordt gemaakt dat gegarandeerd toepassing front-end toohello Hallo internet. Dit kan enkele minuten toocomplete duren. 

toomonitor gemaakt, maar gebruik Hallo [kubectl ophalen service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht Hello `--watch` argument.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

In eerste instantie Hallo **extern IP-** voor Hallo *azure stem voorgrond* service wordt weergegeven als *in behandeling*. Nadat u Hallo extern IP-adres is gewijzigd van *in behandeling* tooan *IP-adres*, gebruik `CTRL-C` toostop hello kubectl controle proces. 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

U kunt nu toohello externe IP-adres toosee hello Azure stem App bladeren.

![Afbeelding van tooAzure stem bladeren](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a>Cluster verwijderen
Wanneer Hallo cluster niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, containerservice en alle gerelateerde resources.

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Hallo code ophalen

In deze snel starten is vooraf gemaakte container installatiekopieën gebruikte toocreate een Kubernetes-implementatie. Hallo gerelateerd toepassingscode, Dockerfile, en het manifestbestand Kubernetes zijn beschikbaar op GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Volgende stappen

In deze snel starten een cluster Kubernetes geïmplementeerd en een toepassing met meerdere container tooit geïmplementeerd. 

toolearn meer informatie over Azure Container Service en doorloop compleet codevoorbeeld met toodeployment blijven toohello Kubernetes cluster zelfstudie.

> [!div class="nextstepaction"]
> [Een ACS Kubernetes-cluster beheren](./container-service-tutorial-kubernetes-prepare-app.md)
