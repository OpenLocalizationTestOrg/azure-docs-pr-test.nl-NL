---
title: Azure Service Fabric-Toepassingsbeheer aaaAutomate | Microsoft Docs
description: Implementeren, bijwerken, testen en verwijderen van Service Fabric-toepassingen met behulp van PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>De levenscyclus van de toepassing hello met behulp van PowerShell automatiseren
Veel aspecten van Hallo [Service Fabric-toepassing lifecycle](service-fabric-application-lifecycle.md) kan worden geautomatiseerd.  Dit artikel laat zien hoe toouse PowerShell tooautomate algemene taken voor het implementeren, bijwerken, verwijderen en testen van Azure Service Fabric-toepassingen.  Beheerd en HTTP-APIs voor app-beheer zijn ook beschikbaar. Zie [app-levenscyclus](service-fabric-application-lifecycle.md) voor meer informatie.  

## <a name="prerequisites"></a>Vereisten
Voordat u de taken in het artikel Hallo toohello verplaatsen, moet u:

* Raak vertrouwd met Hallo Service Fabric-concepten beschreven in [technisch overzicht van Service Fabric](service-fabric-technical-overview.md).
* [Hallo-runtime, SDK en hulpprogramma's installeren](service-fabric-get-started.md), die ook Hallo geïnstalleerd **ServiceFabric** PowerShell-module.
* [Uitvoering van PowerShell-script inschakelen](service-fabric-get-started.md#enable-powershell-script-execution).
* Start een lokaal cluster.  Start een nieuwe PowerShell-venster als beheerder en voer vervolgens Hallo cluster setup-script uit Hallo SDK-map:`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Voordat u een PowerShell-opdrachten in dit artikel uitvoert, moet u eerst toohello lokale Service Fabric-cluster verbinding met behulp van [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Hallo taken te volgen vereisen een toodeploy v1 application-pakket en een toepassingspakket v2 voor upgrade. Hallo downloaden [ **WordCount** voorbeeldtoepassing](http://aka.ms/servicefabricsamples) (te vinden in de voorbeelden van Hallo aan de slag). Bouw en Hallo-toepassing in Visual Studio-pakket (met de rechtermuisknop op **WordCount** in Solution Explorer en selecteer **pakket**). Kopiëren Hallo v1-pakket in `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` te`C:\Temp\WordCount`. Kopiëren `C:\Temp\WordCount` te`C:\Temp\WordCountV2`, maken Hallo v2-toepassingspakket voor upgrade. Open `C:\Temp\WordCountV2\ApplicationManifest.xml` in een teksteditor. In Hallo **ApplicationManifest** element, wijziging Hallo **ApplicationTypeVersion** kenmerk uit '1.0.0' te '2.0.0' tooupdate Hallo app versienummer. Hallo gewijzigd ApplicationManifest.xml bestand opslaan.

## <a name="task-deploy-a-service-fabric-application"></a>Taak: Een Service Fabric-toepassing implementeren
Nadat u hebt gebouwd en verpakte toepassing hello (of gedownload Hallo application-pakket), kunt u de toepassing hello in een lokale Service Fabric-cluster implementeren. Implementatie omvat het Hallo-toepassingspakket uploaden, Hallo toepassingstype registreren en maken van het toepassingsexemplaar Hallo. Hallo-instructies in deze sectie toodeploy een nieuwe toepassing tooa cluster gebruiken.

### <a name="step-1-upload-hello-application-package"></a>Stap 1: Hallo toepassingspakket uploaden
Hallo toepassing pakket toohello uploaden plaatst installatiekopieopslag het in een locatie toegankelijk toointernal Service Fabric-onderdelen.  Hallo-toepassingspakket bevat Hallo nodig manifest van de toepassing en service manifesten code, configuratie en gegevens pakketten toocreate Hallo toepassing en service-exemplaren. Als u tooverify Hallo app-pakket lokaal wilt, gebruikt u Hallo [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.  Hallo [kopie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) opdracht uploads Hallo pakket. Bijvoorbeeld:

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Stap 2: Type van de toepassing hello registreren
Registreren van het Hallo-toepassingspakket maakt Hallo toepassingstype en -versie die zijn gedeclareerd in het toepassingsmanifest Hallo beschikbaar voor gebruik. Hallo gelezen Hallo pakket geüpload in Hallo-stap 1, controleert u of Hallo-pakket (gelijkwaardige toorunning [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) lokaal), Hallo pakketinhoud verwerken en Hallo verwerkt pakket tooan kopiëren interne locatie.  Voer Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
alle Hallo toepassingstypen geregistreerd in Hallo-cluster, Voer Hallo toosee [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Stap 3: Maak Hallo toepassingsexemplaar
Een toepassing kan worden gemaakt met behulp van een versie van het toepassingstype dat is geregistreerd met behulp van Hallo [nieuw ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) opdracht. naam van elke toepassing Hello is gedeclareerd in tijd implementeren en moet beginnen met Hallo **fabric:** schema en uniek zijn voor elk toepassingsexemplaar. Hallo type toepassingsnaam en toepassingsversie type zijn gedeclareerd in Hallo **ApplicationManifest.xml** -bestand van het toepassingspakket Hallo. Als alle services die standaard zijn gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing hello, worden op dit moment die zijn gemaakt.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Hallo [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) opdracht worden alle exemplaren van een toepassing die zijn gemaakt, samen met hun algehele status. Hallo [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) opdracht worden alle Hallo service-exemplaren die zijn gemaakt binnen een bepaalde toepassing-exemplaar. Standaard-services (indien aanwezig) worden weergegeven.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Taak: Upgrade uitvoert voor een Service Fabric-toepassing
U kunt een eerder geïmplementeerde Service Fabric-toepassing met een bijgewerkte pakket bijwerken. Deze taak voert een upgrade Hallo WordCount-toepassing die is geïmplementeerd in ' taak: een Service Fabric-toepassing implementeert. " Lees [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md) voor meer informatie.

simpel tookeep voor dit voorbeeld alleen Hallo versienummer van toepassing is bijgewerkt in Hallo WordCountV2 toepassingspakket is gemaakt in Hallo vereisten. Een meer realistische scenario zou hebben betrekking op voor het bijwerken van uw service-bestanden voor code, de configuratie of de gegevens en opnieuw te bouwen en verpakking toepassing hello met bijgewerkte versienummers.  

### <a name="step-1-upload-hello-updated-application-package"></a>Stap 1: Hallo bijgewerkte toepassingspakket uploaden
Hallo v1-toepassing WordCount is gereed toobe bijgewerkt. Als u het openen van een PowerShell-venster als beheerder en typ [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), ziet u die versie 1.0.0 Hallo type WordCount-toepassing wordt geïmplementeerd.  

Nu kopiëren Hallo pakket toohello Service Fabric installatiekopie toepassingsarchief (waar Hallo toepassingspakketten zijn opgeslagen door de Service Fabric) bijgewerkt. parameter Hallo **ApplicationPackagePathInImageStore** informeert Service Fabric waar het Hallo-toepassingspakket kan vinden. Hallo opdracht kopieën Hallo toepassingspakket te volgen**WordCountV2** in Hallo image store:  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Stap 2: Register Hallo bijgewerkt toepassingstype
Hallo volgende stap is tooregister Hallo nieuwe versie van de toepassing hello met Service Fabric, die kan worden uitgevoerd met behulp van Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Stap 3: Hallo upgrade Start
Verschillende parameters voor het bijwerken, time-outs en health criteria kunnen worden toegepast tooapplication upgrades. Lees Hallo [parameters voor het bijwerken van toepassing](service-fabric-application-upgrade-parameters.md) en [upgradeproces](service-fabric-application-upgrade.md) toolearn meer documenten. Alle services en -exemplaren moet *orde* na de upgrade Hallo.  Set Hallo **HealthCheckStableDuration** too60 seconden (zodat Hallo-services zijn in orde voor ten minste 20 seconden voordat de upgrade Hallo wordt voortgezet toohello volgende upgradedomein).  Ook set Hallo **UpgradeDomainTimeout** too1200 seconden en Hallo **UpgradeTimeout** too3000 seconden. Tot slot stelt Hallo **UpgradeFailureAction** te**terugdraaien**, welke aanvragen die Service Fabric is teruggedraaid Hallo toepassing toohello eerdere versie, als er fouten zijn opgetreden tijdens de upgrade.

U kunt nu een upgrade van de toepassing hello starten met behulp van Hallo [Start ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Opmerking die naam van de toepassing hello is Hallo dezelfde Hallo implementatie eerder v1.0.0 toepassingsnaam (fabric: / WordCount). Service Fabric gebruikt deze naam tooidentify welke toepassing wordt ophalen bijgewerkt. Als u Hallo time-outs toobe te kort instelt, kunt u een time-outwaarde foutbericht dat statussen probleem Hallo kunt tegenkomen. Raadpleeg te[toepassingsupgrades oplossen](service-fabric-application-upgrade-troubleshooting.md), of verhoog de Hallo time-outs.

### <a name="step-4-check-upgrade-progress"></a>Stap 4: Controleer de voortgang van upgrade
U kunt de upgrade voortgang toepassing controleren met behulp van [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), of met behulp van Hallo [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

In een paar minuten Hallo [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet ziet u dat alle upgradedomeinen zijn bijgewerkt (voltooid).

## <a name="task-test-a-service-fabric-application"></a>Taak: Een Service Fabric-toepassing testen
toowrite hoogwaardige services, ontwikkelaars moeten toobe kunnen tooinduce onbetrouwbaar infrastructuur fouten tootest Hallo stabiliteit van hun services. Service Fabric biedt ontwikkelaars Hallo mogelijkheid tooinduce veroorzaakt acties en -services testen in de aanwezigheid van fouten door gebruik te maken met de Hallo Hallo chaos en failover Testscenario's.  Lees [inleiding toohello Analysis Services-fout](service-fabric-testability-overview.md) voor meer informatie.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Stap 1: Hallo chaos Testscenario uitvoeren
Hallo chaos Testscenario genereert fouten over de hele Service Fabric-cluster Hallo. Hallo scenario comprimeren fouten in het algemeen gezien via maanden of jaren tooa enkele uren. Hallo combinatie van interleaved fouten met een hoge fouttolerantie tarief vindt hoek aanvragen die anders zou worden overgeslagen. Hallo volgende voorbeeld wordt uitgevoerd Hallo chaos Testscenario gedurende 60 minuten.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Stap 2: Voer Hallo failover Testscenario
Hallo failover testen scenario doelen een specifieke service partitie in plaats van het volledige cluster Hallo en deze andere services blijft de situatie ongewijzigd blijft. een reeks gesimuleerde storingen in servicevalidatie doorlopen Hallo scenario terwijl uw bedrijfslogica wordt uitgevoerd. Een fout in servicevalidatie geeft een probleem dat verder onderzoek moet. Hallo failover testen induceert slechts één fout tegelijk aan tegengestelde toohello chaos Testscenario, die meerdere fouten kan veroorzaken. Hallo volgende voorbeeld wordt uitgevoerd Hallo failover testen gedurende 60 minuten op Hallo fabric: / WordCount/WordCountService-service.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Taak: Een Service Fabric-toepassing verwijderen
U kunt een exemplaar van een geïmplementeerde toepassing verwijderen, Hallo ingericht toepassingstype uit Hallo cluster verwijderen en Hallo-toepassingspakket uit Hallo Installatiekopieopslag verwijderen.

### <a name="step-1-remove-an-application-instance"></a>Stap 1: Een toepassingsexemplaar van de verwijderen
Wanneer een toepassingsexemplaar niet meer nodig is, u kunt definitief wordt verwijderd met behulp van Hallo [verwijderen ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. Hiermee verwijdert u ook automatisch alle services die toohello toepassing, permanent verwijderen van de status van alle service behoren. Deze bewerking kan niet ongedaan worden gemaakt en de status van toepassing kan niet worden hersteld.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Stap 2: Registratie van het toepassingstype Hallo
Wanneer u een bepaalde versie van het type van een toepassing niet meer nodig hebt, hef de registratie van deze met behulp van Hallo [Unregister ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Registratie ongebruikte typen releases opslagruimte die wordt gebruikt door Hallo toepassingspakket in Hallo image store. Een toepassingstype kunt ongedaan worden gemaakt, zolang er zijn geen toepassingen tegen of in behandeling toepassingsupgrades hiernaar geïnstantieerd.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Stap 3: Hallo toepassingspakket verwijderen
Nadat Hallo toepassingstype geregistreerd is, Hallo-toepassingspakket kan worden verwijderd uit de installatiekopieopslag Hallo via Hallo [verwijderen ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Volgende stappen
[De levenscyclus van de service Fabric-toepassing](service-fabric-application-lifecycle.md)

[Een toepassing implementeren](service-fabric-deploy-remove-applications.md)

[Upgrade van de toepassing](service-fabric-application-upgrade.md)

[Azure Service Fabric-cmdlets](/powershell/azure/overview?view=azureservicefabricps)

