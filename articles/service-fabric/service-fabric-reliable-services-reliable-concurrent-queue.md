---
title: aaaReliableConcurrentQueue in Azure Service Fabric
description: ReliableConcurrentQueue is een hoge gegevensdoorvoer wachtrij die u kunt parallelle enqueues en dequeues.
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Inleiding tooReliableConcurrentQueue in Azure Service Fabric
Betrouwbare gelijktijdige wachtrij is een asynchrone transactionele en gerepliceerde wachtrij welke functies hoge gelijktijdigheid van taken voor de wachtrij plaatsen en bewerkingen in wachtrij. Het is ontworpen toodeliver hoge doorvoer en lage latentie door ontspannen Hallo strikte FIFO-principe ordening geleverd door [betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx) en stelt u in plaats daarvan een rangschikking van best-effort.

## <a name="apis"></a>API's

|Gelijktijdige wachtrij                |Betrouwbare gelijktijdige wachtrij                                         |
|--------------------------------|------------------------------------------------------------------|
| VOID Enqueue(T item)           | Taak EnqueueAsync (tx ITransaction, T-item)                       |
| BOOL TryDequeue (uit resultaat T)  | Taak < ConditionalValue < T >> TryDequeueAsync (tx ITransaction)  |
| int Count()                    | lange Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Vergelijking met [betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Betrouwbare gelijktijdige wachtrij wordt aangeboden als een alternatief te[betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx). Het moet worden gebruikt in gevallen waarbij strikte FIFO-principe ordening niet vereist is als het FIFO-principe vereist een afweging met gelijktijdigheid van taken te garanderen.  [Betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx) maakt gebruik van vergrendelingen tooenforce FIFO-principe bestellen, met maximaal één transactie tooenqueue toegestaan en maximaal één transactie toodequeue tegelijk toegestaan. Ter vergelijking, betrouwbare gelijktijdige wachtrij Hallo beperking rangschikken met deze sjabloon worden en kan een aantal gelijktijdige transacties toointerleave hun in de wachtrij plaatsen en bewerkingen in wachtrij. Best-effort ordening is opgegeven, wordt echter nooit relatieve ordening van Hallo van twee waarden in een betrouwbare gelijktijdige wachtrij kan worden gegarandeerd.

Betrouwbare gelijktijdige wachtrij biedt hogere doorvoer en lagere latentie mogelijk dan [betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx) wanneer er meerdere gelijktijdige transacties enqueues uitvoeren en/of dequeues.

Een voorbeeld van een gebruiksvoorbeeld voor Hallo ReliableConcurrentQueue is Hallo [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario. In dit scenario kan een of meer bericht producenten maken en toevoegen van items toohello wachtrij en een of meer bericht consumenten berichten uit de wachtrij Hallo ophalen en deze te verwerken. Meerdere producenten en consumenten kunnen onafhankelijk werken, met behulp van gelijktijdige transacties in volgorde tooprocess Hallo wachtrij.

## <a name="usage-guidelines"></a>Richtlijnen voor het gebruik
* Hallo-wachtrij wordt verwacht dat items in de wachtrij Hallo Hallo een lage bewaarperiode hebben. Dat wil zeggen, zou Hallo items blijven niet in wachtrij Hallo gedurende een lange periode.
* Hallo-wachtrij wordt niet gegarandeerd dat strikte FIFO-principe bestellen.
* Hallo wachtrij heeft een eigen schrijfbewerkingen niet lezen. Als een item in de wachtrij binnen een transactie is, is het niet langer zichtbaar tooa dequeuer binnen Hallo dezelfde transactie.
* Dequeues zijn niet van elkaar geïsoleerd. Als het item *A* uit wachtrij is geplaatst in transactie *txnA*, ook al *txnA* is geen item worden toegewezen, *A* niet zichtbaar tooa gelijktijdige transactie *txnB*.  Als *txnA* wordt afgebroken, *A* wordt zichtbaar te*txnB* onmiddellijk.
* *TryPeekAsync* gedrag kan worden geïmplementeerd met behulp van een *TryDequeueAsync* en vervolgens Hallo-transactie afgebroken. Een voorbeeld hiervan vindt u in Hallo Programming patronen sectie.
* Aantal is niet-transactionele. Het kan gebruikte tooget een idee van het aantal elementen in de wachtrij Hallo Hallo maar vertegenwoordigt een punt in tijd en kan niet worden gebruikt.
* Dure verwerking op Hallo items uit wachtrij geplaatst moeten niet worden uitgevoerd terwijl Hallo transactie actief is, tooavoid langlopende transacties die mogelijk invloed op de prestaties op Hallo-systeem.

## <a name="code-snippets"></a>Codefragmenten
Laat het ons Bekijk enkele codefragmenten en de verwachte uitvoer. Afhandeling van uitzonderingen wordt in deze sectie genegeerd.

### <a name="enqueueasync"></a>EnqueueAsync
Hier volgen enkele codefragmenten voor het gebruik van EnqueueAsync gevolgd door de verwachte uitvoer.

- *Voorbeeld 1: Één taak in de wachtrij plaatsen*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Wordt ervan uitgegaan dat Hallo-taak is voltooid en dat er geen gelijktijdige transacties Hallo wachtrij wijzigen. Hallo-gebruiker kan Hallo wachtrij toocontain Hallo-items in een van volgende orders Hallo verwachten:

> 10, 20

> 20, 10


- *Voorbeeld 2: Parallelle taak in de wachtrij plaatsen*

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

Wordt ervan uitgegaan dat Hallo taken is voltooid, of Hallo taken parallel uitgevoerd en er zijn geen andere gelijktijdige transacties Hallo wachtrij wijzigen. Er is geen Deductie kan worden gemaakt over Hallo volgorde van items in de wachtrij Hallo. Voor dit codefragment Hallo items mogelijk weergegeven in een van de Hallo 4! mogelijke volgorden.  Hallo wachtrij probeert tookeep Hallo items in volgorde van Hallo oorspronkelijke (in wachtrij gezet), maar kan niet geforceerd tooreorder ze vervaldatum tooconcurrent operations of fouten.


### <a name="dequeueasync"></a>DequeueAsync
Hier volgen enkele codefragmenten voor het gebruik van TryDequeueAsync gevolgd door Hallo verwacht uitvoer. Stel dat die wachtrij Hallo al is gevuld met de volgende items in de wachtrij Hallo Hallo:
> 10, 20, 30, 40, 50, 60

- *Voorbeeld 1: Één taak in wachtrij*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Wordt ervan uitgegaan dat Hallo-taak is voltooid en dat er geen gelijktijdige transacties Hallo wachtrij wijzigen. Omdat er geen Deductie kan worden gemaakt over Hallo volgorde van items in de wachtrij Hallo hello, alle drie Hallo items kunnen worden uit wachtrij geplaatst, in willekeurige volgorde. Hallo wachtrij probeert tookeep Hallo items in volgorde van Hallo oorspronkelijke (in wachtrij gezet), maar kan niet geforceerd tooreorder ze vervaldatum tooconcurrent operations of fouten.  

- *Voorbeeld 2: Taak Parallel uit de wachtrij halen*

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

Wordt ervan uitgegaan dat Hallo taken is voltooid, of Hallo taken parallel uitgevoerd en er zijn geen andere gelijktijdige transacties Hallo wachtrij wijzigen. Omdat er geen Deductie kan worden gemaakt over Hallo volgorde van items in de wachtrij Hallo hello, lijsten Hallo *dequeue1* en *dequeue2* wordt elke twee items, in willekeurige volgorde bevatten.

Hallo hetzelfde item wordt *niet* in beide lijsten worden weergegeven. Daarom als dequeue1 *10*, *30*, en vervolgens dequeue2 zou hebben *20*, *40*.

- *Voorbeeld 3: Wachtrij ordening met transactie afgebroken*

Een transactie met onderweg wordt afgebroken dequeues puts Hallo items terug op Hallo hoofd van Hallo wachtrij. Hallo volgorde waarin Hallo-items worden geplaatst terug op Hallo hoofd van Hallo wachtrij kan niet worden gegarandeerd. Laat het ons Hallo code volgende bekijken:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Stel dat Hallo items uit de wachtrij in Hallo volgorde zijn geplaatst:
> 10, 20

We Hallo transactie afgebroken, Hallo items zou worden toegevoegd wanneer back toohello hoofd van Hallo wachtrij in een Hallo orders te volgen:
> 10, 20

> 20, 10

Hallo geldt voor alle gevallen waarbij Hallo transactie niet met succes is *doorgevoerd*.

## <a name="programming-patterns"></a>Patronen programmering
In deze sectie laat het ons kijken enkele programmering patronen die mogelijk nuttig zijn bij het gebruik van ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Batch Dequeues
Een aanbevolen programming patroon is voor Hallo consumer taak toobatch de dequeues in plaats van een wachtrij op een tijdstip. Hallo-gebruiker kan toothrottle vertragingen tussen elke batch of Hallo batchgrootte kiezen. Hallo bevat volgende codefragment dit programmeermodel.  Houd er rekening mee dat in dit voorbeeld Hallo verwerken is voltooid nadat Hallo transactie doorgevoerd is, dus als een fout toooccur tijdens de verwerking, hello onverwerkte items zullen verloren zonder dat is verwerkt.  U kunt ook Hallo verwerking kan worden uitgevoerd binnen bereik van de transactie hello, maar dit kan een negatieve invloed hebben op prestaties en vereist dat de verwerking van Hallo items al verwerkt.

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a>Verwerking van Best-Effort op basis van meldingen
Hallo Count-API maakt gebruik van een ander interessant programming patroon. Hier kunnen we best-effort op basis van meldingen verwerking voor Hallo wachtrij implementeren. Hallo wachtrij aantal kan worden gebruikt toothrottle een wachtrij plaatsen of een taak wachtrij halen.  Houd er rekening mee dat zoals in het vorige voorbeeld Hallo, aangezien Hallo verwerking vindt plaats buiten Hallo-transactie niet-verwerkte items mogelijk verloren als er een fout optreedt tijdens de verwerking.

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a>Best-Effort leegmaken
Leegmaken van Hallo wachtrij kan niet worden gegarandeerd vanwege toohello gelijktijdige aard van Hallo gegevensstructuur.  Het is mogelijk dat, zelfs als er geen gebruiker bewerkingen op Hallo wachtrij onderweg, een bepaalde oproep tooTryDequeueAsync kan niet als resultaat een item die eerder in de wachtrij en doorgevoerd.  Hallo in wachtrij gezet item te is gegarandeerd*uiteindelijk* zichtbaar toodequeue worden echter zonder een out-of-band-communicatiemechanisme een onafhankelijke consumer kan niet weet die Hallo wachtrij heeft bereikt een stabiele status zelfs als alle producenten zijn gestopt en er zijn geen nieuwe wachtrij plaatsen bewerkingen zijn toegestaan. Hallo leegmaken bewerking is dus best-effort zoals hieronder wordt geïmplementeerd.

Hallo gebruiker moet alle verdere producenten en consumenten taken stoppen en wachten op een onderweg transacties toocommit of afbreken voordat u probeert toodrain Hallo wachtrij.  Als Hallo gebruiker Hallo verwacht aantal items in de wachtrij hello kent, kunnen ze een melding die geeft aan dat alle items uit wachtrij hebben is geplaatst instellen.

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a>Piek
ReliableConcurrentQueue biedt geen Hallo *TryPeekAsync* api. Gebruikers kunnen krijgen Hallo peek semantische met behulp van een *TryDequeueAsync* en vervolgens Hallo-transactie afgebroken. In dit voorbeeld dequeues worden verwerkt alleen als het Hallo-item groter is dan *10*.

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a>Moet lezen
* [Snel starten Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Werken met betrouwbare verzamelingen](service-fabric-work-with-reliable-collections.md)
* [Betrouwbare Services meldingen](service-fabric-reliable-services-notifications.md)
* [Reliable Services Backup and Restore (herstel na noodgevallen)](service-fabric-reliable-services-backup-restore.md)
* [Configuratie van betrouwbare status Manager](service-fabric-reliable-services-configuration.md)
* [Aan de slag met Service Fabric Web API-Services](service-fabric-reliable-services-communication-webapi.md)
* [Geavanceerd gebruik Hallo betrouwbare Services Programming Model](service-fabric-reliable-services-advanced-usage.md)
* [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
