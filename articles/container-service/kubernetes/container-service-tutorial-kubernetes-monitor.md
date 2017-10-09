---
title: zelfstudie voor aaaAzure Container Service - Monitor Kubernetes | Microsoft Docs
description: Zelfstudie voor Azure Container Service - Monitor Kubernetes met Microsoft Operations Management Suite (OMS)
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="fdcc3-104">Monitor voor een cluster Kubernetes met Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="fdcc3-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="fdcc3-105">Uw cluster Kubernetes en containers is niet kritiek, vooral wanneer u een productiecluster op schaal met meerdere apps beheren.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="fdcc3-106">U kunt profiteren van verschillende Kubernetes bewakingsoplossingen, van Microsoft of andere providers.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="fdcc3-107">In deze zelfstudie maakt u uw cluster Kubernetes controleren met behulp van Hallo Containers oplossing in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), van de Microsoft cloud-gebaseerde IT-oplossing.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="fdcc3-108">(Hallo OMS Containers oplossing is in preview.)</span><span class="sxs-lookup"><span data-stu-id="fdcc3-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="fdcc3-109">Deze zelfstudie maakt deel uit zeven zeven, heeft betrekking op Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="fdcc3-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdcc3-110">OMS-werkruimte-instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="fdcc3-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="fdcc3-111">Instellen van OMS-agents op Hallo Kubernetes knooppunten</span><span class="sxs-lookup"><span data-stu-id="fdcc3-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="fdcc3-112">Toegang tot informatie over prestatiebewaking op Hallo OMS-portal of Azure-portal</span><span class="sxs-lookup"><span data-stu-id="fdcc3-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fdcc3-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fdcc3-113">Before you begin</span></span>

<span data-ttu-id="fdcc3-114">In vorige zelfstudies, een toepassing is ingepakt in container-installatiekopieën, maar deze installatiekopieën geüpload tooAzure register van de Container en een Kubernetes-cluster dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="fdcc3-115">Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="fdcc3-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="fdcc3-116">Deze zelfstudie vereist ten minste een Kubernetes-cluster met knooppunten voor Linux-agent en een account van Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="fdcc3-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="fdcc3-117">Indien nodig, zich aanmelden voor een [gratis proefabonnement van OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="fdcc3-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="fdcc3-118">Werkruimte-instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="fdcc3-118">Get Workspace settings</span></span>

<span data-ttu-id="fdcc3-119">Wanneer u toegang hebt tot Hallo [OMS-portal](https://mms.microsoft.com), gaat u te**instellingen** > **verbonden bronnen** > **Linux-Servers**.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="fdcc3-120">Daar vindt u Hallo *werkruimte-ID* en een primaire of secundaire site *Werkruimtesleutel*.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="fdcc3-121">Noteer deze waarden, u moet tooset up OMS-agents op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="fdcc3-122">Instellen van OMS-agents</span><span class="sxs-lookup"><span data-stu-id="fdcc3-122">Set up OMS agents</span></span>

<span data-ttu-id="fdcc3-123">Hier volgt een tooset YAML-bestand van OMS-agents op Hallo Linux clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="fdcc3-124">Het maken van een Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), die een enkele identiek schil wordt uitgevoerd op elk clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="fdcc3-125">Hallo DaemonSet resource is ideaal voor het implementeren van een agent voor toepassingsbewaking.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="fdcc3-126">Hallo na tooa tekstbestand met de naam opslaan `oms-daemonset.yaml`, en vervang de waarden van het Hallo-tijdelijke aanduiding voor *myWorkspaceID* en *myWorkspaceKey* OMS-werkruimte-ID en sleutel van uw.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="fdcc3-127">(In productie, kunt u deze waarden coderen als geheimen.)</span><span class="sxs-lookup"><span data-stu-id="fdcc3-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="fdcc3-128">Hallo DaemonSet maken met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="fdcc3-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="fdcc3-129">toosee die Hallo DaemonSet is gemaakt, worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="fdcc3-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="fdcc3-130">Uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="fdcc3-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="fdcc3-131">Nadat het Hallo-agents worden uitgevoerd, duurt het enkele minuten voor OMS tooingest en proces Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="fdcc3-132">Toegang tot bewakingsgegevens</span><span class="sxs-lookup"><span data-stu-id="fdcc3-132">Access monitoring data</span></span>

<span data-ttu-id="fdcc3-133">Weergeven en analyseren van Hallo OMS container bewakingsgegevens Hello [Container oplossing](../../log-analytics/log-analytics-containers.md) in Hallo OMS-portal of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="fdcc3-134">tooinstall hello Container oplossing met behulp van Hallo [OMS-portal](https://mms.microsoft.com), gaat u te**galerie met oplossingen**.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="fdcc3-135">Voeg vervolgens **Container oplossing**.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-135">Then add **Container Solution**.</span></span> <span data-ttu-id="fdcc3-136">Hallo Containers oplossing ook toevoegen van Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="fdcc3-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="fdcc3-137">In de OMS-portal hello, zoekt u naar een **Containers** tegel samenvatting op Hallo OMS-dashboard.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="fdcc3-138">Klik op de tegel Hallo voor meer informatie, met inbegrip van: container gebeurtenissen, fouten, status, inventaris van de installatiekopie en CPU- en geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="fdcc3-139">Voor meer gedetailleerde informatie op een rij op een tegel of voer een [logboek zoeken](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="fdcc3-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Containers dashboard in OMS-portal](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="fdcc3-141">Op deze manier in hello Azure-portal, gaat u te**logboekanalyse** en selecteer de Werkruimtenaam van uw.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="fdcc3-142">Hallo toosee **Containers** tegel samenvatting, klikt u op **oplossingen** > **Containers**.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="fdcc3-143">toosee, klikt u op de tegel Hallo.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="fdcc3-144">Zie Hallo [Azure Log Analytics-documentatie](../../log-analytics/index.md) voor gedetailleerde hulp bij het uitvoeren van query's en analyseren van bewakingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdcc3-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fdcc3-145">Next steps</span></span>

<span data-ttu-id="fdcc3-146">In deze zelfstudie maakt bewaakt u uw cluster Kubernetes met OMS.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="fdcc3-147">Taken aan de orde opgenomen:</span><span class="sxs-lookup"><span data-stu-id="fdcc3-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdcc3-148">OMS-werkruimte-instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="fdcc3-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="fdcc3-149">Instellen van OMS-agents op Hallo Kubernetes knooppunten</span><span class="sxs-lookup"><span data-stu-id="fdcc3-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="fdcc3-150">Toegang tot informatie over prestatiebewaking op Hallo OMS-portal of Azure-portal</span><span class="sxs-lookup"><span data-stu-id="fdcc3-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="fdcc3-151">Volg deze link toosee vooraf gemaakte scriptvoorbeelden voor Container Service.</span><span class="sxs-lookup"><span data-stu-id="fdcc3-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdcc3-152">Azure Container Service script-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="fdcc3-152">Azure Container Service script samples</span></span>](cli-samples.md)
