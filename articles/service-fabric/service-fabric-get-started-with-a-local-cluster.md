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
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Aan de slag met het implementeren en bijwerken van toepassingen op uw lokale cluster
Hello Azure Service Fabric SDK bevat een volledig lokale ontwikkelingsomgeving waarmee u kunt tooquickly aan de slag met het implementeren en beheren van toepassingen op een lokaal cluster. In dit artikel wordt een lokaal cluster maken, een bestaande toepassing tooit implementeren en vervolgens een upgrade die nieuwe versie tooa van de toepassing, vanuit Windows PowerShell.

> [!NOTE]
> In dit artikel wordt ervan uitgegaan dat u [uw ontwikkelingsomgeving](service-fabric-get-started.md) al hebt ingesteld.
> 
> 

## <a name="create-a-local-cluster"></a>Een lokaal cluster maken
Een Service Fabric-cluster vertegenwoordigt een aantal hardwareresources waarvoor u toepassingen kunt implementeren. Normaal gesproken een cluster bestaat uit een willekeurige plaats van vijf toomany duizenden computers. Hallo Service Fabric SDK bevat echter een clusterconfiguratie die kan worden uitgevoerd op een enkele computer.

Het is belangrijk toounderstand die Hallo lokale Service Fabric-cluster is niet een emulator of simulator. Deze wordt uitgevoerd Hallo dezelfde platformcode is gevonden in clusters met meerdere machines. Hallo enige verschil is dat deze Hallo platform processen die doorgaans worden verdeeld over vijf machines op één computer wordt uitgevoerd.

Hallo SDK biedt twee manieren tooset van een lokaal cluster: een Windows PowerShell-script en Hallo lokaal Clusterbeheer systeemvak van de app. In deze zelfstudie gebruiken we Hallo PowerShell-script.

> [!NOTE]
> Als u al een lokaal cluster hebt gemaakt door een toepassing te implementeren vanuit Visual Studio hebt gemaakt, kunt u dit gedeelte overslaan.
> 
> 

1. Start een nieuw PowerShell-venster als beheerder.
2. Voer Hallo cluster setup-script uit Hallo SDK-map:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    Het installeren van een cluster duurt even. Nadat Setup is voltooid, ziet u soortgelijke uitvoer als deze:
   
    ![Cluster-installatieuitvoer][cluster-setup-success]
   
    U bent nu klaar tootry een toepassing tooyour-cluster implementeren.

