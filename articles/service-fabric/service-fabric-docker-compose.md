---
title: aaaAzure Service Fabric Docker Compose Preview
description: Azure Service Fabric-indeling toomake Docker Compose accepteert deze eenvoudiger tooorchestrate bestaande containers met behulp van Service Fabric. Deze ondersteuning is momenteel in preview.
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
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="f1e3a-104">Ondersteuning voor docker Compose toepassingen in Azure Service Fabric (Preview)</span><span class="sxs-lookup"><span data-stu-id="f1e3a-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="f1e3a-105">Hallo maakt gebruik van docker [docker-compose.yml](https://docs.docker.com/compose) bestand voor het definiëren van toepassingen met meerdere container.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="f1e3a-106">toomake het eenvoudig voor klanten die bekend zijn met Docker tooorchestrate bestaande container-toepassingen op Azure Service Fabric, zijn opgenomen preview-ondersteuning voor Docker Compose systeemeigen op Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="f1e3a-107">Service Fabric kan accepteren versie 3 en hoger van `docker-compose.yml` bestanden.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="f1e3a-108">Omdat deze ondersteuning in preview is, wordt alleen een subset van Compose richtlijnen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="f1e3a-109">Bijvoorbeeld: toepassingsupgrades worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="f1e3a-110">U kunt echter altijd verwijderen en implementeren van toepassingen in plaats van de upgrade.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="f1e3a-111">toouse dit voorbeeld, uw cluster hebt gemaakt met versie 5.7 of hoger van Service Fabric-runtime Hallo via hello Azure-portal samen met de Hallo SDK overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="f1e3a-112">Deze functie is Preview-versie en wordt niet ondersteund in productie.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="f1e3a-113">Een bestand Docker Compose op Service Fabric implementeren</span><span class="sxs-lookup"><span data-stu-id="f1e3a-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="f1e3a-114">Hallo volgende opdrachten een Service Fabric-toepassing maken (met de naam `fabric:/TestContainerApp` in het voorgaande voorbeeld Hallo), die u kunt bewaken en beheert, zoals een andere Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="f1e3a-115">U kunt de opgegeven toepassingsnaam Hallo voor statusquery's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="f1e3a-116">PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="f1e3a-116">Use PowerShell</span></span>

<span data-ttu-id="f1e3a-117">Een Service Fabric opstellen-toepassing van een docker-compose.yml-bestand maken door het uitvoeren van de volgende opdracht in PowerShell Hallo:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="f1e3a-118">`RegistryUserName`en `RegistryPassword` verwijzen toohello container register gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="f1e3a-119">Nadat u de toepassing hello hebt voltooid, kunt u de status ervan controleren met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="f1e3a-120">toodelete Hallo opstellen toepassing via PowerShell, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="f1e3a-121">Gebruik van Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="f1e3a-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="f1e3a-122">U kunt ook Hallo na Service Fabric CLI-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="f1e3a-123">Als u de toepassing hello hebt gemaakt, kunt u de status ervan controleren met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="f1e3a-124">toodelete Hallo opstellen-toepassing hello volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="f1e3a-125">Richtlijnen voor ondersteunde opstellen</span><span class="sxs-lookup"><span data-stu-id="f1e3a-125">Supported Compose directives</span></span>

<span data-ttu-id="f1e3a-126">Deze preview ondersteunt een subset van de configuratieopties Hallo van Hallo opstellen versie 3-indeling, inclusief Hallo primitieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1e3a-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="f1e3a-127">Services > implementeren > replica's</span><span class="sxs-lookup"><span data-stu-id="f1e3a-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="f1e3a-128">Services > implementeren > plaatsing > beperkingen</span><span class="sxs-lookup"><span data-stu-id="f1e3a-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="f1e3a-129">Services > implementeren > Resources > limieten</span><span class="sxs-lookup"><span data-stu-id="f1e3a-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="f1e3a-130">cpu-shares</span><span class="sxs-lookup"><span data-stu-id="f1e3a-130">-cpu-shares</span></span>
    * <span data-ttu-id="f1e3a-131">-geheugen</span><span class="sxs-lookup"><span data-stu-id="f1e3a-131">-memory</span></span>
    * <span data-ttu-id="f1e3a-132">-geheugen-swap</span><span class="sxs-lookup"><span data-stu-id="f1e3a-132">-memory-swap</span></span>
