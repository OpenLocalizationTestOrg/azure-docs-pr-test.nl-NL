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
# <a name="deploy-multiple-guest-executables"></a>Meerdere toepassingen implementeren die door gasten kunnen worden uitgevoerd
Dit artikel laat zien hoe toopackage en implementeren van meerdere Gast uitvoerbare bestanden tooAzure Service Fabric. Voor Lees hoe te maken en implementeren van één Service Fabric-pakket[implementeren van een gast uitvoerbare tooService Fabric](service-fabric-deploy-existing-app.md).

Hoewel dit overzicht hoe een toepassing met een Node.js-front-end dat MongoDB als gegevensarchief Hallo gebruikt toodeploy, u kunt toepassen Hallo stappen tooany toepassing die afhankelijk van een andere toepassing toont is.   

U kunt Visual Studio tooproduce Hallo toepassingspakket met meerdere Gast uitvoerbare bestanden gebruiken. Zie [toopackage Visual Studio met behulp van een bestaande toepassing](service-fabric-deploy-existing-app.md). Wanneer u Hallo eerste Gast uitvoerbaar bestand hebt toegevoegd, klik met de rechtermuisknop op Hallo application-project en selecteer Hallo **toevoegen -> nieuwe Service Fabric-service** tooadd Hallo tweede Gast uitvoerbare project toohello oplossing. Opmerking: Als u ervoor kiest toolink Hallo-bron in Visual Studio-project Hallo Visual Studio-oplossing bouwen Hallo zorgt ervoor dat het toepassingspakket is up toodate met wijzigingen in de Hallo bron. 

