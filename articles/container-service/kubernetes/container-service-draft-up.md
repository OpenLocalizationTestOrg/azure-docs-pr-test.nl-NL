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
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="6bb05-104">Concept gebruiken met Azure Container Service en Azure Container register toobuild en implementeren van een toepassing tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="6bb05-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="6bb05-105">[Concept](https://aka.ms/draft) is een nieuw open-source hulpprogramma die het gemakkelijk toodevelop container gebaseerde toepassingen maakt en implementeert ze tooKubernetes clusters zonder veel over Docker en Kubernetes--weten of deze zelfs te installeren.</span><span class="sxs-lookup"><span data-stu-id="6bb05-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="6bb05-106">Met hulpprogramma's zoals ontwerp kunt u en uw focus teams op Hallo-toepassing met Kubernetes bouwen, niet zoveel tooinfrastructure aandacht te betalen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="6bb05-107">U kunt Draft gebruiken met alle Docker-installatiekopieregisters en alle Kubernetes-clusters, ook de lokale.</span><span class="sxs-lookup"><span data-stu-id="6bb05-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="6bb05-108">Deze zelfstudie laat zien hoe toouse ACS met Kubernetes ACR en Azure DNS toocreate een live CI/CD-ontwikkelaar pipeline-concept gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6bb05-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="6bb05-109">Een Azure Container Registry maken</span><span class="sxs-lookup"><span data-stu-id="6bb05-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="6bb05-110">U kunt gemakkelijk [maken van een nieuwe Azure-Container register](../../container-registry/container-registry-get-started-azure-cli.md), maar Hallo stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="6bb05-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="6bb05-111">Maak een Azure resource group toomanage uw ACR-register en Hallo Kubernetes-cluster in ACS.</span><span class="sxs-lookup"><span data-stu-id="6bb05-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="6bb05-112">Een ACR-installatiekopiekopieregister maken met [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="6bb05-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="6bb05-113">Een Azure Container Service maken met Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6bb05-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="6bb05-114">U kunt nu klaar toouse [az acs maken](/cli/azure/acs#create) toocreate een ACS-cluster met Kubernetes als Hallo `--orchestrator-type` waarde.</span><span class="sxs-lookup"><span data-stu-id="6bb05-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="6bb05-115">Omdat Kubernetes niet Hallo standaard orchestrator-type is, zorg ervoor dat u Hallo `--orchestrator-type kubernetes` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="6bb05-116">Hallo uitvoer wanneer geslaagde vergelijkbare toohello volgende gezocht.</span><span class="sxs-lookup"><span data-stu-id="6bb05-116">hello output when successful looks similar toohello following.</span></span>

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

