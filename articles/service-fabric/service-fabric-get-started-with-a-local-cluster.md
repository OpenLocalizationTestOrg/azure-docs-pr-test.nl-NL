---
title: aaaDeploy en Azure microservices lokaal upgrade | Microsoft Docs
description: Ontdek hoe tooset een lokale Service Fabric-cluster implementeren van een bestaande toepassing tooit en werkt u de toepassing.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="aece6-103">Aan de slag met het implementeren en bijwerken van toepassingen op uw lokale cluster</span><span class="sxs-lookup"><span data-stu-id="aece6-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="aece6-104">Hello Azure Service Fabric SDK bevat een volledig lokale ontwikkelingsomgeving waarmee u kunt tooquickly aan de slag met het implementeren en beheren van toepassingen op een lokaal cluster.</span><span class="sxs-lookup"><span data-stu-id="aece6-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="aece6-105">In dit artikel wordt een lokaal cluster maken, een bestaande toepassing tooit implementeren en vervolgens een upgrade die nieuwe versie tooa van de toepassing, vanuit Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aece6-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="aece6-106">In dit artikel wordt ervan uitgegaan dat u [uw ontwikkelingsomgeving](service-fabric-get-started.md) al hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="aece6-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="aece6-107">Een lokaal cluster maken</span><span class="sxs-lookup"><span data-stu-id="aece6-107">Create a local cluster</span></span>
<span data-ttu-id="aece6-108">Een Service Fabric-cluster vertegenwoordigt een aantal hardwareresources waarvoor u toepassingen kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="aece6-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="aece6-109">Normaal gesproken een cluster bestaat uit een willekeurige plaats van vijf toomany duizenden computers.</span><span class="sxs-lookup"><span data-stu-id="aece6-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="aece6-110">Hallo Service Fabric SDK bevat echter een clusterconfiguratie die kan worden uitgevoerd op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="aece6-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="aece6-111">Het is belangrijk toounderstand die Hallo lokale Service Fabric-cluster is niet een emulator of simulator.</span><span class="sxs-lookup"><span data-stu-id="aece6-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="aece6-112">Deze wordt uitgevoerd Hallo dezelfde platformcode is gevonden in clusters met meerdere machines.</span><span class="sxs-lookup"><span data-stu-id="aece6-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="aece6-113">Hallo enige verschil is dat deze Hallo platform processen die doorgaans worden verdeeld over vijf machines op één computer wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aece6-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="aece6-114">Hallo SDK biedt twee manieren tooset van een lokaal cluster: een Windows PowerShell-script en Hallo lokaal Clusterbeheer systeemvak van de app.</span><span class="sxs-lookup"><span data-stu-id="aece6-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="aece6-115">In deze zelfstudie gebruiken we Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="aece6-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="aece6-116">Als u al een lokaal cluster hebt gemaakt door een toepassing te implementeren vanuit Visual Studio hebt gemaakt, kunt u dit gedeelte overslaan.</span><span class="sxs-lookup"><span data-stu-id="aece6-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="aece6-117">Start een nieuw PowerShell-venster als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aece6-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="aece6-118">Voer Hallo cluster setup-script uit Hallo SDK-map:</span><span class="sxs-lookup"><span data-stu-id="aece6-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="aece6-119">Het installeren van een cluster duurt even.</span><span class="sxs-lookup"><span data-stu-id="aece6-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="aece6-120">Nadat Setup is voltooid, ziet u soortgelijke uitvoer als deze:</span><span class="sxs-lookup"><span data-stu-id="aece6-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Cluster-installatieuitvoer][cluster-setup-success]
   
    <span data-ttu-id="aece6-122">U bent nu klaar tootry een toepassing tooyour-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="aece6-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="aece6-123">Een app implementeren</span><span class="sxs-lookup"><span data-stu-id="aece6-123">Deploy an application</span></span>
