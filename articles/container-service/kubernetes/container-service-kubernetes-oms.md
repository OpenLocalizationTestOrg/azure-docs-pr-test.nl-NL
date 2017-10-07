---
title: aaaMonitor Azure Kubernetes cluster - Operations Management | Microsoft Docs
description: Bewaking van Kubernetes cluster in Azure Container Service met behulp van Microsoft Operations Management Suite
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="70871-103">Een Azure Container Service-cluster met de Microsoft Operations Management Suite (OMS) bewaken</span><span class="sxs-lookup"><span data-stu-id="70871-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70871-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="70871-104">Prerequisites</span></span>
<span data-ttu-id="70871-105">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="70871-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="70871-106">Ook wordt ervan uitgegaan dat u Hallo hebt `az` Azure cli en `kubectl` hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="70871-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="70871-107">U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="70871-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="70871-108">Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="70871-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="70871-109">U kunt ook gebruiken [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), die Hallo heeft `az` Azure cli en `kubectl` hulpprogramma's voor u hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="70871-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="70871-110">U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="70871-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="70871-111">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="70871-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="70871-112">tootest als u kubernetes sleutels die zijn geïnstalleerd in uw kubectl-hulpprogramma hebt die u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="70871-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="70871-113">Als hello boven de fouten van de opdracht uit, moet u tooinstall kubernetes cluster sleutels in de kubectl tool.</span><span class="sxs-lookup"><span data-stu-id="70871-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="70871-114">Met de volgende opdracht Hallo kunt u dat doen:</span><span class="sxs-lookup"><span data-stu-id="70871-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="70871-115">Bewaking van Containers met Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="70871-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="70871-116">Microsoft Operations Management (OMS) is van Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="70871-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="70871-117">Container oplossing is een oplossing in OMS Log Analytics, waardoor u inventaris weergeven Hallo-container, prestaties en logboeken op één locatie.</span><span class="sxs-lookup"><span data-stu-id="70871-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="70871-118">U kunt controleren, containers oplossen door bekijkt hello Logboeken in de centrale locatie en veel ruis veroorzaken verbruikt overtollige container op een host vinden.</span><span class="sxs-lookup"><span data-stu-id="70871-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="70871-119">Raadpleeg voor meer informatie over de oplossing Container toothe [Container oplossing Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="70871-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="70871-120">OMS installeren op Kubernetes</span><span class="sxs-lookup"><span data-stu-id="70871-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="70871-121">Uw werkruimte-ID en sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="70871-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="70871-122">Hallo OMS-agent tootalk toohello-service moet toobe geconfigureerd met een werkruimte-id en een werkruimtesleutel.</span><span class="sxs-lookup"><span data-stu-id="70871-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="70871-123">tooget hello werkruimte-id en sleutel moet u een OMS toocreate account op <https://mms.microsoft.com>. Volg Hallo stappen toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="70871-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="70871-124">Wanneer u klaar bent met het Hallo-account maken, moet u tooobtain uw id en -sleutel door te klikken op **instellingen**, klikt u vervolgens **verbonden bronnen**, en vervolgens **Linux-Servers**, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70871-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="70871-125">Hallo OMS-agent met behulp van een DaemonSet installeren</span><span class="sxs-lookup"><span data-stu-id="70871-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="70871-126">DaemonSets worden gebruikt door Kubernetes toorun één exemplaar van een container op elke host in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="70871-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="70871-127">Ze zijn ideaal voor bewaking agenten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="70871-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="70871-128">Hier volgt Hallo [DaemonSet YAML bestand](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="70871-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="70871-129">Sla het bestand tooa met de naam `oms-daemonset.yaml` en vervang Hallo placeholder waarden voor `WSID` en `KEY` door uw werkruimte-id en sleutel in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="70871-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="70871-130">Nadat u uw werkruimte-ID en sleutel toohello DaemonSet configuratie hebt toegevoegd, kunt u Hallo OMS-agent installeren op uw cluster Hello `kubectl` opdrachtregelprogramma:</span><span class="sxs-lookup"><span data-stu-id="70871-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="70871-131">Hallo OMS-agent met behulp van een geheim Kubernetes installeren</span><span class="sxs-lookup"><span data-stu-id="70871-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="70871-132">tooprotect uw OMS-werkruimte-ID en de sleutel die u kunt Kubernetes geheim gebruiken als onderdeel van DaemonSet YAML-bestand.</span><span class="sxs-lookup"><span data-stu-id="70871-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="70871-133">Hallo-script, geheime sjabloonbestand en Hallo DaemonSet YAML-bestand kopiëren (van [opslagplaats](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) en zorg ervoor dat ze zich op Hallo dezelfde directory.</span><span class="sxs-lookup"><span data-stu-id="70871-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="70871-134">geheim script - geheim gen.sh genereren</span><span class="sxs-lookup"><span data-stu-id="70871-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="70871-135">geheime sjabloon - geheim template.yaml</span><span class="sxs-lookup"><span data-stu-id="70871-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="70871-136">Bestand DaemonSet YAML - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="70871-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="70871-137">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70871-137">Run hello script.</span></span> <span data-ttu-id="70871-138">Hallo script vraagt naar Hallo OMS-werkruimte-ID en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="70871-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="70871-139">Plaats die en Hallo script maakt een geheime yaml-bestand zodat u deze kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70871-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="70871-140">Hallo geheimen schil maken door het uitvoeren van de volgende Hallo:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="70871-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="70871-141">toocheck hello volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="70871-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="70871-142">Maken van uw omsagent daemon-set door te voeren``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="70871-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="70871-143">Conclusie</span><span class="sxs-lookup"><span data-stu-id="70871-143">Conclusion</span></span>
<span data-ttu-id="70871-144">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="70871-144">That's it!</span></span> <span data-ttu-id="70871-145">U moet na een paar minuten kunnen toosee gegevens stromende tooyour OMS-dashboard.</span><span class="sxs-lookup"><span data-stu-id="70871-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
