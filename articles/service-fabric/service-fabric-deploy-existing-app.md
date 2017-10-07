---
title: een bestaand uitvoerbaar tooAzure Service Fabric aaaDeploy | Microsoft Docs
description: "Overzicht over hoe toopackage een bestaande toepassing als een gast uitvoerbaar bestand, zodat deze kan worden geïmplementeerd voor tooa Service Fabric-cluster"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Een gast uitvoerbare tooService Fabric implementeren
Als een service kunt u verschillende typen code, zoals Node.js, Java of C++ uitvoeren in Azure Service Fabric. Service Fabric verwijst toothese soorten services als gast uitvoerbare bestanden.

Gast uitvoerbare bestanden worden behandeld door het Service Fabric zoals stateless services. Als gevolg hiervan worden deze geplaatst op knooppunten in een cluster, op basis van beschikbaarheid en andere metrische gegevens. Dit artikel wordt beschreven hoe toopackage en een gast uitvoerbare tooa Service Fabric-cluster implementeren met behulp van Visual Studio of een opdrachtregelprogramma.

In dit artikel, we hebben betrekking op Hallo stappen toopackage uitvoerbare Gast en implementeert u deze tooService Fabric.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Voordelen van het uitvoeren van een gast uitvoerbare in Service Fabric
Er zijn enkele voordelen toorunning Gast uitvoerbare in een Service Fabric-cluster:

* Hoge beschikbaarheid. Toepassingen die worden uitgevoerd in Service Fabric zijn maximaal beschikbaar is gemaakt. Service Fabric zorgt ervoor dat de exemplaren van een toepassing worden uitgevoerd.
* Statuscontrole. Service Fabric-statuscontrole detecteert als een toepassing wordt uitgevoerd, en bevat de diagnostische gegevens als er een storing optreedt.   
* Levenscyclus van Toepassingsbeheer. Service Fabric bevat eerdere versie van automatisch herstel toohello naast het bieden van upgrades zonder uitvaltijd, als er een ongeldige statusgebeurtenis gerapporteerd tijdens een upgrade.    
* Dichtheid. U kunt meerdere toepassingen uitvoeren in een cluster, zodat Hallo voor elke toepassing toorun op een eigen hardware.
* Zichtbaarheid: REST kunt u aanroepen Hallo Service Fabric Naming service toofind andere services in Hallo-cluster. 

