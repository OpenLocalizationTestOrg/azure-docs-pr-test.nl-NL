---
title: aaaCreate zelfstandige Azure Service Fabric-cluster | Microsoft Docs
description: Een Azure Service Fabric-cluster maken op elke computer (fysiek of virtueel) Windows Server, of het lokale of uitgevoerd in een cloud.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Een zelfstandige cluster met Windows Server maken
U kunt Azure Service Fabric toocreate Service Fabric-clusters op elke virtuele machines of computers met Windows Server gebruiken. Dit betekent dat u kunt implementeren en Service Fabric-toepassingen uitvoeren in een omgeving die een set met elkaar verbonden computers met Windows Server bevat, worden deze on-premises of bij een cloudprovider. Service Fabric bevat een setup-pakket toocreate die service Fabric-clusters Hallo zelfstandig pakket met Windows Server.

Dit artikel begeleidt u bij Hallo stappen voor het maken van een zelfstandige Service Fabric-cluster.

> [!NOTE]
> Dit zelfstandige Windows Server-pakket is commercieel beschikbaar en kan worden gebruikt voor productie-implementaties. Dit pakket bevat nieuwe Service Fabric-functies die 'in Preview' zijn. Schuif naar beneden te'[Preview-functies die zijn opgenomen in dit pakket](#previewfeatures_anchor). " de sectie voor Hallo lijst van Hallo preview-functies. U kunt [download een exemplaar van Hallo overeenkomst](http://go.microsoft.com/fwlink/?LinkID=733084) nu.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Ondersteuning krijgen voor Hallo Service Fabric voor Windows Server-pakket
* Vraag het Hallo-community over Hallo Service Fabric zelfstandige pakket voor Windows Server in Hallo [Azure Service Fabric-forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Open een serviceticket voor [Professional-ondersteuning voor Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).  Meer informatie over ondersteuning van Microsoft-professionals [hier](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* U kunt ook ondersteuning voor dit pakket als onderdeel van [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).
* Zie voor meer informatie [opties voor ondersteuning van Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* toocollect logboeken voor ondersteuning, Voer Hallo [Service Fabric zelfstandige logboekverzamelaar](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Hallo-Service Fabric voor Windows Server downloaden
toocreate hello cluster, gebruik Hallo Service Fabric voor Windows Server-pakket (Windows Server 2012 R2 en nieuwer) hier vinden: <br>
[Link - Service Fabric zelfstandige Package - Windows-Server downloaden](http://go.microsoft.com/fwlink/?LinkId=730690)

Meer informatie vinden van inhoud van pakket Hallo [hier](service-fabric-cluster-standalone-package-contents.md).

Hallo Service Fabric-runtime-pakket is automatisch gedownload tijdens het maken van het cluster. Als het implementeren van een virtuele machine niet verbonden toohello internet, download Hallo runtime-pakket buiten-bandbeheer van hier: <br>
[Link - Service Fabric-Runtime - Windows-Server downloaden](https://go.microsoft.com/fwlink/?linkid=839354)

Voorbeelden van de zelfstandige configuratie van het Cluster op zoeken: <br>
[Voorbeelden van zelfstandige clusterconfiguratie](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Hallo-cluster maken
Service Fabric geïmplementeerde tooa één machine ontwikkelcluster kan worden met behulp van Hallo *ClusterConfig.Unsecure.DevCluster.json* bestand in [voorbeelden](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Uitpakken Hallo zelfstandige pakket tooyour machine, kopie Hallo voorbeeld config bestand toohello lokale computer en Voer Hallo *CreateServiceFabricCluster.ps1* script via een beheerder PowerShell-sessie van Hallo zelfstandige Pakketmap:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Stap 1A: een onbeveiligde lokaal ontwikkelcluster maken
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Zie de sectie omgeving in te stellen op Hallo [plannen en voorbereiden van uw implementatie van het cluster](service-fabric-cluster-standalone-deployment-preparation.md) voor de details voor probleemoplossing.

Als u actieve ontwikkelscenario's hebt voltooid, kunt u Hallo Service Fabric-cluster verwijderen uit de Hallo machine door te verwijzen toosteps in sectie '[verwijderen van een cluster](#removecluster_anchor)'. 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Stap 1B: een cluster met meerdere machines maken
Nadat u hebt doorlopen Hallo plannen en de voorbereidende stappen op gedetailleerde op Hallo onderstaande koppeling, u bent klaar toocreate uw productiecluster met behulp van het configuratiebestand van het cluster. <br>
[Plannen en voorbereiden van uw implementatie van het cluster](service-fabric-cluster-standalone-deployment-preparation.md)

1. Hallo-configuratiebestand u hebt geschreven door het uitvoeren van Hallo valideren *TestConfiguration.ps1* script vanaf Hallo zelfstandige pakketmap:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Ziet u uitvoer zoals hieronder. Als Hallo onder veld 'Passed' wordt geretourneerd als 'True', bevestigingen hebt doorgegeven en Hallo cluster lijkt toobe geïmplementeerd op basis van invoer Hallo-configuratie.

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. Hallo-cluster maken: Hallo uitvoeren *CreateServiceFabricCluster.ps1* script toodeploy Hallo Service Fabric-cluster op elke computer in Hallo-configuratie. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Implementatie traceringen worden geschreven toohello VM/machine waarop u Hallo CreateServiceFabricCluster.ps1 PowerShell-script is uitgevoerd. U vindt deze in Hallo submap DeploymentTraces, op basis van Hallo directory van welke Hallo script wordt uitgevoerd. toosee als Service Fabric is correct is geïmplementeerd tooa machine, Hallo geïnstalleerd bestanden gevonden in de directory van het Hallo FabricDataRoot, zoals beschreven in het configuratiebestand voor Hallo cluster FabricSettings sectie (met standaard c:\ProgramData\SF). FabricHost.exe en Fabric.exe processen kunnen ook worden gezien uitgevoerd in Taakbeheer.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Stap 1C: een offline (op internet verbroken)-cluster maken
Hallo Service Fabric-runtime-pakket wordt automatisch bij het maken van het cluster gedownload. Wanneer het implementeren van een cluster toomachines niet toohello verbonden internet, moet u toodownload Hallo Service Fabric runtime afzonderlijk pakket en bieden Hallo pad tooit bij het maken van het cluster.
Hallo runtime-pakket kan afzonderlijk worden gedownload, vanaf een andere computer verbonden toohello internet, op [- Service Fabric-Runtime - koppeling Download Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Kopieer Hallo runtime pakket toowhere u implementeert Hallo offline cluster uit en Hallo cluster maken door het uitvoeren van `CreateServiceFabricCluster.ps1` Hello `-FabricRuntimePackagePath` parameter opgenomen, zoals hieronder wordt weergegeven: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
waar `.\ClusterConfig.json` en `.\MicrosoftAzureServiceFabric.cab` zijn respectievelijk Hallo paden toohello clusterconfiguratie en Hallo runtime CAB-bestand.


### <a name="step-2-connect-toohello-cluster"></a>Stap 2: Verbinding maken met cluster toohello
tooconnect tooa beveiligde cluster, Zie [Service fabric-cluster toosecure verbinding](service-fabric-connect-to-secure-cluster.md).

tooconnect tooan onbeveiligde cluster Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Voorbeeld:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Stap 3: Online zetten van de Service Fabric Explorer
Nu u toohello cluster verbinding met Service Fabric Explorer vanuit een van de machines Hallo http://localhost:19080/Explorer/index.html of op afstand met http://&lt maken kunt;*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Toevoegen en verwijderen van knooppunten
U kunt toevoegen of verwijderen van knooppunten tooyour zelfstandige Service Fabric-cluster als uw bedrijf. Zie [toevoegen of verwijderen van knooppunten tooa Service Fabric-cluster voor zelfstandige](service-fabric-cluster-windows-server-add-remove-nodes.md) voor gedetailleerde stappen.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Verwijderen van een cluster
tooremove een cluster uitvoert Hallo *RemoveServiceFabricCluster.ps1* PowerShell-script van de pakketmap Hallo en geeft u Hallo pad toohello JSON-configuratiebestand. U kunt optioneel een locatie voor Hallo logboek van Hallo verwijdering opgeven.

Dit script kan worden uitgevoerd op een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in het configuratiebestand Hallo-cluster. Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Telemetrische gegevens verzameld en hoe tooopt buiten het
Standaard verzamelt Hallo product telemetrie op Hallo Service Fabric-gebruik tooimprove Hallo product. Hallo Best Practices Analyzer die wordt uitgevoerd als een deel van Hallo setup voor connectiviteit te controleert[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Als dit niet bereikbaar is, mislukt de installatie van de Hallo tenzij u telemetrie afmelden.

1. Hallo telemetrie pijplijn probeert tooupload Hallo gegevens te volgen[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) eenmaal voor elke dag. Het uploaden van een best effort is en heeft geen invloed op Hallo clusterfunctionaliteit. Hallo telemetrie wordt alleen verzonden van het Hallo-knooppunt dat wordt uitgevoerd failover manager primaire Hallo. Er zijn geen andere knooppunten verzenden telemetrie.
2. Hallo telemetrie bestaat uit Hallo volgende:

* Aantal services
* Aantal ServiceTypes
* Aantal toepassingen
* Aantal ApplicationUpgrades
* Aantal FailoverUnits
* Aantal InBuildFailoverUnits
* Aantal UnhealthyFailoverUnits
* Aantal replica 's
* Aantal InBuildReplicas
* Aantal StandByReplicas
* Aantal OfflineReplicas
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Het aantal knooppunten
* IsContextComplete: True/False
* ClusterId: Dit is een willekeurig gegenereerd voor elk cluster GUID
* ServiceFabricVersion
* IP-adres van Hallo of machine uit welke Hallo telemetrie is geüpload

toodisable-telemetrie hello te volgende toevoegen*eigenschappen* in uw cluster-config: *enableTelemetry: false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Preview-functies die zijn opgenomen in dit pakket
Geen.


> [!NOTE]
> Beginnen met nieuwe Hallo [GA-versie van Hallo zelfstandige cluster voor Windows Server (versie 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), kunt u uw cluster toofuture versies upgraden handmatig of automatisch. Raadpleeg te[upgraden van een zelfstandige Service Fabric-cluster versie](service-fabric-cluster-upgrade-windows-server.md) document voor meer informatie.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Implementeren en verwijderen van toepassingen met behulp van PowerShell](service-fabric-deploy-remove-applications.md)
* [Configuratie-instellingen voor zelfstandige Windows-cluster](service-fabric-cluster-manifest.md)
* [Toevoegen of verwijderen van knooppunten tooa zelfstandige Service Fabric-cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Een zelfstandige Service Fabric-cluster versie upgraden](service-fabric-cluster-upgrade-windows-server.md)
* [Een zelfstandige Service Fabric-cluster maken met Azure Virtual machines waarop Windows wordt uitgevoerd](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging](service-fabric-windows-cluster-windows-security.md)
* [Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