## <a name="deploy-an-application"></a>Een app implementeren
Hallo Service Fabric SDK bevat een uitgebreide reeks frameworks en ontwikkelaarstools voor het maken van toepassingen. Als u geïnteresseerd bent in leren hoe toocreate toepassingen in Visual Studio, Zie [uw eerste Service Fabric-toepassing maken in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

In deze zelfstudie maakt u een bestaande voorbeeldtoepassing (WordCount genoemd) zodat u zich op Hallo management aspecten van Hallo-platform richten kunt: implementatie, bewaking en upgrade.

1. Start een nieuw PowerShell-venster als beheerder.
2. Hallo Service Fabric SDK PowerShell-module importeren.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Maak een map toostore Hallo-toepassing die u downloadt en implementeert, bijvoorbeeld C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Download het WordCount-toepassing hello](http://aka.ms/servicefabric-wordcountapp) toohello locatie die u hebt gemaakt.  Opmerking: Hallo Microsoft Edge-browser slaat Hallo-bestand met een *.zip* extensie.  Hallo-bestandsextensie ook wijzigen*.sfpkg*.
5. Verbinding maken met het lokale cluster toohello:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Maak een nieuwe toepassing hello SDK implementatieopdracht met een naam en een pad toohello-toepassingspakket.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Als alles goed gaat, ziet u Hallo volgende uitvoer:
   
    ![Een toepassing toohello lokale cluster implementeren][deploy-app-to-local-cluster]
7. toosee hello toepassing in actie, Hallo browser starten en te navigeren[http://localhost: 8081/WordCount/index.HTML](http://localhost:8081/wordcount/index.html). U ziet het volgende:
   
    ![De UI van de geïmplementeerde toepassing][deployed-app-ui]
   
    Hallo WordCount-toepassing is eenvoudig. Het omvat client-side JavaScript-code toogenerate willekeurige vijf tekens 'woorden', die vervolgens doorgegeven toohello toepassing via ASP.NET Web API. Een stateful service houdt het aantal woorden geteld Hallo. Ze worden gepartitioneerd op basis van het eerste teken van de Hallo van Hallo woord. U vindt de broncode Hallo Hallo WordCount App in Hallo [klassieke introductie voorbeelden](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    Hallo-toepassing die we hebben geïmplementeerd bevat vier partities. Zodat woorden die beginnen met A tot G worden opgeslagen in de eerste partitie hello, worden woorden die beginnen met H tot N worden opgeslagen in de tweede partitie hello, enzovoort.

## <a name="view-application-details-and-status"></a>Details en de status van de toepassing weergeven
Nu dat we Hallo toepassing hebt geïmplementeerd, bekijken we enkele van de gegevens van de app Hallo in PowerShell.

1. Query alle geïmplementeerde toepassingen op Hallo-cluster:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Ervan uitgaande dat u alleen Hallo WordCount app hebt geïmplementeerd, ziet u iets soortgelijks als:
   
    ![Een query uitvoeren op alle geïmplementeerde toepassingen in PowerShell;][ps-getsfapp]
2. Ga toohello volgende niveau door het uitvoeren van query's Hallo set services die zijn opgenomen in de toepassing WordCount Hallo.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lijst met services voor de toepassing hello in PowerShell][ps-getsfsvc]
   
    Hallo toepassing bestaat uit twee services, Hallo webfront-end en Hallo stateful service die Hallo woorden beheert.
3. Tot slot bekijkt hello lijst met partities voor WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Hallo servicepartities in PowerShell weergeven][ps-getsfpartitions]
   
    Hallo reeks opdrachten die u, zoals alle Service Fabric PowerShell-opdrachten gebruikt, zijn beschikbaar voor een cluster die u mogelijk verbinding met lokale of externe.
   
    Voor een meer visuele manier toointeract met Hallo-cluster, kunt u Hallo Service Fabric Explorer Webhulpprogramma door te navigeren[http://localhost: 19080/Explorer](http://localhost:19080/Explorer) in Hallo browser.
   
    ![Toepassingdetails weergeven in Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > Zie toolearn meer informatie over Service Fabric Explorer [uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Een upgrade van een app uitvoeren
Service Fabric bevat upgrades zonder downtime door de bewaking van Hallo status van de toepassing hello zoals implementatie in Hallo-cluster. Een upgrade uitvoeren van Hallo WordCount-toepassing.

Hallo nieuwe versie van de toepassing hello nu telt alleen woorden die met een klinkerteken beginnen. Als de upgrade Hallo implementeert, ziet u twee zichtbare wijzigingen in gedrag van de toepassing hello. Eerst vertragen Hallo snelheid waarmee Hallo aantal groeit, omdat er minder woorden worden geteld. Tweede, aangezien de eerste partitie Hallo twee klinkers (A en E heeft) en alle andere partities slechts één bevatten, het aantal moet uiteindelijk eerst toooutpace Hallo anderen.

1. [Hallo WordCount versie 2 van het pakket downloaden](http://aka.ms/servicefabric-wordcountappv2) toohello dezelfde locatie waar u Hallo versie 1 pakket hebt gedownload.
2. Retourneren tooyour PowerShell-venster en gebruik van de SDK Hallo upgrade opdracht tooregister nieuwe versie in de cluster Hallo Hallo. Vervolgens begint met het upgraden van Hallo fabric: / WordCount-toepassing.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    U ziet Hallo volgende uitvoer in PowerShell als Hallo upgrade begint.
   
    ![Voortgang van de upgrade in PowerShell][ps-appupgradeprogress]
3. Tijdens het Hallo-upgrade wordt voortgezet, soms is het eenvoudiger toomonitor de status van Service Fabric Explorer. Open een browservenster en navigeer te[http://localhost: 19080/Explorer](http://localhost:19080/Explorer). Vouw **toepassingen** Kies in de boomstructuur Hallo op Hallo links van **WordCount**, en tot slot **fabric: / WordCount**. Hallo essentials tabblad ziet u Hallo status van Hallo upgrade als deze de upgradedomeinen van het cluster Hallo doorlopen.
   
    ![Voortgang van de upgrade in Service Fabric Explorer][sfx-upgradeprogress]
   
    Zoals Hallo upgrade in elk domein verloopt, zijn statuscontroles uitgevoerd tooensure die toepassing hello is correct werkt.
4. Als u opnieuw Hallo eerder doorzoeken op Hallo set van services in Hallo fabric: / WordCount-toepassing u ziet dat Hallo WordCountService versie gewijzigd maar Hallo versie van WordCountWebService niet:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Query’s uitvoeren op toepassingsservices na de upgrade][ps-getsfsvc-postupgrade]
   
    In dit voorbeeld wordt uitgelegd hoe toepassingsupgrades worden beheerd met Service Fabric. Het raakt enige Hallo set services (of code/configuratiepakketten in die services) die zijn gewijzigd, waardoor Hallo upgradeproces sneller en betrouwbaarder.
5. Ten slotte terug toohello browser tooobserve Hallo gedrag van de nieuwe toepassingsversie Hallo. Zoals verwacht, de voortgang van het aantal langzamer Hallo en de eerste partitie Hallo eindigt iets meer volume Hallo.
   
    ![Weergave Hallo nieuwe versie van Hallo-toepassing in de browser Hallo][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Opschonen
Voordat u afsluit, is het belangrijk tooremember die lokale cluster Hallo echte. Toepassingen blijven toorun op Hallo achtergrond totdat u deze verwijdert.  Afhankelijk van de aard van de Hallo van uw apps, kan een actieve app duren behoorlijk aanspraak op uw computer. U hebt verschillende opties toomanage toepassingen en Hallo-cluster:

1. tooremove een afzonderlijke toepassing en alle gegevens, voert u Hallo opdracht na de:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Of verwijder de toepassing hello van Hallo Service Fabric Explorer **acties** menu of Hallo contextmenu in de lijstweergave van Hallo links toepassing.
   
    ![Een toepassing verwijderen in Service Fabric Explorer][sfe-delete-application]
2. Na het verwijderen van de toepassing hello uit Hallo cluster, de registratie versies 1.0.0 en 2.0.0 Hallo type WordCount-toepassing. Verwijdering verwijdert Hallo toepassingspakketten, met inbegrip van Hallo code en configuratie van het archief van de installatiekopie van het cluster Hallo.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Of Kies in de Service Fabric Explorer **Type verwijderen** voor Hallo-toepassing.
3. tooshut Hallo-cluster, maar houd Hallo toepassingsgegevens en traceringen, klikt u op **lokaal Cluster stoppen** in het systeemvak Hallo.
4. toodelete hello cluster volledig, klikt u op **lokaal Cluster verwijderen** in het systeemvak Hallo. Deze optie leidt tot een andere implementatie mogelijk langzamer Hallo op de volgende keer dat u op F5 in Visual Studio. Hallo lokale cluster alleen verwijderen als u niet van plan toouse bent het enige tijd of als u tooreclaim bronnen nodig.

## <a name="one-node-and-five-node-cluster-mode"></a>Clustermodus voor één en voor vijf knooppunten
Wanneer u toepassingen ontwikkelt, moet u vaak snel dezelfde bewerkingen uitvoeren, zoals code schrijven, fouten opsporen, code wijzigen en fouten opsporen. toohelp optimaliseren dit proces, het lokale cluster Hallo kunt uitvoeren in twee modi: één knooppunt of vijf knooppunten. Beide clustermodi hebben hun eigen voordelen. Cluster met vijf knooppunten modus kunt u toowork met een echte cluster. U kunt failover-scenario's testen en werken met meerdere exemplaren en replica's van uw services. Cluster met één knooppunt modus is geoptimaliseerd toodo snelle implementatie en de registratie van services, toohelp u snel code met Service Fabric-runtime Hallo valideren.

Een clustermodus met één knooppunt en een clustermodus met vijf knooppunten kunnen beide niet worden gebruikt als een emulator of simulator. Hallo lokaal ontwikkelcluster voert dezelfde platformcode is gevonden op meerdere machines clusters Hallo.

> [!WARNING]
> Wanneer u Hallo clustermodus wijzigen, Hallo huidig cluster wordt verwijderd uit het systeem en een nieuw cluster is gemaakt. Hallo-gegevens die zijn opgeslagen in het Hallo-cluster wordt verwijderd wanneer u clustermodus wijzigen.
> 
> 

toochange hello modus tooone-node cluster, selecteer **Switch clustermodus** in Hallo Service Fabric Local Cluster Manager.

![De clustermodus wijzigen][switch-cluster-mode]

Of modus wijzigen Hallo cluster met behulp van PowerShell:

1. Start een nieuw PowerShell-venster als beheerder.
2. Voer Hallo cluster setup-script uit Hallo SDK-map:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    Het installeren van een cluster duurt even. Nadat Setup is voltooid, ziet u soortgelijke uitvoer als deze:
   
    ![Cluster-installatieuitvoer][cluster-setup-success-1-node]

## <a name="next-steps"></a>Volgende stappen
* Nu u een aantal vooraf gemaakt toepassen hebt geïmplementeerd een upgrade hebt uitgevoerd, kunt u [proberen zelf toepassingen te ontwikkelen in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Alle Hallo acties die worden uitgevoerd op de lokale cluster Hallo in dit artikel kunnen worden uitgevoerd op een [Azure cluster](service-fabric-cluster-creation-via-portal.md) ook.
* Hallo-upgrade die is uitgevoerd in dit artikel is basic. Zie Hallo [upgradedocumentatie](service-fabric-application-upgrade.md) toolearn meer over Hallo kracht en flexibiliteit van Service Fabric-upgrades.

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