<span data-ttu-id="aece6-124">Hallo Service Fabric SDK bevat een uitgebreide reeks frameworks en ontwikkelaarstools voor het maken van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="aece6-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="aece6-125">Als u geïnteresseerd bent in leren hoe toocreate toepassingen in Visual Studio, Zie [uw eerste Service Fabric-toepassing maken in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="aece6-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="aece6-126">In deze zelfstudie maakt u een bestaande voorbeeldtoepassing (WordCount genoemd) zodat u zich op Hallo management aspecten van Hallo-platform richten kunt: implementatie, bewaking en upgrade.</span><span class="sxs-lookup"><span data-stu-id="aece6-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="aece6-127">Start een nieuw PowerShell-venster als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aece6-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="aece6-128">Hallo Service Fabric SDK PowerShell-module importeren.</span><span class="sxs-lookup"><span data-stu-id="aece6-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="aece6-129">Maak een map toostore Hallo-toepassing die u downloadt en implementeert, bijvoorbeeld C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="aece6-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="aece6-130">[Download het WordCount-toepassing hello](http://aka.ms/servicefabric-wordcountapp) toohello locatie die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aece6-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="aece6-131">Opmerking: Hallo Microsoft Edge-browser slaat Hallo-bestand met een *.zip* extensie.</span><span class="sxs-lookup"><span data-stu-id="aece6-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="aece6-132">Hallo-bestandsextensie ook wijzigen*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="aece6-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="aece6-133">Verbinding maken met het lokale cluster toohello:</span><span class="sxs-lookup"><span data-stu-id="aece6-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="aece6-134">Maak een nieuwe toepassing hello SDK implementatieopdracht met een naam en een pad toohello-toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="aece6-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="aece6-135">Als alles goed gaat, ziet u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="aece6-135">If all goes well, you should see hello following output:</span></span>
   
    ![Een toepassing toohello lokale cluster implementeren][deploy-app-to-local-cluster]