## <a name="samples"></a>Voorbeelden
* [Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Handmatig pakket meerdere Gast uitvoerbare toepassing hello
U kunt ook handmatig Hallo Gast uitvoerbare verpakken. Voor handmatige hello-pakketten, in dit artikel gebruikt Hallo Service Fabric-verpakking hulpprogramma, dat beschikbaar is op [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Verpakking Hallo Node.js-toepassing
In dit artikel wordt ervan uitgegaan dat Node.js niet is geïnstalleerd op de knooppunten Hallo in Hallo Service Fabric-cluster. Als gevolg hiervan moet u tooadd Node.exe toohello hoofdmap van uw knooppunttoepassing voordat pakketten. Hallo directorystructuur van Hallo Node.js-toepassing (met behulp van de Express-webframework en Jade sjabloon engine) ziet vergelijkbare toohello een hieronder:

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

Een volgende stap moet u een toepassingspakket voor Hallo Node.js-toepassing maken. Hallo-code hieronder maakt u een Service Fabric-toepassingspakket dat Hallo Node.js-toepassing bevat.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Hieronder volgt een beschrijving van Hallo-parameters die worden gebruikt:

* **/ source** punten toohello map van het Hallo-toepassing die moet worden verpakt.
* **/ target** definieert Hallo directory aan welke Hallo pakket moet worden gemaakt. Deze map heeft toobe verschilt van de bronmap Hallo.
* **/ AppName** Hallo toepassingsnaam van de bestaande toepassing hello definieert. Het is belangrijk toounderstand dit toohello servicenaam in het manifest Hallo en niet toohello Service Fabric toepassingsnaam vertaalt.
* **exe** definieert Hallo uitvoerbare dat Service Fabric toolaunch, in dit geval moet `node.exe`.
* **/ma** Hallo-argument dat gebruikt toolaunch Hallo uitvoerbare wordt definieert. Als Node.js niet is geïnstalleerd, Service Fabric toolaunch hello Node.js-webserver moet door het uitvoeren van `node.exe bin/www`.  `/ma:'bin/www'`Hallo verpakking hulpprogramma toouse vertelt `bin/ma` als argument voor node.exe Hallo.
* **/ AppType** definieert Hallo Service Fabric-toepassing-typenaam.

Als u toohello map die is opgegeven in de parameter/target Hallo bladert, ziet u dat hulpprogramma Hallo een volledig werkend Service Fabric-pakket is gemaakt, zoals hieronder wordt weergegeven:

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
Hallo gegenereerde ServiceManifest.xml nu een sectie waarin wordt beschreven hoe Hallo Node.js-web-server moet worden gestart heeft, zoals wordt weergegeven in onderstaande Hallo codefragment:

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
In dit voorbeeld Hallo Node.js-webserver, luistert tooport 3000, dus u informatie over de endpoint tooupdate Hallo in Hallo ServiceManifest.xml bestand moet zoals hieronder wordt weergegeven.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Verpakking Hallo MongoDB-toepassing
Nu dat u de Node.js-toepassing hello ingepakt hebt, kunt u doorgaan en MongoDB-pakket. Zoals al eerder vermeld, Hallo stappen die u hebt nu doorlopen zijn niet specifiek tooNode.js en MongoDB. Deze toepassing in feite tooall toepassingen die zijn bedoeld toobe verpakt in een Service Fabric-toepassing.  

toopackage MongoDB, wilt u zeker dat u het pakket Mongod.exe en Mongo.exe toomake. Beide binaire bestanden bevinden zich in Hallo `bin` map van de installatiemap van MongoDB. Hallo-mapstructuur lijkt vergelijkbare toohello een hieronder.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric moet toostart MongoDB met een opdracht vergelijkbare toohello een hieronder, dus u toouse hello moet `/ma` parameter door bij het verpakken van MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> Hallo-gegevens is niet wordt behouden in geval van storing op een knooppunt Hallo Hallo MongoDB-gegevensmap te plaatsen op de lokale directory Hallo van Hallo-knooppunt. U moet duurzame opslag gebruiken of een MongoDB replicaset volgorde tooprevent gegevens verloren gaan implementeren.  
>
>

In PowerShell of Hallo opdrachtshell uitvoeren we Hallo verpakking hulpprogramma met Hallo volgende parameters:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

In de volgorde tooadd MongoDB tooyour Service Fabric-toepassingspakket, moet u ervoor dat parameter Hallo/TARGET verwijst toohello toomake dezelfde directory waarmee bevat al een toepassingsmanifest Hallo samen met de Hallo Node.js-toepassing. U moet ook toomake zeker dat u gebruikmaakt van dezelfde ApplicationType naam Hallo.

We gaan bladeren door mappen toohello en onderzoeken welke hulpprogramma Hallo heeft gemaakt.

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
Zoals u ziet, toegevoegd Hallo hulpprogramma een nieuwe map, MongoDB, toohello map die Hallo MongoDB-binaire bestanden bevat. Als u Hallo openen `ApplicationManifest.xml` -bestand, kunt u zien dat Hallo-pakket bevat nu de Node.js-toepassing hello en MongoDB. Hallo-code hieronder toont Hallo inhoud van het Hallo-toepassingsmanifest.

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

### <a name="publishing-hello-application"></a>Publishing Hallo-toepassing
de laatste stap Hallo is toopublish Hallo toepassing toohello lokale Service Fabric-cluster met behulp van de onderstaande Hallo PowerShell-scripts:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Zodra de toepassing hello is met succes gepubliceerde toohello lokale cluster, kunt u de Node.js-toepassing hello op Hallo-poort die we hebben ingevoerd in Hallo servicemanifest van Hallo Node.js-toepassing--bijvoorbeeld http://localhost: 3000 openen.

In deze zelfstudie hebt u gezien hoe tooeasily twee bestaande toepassingen pakket als een Service Fabric-toepassing. U hebt geleerd hoe toodeploy het tooService Fabric zodanig dat deze van sommige Hallo Service Fabric-functies, zoals hoge beschikbaarheid en health system-integratie profiteren kan.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Meer Gast uitvoerbare bestanden tooan bestaande toepassing toevoegen met behulp van Yeoman op Linux

tooadd een andere service tooan toepassing al gemaakt met behulp van `yo`, Hallo volgende stappen uit te voeren: 
1. Toohello hoofdmap van de bestaande toepassing hello wijzigen.  Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.
2. Voer `yo azuresfguest:AddService` en de benodigde informatie Hallo.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over het implementeren van containers met [overzicht van Service Fabric en containers](service-fabric-containers-overview.md)
* [Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
