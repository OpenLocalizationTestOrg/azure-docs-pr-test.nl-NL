---
title: een Azure Service Fabric-app aaaPackage | Microsoft Docs
description: Hoe toopackage een Service Fabric-toepassing voordat u tooa cluster implementeert.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="d63f0-103">Een toepassing van het pakket</span><span class="sxs-lookup"><span data-stu-id="d63f0-103">Package an application</span></span>
<span data-ttu-id="d63f0-104">Dit artikel wordt beschreven hoe toopackage een Service Fabric-toepassing, waardoor het gereed is voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="d63f0-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="d63f0-105">Lay-out</span><span class="sxs-lookup"><span data-stu-id="d63f0-105">Package layout</span></span>
<span data-ttu-id="d63f0-106">Hallo-toepassingsmanifest, een of meer service-manifesten en andere benodigde pakket bestanden moeten worden opgeslagen in een specifieke indeling voor implementatie in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="d63f0-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="d63f0-107">Hallo voorbeeld manifesten in dit artikel moet toobe georganiseerd in Hallo directory-structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="d63f0-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="d63f0-108">Hallo mappen zijn benoemde toomatch hello **naam** kenmerken van elk element in de bijbehorende.</span><span class="sxs-lookup"><span data-stu-id="d63f0-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="d63f0-109">Bijvoorbeeld, als hello servicemanifest bevat twee code pakketten met Hallo namen **MyCodeA** en **MyCodeB**, en vervolgens twee mappen met dezelfde namen zou bevatten Hallo Hallo nodig binaire bestanden voor elke code het pakket.</span><span class="sxs-lookup"><span data-stu-id="d63f0-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="d63f0-110">Entrypoint gebruiken</span><span class="sxs-lookup"><span data-stu-id="d63f0-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="d63f0-111">Typische scenario's voor het gebruik van **entrypoint** zijn wanneer u toorun een uitvoerbaar bestand voordat Hallo-service wordt gestart dient of u tooperform een bewerking met verhoogde bevoegdheden moet.</span><span class="sxs-lookup"><span data-stu-id="d63f0-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="d63f0-112">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d63f0-112">For example:</span></span>

* <span data-ttu-id="d63f0-113">In te stellen en het initialiseren van omgevingsvariabelen die Hallo service uitvoerbare behoeften.</span><span class="sxs-lookup"><span data-stu-id="d63f0-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="d63f0-114">Het is niet beperkt tooonly uitvoerbare bestanden via Hallo Service Fabric-programmeermodellen geschreven.</span><span class="sxs-lookup"><span data-stu-id="d63f0-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="d63f0-115">Npm.exe moet bijvoorbeeld een aantal omgevingsvariabelen die is geconfigureerd voor het implementeren van een node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d63f0-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="d63f0-116">Instellen van toegangsbeheer door beveiligingscertificaten te installeren.</span><span class="sxs-lookup"><span data-stu-id="d63f0-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="d63f0-117">Voor meer informatie over het tooconfigure hello **entrypoint**, Zie [Hallo beleid configureren voor een service-instelling toegangspunt.](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="d63f0-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="d63f0-118">Configureren</span><span class="sxs-lookup"><span data-stu-id="d63f0-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="d63f0-119">Het bouwen van een pakket met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d63f0-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="d63f0-120">Als u uw toepassing toocreate Visual Studio 2015 gebruikt, kunt u Hallo pakket opdracht tooautomatically een pakket maakt dat overeenkomt met de Hallo lay-out die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="d63f0-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="d63f0-121">toocreate een pakket met de rechtermuisknop op Hallo application-project in Solution Explorer en kiest Hallo pakket, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d63f0-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Een toepassing met Visual Studio-pakket][vs-package-command]

