---
title: aaaHow tooInvoke gegevensverlies op de Service Fabric-Services | Microsoft Docs
description: Hierin wordt beschreven hoe toouse gegevensverlies Hallo api
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="84967-103">Hoe tooInvoke gegevensverlies op Services</span><span class="sxs-lookup"><span data-stu-id="84967-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="84967-104">Dit document wordt beschreven hoe toocause gegevensverlies in uw services, en moet zorgvuldig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="84967-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="84967-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="84967-105">Introduction</span></span>
<span data-ttu-id="84967-106">U kunt het verlies van gegevens op een partitie van uw Service Fabric-Service door de aanroepende StartPartitionDataLossAsync() aanroepen.</span><span class="sxs-lookup"><span data-stu-id="84967-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="84967-107">Deze api gebruikt Hallo veroorzaakt injectie en Analysis Services-tooperform Hallo werk toocause gegevens verloren gaan voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="84967-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="84967-108">Met behulp van Hallo veroorzaakt injectie en Analysis Services</span><span class="sxs-lookup"><span data-stu-id="84967-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="84967-109">Hallo veroorzaakt injectie en Analysis Services ondersteunt momenteel Hallo-API's van Hallo onderstaande te volgen.</span><span class="sxs-lookup"><span data-stu-id="84967-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="84967-110">Hallo rechterzijde van Hallo grafiek bevat Hallo bijbehorende PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84967-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="84967-111">Raadpleeg de msdn-documentatie toohello op elke API voor meer informatie over elk criterium.</span><span class="sxs-lookup"><span data-stu-id="84967-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="84967-112">C# API</span><span class="sxs-lookup"><span data-stu-id="84967-112">C# API</span></span> | <span data-ttu-id="84967-113">PowerShell-Cmdlet</span><span class="sxs-lookup"><span data-stu-id="84967-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="84967-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="84967-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="84967-115">[Start ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="84967-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="84967-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="84967-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="84967-117">[Start ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="84967-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="84967-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="84967-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="84967-119">[Start ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="84967-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="84967-120">Conceptueel overzicht van een opdracht uit te voeren</span><span class="sxs-lookup"><span data-stu-id="84967-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="84967-121">Hallo veroorzaakt injectie en Analysis Services maakt gebruik van een asynchrone model waar u begint Hallo opdracht met één API bedoelde tooas Hallo 'Start' API in dit document, klikt u vervolgens controles Hallo voortgang van deze opdracht met behulp van een API 'GetProgress' totdat het een terminal is bereikt status, of totdat u annuleren deze.</span><span class="sxs-lookup"><span data-stu-id="84967-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="84967-122">een opdracht toostart Hallo 'Start' API niet aanroepen voor de bijbehorende API Hallo.</span><span class="sxs-lookup"><span data-stu-id="84967-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="84967-123">Deze API retourneert wanneer hello veroorzaakt injectie en Analysis Services-Hallo-aanvraag is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="84967-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="84967-124">Maar deze niet wordt aangegeven hoe ver een opdracht is uitgevoerd, of zelfs als deze nog is gestart.</span><span class="sxs-lookup"><span data-stu-id="84967-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="84967-125">Aanroepen in volgorde toocheck voortgang van een opdracht, Hallo 'GetProgress' API die overeenkomt met toohello 'Start' API eerder genoemd.</span><span class="sxs-lookup"><span data-stu-id="84967-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="84967-126">Hallo 'GetProgress' API retourneert een object dat de huidige status Hallo Hallo-opdracht in de eigenschap status die aangeeft.</span><span class="sxs-lookup"><span data-stu-id="84967-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="84967-127">Een opdracht wordt uitgevoerd voor onbepaalde tijd tot:</span><span class="sxs-lookup"><span data-stu-id="84967-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="84967-128">Bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="84967-128">It completes successfully.</span></span>  <span data-ttu-id="84967-129">Als u 'GetProgress' in dit geval erop aanroept, wordt status Hallo voortgang object voltooid.</span><span class="sxs-lookup"><span data-stu-id="84967-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="84967-130">Er wordt een onherstelbare fout aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="84967-130">It encounters a fatal error.</span></span>  <span data-ttu-id="84967-131">Als u 'GetProgress' in dit geval erop aanroept, Hallo voortgang van de status van object mislukt</span><span class="sxs-lookup"><span data-stu-id="84967-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="84967-132">U deze annuleren via Hallo [CancelTestCommandAsync] [ cancel] -API of [Stop ServiceFabricTestCommand] [ cancelps] PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84967-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="84967-133">Als u 'GetProgress' in dit geval erop aanroepen, hello voortgang Objectstatus worden geannuleerd of ForceCancelled, afhankelijk van een argument toothat API.</span><span class="sxs-lookup"><span data-stu-id="84967-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="84967-134">Zie de documentatie voor Hallo [CancelTestCommandAsync] [ cancel] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="84967-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="84967-135">Details van een opdracht uit te voeren</span><span class="sxs-lookup"><span data-stu-id="84967-135">Details of Running a Command</span></span>
<span data-ttu-id="84967-136">In de volgorde toostart een opdracht, roept Hallo API gestart met argumenten Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="84967-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="84967-137">Alle Start API's hebben een Guid-argument met de naam operationId.</span><span class="sxs-lookup"><span data-stu-id="84967-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="84967-138">U moet bijhouden van Hallo operationId argument, omdat deze wordt gebruikt tootrack voortgang van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="84967-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="84967-139">Dit moet worden doorgegeven in Hallo 'GetProgress' API volgorde tootrack uitgevoerd Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="84967-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="84967-140">Hallo operationId moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="84967-140">hello operationId must be unique.</span></span>

<span data-ttu-id="84967-141">De eigenschap State van het object is na het aanroepen van Hallo Start API Hallo GetProgress API moet worden aangeroepen in een lus totdat Hallo geretourneerd voortgang is voltooid.</span><span class="sxs-lookup"><span data-stu-id="84967-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="84967-142">Alle [van FabricTransientException] [ fte] en van OperationCanceledException moet opnieuw worden geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="84967-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="84967-143">Wanneer het Hallo-opdracht heeft een definitieve status (voltooid, Faulted of geannuleerd) bereikt, geretourneerd Hallo voortgang van de eigenschap van het object resultaat heeft aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="84967-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="84967-144">Als het Hallo-status is voltooid, bevat Result.SelectedPartition.PartitionId Hallo partitie-id die is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="84967-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="84967-145">Result.Exception wordt niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="84967-145">Result.Exception will be null.</span></span>  <span data-ttu-id="84967-146">Als Hallo status is mislukt, hebt Result.Exception Hallo reden Hallo veroorzaakt injectie en Analysis Services is een fout opgetreden Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="84967-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="84967-147">Result.SelectedPartition.PartitionId hebben Hallo partitie-id die is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="84967-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="84967-148">In sommige situaties kan Hallo-opdracht niet verdergaat ver toochoose een partitie.</span><span class="sxs-lookup"><span data-stu-id="84967-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="84967-149">Hallo PartitionId wordt in dat geval niet 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="84967-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="84967-150">Als de status van de Hallo is geannuleerd, wordt Result.Exception niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="84967-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="84967-151">Zoals Hallo Faulted geval, Result.SelectedPartition.PartitionId heeft Hallo partitie-id die is gekozen, maar als Hallo-opdracht is niet zo soepel ver toodo, wordt deze 0 zijn.</span><span class="sxs-lookup"><span data-stu-id="84967-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="84967-152">Raadpleeg ook toohello voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="84967-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="84967-153">Hallo voorbeeldcode hieronder ziet u hoe toostart vervolgens uitgevoerd op een opdracht toocause gegevensverlies op een specifieke partitie controleren.</span><span class="sxs-lookup"><span data-stu-id="84967-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="84967-154">Hallo voorbeeld hieronder ziet u hoe toouse Hallo PartitionSelector toochoose een willekeurige partitie van een opgegeven service:</span><span class="sxs-lookup"><span data-stu-id="84967-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="84967-155">Geschiedenis en moet worden afgekapt</span><span class="sxs-lookup"><span data-stu-id="84967-155">History and Truncation</span></span>
<span data-ttu-id="84967-156">Nadat een opdracht een definitieve status bereikt is, de metagegevens van de blijft in Hallo veroorzaakt injectie en Analysis Service voor een bepaalde tijd voordat het is mogelijk verwijderd toosave ruimte.</span><span class="sxs-lookup"><span data-stu-id="84967-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="84967-157">Als 'GetProgress' wordt aangeroepen met Hallo operationId van een opdracht nadat deze is verwijderd, wordt een FabricException met een ErrorCode KeyNotFound geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="84967-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
