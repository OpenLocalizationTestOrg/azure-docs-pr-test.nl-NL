---
title: aaaManage Azure Service Fabric-toepassingen met Azure CLI 2.0
description: Meer informatie over hoe toepassingen toodeploy en verwijderen van een Azure Service Fabric-cluster met behulp van Azure CLI 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="a80d2-103">Een Azure Service Fabric-toepassing te beheren met behulp van Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a80d2-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="a80d2-104">Meer informatie over hoe toocreate en delete-toepassingen die worden uitgevoerd in een Azure Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="a80d2-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a80d2-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a80d2-105">Prerequisites</span></span>

* <span data-ttu-id="a80d2-106">Installeer Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a80d2-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="a80d2-107">Selecteer vervolgens uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="a80d2-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="a80d2-108">Zie voor meer informatie [aan de slag met Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="a80d2-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="a80d2-109">Een Service Fabric-toepassing pakket gereed toobe geïmplementeerd hebben.</span><span class="sxs-lookup"><span data-stu-id="a80d2-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="a80d2-110">Lees voor meer informatie over het tooauthor en een toepassing, pakket over Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="a80d2-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a80d2-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a80d2-111">Overview</span></span>

<span data-ttu-id="a80d2-112">een nieuwe toepassing toodeploy deze stappen hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a80d2-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="a80d2-113">Upload een pakket toohello Service Fabric installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="a80d2-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="a80d2-114">Een toepassingstype inrichten.</span><span class="sxs-lookup"><span data-stu-id="a80d2-114">Provision an application type.</span></span>
3. <span data-ttu-id="a80d2-115">Geef op en maak een toepassing.</span><span class="sxs-lookup"><span data-stu-id="a80d2-115">Specify and create an application.</span></span>
4. <span data-ttu-id="a80d2-116">Geef en services maken.</span><span class="sxs-lookup"><span data-stu-id="a80d2-116">Specify and create services.</span></span>

<span data-ttu-id="a80d2-117">een bestaande toepassing tooremove deze stappen hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a80d2-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="a80d2-118">Hallo-toepassing verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a80d2-118">Delete hello application.</span></span>
2. <span data-ttu-id="a80d2-119">Inrichting verwijderen Hallo gekoppelde toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="a80d2-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="a80d2-120">Hallo image store inhoud verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a80d2-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="a80d2-121">Een nieuwe toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="a80d2-121">Deploy a new application</span></span>

<span data-ttu-id="a80d2-122">toodeploy een nieuwe toepassing voltooid Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="a80d2-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="a80d2-123">Een nieuwe toepassing toohello installatiekopie pakketopslag uploaden</span><span class="sxs-lookup"><span data-stu-id="a80d2-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="a80d2-124">Voordat u een toepassing maakt, uploadt u Hallo pakket toohello Service Fabric installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="a80d2-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="a80d2-125">Bijvoorbeeld, als uw toepassingspakket is in Hallo `app_package_dir` directory, gebruik Hallo opdrachten tooupload Hallo directory te volgen:</span><span class="sxs-lookup"><span data-stu-id="a80d2-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="a80d2-126">Voor grote toepassingpakketten, kunt u Hallo `--show-progress` optie toodisplay Hallo voortgang van Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="a80d2-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="a80d2-127">Hallo-toepassingstype inrichten</span><span class="sxs-lookup"><span data-stu-id="a80d2-127">Provision hello application type</span></span>

<span data-ttu-id="a80d2-128">Wanneer Hallo uploaden is voltooid, inrichten Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a80d2-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="a80d2-129">tooprovision hello toepassing gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a80d2-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="a80d2-130">waarde voor Hallo `application-type-build-path` Hallo naam is van Hallo directory waar u uw toepassingspakket geüpload.</span><span class="sxs-lookup"><span data-stu-id="a80d2-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="a80d2-131">Maak een toepassing van een toepassingstype</span><span class="sxs-lookup"><span data-stu-id="a80d2-131">Create an application from an application type</span></span>