<span data-ttu-id="d63f0-123">Wanneer verpakking voltooid is, kunt u Hallo-locatie van het Hallo-pakket vinden in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="d63f0-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="d63f0-124">Hallo verpakking stap gebeurt automatisch wanneer u implementeert of opsporen in uw toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d63f0-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="d63f0-125">Het bouwen van een pakket met de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="d63f0-125">Build a package by command line</span></span>
<span data-ttu-id="d63f0-126">Het is ook mogelijk tooprogrammatically pakket van uw toepassing met `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="d63f0-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="d63f0-127">Achter de schermen hello, Visual Studio wordt uitgevoerd het Hallo-uitvoer is dus dezelfde.</span><span class="sxs-lookup"><span data-stu-id="d63f0-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="d63f0-128">Hallo-testpakket</span><span class="sxs-lookup"><span data-stu-id="d63f0-128">Test hello package</span></span>
<span data-ttu-id="d63f0-129">U kunt Hallo pakketstructuur lokaal via PowerShell controleren met behulp van Hallo [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d63f0-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="d63f0-130">Met deze opdracht controleert manifest bij het parseren van problemen en controleer of alle verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="d63f0-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="d63f0-131">Met deze opdracht controleert alleen of Hallo structurele juistheid van Hallo mappen en bestanden in Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="d63f0-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="d63f0-132">Er niet gecontroleerd van Hallo pakketinhoud code of gegevens buiten de controleren of alle vereiste bestanden aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="d63f0-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="d63f0-133">Deze fout ziet u dat Hallo *MySetup.bat* bestand waarnaar wordt verwezen in Hallo servicemanifest **entrypoint** ontbreekt in het Hallo-codepakket.</span><span class="sxs-lookup"><span data-stu-id="d63f0-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="d63f0-134">Nadat de ontbrekende Hallo-bestand wordt toegevoegd, wordt verificatie van de toepassing hello doorgegeven:</span><span class="sxs-lookup"><span data-stu-id="d63f0-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="d63f0-135">Als uw toepassing [toepassingsparameters](service-fabric-manage-multiple-environment-app-configuration.md) gedefinieerd, kunt u ze in doorgeven [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) voor de juiste validatie.</span><span class="sxs-lookup"><span data-stu-id="d63f0-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="d63f0-136">Als u Hallo cluster waarop de toepassing hello wordt geïmplementeerd weet, kunt u doorgeeft in Hallo `ImageStoreConnectionString` parameter.</span><span class="sxs-lookup"><span data-stu-id="d63f0-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="d63f0-137">Hallo-pakket is in dit geval ook gevalideerd met eerdere versies van de toepassing hello die al in het Hallo-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d63f0-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="d63f0-138">Bijvoorbeeld, Hallo validatie kan detecteren of een pakket met de Hallo dezelfde versie, maar verschillende inhoud al is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d63f0-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="d63f0-139">Zodra de toepassing hello correct wordt verpakt en is gevalideerd, evalueren op basis van Hallo grootte en het aantal bestanden Hallo als compressie is vereist.</span><span class="sxs-lookup"><span data-stu-id="d63f0-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="d63f0-140">Een pakket comprimeren</span><span class="sxs-lookup"><span data-stu-id="d63f0-140">Compress a package</span></span>
<span data-ttu-id="d63f0-141">Wanneer een pakket grote of veel bestanden heeft, kunt u het comprimeren voor een snellere implementatie.</span><span class="sxs-lookup"><span data-stu-id="d63f0-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="d63f0-142">Compressie vermindert Hallo aantal bestanden en Hallo pakketgrootte.</span><span class="sxs-lookup"><span data-stu-id="d63f0-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="d63f0-143">Voor een gecomprimeerde toepassingspakket [Uploading Hallo toepassingspakket](service-fabric-deploy-remove-applications.md#upload-the-application-package) duurt langer dan toouploading Hallo niet-gecomprimeerde pakket (speciaal als compressie tijd zijn meeberekend), maar [registreren](service-fabric-deploy-remove-applications.md#register-the-application-package) en [afmelden Hallo toepassingstype](service-fabric-deploy-remove-applications.md#unregister-an-application-type) voor een gecomprimeerde pakket sneller zijn.</span><span class="sxs-lookup"><span data-stu-id="d63f0-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="d63f0-144">Hallo-mechanisme voor clientimplementatie is hetzelfde voor gecomprimeerde en ongecomprimeerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="d63f0-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="d63f0-145">Hallo-pakket is gecomprimeerd, wordt deze opgeslagen als zodanig in Hallo cluster image store als deze niet op Hallo knooppunt gecomprimeerd voordat de toepassing hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d63f0-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="d63f0-146">Hallo compressie vervangt Hallo geldig Service Fabric-pakket door Hallo gecomprimeerde versie.</span><span class="sxs-lookup"><span data-stu-id="d63f0-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="d63f0-147">Hallo map moet schrijfmachtigingen toestaan.</span><span class="sxs-lookup"><span data-stu-id="d63f0-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="d63f0-148">Compressie uitgevoerd op een al gecomprimeerde pakket levert geen wijzigingen aangebracht.</span><span class="sxs-lookup"><span data-stu-id="d63f0-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="d63f0-149">U kunt een pakket met de Powershell-opdracht Hallo comprimeren [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) met `CompressPackage` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="d63f0-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="d63f0-150">U kunt Hallo decomprimeren van het pakket met de Hallo dezelfde opdracht met behulp `UncompressPackage` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="d63f0-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="d63f0-151">Hallo volgende opdracht worden gecomprimeerd Hallo pakket zonder deze toohello image store.</span><span class="sxs-lookup"><span data-stu-id="d63f0-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="d63f0-152">U kunt een gecomprimeerde pakket tooone of meer Service Fabric-clusters, kopiëren, indien nodig, met behulp van [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) zonder Hallo `SkipCopy` vlag.</span><span class="sxs-lookup"><span data-stu-id="d63f0-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="d63f0-153">Hallo-pakket bevat nu ZIP-bestanden voor Hallo `code`, `config`, en `data` pakketten.</span><span class="sxs-lookup"><span data-stu-id="d63f0-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="d63f0-154">Hallo-toepassingsmanifest en Hallo service manifesten zijn niet ingepakte, omdat ze nodig zijn voor veel interne bewerkingen (zoals pakket delen van de toepassing de naam en versie extraheren voor bepaalde validaties).</span><span class="sxs-lookup"><span data-stu-id="d63f0-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="d63f0-155">Hallo manifesten comprimeren zouden deze bewerkingen niet efficiënt.</span><span class="sxs-lookup"><span data-stu-id="d63f0-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="d63f0-156">U kunt ook comprimeren en kopieer het pakket met Hallo [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in één stap.</span><span class="sxs-lookup"><span data-stu-id="d63f0-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="d63f0-157">Als Hallo pakket groot is, geeft u een hoog genoeg time-out tooallow tijd voor zowel Hallo pakket compressie en Hallo uploaden toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d63f0-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="d63f0-158">Service Fabric berekent intern controlesommen voor toepassingspakketten Hallo voor validatie.</span><span class="sxs-lookup"><span data-stu-id="d63f0-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="d63f0-159">Bij gebruik van compressie, worden de Hallo controlesommen berekend op Hallo ingepakte versies van elk pakket.</span><span class="sxs-lookup"><span data-stu-id="d63f0-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="d63f0-160">Als u een niet-gecomprimeerde versie van het toepassingspakket hebt gekopieerd, en u toouse compressie voor Hallo wilt hetzelfde pakket, moet u Hallo versies van Hallo `code`, `config`, en `data` pakketten tooavoid checksum komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="d63f0-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="d63f0-161">Als hello-pakketten ongewijzigd zijn, in plaats van Hallo versie wijzigen, kunt u [diff inrichting](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="d63f0-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="d63f0-162">Met deze optie Hallo ongewijzigd pakket niet opnemen in plaats daarvan ernaar verwijzen vanuit Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="d63f0-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="d63f0-163">Als u een gecomprimeerde versie van pakket Hallo geüpload en u wilt dat een niet-gecomprimeerde pakket toouse, moet u op dezelfde manier Hallo versies tooavoid Hallo checksum komt niet overeen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d63f0-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="d63f0-164">Hallo pakket is nu correct verpakt, gevalideerd en gecomprimeerd (indien nodig), zodat deze gereed is voor [implementatie](service-fabric-deploy-remove-applications.md) tooone of meer Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="d63f0-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="d63f0-165">Comprimeren van pakketten bij het implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d63f0-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="d63f0-166">U kunt opgeven dat Visual Studio toocompress pakketten op implementatie door toe te voegen Hallo `CopyPackageParameters` element tooyour publicatieprofiel en stel Hallo `CompressPackage` kenmerk te`true`.</span><span class="sxs-lookup"><span data-stu-id="d63f0-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="d63f0-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d63f0-167">Next steps</span></span>
<span data-ttu-id="d63f0-168">[Implementeren en toepassingen verwijderen] [ 10] wordt beschreven hoe toouse PowerShell toomanage toepassingsexemplaren</span><span class="sxs-lookup"><span data-stu-id="d63f0-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="d63f0-169">[Het beheren van parameters voor de toepassing voor omgevingen met meerdere] [ 11] wordt beschreven hoe tooconfigure parameters en variabelen voor exemplaren van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="d63f0-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="d63f0-170">[Beveiligingsbeleid voor uw toepassing configureert] [ 12] wordt beschreven hoe toorun services onder beveiligingstoegang beleid toorestrict.</span><span class="sxs-lookup"><span data-stu-id="d63f0-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
