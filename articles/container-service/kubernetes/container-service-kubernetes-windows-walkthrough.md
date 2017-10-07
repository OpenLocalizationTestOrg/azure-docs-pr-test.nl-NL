---
title: aaaQuickstart - cluster voor Windows Azure Kubernetes | Microsoft Docs
description: Snel meer toocreate een cluster Kubernetes voor Windows-containers in Azure Container Service met hello Azure CLI.
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Kubernetes-cluster voor Windows-containers implementeren

Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts. De details van deze handleiding hello Azure CLI toodeploy met een [Kubernetes](https://kubernetes.io/docs/home/) -cluster in [Azure Container Service](../container-service-intro.md). Zodra Hallo-cluster is geïmplementeerd, u verbinding maakt tooit Hello Kubernetes `kubectl` opdrachtregelprogramma en u uw eerste Windows-container te implementeren.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

> [!NOTE]
> De ondersteuning voor Windows-containers in Kubernetes in Azure Container Service is momenteel beschikbaar als preview. 
>

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Een Kubernetes-cluster maken
Een cluster Kubernetes maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht. 

Hallo volgende voorbeeld wordt een cluster met de naam *myK8sCluster* hoofdsleutel met een Linux-knooppunt en twee knooppunten van de Windows-agent. In dit voorbeeld maakt SSH-sleutels nodig tooconnect toohello Linux master. In dit voorbeeld wordt *azureuser* voor de naam van een gebruiker met beheerdersrechten en *myPassword12* Hallo-wachtwoord op Hallo Windows knooppunten. Deze waarden toosomething juiste tooyour omgeving bijwerken. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Na enkele minuten Hallo-opdracht is voltooid en ziet u informatie over uw implementatie.

## <a name="install-kubectl"></a>Kubectl installeren

tooconnect toohello Kubernetes-cluster van de clientcomputer gebruik [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), Hallo Kubernetes opdrachtregelprogramma client. 

Als u Azure CloudShell gebruikt, is `kubectl` al geïnstalleerd. Als u wilt dat tooinstall deze lokaal, kunt u Hallo [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) opdracht.

Hallo Azure CLI voorbeeld installeert na `kubectl` tooyour system. In Windows moet u deze opdracht uitvoeren als beheerder.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Verbinden met kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster uitvoeren Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht. Hallo downloadt volgende voorbeeld Hallo clusterconfiguratie voor uw cluster Kubernetes.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello verbinding tooyour cluster van uw computer, probeer uit te voeren:

```azurecli-interactive
kubectl get nodes
```

`kubectl`Geeft een lijst Hallo hoofd- en agent knooppunten.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Een Windows IIS-container implementeren

U kunt een Docker-container uitvoeren binnen een Kubernetes-*schil*, die een of meer containers bevat. 

Dit eenvoudige voorbeeld maakt gebruik van een JSON-bestand toospecify een container Microsoft Internet Information Server (IIS) en maakt vervolgens Hallo schil Hallo met `kubctl apply` opdracht. 

Maken van een lokaal bestand met de naam `iis.json` en kopiëren Hallo tekst. Dit bestand vertelt Kubernetes toorun IIS op Windows Server 2016 Nano Server met de installatiekopie van een openbare container van [Docker Hub](https://hub.docker.com/r/nanoserver/iis/). Hallo-container gebruikt poort 80, maar in eerste instantie is alleen toegankelijk vanuit Hallo clusternetwerk.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart hello schil type:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

implementatie van tootrack hello, type:
  
```azurecli-interactive
kubectl get pods
```

Hoewel Hallo schil implementeert, is het Hallo-status `ContainerCreating`. Het kan enkele minuten duren voordat Hallo container tooenter hello `Running` status.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Weergave Hallo IIS-welkomstpagina

tooexpose Hallo schil toohello wereld met een openbaar IP-adres, type Hallo volgende opdracht:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Met deze opdracht maakt Kubernetes een service en een [Azure load balancer-regel](container-service-kubernetes-load-balancing.md) met een openbaar IP-adres voor Hallo-service. 

Hallo na de opdracht toosee Hallo status van Hallo-service wordt uitgevoerd.

```azurecli-interactive
kubectl get svc
```

In eerste instantie Hallo IP-adres wordt weergegeven als `pending`. Na een paar minuten Hallo externe IP-adres van Hallo `iis` schil is ingesteld:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

U kunt een webbrowser van uw keuze toosee Hallo IIS standaardwelkomstpagina op Hallo externe IP-adres gebruiken:

![Afbeelding van tooIIS bladeren](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Cluster verwijderen
Wanneer Hallo cluster niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, containerservice en alle gerelateerde resources.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u een Kubernetes-cluster geïmplementeerd, het verbonden met `kubectl` en een schil met een IIS-container geïmplementeerd. toolearn meer informatie over Azure Container Service blijven toohello Kubernetes zelfstudie.

> [!div class="nextstepaction"]
> [Een ACS Kubernetes-cluster beheren](container-service-tutorial-kubernetes-prepare-app.md)
