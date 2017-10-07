---
title: een Azure Service Fabric-toepassing tooa partij Cluster aaaDeploy | Microsoft Docs
description: Meer informatie over hoe een toepassing tooa toodeploy partij Cluster.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="8aa02-103">Een toepassing tooa partij Cluster in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="8aa02-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="8aa02-104">Deze zelfstudie maakt deel uit van een reeks en laat u zien hoe toodeploy een Azure Service Fabric-toepassing tooa partij Cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa02-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="8aa02-105">In deel twee reeks Hallo zelfstudie leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="8aa02-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8aa02-106">Een toepassing tooa externe cluster met Visual Studio implementeren</span><span class="sxs-lookup"><span data-stu-id="8aa02-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="8aa02-107">Een toepassing verwijderen van een cluster met behulp van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8aa02-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="8aa02-108">In deze zelfstudie reeks leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="8aa02-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="8aa02-109">Een .NET-Service Fabric-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="8aa02-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="8aa02-110">Hallo toepassing tooa RAS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="8aa02-110">Deploy hello application tooa remote cluster</span></span>
> * [<span data-ttu-id="8aa02-111">CI/CD met behulp van Visual Studio Team Services configureren</span><span class="sxs-lookup"><span data-stu-id="8aa02-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="8aa02-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8aa02-112">Prerequisites</span></span>
<span data-ttu-id="8aa02-113">Voordat u deze zelfstudie begint:</span><span class="sxs-lookup"><span data-stu-id="8aa02-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="8aa02-114">Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="8aa02-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="8aa02-115">[Installeer Visual Studio 2017](https://www.visualstudio.com/) en installeer Hallo **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="8aa02-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="8aa02-116">Hallo Service Fabric SDK installeren</span><span class="sxs-lookup"><span data-stu-id="8aa02-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="8aa02-117">Hallo Voting voorbeeldtoepassing downloaden</span><span class="sxs-lookup"><span data-stu-id="8aa02-117">Download hello Voting sample application</span></span>
<span data-ttu-id="8aa02-118">Als u geen Hallo Voting voorbeeldtoepassing heeft bouwen [deel uitmaken van een van deze zelfstudie reeks](service-fabric-tutorial-create-dotnet-app.md), u kunt dit downloaden.</span><span class="sxs-lookup"><span data-stu-id="8aa02-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="8aa02-119">In een opdrachtvenster Hallo na de opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8aa02-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="8aa02-120">Een Cluster partij instellen</span><span class="sxs-lookup"><span data-stu-id="8aa02-120">Set up a Party Cluster</span></span>
<span data-ttu-id="8aa02-121">Partijen clusters zijn gratis, tijdelijke Service Fabric clusters gehost op Azure en uitgevoerd door Hallo Service Fabric-team waar iedereen toepassingen implementeren en meer informatie over het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="8aa02-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="8aa02-122">Gratis!</span><span class="sxs-lookup"><span data-stu-id="8aa02-122">For free!</span></span>

<span data-ttu-id="8aa02-123">tooget toegang tooa partij Cluster toothis site bladeren: http://aka.ms/tryservicefabric en volg Hallo instructies tooget RAS tooa-cluster.</span><span class="sxs-lookup"><span data-stu-id="8aa02-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="8aa02-124">U moet een Facebook of GitHub-account tooget toegang tooa partij Cluster.</span><span class="sxs-lookup"><span data-stu-id="8aa02-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8aa02-125">Partijen clusters zijn niet beveiligd, zodat uw toepassingen en gegevens die u in deze plaatsen mogelijk zichtbaar tooothers.</span><span class="sxs-lookup"><span data-stu-id="8aa02-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="8aa02-126">Alles wat u niet wilt dat anderen niet implementeren toosee.</span><span class="sxs-lookup"><span data-stu-id="8aa02-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="8aa02-127">Worden ervoor tooread via onze gebruiksvoorwaarden voor alle Hallo meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8aa02-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="8aa02-128">Hallo-luisterpoort configureren</span><span class="sxs-lookup"><span data-stu-id="8aa02-128">Configure hello listening port</span></span>
<span data-ttu-id="8aa02-129">Tijdens het Hallo VotingWeb front-end-service is gemaakt, Visual Studio een poort voor Hallo service toolisten willekeurig geselecteerd op.</span><span class="sxs-lookup"><span data-stu-id="8aa02-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="8aa02-130">Hallo VotingWeb-service fungeert als front-end voor deze toepassing hello en externe verkeer accepteert, dus laten we koppelt die service tooa vast en poort ook weten.</span><span class="sxs-lookup"><span data-stu-id="8aa02-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="8aa02-131">Open in Solution Explorer *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="8aa02-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="8aa02-132">Hallo zoeken **eindpunt** resource in Hallo **Resources** sectie en wijzig Hallo **poort** too80 waarde.</span><span class="sxs-lookup"><span data-stu-id="8aa02-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="8aa02-133">Hallo toepassings-URL-eigenschapwaarde in Hallo Voting project ook bijwerken zodat de juiste poort toohello van een webbrowser wordt geopend wanneer u fouten opspoort, druk op F5 '.</span><span class="sxs-lookup"><span data-stu-id="8aa02-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="8aa02-134">Klik in Solution Explorer, selecteer Hallo **Voting** project en update Hallo **toepassings-URL** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8aa02-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![De URL van toepassing](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="8aa02-136">Hallo app toohello Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="8aa02-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="8aa02-137">Nu dat de toepassing hello klaar is, kunt u deze toohello partij Cluster direct vanuit Visual Studio implementeren.</span><span class="sxs-lookup"><span data-stu-id="8aa02-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="8aa02-138">Met de rechtermuisknop op **Voting** Hallo in Solution Explorer en kiest u **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8aa02-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![Het dialoogvenster Publiceren](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="8aa02-140">Type in Hallo verbindingseindpunt Hallo partij Cluster in Hallo **verbindingseindpunt** veld en klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8aa02-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="8aa02-141">Zodra het Hallo-publiceren is voltooid, moet u kunnen toosend een aanvraag toohello toepassing via een browser.</span><span class="sxs-lookup"><span data-stu-id="8aa02-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="8aa02-142">Open uw voorkeurstijdzone browser en typt u Hallo clusteradres (Hallo verbindingseindpunt zonder poortinformatie Hallo - bijvoorbeeld win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8aa02-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="8aa02-143">U ziet nu Hallo hetzelfde resultaat als u hebt gezien wanneer Hallo toepassing lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8aa02-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![API-reactie van Cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="8aa02-145">Hallo-toepassing verwijderen van een cluster met behulp van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8aa02-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="8aa02-146">Service Fabric Explorer is een grafische interface tooexplore en beheren van toepassingen in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8aa02-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="8aa02-147">tooremove hello toepassing hello partij Cluster:</span><span class="sxs-lookup"><span data-stu-id="8aa02-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="8aa02-148">Blader toohello Service Fabric Explorer via Hallo koppeling door Hallo partij Cluster aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="8aa02-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="8aa02-149">Bijvoorbeeld: http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="8aa02-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="8aa02-150">Navigeer in Service Fabric Explorer toohello **fabric://Voting** knooppunt in de treeview Hallo aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="8aa02-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="8aa02-151">Klik op Hallo **actie** knop in het rechterdeelvenster Hallo **Essentials** deelvenster en kies **toepassing verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="8aa02-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="8aa02-152">Bevestig verwijderen Hallo toepassingsexemplaar, waardoor er Hallo-exemplaar van onze toepassing in Hallo cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8aa02-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![Verwijderen van de toepassing in Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="8aa02-154">Type van de toepassing hello verwijderen uit een cluster met behulp van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8aa02-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="8aa02-155">Toepassingen geïmplementeerd als de soorten toepassingen in een Service Fabric-cluster, waardoor u toohave meerdere exemplaren en versies van Hallo-toepassing uitgevoerd binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8aa02-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="8aa02-156">Nadat de hebt verwijderd met een exemplaar van onze toepassing hello, kunnen we ook Hallo type, toocomplete Hallo opschoning van Hallo implementatie verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8aa02-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="8aa02-157">Zie voor meer informatie over Hallo toepassingsmodel in Service Fabric [Model van een toepassing in Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="8aa02-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="8aa02-158">Navigeer toohello **VotingType** knooppunt in Hallo treeview.</span><span class="sxs-lookup"><span data-stu-id="8aa02-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="8aa02-159">Klik op Hallo **actie** knop in het rechterdeelvenster Hallo **Essentials** deelvenster en kies **Type verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="8aa02-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="8aa02-160">Bevestig de inrichting Hallo toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="8aa02-160">Confirm unprovisioning hello application type.</span></span>

![Inrichting toepassingstype in Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="8aa02-162">Hiermee is Hallo zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8aa02-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8aa02-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8aa02-163">Next steps</span></span>
<span data-ttu-id="8aa02-164">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="8aa02-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8aa02-165">Een toepassing tooa externe cluster met Visual Studio implementeren</span><span class="sxs-lookup"><span data-stu-id="8aa02-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="8aa02-166">Een toepassing verwijderen van een cluster met behulp van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8aa02-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="8aa02-167">Geavanceerde toohello volgende zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="8aa02-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8aa02-168">Stel doorlopende integratie met behulp van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="8aa02-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)