* <span data-ttu-id="f1e3a-133">Services > opdrachten</span><span class="sxs-lookup"><span data-stu-id="f1e3a-133">Services > Commands</span></span>
* <span data-ttu-id="f1e3a-134">Services > omgeving</span><span class="sxs-lookup"><span data-stu-id="f1e3a-134">Services > Environment</span></span>
* <span data-ttu-id="f1e3a-135">Services > poorten</span><span class="sxs-lookup"><span data-stu-id="f1e3a-135">Services > Ports</span></span>
* <span data-ttu-id="f1e3a-136">Services > afbeelding</span><span class="sxs-lookup"><span data-stu-id="f1e3a-136">Services > Image</span></span>
* <span data-ttu-id="f1e3a-137">Services > isolatie (alleen voor Windows)</span><span class="sxs-lookup"><span data-stu-id="f1e3a-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="f1e3a-138">Services > logboekregistratie > stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="f1e3a-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="f1e3a-139">Services > logboekregistratie > stuurprogramma > Opties</span><span class="sxs-lookup"><span data-stu-id="f1e3a-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="f1e3a-140">Volume & implementeren > Volume</span><span class="sxs-lookup"><span data-stu-id="f1e3a-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="f1e3a-141">Hallo-cluster voor het afdwingen van de resource-limieten ingesteld zoals beschreven in [Service Fabric resource governance](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f1e3a-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="f1e3a-142">Alle andere Docker Compose richtlijnen worden niet ondersteund voor deze preview.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="f1e3a-143">ServiceDnsName berekening</span><span class="sxs-lookup"><span data-stu-id="f1e3a-143">ServiceDnsName computation</span></span>

<span data-ttu-id="f1e3a-144">Als het Hallo-servicenaam die u in een bestand Compose opgeeft is een volledig gekwalificeerde domeinnaam (dat wil zeggen, bevat een punt [.]), Hallo DNS-naam is geregistreerd door het Service Fabric is `<ServiceName>` (inclusief Hallo punt).</span><span class="sxs-lookup"><span data-stu-id="f1e3a-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="f1e3a-145">Als dat niet het geval is, wordt elke padsegment in de naam van de toepassing hello verandert in een domeinlabel in Hallo service DNS-naam met Hallo eerste padsegment steeds Hallo topleveldomein label.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="f1e3a-146">Bijvoorbeeld, als Hallo toepassingsnaam opgegeven is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` zou worden Hallo geregistreerde DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="f1e3a-147">Verschillen tussen opstellen (exemplaar definitie) en Service Fabric-toepassingsmodel (typedefinitie)</span><span class="sxs-lookup"><span data-stu-id="f1e3a-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="f1e3a-148">Een docker-compose.yml-bestand wordt een implementeerbaar van containers, waaronder de eigenschappen en de configuraties beschreven.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="f1e3a-149">Hallo-bestand kan bijvoorbeeld bevatten omgevingsvariabelen en poorten.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="f1e3a-150">U kunt ook implementatieparameters, zoals plaatsingsbeperkingen en limieten voor DNS-namen in Hallo docker-compose.yml-bestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="f1e3a-151">Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md) servicetypen gebruikt en de toepassingstypen, waarbij u veel exemplaren van een toepassing van kan hebben Hallo hetzelfde type.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="f1e3a-152">U kunt bijvoorbeeld één exemplaar per klant hebben.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="f1e3a-153">Dit model op basis van het type ondersteunt meerdere versies van Hallo hetzelfde toepassingstype dat geregistreerd bij Hallo-runtime.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="f1e3a-154">Bijvoorbeeld een klant kan een toepassing met het type 1.0 AppTypeA geïnstantieerd hebben en klant B kan een andere toepassing Hello geïnstantieerd hebben hetzelfde type en met versie.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="f1e3a-155">Definieert u Hallo toepassingstypen in Toepassingsmanifesten hello en u naam- en implementatie-parameters van toepassing hello opgeven wanneer u de toepassing hello maakt.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="f1e3a-156">Hoewel dit model flexibiliteit biedt, zijn we ook toosupport een eenvoudigere, op basis van het exemplaar implementatiemodel waar typen impliciete van het manifestbestand Hallo zijn planning.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="f1e3a-157">In dit model wordt elke toepassing een eigen onafhankelijk manifest.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="f1e3a-158">We bekijkt deze inspanningen met ondersteuning voor docker-compose.yml, dit is een implementatie op basis van een exemplaar-indeling.</span><span class="sxs-lookup"><span data-stu-id="f1e3a-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1e3a-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1e3a-159">Next steps</span></span>

* <span data-ttu-id="f1e3a-160">Lees informatie over Hallo [toepassingsmodel Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="f1e3a-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="f1e3a-161">Aan de slag met Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="f1e3a-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
