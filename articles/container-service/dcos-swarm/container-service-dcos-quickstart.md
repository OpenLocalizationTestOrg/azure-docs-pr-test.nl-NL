---
title: aaaAzure Container Service Quick Start - DC/OS-Cluster implementeren | Microsoft Docs
description: Azure Container Service Quick Start - DC/OS-Cluster implementeren
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Een DC/OS-cluster implementeren

DC/OS biedt een gedistribueerde platform voor lopende moderne en beperkte toepassingen. Met Azure Container Service is het inrichten van een productie gereed DC/OS-cluster snel en eenvoudig. Deze eenvoudige stappen voor snel starten details Hallo nodig toodeploy een DC/OS-cluster en voer basic werkbelasting.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Deze zelfstudie vereist hello Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Meld u bij tooAzure 

Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>DC/OS-cluster maken

Maken van een DC/OS-cluster met Hallo [az acs maken](/cli/azure/acs#create) opdracht.

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

Hallo SSH-tunnel kan worden getest door te bladeren`http://localhost`. Als een poort andere 80 is bereikt, Hallo locatie toomatch aanpassen. 

Als de SSH-tunnel Hallo is gemaakt, wordt Hallo DC/OS-portal geretourneerd.

![DCOS GEBRUIKERSINTERFACE](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>DC/OS CLI installeren

Hallo-opdrachtregelinterface voor DC/OS is gebruikte toomanage een DC/OS-cluster met Hallo vanaf de opdrachtregel. Hallo DC/OS cli met Hallo installeren [az acs dcos install-cli](/azure/acs/dcos#install-cli) opdracht. Als u Azure CloudShell, Hallo DC/OS CLI is al geïnstalleerd. 

Als u hello Azure CLI voor Mac OS- of Linux uitvoert, moet u mogelijk toorun Hallo opdracht met sudo.

```azurecli
az acs dcos install-cli
```

Voordat u Hallo die CLI kan worden gebruikt met Hallo-cluster, moet dit geconfigureerde toouse Hallo SSH-tunnel. toodo uitgevoerd dus Hallo de volgende opdracht, Hallo-poort aan te passen, indien nodig.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Een toepassing uitvoeren

Hallo-standaardwaarde planning mechanisme voor een ACS-DC/OS-cluster is Marathon. Marathon gebruikte toostart is een toepassing en status van toepassing op de DC/OS-cluster Hallo HALLO hallo beheren. tooschedule een toepassing via Marathon, maak een bestand met de naam *marathon app.json*, en kopiëren Hallo inhoud in de App. 

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
dcos marathon app add marathon-app.json
```

Hallo Implementatiestatus toosee voor Hallo-app Hallo volgende opdracht uitvoeren.

```azurecli
dcos marathon app list
```

Wanneer Hallo **WACHTEN** kolomwaarde verandert van *True* te*False*, implementatie van toepassing is voltooid.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Hallo openbare IP-adres van Hallo DC/OS-cluster agents worden opgehaald.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Bladeren door toothis adres retourneert Hallo standaard NGINX-site.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>DC/OS-cluster verwijderen

Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, DC/OS-cluster en alle gerelateerde resources.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Volgende stappen

In deze snel starten een DC/OS-cluster hebt geïmplementeerd en een eenvoudige Docker-container op Hallo cluster hebt uitgevoerd. toolearn meer informatie over Azure Container Service blijven toohello ACS zelfstudies.

> [!div class="nextstepaction"]
> [Een ACS-DC/OS-Cluster beheren](container-service-dcos-manage-tutorial.md)