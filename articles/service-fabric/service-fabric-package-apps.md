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
# <a name="package-an-application"></a>Een toepassing van het pakket
Dit artikel wordt beschreven hoe toopackage een Service Fabric-toepassing, waardoor het gereed is voor implementatie.

## <a name="package-layout"></a>Lay-out
Hallo-toepassingsmanifest, een of meer service-manifesten en andere benodigde pakket bestanden moeten worden opgeslagen in een specifieke indeling voor implementatie in een Service Fabric-cluster. Hallo voorbeeld manifesten in dit artikel moet toobe georganiseerd in Hallo directory-structuur te volgen:

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

Hallo mappen zijn benoemde toomatch hello **naam** kenmerken van elk element in de bijbehorende. Bijvoorbeeld, als hello servicemanifest bevat twee code pakketten met Hallo namen **MyCodeA** en **MyCodeB**, en vervolgens twee mappen met dezelfde namen zou bevatten Hallo Hallo nodig binaire bestanden voor elke code het pakket.

## <a name="use-setupentrypoint"></a>Entrypoint gebruiken
Typische scenario's voor het gebruik van **entrypoint** zijn wanneer u toorun een uitvoerbaar bestand voordat Hallo-service wordt gestart dient of u tooperform een bewerking met verhoogde bevoegdheden moet. Bijvoorbeeld:

* In te stellen en het initialiseren van omgevingsvariabelen die Hallo service uitvoerbare behoeften. Het is niet beperkt tooonly uitvoerbare bestanden via Hallo Service Fabric-programmeermodellen geschreven. Npm.exe moet bijvoorbeeld een aantal omgevingsvariabelen die is geconfigureerd voor het implementeren van een node.js-toepassing.
* Instellen van toegangsbeheer door beveiligingscertificaten te installeren.

