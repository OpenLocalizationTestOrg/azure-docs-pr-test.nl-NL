---
title: aaaUse concept met Azure Container Service en Azure Container register | Microsoft Docs
description: Een ACS-Kubernetes-cluster en een Azure Container register toocreate uw eerste toepassing maken in Azure met concept.
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, containers, microservices, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Concept gebruiken met Azure Container Service en Azure Container register toobuild en implementeren van een toepassing tooKubernetes

[Concept](https://aka.ms/draft) is een nieuw open-source hulpprogramma die het gemakkelijk toodevelop container gebaseerde toepassingen maakt en implementeert ze tooKubernetes clusters zonder veel over Docker en Kubernetes--weten of deze zelfs te installeren. Met hulpprogramma's zoals ontwerp kunt u en uw focus teams op Hallo-toepassing met Kubernetes bouwen, niet zoveel tooinfrastructure aandacht te betalen.

U kunt Draft gebruiken met alle Docker-installatiekopieregisters en alle Kubernetes-clusters, ook de lokale. Deze zelfstudie laat zien hoe toouse ACS met Kubernetes ACR en Azure DNS toocreate een live CI/CD-ontwikkelaar pipeline-concept gebruiken.


## <a name="create-an-azure-container-registry"></a>Een Azure Container Registry maken
U kunt gemakkelijk [maken van een nieuwe Azure-Container register](../../container-registry/container-registry-get-started-azure-cli.md), maar Hallo stappen zijn als volgt:

1. Maak een Azure resource group toomanage uw ACR-register en Hallo Kubernetes-cluster in ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Een ACR-installatiekopiekopieregister maken met [az acr create](/cli/azure/acr#create)
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Een Azure Container Service maken met Kubernetes

U kunt nu klaar toouse [az acs maken](/cli/azure/acs#create) toocreate een ACS-cluster met Kubernetes als Hallo `--orchestrator-type` waarde.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Omdat Kubernetes niet Hallo standaard orchestrator-type is, zorg ervoor dat u Hallo `--orchestrator-type kubernetes` overschakelen.

Hallo uitvoer wanneer geslaagde vergelijkbare toohello volgende gezocht.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Nu dat u een cluster hebt, kunt u Hallo referenties importeren met behulp van Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht. U hebt nu een lokale configuratiebestand voor uw cluster, is welke Helm en een concept moet tooget hun werk.

## <a name="install-and-configure-draft"></a>Draft installeren en configureren
Hallo-installatie-instructies voor ontwerp zijn in Hallo [concept opslagplaats](https://github.com/Azure/draft/blob/master/docs/install.md). Ze zijn relatief eenvoudige, maar sommige configuratie vereisen omdat deze afhankelijk van is [Helm](https://aka.ms/helm) toocreate en implementeren van een grafiek Helm in Hallo Kubernetes cluster.

1. [Download en installeer Helm](https://aka.ms/helm#install).
2. Helm toosearch voor gebruik en installeer `stable/traefik`, en inkomend controller tooenable binnenkomende aanvragen voor uw builds.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Stel nu een controle op Hallo `ingress` controller toocapture Hallo externe IP-waarde wanneer deze is geïmplementeerd. Dit IP-adres worden Hallo een [tooyour implementatie domein toegewezen](#wire-up-deployment-domain) in de volgende sectie Hallo.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    In dit geval Hallo extern IP-adres voor Hallo implementatie domein is `13.64.108.240`. U kunt nu uw domein toothat IP toewijzen.

## <a name="wire-up-deployment-domain"></a>Wire-up van het implementatiedomein

Draft maakt een release voor elke Helm-grafiek die er wordt gemaakt en elke toepassing waar u aan werkt. Elke opgehaald van een gegenereerde naam die wordt gebruikt door het concept als een _subdomein_ boven op Hallo hoofdmap _implementatie domein_ dat u beheert. (In dit voorbeeld gebruiken we `squillace.io` als Hallo implementatie domein.) tooenable dit gedrag subdomein moet u een A-record voor `'*'` in uw DNS-vermeldingen voor uw implementatie-domein, zodat elk gegenereerd subdomein is gerouteerde toohello Kubernetes ingress-controller van het cluster.

Uw eigen domeinprovider heeft een eigen manier tooassign DNS-servers. te[delegeren van uw domein nameservers tooAzure DNS-](../../dns/dns-delegate-domain-azure-dns.md), u rekening houden met Hallo stappen te volgen:

1. Maak een resourcegroep voor uw zone.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Maak een DNS-zone voor uw domein.
Gebruik Hallo [az netwerk DNS-zone maken](/cli/azure/network/dns/zone#create) opdracht tooobtain hello nameservers toodelegate DNS-tooAzure DNS voor uw domein beheren.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Hallo DNS-servers, u toohello domeinprovider voor uw implementatie-domein, waardoor u toouse Azure DNS toorepoint uw domein krijgt als u wilt toevoegen.
4. Maak een A-record-set-vermelding voor uw implementatie domein toewijzing toohello `ingress` IP-adres uit stap 2 van de vorige sectie Hallo.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
Hallo-uitvoer ziet er ongeveer als volgt uit:
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Configureer concept toouse het register en maak subdomeinen voor elke Helm grafiek die wordt gemaakt. tooconfigure concept, moet u de:
  - de naam van uw Azure Container Registry (in dit voorbeeld is dat `draft`)
  - de registersleutel of het wachtwoord van `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.
  - Hallo implementatie hoofddomein dat u toomap toohello Kubernetes inkomend externe IP-adres hebt geconfigureerd (hier `squillace.io`)

  Roep `draft init` en configuratieproces Hallo vraagt u om de bovenstaande Hallo-waarden. Hallo proces lijkt iets Hallo volgende Hallo eerst uit te voeren.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

U bent nu klaar toodeploy een toepassing.


## <a name="build-and-deploy-an-application"></a>Een toepassing bouwen en implementeren

In de Hallo concept opslagplaats [zes eenvoudige voorbeeldtoepassingen](https://github.com/Azure/draft/tree/master/examples). Hallo-opslagplaats klonen en we gebruiken Hallo [Python voorbeeld](https://github.com/Azure/draft/tree/master/examples/python). Wijzigen in de map Voorbeelden/Python Hallo en typ `draft create` toobuild Hallo-toepassing. Het moet eruitzien als Hallo voorbeeld te volgen.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

Hallo uitvoer bevat een Dockerfile en een Helm-grafiek. toobuild en implementeren, typt u `draft up`. Hallo uitvoer is uitgebreid, maar begint zoals Hallo voorbeeld te volgen.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

en wanneer geslaagde eindigt met iets dergelijks toohello voorbeeld te volgen.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

Ongeacht de naam van de grafiek is, kunt u nu `curl http://gangly-bronco.squillace.io` tooreceive Hallo beantwoorden, `Hello World!`.

## <a name="next-steps"></a>Volgende stappen

Nu dat u een ACS-Kubernetes cluster hebt, kunt u onderzoeken met [Azure Container register](../../container-registry/container-registry-intro.md) toocreate meer- en andere implementaties van dit scenario. U kunt bijvoorbeeld de domein-DNS-recordset draft._basedomain.toplevel_ maken om processen van specifieke ACS-implementaties vanuit een dieper gelegen subdomein te controleren.