7. <span data-ttu-id="aece6-137">toosee hello toepassing in actie, Hallo browser starten en te navigeren[http://localhost: 8081/WordCount/index.HTML](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="aece6-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="aece6-138">U ziet het volgende:</span><span class="sxs-lookup"><span data-stu-id="aece6-138">You should see:</span></span>
   
    ![De UI van de geïmplementeerde toepassing][deployed-app-ui]
   
    <span data-ttu-id="aece6-140">Hallo WordCount-toepassing is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="aece6-140">hello WordCount application is simple.</span></span> <span data-ttu-id="aece6-141">Het omvat client-side JavaScript-code toogenerate willekeurige vijf tekens 'woorden', die vervolgens doorgegeven toohello toepassing via ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="aece6-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="aece6-142">Een stateful service houdt het aantal woorden geteld Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="aece6-143">Ze worden gepartitioneerd op basis van het eerste teken van de Hallo van Hallo woord.</span><span class="sxs-lookup"><span data-stu-id="aece6-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="aece6-144">U vindt de broncode Hallo Hallo WordCount App in Hallo [klassieke introductie voorbeelden](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="aece6-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="aece6-145">Hallo-toepassing die we hebben geïmplementeerd bevat vier partities.</span><span class="sxs-lookup"><span data-stu-id="aece6-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="aece6-146">Zodat woorden die beginnen met A tot G worden opgeslagen in de eerste partitie hello, worden woorden die beginnen met H tot N worden opgeslagen in de tweede partitie hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="aece6-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="aece6-147">Details en de status van de toepassing weergeven</span><span class="sxs-lookup"><span data-stu-id="aece6-147">View application details and status</span></span>
<span data-ttu-id="aece6-148">Nu dat we Hallo toepassing hebt geïmplementeerd, bekijken we enkele van de gegevens van de app Hallo in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aece6-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="aece6-149">Query alle geïmplementeerde toepassingen op Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="aece6-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="aece6-150">Ervan uitgaande dat u alleen Hallo WordCount app hebt geïmplementeerd, ziet u iets soortgelijks als:</span><span class="sxs-lookup"><span data-stu-id="aece6-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Een query uitvoeren op alle geïmplementeerde toepassingen in PowerShell;][ps-getsfapp]
2. <span data-ttu-id="aece6-152">Ga toohello volgende niveau door het uitvoeren van query's Hallo set services die zijn opgenomen in de toepassing WordCount Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lijst met services voor de toepassing hello in PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="aece6-154">Hallo toepassing bestaat uit twee services, Hallo webfront-end en Hallo stateful service die Hallo woorden beheert.</span><span class="sxs-lookup"><span data-stu-id="aece6-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="aece6-155">Tot slot bekijkt hello lijst met partities voor WordCountService:</span><span class="sxs-lookup"><span data-stu-id="aece6-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Hallo servicepartities in PowerShell weergeven][ps-getsfpartitions]
   
    <span data-ttu-id="aece6-157">Hallo reeks opdrachten die u, zoals alle Service Fabric PowerShell-opdrachten gebruikt, zijn beschikbaar voor een cluster die u mogelijk verbinding met lokale of externe.</span><span class="sxs-lookup"><span data-stu-id="aece6-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="aece6-158">Voor een meer visuele manier toointeract met Hallo-cluster, kunt u Hallo Service Fabric Explorer Webhulpprogramma door te navigeren[http://localhost: 19080/Explorer](http://localhost:19080/Explorer) in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="aece6-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Toepassingdetails weergeven in Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="aece6-160">Zie toolearn meer informatie over Service Fabric Explorer [uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="aece6-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="aece6-161">Een upgrade van een app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="aece6-161">Upgrade an application</span></span>
<span data-ttu-id="aece6-162">Service Fabric bevat upgrades zonder downtime door de bewaking van Hallo status van de toepassing hello zoals implementatie in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aece6-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="aece6-163">Een upgrade uitvoeren van Hallo WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aece6-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="aece6-164">Hallo nieuwe versie van de toepassing hello nu telt alleen woorden die met een klinkerteken beginnen.</span><span class="sxs-lookup"><span data-stu-id="aece6-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="aece6-165">Als de upgrade Hallo implementeert, ziet u twee zichtbare wijzigingen in gedrag van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="aece6-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="aece6-166">Eerst vertragen Hallo snelheid waarmee Hallo aantal groeit, omdat er minder woorden worden geteld.</span><span class="sxs-lookup"><span data-stu-id="aece6-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="aece6-167">Tweede, aangezien de eerste partitie Hallo twee klinkers (A en E heeft) en alle andere partities slechts één bevatten, het aantal moet uiteindelijk eerst toooutpace Hallo anderen.</span><span class="sxs-lookup"><span data-stu-id="aece6-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="aece6-168">[Hallo WordCount versie 2 van het pakket downloaden](http://aka.ms/servicefabric-wordcountappv2) toohello dezelfde locatie waar u Hallo versie 1 pakket hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="aece6-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="aece6-169">Retourneren tooyour PowerShell-venster en gebruik van de SDK Hallo upgrade opdracht tooregister nieuwe versie in de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="aece6-170">Vervolgens begint met het upgraden van Hallo fabric: / WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aece6-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="aece6-171">U ziet Hallo volgende uitvoer in PowerShell als Hallo upgrade begint.</span><span class="sxs-lookup"><span data-stu-id="aece6-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Voortgang van de upgrade in PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="aece6-173">Tijdens het Hallo-upgrade wordt voortgezet, soms is het eenvoudiger toomonitor de status van Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="aece6-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="aece6-174">Open een browservenster en navigeer te[http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="aece6-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="aece6-175">Vouw **toepassingen** Kies in de boomstructuur Hallo op Hallo links van **WordCount**, en tot slot **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="aece6-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="aece6-176">Hallo essentials tabblad ziet u Hallo status van Hallo upgrade als deze de upgradedomeinen van het cluster Hallo doorlopen.</span><span class="sxs-lookup"><span data-stu-id="aece6-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Voortgang van de upgrade in Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="aece6-178">Zoals Hallo upgrade in elk domein verloopt, zijn statuscontroles uitgevoerd tooensure die toepassing hello is correct werkt.</span><span class="sxs-lookup"><span data-stu-id="aece6-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="aece6-179">Als u opnieuw Hallo eerder doorzoeken op Hallo set van services in Hallo fabric: / WordCount-toepassing u ziet dat Hallo WordCountService versie gewijzigd maar Hallo versie van WordCountWebService niet:</span><span class="sxs-lookup"><span data-stu-id="aece6-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Query’s uitvoeren op toepassingsservices na de upgrade][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="aece6-181">In dit voorbeeld wordt uitgelegd hoe toepassingsupgrades worden beheerd met Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="aece6-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="aece6-182">Het raakt enige Hallo set services (of code/configuratiepakketten in die services) die zijn gewijzigd, waardoor Hallo upgradeproces sneller en betrouwbaarder.</span><span class="sxs-lookup"><span data-stu-id="aece6-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="aece6-183">Ten slotte terug toohello browser tooobserve Hallo gedrag van de nieuwe toepassingsversie Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="aece6-184">Zoals verwacht, de voortgang van het aantal langzamer Hallo en de eerste partitie Hallo eindigt iets meer volume Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Weergave Hallo nieuwe versie van Hallo-toepassing in de browser Hallo][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="aece6-186">Opschonen</span><span class="sxs-lookup"><span data-stu-id="aece6-186">Cleaning up</span></span>
<span data-ttu-id="aece6-187">Voordat u afsluit, is het belangrijk tooremember die lokale cluster Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="aece6-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="aece6-188">Toepassingen blijven toorun op Hallo achtergrond totdat u deze verwijdert.</span><span class="sxs-lookup"><span data-stu-id="aece6-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="aece6-189">Afhankelijk van de aard van de Hallo van uw apps, kan een actieve app duren behoorlijk aanspraak op uw computer.</span><span class="sxs-lookup"><span data-stu-id="aece6-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="aece6-190">U hebt verschillende opties toomanage toepassingen en Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="aece6-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="aece6-191">tooremove een afzonderlijke toepassing en alle gegevens, voert u Hallo opdracht na de:</span><span class="sxs-lookup"><span data-stu-id="aece6-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="aece6-192">Of verwijder de toepassing hello van Hallo Service Fabric Explorer **acties** menu of Hallo contextmenu in de lijstweergave van Hallo links toepassing.</span><span class="sxs-lookup"><span data-stu-id="aece6-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Een toepassing verwijderen in Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="aece6-194">Na het verwijderen van de toepassing hello uit Hallo cluster, de registratie versies 1.0.0 en 2.0.0 Hallo type WordCount-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aece6-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="aece6-195">Verwijdering verwijdert Hallo toepassingspakketten, met inbegrip van Hallo code en configuratie van het archief van de installatiekopie van het cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="aece6-196">Of Kies in de Service Fabric Explorer **Type verwijderen** voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aece6-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="aece6-197">tooshut Hallo-cluster, maar houd Hallo toepassingsgegevens en traceringen, klikt u op **lokaal Cluster stoppen** in het systeemvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="aece6-198">toodelete hello cluster volledig, klikt u op **lokaal Cluster verwijderen** in het systeemvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="aece6-199">Deze optie leidt tot een andere implementatie mogelijk langzamer Hallo op de volgende keer dat u op F5 in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aece6-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="aece6-200">Hallo lokale cluster alleen verwijderen als u niet van plan toouse bent het enige tijd of als u tooreclaim bronnen nodig.</span><span class="sxs-lookup"><span data-stu-id="aece6-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="aece6-201">Clustermodus voor één en voor vijf knooppunten</span><span class="sxs-lookup"><span data-stu-id="aece6-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="aece6-202">Wanneer u toepassingen ontwikkelt, moet u vaak snel dezelfde bewerkingen uitvoeren, zoals code schrijven, fouten opsporen, code wijzigen en fouten opsporen.</span><span class="sxs-lookup"><span data-stu-id="aece6-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="aece6-203">toohelp optimaliseren dit proces, het lokale cluster Hallo kunt uitvoeren in twee modi: één knooppunt of vijf knooppunten.</span><span class="sxs-lookup"><span data-stu-id="aece6-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="aece6-204">Beide clustermodi hebben hun eigen voordelen.</span><span class="sxs-lookup"><span data-stu-id="aece6-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="aece6-205">Cluster met vijf knooppunten modus kunt u toowork met een echte cluster.</span><span class="sxs-lookup"><span data-stu-id="aece6-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="aece6-206">U kunt failover-scenario's testen en werken met meerdere exemplaren en replica's van uw services.</span><span class="sxs-lookup"><span data-stu-id="aece6-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="aece6-207">Cluster met één knooppunt modus is geoptimaliseerd toodo snelle implementatie en de registratie van services, toohelp u snel code met Service Fabric-runtime Hallo valideren.</span><span class="sxs-lookup"><span data-stu-id="aece6-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="aece6-208">Een clustermodus met één knooppunt en een clustermodus met vijf knooppunten kunnen beide niet worden gebruikt als een emulator of simulator.</span><span class="sxs-lookup"><span data-stu-id="aece6-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="aece6-209">Hallo lokaal ontwikkelcluster voert dezelfde platformcode is gevonden op meerdere machines clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="aece6-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="aece6-210">Wanneer u Hallo clustermodus wijzigen, Hallo huidig cluster wordt verwijderd uit het systeem en een nieuw cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aece6-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="aece6-211">Hallo-gegevens die zijn opgeslagen in het Hallo-cluster wordt verwijderd wanneer u clustermodus wijzigen.</span><span class="sxs-lookup"><span data-stu-id="aece6-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="aece6-212">toochange hello modus tooone-node cluster, selecteer **Switch clustermodus** in Hallo Service Fabric Local Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="aece6-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![De clustermodus wijzigen][switch-cluster-mode]

<span data-ttu-id="aece6-214">Of modus wijzigen Hallo cluster met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="aece6-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="aece6-215">Start een nieuw PowerShell-venster als beheerder.</span><span class="sxs-lookup"><span data-stu-id="aece6-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="aece6-216">Voer Hallo cluster setup-script uit Hallo SDK-map:</span><span class="sxs-lookup"><span data-stu-id="aece6-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="aece6-217">Het installeren van een cluster duurt even.</span><span class="sxs-lookup"><span data-stu-id="aece6-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="aece6-218">Nadat Setup is voltooid, ziet u soortgelijke uitvoer als deze:</span><span class="sxs-lookup"><span data-stu-id="aece6-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Cluster-installatieuitvoer][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="aece6-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aece6-220">Next steps</span></span>
* <span data-ttu-id="aece6-221">Nu u een aantal vooraf gemaakt toepassen hebt geïmplementeerd een upgrade hebt uitgevoerd, kunt u [proberen zelf toepassingen te ontwikkelen in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="aece6-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="aece6-222">Alle Hallo acties die worden uitgevoerd op de lokale cluster Hallo in dit artikel kunnen worden uitgevoerd op een [Azure cluster](service-fabric-cluster-creation-via-portal.md) ook.</span><span class="sxs-lookup"><span data-stu-id="aece6-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="aece6-223">Hallo-upgrade die is uitgevoerd in dit artikel is basic.</span><span class="sxs-lookup"><span data-stu-id="aece6-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="aece6-224">Zie Hallo [upgradedocumentatie](service-fabric-application-upgrade.md) toolearn meer over Hallo kracht en flexibiliteit van Service Fabric-upgrades.</span><span class="sxs-lookup"><span data-stu-id="aece6-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
