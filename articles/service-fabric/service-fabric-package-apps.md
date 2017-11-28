---
title: Pakket van een Azure-Service Fabric-app | Microsoft Docs
description: Het pakket een Service Fabric-toepassing voordat u implementeert naar een cluster.
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
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="d3afb-103">Een toepassing van het pakket</span><span class="sxs-lookup"><span data-stu-id="d3afb-103">Package an application</span></span>
<span data-ttu-id="d3afb-104">In dit artikel wordt beschreven hoe een Service Fabric-toepassing van het pakket en gereed is voor implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="d3afb-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="d3afb-105">Lay-out</span><span class="sxs-lookup"><span data-stu-id="d3afb-105">Package layout</span></span>
<span data-ttu-id="d3afb-106">Het toepassingsmanifest, een of meer service-manifesten en andere benodigde pakket-bestanden moeten worden ingedeeld in een specifieke indeling voor implementatie in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3afb-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="d3afb-107">De manifesten voorbeeld in dit artikel moet worden ingedeeld in de volgende mapstructuur:</span><span class="sxs-lookup"><span data-stu-id="d3afb-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

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

<span data-ttu-id="d3afb-108">De mappen zijn met de naam overeenkomt met de **naam** kenmerken van elk element in de bijbehorende.</span><span class="sxs-lookup"><span data-stu-id="d3afb-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="d3afb-109">Als de servicemanifest bevat twee code pakketten met de namen bijvoorbeeld **MyCodeA** en **MyCodeB**, en vervolgens twee mappen met dezelfde namen van de benodigde binaire bestanden voor elk codepakket zou bevatten.</span><span class="sxs-lookup"><span data-stu-id="d3afb-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="d3afb-110">Entrypoint gebruiken</span><span class="sxs-lookup"><span data-stu-id="d3afb-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="d3afb-111">Typische scenario's voor het gebruik van **entrypoint** wanneer moet u een uitvoerbaar bestand uitvoeren voordat de service wordt gestart of moet u een bewerking met verhoogde bevoegdheden uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d3afb-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="d3afb-112">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d3afb-112">For example:</span></span>

* <span data-ttu-id="d3afb-113">In te stellen en het initialiseren van omgevingsvariabelen op die moet van het uitvoerbare bestand van de service.</span><span class="sxs-lookup"><span data-stu-id="d3afb-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="d3afb-114">Het is niet beperkt tot alleen uitvoerbare bestanden die zijn geschreven via de Service Fabric-programmeermodellen.</span><span class="sxs-lookup"><span data-stu-id="d3afb-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="d3afb-115">Npm.exe moet bijvoorbeeld een aantal omgevingsvariabelen die is geconfigureerd voor het implementeren van een node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3afb-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="d3afb-116">Instellen van toegangsbeheer door beveiligingscertificaten te installeren.</span><span class="sxs-lookup"><span data-stu-id="d3afb-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="d3afb-117">Voor meer informatie over het configureren van de **entrypoint**, Zie [het beleid voor een toegangspunt voor service-instellingen configureren](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="d3afb-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="d3afb-118">Configureren</span><span class="sxs-lookup"><span data-stu-id="d3afb-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="d3afb-119">Het bouwen van een pakket met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3afb-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="d3afb-120">Als u Visual Studio 2015 gebruikt om uw toepassing te maken, kunt u de pakket-opdracht voor het automatisch maken van een pakket dat overeenkomt met de indeling van de hierboven beschreven.</span><span class="sxs-lookup"><span data-stu-id="d3afb-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="d3afb-121">Voor het maken van een pakket met de rechtermuisknop op de application-project in Solution Explorer en kiest u de opdracht pakket, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d3afb-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Een toepassing met Visual Studio-pakket][vs-package-command]

