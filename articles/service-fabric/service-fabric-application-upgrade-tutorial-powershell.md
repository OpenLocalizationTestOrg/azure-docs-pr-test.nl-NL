---
title: upgrade van aaaService Fabric-App met behulp van PowerShell | Microsoft Docs
description: In dit artikel wordt uitgelegd Hallo-ervaring van een Service Fabric-toepassing implementeren, Hallo programmacode wijzigen en implementeren van een upgrade met behulp van PowerShell.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Upgrade van de service Fabric-toepassing met behulp van PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Hallo het meest gebruikt en aanbevolen upgrade aanpak is uitrollende upgrade Hallo bewaakt.  Azure Service Fabric controleert de status van de Hallo van Hallo-toepassing wordt bijgewerkt op basis van een reeks statusbeleid. Wanneer een updatedomein (UD) is geüpgraded, Service Fabric evalueert Hallo toepassingsstatus en verloopt in de volgende updatedomein toohello of Hallo upgrade, afhankelijk van het statusbeleid Hallo is mislukt.

Een upgrade van de bewaakte toepassing kan worden uitgevoerd met behulp van Hallo beheerd of systeemeigen API's, PowerShell of REST. Zie voor instructies voor het uitvoeren van een upgrade met Visual Studio, [bijwerken van uw toepassing met Visual Studio](service-fabric-application-upgrade-tutorial.md).

Met Service Fabric bewaakt rollende upgrades, kunt Hallo beheerder van de toepassing hello evaluatie statusbeleid dat Service Fabric toodetermine gebruikt als de toepassing hello in orde is configureren. Bovendien configureren Hallo beheerder Hallo actie toobe genomen wanneer Hallo de statusevaluatie mislukt (bijvoorbeeld, voeren een automatische terugdraaien.) Deze sectie helpt bij de upgrade van een bewaakte voor een Hallo SDK-voorbeelden die PowerShell gebruikt. Hallo leidt volgende Microsoft Virtual Academy video u door een app-upgrade:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Stap 1: Bouwen en implementeren van Hallo visuele objecten voorbeeld
Bouwen en Hallo toepassing publiceren door met de rechtermuisknop op het Hallo-toepassingsproject **VisualObjectsApplication,** en het selecteren van Hallo **publiceren** opdracht.  Zie voor meer informatie [upgrade zelfstudie over Service Fabric](service-fabric-application-upgrade-tutorial.md).  U kunt ook kunt u PowerShell toodeploy uw toepassing.

> [!NOTE]
> Voordat een van de Service Fabric-opdrachten Hallo kan worden gebruikt in PowerShell, moet u eerst tooconnect toohello cluster met behulp van Hallo `Connect-ServiceFabricCluster` cmdlet. Op deze manier wordt ervan uitgegaan dat Hallo die cluster al is ingesteld op uw lokale machine. Zie artikel Hallo op [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started.md).
> 
> 

