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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="622cc-103">Inleiding tooReliableConcurrentQueue in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="622cc-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="622cc-104">Betrouwbare gelijktijdige wachtrij is een asynchrone transactionele en gerepliceerde wachtrij welke functies hoge gelijktijdigheid van taken voor de wachtrij plaatsen en bewerkingen in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="622cc-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="622cc-105">Het is ontworpen toodeliver hoge doorvoer en lage latentie door ontspannen Hallo strikte FIFO-principe ordening geleverd door [betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx) en stelt u in plaats daarvan een rangschikking van best-effort.</span><span class="sxs-lookup"><span data-stu-id="622cc-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="622cc-106">API's</span><span class="sxs-lookup"><span data-stu-id="622cc-106">APIs</span></span>

|<span data-ttu-id="622cc-107">Gelijktijdige wachtrij</span><span class="sxs-lookup"><span data-stu-id="622cc-107">Concurrent Queue</span></span>                |<span data-ttu-id="622cc-108">Betrouwbare gelijktijdige wachtrij</span><span class="sxs-lookup"><span data-stu-id="622cc-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="622cc-109">VOID Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="622cc-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="622cc-110">Taak EnqueueAsync (tx ITransaction, T-item)</span><span class="sxs-lookup"><span data-stu-id="622cc-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="622cc-111">BOOL TryDequeue (uit resultaat T)</span><span class="sxs-lookup"><span data-stu-id="622cc-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="622cc-112">Taak < ConditionalValue < T >> TryDequeueAsync (tx ITransaction)</span><span class="sxs-lookup"><span data-stu-id="622cc-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="622cc-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="622cc-113">int Count()</span></span>                    | <span data-ttu-id="622cc-114">lange Count()</span><span class="sxs-lookup"><span data-stu-id="622cc-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="622cc-115">Vergelijking met [betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="622cc-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="622cc-116">Betrouwbare gelijktijdige wachtrij wordt aangeboden als een alternatief te[betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="622cc-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="622cc-117">Het moet worden gebruikt in gevallen waarbij strikte FIFO-principe ordening niet vereist is als het FIFO-principe vereist een afweging met gelijktijdigheid van taken te garanderen.</span><span class="sxs-lookup"><span data-stu-id="622cc-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="622cc-118">[Betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx) maakt gebruik van vergrendelingen tooenforce FIFO-principe bestellen, met maximaal één transactie tooenqueue toegestaan en maximaal één transactie toodequeue tegelijk toegestaan.</span><span class="sxs-lookup"><span data-stu-id="622cc-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="622cc-119">Ter vergelijking, betrouwbare gelijktijdige wachtrij Hallo beperking rangschikken met deze sjabloon worden en kan een aantal gelijktijdige transacties toointerleave hun in de wachtrij plaatsen en bewerkingen in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="622cc-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="622cc-120">Best-effort ordening is opgegeven, wordt echter nooit relatieve ordening van Hallo van twee waarden in een betrouwbare gelijktijdige wachtrij kan worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="622cc-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="622cc-121">Betrouwbare gelijktijdige wachtrij biedt hogere doorvoer en lagere latentie mogelijk dan [betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx) wanneer er meerdere gelijktijdige transacties enqueues uitvoeren en/of dequeues.</span><span class="sxs-lookup"><span data-stu-id="622cc-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="622cc-122">Een voorbeeld van een gebruiksvoorbeeld voor Hallo ReliableConcurrentQueue is Hallo [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span><span class="sxs-lookup"><span data-stu-id="622cc-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="622cc-123">In dit scenario kan een of meer bericht producenten maken en toevoegen van items toohello wachtrij en een of meer bericht consumenten berichten uit de wachtrij Hallo ophalen en deze te verwerken.</span><span class="sxs-lookup"><span data-stu-id="622cc-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="622cc-124">Meerdere producenten en consumenten kunnen onafhankelijk werken, met behulp van gelijktijdige transacties in volgorde tooprocess Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="622cc-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="622cc-125">Richtlijnen voor het gebruik</span><span class="sxs-lookup"><span data-stu-id="622cc-125">Usage Guidelines</span></span>
* <span data-ttu-id="622cc-126">Hallo-wachtrij wordt verwacht dat items in de wachtrij Hallo Hallo een lage bewaarperiode hebben.</span><span class="sxs-lookup"><span data-stu-id="622cc-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="622cc-127">Dat wil zeggen, zou Hallo items blijven niet in wachtrij Hallo gedurende een lange periode.</span><span class="sxs-lookup"><span data-stu-id="622cc-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="622cc-128">Hallo-wachtrij wordt niet gegarandeerd dat strikte FIFO-principe bestellen.</span><span class="sxs-lookup"><span data-stu-id="622cc-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="622cc-129">Hallo wachtrij heeft een eigen schrijfbewerkingen niet lezen.</span><span class="sxs-lookup"><span data-stu-id="622cc-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="622cc-130">Als een item in de wachtrij binnen een transactie is, is het niet langer zichtbaar tooa dequeuer binnen Hallo dezelfde transactie.</span><span class="sxs-lookup"><span data-stu-id="622cc-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="622cc-131">Dequeues zijn niet van elkaar geïsoleerd.</span><span class="sxs-lookup"><span data-stu-id="622cc-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="622cc-132">Als het item *A* uit wachtrij is geplaatst in transactie *txnA*, ook al *txnA* is geen item worden toegewezen, *A* niet zichtbaar tooa gelijktijdige transactie *txnB*.</span><span class="sxs-lookup"><span data-stu-id="622cc-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="622cc-133">Als *txnA* wordt afgebroken, *A* wordt zichtbaar te*txnB* onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="622cc-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="622cc-134">*TryPeekAsync* gedrag kan worden geïmplementeerd met behulp van een *TryDequeueAsync* en vervolgens Hallo-transactie afgebroken.</span><span class="sxs-lookup"><span data-stu-id="622cc-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="622cc-135">Een voorbeeld hiervan vindt u in Hallo Programming patronen sectie.</span><span class="sxs-lookup"><span data-stu-id="622cc-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="622cc-136">Aantal is niet-transactionele.</span><span class="sxs-lookup"><span data-stu-id="622cc-136">Count is non-transactional.</span></span> <span data-ttu-id="622cc-137">Het kan gebruikte tooget een idee van het aantal elementen in de wachtrij Hallo Hallo maar vertegenwoordigt een punt in tijd en kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="622cc-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="622cc-138">Dure verwerking op Hallo items uit wachtrij geplaatst moeten niet worden uitgevoerd terwijl Hallo transactie actief is, tooavoid langlopende transacties die mogelijk invloed op de prestaties op Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="622cc-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="622cc-139">Codefragmenten</span><span class="sxs-lookup"><span data-stu-id="622cc-139">Code Snippets</span></span>
<span data-ttu-id="622cc-140">Laat het ons Bekijk enkele codefragmenten en de verwachte uitvoer.</span><span class="sxs-lookup"><span data-stu-id="622cc-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="622cc-141">Afhandeling van uitzonderingen wordt in deze sectie genegeerd.</span><span class="sxs-lookup"><span data-stu-id="622cc-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="622cc-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="622cc-142">EnqueueAsync</span></span>
<span data-ttu-id="622cc-143">Hier volgen enkele codefragmenten voor het gebruik van EnqueueAsync gevolgd door de verwachte uitvoer.</span><span class="sxs-lookup"><span data-stu-id="622cc-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="622cc-144">*Voorbeeld 1: Één taak in de wachtrij plaatsen*</span><span class="sxs-lookup"><span data-stu-id="622cc-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="622cc-145">Wordt ervan uitgegaan dat Hallo-taak is voltooid en dat er geen gelijktijdige transacties Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="622cc-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="622cc-146">Hallo-gebruiker kan Hallo wachtrij toocontain Hallo-items in een van volgende orders Hallo verwachten:</span><span class="sxs-lookup"><span data-stu-id="622cc-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="622cc-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="622cc-147">10, 20</span></span>

> <span data-ttu-id="622cc-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="622cc-148">20, 10</span></span>


- <span data-ttu-id="622cc-149">*Voorbeeld 2: Parallelle taak in de wachtrij plaatsen*</span><span class="sxs-lookup"><span data-stu-id="622cc-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="622cc-150">Wordt ervan uitgegaan dat Hallo taken is voltooid, of Hallo taken parallel uitgevoerd en er zijn geen andere gelijktijdige transacties Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="622cc-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="622cc-151">Er is geen Deductie kan worden gemaakt over Hallo volgorde van items in de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="622cc-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="622cc-152">Voor dit codefragment Hallo items mogelijk weergegeven in een van de Hallo 4!</span><span class="sxs-lookup"><span data-stu-id="622cc-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="622cc-153">mogelijke volgorden.</span><span class="sxs-lookup"><span data-stu-id="622cc-153">possible orderings.</span></span>  <span data-ttu-id="622cc-154">Hallo wachtrij probeert tookeep Hallo items in volgorde van Hallo oorspronkelijke (in wachtrij gezet), maar kan niet geforceerd tooreorder ze vervaldatum tooconcurrent operations of fouten.</span><span class="sxs-lookup"><span data-stu-id="622cc-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="622cc-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="622cc-155">DequeueAsync</span></span>
<span data-ttu-id="622cc-156">Hier volgen enkele codefragmenten voor het gebruik van TryDequeueAsync gevolgd door Hallo verwacht uitvoer.</span><span class="sxs-lookup"><span data-stu-id="622cc-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="622cc-157">Stel dat die wachtrij Hallo al is gevuld met de volgende items in de wachtrij Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="622cc-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="622cc-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="622cc-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="622cc-159">*Voorbeeld 1: Één taak in wachtrij*</span><span class="sxs-lookup"><span data-stu-id="622cc-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="622cc-160">Wordt ervan uitgegaan dat Hallo-taak is voltooid en dat er geen gelijktijdige transacties Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="622cc-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="622cc-161">Omdat er geen Deductie kan worden gemaakt over Hallo volgorde van items in de wachtrij Hallo hello, alle drie Hallo items kunnen worden uit wachtrij geplaatst, in willekeurige volgorde.</span><span class="sxs-lookup"><span data-stu-id="622cc-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="622cc-162">Hallo wachtrij probeert tookeep Hallo items in volgorde van Hallo oorspronkelijke (in wachtrij gezet), maar kan niet geforceerd tooreorder ze vervaldatum tooconcurrent operations of fouten.</span><span class="sxs-lookup"><span data-stu-id="622cc-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="622cc-163">*Voorbeeld 2: Taak Parallel uit de wachtrij halen*</span><span class="sxs-lookup"><span data-stu-id="622cc-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="622cc-164">Wordt ervan uitgegaan dat Hallo taken is voltooid, of Hallo taken parallel uitgevoerd en er zijn geen andere gelijktijdige transacties Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="622cc-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="622cc-165">Omdat er geen Deductie kan worden gemaakt over Hallo volgorde van items in de wachtrij Hallo hello, lijsten Hallo *dequeue1* en *dequeue2* wordt elke twee items, in willekeurige volgorde bevatten.</span><span class="sxs-lookup"><span data-stu-id="622cc-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="622cc-166">Hallo hetzelfde item wordt *niet* in beide lijsten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="622cc-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="622cc-167">Daarom als dequeue1 *10*, *30*, en vervolgens dequeue2 zou hebben *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="622cc-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="622cc-168">*Voorbeeld 3: Wachtrij ordening met transactie afgebroken*</span><span class="sxs-lookup"><span data-stu-id="622cc-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="622cc-169">Een transactie met onderweg wordt afgebroken dequeues puts Hallo items terug op Hallo hoofd van Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="622cc-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="622cc-170">Hallo volgorde waarin Hallo-items worden geplaatst terug op Hallo hoofd van Hallo wachtrij kan niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="622cc-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="622cc-171">Laat het ons Hallo code volgende bekijken:</span><span class="sxs-lookup"><span data-stu-id="622cc-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="622cc-172">Stel dat Hallo items uit de wachtrij in Hallo volgorde zijn geplaatst:</span><span class="sxs-lookup"><span data-stu-id="622cc-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="622cc-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="622cc-173">10, 20</span></span>

<span data-ttu-id="622cc-174">We Hallo transactie afgebroken, Hallo items zou worden toegevoegd wanneer back toohello hoofd van Hallo wachtrij in een Hallo orders te volgen:</span><span class="sxs-lookup"><span data-stu-id="622cc-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="622cc-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="622cc-175">10, 20</span></span>

> <span data-ttu-id="622cc-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="622cc-176">20, 10</span></span>

<span data-ttu-id="622cc-177">Hallo geldt voor alle gevallen waarbij Hallo transactie niet met succes is *doorgevoerd*.</span><span class="sxs-lookup"><span data-stu-id="622cc-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="622cc-178">Patronen programmering</span><span class="sxs-lookup"><span data-stu-id="622cc-178">Programming Patterns</span></span>
<span data-ttu-id="622cc-179">In deze sectie laat het ons kijken enkele programmering patronen die mogelijk nuttig zijn bij het gebruik van ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="622cc-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="622cc-180">Batch Dequeues</span><span class="sxs-lookup"><span data-stu-id="622cc-180">Batch Dequeues</span></span>
<span data-ttu-id="622cc-181">Een aanbevolen programming patroon is voor Hallo consumer taak toobatch de dequeues in plaats van een wachtrij op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="622cc-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="622cc-182">Hallo-gebruiker kan toothrottle vertragingen tussen elke batch of Hallo batchgrootte kiezen.</span><span class="sxs-lookup"><span data-stu-id="622cc-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="622cc-183">Hallo bevat volgende codefragment dit programmeermodel.</span><span class="sxs-lookup"><span data-stu-id="622cc-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="622cc-184">Houd er rekening mee dat in dit voorbeeld Hallo verwerken is voltooid nadat Hallo transactie doorgevoerd is, dus als een fout toooccur tijdens de verwerking, hello onverwerkte items zullen verloren zonder dat is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="622cc-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="622cc-185">U kunt ook Hallo verwerking kan worden uitgevoerd binnen bereik van de transactie hello, maar dit kan een negatieve invloed hebben op prestaties en vereist dat de verwerking van Hallo items al verwerkt.</span><span class="sxs-lookup"><span data-stu-id="622cc-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

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

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="622cc-186">Verwerking van Best-Effort op basis van meldingen</span><span class="sxs-lookup"><span data-stu-id="622cc-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="622cc-187">Hallo Count-API maakt gebruik van een ander interessant programming patroon.</span><span class="sxs-lookup"><span data-stu-id="622cc-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="622cc-188">Hier kunnen we best-effort op basis van meldingen verwerking voor Hallo wachtrij implementeren.</span><span class="sxs-lookup"><span data-stu-id="622cc-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="622cc-189">Hallo wachtrij aantal kan worden gebruikt toothrottle een wachtrij plaatsen of een taak wachtrij halen.</span><span class="sxs-lookup"><span data-stu-id="622cc-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="622cc-190">Houd er rekening mee dat zoals in het vorige voorbeeld Hallo, aangezien Hallo verwerking vindt plaats buiten Hallo-transactie niet-verwerkte items mogelijk verloren als er een fout optreedt tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="622cc-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

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

### <a name="best-effort-drain"></a><span data-ttu-id="622cc-191">Best-Effort leegmaken</span><span class="sxs-lookup"><span data-stu-id="622cc-191">Best-Effort Drain</span></span>
<span data-ttu-id="622cc-192">Leegmaken van Hallo wachtrij kan niet worden gegarandeerd vanwege toohello gelijktijdige aard van Hallo gegevensstructuur.</span><span class="sxs-lookup"><span data-stu-id="622cc-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="622cc-193">Het is mogelijk dat, zelfs als er geen gebruiker bewerkingen op Hallo wachtrij onderweg, een bepaalde oproep tooTryDequeueAsync kan niet als resultaat een item die eerder in de wachtrij en doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="622cc-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="622cc-194">Hallo in wachtrij gezet item te is gegarandeerd*uiteindelijk* zichtbaar toodequeue worden echter zonder een out-of-band-communicatiemechanisme een onafhankelijke consumer kan niet weet die Hallo wachtrij heeft bereikt een stabiele status zelfs als alle producenten zijn gestopt en er zijn geen nieuwe wachtrij plaatsen bewerkingen zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="622cc-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="622cc-195">Hallo leegmaken bewerking is dus best-effort zoals hieronder wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="622cc-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="622cc-196">Hallo gebruiker moet alle verdere producenten en consumenten taken stoppen en wachten op een onderweg transacties toocommit of afbreken voordat u probeert toodrain Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="622cc-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="622cc-197">Als Hallo gebruiker Hallo verwacht aantal items in de wachtrij hello kent, kunnen ze een melding die geeft aan dat alle items uit wachtrij hebben is geplaatst instellen.</span><span class="sxs-lookup"><span data-stu-id="622cc-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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

### <a name="peek"></a><span data-ttu-id="622cc-198">Piek</span><span class="sxs-lookup"><span data-stu-id="622cc-198">Peek</span></span>
<span data-ttu-id="622cc-199">ReliableConcurrentQueue biedt geen Hallo *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="622cc-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="622cc-200">Gebruikers kunnen krijgen Hallo peek semantische met behulp van een *TryDequeueAsync* en vervolgens Hallo-transactie afgebroken.</span><span class="sxs-lookup"><span data-stu-id="622cc-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="622cc-201">In dit voorbeeld dequeues worden verwerkt alleen als het Hallo-item groter is dan *10*.</span><span class="sxs-lookup"><span data-stu-id="622cc-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

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

## <a name="must-read"></a><span data-ttu-id="622cc-202">Moet lezen</span><span class="sxs-lookup"><span data-stu-id="622cc-202">Must Read</span></span>
* [<span data-ttu-id="622cc-203">Snel starten Reliable Services</span><span class="sxs-lookup"><span data-stu-id="622cc-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="622cc-204">Werken met betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="622cc-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="622cc-205">Betrouwbare Services meldingen</span><span class="sxs-lookup"><span data-stu-id="622cc-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="622cc-206">Reliable Services Backup and Restore (herstel na noodgevallen)</span><span class="sxs-lookup"><span data-stu-id="622cc-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="622cc-207">Configuratie van betrouwbare status Manager</span><span class="sxs-lookup"><span data-stu-id="622cc-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="622cc-208">Aan de slag met Service Fabric Web API-Services</span><span class="sxs-lookup"><span data-stu-id="622cc-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="622cc-209">Geavanceerd gebruik Hallo betrouwbare Services Programming Model</span><span class="sxs-lookup"><span data-stu-id="622cc-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="622cc-210">Referentie voor ontwikkelaars voor betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="622cc-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
