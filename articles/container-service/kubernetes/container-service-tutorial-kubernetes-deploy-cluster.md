---
title: zelfstudie voor aaaAzure Container Service - Cluster implementeren | Microsoft Docs
description: Zelfstudie voor Azure Container Service - Cluster implementeren
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Een cluster Kubernetes in Azure Container Service implementeren

Kubernetes biedt een gedistribueerde platform voor beperkte toepassingen. Met Azure Container Service is het inrichten van een cluster met productie gereed Kubernetes snel en eenvoudig. In deze zelfstudie maakt deel 3 van 7, wordt een Azure Container Service Kubernetes-cluster geïmplementeerd. Stappen voltooid omvatten:

> [!div class="checklist"]
> * Een Kubernetes ACS-cluster implementeren
> * Installatie van Hallo Kubernetes CLI (kubectl)
> * Configuratie van kubectl

In volgende zelfstudies hello Azure stem toepassing is geïmplementeerd toohello cluster geschaald, bijgewerkt en Operations Management Suite geconfigureerde toomonitor hello Kubernetes cluster is.

## <a name="before-you-begin"></a>Voordat u begint

In vorige zelfstudies een installatiekopie van een container is gemaakt en tooan Azure Container register exemplaar geüpload. Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Een Kubernetes-cluster maken

In Hallo [vorige zelfstudie](./container-service-tutorial-kubernetes-prepare-acr.md), een resourcegroep met de naam *myResourceGroup* is gemaakt. Als u dit niet gedaan hebt, nu deze resourcegroep maken.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Een cluster Kubernetes maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht. 

Hallo volgende voorbeeld wordt een cluster met de naam *myK8sCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Hallo-opdracht is voltooid na een paar minuten en json retourneert informatie over de implementatie van Hallo ACS geformatteerd.

## <a name="install-hello-kubectl-cli"></a>Hallo kubectl CLI installeren

tooconnect toohello Kubernetes-cluster van de clientcomputer gebruik [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), Hallo Kubernetes opdrachtregelprogramma client. 

Als u Azure CloudShell gebruikt, is `kubectl` al geïnstalleerd. Als u wilt dat tooinstall het lokaal hello gebruiken [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) opdracht.

Als in de Linux- of Mac OS uitgevoerd, moet u mogelijk toorun met sudo. In Windows, zorg ervoor dat uw shell is uitgevoerd als administrator.

```azurecli-interactive 
az acs kubernetes install-cli 
```

Op Windows hello standaardinstallatie is *c:\program files (x86)\kubectl.exe*. U moet mogelijk tooadd toohello Windows bestandspad. 

## <a name="connect-with-kubectl"></a>Verbinden met kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster uitvoeren Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify hello verbinding tooyour cluster uitvoeren Hallo [kubectl ophalen knooppunten](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.

```azurecli-interactive
kubectl get nodes
```

Uitvoer:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

Zelfstudie is voltooid hebt u een ACS-Kubernetes cluster gereed voor werkbelastingen. In volgende zelfstudies is een toepassing met meerdere container geïmplementeerde toothis cluster, uitgebreid, bijgewerkt en bewaakt.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie is een Azure Container Service Kubernetes-cluster is geïmplementeerd. Hallo stappen zijn voltooid:

> [!div class="checklist"]
> * Implementatie van een cluster Kubernetes ACS
> * Geïnstalleerde Hallo Kubernetes CLI (kubectl)
> * Geconfigureerde kubectl

Ga toohello volgende zelfstudie toolearn over het uitvoeren van toepassing op Hallo-cluster.

> [!div class="nextstepaction"]
> [De toepassing in Kubernetes implementeren](./container-service-tutorial-kubernetes-deploy-application.md)