## <a name="samples"></a>Voorbeelden
* [Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Overzicht van de toepassing en service manifest-bestanden
Als onderdeel van de implementatie van een gast uitvoerbaar bestand, is het nuttig toounderstand Hallo Service Fabric-pakketten en -implementatiemodel zoals beschreven in [toepassingsmodel](service-fabric-application-model.md). Hallo Service Fabric-pakket model is afhankelijk van de twee XML-bestanden: Hallo toepassing en service manifesten. Hallo schemadefinitie voor hello is ApplicationManifest.xml en ServiceManifest.xml-bestanden geïnstalleerd met Hallo Service Fabric SDK in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Het toepassingsmanifest** Hallo-toepassingsmanifest gebruikte toodescribe Hallo toepassing is. Geeft het Hallo-services waaruit deze en andere parameters die zijn gebruikt toodefine hoe een of meer services moeten worden geïmplementeerd, zoals het aantal exemplaren Hallo.

  Een toepassing is in Service Fabric eenheid van de implementatie en upgrade. Een toepassing kan worden bijgewerkt als één eenheid waar de potentiële fouten en mogelijke Rollback worden beheerd. Service Fabric zorgt ervoor dat het upgradeproces Hallo ofwel is geslaagd, of als Hallo upgrade mislukt, laat Hallo-toepassing in een onbekende of onstabiele status heeft.
* **Servicemanifest** Hallo servicemanifest beschrijving Hallo onderdelen van een service. Dit omvat gegevens, zoals het Hallo-naam en type van de service, en de code en configuratie. Hallo servicemanifest bevat ook een aantal extra parameters die kunnen worden gebruikt tooconfigure Hallo service nadat deze is geïmplementeerd.

## <a name="application-package-file-structure"></a>Bestandsstructuur voor Application-pakket
een toepassing tooService Fabric toodeploy, toepassing hello moet volgen op een vooraf gedefinieerde mapstructuur. Hallo Hier volgt een voorbeeld van die structuur.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Hallo ApplicationPackageRoot bevat hello ApplicationManifest.xml-bestand waarin de toepassing hello. Een submap voor elke service die is opgenomen in de toepassing hello is gebruikte toocontain alle Hallo artefacten die Hallo service nodig. Deze submappen zijn Hallo ServiceManifest.xml en normaal gesproken hello te volgen:

* *Code*. Deze map bevat Hallo servicecode.
* *Config*. Deze map bevat een Settings.xml-bestand (en andere bestanden indien nodig) dat Hallo-service toegang op runtime tooretrieve specifieke configuratie-instellingen tot.
* *Gegevens*. Dit is een extra map toostore aanvullende lokale gegevens die Hallo-service moet mogelijk. Gegevens moeten alleen kortstondige gebruikte toostore-gegevens. Service Fabric komt niet worden gekopieerd of repliceren wijzigingen toohello gegevensmap als Hallo-service toobe verplaatst (bijvoorbeeld tijdens de failover moet).

> [!NOTE]
> U hebt geen toocreate hello `config` en `data` mappen als u deze niet nodig hebt.
>
>

## <a name="package-an-existing-executable"></a>Een bestaand uitvoerbaar bestand van het pakket
Wanneer een gast uitvoerbaar bestand verpakking, kunt u beide toouse een Visual Studio-projectsjabloon of te[handmatig maken van het toepassingspakket Hallo](#manually). Pakketstructuur van toepassing met Visual Studio, Hallo en manifest-bestanden in het nieuwe projectsjabloon Hallo voor u gemaakt.

> [!TIP]
> Hallo gemakkelijkste manier toopackage een bestaande Windows uitvoerbare bij een service is toouse Visual Studio en op Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Gebruik Visual Studio toopackage en de implementatie van een bestaand uitvoerbaar bestand
Visual Studio biedt een Service Fabric service sjabloon toohelp implementeren van een gast uitvoerbare tooa Service Fabric-cluster.

1. Kies **bestand** > **nieuw Project**, en maak een Service Fabric-toepassing.
2. Kies **Gast uitvoerbaar bestand** als Hallo-servicesjabloon.
3. Klik op **Bladeren** tooselect Hallo map met de uitvoerbare bestand en vul Hallo rest van Hallo parameters toocreate Hallo service.
   * *Pakketgedrag code*. Kan worden set toocopy alle Hallo inhoud van uw map toohello Visual Studio-Project, dit is handig als Hallo uitvoerbare wordt niet gewijzigd. Als u Hallo uitvoerbare toochange verwacht en Hallo mogelijkheid toopick van nieuwe builds dynamisch wilt, kunt u in plaats daarvan toolink toohello map. U kunt de gekoppelde mappen kunt gebruiken bij het Hallo-toepassingsproject maken in Visual Studio. Toohello bronlocatie uit binnen Hallo-project, waardoor het mogelijk dat u tooupdate Hallo Gast uitvoerbare in de bron-doel wordt gekoppeld. Deze updates uitmaken deel van Hallo-toepassingspakket op build.
   * *Programma* Hallo uitvoerbaar bestand dat moet worden uitgevoerd toostart Hallo service bevat.
   * *Argumenten* Hallo argumenten die moeten worden doorgegeven toohello uitvoerbare. Het kan zijn dat een lijst met parameters met argumenten.
   * *WorkingFolder* Hiermee geeft u de werkmap Hallo voor Hallo-proces dat wordt toobe gestart. U kunt drie waarden opgeven:
     * `CodeBase`Hiermee geeft u deze werkmap Hallo gaat toobe toohello code directory instellen in het toepassingspakket hello (`Code` directory die wordt weergegeven in de voorgaande bestandsstructuur Hallo).
     * `CodePackage`Hiermee geeft u deze werkmap Hallo gaat toobe toohello hoofdmap van het toepassingspakket Hallo ingesteld (`GuestService1Pkg` wordt weergegeven in de voorgaande bestandsstructuur Hallo).
     * `Work`Hiermee geeft u op dat Hallo-bestanden in de submap werk zijn geplaatst.
4. Geef de service een naam en klik op **OK**.
5. Als uw service een eindpunt voor communicatie moet, kunt u nu Hallo-protocol en poort type toohello ServiceManifest.xml bestand toevoegen. Bijvoorbeeld: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. U kunt nu Hallo pakket gebruiken en publiceren van actie tegen uw lokale cluster door foutopsporing Hallo-oplossing in Visual Studio. Wanneer u klaar bent, kunt u Hallo toepassing tooa extern clusterbeheer publiceren of inchecken Hallo oplossing toosource besturingselement.
7. Hoe gaat u toohello einde van dit artikel toosee tooview uw gast uitvoerbare service wordt uitgevoerd op de Service Fabric Explorer.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Gebruik Yoeman toopackage en de implementatie van een bestaand uitvoerbaar bestand op Linux

Hallo-procedure voor het maken en implementeren van een uitvoerbaar zijn op Linux Gast is hetzelfde als het implementeren van een csharp of java-toepassing hello.

1. Typ in een terminal `yo azuresfguest`.
2. Geef uw toepassing een naam.
3. Naam van uw service en Hallo details, zoals het pad van uitvoerbare Hallo en Hallo-parameters die moeten worden aangeroepen met bieden.

Yeoman maakt een toepassingspakket met de juiste toepassing hello en manifest-bestanden samen met het installeren en verwijderen van scripts.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Handmatig verpakken en distribueren van een bestaand uitvoerbaar bestand
Hallo-proces verpakt handmatig een gast uitvoerbaar bestand is gebaseerd op Hallo algemene stappen te volgen:

1. Mapstructuur Hallo-pakket maken.
2. De bestanden code en configuratie van de toepassing hello toevoegen.
3. Servicemanifest Hallo bewerken.
4. Manifestbestand van de toepassing hello bewerken.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Mapstructuur Hallo-pakket maken
U kunt starten door het maken van de mapstructuur Hallo, zoals beschreven in voorgaande sectie Hallo "Application-pakket bestandsstructuur."

### <a name="add-hello-applications-code-and-configuration-files"></a>De bestanden code en configuratie van de toepassing hello toevoegen
Nadat u de mapstructuur Hallo hebt gemaakt, kunt u Hallo van code en configuratie toepassingsbestanden onder Hallo code en config-mappen toevoegen. U kunt ook extra mappen of submappen onder de code of configuratieversie mappen Hallo maken.

Service Fabric biedt een `xcopy` van Hallo inhoud van Hallo hoofdmap van toepassing, zodat er geen toouse vooraf gedefinieerde structuur dan het maken van de twee bovenste mappen, code en instellingen. (U kunt kiezen verschillende namen als u wilt. Meer informatie vindt u in de volgende sectie Hallo.)

> [!NOTE]
> Zorg ervoor dat u alle Hallo bestanden en afhankelijkheden die behoeften toepassing hello opneemt. Service Fabric kopieert Hallo inhoud van het toepassingspakket Hallo op alle knooppunten in Hallo cluster waarbij Hallo toepassingsservices gaat toobe geïmplementeerd. Hallo-pakket moet alle Hallo code dat de toepassing hello toorun moet bevatten. Niet wordt ervan uitgegaan dat Hallo afhankelijkheden al zijn geïnstalleerd.
>
>

### <a name="edit-hello-service-manifest-file"></a>Servicemanifest Hallo bewerken
de volgende stap Hallo is tooedit Hallo service manifestbestand tooinclude Hallo volgende informatie:

* Hallo-naam van het servicetype Hallo. Dit is een ID dat gebruikmaakt van Service Fabric tooidentify een service.
* Hallo opdracht toouse toolaunch Hallo toepassing (ExeHost).
* Elk script dat moet toobe tooset Hallo-toepassing (entrypoint) worden uitgevoerd.

Hallo Hieronder volgt een voorbeeld van een `ServiceManifest.xml` bestand:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Hallo uit te voeren gaan via verschillende onderdelen van Hallo-bestand dat u nodig hebt tooupdate Hallo

#### <a name="update-servicetypes"></a>ServiceTypes bijwerken
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* U kunt elke willekeurige naam die u wilt verzamelen `ServiceTypeName`. Hallo-waarde wordt gebruikt in Hallo `ApplicationManifest.xml` file tooidentify Hallo-service.
* Geef `UseImplicitHost="true"`. Dit kenmerk instrueert Service Fabric dat Hallo-service is gebaseerd op een zelfstandige app, zodat alle Service Fabric moet toodo toolaunch als een proces en de status controleren.

#### <a name="update-codepackage"></a>CodePackage bijwerken
Hallo CodePackage element geeft Hallo locatie (en versie) van Hallo servicecode.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Hallo `Name` element is gebruikte toospecify Hallo naam van de map Hallo in Hallo-toepassingspakket met Hallo servicecode. `CodePackage`heeft ook Hallo `version` kenmerk. Deze versie van de gebruikte toospecify Hallo Hallo code en kan mogelijk ook tooupgrade Hallo service code gebruikt met behulp van Hallo toepassing lifecycle beheerinfrastructuur in Service Fabric.

#### <a name="optional-update-setupentrypoint"></a>Optioneel: Update entrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
Hallo entrypoint element gebruikte toospecify is een uitvoerbaar bestand of batch-bestand dat moet worden uitgevoerd voordat het Hallo servicecode wordt gestart. Het is een optionele stap zodat deze niet toobe opgenomen hoeft als er geen initialisatie vereist. Hallo entrypoint wordt uitgevoerd telkens wanneer het Hallo-service opnieuw wordt gestart.

Er is slechts één entrypoint daarom installatiescripts toobe gegroepeerd in een enkel batchbestand als Hallo toepassingsinstellingen meerdere scripts vereist. Hallo entrypoint elk type bestand kunt uitvoeren: uitvoerbare bestanden, batchbestanden en PowerShell-cmdlets. Zie voor meer informatie [entrypoint configureren](service-fabric-application-runas-security.md).

In Hallo voorgaande voorbeeld, Hallo entrypoint wordt uitgevoerd een batchbestand aangeroepen `LaunchConfig.cmd` dat zich bevindt in Hallo `scripts` submap van Hallo codemap (ervan uitgaande dat Hallo WorkingFolder element tooCodeBase is ingesteld).

#### <a name="update-entrypoint"></a>EntryPoint bijwerken
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Hallo `EntryPoint` -element in Hallo servicemanifestbestand is gebruikte toospecify hoe toolaunch Hallo-service. Hallo `ExeHost` element geeft uitvoerbare hello (en argumenten) die moet worden gebruikt toolaunch Hallo-service.

* `Program`Geeft de naam Hallo van Hallo uitvoerbaar bestand dat Hallo-service moet worden gestart.
* `Arguments`Hiermee geeft u Hallo argumenten die moeten worden doorgegeven toohello uitvoerbare. Het kan zijn dat een lijst met parameters met argumenten.
* `WorkingFolder`Hiermee geeft u de werkmap Hallo voor Hallo-proces dat wordt toobe gestart. U kunt drie waarden opgeven:
  * `CodeBase`Hiermee geeft u deze werkmap Hallo gaat toobe toohello code directory instellen in het toepassingspakket hello (`Code` map in de voorgaande bestandsstructuur Hallo).
  * `CodePackage`Hiermee geeft u deze werkmap Hallo gaat toobe toohello hoofdmap van het toepassingspakket Hallo ingesteld (`GuestService1Pkg` in de voorgaande bestandsstructuur Hallo).
    * `Work`Hiermee geeft u op dat Hallo-bestanden in de submap werk zijn geplaatst.

Hallo WorkingFolder is nuttig tooset Hallo juiste werkmap zodat relatieve paden kunnen worden gebruikt door beide Hallo toepassings- of initialisatie-scripts.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Bijwerken van eindpunten en registreren met Naming Service voor communicatie
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
Hallo in Hallo voorgaande voorbeeld, `Endpoint` element geeft Hallo-eindpunten die toepassing hello kunt luisteren op. In dit voorbeeld luistert Hallo Node.js-toepassing naar http op 3000-poort.

Bovendien kunt u vragen Service Fabric toopublish dit eindpunt toohello Naming Service zodat andere services Hallo eindpunt adres toothis service kunnen detecteren. Hiermee kunt u toobe kunnen toocommunicate tussen services die gast uitvoerbare bestanden.
Hallo gepubliceerde eindpuntadres heeft Hallo vorm `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme`en `PathSuffix` optionele kenmerken zijn. `IPAddressOrFQDN`Hallo IP-adres of FQDN-naam van dit uitvoerbare bestand wordt geplaatst op Hallo-knooppunt en wordt berekend voor u is.

In hello volgende voorbeeld wordt één keer Hallo-service is geïmplementeerd, in Service Fabric Explorer ziet u een eindpunt die vergelijkbaar te`http://10.1.4.92:3000/myapp/` gepubliceerd voor Hallo service-exemplaar. Of als dit een lokale computer is, ziet u `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
U kunt deze adressen met [omgekeerde proxy](service-fabric-reverseproxy.md) toocommunicate tussen services.

### <a name="edit-hello-application-manifest-file"></a>Manifestbestand van de toepassing hello bewerken
Nadat u hebt geconfigureerd Hallo `Servicemanifest.xml` bestand, moet u toomake na enkele wijzigingen toohello `ApplicationManifest.xml` bestand tooensure die Hallo juiste servicetype en de naam worden gebruikt.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
In Hallo `ServiceManifestImport` element, kunt u een of meer services die u wilt dat tooinclude in Hallo-app opgeven. Services wordt verwezen met `ServiceManifestName`, waarmee Hallo-naam van Hallo map waar hello `ServiceManifest.xml` bestand zich bevindt.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Logboekregistratie instellen
Voor uitvoerbare bestanden Gast is het nuttig toobe kunnen toosee console logboeken toofind uit als het Hallo-toepassing en configuratie-scripts tonen eventuele fouten.
Console-omleiding kan worden geconfigureerd in Hallo `ServiceManifest.xml` -bestand met de Hallo `ConsoleRedirection` element.

> [!WARNING]
> Gebruik nooit Omleidingsbeleid Hallo-console in een toepassing die is geïmplementeerd in productie, omdat dit Hallo toepassing failover kan beïnvloeden. *Alleen* Gebruik deze optie voor lokale ontwikkeling en foutopsporing.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`kan worden gebruikt tooredirect console-uitvoer (stdout en stderr) tooa-werkmap. Dit biedt Hallo mogelijkheid tooverify dat er geen fouten zijn opgetreden tijdens het Hallo-setup of uitvoering van de toepassing hello in Hallo Service Fabric-cluster.

`FileRetentionCount`Hiermee wordt bepaald hoeveel bestanden worden opgeslagen in de werkmap Hallo. Een waarde van 5, betekent bijvoorbeeld dat Hallo-logboekbestanden voor de vorige vijf uitvoeringen Hallo zijn opgeslagen in de werkmap Hallo.

`FileMaxSizeInKb`Geeft de maximumomvang Hallo Hallo-logboekbestanden.

Logboekbestanden worden opgeslagen in een van de service Hallo werkende mappen. toodetermine waar Hallo bestanden zich bevinden, gebruik Service Fabric Explorer toodetermine welk knooppunt Hallo-service wordt uitgevoerd op, en welke werkmap wordt gebruikt. Dit proces wordt verderop in dit artikel beschreven.

## <a name="deployment"></a>Implementatie
Hallo laatste stap is te[implementeren van uw toepassing](service-fabric-deploy-remove-applications.md). Hallo volgende PowerShell-script toont hoe toodeploy uw toepassing toohello lokaal ontwikkelcluster en start een nieuwe Service Fabric-service.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert als Hallo-pakket grote is of veel bestanden. Lees meer [hier](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Een Service Fabric-service kan worden geïmplementeerd in verschillende 'configuraties." Bijvoorbeeld, het kan worden geïmplementeerd als één of meerdere exemplaren of deze zodanig dat er een exemplaar van de service op elk knooppunt van de Service Fabric-cluster Hallo Hallo wordt kan worden geïmplementeerd.

Hallo `InstanceCount` parameter Hallo `New-ServiceFabricService` cmdlet gebruikte toospecify hoeveel exemplaren van Hallo-service moeten worden gestart in Hallo Service Fabric-cluster is. U kunt instellen Hallo `InstanceCount` waarde, afhankelijk van het Hallo-type van de toepassing die u implementeert. Hallo twee meest voorkomende scenario's:

* `InstanceCount = "1"`. In dit geval wordt is slechts één exemplaar van het Hallo-service geïmplementeerd in Hallo-cluster. Service-Fabric scheduler bepaalt welke knooppunt Hallo-service gaat toobe geïmplementeerd op.
* `InstanceCount ="-1"`. In dit geval wordt wordt één exemplaar van Hallo-service geïmplementeerd op elk knooppunt in Hallo Service Fabric-cluster. Hallo resultaat heeft één (en slechts één) exemplaar van Hallo-service voor elk knooppunt in het Hallo-cluster.

Dit is een nuttig configuratie voor de front-end-toepassingen (bijvoorbeeld een REST-eindpunt), omdat clienttoepassingen nodig te "verbinding maken met' tooany van Hallo knooppunten in Hallo cluster toouse Hallo eindpunt. Deze configuratie kan ook worden gebruikt als alle knooppunten van het Service Fabric-cluster Hallo bijvoorbeeld verbonden tooa load balancer zijn. Clientverkeer kan vervolgens worden gedistribueerd over Hallo-service die wordt uitgevoerd op alle knooppunten in cluster Hallo.

## <a name="check-your-running-application"></a>Controleer de actieve toepassing
In Service Fabric Explorer geïdentificeerd Hallo knooppunt waarop Hallo-service wordt uitgevoerd. In dit voorbeeld op wordt uitgevoerd knooppunt1:

![Knooppunt waarop de service wordt uitgevoerd](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Als u toohello knooppunt navigeren en toohello toepassing bladeren, ziet u Hallo knooppunt essentiële informatie, waaronder de locatie op schijf.

![Locatie op schijf](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Als u toohello directory bladert met behulp van de Server Explorer, vindt u Hallo-werkmap en logboekmap Hallo-service, zoals wordt weergegeven in de volgende schermafbeelding Hallo: 

![Locatie van logboek](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe een gast uitvoerbaar bestand toopackage en tooService Fabric implementeert. Zie Hallo artikelen voor meer informatie en taken te volgen.

* [Voorbeeld voor verpakken en distribueren van een gast uitvoerbaar bestand](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), met inbegrip van een koppeling toohello voorlopige versie van hulpprogramma voor hello-pakketten
* [Voorbeeld van twee Gast uitvoerbare bestanden (C# en nodejs) communiceert via Hallo Naming service met behulp van REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Meerdere toepassingen implementeren die door gasten kunnen worden uitgevoerd](service-fabric-deploy-multiple-apps.md)
* [Uw eerste Service Fabric-toepassing met Visual Studio maken](service-fabric-create-your-first-application-in-visual-studio.md)
