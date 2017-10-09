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
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="c3da4-103">Upgrade van uw zelfstandige Azure Service Fabric op Windows Server-cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3da4-104">Azure-Cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="c3da4-105">Zelfstandige Cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="c3da4-106">Voor elk moderne systeem is Hallo mogelijkheid tooupgrade geslaagd sleutel toohello op lange termijn van uw product.</span><span class="sxs-lookup"><span data-stu-id="c3da4-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="c3da4-107">Een Azure Service Fabric-cluster is een resource waarvan u eigenaar.</span><span class="sxs-lookup"><span data-stu-id="c3da4-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="c3da4-108">Dit artikel wordt beschreven hoe u ervoor kunt zorgen dat cluster hello wordt altijd uitgevoerd ondersteunde versies van Service Fabric-code en configuraties.</span><span class="sxs-lookup"><span data-stu-id="c3da4-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="c3da4-109">Besturingselement Hallo Service Fabric-versie die wordt uitgevoerd op het cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="c3da4-110">tooset updates voor uw cluster toodownload van Service Fabric wanneer Microsoft een nieuwe versie, set Hallo loslaat **fabricClusterAutoupgradeEnabled** configuratie tootrue cluster.</span><span class="sxs-lookup"><span data-stu-id="c3da4-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="c3da4-111">een ondersteunde versie van Service Fabric die u wilt dat uw cluster toobe op set Hallo tooselect **fabricClusterAutoupgradeEnabled** configuratie toofalse cluster.</span><span class="sxs-lookup"><span data-stu-id="c3da4-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="c3da4-112">Zorg ervoor dat uw cluster altijd wordt uitgevoerd een ondersteunde versie van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c3da4-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="c3da4-113">Wanneer Microsoft Hallo-release van een nieuwe versie van Service Fabric introduceert, is Hallo vorige versie na een minimum van 60 dagen na de datum van de aankondiging Hallo Hallo gemarkeerd voor einde van ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="c3da4-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="c3da4-114">Nieuwe releases worden aangekondigd [op Hallo Service Fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="c3da4-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="c3da4-115">Hallo nieuwe release is beschikbaar toochoose op dat moment.</span><span class="sxs-lookup"><span data-stu-id="c3da4-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="c3da4-116">Alleen als u een productie-stijl knooppuntconfiguratie, waarbij elk Service Fabric-knooppunt is toegewezen aan een afzonderlijke fysieke of virtuele machine, kunt u uw cluster toohello nieuwe versie upgraden.</span><span class="sxs-lookup"><span data-stu-id="c3da4-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="c3da4-117">Als u een ontwikkelcluster waarbij meer dan één Service Fabric-knooppunt op een enkele fysieke of virtuele machine hebt is, moet u Hallo-cluster met de nieuwe versie Hallo opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="c3da4-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="c3da4-118">Twee afzonderlijke werkstromen kunnen upgraden voor uw cluster toohello meest recente versie of een ondersteunde versie van de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c3da4-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="c3da4-119">Een werkstroom is voor clusters die automatisch verbinding toodownload Hallo meest recente versie hebt.</span><span class="sxs-lookup"><span data-stu-id="c3da4-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="c3da4-120">Hallo andere werkstroom is voor clusters die geen connectiviteit toodownload Hallo nieuwste Service Fabric-versie.</span><span class="sxs-lookup"><span data-stu-id="c3da4-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="c3da4-121">Bijwerken van clusters met connectiviteit toodownload Hallo meest recente code en configuratie</span><span class="sxs-lookup"><span data-stu-id="c3da4-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="c3da4-122">Deze stappen tooupgrade uw cluster tooa ondersteund versie gebruiken als de clusterknooppunten beschikt over een internetverbinding te[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c3da4-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="c3da4-123">Voor clusters die verbonden te zijn[http://download.microsoft.com](http://download.microsoft.com), Microsoft controleert periodiek op Hallo beschikbaarheid van de nieuwe Service Fabric-versies.</span><span class="sxs-lookup"><span data-stu-id="c3da4-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="c3da4-124">Wanneer een nieuwe Service Fabric-versie beschikbaar is, Hallo pakket lokaal wordt gedownload toohello cluster en ingericht voor upgrade.</span><span class="sxs-lookup"><span data-stu-id="c3da4-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="c3da4-125">Bovendien tooinform Hallo klant van deze nieuwe versie, Hallo system ziet u een waarschuwing expliciete cluster die soortgelijke toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3da4-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="c3da4-126">'Hallo huidige versie [versie #] clusterondersteuning eindigt [datum]'.</span><span class="sxs-lookup"><span data-stu-id="c3da4-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="c3da4-127">Nadat het Hallo-cluster wordt uitgevoerd de meest recente versie hello, verdwijnt Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c3da4-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="c3da4-128">Werkstroom voor serverupgrades cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="c3da4-129">Nadat u Hallo cluster waarschuwing ziet, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3da4-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="c3da4-130">Toohello cluster vanaf een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in cluster Hallo verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="c3da4-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="c3da4-131">Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c3da4-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

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

2. <span data-ttu-id="c3da4-132">Hallo-lijst van Service Fabric-versies die u naar upgraden kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="c3da4-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="c3da4-133">Deze krijgt u een vergelijkbare toothis uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c3da4-133">You should get an output similar toothis:</span></span>

    ![fabric-versies ophalen][getfabversions]
3. <span data-ttu-id="c3da4-135">Starten van een cluster upgrade tooan beschikbare versie met behulp van de [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span><span class="sxs-lookup"><span data-stu-id="c3da4-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="c3da4-136">toomonitor Hallo voortgang van de upgrade hello, kunt u Service Fabric Explorer of Voer Hallo volgende Windows PowerShell-opdracht.</span><span class="sxs-lookup"><span data-stu-id="c3da4-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="c3da4-137">Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="c3da4-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="c3da4-138">aangepaste statusbeleid voor Hallo toospecify **Start ServiceFabricClusterUpgrade** opdracht, Zie de documentatie voor [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3da4-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="c3da4-139">Nadat u problemen met de Hallo dat heeft geresulteerd in Hallo terugdraaien hebt opgelost, start u Hallo upgrade opnieuw door de volgende Hallo dezelfde stappen als eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="c3da4-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="c3da4-140">Bijwerken van clusters met <U>geen verbinding</u> toodownload Hallo meest recente code en configuratie</span><span class="sxs-lookup"><span data-stu-id="c3da4-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="c3da4-141">Deze stappen tooupgrade uw cluster tooa ondersteund versie gebruiken als de clusterknooppunten geen verbinding met Internet te[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c3da4-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="c3da4-142">Als u een cluster dat is niet verbonden toohello Internet uitvoert, hebt u toomonitor Hallo Service Fabric-team blog toolearn over een nieuwe release.</span><span class="sxs-lookup"><span data-stu-id="c3da4-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="c3da4-143">Hallo-systeem wordt niet weergegeven voor een cluster health waarschuwing tooalert u een nieuwe release.</span><span class="sxs-lookup"><span data-stu-id="c3da4-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="c3da4-144">Automatische inrichting tegenover handmatige inrichting</span><span class="sxs-lookup"><span data-stu-id="c3da4-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="c3da4-145">tooenable automatisch downloaden en registratie voor de meest recente code-versie hello, instellen van Service Fabric-Update-Service.</span><span class="sxs-lookup"><span data-stu-id="c3da4-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="c3da4-146">Raadpleeg toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt binnen Hallo [zelfstandig pakket](service-fabric-cluster-standalone-package-contents.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="c3da4-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="c3da4-147">Volg onderstaande instructies voor Hallo voor handmatige verwerking.</span><span class="sxs-lookup"><span data-stu-id="c3da4-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="c3da4-148">Uw cluster configuratie tooset Hallo eigenschap toofalse volgen voordat u een upgrade van een configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3da4-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="c3da4-149">Raadpleeg te[Start ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) voor informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="c3da4-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="c3da4-150">Zorg ervoor dat tooupdate 'clusterConfigurationVersion' in de JSON voordat u Hallo configuratie upgrade start.</span><span class="sxs-lookup"><span data-stu-id="c3da4-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="c3da4-151">Werkstroom voor serverupgrades cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="c3da4-152">Get-ServiceFabricClusterUpgrade uitvoeren vanaf een van de knooppunten Hallo in Hallo-cluster en noteer Hallo TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="c3da4-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="c3da4-153">Voer Hallo volgende vanaf een internet verbonden machine toolist alle compatibele versies met de huidige versie Hallo upgraden en download Hallo pakket van de bijbehorende downloadkoppelingen Hallo overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="c3da4-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="c3da4-154">Toohello cluster vanaf een machine met de beheerder toegang tooall Hallo machines die worden vermeld als knooppunten in cluster Hallo verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="c3da4-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="c3da4-155">Hallo-machine die op dit script wordt uitgevoerd heeft geen toobe onderdeel van Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="c3da4-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="c3da4-156">Hallo gedownload pakket kopiëren naar Hallo cluster image store.</span><span class="sxs-lookup"><span data-stu-id="c3da4-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="c3da4-157">Hallo gekopieerd pakket registreren.</span><span class="sxs-lookup"><span data-stu-id="c3da4-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="c3da4-158">Start een cluster upgrade tooan beschikbare versie.</span><span class="sxs-lookup"><span data-stu-id="c3da4-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="c3da4-159">U kunt Hallo voortgang van Hallo upgrade in Service Fabric Explorer of Hallo volgende PowerShell-opdracht kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3da4-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="c3da4-160">Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="c3da4-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="c3da4-161">aangepaste statusbeleid voor Hallo toospecify **Start ServiceFabricClusterUpgrade** opdracht, Zie de documentatie voor Hallo [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3da4-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="c3da4-162">Nadat u problemen met de Hallo dat heeft geresulteerd in Hallo terugdraaien hebt opgelost, start u Hallo upgrade opnieuw door de volgende Hallo dezelfde stappen als eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="c3da4-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="c3da4-163">Hallo-clusterconfiguratie upgraden</span><span class="sxs-lookup"><span data-stu-id="c3da4-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="c3da4-164">Voordat u Hallo configuratie upgrade initiëren, kunt u het nieuwe cluster configuratie json testen door Hallo powershell-script in Hallo zelfstandig pakket.</span><span class="sxs-lookup"><span data-stu-id="c3da4-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="c3da4-165">of</span><span class="sxs-lookup"><span data-stu-id="c3da4-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="c3da4-166">Sommige configuraties kunnen niet worden bijgewerkt, zoals eindpunten, de naam van het cluster, knooppunt IP-adres enzovoort. Hiermee wordt de Hallo nieuwe cluster configuratie json tegen Hallo oude testen en fouten in de Powershell-venster Hallo genereren als er een probleem is.</span><span class="sxs-lookup"><span data-stu-id="c3da4-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="c3da4-167">tooupgrade hello cluster configuratie upgrade uitvoeren **Start ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="c3da4-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="c3da4-168">Er is een fout opgetreden in Hallo configuratie upgrade verwerkte upgradedomein door upgradedomein.</span><span class="sxs-lookup"><span data-stu-id="c3da4-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="c3da4-169">Upgraden van cluster certificaat-configuratie</span><span class="sxs-lookup"><span data-stu-id="c3da4-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="c3da4-170">Cluster-certificaat wordt gebruikt voor authenticatie tussen clusterknooppunten, zodat Hallo certificaat via moeten worden uitgevoerd met extra voorzichtig omdat fout Hallo communicatie tussen clusterknooppunten wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="c3da4-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="c3da4-171">Technisch gezien is worden drie opties ondersteund:</span><span class="sxs-lookup"><span data-stu-id="c3da4-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="c3da4-172">Er wordt één certificaat upgrade: Hallo upgradepad is ' certificaat een (primaire) -> certificaat B (primair) -> certificaat C (primair) ->...'.</span><span class="sxs-lookup"><span data-stu-id="c3da4-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="c3da4-173">Dubbele certificaat upgrade: Hallo upgradepad is ' certificaat een (primaire) -> van het certificaat een (primaire) en B (secundair) -> certificaat B (primair) -> certificaat B (primair) en C (secundair) -> certificaat C (primair) ->...'.</span><span class="sxs-lookup"><span data-stu-id="c3da4-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="c3da4-174">Type upgrade van het certificaat: op basis van de vingerafdruk van certificaat configuratie <>--certificaat CommonName gebaseerde configuratie.</span><span class="sxs-lookup"><span data-stu-id="c3da4-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="c3da4-175">Bijvoorbeeld, de vingerafdruk van het certificaat een (primaire) en vingerafdruk B (secundair) -> certificaat CommonName C.</span><span class="sxs-lookup"><span data-stu-id="c3da4-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c3da4-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3da4-176">Next steps</span></span>
* <span data-ttu-id="c3da4-177">Meer informatie over hoe toocustomize sommige [Service Fabric-clusterinstellingen](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c3da4-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="c3da4-178">Meer informatie over hoe te[in en uit het cluster schalen](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="c3da4-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="c3da4-179">Meer informatie over [toepassingsupgrades](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="c3da4-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
