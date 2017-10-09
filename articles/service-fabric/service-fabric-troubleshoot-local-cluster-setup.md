---
title: aaaTroubleshoot uw lokale installatie van de Service Fabric-cluster | Microsoft Docs
description: In dit artikel wordt een reeks suggesties voor het oplossen van uw lokaal ontwikkelcluster behandeld.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Installatie van uw lokale ontwikkeling oplossen
Wanneer u een probleem tijdens interactie met uw lokale cluster van de Azure Service Fabric-ontwikkeling, controleert u Hallo suggesties voor mogelijke oplossingen te volgen.

## <a name="cluster-setup-failures"></a>Setup van clusters
### <a name="cannot-clean-up-service-fabric-logs"></a>Kan niet opschonen van Service Fabric-Logboeken
#### <a name="problem"></a>Probleem
Tijdens het Hallo DevClusterSetup script uitvoeren, ziet u een fout als volgt:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Oplossing
Sluit Hallo huidige PowerShell-venster en opent u een nieuwe PowerShell-venster als beheerder. Nu moet u kunnen toosuccessfully Hallo-script uitvoeren.

## <a name="cluster-connection-failures"></a>Verbindingsfouten cluster
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Service Fabric PowerShell-cmdlets worden niet herkend in Azure PowerShell
#### <a name="problem"></a>Probleem
Als u toorun Hallo Service Fabric PowerShell-cmdlets, zoals gaat `Connect-ServiceFabricCluster` in een Azure PowerShell-venster het mislukt, vermeld die Hallo-cmdlet wordt niet herkend. Hallo reden hiervoor is dat gebruikmaakt van Azure PowerShell Hallo 32-bits versie van Windows PowerShell (zelfs op 64-bits OS-versies), terwijl Hallo Service Fabric-cmdlets alleen werken in 64-bits-omgevingen.

#### <a name="solution"></a>Oplossing
Service Fabric-cmdlets worden altijd uitgevoerd rechtstreeks vanuit Windows PowerShell.

> [!NOTE]
> meest recente versie van Azure PowerShell Hallo maakt geen een speciale snelkoppeling zodat dit niet langer moet gebeuren.
> 
> 

### <a name="type-initialization-exception"></a>Type initialisatie van de uitzondering
#### <a name="problem"></a>Probleem
Wanneer u verbinding toohello cluster in PowerShell maakt, ziet u fout Hallo TypeInitializationException voor System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Oplossing
De variabele path is niet correct ingesteld tijdens de installatie. Afmelden bij Windows en meld u opnieuw aan. Dit vernieuwt pad naar uw.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Cluster-verbinding is mislukt met '-Object is gesloten'
#### <a name="problem"></a>Probleem
Een aanroep van tooConnect-ServiceFabricCluster mislukt met een fout als volgt:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Oplossing
Sluit Hallo huidige PowerShell-venster en opent u een nieuwe PowerShell-venster als beheerder. Nu moet u kunnen toosuccessfully verbinding maken.

### <a name="fabric-connection-denied-exception"></a>Verbinding geweigerd fabric-uitzondering
#### <a name="problem"></a>Probleem
Als u foutopsporing van Visual Studio, krijgt u een FabricConnectionDeniedException-fout.

#### <a name="solution"></a>Oplossing
Deze fout treedt meestal op wanneer u toostart een hostproces van de service handmatig, probeert in plaats van Hallo Service Fabric-runtime toostart zodat het voor u.

Zorg ervoor dat er geen serviceprojecten die zijn ingesteld als opstartprojecten in uw oplossing. Alleen de projecten van Service Fabric-toepassing moeten worden ingesteld als opstartprojecten.

> [!TIP]
> Als na de installatie, uw lokale cluster toobehave abnormaal begint, kunt u het opnieuw met behulp van Hallo lokale cluster manager system lade-toepassing instellen. Hiermee verwijdert u Hallo bestaand cluster en een nieuw wachtwoord instellen. Houd er rekening mee dat alle toepassingen geïmplementeerde en bijbehorende gegevens worden verwijderd.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Begrijpen en oplossen van het cluster met systeemstatusrapporten](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Een cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

