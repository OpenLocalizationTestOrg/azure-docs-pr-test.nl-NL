---
title: aaaAzure implementatie voor Service Fabric-toepassing | Microsoft Docs
description: Hallo FabricClient APIs toodeploy gebruiken en verwijderen van toepassingen in Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="84949-103">Implementeren en toepassingen die gebruikmaken van FabricClient verwijderen</span><span class="sxs-lookup"><span data-stu-id="84949-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84949-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84949-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="84949-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84949-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="84949-106">FabricClient-API's</span><span class="sxs-lookup"><span data-stu-id="84949-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="84949-107">Eenmaal een [toepassingstype zijn ingepakt][10], deze gereed is voor implementatie in een Azure Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="84949-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="84949-108">Implementatie omvat het Hallo drie stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="84949-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="84949-109">Hallo pakket toohello installatiekopie toepassingsarchief uploaden</span><span class="sxs-lookup"><span data-stu-id="84949-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="84949-110">Registratie van toepassingstype Hallo</span><span class="sxs-lookup"><span data-stu-id="84949-110">Register hello application type</span></span>
3. <span data-ttu-id="84949-111">Exemplaar van de toepassing hello maken</span><span class="sxs-lookup"><span data-stu-id="84949-111">Create hello application instance</span></span>

<span data-ttu-id="84949-112">Nadat een toepassing wordt geïmplementeerd en een exemplaar in Hallo-cluster wordt uitgevoerd, kunt u Hallo toepassingsexemplaar en het toepassingstype verwijderen.</span><span class="sxs-lookup"><span data-stu-id="84949-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="84949-113">toocompletely verwijderen een toepassing uit Hallo cluster omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="84949-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="84949-114">Met een toepassingsexemplaar van de hello verwijderen (of verwijderen)</span><span class="sxs-lookup"><span data-stu-id="84949-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="84949-115">Hef de registratie van toepassingstype Hallo als u deze niet langer nodig hebt</span><span class="sxs-lookup"><span data-stu-id="84949-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="84949-116">Hallo-toepassingspakket verwijderen uit de installatiekopieopslag Hallo</span><span class="sxs-lookup"><span data-stu-id="84949-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="84949-117">Als u [Visual Studio voor het implementeren en foutopsporing in toepassingen](service-fabric-publish-app-remote-cluster.md) op uw lokaal ontwikkelcluster alle voorgaande stappen Hallo automatisch via een PowerShell-script worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="84949-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="84949-118">Dit script is gevonden in Hallo *Scripts* map van het toepassingsproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="84949-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="84949-119">Dit artikel vindt u achtergrond op script doet zodat u kunt uitvoeren Hallo dezelfde bewerkingen buiten Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84949-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="84949-120">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="84949-120">Connect toohello cluster</span></span>
<span data-ttu-id="84949-121">Verbinding maken met cluster toohello door het maken van een [FabricClient](/dotnet/api/system.fabric.fabricclient) exemplaar voordat u een van de Hallo codevoorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="84949-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="84949-122">Voor voorbeelden van verbindende tooa lokaal ontwikkelcluster of een externe-cluster of -cluster beveiligd met Azure Active Directory, X509 certificaten of Windows Active Directory-Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="84949-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="84949-123">tooconnect toohello lokaal ontwikkelcluster, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="84949-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="84949-124">Hallo-toepassingspakket uploaden</span><span class="sxs-lookup"><span data-stu-id="84949-124">Upload hello application package</span></span>
<span data-ttu-id="84949-125">Stel dat u maakt en een toepassing met de naam van het pakket *Mijntoepassing* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84949-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="84949-126">Standaard is Hallo naam van het toepassingstype die worden vermeld in Hallo ApplicationManifest.xml 'MyApplicationType'.</span><span class="sxs-lookup"><span data-stu-id="84949-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="84949-127">Hallo-toepassingspakket dat manifest van de benodigde toepassing hello, manifesten service en config-code-gegevens pakketten bevat, zich in *C:\Users\&lt; gebruikersnaam&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="84949-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="84949-128">Uploaden van het Hallo-toepassingspakket plaatst het in een locatie die toegankelijk is voor Hallo interne Service Fabric-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="84949-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="84949-129">Service Fabric verifieert Hallo-toepassingspakket tijdens de registratie van het toepassingspakket Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="84949-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="84949-130">Als u wilt dat tooverify Hallo toepassingspakket lokaal (dat wil zeggen, voordat u uploadt), gebruiken Hallo [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84949-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="84949-131">Hallo [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploadt Hallo pakket toohello cluster installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="84949-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="84949-132">Als het Hallo-toepassingspakket is groot en/of veel bestanden, kunt u [comprimeert](service-fabric-package-apps.md#compress-a-package) en kopieer het toohello installatiekopieopslag met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84949-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="84949-133">Hallo compressie vermindert Hallo grootte en het aantal bestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="84949-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="84949-134">Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="84949-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="84949-135">Hallo-toepassingspakket registreren</span><span class="sxs-lookup"><span data-stu-id="84949-135">Register hello application package</span></span>
<span data-ttu-id="84949-136">type van de toepassing Hello en versie gedeclareerd in het toepassingsmanifest Hallo komen beschikbaar voor gebruik wanneer het Hallo-toepassingspakket is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="84949-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="84949-137">Hallo system Hallo pakket geüpload in de vorige stap Hallo leest, verifieert Hallo pakket Hallo pakketinhoud verwerkt en Hallo verwerkt pakket tooan intern systeemprobleem locatie kopieert.</span><span class="sxs-lookup"><span data-stu-id="84949-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="84949-138">Hallo [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers Hallo toepassingstype in Hallo-cluster en het beschikbaar voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="84949-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="84949-139">Hallo [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API bevat informatie over alle toepassingstypen is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="84949-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="84949-140">U kunt deze API toodetermine gebruiken als het Hallo-registratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="84949-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="84949-141">Maak een toepassingsinstantie</span><span class="sxs-lookup"><span data-stu-id="84949-141">Create an application instance</span></span>
<span data-ttu-id="84949-142">U kunt een toepassing vanuit elk toepassingstype dat is geregistreerd met behulp van Hallo instantiëren [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="84949-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="84949-143">Hallo-naam van elke toepassing moet beginnen met Hallo *"fabric: '* schema en moet uniek zijn voor elk toepassingsexemplaar (binnen een cluster).</span><span class="sxs-lookup"><span data-stu-id="84949-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="84949-144">Alle services die standaard gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing Hallo worden ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="84949-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="84949-145">Meerdere exemplaren van een toepassing kunnen worden gemaakt voor een bepaalde versie van een geregistreerde toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="84949-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="84949-146">Elk toepassingsexemplaar wordt uitgevoerd in een geïsoleerde omgeving met een eigen werkmap en het aantal processen.</span><span class="sxs-lookup"><span data-stu-id="84949-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="84949-147">toosee die met de naam toepassingen en services worden uitgevoerd in de cluster Hallo Hallo uitvoeren [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) en [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API's.</span><span class="sxs-lookup"><span data-stu-id="84949-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="84949-148">Een service-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="84949-148">Create a service instance</span></span>
<span data-ttu-id="84949-149">U kunt een service van een service met behulp van Hallo instantiëren [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="84949-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="84949-150">Als Hallo-service is gedeclareerd als een standaardservice in het toepassingsmanifest hello, wordt Hallo service gemaakt wanneer de toepassing hello wordt geïnstantieerd.</span><span class="sxs-lookup"><span data-stu-id="84949-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="84949-151">Aanroepen Hallo [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API voor een service die al wordt geïnstantieerd wordt een uitzondering van type met een foutcode met een waarde van FabricErrorCode.ServiceAlreadyExists FabricException geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="84949-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="84949-152">Verwijderen van een service-exemplaar</span><span class="sxs-lookup"><span data-stu-id="84949-152">Remove a service instance</span></span>
<span data-ttu-id="84949-153">Wanneer een service-exemplaar niet langer nodig is, kunt u deze verwijderen uit met een toepassingsexemplaar van de door de aanroepende Hallo Hallo [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="84949-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="84949-154">Deze bewerking kan niet ongedaan worden gemaakt en de status van service kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="84949-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="84949-155">Verwijderen van instantie van een toepassing</span><span class="sxs-lookup"><span data-stu-id="84949-155">Remove an application instance</span></span>
<span data-ttu-id="84949-156">Wanneer een toepassingsexemplaar niet meer nodig is, kunt u permanent verwijderen deze op naam Hallo met [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="84949-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="84949-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) alle services die deel uitmaken van toohello toepassing ook, permanent verwijderen van de status van alle service wordt automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="84949-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="84949-158">Deze bewerking kan niet ongedaan worden gemaakt en de status van toepassing kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="84949-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="84949-159">Registratie van een toepassingstype</span><span class="sxs-lookup"><span data-stu-id="84949-159">Unregister an application type</span></span>
<span data-ttu-id="84949-160">Wanneer een bepaalde versie van het type van een toepassing niet meer nodig is, moet u die bepaalde versie van het toepassingstype Hallo Hallo met registratie [Unregister ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="84949-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="84949-161">Registratie ongebruikte versies van de toepassing typen releases opslagruimte die wordt gebruikt door Hallo image store.</span><span class="sxs-lookup"><span data-stu-id="84949-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="84949-162">Een versie van het type van een toepassing kunt ongedaan worden gemaakt als geen toepassingen zijn gemaakt op basis van die versie van het type van de toepassing hello en er geen updates van toepassing op in behandeling die versie van het type van de toepassing hello verwijzen.</span><span class="sxs-lookup"><span data-stu-id="84949-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="84949-163">Een toepassingspakket verwijderen uit de installatiekopieopslag Hallo</span><span class="sxs-lookup"><span data-stu-id="84949-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="84949-164">Wanneer een toepassingspakket is niet langer nodig is, kunt u deze verwijderen uit Hallo image store toofree system resources met behulp van Hallo [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="84949-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="84949-165">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="84949-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="84949-166">Kopiëren ServiceFabricApplicationPackage vraagt om een ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="84949-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="84949-167">Hallo Service Fabric SDK omgeving moet al Hallo juiste standaardwaarden wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="84949-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="84949-168">Maar desgewenst Hallo ImageStoreConnectionString voor alle opdrachten moet overeenkomen met Hallo-waarde die Hallo Service Fabric-cluster wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="84949-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="84949-169">Hallo ImageStoreConnectionString vindt u in het clustermanifest Hallo opgehaald met Hallo [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) en Get-ImageStoreConnectionStringFromClusterManifest-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="84949-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="84949-170">Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="84949-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="84949-171">tooimport hello SDK-module, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="84949-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="84949-172">Hallo ImageStoreConnectionString is gevonden in clustermanifest Hallo:</span><span class="sxs-lookup"><span data-stu-id="84949-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="84949-173">Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="84949-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="84949-174">Grote toepassingspakket implementeren</span><span class="sxs-lookup"><span data-stu-id="84949-174">Deploy large application package</span></span>
<span data-ttu-id="84949-175">Probleem: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API een time-out voor een groot pakket (in volgorde van GB).</span><span class="sxs-lookup"><span data-stu-id="84949-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="84949-176">Probeer een van:</span><span class="sxs-lookup"><span data-stu-id="84949-176">Try:</span></span>
- <span data-ttu-id="84949-177">Geef een hogere time-out voor [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) methode met `timeout` parameter.</span><span class="sxs-lookup"><span data-stu-id="84949-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="84949-178">Hallo-out is standaard 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="84949-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="84949-179">Controleer de netwerkverbinding Hallo tussen de bron- en cluster.</span><span class="sxs-lookup"><span data-stu-id="84949-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="84949-180">Als Hallo verbinding langzaam is, kunt u overwegen een machine met een betere netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="84949-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="84949-181">Hallo client-computer in een andere regio dan het Hallo-cluster, dan kunt u met behulp van een client-computer in een dichter of dezelfde regio als Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="84949-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="84949-182">Controleer als u externe beperking zijn raken.</span><span class="sxs-lookup"><span data-stu-id="84949-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="84949-183">Wanneer de installatiekopieopslag Hallo geconfigureerde toouse azure storage, kunnen uploaden bijvoorbeeld kan worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="84949-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="84949-184">Probleem: Upload-pakket is voltooid, maar [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API een time-out optreedt. Probeer een van:</span><span class="sxs-lookup"><span data-stu-id="84949-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="84949-185">[Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert.</span><span class="sxs-lookup"><span data-stu-id="84949-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="84949-186">Hallo compressie Hallo verkleint en Hallo aantal bestanden, die op zijn beurt minder Hallo hoeveelheid verkeer en werkt deze Service Fabric moet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="84949-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="84949-187">Hallo uploadbewerking mogelijk langzamer (met name als u Hallo compressie tijd opnemen), maar registreren en ongedaan maken van de registratie Hallo toepassingstype sneller.</span><span class="sxs-lookup"><span data-stu-id="84949-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="84949-188">Geef een hogere time-out voor [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API met `timeout` parameter.</span><span class="sxs-lookup"><span data-stu-id="84949-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="84949-189">Toepassingspakket implementeren met veel bestanden</span><span class="sxs-lookup"><span data-stu-id="84949-189">Deploy application package with many files</span></span>
<span data-ttu-id="84949-190">Probleem: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) time-out voor een toepassingspakket met veel bestanden (volgorde van duizendtallen).</span><span class="sxs-lookup"><span data-stu-id="84949-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="84949-191">Probeer een van:</span><span class="sxs-lookup"><span data-stu-id="84949-191">Try:</span></span>
- <span data-ttu-id="84949-192">[Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert.</span><span class="sxs-lookup"><span data-stu-id="84949-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="84949-193">Hallo compressie vermindert het aantal bestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="84949-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="84949-194">Geef een hogere time-out voor [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) met `timeout` parameter.</span><span class="sxs-lookup"><span data-stu-id="84949-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="84949-195">Voorbeeld van code</span><span class="sxs-lookup"><span data-stu-id="84949-195">Code example</span></span>
<span data-ttu-id="84949-196">Hallo volgende voorbeeld gekopieerd van een toepassing pakket toohello image store, richt Hallo toepassingstype, instantie van een toepassing maakt, maakt een service-exemplaar, verwijdert Hallo toepassingsexemplaar, ongedaan maken met de bepalingen Hallo toepassingstype, en Hallo-toepassingspakket verwijdert uit de installatiekopieopslag Hallo.</span><span class="sxs-lookup"><span data-stu-id="84949-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="84949-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84949-197">Next steps</span></span>
[<span data-ttu-id="84949-198">Upgrade van de service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="84949-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="84949-199">Service Fabric health Inleiding</span><span class="sxs-lookup"><span data-stu-id="84949-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="84949-200">Vaststellen en oplossen van een Service Fabric-service</span><span class="sxs-lookup"><span data-stu-id="84949-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="84949-201">Model van een toepassing in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="84949-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
