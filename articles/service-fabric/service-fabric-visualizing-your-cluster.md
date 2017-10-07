---
title: aaaVisualizing uw cluster met behulp van Service Fabric Explorer | Microsoft Docs
description: Service Fabric Explorer is een Webhulpprogramma voor te bekijken en beheren van cloudtoepassingen en -knooppunten in een Microsoft Azure Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Visualisern van uw cluster met Service Fabric Explorer
Service Fabric Explorer is een Webhulpprogramma voor te bekijken en beheren van toepassingen en de knooppunten in een Azure Service Fabric-cluster. Service Fabric Explorer wordt gehost rechtstreeks in het Hallo-cluster, zodat deze altijd beschikbaar is, ongeacht waar uw cluster wordt uitgevoerd.

## <a name="video-tutorial"></a>Zelfstudievideo

toolearn hoe toouse Service Fabric Explorer bekijkt hello Microsoft Virtual Academy video te volgen:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Verbinding maken met tooService Fabric Explorer
Als u te Hallo instructies hebt gevolgd[uw ontwikkelingsomgeving voorbereiden](service-fabric-get-started.md), kunt u de Service Fabric Explorer starten op uw lokale cluster door te navigeren toohttp://localhost:19080 / Explorer.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Hallo Service Fabric Explorer indeling begrijpen
U kunt via Service Fabric Explorer navigeren met behulp van Hallo structuur op Hallo links. In de hoofdmap van de Hallo van Hallo structuur overzicht Hallo cluster-dashboard van uw cluster, inclusief een overzicht van de toepassing en het knooppunt status.

