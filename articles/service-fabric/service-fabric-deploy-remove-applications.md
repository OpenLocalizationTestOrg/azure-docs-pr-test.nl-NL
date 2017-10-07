---
title: aaaAzure implementatie voor Service Fabric-toepassing | Microsoft Docs
description: Hoe toodeploy en verwijder toepassingen in Service Fabric met behulp van PowerShell.
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
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="4da86-103">Implementeren en verwijderen van toepassingen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="4da86-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4da86-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4da86-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="4da86-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4da86-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="4da86-106">FabricClient-API's</span><span class="sxs-lookup"><span data-stu-id="4da86-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="4da86-107">Eenmaal een [toepassingstype zijn ingepakt][10], deze gereed is voor implementatie in een Azure Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="4da86-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="4da86-108">Implementatie omvat het Hallo drie stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4da86-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="4da86-109">Hallo pakket toohello installatiekopie toepassingsarchief uploaden</span><span class="sxs-lookup"><span data-stu-id="4da86-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="4da86-110">Registratie van toepassingstype Hallo</span><span class="sxs-lookup"><span data-stu-id="4da86-110">Register hello application type</span></span>
3. <span data-ttu-id="4da86-111">Exemplaar van de toepassing hello maken</span><span class="sxs-lookup"><span data-stu-id="4da86-111">Create hello application instance</span></span>

