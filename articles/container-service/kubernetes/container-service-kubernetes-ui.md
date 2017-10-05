---
title: Beheer van Azure Kubernetes clusters met de webgebruikersinterface | Microsoft Docs
description: Met behulp van de webgebruikersinterface Kubernetes in Azure Container Service
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
ms.openlocfilehash: e31f90d61fc61f17582372fe9f491a1e21f628b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="d8ed5-103">Met behulp van de webgebruikersinterface Kubernetes met Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d8ed5-103">Using the Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8ed5-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d8ed5-104">Prerequisites</span></span>
<span data-ttu-id="d8ed5-105">In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d8ed5-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="d8ed5-106">Ook wordt ervan uitgegaan dat u de Azure CLI 2.0 hebt en `kubectl` hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-106">It also assumes that you have the Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="d8ed5-107">U kunt testen, hebt u de `az` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="d8ed5-108">Als u hebt de `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="d8ed5-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="d8ed5-109">U kunt testen, hebt u de `kubectl` hulpprogramma is geïnstalleerd door te voeren:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="d8ed5-110">Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="d8ed5-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d8ed5-111">Overview</span></span>

### <a name="connect-to-the-web-ui"></a><span data-ttu-id="d8ed5-112">Verbinding maken met de webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="d8ed5-112">Connect to the web UI</span></span>
<span data-ttu-id="d8ed5-113">U kunt de webgebruikersinterface Kubernetes starten door te voeren:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-113">You can launch the Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="d8ed5-114">Dit moet een webbrowser die is geconfigureerd om te communiceren met een beveiligde proxy uw lokale computer verbinden met de webgebruikersinterface Kubernetes openen.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-114">This should open a web browser configured to talk to a secure proxy connecting your local machine to the Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="d8ed5-115">Maken en weergeven van een service</span><span class="sxs-lookup"><span data-stu-id="d8ed5-115">Create and expose a service</span></span>
1. <span data-ttu-id="d8ed5-116">Klik in het Kubernetes web UI op **maken** knop in het bovenste rechtervenster.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-116">In the Kubernetes web UI, click **Create** button in the upper right window.</span></span>

    ![Kubernetes maken gebruikersinterface](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="d8ed5-118">Een dialoogvenster weergegeven waarin u kunt starten maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="d8ed5-119">Geef deze de naam `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-119">Give it the name `hello-nginx`.</span></span> <span data-ttu-id="d8ed5-120">Gebruik de [ `nginx` container in Docker](https://hub.docker.com/_/nginx/) en drie replica's van deze webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-120">Use the [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Dialoogvenster maken Kubernetes schil](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="d8ed5-122">Onder **Service**, selecteer **externe** en voert u poort 80.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="d8ed5-123">Deze instelling taakverdelingen verkeer naar de drie replica's.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-123">This setting load-balances traffic to the three replicas.</span></span>

    ![Dialoogvenster maken Kubernetes Service](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="d8ed5-125">Klik op **implementeren** voor het implementeren van deze containers en -services.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-125">Click **Deploy** to deploy these containers and services.</span></span>

    ![Kubernetes implementeren](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="d8ed5-127">Uw containers weergeven</span><span class="sxs-lookup"><span data-stu-id="d8ed5-127">View your containers</span></span>
<span data-ttu-id="d8ed5-128">Nadat u op **implementeren**, ziet u de gebruikersinterface een weergave van uw service omdat het wordt geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-128">After you click **Deploy**, the UI shows a view of your service as it deploys:</span></span>

![Kubernetes Status](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="d8ed5-130">U kunt de status van elk object Kubernetes in de cirkel onder aan de linkerkant van de gebruikersinterface zien **gehele product**.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-130">You can see the status of each Kubernetes object in the circle on the left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="d8ed5-131">Als het een gedeeltelijk volledige cirkel, klikt u vervolgens implementeert het object nog steeds.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-131">If it is a partially full circle, then the object is still deploying.</span></span> <span data-ttu-id="d8ed5-132">Wanneer een object volledig is geïmplementeerd, wordt een groen vinkje weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes geïmplementeerd](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="d8ed5-134">Zodra u alles wordt uitgevoerd, klikt u op een van uw gehele product voor informatie over de webservice.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-134">Once everything is running, click one of your pods to see details about the running web service.</span></span>

![Kubernetes gehele product](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="d8ed5-136">In de **gehele product** weergave ziet u informatie over de containers in schil, evenals de CPU en geheugen resources gebruikt door deze containers:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-136">In the **Pods** view, you can see information about the containers in the pod as well as the CPU and memory resources used by those containers:</span></span>

![Kubernetes Resources](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="d8ed5-138">Als u de resources niet ziet, moet u wellicht wacht een paar minuten voordat de bewakingsgegevens worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-138">If you don't see the resources, you may need to wait a few minutes for the monitoring data to propagate.</span></span>

<span data-ttu-id="d8ed5-139">Klik op een overzicht van de logboeken voor de container **logboeken bekijken**.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-139">To see the logs for your container, click **View logs**.</span></span>

![Kubernetes Logboeken](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="d8ed5-141">Uw service weergeven</span><span class="sxs-lookup"><span data-stu-id="d8ed5-141">Viewing your service</span></span>
<span data-ttu-id="d8ed5-142">De UI Kubernetes gecreëerd naast uw containers wordt uitgevoerd, een externe `Service` die voorziet in een load balancer om verkeer naar de containers in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-142">In addition to running your containers, the Kubernetes UI has created an external `Service` which provisions a load balancer to bring traffic to the containers in your cluster.</span></span>

<span data-ttu-id="d8ed5-143">Klik in het navigatiedeelvenster links op **Services** om weer te geven van alle services (er moet slechts één).</span><span class="sxs-lookup"><span data-stu-id="d8ed5-143">In the left navigation pane, click **Services** to view all services (there should be only one).</span></span>

![Kubernetes Services](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="d8ed5-145">In deze weergave ziet u een extern eindpunt (IP-adres) dat is toegewezen aan uw service.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-145">In that view, you should see an external endpoint (IP address) that has been allocated to your service.</span></span>
<span data-ttu-id="d8ed5-146">Als u op dat IP-adres, ziet u het Nginx-container die achter de load balancer.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx weergeven](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="d8ed5-148">Uw service vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="d8ed5-148">Resizing your service</span></span>
<span data-ttu-id="d8ed5-149">U kunt niet alleen uw objecten in de gebruikersinterface weergeven, bewerken en de objecten Kubernetes API bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-149">In addition to viewing your objects in the UI, you can edit and update the Kubernetes API objects.</span></span>

<span data-ttu-id="d8ed5-150">Klik eerst **implementaties** in het navigatiedeelvenster links om te zien van de implementatie voor uw service.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-150">First, click **Deployments** in the left navigation pane to see the deployment for your service.</span></span>

<span data-ttu-id="d8ed5-151">Wanneer u zich in die weergave, klikt u op de replicaset en klik vervolgens op **bewerken** in de bovenste navigatiebalk:</span><span class="sxs-lookup"><span data-stu-id="d8ed5-151">Once you are in that view, click on the replica set, and then click **Edit** in the upper navigation bar:</span></span>

![Kubernetes bewerken](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="d8ed5-153">Bewerk de `spec.replicas` veld `2`, en klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-153">Edit the `spec.replicas` field to be `2`, and click **Update**.</span></span>

<span data-ttu-id="d8ed5-154">Dit zorgt ervoor dat het aantal replica's op twee door een van uw gehele product te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d8ed5-154">This causes the number of replicas to drop to two by deleting one of your pods.</span></span>

 