Na het Hallo-project in Visual Studio maakt, kunt u de PowerShell-opdracht Hallo [kopie ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy Hallo toepassing pakket toohello Installatiekopieopslag. Als u tooverify Hallo app-pakket lokaal wilt, gebruikt u Hallo [Test ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet. Hallo volgende stap is tooregister hello toohello Service Fabric runtime voor de toepassing hello met [registreren ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet. Hallo laatste stap is een exemplaar van de toepassing hello toostart via Hallo [nieuw ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.  Deze drie stappen zijn vergelijkbaar toousing hello **implementeren** menu-item in Visual Studio.

U kunt nu [Service Fabric Explorer tooview Hallo cluster en Hallo toepassing](service-fabric-visualizing-your-cluster.md). Hallo toepassing heeft een webservice die waarin navigeren tooin Internet Explorer te typen worden kan [http://localhost: 8081/visualobjects](http://localhost:8081/visualobjects) in de adresbalk Hallo.  Hier ziet u enkele zwevende visual objecten navigeren in het welkomstscherm.  Bovendien kunt u [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck Hallo toepassingsstatus.

## <a name="step-2-update-hello-visual-objects-sample"></a>Stap 2: Hallo visuele objecten voorbeeld bijwerken
U wellicht opgevallen dat met Hallo-versie die is geïmplementeerd in stap 1, Hallo visuele objecten niet draaien. Deze toepassing tooone waar Hallo visuele objecten ook draaien gaat upgraden.

Selecteer Hallo VisualObjects.ActorService-project binnen Hallo VisualObjects oplossing en Hallo StatefulVisualObjectActor.cs bestand opent. In dat bestand navigeren toohello methode `MoveObject`, uitcommentariëren `this.State.Move()`, en verwijder het commentaarteken `this.State.Move(true)`. Deze wijziging draait Hallo objecten na de upgrade van Hallo-service.

Er moet ook tooupdate hello *ServiceManifest.xml* -bestand (onder PackageRoot) van Hallo project **VisualObjects.ActorService**. Update Hallo *CodePackage* Hallo service versie too2.0 en overeenkomende regels in Hallo Hallo *ServiceManifest.xml* bestand.
U kunt Visual Studio Hallo *Manifest bestanden bewerken* optie nadat u met de rechtermuisknop op Hallo oplossing toomake Hallo manifestbestand wijzigingen.

Nadat Hallo wijzigingen zijn aangebracht, Hallo manifest moet eruitzien als in de volgende Hallo (gemarkeerde gedeelten weergeven Hallo wijzigingen):

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Nu Hallo *ApplicationManifest.xml* bestand (vinden onder Hallo **VisualObjects** project onder Hallo **VisualObjects** oplossing) bijgewerkte tooversion 2.0 Hallo is **VisualObjects.ActorService** project. Bovendien is de versie van de toepassing hello bijgewerkte too2.0.0.0 van 1.0.0.0. Hallo *ApplicationManifest.xml* moet eruit Hallo volgende codefragment:

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


Nu Hallo-project te bouwen door het selecteren van alleen Hallo **ActorService** -project en klik vervolgens met de rechtermuisknop op en te selecteren Hallo **bouwen** optie in Visual Studio. Als u selecteert **alles opnieuw opbouwen**, moet u Hallo-versies voor alle projecten, bijwerken, omdat het Hallo-code zou hebben gewijzigd. Daarna laten we pakket Hallo toepassing bijgewerkt door met de rechtermuisknop op ***VisualObjectsApplication***, Hallo Service Fabric-Menu selecteren en te kiezen **pakket**. Deze actie wordt gemaakt van een toepassingspakket dat kan worden geïmplementeerd.  De bijgewerkte toepassing is gereed toobe geïmplementeerd.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Stap 3: Bepaal statusbeleid en parameters bijwerken
Maak uzelf bekend met Hallo [parameters voor het bijwerken van toepassing](service-fabric-application-upgrade-parameters.md) en Hallo [upgradeproces](service-fabric-application-upgrade.md) tooget een goed begrip van Hallo verschillende parameters, time-outs en health criterium toegepast upgraden . Voor dit scenario is Hallo service health evaluatiecriterium toohello instellen (en aanbevolen) waarden, wat betekent dat alle services en -exemplaren moeten *orde* na de upgrade Hallo.  

Hallo echter we verhogen *HealthCheckStableDuration* too60 seconden (zodat Hallo-services zijn in orde voor ten minste 20 seconden voordat de upgrade Hallo wordt voortgezet toohello naast domein bijwerken).  Stel de Hallo ook *UpgradeDomainTimeout* toobe 1200 seconden en Hallo *UpgradeTimeout* toobe 3000 seconden.

Tot slot gaan we ook stelt Hallo *UpgradeFailureAction* toorollback. Deze optie vereist Service Fabric tooroll back Hallo toohello vorige toepassingsversie als er problemen worden aangetroffen tijdens het Hallo-upgrade. Dus bij het starten van de upgrade hello (in stap 4) worden hello volgende parameters opgegeven:

FailureAction = terugdraaien

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec 1200 =

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Stap 4: De toepassing voor een upgrade voorbereiden
Nu de toepassing hello wordt samengesteld en gereed toobe bijgewerkt. Als u het openen van een PowerShell-venster als beheerder en typ [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), het laat u weten dat het toepassingstype 1.0.0.0 van **VisualObjects** die zijn geïmplementeerd.  

Hallo toepassingspakket wordt opgeslagen onder de volgende Hallo relatief pad waar u Hallo Service Fabric SDK - ongecomprimeerde *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. U moet een pakketmap '' vinden in die map waar het Hallo-toepassingspakket wordt opgeslagen. Controleer Hallo tijdstempels tooensure is de laatste build hello (mogelijk moet u ook op de juiste wijze toomodify Hallo paden).

Nu gaan we bijgewerkt kopie Hallo toepassing pakket toohello Service Fabric Installatiekopieopslag (waar Hallo toepassingspakketten zijn opgeslagen door de Fabric-Service). parameter Hallo *ApplicationPackagePathInImageStore* informeert Service Fabric waar het Hallo-toepassingspakket kan vinden. We hebben bijgewerkt Hallo toepassing plaatsen ' VisualObjects\_V2 ' Hello opdracht (mogelijk moet u toomodify paden opnieuw op de juiste wijze) te volgen.

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

de volgende stap Hallo tooregister is deze toepassing met Service Fabric, die kan worden uitgevoerd met behulp van Hallo [registreren ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) opdracht:

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Als hello voorgaande opdracht niet lukt, is het waarschijnlijk dat u het opbouwen van alle services moet. Zoals vermeld in stap 2, wellicht tooupdate uw WebService-versie.

## <a name="step-5-start-hello-application-upgrade"></a>Stap 5: Start de upgrade van de toepassing hello
Nu we zijn alle set toostart Hallo toepassing upgraden met behulp van Hallo [Start ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) opdracht:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Hallo toepassingsnaam is Hallo dezelfde zoals beschreven in Hallo *ApplicationManifest.xml* bestand. Service Fabric gebruikt deze naam tooidentify welke toepassing wordt ophalen bijgewerkt. Als u Hallo time-outs toobe te kort instelt, kunt u een foutbericht dat statussen Hallo probleem tegenkomen. Raadpleeg de sectie Probleemoplossing toohello of Hallo time-outs vergroot.

Nu, zoals upgrade opbrengst toepassing hello, kunt u deze bewaken met behulp van Service Fabric Explorer of met behulp van Hallo [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) PowerShell-opdracht: 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

In een paar minuten Hallo status die u hebt verkregen via Hallo voorafgaand aan de PowerShell-opdracht moet staat dat alle domeinen van de update zijn bijgewerkt (voltooid). En zult u visuele objecten in uw browservenster Hallo hebt gestart roteren!

Een upgrade van versie 2 tooversion 3 of van versie 2 tooversion 1 wijze van oefening maakt, kunt u proberen. Verplaatsen van versie 2 tooversion 1 wordt ook beschouwd als een upgrade. Spelen met time-outs en health beleid toomake uzelf bekend mee. Wanneer u tooan Azure-cluster implementeert, Hallo u parameters nodig toobe ingesteld op de juiste wijze. Goede tooset Hallo time-outs is conservatieve.

## <a name="next-steps"></a>Volgende stappen
[Bijwerken van uw toepassing met Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.

Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [parameters upgrade](service-fabric-application-upgrade-parameters.md).

Uw toepassingsupgrades compatibel maken door leren hoe toouse [serialisatie van gegevens](service-fabric-application-upgrade-data-serialization.md).

Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).

Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [probleemoplossing toepassingsupgrades](service-fabric-application-upgrade-troubleshooting.md).