<span data-ttu-id="4da86-112">Nadat een toepassing wordt geïmplementeerd en een exemplaar in Hallo-cluster wordt uitgevoerd, kunt u Hallo toepassingsexemplaar en het toepassingstype verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4da86-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="4da86-113">toocompletely verwijderen een toepassing uit Hallo cluster omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4da86-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="4da86-114">Met een toepassingsexemplaar van de hello verwijderen (of verwijderen)</span><span class="sxs-lookup"><span data-stu-id="4da86-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="4da86-115">Hef de registratie van toepassingstype Hallo als u deze niet langer nodig hebt</span><span class="sxs-lookup"><span data-stu-id="4da86-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="4da86-116">Hallo-toepassingspakket verwijderen uit de installatiekopieopslag Hallo</span><span class="sxs-lookup"><span data-stu-id="4da86-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="4da86-117">Als u [Visual Studio voor het implementeren en foutopsporing in toepassingen](service-fabric-publish-app-remote-cluster.md) op uw lokaal ontwikkelcluster alle voorgaande stappen Hallo automatisch via een PowerShell-script worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4da86-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="4da86-118">Dit script is gevonden in Hallo *Scripts* map van het toepassingsproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="4da86-119">Dit artikel vindt u achtergrond op script doet zodat u kunt uitvoeren Hallo dezelfde bewerkingen buiten Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4da86-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="4da86-120">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="4da86-120">Connect toohello cluster</span></span>
<span data-ttu-id="4da86-121">Voordat u een PowerShell-opdrachten in dit artikel uitvoert, wordt altijd gestart via [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="4da86-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="4da86-122">tooconnect toohello lokaal ontwikkelcluster, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4da86-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="4da86-123">Voor voorbeelden van verbindende tooa externe cluster of -cluster beveiligd met Azure Active Directory, X509 certificaten of Windows Active Directory-Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4da86-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="4da86-124">Hallo-toepassingspakket uploaden</span><span class="sxs-lookup"><span data-stu-id="4da86-124">Upload hello application package</span></span>
<span data-ttu-id="4da86-125">Uploaden van het Hallo-toepassingspakket plaatst het in een locatie die toegankelijk is voor interne Service Fabric-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="4da86-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="4da86-126">Als u tooverify Hallo toepassingspakket lokaal wilt, gebruikt u Hallo [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4da86-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4da86-127">Hallo [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht uploads Hallo pakket toohello cluster installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="4da86-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="4da86-128">Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="4da86-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="4da86-129">tooimport hello SDK-module, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4da86-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="4da86-130">Stel dat u maakt en een toepassing met de naam van het pakket *Mijntoepassing* in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4da86-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="4da86-131">Standaard is Hallo naam van het toepassingstype die worden vermeld in Hallo ApplicationManifest.xml 'MyApplicationType'.</span><span class="sxs-lookup"><span data-stu-id="4da86-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="4da86-132">Hallo-toepassingspakket dat manifest van de benodigde toepassing hello, manifesten service en config-code-gegevens pakketten bevat, zich in *C:\Users\<gebruikersnaam\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="4da86-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="4da86-133">Hallo volgende opdracht worden Hallo inhoud van het toepassingspakket Hallo:</span><span class="sxs-lookup"><span data-stu-id="4da86-133">hello following command lists hello contents of hello application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="4da86-134">Als het Hallo-toepassingspakket is groot en/of veel bestanden, kunt u [comprimeert](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="4da86-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="4da86-135">Hallo compressie vermindert Hallo grootte en het aantal bestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="4da86-136">Hallo neveneffect is dat Hallo registreren en afmelden toepassingstype zijn sneller.</span><span class="sxs-lookup"><span data-stu-id="4da86-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="4da86-137">Uploadtijd trager worden momenteel, met name als u Hallo tijd toocompress Hallo pakket opnemen.</span><span class="sxs-lookup"><span data-stu-id="4da86-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="4da86-138">een pakket, gebruik toocompress Hallo dezelfde [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4da86-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="4da86-139">Compressie kan worden gedaan afzonderlijke van uploaden met Hallo `SkipCopy` markeren of samen met de Hallo bewerking voor het uploaden.</span><span class="sxs-lookup"><span data-stu-id="4da86-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="4da86-140">Compressie toepassen op een gecomprimeerde pakket is geen.</span><span class="sxs-lookup"><span data-stu-id="4da86-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="4da86-141">een gecomprimeerde pakket gebruik toouncompress Hallo dezelfde [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht Hello `UncompressPackage` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="4da86-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="4da86-142">Hallo volgende cmdlet wordt gecomprimeerd Hallo pakket zonder deze toohello image store.</span><span class="sxs-lookup"><span data-stu-id="4da86-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="4da86-143">Hallo-pakket bevat nu ZIP-bestanden voor Hallo `Code` en `Config` pakketten.</span><span class="sxs-lookup"><span data-stu-id="4da86-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="4da86-144">Hallo-toepassing en Hallo service manifesten zijn niet ingepakte, omdat ze nodig zijn voor veel interne bewerkingen (zoals pakket delen van de toepassing de naam en versie extraheren voor bepaalde validaties).</span><span class="sxs-lookup"><span data-stu-id="4da86-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="4da86-145">Hallo manifesten comprimeren zouden deze bewerkingen niet efficiënt.</span><span class="sxs-lookup"><span data-stu-id="4da86-145">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="4da86-146">Voor grote toepassingpakketten duurt Hallo compressie.</span><span class="sxs-lookup"><span data-stu-id="4da86-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="4da86-147">Gebruik een snel SSD-station voor de beste resultaten.</span><span class="sxs-lookup"><span data-stu-id="4da86-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="4da86-148">Hallo compressie tijden en grootte van het gecomprimeerde pakket Hallo Hallo ook u verschillen op basis van de pakketinhoud Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="4da86-149">Dit is bijvoorbeeld compressie statistieken van sommige pakketten die Hallo initiële weergeven en grootte van gecomprimeerde pakket, met Hallo compressie tijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="4da86-150">Aanvankelijke grootte (MB)</span><span class="sxs-lookup"><span data-stu-id="4da86-150">Initial size (MB)</span></span>|<span data-ttu-id="4da86-151">Aantal bestanden</span><span class="sxs-lookup"><span data-stu-id="4da86-151">File count</span></span>|<span data-ttu-id="4da86-152">Compressie tijd</span><span class="sxs-lookup"><span data-stu-id="4da86-152">Compression Time</span></span>|<span data-ttu-id="4da86-153">Gecomprimeerde pakketgrootte (MB)</span><span class="sxs-lookup"><span data-stu-id="4da86-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="4da86-154">100</span><span class="sxs-lookup"><span data-stu-id="4da86-154">100</span></span>|<span data-ttu-id="4da86-155">100</span><span class="sxs-lookup"><span data-stu-id="4da86-155">100</span></span>|<span data-ttu-id="4da86-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="4da86-156">00:00:03.3547592</span></span>|<span data-ttu-id="4da86-157">60</span><span class="sxs-lookup"><span data-stu-id="4da86-157">60</span></span>|
|<span data-ttu-id="4da86-158">512</span><span class="sxs-lookup"><span data-stu-id="4da86-158">512</span></span>|<span data-ttu-id="4da86-159">100</span><span class="sxs-lookup"><span data-stu-id="4da86-159">100</span></span>|<span data-ttu-id="4da86-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="4da86-160">00:00:16.3850303</span></span>|<span data-ttu-id="4da86-161">307</span><span class="sxs-lookup"><span data-stu-id="4da86-161">307</span></span>|
|<span data-ttu-id="4da86-162">1024</span><span class="sxs-lookup"><span data-stu-id="4da86-162">1024</span></span>|<span data-ttu-id="4da86-163">500</span><span class="sxs-lookup"><span data-stu-id="4da86-163">500</span></span>|<span data-ttu-id="4da86-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="4da86-164">00:00:32.5907950</span></span>|<span data-ttu-id="4da86-165">615</span><span class="sxs-lookup"><span data-stu-id="4da86-165">615</span></span>|
|<span data-ttu-id="4da86-166">2048</span><span class="sxs-lookup"><span data-stu-id="4da86-166">2048</span></span>|<span data-ttu-id="4da86-167">1000</span><span class="sxs-lookup"><span data-stu-id="4da86-167">1000</span></span>|<span data-ttu-id="4da86-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="4da86-168">00:01:04.3775554</span></span>|<span data-ttu-id="4da86-169">1231</span><span class="sxs-lookup"><span data-stu-id="4da86-169">1231</span></span>|
|<span data-ttu-id="4da86-170">5012</span><span class="sxs-lookup"><span data-stu-id="4da86-170">5012</span></span>|<span data-ttu-id="4da86-171">100</span><span class="sxs-lookup"><span data-stu-id="4da86-171">100</span></span>|<span data-ttu-id="4da86-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="4da86-172">00:02:45.2951288</span></span>|<span data-ttu-id="4da86-173">3074</span><span class="sxs-lookup"><span data-stu-id="4da86-173">3074</span></span>|

<span data-ttu-id="4da86-174">Nadat u een pakket is gecomprimeerd, kan het geüploade tooone of meerdere Service Fabric-clusters indien nodig.</span><span class="sxs-lookup"><span data-stu-id="4da86-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="4da86-175">Hallo-mechanisme voor clientimplementatie is hetzelfde voor gecomprimeerde en ongecomprimeerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="4da86-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="4da86-176">Hallo-pakket is gecomprimeerd, wordt deze opgeslagen als zodanig in Hallo cluster image store als deze niet op Hallo knooppunt gecomprimeerd voordat de toepassing hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4da86-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="4da86-177">Hallo volgende voorbeeld wordt geüpload Hallo pakket toohello image store in een map met de naam 'MyApplicationV1':</span><span class="sxs-lookup"><span data-stu-id="4da86-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="4da86-178">Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="4da86-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="4da86-179">tooimport hello SDK-module, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4da86-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="4da86-180">Als u geen Hallo opgeeft *- ApplicationPackagePathInImageStore* parameter Hallo-toepassingspakket is gekopieerd naar 'Debug' Hallo-map in Hallo image store.</span><span class="sxs-lookup"><span data-stu-id="4da86-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="4da86-181">Hallo duurt tooupload een pakket is afhankelijk van meerdere factoren.</span><span class="sxs-lookup"><span data-stu-id="4da86-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="4da86-182">Sommige van deze factoren zijn Hallo aantal bestanden in Hallo pakket Hallo pakketgrootte en bestandsgrootten Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="4da86-183">de netwerksnelheid Hallo tussen bron- en Service Fabric-cluster Hallo Hallo ook van invloed is op Hallo tijd.</span><span class="sxs-lookup"><span data-stu-id="4da86-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="4da86-184">Hallo standaardtime-out voor [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="4da86-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="4da86-185">Afhankelijk van factoren beschreven Hallo, moet u wellicht tooincrease Hallo time-out.</span><span class="sxs-lookup"><span data-stu-id="4da86-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="4da86-186">Als u Hallo-pakket in aanroep van Hallo kopiëren comprimeert, moet u tooalso beschouwd als Hallo compressie keer.</span><span class="sxs-lookup"><span data-stu-id="4da86-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="4da86-187">Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="4da86-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="4da86-188">Hallo-toepassingspakket registreren</span><span class="sxs-lookup"><span data-stu-id="4da86-188">Register hello application package</span></span>
<span data-ttu-id="4da86-189">type van de toepassing Hello en versie gedeclareerd in het toepassingsmanifest Hallo komen beschikbaar voor gebruik wanneer het Hallo-toepassingspakket is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4da86-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="4da86-190">Hallo system Hallo pakket geüpload in de vorige stap Hallo leest, verifieert Hallo pakket Hallo pakketinhoud verwerkt en Hallo verwerkt pakket tooan intern systeemprobleem locatie kopieert.</span><span class="sxs-lookup"><span data-stu-id="4da86-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="4da86-191">Voer Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister Hallo toepassingstype in Hallo-cluster en het beschikbaar voor implementatie:</span><span class="sxs-lookup"><span data-stu-id="4da86-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="4da86-192">'MyApplicationV1' is Hallo-map in Hallo image store waar Hallo toepassingspakket zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4da86-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="4da86-193">type van de toepassing Hello met de naam 'MyApplicationType' en versie '1.0.0' (zowel gevonden in het toepassingsmanifest Hallo) is nu geregistreerd in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4da86-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="4da86-194">Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) opdracht retourneert alleen nadat Hallo systeem geregistreerd Hallo-toepassingspakket heeft.</span><span class="sxs-lookup"><span data-stu-id="4da86-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="4da86-195">Hoe lang duurt registratie afhankelijk van Hallo grootte en de inhoud van het toepassingspakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="4da86-196">Indien nodig, Hallo **- TimeoutSec** parameter gebruikte toosupply een langere time-out kan zijn (Hallo standaardtime-out is 60 seconden).</span><span class="sxs-lookup"><span data-stu-id="4da86-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="4da86-197">Als u een grote toepassing van het pakket of als u time-outs ondervindt, gebruikt u Hallo **Async -** parameter.</span><span class="sxs-lookup"><span data-stu-id="4da86-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="4da86-198">Hallo-opdracht geretourneerd wanneer Hallo cluster de opdracht register Hallo accepteert en Hallo verwerking blijft indien nodig.</span><span class="sxs-lookup"><span data-stu-id="4da86-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="4da86-199">Hallo [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) opdracht geeft een lijst van alle versies van het type toepassing is geregistreerd en hun registratiestatus.</span><span class="sxs-lookup"><span data-stu-id="4da86-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4da86-200">U kunt deze opdracht toodetermine gebruiken als het Hallo-registratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4da86-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="4da86-201">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="4da86-201">Create hello application</span></span>
<span data-ttu-id="4da86-202">U kunt een toepassing met een versie van het toepassingstype dat is geregistreerd met behulp van Hallo instantiëren [nieuw ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4da86-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4da86-203">Hallo-naam van elke toepassing moet beginnen met Hallo *"fabric: '* schema en moet uniek zijn voor elk toepassingsexemplaar.</span><span class="sxs-lookup"><span data-stu-id="4da86-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="4da86-204">Alle services die standaard gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing Hallo worden ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4da86-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="4da86-205">Meerdere exemplaren van een toepassing kunnen worden gemaakt voor een bepaalde versie van een geregistreerde toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="4da86-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="4da86-206">Elk toepassingsexemplaar wordt uitgevoerd in een geïsoleerde omgeving met een eigen werk directory en het proces.</span><span class="sxs-lookup"><span data-stu-id="4da86-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="4da86-207">toosee die met de naam apps en services worden uitgevoerd in de cluster Hallo Hallo uitvoeren [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) en [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span><span class="sxs-lookup"><span data-stu-id="4da86-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="4da86-208">Een toepassing verwijderen</span><span class="sxs-lookup"><span data-stu-id="4da86-208">Remove an application</span></span>
<span data-ttu-id="4da86-209">Wanneer een toepassingsexemplaar niet meer nodig is, kunt u permanent verwijderen deze op naam Hallo met [verwijderen ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4da86-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4da86-210">[Verwijder ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) alle services die deel uitmaken van toohello toepassing ook, permanent verwijderen van de status van alle service wordt automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4da86-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="4da86-211">Deze bewerking kan niet ongedaan worden gemaakt en de status van toepassing kan niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="4da86-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="4da86-212">Registratie van een toepassingstype</span><span class="sxs-lookup"><span data-stu-id="4da86-212">Unregister an application type</span></span>
<span data-ttu-id="4da86-213">Wanneer een bepaalde versie van het type van een toepassing niet meer nodig is, moet u registratie toepassingstype Hallo Hallo met [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4da86-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4da86-214">Registratie ongebruikte toepassing typen releases opslagruimte die wordt gebruikt door Hallo image store.</span><span class="sxs-lookup"><span data-stu-id="4da86-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="4da86-215">Een toepassingstype kan ongedaan worden zolang geen toepassingen worden geïnstantieerd tegen en niet in afwachting van toepassing upgrades hiernaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="4da86-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="4da86-216">Voer [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee Hallo toepassingstypen worden momenteel geregistreerd in Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="4da86-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="4da86-217">Voer [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister een specifieke toepassingstype:</span><span class="sxs-lookup"><span data-stu-id="4da86-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="4da86-218">Een toepassingspakket verwijderen uit de installatiekopieopslag Hallo</span><span class="sxs-lookup"><span data-stu-id="4da86-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="4da86-219">Wanneer een toepassingspakket is niet langer nodig is, kunt u deze verwijderen uit Hallo image store toofree Maak systeembronnen.</span><span class="sxs-lookup"><span data-stu-id="4da86-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="4da86-220">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4da86-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="4da86-221">Kopiëren ServiceFabricApplicationPackage vraagt om een ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="4da86-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="4da86-222">Hallo Service Fabric SDK omgeving moet al Hallo juiste standaardwaarden wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4da86-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="4da86-223">Maar desgewenst Hallo ImageStoreConnectionString voor alle opdrachten moet overeenkomen met Hallo-waarde die Hallo Service Fabric-cluster wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4da86-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="4da86-224">Hallo ImageStoreConnectionString vindt u in het clustermanifest Hallo opgehaald met Hallo [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) en Get-ImageStoreConnectionStringFromClusterManifest-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="4da86-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="4da86-225">Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="4da86-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="4da86-226">tooimport hello SDK-module, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4da86-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="4da86-227">Hallo ImageStoreConnectionString is gevonden in clustermanifest Hallo:</span><span class="sxs-lookup"><span data-stu-id="4da86-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="4da86-228">Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.</span><span class="sxs-lookup"><span data-stu-id="4da86-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="4da86-229">Grote toepassingspakket implementeren</span><span class="sxs-lookup"><span data-stu-id="4da86-229">Deploy large application package</span></span>
<span data-ttu-id="4da86-230">Probleem: [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) een time-out voor een groot pakket (in volgorde van GB).</span><span class="sxs-lookup"><span data-stu-id="4da86-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="4da86-231">Probeer een van:</span><span class="sxs-lookup"><span data-stu-id="4da86-231">Try:</span></span>
- <span data-ttu-id="4da86-232">Geef een hogere time-out voor [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht met `TimeoutSec` parameter.</span><span class="sxs-lookup"><span data-stu-id="4da86-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="4da86-233">Hallo-out is standaard 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="4da86-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="4da86-234">Controleer de netwerkverbinding Hallo tussen de bron- en cluster.</span><span class="sxs-lookup"><span data-stu-id="4da86-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="4da86-235">Als Hallo verbinding langzaam is, kunt u overwegen een machine met een betere netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="4da86-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="4da86-236">Hallo client-computer in een andere regio dan het Hallo-cluster, dan kunt u met behulp van een client-computer in een dichter of dezelfde regio als Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4da86-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="4da86-237">Controleer als u externe beperking zijn raken.</span><span class="sxs-lookup"><span data-stu-id="4da86-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="4da86-238">Wanneer de installatiekopieopslag Hallo geconfigureerde toouse azure storage, kunnen uploaden bijvoorbeeld kan worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="4da86-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="4da86-239">Probleem: Upload-pakket is voltooid, maar [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) een time-out optreedt. Probeer een van:</span><span class="sxs-lookup"><span data-stu-id="4da86-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="4da86-240">[Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert.</span><span class="sxs-lookup"><span data-stu-id="4da86-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="4da86-241">Hallo compressie Hallo verkleint en Hallo aantal bestanden, die op zijn beurt minder Hallo hoeveelheid verkeer en werkt deze Service Fabric moet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4da86-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="4da86-242">Hallo uploadbewerking mogelijk langzamer (met name als u Hallo compressie tijd opnemen), maar registreren en ongedaan maken van de registratie Hallo toepassingstype sneller.</span><span class="sxs-lookup"><span data-stu-id="4da86-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="4da86-243">Geef een hogere time-out voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) met `TimeoutSec` parameter.</span><span class="sxs-lookup"><span data-stu-id="4da86-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="4da86-244">Geef `Async` overschakelen voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4da86-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="4da86-245">Hallo-opdracht geretourneerd wanneer Hallo cluster Hallo opdracht accepteert en registratie van toepassingstype Hallo Hallo asynchroon blijft.</span><span class="sxs-lookup"><span data-stu-id="4da86-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="4da86-246">Daarom wordt is er geen toospecify moet een hogere time-out in dit geval.</span><span class="sxs-lookup"><span data-stu-id="4da86-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="4da86-247">Hallo [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) opdracht geeft een lijst van alle versies van het type toepassing is geregistreerd en hun registratiestatus.</span><span class="sxs-lookup"><span data-stu-id="4da86-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4da86-248">U kunt deze opdracht toodetermine gebruiken als het Hallo-registratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4da86-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="4da86-249">Toepassingspakket implementeren met veel bestanden</span><span class="sxs-lookup"><span data-stu-id="4da86-249">Deploy application package with many files</span></span>
<span data-ttu-id="4da86-250">Probleem: [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) time-out voor een toepassingspakket met veel bestanden (volgorde van duizendtallen).</span><span class="sxs-lookup"><span data-stu-id="4da86-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="4da86-251">Probeer een van:</span><span class="sxs-lookup"><span data-stu-id="4da86-251">Try:</span></span>
- <span data-ttu-id="4da86-252">[Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert.</span><span class="sxs-lookup"><span data-stu-id="4da86-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="4da86-253">Hallo compressie vermindert het aantal bestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="4da86-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="4da86-254">Geef een hogere time-out voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) met `TimeoutSec` parameter.</span><span class="sxs-lookup"><span data-stu-id="4da86-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="4da86-255">Geef `Async` overschakelen voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4da86-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="4da86-256">Hallo-opdracht geretourneerd wanneer Hallo cluster Hallo opdracht accepteert en registratie van toepassingstype Hallo Hallo asynchroon blijft.</span><span class="sxs-lookup"><span data-stu-id="4da86-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="4da86-257">Daarom wordt is er geen toospecify moet een hogere time-out in dit geval.</span><span class="sxs-lookup"><span data-stu-id="4da86-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="4da86-258">Hallo [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) opdracht geeft een lijst van alle versies van het type toepassing is geregistreerd en hun registratiestatus.</span><span class="sxs-lookup"><span data-stu-id="4da86-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4da86-259">U kunt deze opdracht toodetermine gebruiken als het Hallo-registratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4da86-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="4da86-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4da86-260">Next steps</span></span>
[<span data-ttu-id="4da86-261">Upgrade van de service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="4da86-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="4da86-262">Service Fabric health Inleiding</span><span class="sxs-lookup"><span data-stu-id="4da86-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="4da86-263">Vaststellen en oplossen van een Service Fabric-service</span><span class="sxs-lookup"><span data-stu-id="4da86-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="4da86-264">Model van een toepassing in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4da86-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
