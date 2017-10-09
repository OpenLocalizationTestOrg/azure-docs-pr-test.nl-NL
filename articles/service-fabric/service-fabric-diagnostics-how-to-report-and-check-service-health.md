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
# <a name="report-and-check-service-health"></a><span data-ttu-id="96f42-103">Servicestatus rapporteren en controleren</span><span class="sxs-lookup"><span data-stu-id="96f42-103">Report and check service health</span></span>
<span data-ttu-id="96f42-104">Wanneer uw services problemen ondervindt, afhankelijk de mogelijkheid toorespond tooand fix incidenten en storingen van uw mogelijkheid toodetect Hallo problemen snel.</span><span class="sxs-lookup"><span data-stu-id="96f42-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="96f42-105">Als u problemen en fouten toohello Azure Service Fabric health manager vanuit uw servicecode rapporteert, kunt u standaard voor health monitoring dat Service Fabric toocheck Hallo gezondheidsstatus biedt hulpprogramma's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96f42-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="96f42-106">Er zijn drie manieren dat u de status van de service Hallo kunt melden:</span><span class="sxs-lookup"><span data-stu-id="96f42-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="96f42-107">Gebruik [partitie](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) of [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objecten.</span><span class="sxs-lookup"><span data-stu-id="96f42-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="96f42-108">U kunt Hallo `Partition` en `CodePackageActivationContext` tooreport Hallo status van de elementen die deel van de huidige context Hallo uitmaken-objecten.</span><span class="sxs-lookup"><span data-stu-id="96f42-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="96f42-109">Code die wordt uitgevoerd als onderdeel van een replica kan bijvoorbeeld health rapporteren alleen op die replica, Hallo partitie die hoort bij en Hallo-toepassing die deel van uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="96f42-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="96f42-110">Gebruik `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="96f42-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="96f42-111">U kunt `FabricClient` tooreport de status van Hallo servicecode als Hallo-cluster niet is [beveiligde](service-fabric-cluster-security.md) of als het Hallo-service wordt uitgevoerd met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="96f42-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="96f42-112">De meeste real-world scenario's geen niet-beveiligde clusters gebruiken of bieden beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="96f42-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="96f42-113">Met `FabricClient`, u kunt een entiteit die deel uitmaakt van de cluster Hallo health rapporteren.</span><span class="sxs-lookup"><span data-stu-id="96f42-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="96f42-114">In het ideale geval echter moet servicecode alleen rapporten verzenden die eigen health gerelateerde tooits zijn.</span><span class="sxs-lookup"><span data-stu-id="96f42-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="96f42-115">Hallo REST-API's gebruiken op Hallo cluster, toepassing, geïmplementeerde toepassing, service, servicepakket, partitie, replica of knooppunt niveaus.</span><span class="sxs-lookup"><span data-stu-id="96f42-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="96f42-116">Dit kan de status van gebruikte tooreport binnen een container zijn.</span><span class="sxs-lookup"><span data-stu-id="96f42-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="96f42-117">Dit artikel begeleidt u bij een voorbeeld waarin de status van de servicecode Hallo-rapporten.</span><span class="sxs-lookup"><span data-stu-id="96f42-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="96f42-118">Hallo-voorbeeld ziet u ook hoe Hallo-hulpprogramma's van Service Fabric gebruikte toocheck Hallo gezondheidsstatus kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="96f42-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="96f42-119">In dit artikel is bedoeld toobe een korte inleiding toohello controlefuncties van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="96f42-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="96f42-120">U kunt Hallo reeks diepgaande artikelen over status die met Hallo koppeling aan Hallo einde van dit artikel beginnen lezen voor meer gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="96f42-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96f42-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="96f42-121">Prerequisites</span></span>
<span data-ttu-id="96f42-122">Hallo volgende zijn geïnstalleerd, moet u hebben:</span><span class="sxs-lookup"><span data-stu-id="96f42-122">You must have hello following installed:</span></span>

* <span data-ttu-id="96f42-123">Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="96f42-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="96f42-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="96f42-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="96f42-125">toocreate een lokale veilige dev-cluster</span><span class="sxs-lookup"><span data-stu-id="96f42-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="96f42-126">Open PowerShell met beheerdersbevoegdheden en Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="96f42-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Opdrachten die tonen hoe toocreate een beveiligde dev-cluster](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="96f42-128">toodeploy een toepassing en controleer de status</span><span class="sxs-lookup"><span data-stu-id="96f42-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="96f42-129">Open Visual Studio als beheerder.</span><span class="sxs-lookup"><span data-stu-id="96f42-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="96f42-130">Een project maken met behulp van Hallo **Stateful Service** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="96f42-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Maken van een Service Fabric-toepassing met Stateful Service](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="96f42-132">Druk op **F5** toorun Hallo toepassing in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="96f42-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="96f42-133">Hallo-toepassing is geïmplementeerd toohello lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="96f42-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="96f42-134">Nadat het Hallo-toepassing wordt uitgevoerd, met de rechtermuisknop op Hallo lokaal Clusterbeheer pictogram in systeemvak Hallo en selecteert u **lokaal Cluster beheren** van Hallo snelkoppeling menu tooopen Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="96f42-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Service Fabric Explorer openen vanuit het systeemvak](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="96f42-136">de toepassingsstatus Hallo moet worden weergegeven zoals in deze afbeelding.</span><span class="sxs-lookup"><span data-stu-id="96f42-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="96f42-137">Op dit moment moet Hallo toepassing zonder fouten in orde.</span><span class="sxs-lookup"><span data-stu-id="96f42-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![In orde toepassing in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="96f42-139">U kunt ook Hallo health controleren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96f42-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="96f42-140">U kunt ```Get-ServiceFabricApplicationHealth``` toocheck status van een toepassing en u kunt gebruiken ```Get-ServiceFabricServiceHealth``` toocheck status van een service.</span><span class="sxs-lookup"><span data-stu-id="96f42-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="96f42-141">Hallo statusrapport voor Hallo dezelfde toepassing in PowerShell in deze afbeelding is.</span><span class="sxs-lookup"><span data-stu-id="96f42-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![In orde toepassing in PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="96f42-143">tooadd aangepaste health gebeurtenissen tooyour servicecode</span><span class="sxs-lookup"><span data-stu-id="96f42-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="96f42-144">Hallo Service Fabric-projectsjablonen in Visual Studio bevatten voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="96f42-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="96f42-145">Hallo volgende stappen laten zien hoe u aangepaste health gebeurtenissen vanuit uw servicecode kan rapporteren.</span><span class="sxs-lookup"><span data-stu-id="96f42-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="96f42-146">Deze rapporten weergegeven automatisch in Hallo standaardprogramma's voor health monitoring biedt Service Fabric, zoals Service Fabric Explorer, Azure portal health weergeven en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96f42-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="96f42-147">Hallo-toepassing die u eerder hebt gemaakt in Visual Studio opnieuw of maak een nieuwe toepassing met behulp van Hallo **Stateful Service** Visual Studio-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="96f42-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="96f42-148">Hallo Stateful1.cs bestand openen en Hallo zoeken `myDictionary.TryGetValueAsync` -aanroep in Hallo `RunAsync` methode.</span><span class="sxs-lookup"><span data-stu-id="96f42-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="96f42-149">U ziet dat deze methode retourneert een `result` dat blokkeringen huidige waarde van de teller Hallo Hallo omdat sleutel logica in deze toepassing hello tookeep een aantal die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="96f42-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="96f42-150">Als dit een echte toepassing zijn, en als Hallo gebrek aan resultaat een fout weergegeven, kunt u tooflag die gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="96f42-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="96f42-151">een statusgebeurtenis wanneer Hallo gebrek aan resultaat duidt op een fout tooreport toevoegen Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="96f42-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="96f42-152">a.</span><span class="sxs-lookup"><span data-stu-id="96f42-152">a.</span></span> <span data-ttu-id="96f42-153">Hallo toevoegen `System.Fabric.Health` naamruimte toohello Stateful1.cs bestand.</span><span class="sxs-lookup"><span data-stu-id="96f42-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="96f42-154">b.</span><span class="sxs-lookup"><span data-stu-id="96f42-154">b.</span></span> <span data-ttu-id="96f42-155">Hallo code volgen na Hallo toevoegen `myDictionary.TryGetValueAsync` aanroepen</span><span class="sxs-lookup"><span data-stu-id="96f42-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="96f42-156">We gerapporteerd replica health omdat deze wordt gerapporteerd van een stateful service.</span><span class="sxs-lookup"><span data-stu-id="96f42-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="96f42-157">Hallo `HealthInformation` parameter wordt informatie opgeslagen over Hallo probleem met de status wordt gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="96f42-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="96f42-158">Als u een stateless service hebt gemaakt, Hallo volgende code gebruiken</span><span class="sxs-lookup"><span data-stu-id="96f42-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="96f42-159">Als uw service wordt uitgevoerd met beheerdersbevoegdheden, of als Hallo-cluster niet is [beveiligde](service-fabric-cluster-security.md), u kunt ook `FabricClient` tooreport health zoals weergegeven in Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="96f42-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="96f42-160">a.</span><span class="sxs-lookup"><span data-stu-id="96f42-160">a.</span></span> <span data-ttu-id="96f42-161">Hallo maken `FabricClient` exemplaar na Hallo `var myDictionary` declaratie.</span><span class="sxs-lookup"><span data-stu-id="96f42-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="96f42-162">b.</span><span class="sxs-lookup"><span data-stu-id="96f42-162">b.</span></span> <span data-ttu-id="96f42-163">Hallo code volgen na Hallo toevoegen `myDictionary.TryGetValueAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="96f42-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="96f42-164">We deze fout te simuleren en wordt weergegeven in Hallo health controleprogramma's weergegeven.</span><span class="sxs-lookup"><span data-stu-id="96f42-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="96f42-165">toosimulate hello is mislukt, commentaar Hallo eerste regel in Hallo health reporting code die u eerder hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="96f42-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="96f42-166">Nadat u de eerste regel Hallo uitcommentariëren, eruit Hallo code Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="96f42-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="96f42-167">Deze code wordt geactiveerd Hallo statusrapport telkens `RunAsync` wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="96f42-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="96f42-168">Nadat u Hallo wijzigen, drukt u op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="96f42-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="96f42-169">Nadat het Hallo-toepassing wordt uitgevoerd, opent u Service Fabric Explorer toocheck Hallo status van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="96f42-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="96f42-170">Deze tijd toont Service Fabric Explorer toepassing hello is beschadigd.</span><span class="sxs-lookup"><span data-stu-id="96f42-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="96f42-171">Dit is vanwege Hallo-fout die is gerapporteerd door Hallo code dat we eerder toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="96f42-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Slecht toepassingstype in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="96f42-173">Als u de primaire replica Hallo in de structuurweergave Hallo van Service Fabric Explorer selecteert, ziet u dat **status** te duidt op een fout.</span><span class="sxs-lookup"><span data-stu-id="96f42-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="96f42-174">Service Fabric Explorer geeft ook Hallo statusrapport details die waren toegevoegd toohello `HealthInformation` parameter in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="96f42-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="96f42-175">U kunt zien Hallo dezelfde statusrapporten in PowerShell en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="96f42-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Status van de replica in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="96f42-177">Dit rapport blijft in Hallo health manager totdat deze is vervangen door een ander rapport of totdat deze replica wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="96f42-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="96f42-178">Omdat we niet hebt ingesteld `TimeToLive` voor dit rapport health in Hallo `HealthInformation` object Hallo rapport verloopt nooit.</span><span class="sxs-lookup"><span data-stu-id="96f42-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="96f42-179">Het is raadzaam dat status op Hallo meest gedetailleerd niveau, dat in dit geval Hallo replica moet worden gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="96f42-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="96f42-180">U kunt ook rapporteren health `Partition`.</span><span class="sxs-lookup"><span data-stu-id="96f42-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="96f42-181">status voor tooreport `Application`, `DeployedApplication`, en `DeployedServicePackage`, gebruik `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="96f42-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="96f42-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96f42-182">Next steps</span></span>
* [<span data-ttu-id="96f42-183">Deep dive op Service Fabric-status</span><span class="sxs-lookup"><span data-stu-id="96f42-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="96f42-184">REST-API voor de status van de service reporting</span><span class="sxs-lookup"><span data-stu-id="96f42-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="96f42-185">REST-API voor het melden van toepassingsstatus</span><span class="sxs-lookup"><span data-stu-id="96f42-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

