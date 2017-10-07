---
title: zelfstudie voor aaaAzure Container Service - DC/OS beheren | Microsoft Docs
description: Zelfstudie voor Azure Container Service - DC/OS beheren
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
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Zelfstudie voor Azure Container Service - DC/OS beheren

DC/OS biedt een gedistribueerde platform voor lopende moderne en beperkte toepassingen. Met Azure Container Service is het inrichten van een productie gereed DC/OS-cluster snel en eenvoudig. Deze eenvoudige stappen voor snel starten-informatie nodig toodeploy een DC/OS-cluster en voer basic werkbelasting.

> [!div class="checklist"]
> * Een ACS-DC/OS-cluster maken
> * Verbinding maken met cluster toohello
> * Hallo DC/OS CLI installeren
> * Een toepassing toohello-cluster implementeren
> * Een toepassing op Hallo cluster schalen
> * Hallo DC/OS clusterknooppunten schalen
> * Basic DC/OS-management
> * Hallo DC/OS-cluster verwijderen

Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>DC/OS-cluster maken

Maak eerst een resourcegroep met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Maak vervolgens een DC/OS-cluster met Hallo [az acs maken](/cli/azure/acs#create) opdracht.

Hallo volgende voorbeeld maakt u een DC/OS-cluster met de naam *myDCOSCluster* en SSH-sleutels gemaakt als deze niet al bestaan. toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Hallo-opdracht is voltooid en retourneert informatie over de implementatie van Hallo na enkele minuten.

## <a name="connect-toodcos-cluster"></a>Verbinding maken met tooDC/OS-cluster

Zodra een DC/OS-cluster is gemaakt, kan het zijn toegang tot en met een SSH-tunnel. Hallo volgende opdracht tooreturn Hallo openbare IP-adres van de DC/OS-master Hallo worden uitgevoerd. Dit IP-adres is opgeslagen in een variabele en gebruikt in de volgende stap Hallo.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate Hallo SSH-tunnel, Hallo volgende opdracht uitvoeren en volg Hallo op het scherm instructies. Als poort 80 al in gebruik is is, mislukt de Hallo-opdracht. Update Hallo via een tunnel tooone poort niet in gebruik, zoals `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>DC/OS CLI installeren

Hallo DC/OS cli met Hallo installeren [az acs dcos install-cli](/azure/acs/dcos#install-cli) opdracht. Als u Azure CloudShell, Hallo DC/OS CLI is al geïnstalleerd. Als u hello Azure CLI voor Mac OS- of Linux uitvoert, moet u mogelijk toorun Hallo opdracht met sudo.

```azurecli
az acs dcos install-cli
```

Voordat u Hallo die CLI kan worden gebruikt met Hallo-cluster, moet dit geconfigureerde toouse Hallo SSH-tunnel. toodo uitgevoerd dus Hallo de volgende opdracht, Hallo-poort aan te passen, indien nodig.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Een toepassing uitvoeren

Hallo-standaardwaarde planning mechanisme voor een ACS-DC/OS-cluster is Marathon. Marathon gebruikte toostart is een toepassing en status van toepassing op de DC/OS-cluster Hallo HALLO hallo beheren. tooschedule een toepassing via Marathon, maak een bestand met de naam **marathon app.json**, en kopiëren Hallo inhoud in de App. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Hallo opdracht tooschedule Hallo toepassing toorun volgen op Hallo DC/OS-cluster worden uitgevoerd.

```azurecli
dcos marathon app add marathon-app.json
```

Hallo Implementatiestatus toosee voor Hallo-app Hallo volgende opdracht uitvoeren.

```azurecli
dcos marathon app list
```

Wanneer Hallo **taken** kolomwaarde verandert van *0/1* te*1/1*, implementatie van toepassing is voltooid.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Marathon-toepassing schalen

In het vorige voorbeeld hello, is een toepassing met één exemplaar gemaakt. Deze implementatie dat drie exemplaren van Hallo toepassing beschikbaar is, zijn geopend Hallo tooupdate **marathon app.json** bestand en Hallo exemplaar eigenschap too3 bijwerken.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Hallo-toepassing hello met bijwerken `dcos marathon app update` opdracht.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

Hallo Implementatiestatus toosee voor Hallo-app Hallo volgende opdracht uitvoeren.

```azurecli
dcos marathon app list
```

Wanneer Hallo **taken** kolomwaarde verandert van *1/3* te*31/*, implementatie van toepassing is voltooid.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Internet toegankelijk app uitvoeren

Hallo ACS DC/OS-cluster bestaat uit twee sets knooppunt, een openbare die toegankelijk is op internet Hallo en een particuliere dat niet toegankelijk op Hallo internet. Hallo standaardset is Hallo persoonlijke knooppunten, die is gebruikt in het laatste voorbeeld Hallo.

een toepassing toegankelijk toomake op Hallo van internet, deze toohello openbare knooppuntset implementeren. toodo geven dus Hallo `acceptedResourceRoles` een waarde van het object `slave_public`.

Maak een bestand met de naam **nginx public.json** en kopiëren Hallo inhoud in de App.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Hallo opdracht tooschedule Hallo toepassing toorun volgen op Hallo DC/OS-cluster worden uitgevoerd.

```azurecli 
dcos marathon app add nginx-public.json
```

Hallo openbaar IP-adres van Hallo DC/OS-cluster openbare agents worden opgehaald.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Bladeren door toothis adres retourneert Hallo standaard NGINX-site.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Schaal DC/OS-cluster

In de voorgaande voorbeelden hello is een toepassing geschaald toomultiple exemplaar. Hallo DC/OS-infrastructuur kan ook worden uitgebreid tooprovide meer of minder rekencapaciteit. Dit wordt gedaan met Hallo [az acs schalen]() opdracht. 

toosee hello Huidig aantal van de DC/OS-agents gebruiken Hallo [az acs weergeven](/cli/azure/acs#show) opdracht.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease aantal too5 hello, gebruikt u Hallo [az acs schalen](/cli/azure/acs#scale) opdracht. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>DC/OS-cluster verwijderen

Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, DC/OS-cluster en alle gerelateerde resources.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd over basic DC/OS-beheertaak, waaronder de volgende Hallo. 

> [!div class="checklist"]
> * Een ACS-DC/OS-cluster maken
> * Verbinding maken met cluster toohello
> * Hallo DC/OS CLI installeren
> * Een toepassing toohello-cluster implementeren
> * Een toepassing op Hallo cluster schalen
> * Hallo DC/OS clusterknooppunten schalen
> * Hallo DC/OS-cluster verwijderen

Geavanceerde toohello volgende zelfstudie toolearn over laden taakverdeling toepassing in DC/OS op Azure. 

> [!div class="nextstepaction"]
> [Load balancing gebruiken voor toepassingen](container-service-load-balancing.md)