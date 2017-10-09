---
title: een zelfstandige Azure Service Fabric-cluster op Windows Server aaaUpgrade | Microsoft Docs
description: Voer een upgrade hello Azure Service Fabric-code en/of de configuratie die wordt uitgevoerd een zelfstandige Service Fabric-cluster, inclusief het instellen van de updatemodus Hallo-cluster.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Upgrade van uw zelfstandige Azure Service Fabric op Windows Server-cluster
> [!div class="op_single_selector"]
> * [Azure-Cluster](service-fabric-cluster-upgrade.md)
> * [Zelfstandige Cluster](service-fabric-cluster-upgrade-windows-server.md)
>
>

Voor elk moderne systeem is Hallo mogelijkheid tooupgrade geslaagd sleutel toohello op lange termijn van uw product. Een Azure Service Fabric-cluster is een resource waarvan u eigenaar. Dit artikel wordt beschreven hoe u ervoor kunt zorgen dat cluster hello wordt altijd uitgevoerd ondersteunde versies van Service Fabric-code en configuraties.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Besturingselement Hallo Service Fabric-versie die wordt uitgevoerd op het cluster
tooset updates voor uw cluster toodownload van Service Fabric wanneer Microsoft een nieuwe versie, set Hallo loslaat **fabricClusterAutoupgradeEnabled** configuratie tootrue cluster. een ondersteunde versie van Service Fabric die u wilt dat uw cluster toobe op set Hallo tooselect **fabricClusterAutoupgradeEnabled** configuratie toofalse cluster.

> [!NOTE]
> Zorg ervoor dat uw cluster altijd wordt uitgevoerd een ondersteunde versie van Service Fabric. Wanneer Microsoft Hallo-release van een nieuwe versie van Service Fabric introduceert, is Hallo vorige versie na een minimum van 60 dagen na de datum van de aankondiging Hallo Hallo gemarkeerd voor einde van ondersteuning. Nieuwe releases worden aangekondigd [op Hallo Service Fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/). Hallo nieuwe release is beschikbaar toochoose op dat moment.
>
>

Alleen als u een productie-stijl knooppuntconfiguratie, waarbij elk Service Fabric-knooppunt is toegewezen aan een afzonderlijke fysieke of virtuele machine, kunt u uw cluster toohello nieuwe versie upgraden. Als u een ontwikkelcluster waarbij meer dan één Service Fabric-knooppunt op een enkele fysieke of virtuele machine hebt is, moet u Hallo-cluster met de nieuwe versie Hallo opnieuw maken.