<span data-ttu-id="a80d2-132">Nadat u de toepassing hello inricht, na de opdracht tooname hello gebruiken en uw toepassing maken:</span><span class="sxs-lookup"><span data-stu-id="a80d2-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="a80d2-133">`app-name`wilt u toouse voor toepassingsexemplaar Hallo Hallo-naam is.</span><span class="sxs-lookup"><span data-stu-id="a80d2-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="a80d2-134">Aanvullende parameters kunt u krijgen via Hallo eerder ingerichte toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="a80d2-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="a80d2-135">Hallo toepassingsnaam moet beginnen met Hallo voorvoegsel `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="a80d2-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="a80d2-136">Services voor de nieuwe toepassing hello maken</span><span class="sxs-lookup"><span data-stu-id="a80d2-136">Create services for hello new application</span></span>

<span data-ttu-id="a80d2-137">Nadat u een toepassing hebt gemaakt, kunt u services maken van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="a80d2-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="a80d2-138">In Hallo voorbeeld te volgen, maken we een nieuwe service staatloze van onze toepassing.</span><span class="sxs-lookup"><span data-stu-id="a80d2-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="a80d2-139">Hallo-services die u van een toepassing maken kunt worden gedefinieerd in een servicemanifest in Hallo eerder ingerichte toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="a80d2-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="a80d2-140">Controleer of de implementatie van de toepassing en status</span><span class="sxs-lookup"><span data-stu-id="a80d2-140">Verify application deployment and health</span></span>

<span data-ttu-id="a80d2-141">tooverify dat een toepassing en service zijn geïmplementeerd, controleert u Hallo-toepassing en service worden vermeld:</span><span class="sxs-lookup"><span data-stu-id="a80d2-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="a80d2-142">Hallo-service is in orde, tooverify vergelijkbare opdrachten tooretrieve Hallo status van zowel Hallo-service en toepassing hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a80d2-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="a80d2-143">In orde services en toepassingen hebben een `HealthState` waarde van `Ok`.</span><span class="sxs-lookup"><span data-stu-id="a80d2-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="a80d2-144">Een bestaande toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="a80d2-144">Remove an existing application</span></span>

<span data-ttu-id="a80d2-145">tooremove een toepassing, volledige Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="a80d2-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="a80d2-146">Hallo-toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="a80d2-146">Delete hello application</span></span>

<span data-ttu-id="a80d2-147">toodelete hello toepassing gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a80d2-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="a80d2-148">Type van de toepassing hello inrichting</span><span class="sxs-lookup"><span data-stu-id="a80d2-148">Unprovision hello application type</span></span>

<span data-ttu-id="a80d2-149">Nadat u de toepassing hello verwijdert, kunt u het toepassingstype Hallo inrichting als u niet langer.</span><span class="sxs-lookup"><span data-stu-id="a80d2-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="a80d2-150">toounprovision toepassingstype hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a80d2-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="a80d2-151">Hallo type naam en type versie moet overeenkomen met Hallo naam en versie Hallo eerder ingerichte toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="a80d2-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="a80d2-152">Hallo-toepassingspakket wissen</span><span class="sxs-lookup"><span data-stu-id="a80d2-152">Delete hello application package</span></span>

<span data-ttu-id="a80d2-153">Nadat u hebt het toepassingstype Hallo inrichting, kunt u Hallo toepassingspakket verwijderen uit de installatiekopieopslag Hallo als u deze niet langer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="a80d2-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="a80d2-154">Verwijderen van toepassingspakketten helpt Maak schijfruimte vrij.</span><span class="sxs-lookup"><span data-stu-id="a80d2-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="a80d2-155">Hallo toepassingspakket toodelete uit de installatiekopieopslag hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a80d2-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="a80d2-156">`content-path`moet de naam Hallo van Hallo-directory die u tijdens het maken van de toepassing hello geüpload.</span><span class="sxs-lookup"><span data-stu-id="a80d2-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a80d2-157">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="a80d2-157">Related articles</span></span>

* [<span data-ttu-id="a80d2-158">Aan de slag met Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a80d2-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="a80d2-159">Aan de slag met Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="a80d2-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
