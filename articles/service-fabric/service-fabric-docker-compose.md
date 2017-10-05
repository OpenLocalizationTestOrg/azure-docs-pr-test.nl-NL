---
title: Azure Service Fabric Docker Compose Preview
description: Azure Service Fabric accepteert Docker Compose indeling voor het indelen van bestaande containers met behulp van Service Fabric te vereenvoudigen. Deze ondersteuning is momenteel in preview.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="be7b7-104">Ondersteuning voor docker Compose toepassingen in Azure Service Fabric (Preview)</span><span class="sxs-lookup"><span data-stu-id="be7b7-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="be7b7-105">Maakt gebruik van docker de [docker-compose.yml](https://docs.docker.com/compose) bestand voor het definiëren van toepassingen met meerdere container.</span><span class="sxs-lookup"><span data-stu-id="be7b7-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="be7b7-106">Als u eenvoudig voor klanten bekend zijn met Docker u bestaande containertoepassingen op Azure Service Fabric indeelt, hebben we preview-ondersteuning voor Docker Compose systeemeigen opgenomen in het platform.</span><span class="sxs-lookup"><span data-stu-id="be7b7-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="be7b7-107">Service Fabric kan accepteren versie 3 en hoger van `docker-compose.yml` bestanden.</span><span class="sxs-lookup"><span data-stu-id="be7b7-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="be7b7-108">Omdat deze ondersteuning in preview is, wordt alleen een subset van Compose richtlijnen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="be7b7-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="be7b7-109">Bijvoorbeeld: toepassingsupgrades worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="be7b7-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="be7b7-110">U kunt echter altijd verwijderen en implementeren van toepassingen in plaats van de upgrade.</span><span class="sxs-lookup"><span data-stu-id="be7b7-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="be7b7-111">Maak het cluster wilt gebruiken deze preview, met versie 5.7 of hoger van de Service Fabric-runtime via de Azure portal samen met de bijbehorende SDK.</span><span class="sxs-lookup"><span data-stu-id="be7b7-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="be7b7-112">Deze functie is Preview-versie en wordt niet ondersteund in productie.</span><span class="sxs-lookup"><span data-stu-id="be7b7-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="be7b7-113">Een bestand Docker Compose op Service Fabric implementeren</span><span class="sxs-lookup"><span data-stu-id="be7b7-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="be7b7-114">De volgende opdrachten een Service Fabric-toepassing maken (met de naam `fabric:/TestContainerApp` in het voorgaande voorbeeld), die u kunt bewaken en beheert, zoals een andere Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="be7b7-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="be7b7-115">U kunt de naam van de opgegeven toepassing voor statusquery's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="be7b7-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="be7b7-116">PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="be7b7-116">Use PowerShell</span></span>

<span data-ttu-id="be7b7-117">Een opstellen voor Service Fabric-toepassing maken van een docker-compose.yml-bestand met de volgende opdracht in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="be7b7-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="be7b7-118">`RegistryUserName`en `RegistryPassword` verwijzen naar de container register gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="be7b7-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="be7b7-119">Nadat u de toepassing hebt voltooid, kunt u de status ervan controleren met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be7b7-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="be7b7-120">Gebruik de volgende opdracht voor het verwijderen van de toepassing opstellen via PowerShell:</span><span class="sxs-lookup"><span data-stu-id="be7b7-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="be7b7-121">Gebruik van Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="be7b7-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="be7b7-122">U kunt ook de volgende Service Fabric CLI-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="be7b7-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="be7b7-123">Als u de toepassing hebt gemaakt, kunt u de status ervan controleren met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="be7b7-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="be7b7-124">Gebruik de volgende opdracht voor het verwijderen van de toepassing opstellen:</span><span class="sxs-lookup"><span data-stu-id="be7b7-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="be7b7-125">Richtlijnen voor ondersteunde opstellen</span><span class="sxs-lookup"><span data-stu-id="be7b7-125">Supported Compose directives</span></span>

<span data-ttu-id="be7b7-126">Deze preview ondersteunt een subset van de configuratieopties uit de opstellen versie 3-indeling, met inbegrip van de volgende primitieven:</span><span class="sxs-lookup"><span data-stu-id="be7b7-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="be7b7-127">Services > implementeren > replica's</span><span class="sxs-lookup"><span data-stu-id="be7b7-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="be7b7-128">Services > implementeren > plaatsing > beperkingen</span><span class="sxs-lookup"><span data-stu-id="be7b7-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="be7b7-129">Services > implementeren > Resources > limieten</span><span class="sxs-lookup"><span data-stu-id="be7b7-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="be7b7-130">cpu-shares</span><span class="sxs-lookup"><span data-stu-id="be7b7-130">-cpu-shares</span></span>
    * <span data-ttu-id="be7b7-131">-geheugen</span><span class="sxs-lookup"><span data-stu-id="be7b7-131">-memory</span></span>
    * <span data-ttu-id="be7b7-132">-geheugen-swap</span><span class="sxs-lookup"><span data-stu-id="be7b7-132">-memory-swap</span></span>