Twee afzonderlijke werkstromen kunnen upgraden voor uw cluster toohello meest recente versie of een ondersteunde versie van de Service Fabric. Een werkstroom is voor clusters die automatisch verbinding toodownload Hallo meest recente versie hebt. Hallo andere werkstroom is voor clusters die geen connectiviteit toodownload Hallo nieuwste Service Fabric-versie.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Bijwerken van clusters met connectiviteit toodownload Hallo meest recente code en configuratie
Deze stappen tooupgrade uw cluster tooa ondersteund versie gebruiken als de clusterknooppunten beschikt over een internetverbinding te[http://download.microsoft.com](http://download.microsoft.com).

Voor clusters die verbonden te zijn[http://download.microsoft.com](http://download.microsoft.com), Microsoft controleert periodiek op Hallo beschikbaarheid van de nieuwe Service Fabric-versies.

Wanneer een nieuwe Service Fabric-versie beschikbaar is, Hallo pakket lokaal wordt gedownload toohello cluster en ingericht voor upgrade. Bovendien tooinform Hallo klant van deze nieuwe versie, Hallo system ziet u een waarschuwing expliciete cluster die soortgelijke toohello te volgen:

'Hallo huidige versie [versie #] clusterondersteuning eindigt [datum]'.

Nadat het Hallo-cluster wordt uitgevoerd de meest recente versie hello, verdwijnt Hallo waarschuwing.

#### <a name="cluster-upgrade-workflow"></a>Werkstroom voor serverupgrades cluster
Nadat u Hallo cluster waarschuwing ziet, Hallo te volgen:

1. Toohello cluster vanaf een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in cluster Hallo verbinding te maken. Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Hallo-lijst van Service Fabric-versies die u naar upgraden kunt ophalen.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Deze krijgt u een vergelijkbare toothis uitvoer:

    ![fabric-versies ophalen][getfabversions]
3. Starten van een cluster upgrade tooan beschikbare versie met behulp van de [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   toomonitor Hallo voortgang van de upgrade hello, kunt u Service Fabric Explorer of Voer Hallo volgende Windows PowerShell-opdracht.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid. aangepaste statusbeleid voor Hallo toospecify **Start ServiceFabricClusterUpgrade** opdracht, Zie de documentatie voor [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Nadat u problemen met de Hallo dat heeft geresulteerd in Hallo terugdraaien hebt opgelost, start u Hallo upgrade opnieuw door de volgende Hallo dezelfde stappen als eerder beschreven.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Bijwerken van clusters met <U>geen verbinding</u> toodownload Hallo meest recente code en configuratie
Deze stappen tooupgrade uw cluster tooa ondersteund versie gebruiken als de clusterknooppunten geen verbinding met Internet te[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Als u een cluster dat is niet verbonden toohello Internet uitvoert, hebt u toomonitor Hallo Service Fabric-team blog toolearn over een nieuwe release. Hallo-systeem wordt niet weergegeven voor een cluster health waarschuwing tooalert u een nieuwe release.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Automatische inrichting tegenover handmatige inrichting
tooenable automatisch downloaden en registratie voor de meest recente code-versie hello, instellen van Service Fabric-Update-Service. Raadpleeg toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt binnen Hallo [zelfstandig pakket](service-fabric-cluster-standalone-package-contents.md) voor instructies.
Volg onderstaande instructies voor Hallo voor handmatige verwerking.

Uw cluster configuratie tooset Hallo eigenschap toofalse volgen voordat u een upgrade van een configuratie wijzigen.

        "fabricClusterAutoupgradeEnabled": false,

Raadpleeg te[Start ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) voor informatie over het gebruik. Zorg ervoor dat tooupdate 'clusterConfigurationVersion' in de JSON voordat u Hallo configuratie upgrade start.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Werkstroom voor serverupgrades cluster

1. Get-ServiceFabricClusterUpgrade uitvoeren vanaf een van de knooppunten Hallo in Hallo-cluster en noteer Hallo TargetCodeVersion.
2. Voer Hallo volgende vanaf een internet verbonden machine toolist alle compatibele versies met de huidige versie Hallo upgraden en download Hallo pakket van de bijbehorende downloadkoppelingen Hallo overeenkomt.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Toohello cluster vanaf een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in cluster Hallo verbinding te maken. Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Hallo gedownload pakket kopiëren naar Hallo cluster image store.

5. Hallo gekopieerd pakket registreren.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Start een cluster upgrade tooan beschikbare versie.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   U kunt Hallo voortgang van Hallo upgrade in Service Fabric Explorer of Hallo volgende PowerShell-opdracht kan worden uitgevoerd.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid. aangepaste statusbeleid voor Hallo toospecify **Start ServiceFabricClusterUpgrade** opdracht, Zie de documentatie voor Hallo [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Nadat u problemen met de Hallo dat heeft geresulteerd in Hallo terugdraaien hebt opgelost, start u Hallo upgrade opnieuw door de volgende Hallo dezelfde stappen als eerder beschreven.


## <a name="upgrade-hello-cluster-configuration"></a>Hallo-clusterconfiguratie upgraden
Voordat u Hallo configuratie upgrade initiëren, kunt u het nieuwe cluster configuratie json testen door Hallo powershell-script in Hallo zelfstandig pakket.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
of

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Sommige configuraties kunnen niet worden bijgewerkt, zoals eindpunten, de naam van het cluster, knooppunt IP-adres enzovoort. Hiermee wordt de Hallo nieuwe cluster configuratie json tegen Hallo oude testen en fouten in de Powershell-venster Hallo genereren als er een probleem is.

tooupgrade hello cluster configuratie upgrade uitvoeren **Start ServiceFabricClusterConfigurationUpgrade**. Er is een fout opgetreden in Hallo configuratie upgrade verwerkte upgradedomein door upgradedomein.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Upgraden van cluster certificaat-configuratie  
Cluster-certificaat wordt gebruikt voor authenticatie tussen clusterknooppunten, zodat Hallo certificaat via moeten worden uitgevoerd met extra voorzichtig omdat fout Hallo communicatie tussen clusterknooppunten wordt geblokkeerd.  
Technisch gezien is worden drie opties ondersteund:  

1. Er wordt één certificaat upgrade: Hallo upgradepad is ' certificaat een (primaire) -> certificaat B (primair) -> certificaat C (primair) ->...'.   
2. Dubbele certificaat upgrade: Hallo upgradepad is ' certificaat een (primaire) -> van het certificaat een (primaire) en B (secundair) -> certificaat B (primair) -> certificaat B (primair) en C (secundair) -> certificaat C (primair) ->...'.
3. Type upgrade van het certificaat: op basis van de vingerafdruk van certificaat configuratie <>--certificaat CommonName gebaseerde configuratie. Bijvoorbeeld, de vingerafdruk van het certificaat een (primaire) en vingerafdruk B (secundair) -> certificaat CommonName C.


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe toocustomize sommige [Service Fabric-clusterinstellingen](service-fabric-cluster-fabric-settings.md).
* Meer informatie over hoe te[in en uit het cluster schalen](service-fabric-cluster-scale-up-down.md).
* Meer informatie over [toepassingsupgrades](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
