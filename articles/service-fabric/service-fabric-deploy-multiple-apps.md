---
title: een Node.js-toepassing die gebruikmaakt van MongoDB aaaDeploy | Microsoft Docs
description: Overzicht over het toopackage meerdere Gast uitvoerbare bestanden toodeploy tooan Azure Service Fabric-cluster
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="fa83f-103">Meerdere toepassingen implementeren die door gasten kunnen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="fa83f-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="fa83f-104">Dit artikel laat zien hoe toopackage en implementeren van meerdere Gast uitvoerbare bestanden tooAzure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fa83f-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="fa83f-105">Voor Lees hoe te maken en implementeren van één Service Fabric-pakket[implementeren van een gast uitvoerbare tooService Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa83f-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="fa83f-106">Hoewel dit overzicht hoe een toepassing met een Node.js-front-end dat MongoDB als gegevensarchief Hallo gebruikt toodeploy, u kunt toepassen Hallo stappen tooany toepassing die afhankelijk van een andere toepassing toont is.</span><span class="sxs-lookup"><span data-stu-id="fa83f-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="fa83f-107">U kunt Visual Studio tooproduce Hallo toepassingspakket met meerdere Gast uitvoerbare bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa83f-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="fa83f-108">Zie [toopackage Visual Studio met behulp van een bestaande toepassing](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa83f-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="fa83f-109">Wanneer u Hallo eerste Gast uitvoerbaar bestand hebt toegevoegd, klik met de rechtermuisknop op Hallo application-project en selecteer Hallo **toevoegen -> nieuwe Service Fabric-service** tooadd Hallo tweede Gast uitvoerbare project toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="fa83f-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="fa83f-110">Opmerking: Als u ervoor kiest toolink Hallo-bron in Visual Studio-project Hallo Visual Studio-oplossing bouwen Hallo zorgt ervoor dat het toepassingspakket is up toodate met wijzigingen in de Hallo bron.</span><span class="sxs-lookup"><span data-stu-id="fa83f-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="fa83f-111">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="fa83f-111">Samples</span></span>
* [<span data-ttu-id="fa83f-112">Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="fa83f-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="fa83f-113">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="fa83f-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="fa83f-114">Handmatig pakket meerdere Gast uitvoerbare toepassing hello</span><span class="sxs-lookup"><span data-stu-id="fa83f-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="fa83f-115">U kunt ook handmatig Hallo Gast uitvoerbare verpakken.</span><span class="sxs-lookup"><span data-stu-id="fa83f-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="fa83f-116">Voor handmatige hello-pakketten, in dit artikel gebruikt Hallo Service Fabric-verpakking hulpprogramma, dat beschikbaar is op [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="fa83f-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="fa83f-117">Verpakking Hallo Node.js-toepassing</span><span class="sxs-lookup"><span data-stu-id="fa83f-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="fa83f-118">In dit artikel wordt ervan uitgegaan dat Node.js niet is geïnstalleerd op de knooppunten Hallo in Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="fa83f-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="fa83f-119">Als gevolg hiervan moet u tooadd Node.exe toohello hoofdmap van uw knooppunttoepassing voordat pakketten.</span><span class="sxs-lookup"><span data-stu-id="fa83f-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="fa83f-120">Hallo directorystructuur van Hallo Node.js-toepassing (met behulp van de Express-webframework en Jade sjabloon engine) ziet vergelijkbare toohello een hieronder:</span><span class="sxs-lookup"><span data-stu-id="fa83f-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="fa83f-121">Een volgende stap moet u een toepassingspakket voor Hallo Node.js-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="fa83f-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="fa83f-122">Hallo-code hieronder maakt u een Service Fabric-toepassingspakket dat Hallo Node.js-toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="fa83f-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="fa83f-123">Hieronder volgt een beschrijving van Hallo-parameters die worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fa83f-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="fa83f-124">**/ source** punten toohello map van het Hallo-toepassing die moet worden verpakt.</span><span class="sxs-lookup"><span data-stu-id="fa83f-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="fa83f-125">**/ target** definieert Hallo directory aan welke Hallo pakket moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa83f-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="fa83f-126">Deze map heeft toobe verschilt van de bronmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa83f-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="fa83f-127">**/ AppName** Hallo toepassingsnaam van de bestaande toepassing hello definieert.</span><span class="sxs-lookup"><span data-stu-id="fa83f-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="fa83f-128">Het is belangrijk toounderstand dit toohello servicenaam in het manifest Hallo en niet toohello Service Fabric toepassingsnaam vertaalt.</span><span class="sxs-lookup"><span data-stu-id="fa83f-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="fa83f-129">**exe** definieert Hallo uitvoerbare dat Service Fabric toolaunch, in dit geval moet `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="fa83f-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="fa83f-130">**/ma** Hallo-argument dat gebruikt toolaunch Hallo uitvoerbare wordt definieert.</span><span class="sxs-lookup"><span data-stu-id="fa83f-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="fa83f-131">Als Node.js niet is geïnstalleerd, Service Fabric toolaunch hello Node.js-webserver moet door het uitvoeren van `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="fa83f-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="fa83f-132">`/ma:'bin/www'`Hallo verpakking hulpprogramma toouse vertelt `bin/ma` als argument voor node.exe Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa83f-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="fa83f-133">**/ AppType** definieert Hallo Service Fabric-toepassing-typenaam.</span><span class="sxs-lookup"><span data-stu-id="fa83f-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="fa83f-134">Als u toohello map die is opgegeven in de parameter/target Hallo bladert, ziet u dat hulpprogramma Hallo een volledig werkend Service Fabric-pakket is gemaakt, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="fa83f-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="fa83f-135">Hallo gegenereerde ServiceManifest.xml nu een sectie waarin wordt beschreven hoe Hallo Node.js-web-server moet worden gestart heeft, zoals wordt weergegeven in onderstaande Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="fa83f-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="fa83f-136">In dit voorbeeld Hallo Node.js-webserver, luistert tooport 3000, dus u informatie over de endpoint tooupdate Hallo in Hallo ServiceManifest.xml bestand moet zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa83f-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="fa83f-137">Verpakking Hallo MongoDB-toepassing</span><span class="sxs-lookup"><span data-stu-id="fa83f-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="fa83f-138">Nu dat u de Node.js-toepassing hello ingepakt hebt, kunt u doorgaan en MongoDB-pakket.</span><span class="sxs-lookup"><span data-stu-id="fa83f-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="fa83f-139">Zoals al eerder vermeld, Hallo stappen die u hebt nu doorlopen zijn niet specifiek tooNode.js en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fa83f-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="fa83f-140">Deze toepassing in feite tooall toepassingen die zijn bedoeld toobe verpakt in een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa83f-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="fa83f-141">toopackage MongoDB, wilt u zeker dat u het pakket Mongod.exe en Mongo.exe toomake.</span><span class="sxs-lookup"><span data-stu-id="fa83f-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="fa83f-142">Beide binaire bestanden bevinden zich in Hallo `bin` map van de installatiemap van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fa83f-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="fa83f-143">Hallo-mapstructuur lijkt vergelijkbare toohello een hieronder.</span><span class="sxs-lookup"><span data-stu-id="fa83f-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="fa83f-144">Service Fabric moet toostart MongoDB met een opdracht vergelijkbare toohello een hieronder, dus u toouse hello moet `/ma` parameter door bij het verpakken van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fa83f-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="fa83f-145">Hallo-gegevens is niet wordt behouden in geval van storing op een knooppunt Hallo Hallo MongoDB-gegevensmap te plaatsen op de lokale directory Hallo van Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fa83f-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="fa83f-146">U moet duurzame opslag gebruiken of een MongoDB replicaset volgorde tooprevent gegevens verloren gaan implementeren.</span><span class="sxs-lookup"><span data-stu-id="fa83f-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="fa83f-147">In PowerShell of Hallo opdrachtshell uitvoeren we Hallo verpakking hulpprogramma met Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="fa83f-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="fa83f-148">In de volgorde tooadd MongoDB tooyour Service Fabric-toepassingspakket, moet u ervoor dat parameter Hallo/TARGET verwijst toohello toomake dezelfde directory waarmee bevat al een toepassingsmanifest Hallo samen met de Hallo Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa83f-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="fa83f-149">U moet ook toomake zeker dat u gebruikmaakt van dezelfde ApplicationType naam Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa83f-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="fa83f-150">We gaan bladeren door mappen toohello en onderzoeken welke hulpprogramma Hallo heeft gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa83f-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="fa83f-151">Zoals u ziet, toegevoegd Hallo hulpprogramma een nieuwe map, MongoDB, toohello map die Hallo MongoDB-binaire bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="fa83f-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="fa83f-152">Als u Hallo openen `ApplicationManifest.xml` -bestand, kunt u zien dat Hallo-pakket bevat nu de Node.js-toepassing hello en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fa83f-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="fa83f-153">Hallo-code hieronder toont Hallo inhoud van het Hallo-toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="fa83f-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="fa83f-154">Publishing Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="fa83f-154">Publishing hello application</span></span>
<span data-ttu-id="fa83f-155">de laatste stap Hallo is toopublish Hallo toepassing toohello lokale Service Fabric-cluster met behulp van de onderstaande Hallo PowerShell-scripts:</span><span class="sxs-lookup"><span data-stu-id="fa83f-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="fa83f-156">Zodra de toepassing hello is met succes gepubliceerde toohello lokale cluster, kunt u de Node.js-toepassing hello op Hallo-poort die we hebben ingevoerd in Hallo servicemanifest van Hallo Node.js-toepassing--bijvoorbeeld http://localhost: 3000 openen.</span><span class="sxs-lookup"><span data-stu-id="fa83f-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="fa83f-157">In deze zelfstudie hebt u gezien hoe tooeasily twee bestaande toepassingen pakket als een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa83f-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="fa83f-158">U hebt geleerd hoe toodeploy het tooService Fabric zodanig dat deze van sommige Hallo Service Fabric-functies, zoals hoge beschikbaarheid en health system-integratie profiteren kan.</span><span class="sxs-lookup"><span data-stu-id="fa83f-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="fa83f-159">Meer Gast uitvoerbare bestanden tooan bestaande toepassing toevoegen met behulp van Yeoman op Linux</span><span class="sxs-lookup"><span data-stu-id="fa83f-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="fa83f-160">tooadd een andere service tooan toepassing al gemaakt met behulp van `yo`, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="fa83f-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="fa83f-161">Toohello hoofdmap van de bestaande toepassing hello wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fa83f-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="fa83f-162">Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fa83f-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="fa83f-163">Voer `yo azuresfguest:AddService` en de benodigde informatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa83f-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa83f-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa83f-164">Next steps</span></span>
* <span data-ttu-id="fa83f-165">Meer informatie over het implementeren van containers met [overzicht van Service Fabric en containers](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fa83f-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="fa83f-166">Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="fa83f-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="fa83f-167">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="fa83f-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