* <span data-ttu-id="be7b7-133">Services > opdrachten</span><span class="sxs-lookup"><span data-stu-id="be7b7-133">Services > Commands</span></span>
* <span data-ttu-id="be7b7-134">Services > omgeving</span><span class="sxs-lookup"><span data-stu-id="be7b7-134">Services > Environment</span></span>
* <span data-ttu-id="be7b7-135">Services > poorten</span><span class="sxs-lookup"><span data-stu-id="be7b7-135">Services > Ports</span></span>
* <span data-ttu-id="be7b7-136">Services > afbeelding</span><span class="sxs-lookup"><span data-stu-id="be7b7-136">Services > Image</span></span>
* <span data-ttu-id="be7b7-137">Services > isolatie (alleen voor Windows)</span><span class="sxs-lookup"><span data-stu-id="be7b7-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="be7b7-138">Services > logboekregistratie > stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="be7b7-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="be7b7-139">Services > logboekregistratie > stuurprogramma > Opties</span><span class="sxs-lookup"><span data-stu-id="be7b7-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="be7b7-140">Volume & implementeren > Volume</span><span class="sxs-lookup"><span data-stu-id="be7b7-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="be7b7-141">Instellen van het cluster voor het afdwingen van de resource-limieten, zoals beschreven in [Service Fabric resource governance](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="be7b7-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="be7b7-142">Alle andere Docker Compose richtlijnen worden niet ondersteund voor deze preview.</span><span class="sxs-lookup"><span data-stu-id="be7b7-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="be7b7-143">ServiceDnsName berekening</span><span class="sxs-lookup"><span data-stu-id="be7b7-143">ServiceDnsName computation</span></span>

<span data-ttu-id="be7b7-144">Als de naam van de service die u in een bestand Compose opgeeft een volledig gekwalificeerde domeinnaam is (dat wil zeggen, bevat een punt [.]), de DNS-naam geregistreerd door het Service Fabric `<ServiceName>` (inclusief de punt).</span><span class="sxs-lookup"><span data-stu-id="be7b7-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="be7b7-145">Als dat niet het geval is, moet u elk padsegment in de naam van de toepassing wordt een domeinlabel in de service DNS-naam met het eerste padsegment om het domeinlabel op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="be7b7-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="be7b7-146">Als de naam van de opgegeven toepassing is bijvoorbeeld `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` zou de geregistreerde DNS-naam zijn.</span><span class="sxs-lookup"><span data-stu-id="be7b7-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="be7b7-147">Verschillen tussen opstellen (exemplaar definitie) en Service Fabric-toepassingsmodel (typedefinitie)</span><span class="sxs-lookup"><span data-stu-id="be7b7-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="be7b7-148">Een docker-compose.yml-bestand wordt een implementeerbaar van containers, waaronder de eigenschappen en de configuraties beschreven.</span><span class="sxs-lookup"><span data-stu-id="be7b7-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="be7b7-149">Het bestand kan bijvoorbeeld omgevingsvariabelen en poorten bevatten.</span><span class="sxs-lookup"><span data-stu-id="be7b7-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="be7b7-150">U kunt ook implementatieparameters, zoals plaatsingsbeperkingen en limieten voor DNS-namen, in de docker-compose.yml-bestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="be7b7-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="be7b7-151">De [Service Fabric-toepassingsmodel](service-fabric-application-model.md) maakt gebruik van service typen en de toepassingstypen, waarbij u veel exemplaren van een toepassing van hetzelfde type kan hebben.</span><span class="sxs-lookup"><span data-stu-id="be7b7-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="be7b7-152">U kunt bijvoorbeeld één exemplaar per klant hebben.</span><span class="sxs-lookup"><span data-stu-id="be7b7-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="be7b7-153">Dit model op basis van het type ondersteunt meerdere versies van hetzelfde toepassingstype dat geregistreerd bij de runtime.</span><span class="sxs-lookup"><span data-stu-id="be7b7-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="be7b7-154">Bijvoorbeeld kan een klant een toepassing met het type 1.0 AppTypeA geïnstantieerd, en klant B kan een andere toepassing die zijn gemaakt met hetzelfde type en dezelfde versie hebben.</span><span class="sxs-lookup"><span data-stu-id="be7b7-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="be7b7-155">Definieert u de soorten toepassingen in de Toepassingsmanifesten en u de naam en de implementatie van een toepassingsparameters opgeven wanneer u de toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="be7b7-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="be7b7-156">Dit model biedt flexibiliteit, wel we hebben ook plannen voor de ondersteuning van een eenvoudigere, op basis van het exemplaar implementatiemodel waar typen impliciete van het manifestbestand zijn.</span><span class="sxs-lookup"><span data-stu-id="be7b7-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="be7b7-157">In dit model wordt elke toepassing een eigen onafhankelijk manifest.</span><span class="sxs-lookup"><span data-stu-id="be7b7-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="be7b7-158">We bekijkt deze inspanningen met ondersteuning voor docker-compose.yml, dit is een implementatie op basis van een exemplaar-indeling.</span><span class="sxs-lookup"><span data-stu-id="be7b7-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be7b7-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="be7b7-159">Next steps</span></span>

* <span data-ttu-id="be7b7-160">Lees informatie over de [toepassingsmodel Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="be7b7-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="be7b7-161">Aan de slag met Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="be7b7-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