Voor meer informatie over het tooconfigure hello **entrypoint**, Zie [Hallo beleid configureren voor een service-instelling toegangspunt.](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Configureren
### <a name="build-a-package-by-using-visual-studio"></a>Het bouwen van een pakket met behulp van Visual Studio
Als u uw toepassing toocreate Visual Studio 2015 gebruikt, kunt u Hallo pakket opdracht tooautomatically een pakket maakt dat overeenkomt met de Hallo lay-out die hierboven worden beschreven.

toocreate een pakket met de rechtermuisknop op Hallo application-project in Solution Explorer en kiest Hallo pakket, zoals hieronder wordt weergegeven:

![Een toepassing met Visual Studio-pakket][vs-package-command]

Wanneer verpakking voltooid is, kunt u Hallo-locatie van het Hallo-pakket vinden in Hallo **uitvoer** venster. Hallo verpakking stap gebeurt automatisch wanneer u implementeert of opsporen in uw toepassing in Visual Studio.

### <a name="build-a-package-by-command-line"></a>Het bouwen van een pakket met de opdrachtregel
Het is ook mogelijk tooprogrammatically pakket van uw toepassing met `msbuild.exe`. Achter de schermen hello, Visual Studio wordt uitgevoerd het Hallo-uitvoer is dus dezelfde.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Hallo-testpakket
U kunt Hallo pakketstructuur lokaal via PowerShell controleren met behulp van Hallo [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) opdracht.
Met deze opdracht controleert manifest bij het parseren van problemen en controleer of alle verwijzingen. Met deze opdracht controleert alleen of Hallo structurele juistheid van Hallo mappen en bestanden in Hallo-pakket.
Er niet gecontroleerd van Hallo pakketinhoud code of gegevens buiten de controleren of alle vereiste bestanden aanwezig zijn.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Deze fout ziet u dat Hallo *MySetup.bat* bestand waarnaar wordt verwezen in Hallo servicemanifest **entrypoint** ontbreekt in het Hallo-codepakket. Nadat de ontbrekende Hallo-bestand wordt toegevoegd, wordt verificatie van de toepassing hello doorgegeven:

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

Als uw toepassing [toepassingsparameters](service-fabric-manage-multiple-environment-app-configuration.md) gedefinieerd, kunt u ze in doorgeven [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) voor de juiste validatie.

Als u Hallo cluster waarop de toepassing hello wordt geïmplementeerd weet, kunt u doorgeeft in Hallo `ImageStoreConnectionString` parameter. Hallo-pakket is in dit geval ook gevalideerd met eerdere versies van de toepassing hello die al in het Hallo-cluster worden uitgevoerd. Bijvoorbeeld, Hallo validatie kan detecteren of een pakket met de Hallo dezelfde versie, maar verschillende inhoud al is geïmplementeerd.  

Zodra de toepassing hello correct wordt verpakt en is gevalideerd, evalueren op basis van Hallo grootte en het aantal bestanden Hallo als compressie is vereist.

## <a name="compress-a-package"></a>Een pakket comprimeren
Wanneer een pakket grote of veel bestanden heeft, kunt u het comprimeren voor een snellere implementatie. Compressie vermindert Hallo aantal bestanden en Hallo pakketgrootte.
Voor een gecomprimeerde toepassingspakket [Uploading Hallo toepassingspakket](service-fabric-deploy-remove-applications.md#upload-the-application-package) duurt langer dan toouploading Hallo niet-gecomprimeerde pakket (speciaal als compressie tijd zijn meeberekend), maar [registreren](service-fabric-deploy-remove-applications.md#register-the-application-package) en [afmelden Hallo toepassingstype](service-fabric-deploy-remove-applications.md#unregister-an-application-type) voor een gecomprimeerde pakket sneller zijn.

Hallo-mechanisme voor clientimplementatie is hetzelfde voor gecomprimeerde en ongecomprimeerde pakketten. Hallo-pakket is gecomprimeerd, wordt deze opgeslagen als zodanig in Hallo cluster image store als deze niet op Hallo knooppunt gecomprimeerd voordat de toepassing hello wordt uitgevoerd.
Hallo compressie vervangt Hallo geldig Service Fabric-pakket door Hallo gecomprimeerde versie. Hallo map moet schrijfmachtigingen toestaan. Compressie uitgevoerd op een al gecomprimeerde pakket levert geen wijzigingen aangebracht.

U kunt een pakket met de Powershell-opdracht Hallo comprimeren [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) met `CompressPackage` overschakelen. U kunt Hallo decomprimeren van het pakket met de Hallo dezelfde opdracht met behulp `UncompressPackage` overschakelen.

Hallo volgende opdracht worden gecomprimeerd Hallo pakket zonder deze toohello image store. U kunt een gecomprimeerde pakket tooone of meer Service Fabric-clusters, kopiëren, indien nodig, met behulp van [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) zonder Hallo `SkipCopy` vlag.
Hallo-pakket bevat nu ZIP-bestanden voor Hallo `code`, `config`, en `data` pakketten. Hallo-toepassingsmanifest en Hallo service manifesten zijn niet ingepakte, omdat ze nodig zijn voor veel interne bewerkingen (zoals pakket delen van de toepassing de naam en versie extraheren voor bepaalde validaties).
Hallo manifesten comprimeren zouden deze bewerkingen niet efficiënt.

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

U kunt ook comprimeren en kopieer het pakket met Hallo [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in één stap.
Als Hallo pakket groot is, geeft u een hoog genoeg time-out tooallow tijd voor zowel Hallo pakket compressie en Hallo uploaden toohello cluster.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Service Fabric berekent intern controlesommen voor toepassingspakketten Hallo voor validatie. Bij gebruik van compressie, worden de Hallo controlesommen berekend op Hallo ingepakte versies van elk pakket.
Als u een niet-gecomprimeerde versie van het toepassingspakket hebt gekopieerd, en u toouse compressie voor Hallo wilt hetzelfde pakket, moet u Hallo versies van Hallo `code`, `config`, en `data` pakketten tooavoid checksum komt niet overeen. Als hello-pakketten ongewijzigd zijn, in plaats van Hallo versie wijzigen, kunt u [diff inrichting](service-fabric-application-upgrade-advanced.md). Met deze optie Hallo ongewijzigd pakket niet opnemen in plaats daarvan ernaar verwijzen vanuit Hallo servicemanifest.

Als u een gecomprimeerde versie van pakket Hallo geüpload en u wilt dat een niet-gecomprimeerde pakket toouse, moet u op dezelfde manier Hallo versies tooavoid Hallo checksum komt niet overeen bijwerken.

Hallo pakket is nu correct verpakt, gevalideerd en gecomprimeerd (indien nodig), zodat deze gereed is voor [implementatie](service-fabric-deploy-remove-applications.md) tooone of meer Service Fabric-clusters.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Comprimeren van pakketten bij het implementeren met Visual Studio
U kunt opgeven dat Visual Studio toocompress pakketten op implementatie door toe te voegen Hallo `CopyPackageParameters` element tooyour publicatieprofiel en stel Hallo `CompressPackage` kenmerk te`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Volgende stappen
[Implementeren en toepassingen verwijderen] [ 10] wordt beschreven hoe toouse PowerShell toomanage toepassingsexemplaren

[Het beheren van parameters voor de toepassing voor omgevingen met meerdere] [ 11] wordt beschreven hoe tooconfigure parameters en variabelen voor exemplaren van een andere toepassing.

[Beveiligingsbeleid voor uw toepassing configureert] [ 12] wordt beschreven hoe toorun services onder beveiligingstoegang beleid toorestrict.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
