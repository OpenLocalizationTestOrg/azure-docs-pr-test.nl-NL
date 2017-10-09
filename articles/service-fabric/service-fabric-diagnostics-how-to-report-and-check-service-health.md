---
title: aaaReport en controleer health met Azure Service Fabric | Microsoft Docs
description: Informatie over hoe toosend systeemstatusrapporten vanuit uw servicecode en hoe toocheck Hallo status van uw service met behulp van Hallo voor health monitoring hulpprogramma's die Azure Service Fabric biedt.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Servicestatus rapporteren en controleren
Wanneer uw services problemen ondervindt, afhankelijk de mogelijkheid toorespond tooand fix incidenten en storingen van uw mogelijkheid toodetect Hallo problemen snel. Als u problemen en fouten toohello Azure Service Fabric health manager vanuit uw servicecode rapporteert, kunt u standaard voor health monitoring dat Service Fabric toocheck Hallo gezondheidsstatus biedt hulpprogramma's gebruiken.

Er zijn drie manieren dat u de status van de service Hallo kunt melden:

* Gebruik [partitie](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) of [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objecten.  
  U kunt Hallo `Partition` en `CodePackageActivationContext` tooreport Hallo status van de elementen die deel van de huidige context Hallo uitmaken-objecten. Code die wordt uitgevoerd als onderdeel van een replica kan bijvoorbeeld health rapporteren alleen op die replica, Hallo partitie die hoort bij en Hallo-toepassing die deel van uitmaakt.
* Gebruik `FabricClient`.   
  U kunt `FabricClient` tooreport de status van Hallo servicecode als Hallo-cluster niet is [beveiligde](service-fabric-cluster-security.md) of als het Hallo-service wordt uitgevoerd met beheerdersbevoegdheden. De meeste real-world scenario's geen niet-beveiligde clusters gebruiken of bieden beheerdersbevoegdheden. Met `FabricClient`, u kunt een entiteit die deel uitmaakt van de cluster Hallo health rapporteren. In het ideale geval echter moet servicecode alleen rapporten verzenden die eigen health gerelateerde tooits zijn.
* Hallo REST-API's gebruiken op Hallo cluster, toepassing, geïmplementeerde toepassing, service, servicepakket, partitie, replica of knooppunt niveaus. Dit kan de status van gebruikte tooreport binnen een container zijn.

Dit artikel begeleidt u bij een voorbeeld waarin de status van de servicecode Hallo-rapporten. Hallo-voorbeeld ziet u ook hoe Hallo-hulpprogramma's van Service Fabric gebruikte toocheck Hallo gezondheidsstatus kunnen zijn. In dit artikel is bedoeld toobe een korte inleiding toohello controlefuncties van Service Fabric. U kunt Hallo reeks diepgaande artikelen over status die met Hallo koppeling aan Hallo einde van dit artikel beginnen lezen voor meer gedetailleerde informatie.

## <a name="prerequisites"></a>Vereisten
Hallo volgende zijn geïnstalleerd, moet u hebben:

* Visual Studio 2015 of Visual Studio 2017
* Service Fabric SDK

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate een lokale veilige dev-cluster
* Open PowerShell met beheerdersbevoegdheden en Hallo volgende opdrachten uitvoeren:

![Opdrachten die tonen hoe toocreate een beveiligde dev-cluster](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy een toepassing en controleer de status
1. Open Visual Studio als beheerder.
2. Een project maken met behulp van Hallo **Stateful Service** sjabloon.
   
    ![Maken van een Service Fabric-toepassing met Stateful Service](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Druk op **F5** toorun Hallo toepassing in de foutopsporingsmodus. Hallo-toepassing is geïmplementeerd toohello lokale cluster.
4. Nadat het Hallo-toepassing wordt uitgevoerd, met de rechtermuisknop op Hallo lokaal Clusterbeheer pictogram in systeemvak Hallo en selecteert u **lokaal Cluster beheren** van Hallo snelkoppeling menu tooopen Service Fabric Explorer.
   
    ![Service Fabric Explorer openen vanuit het systeemvak](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. de toepassingsstatus Hallo moet worden weergegeven zoals in deze afbeelding. Op dit moment moet Hallo toepassing zonder fouten in orde.
   
    ![In orde toepassing in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. U kunt ook Hallo health controleren met behulp van PowerShell. U kunt ```Get-ServiceFabricApplicationHealth``` toocheck status van een toepassing en u kunt gebruiken ```Get-ServiceFabricServiceHealth``` toocheck status van een service. Hallo statusrapport voor Hallo dezelfde toepassing in PowerShell in deze afbeelding is.
   
    ![In orde toepassing in PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>tooadd aangepaste health gebeurtenissen tooyour servicecode
Hallo Service Fabric-projectsjablonen in Visual Studio bevatten voorbeeldcode. Hallo volgende stappen laten zien hoe u aangepaste health gebeurtenissen vanuit uw servicecode kan rapporteren. Deze rapporten weergegeven automatisch in Hallo standaardprogramma's voor health monitoring biedt Service Fabric, zoals Service Fabric Explorer, Azure portal health weergeven en PowerShell.

1. Hallo-toepassing die u eerder hebt gemaakt in Visual Studio opnieuw of maak een nieuwe toepassing met behulp van Hallo **Stateful Service** Visual Studio-sjabloon.
2. Hallo Stateful1.cs bestand openen en Hallo zoeken `myDictionary.TryGetValueAsync` -aanroep in Hallo `RunAsync` methode. U ziet dat deze methode retourneert een `result` dat blokkeringen huidige waarde van de teller Hallo Hallo omdat sleutel logica in deze toepassing hello tookeep een aantal die wordt uitgevoerd. Als dit een echte toepassing zijn, en als Hallo gebrek aan resultaat een fout weergegeven, kunt u tooflag die gebeurtenis.
3. een statusgebeurtenis wanneer Hallo gebrek aan resultaat duidt op een fout tooreport toevoegen Hallo stappen te volgen.
   
    a. Hallo toevoegen `System.Fabric.Health` naamruimte toohello Stateful1.cs bestand.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Hallo code volgen na Hallo toevoegen `myDictionary.TryGetValueAsync` aanroepen
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    We gerapporteerd replica health omdat deze wordt gerapporteerd van een stateful service. Hallo `HealthInformation` parameter wordt informatie opgeslagen over Hallo probleem met de status wordt gerapporteerd.
   
    Als u een stateless service hebt gemaakt, Hallo volgende code gebruiken
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Als uw service wordt uitgevoerd met beheerdersbevoegdheden, of als Hallo-cluster niet is [beveiligde](service-fabric-cluster-security.md), u kunt ook `FabricClient` tooreport health zoals weergegeven in Hallo stappen te volgen.  
   
    a. Hallo maken `FabricClient` exemplaar na Hallo `var myDictionary` declaratie.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Hallo code volgen na Hallo toevoegen `myDictionary.TryGetValueAsync` aanroepen.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. We deze fout te simuleren en wordt weergegeven in Hallo health controleprogramma's weergegeven. toosimulate hello is mislukt, commentaar Hallo eerste regel in Hallo health reporting code die u eerder hebt toegevoegd. Nadat u de eerste regel Hallo uitcommentariëren, eruit Hallo code Hallo voorbeeld te volgen.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Deze code wordt geactiveerd Hallo statusrapport telkens `RunAsync` wordt uitgevoerd. Nadat u Hallo wijzigen, drukt u op **F5** toorun Hallo-toepassing.
6. Nadat het Hallo-toepassing wordt uitgevoerd, opent u Service Fabric Explorer toocheck Hallo status van Hallo-toepassing. Deze tijd toont Service Fabric Explorer toepassing hello is beschadigd. Dit is vanwege Hallo-fout die is gerapporteerd door Hallo code dat we eerder toegevoegd.
   
    ![Slecht toepassingstype in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Als u de primaire replica Hallo in de structuurweergave Hallo van Service Fabric Explorer selecteert, ziet u dat **status** te duidt op een fout. Service Fabric Explorer geeft ook Hallo statusrapport details die waren toegevoegd toohello `HealthInformation` parameter in Hallo-code. U kunt zien Hallo dezelfde statusrapporten in PowerShell en hello Azure-portal.
   
    ![Status van de replica in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Dit rapport blijft in Hallo health manager totdat deze is vervangen door een ander rapport of totdat deze replica wordt verwijderd. Omdat we niet hebt ingesteld `TimeToLive` voor dit rapport health in Hallo `HealthInformation` object Hallo rapport verloopt nooit.

Het is raadzaam dat status op Hallo meest gedetailleerd niveau, dat in dit geval Hallo replica moet worden gerapporteerd. U kunt ook rapporteren health `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

status voor tooreport `Application`, `DeployedApplication`, en `DeployedServicePackage`, gebruik `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Volgende stappen
* [Deep dive op Service Fabric-status](service-fabric-health-introduction.md)
* [REST-API voor de status van de service reporting](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [REST-API voor het melden van toepassingsstatus](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