<span data-ttu-id="d3afb-123">Wanneer het pakket is voltooid, kunt u de locatie van het pakket in vinden de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="d3afb-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="d3afb-124">De stap pakket worden automatisch uitgevoerd wanneer u implementeert of opsporen in uw toepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3afb-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="d3afb-125">Het bouwen van een pakket met de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="d3afb-125">Build a package by command line</span></span>
<span data-ttu-id="d3afb-126">Het is ook mogelijk via een programma wordt gebruikt door uw toepassing verpakken `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="d3afb-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="d3afb-127">Achter de schermen Visual Studio wordt uitgevoerd het zodat de uitvoer hetzelfde is.</span><span class="sxs-lookup"><span data-stu-id="d3afb-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="d3afb-128">Het pakket testen</span><span class="sxs-lookup"><span data-stu-id="d3afb-128">Test the package</span></span>
<span data-ttu-id="d3afb-129">U kunt de pakketstructuur lokaal via PowerShell controleren met behulp van de [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d3afb-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="d3afb-130">Met deze opdracht controleert manifest bij het parseren van problemen en controleer of alle verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="d3afb-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="d3afb-131">Met deze opdracht controleert alleen of de structurele juistheid van de mappen en bestanden in het pakket.</span><span class="sxs-lookup"><span data-stu-id="d3afb-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="d3afb-132">Het niet controleren of een van de pakketinhoud code of gegevens buiten de controleren of alle vereiste bestanden aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="d3afb-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="d3afb-133">Deze fout ziet u dat de *MySetup.bat* bestand waarnaar wordt verwezen in het servicemanifest **entrypoint** ontbreekt in het codepakket.</span><span class="sxs-lookup"><span data-stu-id="d3afb-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="d3afb-134">Nadat het ontbrekende bestand is toegevoegd, wordt de controle van toepassingen wordt doorgegeven:</span><span class="sxs-lookup"><span data-stu-id="d3afb-134">After the missing file is added, the application verification passes:</span></span>

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

<span data-ttu-id="d3afb-135">Als uw toepassing [toepassingsparameters](service-fabric-manage-multiple-environment-app-configuration.md) gedefinieerd, kunt u ze in doorgeven [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) voor de juiste validatie.</span><span class="sxs-lookup"><span data-stu-id="d3afb-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="d3afb-136">Als u het cluster waarop de toepassing wordt geïmplementeerd, kunt u doorgeeft in de `ImageStoreConnectionString` parameter.</span><span class="sxs-lookup"><span data-stu-id="d3afb-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="d3afb-137">Het pakket wordt in dit geval ook gevalideerd met eerdere versies van de toepassing die al in het cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d3afb-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="d3afb-138">Bijvoorbeeld: de validatie kan detecteren of een pakket met dezelfde versie maar verschillende inhoud al is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d3afb-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="d3afb-139">Als de toepassing correct wordt verpakt en is gevalideerd, evalueren op basis van de grootte en het aantal bestanden als compressie is vereist.</span><span class="sxs-lookup"><span data-stu-id="d3afb-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="d3afb-140">Een pakket comprimeren</span><span class="sxs-lookup"><span data-stu-id="d3afb-140">Compress a package</span></span>
<span data-ttu-id="d3afb-141">Wanneer een pakket grote of veel bestanden heeft, kunt u het comprimeren voor een snellere implementatie.</span><span class="sxs-lookup"><span data-stu-id="d3afb-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="d3afb-142">Compressie vermindert het aantal bestanden en de grootte van het pakket.</span><span class="sxs-lookup"><span data-stu-id="d3afb-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="d3afb-143">Voor een gecomprimeerde toepassingspakket [uploaden van het toepassingspakket](service-fabric-deploy-remove-applications.md#upload-the-application-package) kan het langer duren vergeleken met het uploaden van de niet-gecomprimeerde pakket (speciaal als compressie tijd zijn meeberekend), maar [registreren](service-fabric-deploy-remove-applications.md#register-the-application-package)en [afmelden het toepassingstype](service-fabric-deploy-remove-applications.md#unregister-an-application-type) voor een gecomprimeerde pakket sneller zijn.</span><span class="sxs-lookup"><span data-stu-id="d3afb-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="d3afb-144">Het mechanisme deployment is hetzelfde voor gecomprimeerde en ongecomprimeerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="d3afb-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="d3afb-145">Als het pakket is gecomprimeerd, wordt deze als zodanig in het archief van de cluster-installatiekopie is opgeslagen en wordt deze op het knooppunt wordt gedecomprimeerd voordat de toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d3afb-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="d3afb-146">De compressie vervangt het geldig Service Fabric-pakket met de gecomprimeerde versie.</span><span class="sxs-lookup"><span data-stu-id="d3afb-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="d3afb-147">De map moet schrijfmachtigingen toestaan.</span><span class="sxs-lookup"><span data-stu-id="d3afb-147">The folder must allow write permissions.</span></span> <span data-ttu-id="d3afb-148">Compressie uitgevoerd op een al gecomprimeerde pakket levert geen wijzigingen aangebracht.</span><span class="sxs-lookup"><span data-stu-id="d3afb-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="d3afb-149">U kunt een pakket met de Powershell-opdracht comprimeren [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) met `CompressPackage` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3afb-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="d3afb-150">U kunt het pakket met dezelfde decomprimeren opdracht met behulp `UncompressPackage` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3afb-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="d3afb-151">De volgende opdracht wordt het pakket gecomprimeerd zonder kopiëren naar de image store.</span><span class="sxs-lookup"><span data-stu-id="d3afb-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="d3afb-152">U kunt een gecomprimeerde pakket kopiëren naar een of meer Service Fabric-clusters, indien nodig, met behulp van [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) zonder de `SkipCopy` vlag.</span><span class="sxs-lookup"><span data-stu-id="d3afb-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="d3afb-153">Het pakket bevat nu ZIP-bestanden voor de `code`, `config`, en `data` pakketten.</span><span class="sxs-lookup"><span data-stu-id="d3afb-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="d3afb-154">Het toepassingsmanifest en de manifesten voor de service zijn niet ingepakte, omdat ze nodig zijn voor veel interne bewerkingen (zoals pakket delen, een toepassing de naam en versie extraheren voor bepaalde validaties).</span><span class="sxs-lookup"><span data-stu-id="d3afb-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="d3afb-155">Comprimeren van de manifesten zouden deze bewerkingen niet efficiënt.</span><span class="sxs-lookup"><span data-stu-id="d3afb-155">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="d3afb-156">U kunt ook comprimeren en kopieer het pakket met [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in één stap.</span><span class="sxs-lookup"><span data-stu-id="d3afb-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="d3afb-157">Als het pakket groot is, geeft u een hoog genoeg time-out zodat de tijd voor de compressie van het pakket en voor het uploaden naar het cluster.</span><span class="sxs-lookup"><span data-stu-id="d3afb-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="d3afb-158">Service Fabric berekent intern controlesommen voor de toepassingspakketten voor validatie.</span><span class="sxs-lookup"><span data-stu-id="d3afb-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="d3afb-159">Bij gebruik van compressie, worden de controlesommen berekend op de gecomprimeerde versies van elk pakket.</span><span class="sxs-lookup"><span data-stu-id="d3afb-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="d3afb-160">Als u een niet-gecomprimeerde versie van het toepassingspakket gekopieerd en u wilt gebruik compressie voor hetzelfde pakket, moet u de versies van de `code`, `config`, en `data` pakketten om te voorkomen dat checksum komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="d3afb-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="d3afb-161">Als de pakketten niet gewijzigd in plaats van de versie wijzigen zijn, kunt u [diff inrichting](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="d3afb-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="d3afb-162">Met deze optie wordt het pakket ongewijzigd niet opnemen in plaats daarvan ernaar verwijzen vanuit het servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="d3afb-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="d3afb-163">Als u een gecomprimeerde versie van het pakket hebt geüpload en u wilt een niet-gecomprimeerde pakket gebruiken, moet u ook de versies om te voorkomen dat de checksum komt niet overeen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d3afb-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="d3afb-164">Het pakket is nu correct verpakt, gevalideerd en gecomprimeerd (indien nodig), zodat deze gereed is voor [implementatie](service-fabric-deploy-remove-applications.md) op een of meer Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="d3afb-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="d3afb-165">Comprimeren van pakketten bij het implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3afb-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="d3afb-166">U kunt opgeven dat Visual Studio te comprimeren van pakketten op implementatie door toe te voegen de `CopyPackageParameters` element dat u wilt uw publicatieprofiel en stel de `CompressPackage` kenmerk `true`.</span><span class="sxs-lookup"><span data-stu-id="d3afb-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="d3afb-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3afb-167">Next steps</span></span>
<span data-ttu-id="d3afb-168">[Implementeren en toepassingen verwijderen] [ 10] wordt beschreven hoe u PowerShell gebruiken voor het beheren van toepassingsexemplaren</span><span class="sxs-lookup"><span data-stu-id="d3afb-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="d3afb-169">[Het beheren van parameters voor de toepassing voor omgevingen met meerdere] [ 11] wordt beschreven hoe u parameters en variabelen voor exemplaren van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3afb-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="d3afb-170">[Beveiligingsbeleid voor uw toepassing configureert] [ 12] wordt beschreven hoe u services onder het beveiligingsbeleid om toegang te beperken.</span><span class="sxs-lookup"><span data-stu-id="d3afb-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