![Service Fabric Explorer cluster-dashboard][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Indeling van het cluster Hallo weergeven
Knooppunten in een Service Fabric-cluster worden geplaatst in een tweedimensionale raster van domeinen met fouten en upgradedomeinen. Deze plaatsing zorgt ervoor dat uw toepassingen beschikbaar in Hallo aanwezigheid van hardwarefouten en toepassingsupgrades blijven. U kunt bekijken hoe Hallo huidig cluster met behulp van de clustertoewijzing Hallo worden verspreid.

![Service Fabric Explorer clustertoewijzing][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Weergave-toepassingen en services
Hallo-cluster bevat twee substructuren: één voor toepassingen en andere voor knooppunten.

U kunt Hallo toepassing weergave toonavigate via Service Fabric van logische hiërarchie: toepassingen, services, partities en replica's.

In onderstaande Hallo voorbeeld, Hallo toepassing **MyApp** bestaat uit twee services **MyStatefulService** en **WebService**. Aangezien **MyStatefulService** stateful is, bevat een partitie met een primaire en twee secundaire replica's. Daarentegen is WebSvcService staatloze en slechts één exemplaar bevat.

![Service Fabric Explorer toepassing weergeven][sfx-application-tree]

Op elk niveau van Hallo-structuur bevat Hallo hoofdvenster relevante informatie over het Hallo-item. Bijvoorbeeld, ziet u Hallo gezondheidsstatus en versie voor een bepaalde service.

![Service Fabric Explorer essentials deelvenster][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Hallo clusterknooppunten weergeven
Hallo knooppunt weergave toont de fysieke indeling Hallo van Hallo-cluster. Voor elk knooppunt kunt u controleren voor welke toepassingen er op het knooppunt code is geïmplementeerd. Meer specifiek, kunt u zien welke replica er momenteel worden uitgevoerd.

## <a name="actions"></a>Acties
Service Fabric Explorer biedt een snelle manier tooinvoke acties op de knooppunten, toepassingen en services in uw cluster.

Bijvoorbeeld: toodelete instantie van een toepassing hello toepassing kiezen uit Hallo structuur aan de linkerkant Hallo en kies vervolgens **acties** > **toepassing verwijderen**.

![Verwijderen van een toepassing in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> U kunt uitvoeren Hallo dezelfde acties door te klikken op Hallo weglatingsteken volgende tooeach element.
>
>

Hallo bevat volgende tabel Hallo acties die beschikbaar zijn voor elke entiteit:

| **Entiteit** | **Actie** | **Beschrijving** |
| --- | --- | --- |
| Toepassingstype |Type inrichting |Hallo-toepassingspakket verwijdert uit de installatiekopieopslag Hallo-cluster. Vereist dat alle toepassingen van dat type toobe eerst verwijderd. |
| Toepassing |Toepassing verwijderen |Hallo-toepassing, met inbegrip van alle services en hun status (indien aanwezig) verwijderen. |
| Service |Verwijderen van de Service |Hallo-service en de status verwijderd (indien aanwezig). |
| Knooppunt |Activeren |Hallo knooppunt activeren. |
| Knooppunt | Deactiveren (pause) | Hallo-knooppunt onderbreken met de huidige status. Services toorun doorgaan, maar Service Fabric proactief verplaatst geen alles naar of uit deze tenzij dit vereist tooprevent een storing of inconsistenties in de gegevens. Deze actie is gewoonlijk gebruikte tooenable services op een specifiek knooppunt tooensure dat ze niet tijdens de inspectie verplaatsen foutopsporing. | |
| Knooppunt | (Opnieuw opstarten) deactiveren | Veilig Verplaats alle in het geheugen services een knooppunt uit en sluit permanente services. Normaal gesproken gebruikt bij Hallo hostprocessen of machine nodig toobe opnieuw opgestart. | |
| Knooppunt | Deactiveren (gegevens verwijderen) | Alle services die worden uitgevoerd op Hallo knooppunt na het bouwen van voldoende spare replica's sluiten. Doorgaans gebruikt wanneer een knooppunt (of ten minste bijbehorende opslag) is buiten het Commissie permanent genomen. | |
| Knooppunt | Status van knooppunt verwijderen | Kennis van replica's van een knooppunt uit cluster Hallo verwijderen. Doorgaans gebruikt wanneer een knooppunt al onherstelbare wordt geacht. | |
| Knooppunt | Opnieuw starten | Een knooppuntfout simuleren door Hallo knooppunt opnieuw te starten. Meer informatie [hier](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Aangezien veel acties destructieve, hebt u mogelijk gevraagd u tooconfirm uw bedoeling voordat Hallo actie is voltooid.

> [!TIP]
> Elke actie die kan worden uitgevoerd via Service Fabric Explorer kan ook worden uitgevoerd via PowerShell of REST-API, tooenable automation.
>
>

U kunt ook een Service Fabric Explorer toocreate toepassingsexemplaren gebruiken voor een bepaalde toepassingstype en -versie. Type van de toepassing hello kiezen in de structuurweergave hello, en klik vervolgens op Hallo **app-exemplaar maken** koppeling volgende toohello versie u in het rechterdeelvenster Hallo dat wilt.

![Instantie van een toepassing maken in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> Exemplaren van een toepassing gemaakt via Service Fabric Explorer kunnen niet op dit moment parameters worden gebruikt. Ze zijn gemaakt met behulp van de standaardwaarden voor parameters.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Verbinding maken met de externe Service Fabric-cluster tooa
Als u Hallo clustereindpunt kent en voldoende machtigingen hebt u toegang tot Service Fabric Explorer vanuit elke browser. Dit komt doordat het Service Fabric Explorer is gewoon een service die wordt uitgevoerd in Hallo-cluster.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Hallo Service Fabric Explorer-eindpunt voor een cluster met externe detecteren
tooreach Service Fabric Explorer voor een bepaald cluster punt uw browser:

http://&lt;uw cluster-eindpunt&gt;: 19080/Explorer

Hallo volledige URL is voor Azure-clusters is ook beschikbaar in Hallo cluster essentials deelvenster Hallo Azure-portal.

### <a name="connect-tooa-secure-cluster"></a>Verbinding maken met de beveiligde cluster tooa
U kunt de client toegang tooyour Service Fabric-cluster met certificaten of met behulp van Azure Active Directory (AAD) beheren.

Als u tooconnect tooService Fabric Explorer op een beveiligde cluster probeert, vervolgens afhankelijk van Hallo clusterconfiguratie zult u worden toopresent vereist een clientcertificaat of meld u aan met AAD.

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van testbaarheid](service-fabric-testability-overview.md)
* [Het beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Implementatie van de service Fabric-toepassing met behulp van PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
