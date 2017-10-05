---
title: Draft gebruiken met Azure Container Service en Azure Container Registry | Microsoft Docs
description: Maak een ACS Kubernetes-cluster en een Azure Container Registry om uw eerste toepassing met Draft te maken in Azure.
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
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="bc3ad-104">Draft gebruiken met Azure Container Service en Azure Container Registry om een Kubernetes-toepassing te bouwen en implementeren</span><span class="sxs-lookup"><span data-stu-id="bc3ad-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="bc3ad-105">[Draft](https://aka.ms/draft) is een nieuw open-source hulpprogramma waarmee u eenvoudig containertoepassingen kunt ontwikkelen en ze kunt implementeren in Kubernetes-clusters. U hoeft hiervoor niet veel te weten over Docker en Kubernetes (u hoeft ze zelfs niet eens te installeren!).</span><span class="sxs-lookup"><span data-stu-id="bc3ad-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="bc3ad-106">Als u een hulpprogramma als Draft gebruikt, kunnen u en uw team zich richten op het bouwen van de toepassing met Kubernetes en hoeft er minder aandacht te worden besteed aan de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="bc3ad-107">U kunt Draft gebruiken met alle Docker-installatiekopieregisters en alle Kubernetes-clusters, ook de lokale.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="bc3ad-108">In deze zelfstudie leert u hoe u ACS gebruikt met Kubernetes, ACR en Azure DNS om een live-CI/CD-ontwikkelingspijplijn maakt met Draft.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="bc3ad-109">Een Azure Container Registry maken</span><span class="sxs-lookup"><span data-stu-id="bc3ad-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="bc3ad-110">U kunt eenvoudig [een nieuw Azure Container Registry maken](../../container-registry/container-registry-get-started-azure-cli.md). De stappen daarvoor zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="bc3ad-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="bc3ad-111">Maak een Azure-resourcegroep voor het beheren van uw ACR-register en het Kubernetes-cluster in ACS.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="bc3ad-112">Een ACR-installatiekopiekopieregister maken met [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="bc3ad-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="bc3ad-113">Een Azure Container Service maken met Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bc3ad-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="bc3ad-114">U bent er nu klaar voor om [az acs create](/cli/azure/acs#create) te gebruiken voor het maken van een ACS-cluster met Kubernetes als de `--orchestrator-type`-waarde.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="bc3ad-115">Kubernetes is niet het standaardorchestratortype, dus gebruik de `--orchestrator-type kubernetes`-switch.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="bc3ad-116">Wanneer dit is gelukt, ziet de uitvoer er als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
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

<span data-ttu-id="bc3ad-117">Wanneer u een cluster hebt, kunt u de referenties importeren met de opdracht [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="bc3ad-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="bc3ad-118">U hebt nu een lokaal configuratiebestand voor uw cluster. Dit bestand hebben Helm en Draft nodig om werk te verrichten.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="bc3ad-119">Draft installeren en configureren</span><span class="sxs-lookup"><span data-stu-id="bc3ad-119">Install and configure draft</span></span>
<span data-ttu-id="bc3ad-120">De installatie-instructies voor Draft staan in de [Draft-opslagplaats](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="bc3ad-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="bc3ad-121">De instructies zijn relatief eenvoudig, maar er is wel enige configuratie nodig. [Helm](https://aka.ms/helm) is namelijk nodig om een Helm-grafiek te maken en implementeren in het Kubernetes-cluster.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="bc3ad-122">[Download en installeer Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="bc3ad-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="bc3ad-123">Gebruik Helm om `stable/traefik` te zoeken en installeren en gebruik een ingangscontroller om binnenkomende verzoeken in te schakelen voor uw builds.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="bc3ad-124">Stel nu een controle in voor de `ingress`-controller om de externe IP-waarde vast te leggen bij de implementatie.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="bc3ad-125">Dit IP-adres wordt [toegewezen aan het implementatiedomein](#wire-up-deployment-domain) in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="bc3ad-126">In dit geval is het externe IP-adres voor het implementatiedomein `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="bc3ad-127">U kunt uw domein nu toewijzen aan dat IP-adres.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="bc3ad-128">Wire-up van het implementatiedomein</span><span class="sxs-lookup"><span data-stu-id="bc3ad-128">Wire up deployment domain</span></span>

<span data-ttu-id="bc3ad-129">Draft maakt een release voor elke Helm-grafiek die er wordt gemaakt en elke toepassing waar u aan werkt.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="bc3ad-130">Elk item krijgt een gegenereerde naam die door Draft als _subdomein_ wordt gebruikt op het hoofd_implementatiedomein_ dat u beheert.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="bc3ad-131">(In dit voorbeeld wordt `squillace.io` gebruikt als domein voor implementatie.) Als u dit subdomeingedrag wilt inschakelen, moet u een A-record maken voor `'*'` in de DNS-vermeldingen van het implementatiedomein. Op die manier wordt elk gegenereerde subdomein gerouteerd naar de controller voor binnenkomend verkeer van het Kubernetes-cluster.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="bc3ad-132">Elke eigen domeinprovider wijst op zijn eigen manier DNS-servers toe. Als u uw [domeinnaamservers wilt overdragen aan Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bc3ad-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="bc3ad-133">Maak een resourcegroep voor uw zone.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="bc3ad-134">Maak een DNS-zone voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="bc3ad-135">Gebruik de opdracht [az network dns zone create](/cli/azure/network/dns/zone#create) om de naamservers te verkrijgen voor het delegeren van DNS-controle over uw domein aan Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
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
3. <span data-ttu-id="bc3ad-136">Voeg de DNS-servers die u ontvangt toe aan de domeinprovider van uw implementatiedomein. Op die manier kunt u Azure DNS gebruiken om uw domein naar wens opnieuw toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="bc3ad-137">Maak een A-recordsetvermelding voor uw implementatiedomein dat is toegewezen aan het `ingress` IP-adres uit stap 2 van de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="bc3ad-138">De uitvoer ziet er ongeveer zo uit:</span><span class="sxs-lookup"><span data-stu-id="bc3ad-138">The output looks something like:</span></span>
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

5. <span data-ttu-id="bc3ad-139">Configureer Draft om uw eigen register te gebruiken en om subdomeinen te maken voor elk Helm-diagram dat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="bc3ad-140">U hebt het volgende nodig voor het configureren van Draft:</span><span class="sxs-lookup"><span data-stu-id="bc3ad-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="bc3ad-141">de naam van uw Azure Container Registry (in dit voorbeeld is dat `draft`)</span><span class="sxs-lookup"><span data-stu-id="bc3ad-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="bc3ad-142">de registersleutel of het wachtwoord van `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="bc3ad-143">het hoofdimplementatiedomein dat u hebt geconfigureerd voor toewijzing aan het externe-IP-adres voor binnenkomend verkeer van Kubernetes (hier is dat `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="bc3ad-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="bc3ad-144">Roep `draft init` aan. In het configuratieproces wordt u dan om de bovenstaande waarden gevraagd.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="bc3ad-145">De eerste keer dat u het proces uitvoert, ziet het er ongeveer als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-145">The process looks something like the following the first time you run it.</span></span>
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

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="bc3ad-146">U kunt nu een toepassing implementeren.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="bc3ad-147">Een toepassing bouwen en implementeren</span><span class="sxs-lookup"><span data-stu-id="bc3ad-147">Build and deploy an application</span></span>

<span data-ttu-id="bc3ad-148">In de Draft-opslagplaats staan [zes eenvoudige voorbeeldtoepassingen](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="bc3ad-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="bc3ad-149">Kloon de opslagplaats en gebruik het [Python-voorbeeld](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="bc3ad-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="bc3ad-150">Ga naar de map examples/Python en typ `draft create` om de toepassing te bouwen.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="bc3ad-151">De toepassing zou er als volgt moeten uitzien.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="bc3ad-152">De uitvoer bevat een Dockerfile en een Helm-diagram.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="bc3ad-153">Typ `draft up` om te bouwen en implementeren.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="bc3ad-154">De uitvoer is uitgebreid, maar begint als het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-154">The output is extensive, but begins like the following example.</span></span>
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

<span data-ttu-id="bc3ad-155">en eindigt ongeveer als in het volgende voorbeeld als het proces goed is verlopen.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="bc3ad-156">Ongeacht de naam van de grafiek is, kunt u nu naar `curl http://gangly-bronco.squillace.io` gaan voor het ontvangen van het antwoord `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc3ad-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc3ad-157">Next steps</span></span>

<span data-ttu-id="bc3ad-158">Nu u beschikt over een ACS Kubernetes-cluster, kunt u onderzoek uitvoeren met [Azure Container Registry](../../container-registry/container-registry-intro.md) om meer en andere implementaties te maken voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="bc3ad-159">U kunt bijvoorbeeld de domein-DNS-recordset draft._basedomain.toplevel_ maken om processen van specifieke ACS-implementaties vanuit een dieper gelegen subdomein te controleren.</span><span class="sxs-lookup"><span data-stu-id="bc3ad-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






