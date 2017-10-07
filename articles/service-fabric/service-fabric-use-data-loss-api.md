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
# <a name="how-tooinvoke-data-loss-on-services"></a>Hoe tooInvoke gegevensverlies op Services
> [!WARNING]
> Dit document wordt beschreven hoe toocause gegevensverlies in uw services, en moet zorgvuldig worden gebruikt.
> 
> 

## <a name="introduction"></a>Inleiding
U kunt het verlies van gegevens op een partitie van uw Service Fabric-Service door de aanroepende StartPartitionDataLossAsync() aanroepen.  Deze api gebruikt Hallo veroorzaakt injectie en Analysis Services-tooperform Hallo werk toocause gegevens verloren gaan voorwaarden.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Met behulp van Hallo veroorzaakt injectie en Analysis Services
Hallo veroorzaakt injectie en Analysis Services ondersteunt momenteel Hallo-API's van Hallo onderstaande te volgen.  Hallo rechterzijde van Hallo grafiek bevat Hallo bijbehorende PowerShell-cmdlet.  Raadpleeg de msdn-documentatie toohello op elke API voor meer informatie over elk criterium.

| C# API | PowerShell-Cmdlet |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Conceptueel overzicht van een opdracht uit te voeren
Hallo veroorzaakt injectie en Analysis Services maakt gebruik van een asynchrone model waar u begint Hallo opdracht met één API bedoelde tooas Hallo 'Start' API in dit document, klikt u vervolgens controles Hallo voortgang van deze opdracht met behulp van een API 'GetProgress' totdat het een terminal is bereikt status, of totdat u annuleren deze.
een opdracht toostart Hallo 'Start' API niet aanroepen voor de bijbehorende API Hallo.  Deze API retourneert wanneer hello veroorzaakt injectie en Analysis Services-Hallo-aanvraag is geaccepteerd.  Maar deze niet wordt aangegeven hoe ver een opdracht is uitgevoerd, of zelfs als deze nog is gestart.  Aanroepen in volgorde toocheck voortgang van een opdracht, Hallo 'GetProgress' API die overeenkomt met toohello 'Start' API eerder genoemd.  Hallo 'GetProgress' API retourneert een object dat de huidige status Hallo Hallo-opdracht in de eigenschap status die aangeeft.  Een opdracht wordt uitgevoerd voor onbepaalde tijd tot:

1. Bewerking is voltooid.  Als u 'GetProgress' in dit geval erop aanroept, wordt status Hallo voortgang object voltooid.
2. Er wordt een onherstelbare fout aangetroffen.  Als u 'GetProgress' in dit geval erop aanroept, Hallo voortgang van de status van object mislukt
3. U deze annuleren via Hallo [CancelTestCommandAsync] [ cancel] -API of [Stop ServiceFabricTestCommand] [ cancelps] PowerShell-cmdlet.  Als u 'GetProgress' in dit geval erop aanroepen, hello voortgang Objectstatus worden geannuleerd of ForceCancelled, afhankelijk van een argument toothat API.  Zie de documentatie voor Hallo [CancelTestCommandAsync] [ cancel] voor meer informatie.

## <a name="details-of-running-a-command"></a>Details van een opdracht uit te voeren
In de volgorde toostart een opdracht, roept Hallo API gestart met argumenten Hallo verwacht.  Alle Start API's hebben een Guid-argument met de naam operationId.  U moet bijhouden van Hallo operationId argument, omdat deze wordt gebruikt tootrack voortgang van deze opdracht.  Dit moet worden doorgegeven in Hallo 'GetProgress' API volgorde tootrack uitgevoerd Hallo-opdracht.  Hallo operationId moet uniek zijn.

De eigenschap State van het object is na het aanroepen van Hallo Start API Hallo GetProgress API moet worden aangeroepen in een lus totdat Hallo geretourneerd voortgang is voltooid.  Alle [van FabricTransientException] [ fte] en van OperationCanceledException moet opnieuw worden geprobeerd.
Wanneer het Hallo-opdracht heeft een definitieve status (voltooid, Faulted of geannuleerd) bereikt, geretourneerd Hallo voortgang van de eigenschap van het object resultaat heeft aanvullende informatie.  Als het Hallo-status is voltooid, bevat Result.SelectedPartition.PartitionId Hallo partitie-id die is geselecteerd.  Result.Exception wordt niet null zijn.  Als Hallo status is mislukt, hebt Result.Exception Hallo reden Hallo veroorzaakt injectie en Analysis Services is een fout opgetreden Hallo-opdracht.  Result.SelectedPartition.PartitionId hebben Hallo partitie-id die is geselecteerd.  In sommige situaties kan Hallo-opdracht niet verdergaat ver toochoose een partitie.  Hallo PartitionId wordt in dat geval niet 0 zijn.  Als de status van de Hallo is geannuleerd, wordt Result.Exception niet null zijn.  Zoals Hallo Faulted geval, Result.SelectedPartition.PartitionId heeft Hallo partitie-id die is gekozen, maar als Hallo-opdracht is niet zo soepel ver toodo, wordt deze 0 zijn.  Raadpleeg ook toohello voorbeeld hieronder.

Hallo voorbeeldcode hieronder ziet u hoe toostart vervolgens uitgevoerd op een opdracht toocause gegevensverlies op een specifieke partitie controleren.

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

Hallo voorbeeld hieronder ziet u hoe toouse Hallo PartitionSelector toochoose een willekeurige partitie van een opgegeven service:

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

## <a name="history-and-truncation"></a>Geschiedenis en moet worden afgekapt
Nadat een opdracht een definitieve status bereikt is, de metagegevens van de blijft in Hallo veroorzaakt injectie en Analysis Service voor een bepaalde tijd voordat het is mogelijk verwijderd toosave ruimte.  Als 'GetProgress' wordt aangeroepen met Hallo operationId van een opdracht nadat deze is verwijderd, wordt een FabricException met een ErrorCode KeyNotFound geretourneerd.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
