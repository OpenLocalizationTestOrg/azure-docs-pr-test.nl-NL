---
title: Toepassing bijwerken onderwerpen aaaAdvanced | Microsoft Docs
description: In dit artikel bevat informatie over sommige geavanceerde onderwerpen die betrekking hebben tooupgrading Service Fabric-toepassing.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="e9038-103">Upgrade van de service Fabric-toepassing: geavanceerde onderwerpen</span><span class="sxs-lookup"><span data-stu-id="e9038-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="e9038-104">Het toevoegen of verwijderen van services tijdens een upgrade van de toepassing</span><span class="sxs-lookup"><span data-stu-id="e9038-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="e9038-105">Als een nieuwe service wordt tooan-toepassing die wordt al geïmplementeerd en gepubliceerd als een upgrade toegevoegd, is de nieuwe service Hallo toegevoegde toohello geïmplementeerd toepassing.</span><span class="sxs-lookup"><span data-stu-id="e9038-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="e9038-106">Een dergelijke upgrade heeft geen invloed op Hallo-services die al deel van de toepassing hello uitmaakten.</span><span class="sxs-lookup"><span data-stu-id="e9038-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="e9038-107">Een exemplaar van Hallo-service die is toegevoegd moet echter worden gestart voor Hallo nieuwe service toobe active (met behulp van Hallo `New-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="e9038-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="e9038-108">Services kunnen ook worden verwijderd uit een toepassing als onderdeel van een upgrade.</span><span class="sxs-lookup"><span data-stu-id="e9038-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="e9038-109">Echter alle huidige exemplaren van Hallo naar-worden verwijderd service moeten worden gestopt voordat u doorgaat met de Hallo-upgrade (met behulp van Hallo `Remove-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="e9038-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="e9038-110">Handmatige upgrademodus</span><span class="sxs-lookup"><span data-stu-id="e9038-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="e9038-111">niet-bewaakte handmatige modus Hallo rekening met alleen voor de upgrade van een mislukte of onderbroken.</span><span class="sxs-lookup"><span data-stu-id="e9038-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="e9038-112">Hallo bewaakte modus is Hallo aanbevolen upgrademodus voor Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e9038-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="e9038-113">Azure Service Fabric bevat meerdere upgrade modi toosupport ontwikkeling en productie-clusters.</span><span class="sxs-lookup"><span data-stu-id="e9038-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="e9038-114">Implementatieopties gekozen kunnen afwijken voor verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="e9038-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="e9038-115">Er is een fout opgetreden in Hallo bewaakt rolling toepassing upgrade Hallo meest voorkomende upgrade toouse in de productieomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9038-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="e9038-116">Wanneer een upgrade Hallo beleid is opgegeven, Service Fabric zorgt ervoor dat de toepassing hello orde voordat Hallo upgrade wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e9038-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="e9038-117">Hallo beheerder van de toepassing kunt Hallo handmatige rolling toepassing upgrademodus toohave volledige controle over upgradevoortgang via Hallo Hallo verschillende upgradedomeinen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9038-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="e9038-118">Deze modus is handig wanneer een aangepaste of complexe evaluatie statusbeleid vereist is, of een upgrade van een ongebruikelijke activiteiten (bijvoorbeeld Hallo toepassing is al in het verlies van gegevens).</span><span class="sxs-lookup"><span data-stu-id="e9038-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="e9038-119">Ten slotte is hello geautomatiseerde rolling upgrade van de toepassing handig voor ontwikkeling of tests omgevingen tooprovide een snelle iteratie cyclus tijdens het ontwikkelen van de service.</span><span class="sxs-lookup"><span data-stu-id="e9038-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="e9038-120">Upgrade toomanual-modus wijzigen</span><span class="sxs-lookup"><span data-stu-id="e9038-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="e9038-121">**Handmatige**--stoppen Hallo upgrade van de toepassing op de huidige UD en wijzig Hallo Hallo modus tooUnmonitored handmatig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e9038-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="e9038-122">Hallo beheerder moet toomanually aanroep **MoveNextApplicationUpgradeDomainAsync** tooproceed Hello upgraden of activeren van een terugdraaibewerking door een nieuwe upgrade initiëren.</span><span class="sxs-lookup"><span data-stu-id="e9038-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="e9038-123">Zodra het Hallo-upgrade in de handmatige modus Hallo invoert, blijft in de handmatige modus Hallo totdat een nieuwe upgrade wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e9038-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="e9038-124">Hallo **GetApplicationUpgradeProgressAsync** opdracht retourneert FABRIC\_toepassing\_UPGRADE\_status\_rollend\_doorsturen\_in behandeling.</span><span class="sxs-lookup"><span data-stu-id="e9038-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="e9038-125">Een upgrade uitvoert op een diff-pakket</span><span class="sxs-lookup"><span data-stu-id="e9038-125">Upgrade with a diff package</span></span>
<span data-ttu-id="e9038-126">Een Service Fabric-toepassing kan worden bijgewerkt door de inrichting met een volledige en zelfstandige toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="e9038-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="e9038-127">Een toepassing kan ook worden bijgewerkt met behulp van een diff-pakket met alleen Hallo bijgewerkt toepassingsbestanden, Hallo toepassingsmanifest en Hallo service manifest-bestanden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e9038-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="e9038-128">Een volledige toepassingspakket bevat alle Hallo bestanden nodig toostart en een Service Fabric-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e9038-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="e9038-129">Een diff-pakket bevat alleen Hallo-bestanden die gewijzigd tussen Hallo laatste inrichten en de huidige upgrade hello, plus manifest van de volledige toepassing hello en Hallo service manifest bestanden.</span><span class="sxs-lookup"><span data-stu-id="e9038-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="e9038-130">Elke vermelding in het toepassingsmanifest Hallo of servicemanifest dat niet is gevonden in Hallo build lay-out wordt gezocht naar in Hallo image store.</span><span class="sxs-lookup"><span data-stu-id="e9038-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="e9038-131">Volledige toepassingspakketten zijn vereist voor de eerste installatie Hallo van een toepassing toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="e9038-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="e9038-132">Daaropvolgende updates kunnen zijn voor een volledige toepassingspakket of een diff-pakket.</span><span class="sxs-lookup"><span data-stu-id="e9038-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="e9038-133">Gevallen terwijl een goede keuze met behulp van een pakket diff zou zijn:</span><span class="sxs-lookup"><span data-stu-id="e9038-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="e9038-134">Een diff-pakket verdient de voorkeur wanneer u een groot pakket die verwijst naar verschillende service manifest-bestanden en/of verschillende pakketten code, config pakketten of gegevenspakketten hebt.</span><span class="sxs-lookup"><span data-stu-id="e9038-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="e9038-135">Een diff-pakket verdient de voorkeur wanneer u een implementatiesysteem dat Hallo build indeling rechtstreeks vanuit uw buildproces toepassing genereert.</span><span class="sxs-lookup"><span data-stu-id="e9038-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="e9038-136">Hoewel Hallo code nog niet is gewijzigd, ophalen nieuw gebouwde assembly's in dit geval een andere controlesom.</span><span class="sxs-lookup"><span data-stu-id="e9038-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="e9038-137">Met behulp van een volledige toepassingspakket, moet u tooupdate Hallo versie op alle code pakketten.</span><span class="sxs-lookup"><span data-stu-id="e9038-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="e9038-138">Met een diff-pakket bieden u alleen Hallo-bestanden die gewijzigd en Hallo manifestbestanden waarbij het Hallo-versie is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e9038-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="e9038-139">Wanneer een toepassing wordt bijgewerkt met behulp van Visual Studio, wordt Hallo diff-pakket wordt automatisch gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="e9038-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="e9038-140">toocreate een diff-pakket Hallo handmatig het manifest van de toepassing en Hallo service manifesten moeten worden bijgewerkt, maar alleen gewijzigd hello-pakketten moeten worden opgenomen in de laatste toepassingspakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9038-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="e9038-141">Bijvoorbeeld, u begint met het Hallo volgende van toepassing (versienummers opgegeven voor het gemak van wat):</span><span class="sxs-lookup"><span data-stu-id="e9038-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="e9038-142">Nu gaan we ervan uit gewenste tooupdate alleen Hallo codepakket van service1 met een diff-pakket met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9038-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="e9038-143">Nu is uw bijgewerkte toepassing hello volgende mapstructuur:</span><span class="sxs-lookup"><span data-stu-id="e9038-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="e9038-144">In dit geval bijwerken u Hallo application manifest too2.0.0 en Hallo servicemanifest voor service1 tooreflect Hallo code pakketupdate.</span><span class="sxs-lookup"><span data-stu-id="e9038-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="e9038-145">Hallo-map voor het toepassingspakket moet Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9038-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="e9038-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9038-146">Next steps</span></span>
<span data-ttu-id="e9038-147">[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9038-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="e9038-148">[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9038-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="e9038-149">Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="e9038-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="e9038-150">Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="e9038-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="e9038-151">Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e9038-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
