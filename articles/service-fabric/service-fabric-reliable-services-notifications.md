---
title: aaaReliable Services meldingen | Microsoft Docs
description: Conceptuele documentatie voor Service Fabric Reliable Services meldingen
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="797ac-103">Betrouwbare Services meldingen</span><span class="sxs-lookup"><span data-stu-id="797ac-103">Reliable Services notifications</span></span>
<span data-ttu-id="797ac-104">Kennisgevingen kunnen clients tootrack Hallo wijzigingen die tooan-object dat ze geïnteresseerd bent in worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="797ac-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="797ac-105">Twee soorten objecten ondersteunen meldingen: *betrouwbare statusbeheer* en *betrouwbare woordenlijst*.</span><span class="sxs-lookup"><span data-stu-id="797ac-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="797ac-106">Er zijn veelvoorkomende redenen voor het gebruik van meldingen:</span><span class="sxs-lookup"><span data-stu-id="797ac-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="797ac-107">Gebouw gematerialiseerd weergaven, zoals secundaire indexen of gefilterde weergaven van Hallo replicastatus geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="797ac-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="797ac-108">Een voorbeeld is een gesorteerde index van alle sleutels in betrouwbare woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="797ac-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="797ac-109">Verzenden bewakingsgegevens, zoals het aantal gebruikers die zijn toegevoegd in Hallo afgelopen uur Hallo.</span><span class="sxs-lookup"><span data-stu-id="797ac-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="797ac-110">Meldingen worden gestart als onderdeel van het toepassen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="797ac-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="797ac-111">Vanwege die worden meldingen zo snel mogelijk en synchrone gebeurtenissen mag niet zijn dure bewerkingen behandeld.</span><span class="sxs-lookup"><span data-stu-id="797ac-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="797ac-112">Betrouwbaar status Manager-meldingen</span><span class="sxs-lookup"><span data-stu-id="797ac-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="797ac-113">Betrouwbaar status Manager biedt meldingen voor Hallo gebeurtenissen te volgen:</span><span class="sxs-lookup"><span data-stu-id="797ac-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="797ac-114">Transactie</span><span class="sxs-lookup"><span data-stu-id="797ac-114">Transaction</span></span>
  * <span data-ttu-id="797ac-115">Doorvoeren</span><span class="sxs-lookup"><span data-stu-id="797ac-115">Commit</span></span>
* <span data-ttu-id="797ac-116">Status manager</span><span class="sxs-lookup"><span data-stu-id="797ac-116">State manager</span></span>
  * <span data-ttu-id="797ac-117">Opnieuw samenstellen</span><span class="sxs-lookup"><span data-stu-id="797ac-117">Rebuild</span></span>
  * <span data-ttu-id="797ac-118">Toevoeging van een betrouwbare status</span><span class="sxs-lookup"><span data-stu-id="797ac-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="797ac-119">Verwijderen van een betrouwbare status</span><span class="sxs-lookup"><span data-stu-id="797ac-119">Removal of a reliable state</span></span>

