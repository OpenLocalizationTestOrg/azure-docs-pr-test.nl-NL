---
title: Een Node.js-toepassing die gebruikmaakt van MongoDB implementeren | Microsoft Docs
description: Overzicht over het pakket meerdere Gast uitvoerbare bestanden naar een Azure Service Fabric-cluster implementeren
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
ms.openlocfilehash: b71723034e5f663986c49481072bfd6779d3d57b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="8bfb8-103">Meerdere toepassingen implementeren die door gasten kunnen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="8bfb8-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="8bfb8-104">In dit artikel laat zien hoe verpakken en distribueren van meerdere Gast uitvoerbare bestanden naar de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span></span> <span data-ttu-id="8bfb8-105">Voor het maken en implementeren van één Service Fabric-pakket leest u hoe aan [uitvoerbare Gast implementeren op Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="8bfb8-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="8bfb8-106">Terwijl dit overzicht hoe een toepassing met een Node.js-front-end dat u MongoDB als het gegevensarchief gebruikt implementeren toont, kunt u de stappen toepassen op alle toepassingen die afhankelijk van een andere toepassing is.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span></span>   

<span data-ttu-id="8bfb8-107">U kunt Visual Studio gebruiken voor het produceren van het toepassingspakket dat meerdere Gast uitvoerbare bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span></span> <span data-ttu-id="8bfb8-108">Zie [met behulp van Visual Studio aan het pakket van een bestaande toepassing](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="8bfb8-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="8bfb8-109">Nadat u het eerste uitvoerbare bestand van het gastbesturingssysteem hebt toegevoegd, klik met de rechtermuisknop op het toepassingsproject en selecteer de **toevoegen -> nieuwe Service Fabric-service** het tweede Gast uitvoerbare project toevoegen aan de oplossing.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span></span> <span data-ttu-id="8bfb8-110">Opmerking: Als u de bron is in de Visual Studio-project koppelt, de Visual Studio-oplossing bouwen zorgt ervoor dat het toepassingspakket bijgewerkt met wijzigingen in de bron is.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span></span> 

## <a name="samples"></a><span data-ttu-id="8bfb8-111">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="8bfb8-111">Samples</span></span>
* [<span data-ttu-id="8bfb8-112">Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="8bfb8-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="8bfb8-113">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceren via de Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="8bfb8-113">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-the-multiple-guest-executable-application"></a><span data-ttu-id="8bfb8-114">De meerdere Gast uitvoerbare toepassing handmatig van het pakket</span><span class="sxs-lookup"><span data-stu-id="8bfb8-114">Manually package the multiple guest executable application</span></span>
<span data-ttu-id="8bfb8-115">U kunt ook kunt u handmatig de Gast uitvoerbare pakket.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-115">Alternatively you can manually package the guest executable.</span></span> <span data-ttu-id="8bfb8-116">Voor de handmatige verpakking, het hulpprogramma Service Fabric-pakket, dat beschikbaar is op dit artikel wordt gebruikt [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="8bfb8-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-the-nodejs-application"></a><span data-ttu-id="8bfb8-117">Het verpakken van de Node.js-toepassing</span><span class="sxs-lookup"><span data-stu-id="8bfb8-117">Packaging the Node.js application</span></span>
<span data-ttu-id="8bfb8-118">In dit artikel wordt ervan uitgegaan dat Node.js niet is geïnstalleerd op de knooppunten in het Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span></span> <span data-ttu-id="8bfb8-119">Als gevolg hiervan moet u Node.exe toevoegen aan de hoofdmap van uw knooppunttoepassing voordat de pakketten.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span></span> <span data-ttu-id="8bfb8-120">De mapstructuur van de Node.js-toepassing (met behulp van de Express-webframework en Jade sjabloon engine), moet er ongeveer als hieronder:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span></span>

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

<span data-ttu-id="8bfb8-121">Een volgende stap moet u een pakket voor de Node.js-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-121">As a next step, you create an application package for the Node.js application.</span></span> <span data-ttu-id="8bfb8-122">De code hieronder maakt een Service Fabric-toepassingspakket dat u de Node.js-toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-122">The code below creates a Service Fabric application package that contains the Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="8bfb8-123">Hieronder volgt een beschrijving van de parameters die worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-123">Below is a description of the parameters that are being used:</span></span>

* <span data-ttu-id="8bfb8-124">**/ source** verwijst naar de map van de toepassing die moet worden verpakt.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-124">**/source** points to the directory of the application that should be packaged.</span></span>
* <span data-ttu-id="8bfb8-125">**/ target** definieert u de map waarin het pakket moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-125">**/target** defines the directory in which the package should be created.</span></span> <span data-ttu-id="8bfb8-126">Deze map moet afwijken van de bronmap.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-126">This directory has to be different from the source directory.</span></span>
* <span data-ttu-id="8bfb8-127">**/ AppName** definieert de naam van de toepassing van de bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-127">**/appname** defines the application name of the existing application.</span></span> <span data-ttu-id="8bfb8-128">Het is belangrijk om te begrijpen dat dit komt neer op de servicenaam in het manifest en niet op de naam van de Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span></span>
* <span data-ttu-id="8bfb8-129">**exe** definieert het uitvoerbare bestand dat de Service Fabric behoort te starten in dit geval `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span></span>
* <span data-ttu-id="8bfb8-130">**/ma** het argument dat wordt gebruikt voor het starten van het uitvoerbare bestand definieert.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-130">**/ma** defines the argument that is being used to launch the executable.</span></span> <span data-ttu-id="8bfb8-131">Als Node.js niet is geïnstalleerd, Service Fabric moet de Node.js-webserver start door te voeren `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="8bfb8-132">`/ma:'bin/www'`vertelt verpakking hulpprogramma gebruikt `bin/ma` als het argument voor node.exe.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span></span>
* <span data-ttu-id="8bfb8-133">**/ AppType** definieert de naam van het Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-133">**/AppType** defines the Service Fabric application type name.</span></span>

<span data-ttu-id="8bfb8-134">Als u de map die is opgegeven in de parameter/target bladert, ziet u dat het hulpprogramma een volledig werkend Service Fabric-pakket is gemaakt, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="8bfb8-135">De gegenereerde ServiceManifest.xml heeft nu een sectie waarin wordt beschreven hoe de Node.js-web-server moet worden gestart, zoals wordt weergegeven in het onderstaande codefragment:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span></span>

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
<span data-ttu-id="8bfb8-136">In dit voorbeeld luistert de Node.js-webserver op poort 3000, dus moet u het bijwerken van de endpoint-informatie in het bestand ServiceManifest.xml zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-the-mongodb-application"></a><span data-ttu-id="8bfb8-137">Het verpakken van de MongoDB-toepassing</span><span class="sxs-lookup"><span data-stu-id="8bfb8-137">Packaging the MongoDB application</span></span>
<span data-ttu-id="8bfb8-138">Nu dat u de Node.js-toepassing ingepakt hebt, kunt u doorgaan en MongoDB-pakket.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="8bfb8-139">Zoals al eerder vermeld, zijn de stappen die u hebt nu doorlopen niet specifiek zijn voor Node.js en MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span></span> <span data-ttu-id="8bfb8-140">In feite ze gelden voor alle toepassingen die zijn bedoeld om samen als één Service Fabric-toepassing worden verpakt.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="8bfb8-141">Als u wilt inpakken MongoDB, die u wilt Zorg ervoor dat u het pakket Mongod.exe en Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="8bfb8-142">Beide binaire bestanden bevinden zich in de `bin` map van de installatiemap van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="8bfb8-143">De mapstructuur lijkt op hieronder.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-143">The directory structure looks similar to the one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="8bfb8-144">Service Fabric moet MongoDB beginnen met een opdracht vergelijkbaar met die hieronder, zodat u wilt gebruiken, de `/ma` parameter door bij het verpakken van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path to data]
```
> [!NOTE]
> <span data-ttu-id="8bfb8-145">De gegevens is niet het geval van storing op een knooppunt wordt behouden als u de MongoDB-gegevensmap op de lokale map van het knooppunt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span></span> <span data-ttu-id="8bfb8-146">U moet duurzame opslag gebruiken of implementeren van een replicaset MongoDB om gegevensverlies te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span></span>  
>
>

<span data-ttu-id="8bfb8-147">In PowerShell of de opdrachtshell uitvoeren we het verpakking-hulpprogramma met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

<span data-ttu-id="8bfb8-148">U moet MongoDB toevoegen aan uw Service Fabric-toepassingspakket, zorg ervoor dat de parameter/target naar dezelfde directory waarmee al de toepassing bevat verwijst samen met de Node.js-toepassing manifest.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span></span> <span data-ttu-id="8bfb8-149">U moet ook om ervoor te zorgen dat u van dezelfde ApplicationType naam gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-149">You also need to make sure that you are using the same ApplicationType name.</span></span>

<span data-ttu-id="8bfb8-150">Laten we Blader naar de map en onderzoeken van wat het hulpprogramma heeft gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-150">Let's browse to the directory and examine what the tool has created.</span></span>

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
<span data-ttu-id="8bfb8-151">Zoals u ziet, wordt met het hulpprogramma een nieuwe map, MongoDB, toegevoegd aan de map waarin de binaire bestanden voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span></span> <span data-ttu-id="8bfb8-152">Als u opent de `ApplicationManifest.xml` -bestand, kunt u zien dat het pakket nu de Node.js-toepassing en de MongoDB bevat.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span></span> <span data-ttu-id="8bfb8-153">De volgende code toont de inhoud van het toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-153">The code below shows the content of the application manifest.</span></span>

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

### <a name="publishing-the-application"></a><span data-ttu-id="8bfb8-154">De toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="8bfb8-154">Publishing the application</span></span>
<span data-ttu-id="8bfb8-155">De laatste stap is het publiceren van de toepassing naar de lokale Service Fabric-cluster met behulp van de onderstaande PowerShell-scripts:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="8bfb8-156">Zodra de toepassing is gepubliceerd naar het lokale cluster, kunt u de Node.js-toepassing op de poort die we hebben ingevoerd in het servicemanifest van de Node.js-toepassing bijvoorbeeld http://localhost: 3000 openen.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="8bfb8-157">In deze zelfstudie hebt u gezien hoe eenvoudig het verpakken van twee bestaande toepassingen als een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="8bfb8-158">U hebt ook geleerd implementeren naar Service Fabric, zodat deze van enkele van de Service Fabric-functies, zoals hoge beschikbaarheid en health systeemintegratie profiteren kan.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-to-an-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="8bfb8-159">Meer Gast uitvoerbare bestanden toe te voegen aan een bestaande toepassing Yeoman met op Linux</span><span class="sxs-lookup"><span data-stu-id="8bfb8-159">Adding more guest executables to an existing application using Yeoman on Linux</span></span>

<span data-ttu-id="8bfb8-160">Voer de volgende stappen uit als u nog een service wilt toevoegen aan een toepassing die al is gemaakt met `yo`:</span><span class="sxs-lookup"><span data-stu-id="8bfb8-160">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="8bfb8-161">Stel de directory in op de hoofdmap van de bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-161">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="8bfb8-162">Bijvoorbeeld `cd ~/YeomanSamples/MyApplication` als `MyApplication` de toepassing is die is gemaakt door Yeoman.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="8bfb8-163">Voer `yo azuresfguest:AddService` en geef de benodigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="8bfb8-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bfb8-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bfb8-164">Next steps</span></span>
* <span data-ttu-id="8bfb8-165">Meer informatie over het implementeren van containers met [overzicht van Service Fabric en containers](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8bfb8-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="8bfb8-166">Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand</span><span class="sxs-lookup"><span data-stu-id="8bfb8-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="8bfb8-167">Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceren via de Naming service met behulp van REST</span><span class="sxs-lookup"><span data-stu-id="8bfb8-167">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
