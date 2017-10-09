---
title: aaaManage uw toepassingen in Visual Studio | Microsoft Docs
description: Visual Studio toocreate gebruiken, ontwikkelen, pakket, implementeren en foutopsporing van uw Service Fabric-toepassingen en services.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="6d74c-103">Gebruik Visual Studio toosimplify schrijven en beheren van uw Service Fabric-toepassingen</span><span class="sxs-lookup"><span data-stu-id="6d74c-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="6d74c-104">U kunt uw Azure Service Fabric-toepassingen en services met Visual Studio kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="6d74c-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="6d74c-105">Zodra u hebt [uw ontwikkelomgeving instellen](service-fabric-get-started.md), gebruikt u Visual Studio toocreate Service Fabric-toepassingen, services of pakket, register toevoegen en toepassingen implementeren in uw lokaal ontwikkelcluster.</span><span class="sxs-lookup"><span data-stu-id="6d74c-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="6d74c-106">Service Fabric-toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="6d74c-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="6d74c-107">Standaard combineert een toepassing implementeren Hallo stappen te volgen in één bewerking:</span><span class="sxs-lookup"><span data-stu-id="6d74c-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="6d74c-108">Hallo-toepassingspakket maken</span><span class="sxs-lookup"><span data-stu-id="6d74c-108">Creating hello application package</span></span>
2. <span data-ttu-id="6d74c-109">Hallo pakket toohello installatiekopie toepassingsarchief uploaden</span><span class="sxs-lookup"><span data-stu-id="6d74c-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="6d74c-110">Type van de toepassing hello registreren</span><span class="sxs-lookup"><span data-stu-id="6d74c-110">Registering hello application type</span></span>
4. <span data-ttu-id="6d74c-111">Als u een actieve toepassingsexemplaren</span><span class="sxs-lookup"><span data-stu-id="6d74c-111">Removing any running application instances</span></span>
5. <span data-ttu-id="6d74c-112">Maken van een toepassingsexemplaar</span><span class="sxs-lookup"><span data-stu-id="6d74c-112">Creating an application instance</span></span>