<span data-ttu-id="6bb05-117">Nu dat u een cluster hebt, kunt u Hallo referenties importeren met behulp van Hallo [az acs kubernetes get-referenties](/cli/azure/acs/kubernetes#get-credentials) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6bb05-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="6bb05-118">U hebt nu een lokale configuratiebestand voor uw cluster, is welke Helm en een concept moet tooget hun werk.</span><span class="sxs-lookup"><span data-stu-id="6bb05-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="6bb05-119">Draft installeren en configureren</span><span class="sxs-lookup"><span data-stu-id="6bb05-119">Install and configure draft</span></span>
<span data-ttu-id="6bb05-120">Hallo-installatie-instructies voor ontwerp zijn in Hallo [concept opslagplaats](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="6bb05-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="6bb05-121">Ze zijn relatief eenvoudige, maar sommige configuratie vereisen omdat deze afhankelijk van is [Helm](https://aka.ms/helm) toocreate en implementeren van een grafiek Helm in Hallo Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="6bb05-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="6bb05-122">[Download en installeer Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="6bb05-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="6bb05-123">Helm toosearch voor gebruik en installeer `stable/traefik`, en inkomend controller tooenable binnenkomende aanvragen voor uw builds.</span><span class="sxs-lookup"><span data-stu-id="6bb05-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="6bb05-124">Stel nu een controle op Hallo `ingress` controller toocapture Hallo externe IP-waarde wanneer deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6bb05-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="6bb05-125">Dit IP-adres worden Hallo een [tooyour implementatie domein toegewezen](#wire-up-deployment-domain) in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6bb05-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="6bb05-126">In dit geval Hallo extern IP-adres voor Hallo implementatie domein is `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="6bb05-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="6bb05-127">U kunt nu uw domein toothat IP toewijzen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="6bb05-128">Wire-up van het implementatiedomein</span><span class="sxs-lookup"><span data-stu-id="6bb05-128">Wire up deployment domain</span></span>

<span data-ttu-id="6bb05-129">Draft maakt een release voor elke Helm-grafiek die er wordt gemaakt en elke toepassing waar u aan werkt.</span><span class="sxs-lookup"><span data-stu-id="6bb05-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="6bb05-130">Elke opgehaald van een gegenereerde naam die wordt gebruikt door het concept als een _subdomein_ boven op Hallo hoofdmap _implementatie domein_ dat u beheert.</span><span class="sxs-lookup"><span data-stu-id="6bb05-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="6bb05-131">(In dit voorbeeld gebruiken we `squillace.io` als Hallo implementatie domein.) tooenable dit gedrag subdomein moet u een A-record voor `'*'` in uw DNS-vermeldingen voor uw implementatie-domein, zodat elk gegenereerd subdomein is gerouteerde toohello Kubernetes ingress-controller van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6bb05-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="6bb05-132">Uw eigen domeinprovider heeft een eigen manier tooassign DNS-servers. te[delegeren van uw domein nameservers tooAzure DNS-](../../dns/dns-delegate-domain-azure-dns.md), u rekening houden met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6bb05-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="6bb05-133">Maak een resourcegroep voor uw zone.</span><span class="sxs-lookup"><span data-stu-id="6bb05-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="6bb05-134">Maak een DNS-zone voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="6bb05-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="6bb05-135">Gebruik Hallo [az netwerk DNS-zone maken](/cli/azure/network/dns/zone#create) opdracht tooobtain hello nameservers toodelegate DNS-tooAzure DNS voor uw domein beheren.</span><span class="sxs-lookup"><span data-stu-id="6bb05-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
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
3. <span data-ttu-id="6bb05-136">Hallo DNS-servers, u toohello domeinprovider voor uw implementatie-domein, waardoor u toouse Azure DNS toorepoint uw domein krijgt als u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="6bb05-137">Maak een A-record-set-vermelding voor uw implementatie domein toewijzing toohello `ingress` IP-adres uit stap 2 van de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6bb05-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="6bb05-138">Hallo-uitvoer ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="6bb05-138">hello output looks something like:</span></span>
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

5. <span data-ttu-id="6bb05-139">Configureer concept toouse het register en maak subdomeinen voor elke Helm grafiek die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bb05-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="6bb05-140">tooconfigure concept, moet u de:</span><span class="sxs-lookup"><span data-stu-id="6bb05-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="6bb05-141">de naam van uw Azure Container Registry (in dit voorbeeld is dat `draft`)</span><span class="sxs-lookup"><span data-stu-id="6bb05-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="6bb05-142">de registersleutel of het wachtwoord van `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="6bb05-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="6bb05-143">Hallo implementatie hoofddomein dat u toomap toohello Kubernetes inkomend externe IP-adres hebt geconfigureerd (hier `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="6bb05-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="6bb05-144">Roep `draft init` en configuratieproces Hallo vraagt u om de bovenstaande Hallo-waarden.</span><span class="sxs-lookup"><span data-stu-id="6bb05-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="6bb05-145">Hallo proces lijkt iets Hallo volgende Hallo eerst uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="6bb05-145">hello process looks something like hello following hello first time you run it.</span></span>
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

<span data-ttu-id="6bb05-146">U bent nu klaar toodeploy een toepassing.</span><span class="sxs-lookup"><span data-stu-id="6bb05-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="6bb05-147">Een toepassing bouwen en implementeren</span><span class="sxs-lookup"><span data-stu-id="6bb05-147">Build and deploy an application</span></span>

<span data-ttu-id="6bb05-148">In de Hallo concept opslagplaats [zes eenvoudige voorbeeldtoepassingen](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="6bb05-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="6bb05-149">Hallo-opslagplaats klonen en we gebruiken Hallo [Python voorbeeld](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="6bb05-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="6bb05-150">Wijzigen in de map Voorbeelden/Python Hallo en typ `draft create` toobuild Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6bb05-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="6bb05-151">Het moet eruitzien als Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="6bb05-152">Hallo uitvoer bevat een Dockerfile en een Helm-grafiek.</span><span class="sxs-lookup"><span data-stu-id="6bb05-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="6bb05-153">toobuild en implementeren, typt u `draft up`.</span><span class="sxs-lookup"><span data-stu-id="6bb05-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="6bb05-154">Hallo uitvoer is uitgebreid, maar begint zoals Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-154">hello output is extensive, but begins like hello following example.</span></span>
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

<span data-ttu-id="6bb05-155">en wanneer geslaagde eindigt met iets dergelijks toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bb05-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="6bb05-156">Ongeacht de naam van de grafiek is, kunt u nu `curl http://gangly-bronco.squillace.io` tooreceive Hallo beantwoorden, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="6bb05-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bb05-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bb05-157">Next steps</span></span>

<span data-ttu-id="6bb05-158">Nu dat u een ACS-Kubernetes cluster hebt, kunt u onderzoeken met [Azure Container register](../../container-registry/container-registry-intro.md) toocreate meer- en andere implementaties van dit scenario.</span><span class="sxs-lookup"><span data-stu-id="6bb05-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="6bb05-159">U kunt bijvoorbeeld de domein-DNS-recordset draft._basedomain.toplevel_ maken om processen van specifieke ACS-implementaties vanuit een dieper gelegen subdomein te controleren.</span><span class="sxs-lookup"><span data-stu-id="6bb05-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