<span data-ttu-id="797ac-120">Statusbeheer voor betrouwbaar houdt Hallo huidige inflight transacties.</span><span class="sxs-lookup"><span data-stu-id="797ac-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="797ac-121">de enige wijziging Hallo in transactiestatus dat ervoor zorgt een melding toobe gestart dat is een transactie wordt doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="797ac-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="797ac-122">Statusbeheer voor betrouwbaar onderhoudt een verzameling van betrouwbare statussen zoals betrouwbare woordenlijst en betrouwbare wachtrij.</span><span class="sxs-lookup"><span data-stu-id="797ac-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="797ac-123">Statusbeheer voor betrouwbaar meldingen wordt geactiveerd wanneer deze verzameling wordt gewijzigd: een betrouwbare status wordt toegevoegd of verwijderd of de volledige verzameling Hallo opnieuw wordt opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="797ac-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="797ac-124">Hallo betrouwbare status Manager-verzameling is opnieuw opgebouwd in drie gevallen:</span><span class="sxs-lookup"><span data-stu-id="797ac-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="797ac-125">Herstel: Wanneer een replica wordt gestart, het herstelt de vorige status van Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="797ac-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="797ac-126">Hallo na herstel gebruikt **NotifyStateManagerChangedEventArgs** toofire een gebeurtenis die Hallo set van herstelde betrouwbare statussen bevat.</span><span class="sxs-lookup"><span data-stu-id="797ac-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="797ac-127">Volledige kopiëren: voordat u een replica kunt deelnemen aan configuratieset hello, hieraan toobe gebouwd.</span><span class="sxs-lookup"><span data-stu-id="797ac-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="797ac-128">Soms moet hiervoor een volledige kopie van de status van het betrouwbare statusbeheer van Hallo primaire replica toobe toegepaste toohello niet-actieve secundaire replica.</span><span class="sxs-lookup"><span data-stu-id="797ac-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="797ac-129">Statusbeheer voor betrouwbaar op Hallo secundaire replica gebruikt **NotifyStateManagerChangedEventArgs** toofire een gebeurtenis dat het aantal betrouwbare statussen die die is verkregen van de primaire replica Hallo Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="797ac-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="797ac-130">Herstel: In scenario's voor herstel na noodgevallen, Hallo replicastatus kan worden hersteld vanuit een back-up via **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="797ac-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="797ac-131">In dergelijke gevallen betrouwbare status Manager op de primaire replica Hallo gebruikt **NotifyStateManagerChangedEventArgs** toofire een gebeurtenis dat het aantal betrouwbare statussen die deze vanuit een back-up Hallo teruggezet Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="797ac-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="797ac-132">tooregister voor transactie meldingen en/of de status manager-meldingen, moet u tooregister Hello **TransactionChanged** of **StateManagerChanged** gebeurtenissen op betrouwbare status Manager.</span><span class="sxs-lookup"><span data-stu-id="797ac-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="797ac-133">Een algemene plaats tooregister met deze gebeurtenis-handlers Hallo constructor van uw stateful service is.</span><span class="sxs-lookup"><span data-stu-id="797ac-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="797ac-134">Wanneer u op Hallo constructor registreert, u een melding die wordt veroorzaakt door een wijziging tijdens de levensduur van hello niet naar hun **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="797ac-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="797ac-135">Hallo **TransactionChanged** maakt gebruik van gebeurtenis-handler **NotifyTransactionChangedEventArgs** tooprovide details over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="797ac-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="797ac-136">Deze eigenschap Hallo-action bevat (bijvoorbeeld **NotifyTransactionChangedAction.Commit**) die aangeeft Hallo type wijziging.</span><span class="sxs-lookup"><span data-stu-id="797ac-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="797ac-137">Het bevat ook Hallo transactie-eigenschap waarmee een verwijzing toohello transactie die gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="797ac-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="797ac-138">Vandaag de dag **TransactionChanged** gebeurtenissen worden gegenereerd, alleen als Hallo transactie doorgevoerd is.</span><span class="sxs-lookup"><span data-stu-id="797ac-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="797ac-139">Hallo actie is vervolgens gelijk te**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="797ac-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="797ac-140">Maar in toekomstige hello, gebeurtenissen voor andere soorten statuswijzigingen transactie kunnen worden verhoogd.</span><span class="sxs-lookup"><span data-stu-id="797ac-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="797ac-141">U wordt aangeraden Hallo actie controleren en verwerking van Hallo gebeurtenis alleen als het is een die u verwacht.</span><span class="sxs-lookup"><span data-stu-id="797ac-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="797ac-142">Hieronder volgt een voorbeeld **TransactionChanged** gebeurtenis-handler.</span><span class="sxs-lookup"><span data-stu-id="797ac-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="797ac-143">Hallo **StateManagerChanged** maakt gebruik van gebeurtenis-handler **NotifyStateManagerChangedEventArgs** tooprovide details over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="797ac-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="797ac-144">**NotifyStateManagerChangedEventArgs** twee subklassen: **NotifyStateManagerRebuildEventArgs** en **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="797ac-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="797ac-145">U Hallo actie eigenschap in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello juiste subklasse:</span><span class="sxs-lookup"><span data-stu-id="797ac-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="797ac-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="797ac-147">**NotifyStateManagerChangedAction.Add** en **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="797ac-148">Hieronder volgt een voorbeeld **StateManagerChanged** meldings-handler.</span><span class="sxs-lookup"><span data-stu-id="797ac-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="797ac-149">Betrouwbare woordenlijst meldingen</span><span class="sxs-lookup"><span data-stu-id="797ac-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="797ac-150">Betrouwbare woordenlijst biedt meldingen voor Hallo gebeurtenissen te volgen:</span><span class="sxs-lookup"><span data-stu-id="797ac-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="797ac-151">Opnieuw maken: Aangeroepen wanneer **ReliableDictionary** heeft de status is hersteld van een herstelde of gekopieerde lokale staat of de back-up.</span><span class="sxs-lookup"><span data-stu-id="797ac-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="797ac-152">Wissen: Aangeroepen wanneer Hallo status van **ReliableDictionary** is gewist via Hallo **ClearAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="797ac-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="797ac-153">Toevoegen: Wordt aangeroepen wanneer een item is toegevoegd te**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="797ac-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="797ac-154">Update: Wordt aangeroepen wanneer een item in **IReliableDictionary** is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="797ac-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="797ac-155">Verwijderen: Wordt aangeroepen wanneer een item in **IReliableDictionary** is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="797ac-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="797ac-156">tooget betrouwbare woordenlijst meldingen, moet u tooregister Hello **DictionaryChanged** gebeurtenis-handler op **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="797ac-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="797ac-157">Een algemene plaats tooregister met deze gebeurtenis-handlers wordt Hallo **ReliableStateManager.StateManagerChanged** melding toevoegen.</span><span class="sxs-lookup"><span data-stu-id="797ac-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="797ac-158">Wanneer u registreert **IReliableDictionary** te wordt toegevoegd**IReliableStateManager** zorgt ervoor dat u meldingen niet naar hun.</span><span class="sxs-lookup"><span data-stu-id="797ac-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="797ac-159">**ProcessStateManagerSingleEntityNotification** is Hallo voorbeeldmethode die voorgaande Hallo **OnStateManagerChangedHandler** voorbeeld aanroepen.</span><span class="sxs-lookup"><span data-stu-id="797ac-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="797ac-160">Hallo voorafgaande code ingesteld Hallo **IReliableNotificationAsyncCallback** interface, samen met **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="797ac-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="797ac-161">Omdat **NotifyDictionaryRebuildEventArgs** bevat een **IAsyncEnumerable** interface--moeten toobe asynchroon--opgesomd meldingen opnieuw worden gestart via  **RebuildNotificationAsyncCallback** in plaats van **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="797ac-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="797ac-162">In Hallo voorafgaand aan code, als onderdeel van verwerking Hallo rebuild melding onderhouden eerste Hallo geaggregeerde status is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="797ac-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="797ac-163">Omdat Hallo betrouwbare verzameling wordt opnieuw opgebouwd met een nieuwe status, zijn alle eerdere meldingen niet relevant.</span><span class="sxs-lookup"><span data-stu-id="797ac-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="797ac-164">Hallo **DictionaryChanged** maakt gebruik van gebeurtenis-handler **NotifyDictionaryChangedEventArgs** tooprovide details over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="797ac-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="797ac-165">**NotifyDictionaryChangedEventArgs** vijf subklassen.</span><span class="sxs-lookup"><span data-stu-id="797ac-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="797ac-166">Hallo actie eigenschap gebruiken in een **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello juiste subklasse:</span><span class="sxs-lookup"><span data-stu-id="797ac-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="797ac-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="797ac-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="797ac-169">**NotifyDictionaryChangedAction.Add** en **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="797ac-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="797ac-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="797ac-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="797ac-172">Aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="797ac-172">Recommendations</span></span>
* <span data-ttu-id="797ac-173">*Voer* meldingsgebeurtenissen zo snel mogelijk te voltooien.</span><span class="sxs-lookup"><span data-stu-id="797ac-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="797ac-174">*Geen* dure bewerkingen (bijvoorbeeld i/o-bewerkingen) worden uitgevoerd als onderdeel van synchrone gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="797ac-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="797ac-175">*Voer* Hallo actietype controleren voordat u Hallo gebeurtenis verwerkt.</span><span class="sxs-lookup"><span data-stu-id="797ac-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="797ac-176">Nieuwe actietypen kunnen in toekomstige Hallo worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="797ac-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="797ac-177">Hier volgen enkele dingen tookeep rekening:</span><span class="sxs-lookup"><span data-stu-id="797ac-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="797ac-178">Meldingen worden gestart als onderdeel van Hallo uitvoering van een bewerking.</span><span class="sxs-lookup"><span data-stu-id="797ac-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="797ac-179">Bijvoorbeeld, een melding terugzetten als laatste stap van een herstelbewerking Hallo gestart.</span><span class="sxs-lookup"><span data-stu-id="797ac-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="797ac-180">Een herstelpunt wordt niet voltooien totdat een meldingsgebeurtenis Hallo is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="797ac-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="797ac-181">Omdat meldingen worden gestart als onderdeel van Hallo bewerkingen zijn toegepast, wordt door clients alleen meldingen voor lokaal doorgevoerd bewerkingen zien.</span><span class="sxs-lookup"><span data-stu-id="797ac-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="797ac-182">En omdat operations gegarandeerd alleen toobe lokaal toegewezen (met andere woorden, aangemelde) ze kunnen wel of kan niet ongedaan in toekomstige Hallo worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="797ac-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="797ac-183">Op Hallo opnieuw pad, wordt één melding geactiveerd voor elke toegepaste bewerking.</span><span class="sxs-lookup"><span data-stu-id="797ac-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="797ac-184">Dit betekent dat als transactie T1 Create(X) Delete(X) en Create(X) bevat, u een melding voor Hallo maken van X, één voor Hallo verwijdering en één voor het maken van Hallo opnieuw in die volgorde krijgt.</span><span class="sxs-lookup"><span data-stu-id="797ac-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="797ac-185">Voor transacties die meerdere bewerkingen bevatten, worden bewerkingen in Hallo volgorde waarin ze zijn ontvangen op de primaire replica Hallo van Hallo gebruiker toegepast.</span><span class="sxs-lookup"><span data-stu-id="797ac-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="797ac-186">Als onderdeel van de verwerking van false voortgang bepaalde bewerkingen mogelijk ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="797ac-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="797ac-187">Meldingen worden gegenereerd voor deze bewerkingen ongedaan maken, rolling Hallo status van Hallo replica back tooa stabiel punt.</span><span class="sxs-lookup"><span data-stu-id="797ac-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="797ac-188">Een belangrijk verschil van meldingen voor ongedaan maken is dat de gebeurtenissen die dubbele sleutels hebben worden geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="797ac-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="797ac-189">Bijvoorbeeld, als T1 transactie wordt ongedaan wordt gemaakt, ziet u een tooDelete(X) één melding.</span><span class="sxs-lookup"><span data-stu-id="797ac-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="797ac-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="797ac-190">Next steps</span></span>
* [<span data-ttu-id="797ac-191">Betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="797ac-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="797ac-192">Betrouwbare Services snel starten</span><span class="sxs-lookup"><span data-stu-id="797ac-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="797ac-193">Betrouwbare Services back-up en herstel (herstel na noodgevallen)</span><span class="sxs-lookup"><span data-stu-id="797ac-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="797ac-194">Referentie voor ontwikkelaars voor betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="797ac-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