<span data-ttu-id="6d74c-113">In Visual Studio, drukt u op **F5** uw toepassing implementeert en Hallo foutopsporingsprogramma tooall toepassingsexemplaren koppelen.</span><span class="sxs-lookup"><span data-stu-id="6d74c-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="6d74c-114">U kunt **Ctrl + F5** toodeploy een toepassing zonder foutopsporing, of u kunt publiceren tooa lokale of externe-cluster met behulp van Hallo publicatieprofiel.</span><span class="sxs-lookup"><span data-stu-id="6d74c-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="6d74c-115">Zie voor meer informatie [publiceren van een externe toepassing tooa-cluster met behulp van Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6d74c-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="6d74c-116">De foutopsporingsmodus toepassing</span><span class="sxs-lookup"><span data-stu-id="6d74c-116">Application Debug Mode</span></span>
<span data-ttu-id="6d74c-117">Visual Studio bieden een eigenschap genaamd **toepassing foutopsporingsmodus**, die bepaalt hoe u wilt dat Visual Studios toohandle toepassingsimplementatie als onderdeel van het opsporen van fouten.</span><span class="sxs-lookup"><span data-stu-id="6d74c-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="6d74c-118">tooset hello toepassing foutopsporingsmodus eigenschap</span><span class="sxs-lookup"><span data-stu-id="6d74c-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="6d74c-119">Op Hallo Service Fabric-toepassing van het project (*.sfproj) snelmenu kiezen **eigenschappen** (of drukt u op Hallo **F4** sleutel).</span><span class="sxs-lookup"><span data-stu-id="6d74c-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="6d74c-120">In Hallo **eigenschappen** venster, set Hallo **toepassing foutopsporingsmodus** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6d74c-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Toepassing foutopsporing modus eigenschap instellen][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="6d74c-122">Toepassing Foutopsporingsmodi</span><span class="sxs-lookup"><span data-stu-id="6d74c-122">Application Debug Modes</span></span>

1. <span data-ttu-id="6d74c-123">**Vernieuwen van de toepassing** deze modus kunt u tooquickly wijzigen en fouten opsporen in uw code en ondersteunt het bewerken van statische webbestanden tijdens het opsporen van fouten.</span><span class="sxs-lookup"><span data-stu-id="6d74c-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="6d74c-124">Deze modus werkt alleen als uw lokaal ontwikkelcluster in [modus 1-Node](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="6d74c-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="6d74c-125">**Toepassing verwijderen** oorzaken Hallo toepassing toobe verwijderd wanneer Hallo foutopsporingssessie wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="6d74c-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="6d74c-126">**Automatische Upgrade** toepassing hello toorun blijft wanneer Hallo debug-sessie wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="6d74c-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="6d74c-127">Hallo wordt volgende foutopsporingssessie behandeld Hallo implementatie een upgrade.</span><span class="sxs-lookup"><span data-stu-id="6d74c-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="6d74c-128">Hallo-upgradeproces behoudt alle gegevens die u hebt ingevoerd in een vorige foutopsporingssessie.</span><span class="sxs-lookup"><span data-stu-id="6d74c-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="6d74c-129">**Toepassing houden** eindigt fouten opsporen in Hallo toepassing houdt in Hallo cluster wanneer hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6d74c-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="6d74c-130">Aan Hallo begin Hallo volgende foutopsporingssessie, worden Hallo toepassing verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6d74c-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="6d74c-131">Voor **automatische Upgrade** gegevens blijven behouden door toe te passen Hallo toepassing upgrade mogelijkheden van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d74c-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="6d74c-132">Zie voor meer informatie over het upgraden van toepassingen en hoe u een upgrade kunt uitvoeren in een omgeving met echte [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="6d74c-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="6d74c-133">Een service tooyour Service Fabric-toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d74c-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="6d74c-134">U kunt nieuwe services tooyour toepassing tooextend functionaliteit ervan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d74c-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="6d74c-135">tooensure dat Hallo-service wordt opgenomen in het toepassingspakket toevoegen Hallo-service via Hallo **nieuwe Fabric-Service...**  menu-item.</span><span class="sxs-lookup"><span data-stu-id="6d74c-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Een nieuwe Service Fabric-service toevoegen][newservice]

<span data-ttu-id="6d74c-137">Selecteer een Service Fabric-project type tooadd tooyour-toepassing en geef een naam voor het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6d74c-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="6d74c-138">Zie [kiezen een framework voor uw service](service-fabric-choose-framework.md) toohelp u besluit welke service type toouse.</span><span class="sxs-lookup"><span data-stu-id="6d74c-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Een Service Fabric-service-project type tooadd tooyour toepassing selecteren][addserviceproject]

<span data-ttu-id="6d74c-140">de nieuwe service Hello wordt toegevoegd tooyour oplossing en bestaande toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="6d74c-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="6d74c-141">Hallo Serviceverwijzingen en een standaard service-exemplaar wordt toegevoegd toohello toepassingsmanifest, waardoor Hallo service toobe gemaakt en gestart Hallo volgende keer dat u de toepassing hello implementeren.</span><span class="sxs-lookup"><span data-stu-id="6d74c-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![de nieuwe service Hallo is tooyour toepassingsmanifest toegevoegd][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="6d74c-143">Uw toepassing Service Fabric-pakket</span><span class="sxs-lookup"><span data-stu-id="6d74c-143">Package your Service Fabric application</span></span>
<span data-ttu-id="6d74c-144">toodeploy hello toepassing en de services tooa-cluster, moet u toocreate toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="6d74c-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="6d74c-145">Hallo pakket ordent toepassingsmanifest hello, service manifesten en andere benodigde bestanden in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="6d74c-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="6d74c-146">Visual Studio instellen en beheren van Hallo-pakket in de map Hallo toepassing van het project, in Hallo 'pkg' directory.</span><span class="sxs-lookup"><span data-stu-id="6d74c-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="6d74c-147">Te klikken op **pakket** van Hallo **toepassing** contextmenu maakt of updates Hallo toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="6d74c-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="6d74c-148">Verwijderen van toepassingen en toepassingstypen met Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="6d74c-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="6d74c-149">U kunt basiscluster beheerbewerkingen uitvoeren vanuit Visual Studio gebruikt Cloud Explorer, die u vanuit Hallo starten kunt **weergave** menu.</span><span class="sxs-lookup"><span data-stu-id="6d74c-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="6d74c-150">U kunt bijvoorbeeld verwijderen van toepassingen en inrichting van toepassingstypen op lokale of externe clusters.</span><span class="sxs-lookup"><span data-stu-id="6d74c-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Een toepassing verwijderen][removeapplication]

> [!TIP]
> <span data-ttu-id="6d74c-152">Zie voor uitgebreidere cluster beheerfunctionaliteit, [uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6d74c-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6d74c-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d74c-153">Next steps</span></span>
* [<span data-ttu-id="6d74c-154">Service Fabric-toepassingsmodel</span><span class="sxs-lookup"><span data-stu-id="6d74c-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="6d74c-155">Implementatie van service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="6d74c-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="6d74c-156">Parameters voor de toepassing voor omgevingen met meerdere beheren</span><span class="sxs-lookup"><span data-stu-id="6d74c-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="6d74c-157">Foutopsporing van uw Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="6d74c-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="6d74c-158">Uw cluster visualiseren met behulp van Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="6d74c-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png