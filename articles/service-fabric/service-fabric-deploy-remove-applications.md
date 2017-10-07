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
# <a name="deploy-and-remove-applications-using-powershell"></a>Implementeren en verwijderen van toepassingen met behulp van PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient-API's](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Eenmaal een [toepassingstype zijn ingepakt][10], deze gereed is voor implementatie in een Azure Service Fabric-cluster. Implementatie omvat het Hallo drie stappen te volgen:

1. Hallo pakket toohello installatiekopie toepassingsarchief uploaden
2. Registratie van toepassingstype Hallo
3. Exemplaar van de toepassing hello maken

Nadat een toepassing wordt geïmplementeerd en een exemplaar in Hallo-cluster wordt uitgevoerd, kunt u Hallo toepassingsexemplaar en het toepassingstype verwijderen. toocompletely verwijderen een toepassing uit Hallo cluster omvat Hallo stappen te volgen:

1. Met een toepassingsexemplaar van de hello verwijderen (of verwijderen)
2. Hef de registratie van toepassingstype Hallo als u deze niet langer nodig hebt
3. Hallo-toepassingspakket verwijderen uit de installatiekopieopslag Hallo

Als u [Visual Studio voor het implementeren en foutopsporing in toepassingen](service-fabric-publish-app-remote-cluster.md) op uw lokaal ontwikkelcluster alle voorgaande stappen Hallo automatisch via een PowerShell-script worden verwerkt.  Dit script is gevonden in Hallo *Scripts* map van het toepassingsproject Hallo. Dit artikel vindt u achtergrond op script doet zodat u kunt uitvoeren Hallo dezelfde bewerkingen buiten Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello
Voordat u een PowerShell-opdrachten in dit artikel uitvoert, wordt altijd gestart via [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric-cluster. tooconnect toohello lokaal ontwikkelcluster, voert u de volgende Hallo:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Voor voorbeelden van verbindende tooa externe cluster of -cluster beveiligd met Azure Active Directory, X509 certificaten of Windows Active Directory-Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Hallo-toepassingspakket uploaden
Uploaden van het Hallo-toepassingspakket plaatst het in een locatie die toegankelijk is voor interne Service Fabric-onderdelen.
Als u tooverify Hallo toepassingspakket lokaal wilt, gebruikt u Hallo [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Hallo [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht uploads Hallo pakket toohello cluster installatiekopie toepassingsarchief.
Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.  tooimport hello SDK-module, uitvoeren:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Stel dat u maakt en een toepassing met de naam van het pakket *Mijntoepassing* in Visual Studio 2015. Standaard is Hallo naam van het toepassingstype die worden vermeld in Hallo ApplicationManifest.xml 'MyApplicationType'.  Hallo-toepassingspakket dat manifest van de benodigde toepassing hello, manifesten service en config-code-gegevens pakketten bevat, zich in *C:\Users\<gebruikersnaam\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*. 

Hallo volgende opdracht worden Hallo inhoud van het toepassingspakket Hallo:

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

Als het Hallo-toepassingspakket is groot en/of veel bestanden, kunt u [comprimeert](service-fabric-package-apps.md#compress-a-package). Hallo compressie vermindert Hallo grootte en het aantal bestanden Hallo.
Hallo neveneffect is dat Hallo registreren en afmelden toepassingstype zijn sneller. Uploadtijd trager worden momenteel, met name als u Hallo tijd toocompress Hallo pakket opnemen. 

een pakket, gebruik toocompress Hallo dezelfde [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht. Compressie kan worden gedaan afzonderlijke van uploaden met Hallo `SkipCopy` markeren of samen met de Hallo bewerking voor het uploaden. Compressie toepassen op een gecomprimeerde pakket is geen.
een gecomprimeerde pakket gebruik toouncompress Hallo dezelfde [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht Hello `UncompressPackage` overschakelen.

Hallo volgende cmdlet wordt gecomprimeerd Hallo pakket zonder deze toohello image store. Hallo-pakket bevat nu ZIP-bestanden voor Hallo `Code` en `Config` pakketten. Hallo-toepassing en Hallo service manifesten zijn niet ingepakte, omdat ze nodig zijn voor veel interne bewerkingen (zoals pakket delen van de toepassing de naam en versie extraheren voor bepaalde validaties). Hallo manifesten comprimeren zouden deze bewerkingen niet efficiënt.

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

Voor grote toepassingpakketten duurt Hallo compressie. Gebruik een snel SSD-station voor de beste resultaten. Hallo compressie tijden en grootte van het gecomprimeerde pakket Hallo Hallo ook u verschillen op basis van de pakketinhoud Hallo.
Dit is bijvoorbeeld compressie statistieken van sommige pakketten die Hallo initiële weergeven en grootte van gecomprimeerde pakket, met Hallo compressie tijd Hallo.

|Aanvankelijke grootte (MB)|Aantal bestanden|Compressie tijd|Gecomprimeerde pakketgrootte (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Nadat u een pakket is gecomprimeerd, kan het geüploade tooone of meerdere Service Fabric-clusters indien nodig. Hallo-mechanisme voor clientimplementatie is hetzelfde voor gecomprimeerde en ongecomprimeerde pakketten. Hallo-pakket is gecomprimeerd, wordt deze opgeslagen als zodanig in Hallo cluster image store als deze niet op Hallo knooppunt gecomprimeerd voordat de toepassing hello wordt uitgevoerd.


Hallo volgende voorbeeld wordt geüpload Hallo pakket toohello image store in een map met de naam 'MyApplicationV1':

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.  tooimport hello SDK-module, uitvoeren:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Als u geen Hallo opgeeft *- ApplicationPackagePathInImageStore* parameter Hallo-toepassingspakket is gekopieerd naar 'Debug' Hallo-map in Hallo image store.

Hallo duurt tooupload een pakket is afhankelijk van meerdere factoren. Sommige van deze factoren zijn Hallo aantal bestanden in Hallo pakket Hallo pakketgrootte en bestandsgrootten Hallo. de netwerksnelheid Hallo tussen bron- en Service Fabric-cluster Hallo Hallo ook van invloed is op Hallo tijd. Hallo standaardtime-out voor [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minuten.
Afhankelijk van factoren beschreven Hallo, moet u wellicht tooincrease Hallo time-out. Als u Hallo-pakket in aanroep van Hallo kopiëren comprimeert, moet u tooalso beschouwd als Hallo compressie keer.

Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.

## <a name="register-hello-application-package"></a>Hallo-toepassingspakket registreren
type van de toepassing Hello en versie gedeclareerd in het toepassingsmanifest Hallo komen beschikbaar voor gebruik wanneer het Hallo-toepassingspakket is geregistreerd. Hallo system Hallo pakket geüpload in de vorige stap Hallo leest, verifieert Hallo pakket Hallo pakketinhoud verwerkt en Hallo verwerkt pakket tooan intern systeemprobleem locatie kopieert.  

Voer Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister Hallo toepassingstype in Hallo-cluster en het beschikbaar voor implementatie:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

'MyApplicationV1' is Hallo-map in Hallo image store waar Hallo toepassingspakket zich bevindt. type van de toepassing Hello met de naam 'MyApplicationType' en versie '1.0.0' (zowel gevonden in het toepassingsmanifest Hallo) is nu geregistreerd in Hallo-cluster.

Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) opdracht retourneert alleen nadat Hallo systeem geregistreerd Hallo-toepassingspakket heeft. Hoe lang duurt registratie afhankelijk van Hallo grootte en de inhoud van het toepassingspakket Hallo. Indien nodig, Hallo **- TimeoutSec** parameter gebruikte toosupply een langere time-out kan zijn (Hallo standaardtime-out is 60 seconden).

Als u een grote toepassing van het pakket of als u time-outs ondervindt, gebruikt u Hallo **Async -** parameter. Hallo-opdracht geretourneerd wanneer Hallo cluster de opdracht register Hallo accepteert en Hallo verwerking blijft indien nodig.
Hallo [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) opdracht geeft een lijst van alle versies van het type toepassing is geregistreerd en hun registratiestatus. U kunt deze opdracht toodetermine gebruiken als het Hallo-registratie is voltooid.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Hallo-toepassing maken
U kunt een toepassing met een versie van het toepassingstype dat is geregistreerd met behulp van Hallo instantiëren [nieuw ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet. Hallo-naam van elke toepassing moet beginnen met Hallo *"fabric: '* schema en moet uniek zijn voor elk toepassingsexemplaar. Alle services die standaard gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing Hallo worden ook gemaakt.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Meerdere exemplaren van een toepassing kunnen worden gemaakt voor een bepaalde versie van een geregistreerde toepassingstype. Elk toepassingsexemplaar wordt uitgevoerd in een geïsoleerde omgeving met een eigen werk directory en het proces.

toosee die met de naam apps en services worden uitgevoerd in de cluster Hallo Hallo uitvoeren [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) en [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:

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

## <a name="remove-an-application"></a>Een toepassing verwijderen
Wanneer een toepassingsexemplaar niet meer nodig is, kunt u permanent verwijderen deze op naam Hallo met [verwijderen ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. [Verwijder ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) alle services die deel uitmaken van toohello toepassing ook, permanent verwijderen van de status van alle service wordt automatisch verwijderd. 

> [!WARNING]
> Deze bewerking kan niet ongedaan worden gemaakt en de status van toepassing kan niet worden hersteld.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Registratie van een toepassingstype
Wanneer een bepaalde versie van het type van een toepassing niet meer nodig is, moet u registratie toepassingstype Hallo Hallo met [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Registratie ongebruikte toepassing typen releases opslagruimte die wordt gebruikt door Hallo image store. Een toepassingstype kan ongedaan worden zolang geen toepassingen worden geïnstantieerd tegen en niet in afwachting van toepassing upgrades hiernaar wordt verwezen.

Voer [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee Hallo toepassingstypen worden momenteel geregistreerd in Hallo-cluster:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Voer [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister een specifieke toepassingstype:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Een toepassingspakket verwijderen uit de installatiekopieopslag Hallo
Wanneer een toepassingspakket is niet langer nodig is, kunt u deze verwijderen uit Hallo image store toofree Maak systeembronnen.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Kopiëren ServiceFabricApplicationPackage vraagt om een ImageStoreConnectionString
Hallo Service Fabric SDK omgeving moet al Hallo juiste standaardwaarden wordt ingesteld. Maar desgewenst Hallo ImageStoreConnectionString voor alle opdrachten moet overeenkomen met Hallo-waarde die Hallo Service Fabric-cluster wordt gebruikt. Hallo ImageStoreConnectionString vindt u in het clustermanifest Hallo opgehaald met Hallo [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) en Get-ImageStoreConnectionStringFromClusterManifest-opdrachten:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.  tooimport hello SDK-module, uitvoeren:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Hallo ImageStoreConnectionString is gevonden in clustermanifest Hallo:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.

### <a name="deploy-large-application-package"></a>Grote toepassingspakket implementeren
Probleem: [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) een time-out voor een groot pakket (in volgorde van GB).
Probeer een van:
- Geef een hogere time-out voor [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht met `TimeoutSec` parameter. Hallo-out is standaard 30 minuten.
- Controleer de netwerkverbinding Hallo tussen de bron- en cluster. Als Hallo verbinding langzaam is, kunt u overwegen een machine met een betere netwerkverbinding.
Hallo client-computer in een andere regio dan het Hallo-cluster, dan kunt u met behulp van een client-computer in een dichter of dezelfde regio als Hallo-cluster.
- Controleer als u externe beperking zijn raken. Wanneer de installatiekopieopslag Hallo geconfigureerde toouse azure storage, kunnen uploaden bijvoorbeeld kan worden beperkt.

Probleem: Upload-pakket is voltooid, maar [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) een time-out optreedt. Probeer een van:
- [Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert.
Hallo compressie Hallo verkleint en Hallo aantal bestanden, die op zijn beurt minder Hallo hoeveelheid verkeer en werkt deze Service Fabric moet uitvoeren. Hallo uploadbewerking mogelijk langzamer (met name als u Hallo compressie tijd opnemen), maar registreren en ongedaan maken van de registratie Hallo toepassingstype sneller.
- Geef een hogere time-out voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) met `TimeoutSec` parameter.
- Geef `Async` overschakelen voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Hallo-opdracht geretourneerd wanneer Hallo cluster Hallo opdracht accepteert en registratie van toepassingstype Hallo Hallo asynchroon blijft. Daarom wordt is er geen toospecify moet een hogere time-out in dit geval. Hallo [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) opdracht geeft een lijst van alle versies van het type toepassing is geregistreerd en hun registratiestatus. U kunt deze opdracht toodetermine gebruiken als het Hallo-registratie is voltooid.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Toepassingspakket implementeren met veel bestanden
Probleem: [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) time-out voor een toepassingspakket met veel bestanden (volgorde van duizendtallen).
Probeer een van:
- [Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert. Hallo compressie vermindert het aantal bestanden Hallo.
- Geef een hogere time-out voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) met `TimeoutSec` parameter.
- Geef `Async` overschakelen voor [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Hallo-opdracht geretourneerd wanneer Hallo cluster Hallo opdracht accepteert en registratie van toepassingstype Hallo Hallo asynchroon blijft.
Daarom wordt is er geen toospecify moet een hogere time-out in dit geval. Hallo [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) opdracht geeft een lijst van alle versies van het type toepassing is geregistreerd en hun registratiestatus. U kunt deze opdracht toodetermine gebruiken als het Hallo-registratie is voltooid.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Volgende stappen
[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)

[Service Fabric health Inleiding](service-fabric-health-introduction.md)

[Vaststellen en oplossen van een Service Fabric-service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Model van een toepassing in Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
