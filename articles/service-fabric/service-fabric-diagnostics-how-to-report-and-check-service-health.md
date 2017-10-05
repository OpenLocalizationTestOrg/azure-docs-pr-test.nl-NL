---
title: Rapporteren en controleer de status van Azure Service Fabric | Microsoft Docs
description: Informatie over het statusrapporten verzenden vanuit uw servicecode en het controleren van de status van uw service met behulp van de health-controleprogramma die Azure Service Fabric bevat.
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="7b17c-103">Servicestatus rapporteren en controleren</span><span class="sxs-lookup"><span data-stu-id="7b17c-103">Report and check service health</span></span>
<span data-ttu-id="7b17c-104">Wanneer uw services problemen ondervindt, is de mogelijkheid om te reageren op en oplossen van incidenten en storingen afhankelijk van de mogelijkheid voor het detecteren van de problemen snel.</span><span class="sxs-lookup"><span data-stu-id="7b17c-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="7b17c-105">Als u problemen en fouten aan de Azure Service Fabric health manager vanuit uw servicecode, kunt u standaard voor health monitoring hulpprogramma's die Service Fabric bevat om de health-status te controleren.</span><span class="sxs-lookup"><span data-stu-id="7b17c-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="7b17c-106">Er zijn drie manieren dat u de status van de service kan rapporteren:</span><span class="sxs-lookup"><span data-stu-id="7b17c-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="7b17c-107">Gebruik [partitie](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) of [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objecten.</span><span class="sxs-lookup"><span data-stu-id="7b17c-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="7b17c-108">U kunt de `Partition` en `CodePackageActivationContext` objecten voor het rapporteren van de status van de elementen die deel van de huidige context uitmaken.</span><span class="sxs-lookup"><span data-stu-id="7b17c-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="7b17c-109">Code die wordt uitgevoerd als onderdeel van een replica kan bijvoorbeeld health rapporteren alleen op die replica en de partitie die hoort bij de toepassing die deel van uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="7b17c-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="7b17c-110">Gebruik `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="7b17c-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="7b17c-111">U kunt `FabricClient` aan het rapport de status van de code als het cluster niet [beveiligde](service-fabric-cluster-security.md) of als de service wordt uitgevoerd met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="7b17c-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="7b17c-112">De meeste real-world scenario's geen niet-beveiligde clusters gebruiken of bieden beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="7b17c-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="7b17c-113">Met `FabricClient`, u kunt een entiteit die deel uitmaakt van het cluster health rapporteren.</span><span class="sxs-lookup"><span data-stu-id="7b17c-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="7b17c-114">In het ideale geval echter moet servicecode alleen rapporten verzenden die gerelateerd zijn aan een eigen health.</span><span class="sxs-lookup"><span data-stu-id="7b17c-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="7b17c-115">Gebruik de REST API's op het cluster, toepassing, geïmplementeerde toepassingen, service, servicepakket, partitie, replica of knooppunt niveaus.</span><span class="sxs-lookup"><span data-stu-id="7b17c-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="7b17c-116">Dit kan worden gebruikt voor het rapporteren van de status van binnen een container.</span><span class="sxs-lookup"><span data-stu-id="7b17c-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="7b17c-117">Dit artikel begeleidt u bij een voorbeeld waarin de status van de code van de rapporten.</span><span class="sxs-lookup"><span data-stu-id="7b17c-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="7b17c-118">Het voorbeeld ziet ook hoe de hulpprogramma's van Service Fabric kunnen worden gebruikt om de health-status te controleren.</span><span class="sxs-lookup"><span data-stu-id="7b17c-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="7b17c-119">In dit artikel is bedoeld als een korte inleiding in de controlefuncties van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b17c-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="7b17c-120">U kunt de reeks diepgaande artikelen over health die met de koppeling aan het einde van dit artikel beginnen lezen voor meer gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="7b17c-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b17c-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b17c-121">Prerequisites</span></span>
<span data-ttu-id="7b17c-122">Hiervoor hebt u het volgende zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="7b17c-122">You must have the following installed:</span></span>

* <span data-ttu-id="7b17c-123">Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7b17c-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="7b17c-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="7b17c-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="7b17c-125">Een lokale veilige dev-cluster maken</span><span class="sxs-lookup"><span data-stu-id="7b17c-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="7b17c-126">Open PowerShell met beheerdersbevoegdheden en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7b17c-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Opdrachten die laten zien hoe u een beveiligde dev-cluster maken](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="7b17c-128">Een toepassing implementeren en controleren van de status</span><span class="sxs-lookup"><span data-stu-id="7b17c-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="7b17c-129">Open Visual Studio als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7b17c-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="7b17c-130">Een project maken met behulp van de **Stateful Service** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7b17c-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Maken van een Service Fabric-toepassing met Stateful Service](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="7b17c-132">Druk op **F5** voor het uitvoeren van de toepassing in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="7b17c-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="7b17c-133">De toepassing wordt geïmplementeerd op het lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="7b17c-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="7b17c-134">Nadat de toepassing wordt uitgevoerd, met de rechtermuisknop op het pictogram Lokaal Clusterbeheer in het systeemvak en selecteert u **lokaal Cluster beheren** in het snelmenu om Service Fabric Explorer te openen.</span><span class="sxs-lookup"><span data-stu-id="7b17c-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Service Fabric Explorer openen vanuit het systeemvak](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="7b17c-136">De toepassingsstatus moet worden weergegeven zoals in deze afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7b17c-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="7b17c-137">Op dit moment moet de toepassing zonder fouten in orde.</span><span class="sxs-lookup"><span data-stu-id="7b17c-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![In orde toepassing in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="7b17c-139">U kunt ook de status controleren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b17c-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="7b17c-140">U kunt ```Get-ServiceFabricApplicationHealth``` om te controleren van de status van een toepassing, en u kunnen gebruiken ```Get-ServiceFabricServiceHealth``` om te controleren van de status van een service.</span><span class="sxs-lookup"><span data-stu-id="7b17c-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="7b17c-141">Het statusrapport voor dezelfde toepassing in PowerShell is in deze afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7b17c-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![In orde toepassing in PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="7b17c-143">Aangepaste health gebeurtenissen toevoegen aan uw servicecode</span><span class="sxs-lookup"><span data-stu-id="7b17c-143">To add custom health events to your service code</span></span>
<span data-ttu-id="7b17c-144">De sjablonen voor de Service Fabric-project in Visual Studio bevatten voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="7b17c-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="7b17c-145">De volgende stappen laten zien hoe u aangepaste health gebeurtenissen vanuit uw servicecode kan rapporteren.</span><span class="sxs-lookup"><span data-stu-id="7b17c-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="7b17c-146">Deze rapporten weergegeven automatisch in de standaard hulpprogramma's voor statuscontrole biedt Service Fabric, zoals Service Fabric Explorer, Azure portal health weergeven en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b17c-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="7b17c-147">Open de toepassing die u eerder hebt gemaakt in Visual Studio of een nieuwe toepassing maken met behulp van de **Stateful Service** Visual Studio-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7b17c-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="7b17c-148">Open het bestand Stateful1.cs en zoek de `myDictionary.TryGetValueAsync` -aanroep in de `RunAsync` methode.</span><span class="sxs-lookup"><span data-stu-id="7b17c-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="7b17c-149">U ziet dat deze methode retourneert een `result` die bevat de huidige waarde van de teller omdat de sleutel logica in deze toepassing is een aantal actief houden.</span><span class="sxs-lookup"><span data-stu-id="7b17c-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="7b17c-150">Als dit een echte toepassing zijn, en als het ontbreken van het resultaat van een fout weergegeven, wilt u dat de gebeurtenis vlag.</span><span class="sxs-lookup"><span data-stu-id="7b17c-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="7b17c-151">Toevoegen de volgende stappen uit om het rapport een statusgebeurtenis wanneer het ontbreken van resultaat duidt op een fout.</span><span class="sxs-lookup"><span data-stu-id="7b17c-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="7b17c-152">a.</span><span class="sxs-lookup"><span data-stu-id="7b17c-152">a.</span></span> <span data-ttu-id="7b17c-153">Voeg de `System.Fabric.Health` naamruimte naar het bestand Stateful1.cs.</span><span class="sxs-lookup"><span data-stu-id="7b17c-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="7b17c-154">b.</span><span class="sxs-lookup"><span data-stu-id="7b17c-154">b.</span></span> <span data-ttu-id="7b17c-155">Voeg de volgende code na de `myDictionary.TryGetValueAsync` aanroepen</span><span class="sxs-lookup"><span data-stu-id="7b17c-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="7b17c-156">We gerapporteerd replica health omdat deze wordt gerapporteerd van een stateful service.</span><span class="sxs-lookup"><span data-stu-id="7b17c-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="7b17c-157">De `HealthInformation` parameter wordt opgeslagen informatie over het statusprobleem met de wordt gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="7b17c-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="7b17c-158">Als u een stateless service hebt gemaakt, gebruikt u de volgende code</span><span class="sxs-lookup"><span data-stu-id="7b17c-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="7b17c-159">Als uw service wordt uitgevoerd met beheerdersbevoegdheden, of als het cluster niet [beveiligde](service-fabric-cluster-security.md), u kunt ook `FabricClient` voor de gezondheid van het rapport zoals weergegeven in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="7b17c-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="7b17c-160">a.</span><span class="sxs-lookup"><span data-stu-id="7b17c-160">a.</span></span> <span data-ttu-id="7b17c-161">Maak de `FabricClient` exemplaar na de `var myDictionary` declaratie.</span><span class="sxs-lookup"><span data-stu-id="7b17c-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="7b17c-162">b.</span><span class="sxs-lookup"><span data-stu-id="7b17c-162">b.</span></span> <span data-ttu-id="7b17c-163">Voeg de volgende code na de `myDictionary.TryGetValueAsync` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="7b17c-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="7b17c-164">Laten we simuleren van deze fout en wordt weergegeven in de health-controleprogramma weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b17c-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="7b17c-165">De fout moet de eerste regel in de health reporting code die u eerder hebt toegevoegd commentaar simuleren.</span><span class="sxs-lookup"><span data-stu-id="7b17c-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="7b17c-166">Nadat u de eerste regel uitcommentariëren, wordt de code eruit als in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7b17c-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="7b17c-167">Deze code wordt het statusrapport geactiveerd telkens `RunAsync` wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b17c-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="7b17c-168">Nadat u de wijziging aanbrengt, drukt u op **F5** de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7b17c-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="7b17c-169">Nadat de toepassing wordt uitgevoerd, opent u de Service Fabric Explorer om te controleren van de status van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b17c-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="7b17c-170">Deze tijd ziet Service Fabric Explorer u dat de toepassing niet in orde is.</span><span class="sxs-lookup"><span data-stu-id="7b17c-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="7b17c-171">Dit is vanwege de fout die is gerapporteerd door de code dat we eerder toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7b17c-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Slecht toepassingstype in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="7b17c-173">Als u de primaire replica in de structuurweergave van Service Fabric Explorer selecteert, ziet u dat **status** te duidt op een fout.</span><span class="sxs-lookup"><span data-stu-id="7b17c-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="7b17c-174">Service Fabric Explorer geeft ook de health-rapportgegevens die zijn toegevoegd aan de `HealthInformation` parameter in de code.</span><span class="sxs-lookup"><span data-stu-id="7b17c-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="7b17c-175">Hier ziet u de dezelfde statusrapporten in PowerShell en de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7b17c-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Status van de replica in Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="7b17c-177">Dit rapport blijft in de health manager totdat deze is vervangen door een ander rapport of totdat deze replica wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7b17c-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="7b17c-178">Omdat we niet hebt ingesteld `TimeToLive` voor deze health-rapport in de `HealthInformation` object, het rapport verloopt nooit.</span><span class="sxs-lookup"><span data-stu-id="7b17c-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="7b17c-179">Het is raadzaam dat status op het meest gedetailleerd niveau, in dit geval de replica wordt moet worden gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="7b17c-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="7b17c-180">U kunt ook rapporteren health `Partition`.</span><span class="sxs-lookup"><span data-stu-id="7b17c-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="7b17c-181">Voor de gezondheid van het rapport op `Application`, `DeployedApplication`, en `DeployedServicePackage`, gebruik `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="7b17c-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="7b17c-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b17c-182">Next steps</span></span>
* [<span data-ttu-id="7b17c-183">Deep dive op Service Fabric-status</span><span class="sxs-lookup"><span data-stu-id="7b17c-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="7b17c-184">REST-API voor de status van de service reporting</span><span class="sxs-lookup"><span data-stu-id="7b17c-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="7b17c-185">REST-API voor het melden van toepassingsstatus</span><span class="sxs-lookup"><span data-stu-id="7b17c-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

