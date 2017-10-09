---
title: aaaManage Azure Service Fabric-toepassingen met Azure Service Fabric CLI
description: Meer informatie over hoe toepassingen toodeploy en verwijderen van een Azure Service Fabric-cluster met behulp van Azure Service Fabric CLI
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="86c4d-103">Een Azure Service Fabric-toepassing te beheren met behulp van Azure Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="86c4d-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="86c4d-104">Meer informatie over hoe toocreate en delete-toepassingen die worden uitgevoerd in een Azure Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="86c4d-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86c4d-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="86c4d-105">Prerequisites</span></span>

* <span data-ttu-id="86c4d-106">Service Fabric CLI installeren.</span><span class="sxs-lookup"><span data-stu-id="86c4d-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="86c4d-107">Selecteer vervolgens uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="86c4d-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="86c4d-108">Zie voor meer informatie [aan de slag met Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="86c4d-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="86c4d-109">Een Service Fabric-toepassing pakket gereed toobe geïmplementeerd hebben.</span><span class="sxs-lookup"><span data-stu-id="86c4d-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="86c4d-110">Lees voor meer informatie over het tooauthor en een toepassing, pakket over Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="86c4d-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="86c4d-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="86c4d-111">Overview</span></span>

<span data-ttu-id="86c4d-112">een nieuwe toepassing toodeploy deze stappen hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="86c4d-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="86c4d-113">Upload een pakket toohello Service Fabric installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="86c4d-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="86c4d-114">Een toepassingstype inrichten.</span><span class="sxs-lookup"><span data-stu-id="86c4d-114">Provision an application type.</span></span>
3. <span data-ttu-id="86c4d-115">Geef op en maak een toepassing.</span><span class="sxs-lookup"><span data-stu-id="86c4d-115">Specify and create an application.</span></span>
4. <span data-ttu-id="86c4d-116">Geef en services maken.</span><span class="sxs-lookup"><span data-stu-id="86c4d-116">Specify and create services.</span></span>

<span data-ttu-id="86c4d-117">een bestaande toepassing tooremove deze stappen hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="86c4d-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="86c4d-118">Hallo-toepassing verwijderen.</span><span class="sxs-lookup"><span data-stu-id="86c4d-118">Delete hello application.</span></span>
2. <span data-ttu-id="86c4d-119">Inrichting verwijderen Hallo gekoppelde toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="86c4d-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="86c4d-120">Hallo image store inhoud verwijderen.</span><span class="sxs-lookup"><span data-stu-id="86c4d-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="86c4d-121">Een nieuwe toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="86c4d-121">Deploy a new application</span></span>

<span data-ttu-id="86c4d-122">toodeploy een nieuwe toepassing voltooid Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="86c4d-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="86c4d-123">Een nieuwe toepassing toohello installatiekopie pakketopslag uploaden</span><span class="sxs-lookup"><span data-stu-id="86c4d-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="86c4d-124">Voordat u een toepassing maakt, uploadt u Hallo pakket toohello Service Fabric installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="86c4d-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="86c4d-125">Bijvoorbeeld, als uw toepassingspakket is in Hallo `app_package_dir` directory, gebruik Hallo opdrachten tooupload Hallo directory te volgen:</span><span class="sxs-lookup"><span data-stu-id="86c4d-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="86c4d-126">Voor grote toepassingpakketten, kunt u Hallo `--show-progress` optie toodisplay Hallo voortgang van Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="86c4d-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="86c4d-127">Hallo-toepassingstype inrichten</span><span class="sxs-lookup"><span data-stu-id="86c4d-127">Provision hello application type</span></span>

<span data-ttu-id="86c4d-128">Wanneer Hallo uploaden is voltooid, inrichten Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="86c4d-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="86c4d-129">tooprovision hello toepassing gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="86c4d-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="86c4d-130">waarde voor Hallo `application-type-build-path` Hallo naam is van Hallo directory waar u uw toepassingspakket geüpload.</span><span class="sxs-lookup"><span data-stu-id="86c4d-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="86c4d-131">Maak een toepassing van een toepassingstype</span><span class="sxs-lookup"><span data-stu-id="86c4d-131">Create an application from an application type</span></span>

<span data-ttu-id="86c4d-132">Nadat u de toepassing hello inricht, na de opdracht tooname hello gebruiken en uw toepassing maken:</span><span class="sxs-lookup"><span data-stu-id="86c4d-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="86c4d-133">`app-name`wilt u toouse voor toepassingsexemplaar Hallo Hallo-naam is.</span><span class="sxs-lookup"><span data-stu-id="86c4d-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="86c4d-134">Aanvullende parameters kunt u krijgen via het eerder ingerichte toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="86c4d-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="86c4d-135">Hallo toepassingsnaam moet beginnen met Hallo voorvoegsel `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="86c4d-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="86c4d-136">Services voor de nieuwe toepassing hello maken</span><span class="sxs-lookup"><span data-stu-id="86c4d-136">Create services for hello new application</span></span>

<span data-ttu-id="86c4d-137">Nadat u een toepassing hebt gemaakt, kunt u services maken van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="86c4d-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="86c4d-138">In Hallo voorbeeld te volgen, maken we een nieuwe service staatloze van onze toepassing.</span><span class="sxs-lookup"><span data-stu-id="86c4d-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="86c4d-139">Hallo-services die u van een toepassing maken kunt worden gedefinieerd in een servicemanifest in Hallo eerder ingerichte toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="86c4d-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="86c4d-140">Controleer of de implementatie van de toepassing en status</span><span class="sxs-lookup"><span data-stu-id="86c4d-140">Verify application deployment and health</span></span>

<span data-ttu-id="86c4d-141">tooverify alles in orde is, gebruikt u Hallo health opdrachten te volgen:</span><span class="sxs-lookup"><span data-stu-id="86c4d-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="86c4d-142">tooverify Hallo-service is in orde, gebruikt u dezelfde opdrachten tooretrieve Hallo status van zowel Hallo-service en de toepassing:</span><span class="sxs-lookup"><span data-stu-id="86c4d-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="86c4d-143">In orde services en toepassingen hebben een `HealthState` waarde van `Ok`.</span><span class="sxs-lookup"><span data-stu-id="86c4d-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="86c4d-144">Een bestaande toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="86c4d-144">Remove an existing application</span></span>

<span data-ttu-id="86c4d-145">tooremove een toepassing, volledige Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="86c4d-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="86c4d-146">Hallo-toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="86c4d-146">Delete hello application</span></span>

<span data-ttu-id="86c4d-147">toodelete hello toepassing gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="86c4d-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="86c4d-148">Type van de toepassing hello inrichting</span><span class="sxs-lookup"><span data-stu-id="86c4d-148">Unprovision hello application type</span></span>

<span data-ttu-id="86c4d-149">Nadat u de toepassing hello verwijdert, kunt u het toepassingstype Hallo inrichting als u niet langer.</span><span class="sxs-lookup"><span data-stu-id="86c4d-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="86c4d-150">toounprovision toepassingstype hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="86c4d-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="86c4d-151">Hallo type naam en type versie moet overeenkomen met Hallo naam en versie Hallo eerder ingerichte toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="86c4d-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="86c4d-152">Hallo-toepassingspakket wissen</span><span class="sxs-lookup"><span data-stu-id="86c4d-152">Delete hello application package</span></span>

<span data-ttu-id="86c4d-153">Nadat u hebt het toepassingstype Hallo inrichting, kunt u Hallo toepassingspakket verwijderen uit de installatiekopieopslag Hallo als u deze niet langer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="86c4d-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="86c4d-154">Verwijderen van toepassingspakketten helpt Maak schijfruimte vrij.</span><span class="sxs-lookup"><span data-stu-id="86c4d-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="86c4d-155">Hallo toepassingspakket toodelete uit de installatiekopieopslag hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="86c4d-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="86c4d-156">`content-path`moet de naam Hallo van Hallo-directory die u tijdens het maken van de toepassing hello geüpload.</span><span class="sxs-lookup"><span data-stu-id="86c4d-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="86c4d-157">Toepassing bijwerken</span><span class="sxs-lookup"><span data-stu-id="86c4d-157">Upgrade application</span></span>

<span data-ttu-id="86c4d-158">Na het maken van uw toepassing, kunt u herhalen Hallo dezelfde reeks stappen tooprovision een tweede versie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="86c4d-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="86c4d-159">Vervolgens kunt u met de upgrade van een Service Fabric-toepassing toorunning Hallo tweede versie van de toepassing hello overstappen.</span><span class="sxs-lookup"><span data-stu-id="86c4d-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="86c4d-160">Zie voor meer informatie Hallo-documentatie op [Service Fabric-toepassingsupgrades](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="86c4d-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="86c4d-161">tooperform een upgrade eerste inrichten Hallo volgende versie van het gebruik van de toepassing hello Hallo dezelfde opdrachten als voorheen:</span><span class="sxs-lookup"><span data-stu-id="86c4d-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="86c4d-162">U wordt aangeraden en vervolgens een bewaakte Automatische upgrade tooperform Hallo-upgrade starten door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="86c4d-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="86c4d-163">Upgrades overschrijven bestaande parameters met welke set is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="86c4d-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="86c4d-164">Parameters voor de toepassing moeten worden doorgegeven als argumenten toohello opdracht upgraden, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="86c4d-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="86c4d-165">Parameters voor de toepassing moeten worden gecodeerd als een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="86c4d-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="86c4d-166">tooretrieve parameters eerder hebt opgegeven, kunt u Hallo `sfctl application info` opdracht.</span><span class="sxs-lookup"><span data-stu-id="86c4d-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="86c4d-167">Wanneer u een upgrade van de toepassing wordt uitgevoerd, Hallo status kan worden opgehaald met de `sfctl application upgrade-status` opdracht.</span><span class="sxs-lookup"><span data-stu-id="86c4d-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="86c4d-168">Ten slotte, als een upgrade uitgevoerd wordt en toobe geannuleerd moet, kunt u Hallo `sfctl application upgrade-rollback` tooroll terug Hallo upgrade.</span><span class="sxs-lookup"><span data-stu-id="86c4d-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c4d-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86c4d-169">Next steps</span></span>

* [<span data-ttu-id="86c4d-170">Basisprincipes van service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="86c4d-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="86c4d-171">Aan de slag met Service Fabric op Linux</span><span class="sxs-lookup"><span data-stu-id="86c4d-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="86c4d-172">Starten van de upgrade van een Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="86c4d-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
