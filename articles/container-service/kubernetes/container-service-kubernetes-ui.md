---
title: aaaManage Azure Kubernetes cluster met de webgebruikersinterface | Microsoft Docs
description: Met behulp van Hallo Kubernetes-webgebruikersinterface in Azure Container Service
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="68b88-103">Met behulp van Hallo Kubernetes-webgebruikersinterface met Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="68b88-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68b88-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="68b88-104">Prerequisites</span></span>
<span data-ttu-id="68b88-105">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="68b88-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="68b88-106">Ook wordt ervan uitgegaan dat u hello Azure CLI 2.0 hebt en `kubectl` hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="68b88-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="68b88-107">U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="68b88-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="68b88-108">Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="68b88-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="68b88-109">U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="68b88-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="68b88-110">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="68b88-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="68b88-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="68b88-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="68b88-112">Verbinding maken met toohello webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="68b88-112">Connect toohello web UI</span></span>
<span data-ttu-id="68b88-113">U kunt Hallo Kubernetes webgebruikersinterface starten door te voeren:</span><span class="sxs-lookup"><span data-stu-id="68b88-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="68b88-114">Dit moet een browser geconfigureerd tootalk tooa beveiligde webproxy verbinding maken met uw lokale machine toohello Kubernetes webgebruikersinterface openen.</span><span class="sxs-lookup"><span data-stu-id="68b88-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="68b88-115">Maken en weergeven van een service</span><span class="sxs-lookup"><span data-stu-id="68b88-115">Create and expose a service</span></span>
1. <span data-ttu-id="68b88-116">Klik in het Hallo Kubernetes web UI op **maken** knop in het bovenste rechtervenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="68b88-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Kubernetes maken gebruikersinterface](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="68b88-118">Een dialoogvenster weergegeven waarin u kunt starten maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="68b88-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="68b88-119">Geef het Hallo-naam `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="68b88-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="68b88-120">Gebruik Hallo [ `nginx` container in Docker](https://hub.docker.com/_/nginx/) en drie replica's van deze webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="68b88-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Dialoogvenster maken Kubernetes schil](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="68b88-122">Onder **Service**, selecteer **externe** en voert u poort 80.</span><span class="sxs-lookup"><span data-stu-id="68b88-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="68b88-123">Deze instelling taakverdelingen verkeer toohello drie replica's.</span><span class="sxs-lookup"><span data-stu-id="68b88-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Dialoogvenster maken Kubernetes Service](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="68b88-125">Klik op **implementeren** toodeploy deze containers en -services.</span><span class="sxs-lookup"><span data-stu-id="68b88-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Kubernetes implementeren](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="68b88-127">Uw containers weergeven</span><span class="sxs-lookup"><span data-stu-id="68b88-127">View your containers</span></span>
<span data-ttu-id="68b88-128">Nadat u op **implementeren**, Hallo UI ziet u een weergave van uw service zoals deze implementeert:</span><span class="sxs-lookup"><span data-stu-id="68b88-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Kubernetes Status](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="68b88-130">Kunt u Hallo status van elk object Kubernetes in Hallo cirkel onder aan de linkerkant Hallo van de gebruikersinterface bekijken **gehele product**.</span><span class="sxs-lookup"><span data-stu-id="68b88-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="68b88-131">Als het een gedeeltelijk volledige cirkel, is nog steeds Hallo object implementeren.</span><span class="sxs-lookup"><span data-stu-id="68b88-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="68b88-132">Wanneer een object volledig is geïmplementeerd, wordt een groen vinkje weergegeven:</span><span class="sxs-lookup"><span data-stu-id="68b88-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes geïmplementeerd](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="68b88-134">Zodra u alles wordt uitgevoerd, klikt u op een van uw gehele product toosee details over het Hallo-webservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="68b88-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Kubernetes gehele product](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="68b88-136">In Hallo **gehele product** weergave ziet u informatie over het Hallo-containers in Hallo schil, evenals Hallo CPU en geheugenbronnen kost gebruikt door deze containers:</span><span class="sxs-lookup"><span data-stu-id="68b88-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Kubernetes Resources](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="68b88-138">Als u Hallo resources niet ziet, moet u mogelijk toowait een paar minuten voor Hallo gegevens toopropagate bewaking.</span><span class="sxs-lookup"><span data-stu-id="68b88-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="68b88-139">toosee hello logboeken voor de container, klik **logboeken bekijken**.</span><span class="sxs-lookup"><span data-stu-id="68b88-139">toosee hello logs for your container, click **View logs**.</span></span>

![Kubernetes Logboeken](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="68b88-141">Uw service weergeven</span><span class="sxs-lookup"><span data-stu-id="68b88-141">Viewing your service</span></span>
<span data-ttu-id="68b88-142">In aanvulling toorunning uw containers Hallo Kubernetes UI heeft gemaakt een externe `Service` die voorziet in een load balancer toobring verkeer toohello containers in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="68b88-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="68b88-143">Klik in het Hallo navigatiedeelvenster links op **Services** tooview alle services (er moet slechts één).</span><span class="sxs-lookup"><span data-stu-id="68b88-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Kubernetes Services](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="68b88-145">In deze weergave ziet u een extern eindpunt (IP-adres) tooyour-service is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="68b88-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="68b88-146">Als u op dat IP-adres, ziet u het Nginx-container die achter de load balancer.</span><span class="sxs-lookup"><span data-stu-id="68b88-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx weergeven](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="68b88-148">Uw service vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="68b88-148">Resizing your service</span></span>
<span data-ttu-id="68b88-149">In toevoeging tooviewing Hallo uw objecten in de gebruikersinterface, kunt u bewerken en bijwerken Hallo Kubernetes API-objecten.</span><span class="sxs-lookup"><span data-stu-id="68b88-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="68b88-150">Klik eerst **implementaties** in Hallo links navigatie deelvenster toosee Hallo implementatie voor uw service.</span><span class="sxs-lookup"><span data-stu-id="68b88-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="68b88-151">Wanneer u zich in die weergave, klikt u op Hallo replicaset en klik vervolgens op **bewerken** in de bovenste navigatiebalk Hallo:</span><span class="sxs-lookup"><span data-stu-id="68b88-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Kubernetes bewerken](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="68b88-153">Hallo bewerken `spec.replicas` veld toobe `2`, en klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="68b88-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="68b88-154">Dit zorgt ervoor dat het aantal replica's toodrop tootwo Hallo door een van uw gehele product te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="68b88-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

