---
title: Beheren van Azure Service Fabric-toepassingen met Azure CLI 2.0
description: Informatie over het implementeren en toepassingen van een Azure Service Fabric-cluster verwijderen met behulp van Azure CLI 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="a476f-103">Een Azure Service Fabric-toepassing te beheren met behulp van Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a476f-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="a476f-104">Informatie over het maken en verwijderen van toepassingen die worden uitgevoerd in een Azure Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="a476f-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a476f-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a476f-105">Prerequisites</span></span>

* <span data-ttu-id="a476f-106">Installeer Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a476f-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="a476f-107">Selecteer vervolgens uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="a476f-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="a476f-108">Zie voor meer informatie [aan de slag met Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="a476f-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="a476f-109">Een Service Fabric-toepassingspakket gereed om te worden geïmplementeerd hebben.</span><span class="sxs-lookup"><span data-stu-id="a476f-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="a476f-110">Lees voor meer informatie over het maken en een toepassing pakket over de [Service Fabric-toepassingsmodel](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="a476f-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a476f-111">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a476f-111">Overview</span></span>

<span data-ttu-id="a476f-112">Voer deze stappen voor het implementeren van een nieuwe toepassing:</span><span class="sxs-lookup"><span data-stu-id="a476f-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="a476f-113">Upload een toepassingspakket naar het archief van de Service Fabric-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a476f-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="a476f-114">Een toepassingstype inrichten.</span><span class="sxs-lookup"><span data-stu-id="a476f-114">Provision an application type.</span></span>
3. <span data-ttu-id="a476f-115">Geef op en maak een toepassing.</span><span class="sxs-lookup"><span data-stu-id="a476f-115">Specify and create an application.</span></span>
4. <span data-ttu-id="a476f-116">Geef en services maken.</span><span class="sxs-lookup"><span data-stu-id="a476f-116">Specify and create services.</span></span>

<span data-ttu-id="a476f-117">Een bestaande toepassing te verwijderen door deze stappen te voltooien:</span><span class="sxs-lookup"><span data-stu-id="a476f-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="a476f-118">Verwijder de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a476f-118">Delete the application.</span></span>
2. <span data-ttu-id="a476f-119">Het type van de bijbehorende inrichting.</span><span class="sxs-lookup"><span data-stu-id="a476f-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="a476f-120">Verwijder de inhoud van de store.</span><span class="sxs-lookup"><span data-stu-id="a476f-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="a476f-121">Een nieuwe toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="a476f-121">Deploy a new application</span></span>

<span data-ttu-id="a476f-122">Voer de volgende taken voor het implementeren van een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="a476f-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="a476f-123">Een nieuw toepassingspakket uploaden naar de image store</span><span class="sxs-lookup"><span data-stu-id="a476f-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="a476f-124">Voordat u een toepassing maakt, moet u het toepassingspakket uploaden naar het archief van de Service Fabric-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a476f-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="a476f-125">Bijvoorbeeld, als uw toepassingspakket is in de `app_package_dir` directory, de volgende opdrachten gebruiken voor het uploaden van de map:</span><span class="sxs-lookup"><span data-stu-id="a476f-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="a476f-126">Voor grote toepassingpakketten, kunt u de `--show-progress` optie om de voortgang van het uploaden van de weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a476f-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="a476f-127">Het toepassingstype inrichten</span><span class="sxs-lookup"><span data-stu-id="a476f-127">Provision the application type</span></span>

<span data-ttu-id="a476f-128">Wanneer het uploaden is voltooid, richt u de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a476f-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="a476f-129">Gebruik de volgende opdracht voor het inrichten van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="a476f-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="a476f-130">De waarde voor `application-type-build-path` is de naam van de map waar u uw toepassingspakket geüpload.</span><span class="sxs-lookup"><span data-stu-id="a476f-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="a476f-131">Maak een toepassing van een toepassingstype</span><span class="sxs-lookup"><span data-stu-id="a476f-131">Create an application from an application type</span></span>

<span data-ttu-id="a476f-132">Nadat u de toepassing inricht, moet u de volgende opdracht gebruiken een naam en het maken van uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="a476f-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="a476f-133">`app-name`de naam die u wilt gebruiken voor het toepassingsexemplaar is.</span><span class="sxs-lookup"><span data-stu-id="a476f-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="a476f-134">Aanvullende parameters kunt u krijgen via het eerder ingerichte toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="a476f-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="a476f-135">De toepassingsnaam moet beginnen met het voorvoegsel `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="a476f-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="a476f-136">Services voor de nieuwe toepassing maken</span><span class="sxs-lookup"><span data-stu-id="a476f-136">Create services for the new application</span></span>

<span data-ttu-id="a476f-137">Nadat u een toepassing hebt gemaakt, kunt u services maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a476f-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="a476f-138">In het volgende voorbeeld maken wordt een nieuwe staatloze service van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a476f-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="a476f-139">De services die u van een toepassing maken kunt worden gedefinieerd in een servicemanifest in het eerder ingerichte toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="a476f-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="a476f-140">Controleer of de implementatie van de toepassing en status</span><span class="sxs-lookup"><span data-stu-id="a476f-140">Verify application deployment and health</span></span>

<span data-ttu-id="a476f-141">Om te bevestigen dat een toepassing en service zijn geïmplementeerd, Controleer of de toepassing en service zijn vermeld:</span><span class="sxs-lookup"><span data-stu-id="a476f-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="a476f-142">Om te controleren of de service in orde is, gelijksoortige opdrachten te gebruiken voor het ophalen van de status van de service en de toepassing:</span><span class="sxs-lookup"><span data-stu-id="a476f-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="a476f-143">In orde services en toepassingen hebben een `HealthState` waarde van `Ok`.</span><span class="sxs-lookup"><span data-stu-id="a476f-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="a476f-144">Een bestaande toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="a476f-144">Remove an existing application</span></span>

<span data-ttu-id="a476f-145">Voer de volgende taken een toepassing te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a476f-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="a476f-146">De toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="a476f-146">Delete the application</span></span>

<span data-ttu-id="a476f-147">Gebruik de volgende opdracht voor het verwijderen van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="a476f-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="a476f-148">Het type van de inrichting</span><span class="sxs-lookup"><span data-stu-id="a476f-148">Unprovision the application type</span></span>

<span data-ttu-id="a476f-149">Nadat u de toepassing hebt verwijderd, kunt u het type van de inrichting als u deze niet langer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="a476f-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="a476f-150">Als u wilt het toepassingstype inrichting, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a476f-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="a476f-151">De naam en type versie moeten overeenkomen met de naam en versie in de eerder ingerichte toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="a476f-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="a476f-152">Het toepassingspakket wissen</span><span class="sxs-lookup"><span data-stu-id="a476f-152">Delete the application package</span></span>

<span data-ttu-id="a476f-153">Nadat u hebt het toepassingstype inrichting, kunt u het toepassingspakket verwijderen uit het installatiekopiearchief als u deze niet langer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="a476f-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="a476f-154">Verwijderen van toepassingspakketten helpt Maak schijfruimte vrij.</span><span class="sxs-lookup"><span data-stu-id="a476f-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="a476f-155">De om toepassingspakket te verwijderen uit het installatiekopiearchief, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a476f-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="a476f-156">`content-path`moet de naam van de map die u hebt geüpload wanneer u de toepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a476f-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a476f-157">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="a476f-157">Related articles</span></span>

* [<span data-ttu-id="a476f-158">Aan de slag met Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a476f-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="a476f-159">Aan de slag met Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="a476f-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
