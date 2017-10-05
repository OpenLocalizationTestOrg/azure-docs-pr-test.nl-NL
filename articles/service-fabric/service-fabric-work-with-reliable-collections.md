---
title: Werken met betrouwbare collecties | Microsoft Docs
description: Meer informatie over de aanbevolen procedures voor het werken met betrouwbare verzamelingen.
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: f53f13e4fb83b1cd370ec673e86e5311cd93055f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="6bca9-103">Werken met betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="6bca9-103">Working with Reliable Collections</span></span>
<span data-ttu-id="6bca9-104">Service Fabric biedt een stateful programmeermodel beschikbaar voor .NET-ontwikkelaars via betrouwbare verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span></span> <span data-ttu-id="6bca9-105">In het bijzonder biedt Service Fabric betrouwbare woordenlijst en betrouwbare wachtrij klassen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="6bca9-106">Wanneer u deze klassen gebruikt, wordt uw status gepartitioneerd (voor schaalbaarheid), gerepliceerd (voor beschikbaarheid) en transactionele binnen een partitie (voor ACID-semantiek).</span><span class="sxs-lookup"><span data-stu-id="6bca9-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="6bca9-107">Laten we kijken naar het standaardgebruik van een betrouwbare dictionary-object en zien welke ervan daadwerkelijk doen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record to log & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record to log & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="6bca9-108">Alle bewerkingen op betrouwbare dictionary-objecten (met uitzondering van ClearAsync die niet ongedaan maken), vereisen een ITransaction-object.</span><span class="sxs-lookup"><span data-stu-id="6bca9-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="6bca9-109">Dit object is gekoppeld aan een en alle wijzigingen die u probeert te maken aan de woordenlijst van een betrouwbare en/of betrouwbare objecten binnen één partitie in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="6bca9-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="6bca9-110">Verkrijgen van een ITransaction object door het aanroepen van de partitie de StateManager van CreateTransaction methode.</span><span class="sxs-lookup"><span data-stu-id="6bca9-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="6bca9-111">In de bovenstaande code wordt de ITransaction-object doorgegeven aan een betrouwbare woordenlijst AddAsync methode.</span><span class="sxs-lookup"><span data-stu-id="6bca9-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="6bca9-112">Intern woordenlijst methoden die een sleutel accepteert maken gebruik van een lezer/schrijver vergrendeling die zijn gekoppeld aan de sleutel.</span><span class="sxs-lookup"><span data-stu-id="6bca9-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span></span> <span data-ttu-id="6bca9-113">Als de methode van de sleutel waarde wijzigt, gaat de methode een schrijfvergrendeling voor de sleutel en als de methode is alleen wordt gelezen van de waarde van de sleutel, wordt een leesvergrendeling genomen voor de sleutel.</span><span class="sxs-lookup"><span data-stu-id="6bca9-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span></span> <span data-ttu-id="6bca9-114">Aangezien AddAsync waarde van de sleutel op de nieuwe, doorgegeven waarde wijzigt, wordt de sleutel-/ schrijfvergrendeling genomen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span></span> <span data-ttu-id="6bca9-115">Dus 2 (of hoger) threads probeert toe te voegen van waarden met dezelfde sleutel op hetzelfde moment, één thread wordt de schrijfvergrendeling verkrijgen als de andere threads wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span></span> <span data-ttu-id="6bca9-116">Standaard methoden blokkeren voor maximaal 4 seconden de vergrendeling; de methoden genereren na 4 seconden een TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="6bca9-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span></span> <span data-ttu-id="6bca9-117">Methode overloads bestaan zodat u een expliciete time-outwaarde doorgeven als u liever.</span><span class="sxs-lookup"><span data-stu-id="6bca9-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="6bca9-118">Meestal kunt u uw code schrijven om te reageren op een TimeoutException door het afvangen en u de hele bewerking (zoals weergegeven in de bovenstaande code).</span><span class="sxs-lookup"><span data-stu-id="6bca9-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span></span> <span data-ttu-id="6bca9-119">In mijn eenvoudige code alleen gebeld Task.Delay 100 milliseconden elke keer dat wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="6bca9-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="6bca9-120">Maar in werkelijkheid is het mogelijk dat beter met een soort exponentiële back-uit vertraging in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="6bca9-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="6bca9-121">Zodra de vergrendeling wordt verkregen, voegt AddAsync de sleutel en waarde objectverwijzingen naar een interne tijdelijke woordenlijst is gekoppeld aan de ITransaction-object.</span><span class="sxs-lookup"><span data-stu-id="6bca9-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span></span> <span data-ttu-id="6bca9-122">Dit wordt gedaan om te lezen-your-eigenaar-schrijven semantiek bieden.</span><span class="sxs-lookup"><span data-stu-id="6bca9-122">This is done to provide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="6bca9-123">Dat wil zeggen, na het aanroepen van AddAsync een aanroep van TryGetValueAsync (met hetzelfde object ITransaction) hoger de waarde als resultaat zelfs als u zich nog niet de transactie verplicht hebt.</span><span class="sxs-lookup"><span data-stu-id="6bca9-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span></span> <span data-ttu-id="6bca9-124">Vervolgens AddAsync serialiseert uw sleutel en waarde objecten naar byte matrices en voegt deze byte-matrices met een logboekbestand op het lokale knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6bca9-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span></span> <span data-ttu-id="6bca9-125">AddAsync verzendt ten slotte de byte-matrices naar de secundaire replica's zodat ze dezelfde sleutel/waarde-gegevens hebben.</span><span class="sxs-lookup"><span data-stu-id="6bca9-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span></span> <span data-ttu-id="6bca9-126">Hoewel de sleutel/waarde-informatie is geschreven naar een logboekbestand, de informatie wordt niet beschouwd als onderdeel van het woordenboek totdat de transactie die ze zijn gekoppeld aan is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="6bca9-127">In de code voert de aanroep van CommitAsync alle bewerkingen van de transactie.</span><span class="sxs-lookup"><span data-stu-id="6bca9-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span></span> <span data-ttu-id="6bca9-128">In het bijzonder commit informatie toegevoegd aan het logboekbestand op het lokale knooppunt en verstuurt ook de commit-record op de secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="6bca9-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span></span> <span data-ttu-id="6bca9-129">Zodra een quorum (meerderheid) van de replica's al heeft geantwoord, worden alle gegevenswijzigingen als permanente beschouwd en alle sleutels die zijn gemanipuleerd via de ITransaction-object gekoppeld vergrendelingen zijn vrijgegeven zodat andere threads/transacties dezelfde sleutels kunt bewerken en hun waarden.</span><span class="sxs-lookup"><span data-stu-id="6bca9-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span></span>

<span data-ttu-id="6bca9-130">Als CommitAsync (meestal als gevolg van een uitzondering wordt veroorzaakt) niet wordt aangeroepen, haalt de ITransaction-object verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span></span> <span data-ttu-id="6bca9-131">Bij de buitengebruikstelling van een niet-doorgevoerde ITransaction-object, Service Fabric afbreken informatie toegevoegd aan het lokale knooppunt logboekbestand en hoeft u niets worden verzonden naar een van de secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="6bca9-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span></span> <span data-ttu-id="6bca9-132">En vervolgens alle vergrendelingen die zijn gekoppeld aan de sleutels die zijn gemanipuleerd via de transactie zijn vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="6bca9-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span></span>

## <a name="common-pitfalls-and-how-to-avoid-them"></a><span data-ttu-id="6bca9-133">Veelvoorkomende valkuilen en hoe te vermijden</span><span class="sxs-lookup"><span data-stu-id="6bca9-133">Common pitfalls and how to avoid them</span></span>
<span data-ttu-id="6bca9-134">Nu dat u hoe de betrouwbare verzamelingen intern werken begrijpt, gaan we verdiepen in enkele algemene misbruik van deze.</span><span class="sxs-lookup"><span data-stu-id="6bca9-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="6bca9-135">Zie de volgende code:</span><span class="sxs-lookup"><span data-stu-id="6bca9-135">See the code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes the name/user, logs the bytes,
   // & sends the bytes to the secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // The line below updates the property’s value in memory only; the
   // new value is NOT serialized, logged, & sent to secondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="6bca9-136">Als u werkt met een normale .NET-woordenlijst, kunt u een sleutel/waarde toevoegen aan de woordenlijst en wijzig de waarde van een eigenschap (zoals LastLogin).</span><span class="sxs-lookup"><span data-stu-id="6bca9-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span></span> <span data-ttu-id="6bca9-137">Echter, deze code werkt niet correct met een betrouwbare woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="6bca9-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="6bca9-138">Onthouden van de eerdere discussie de aanroep van AddAsync serialiseert van de sleutel/waarde-objecten voor matrices byte en slaat vervolgens de matrices met een lokaal bestand en verzendt ze ook naar de secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="6bca9-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span></span> <span data-ttu-id="6bca9-139">Als u later een eigenschap wijzigt, Hiermee kunt u de waarde van de eigenschap in het geheugen. Dit heeft geen gevolgen voor het lokale bestand of de gegevens die worden verzonden met de replica's.</span><span class="sxs-lookup"><span data-stu-id="6bca9-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span></span> <span data-ttu-id="6bca9-140">Als het proces vastloopt, is wat is er in het geheugen weggegooid.</span><span class="sxs-lookup"><span data-stu-id="6bca9-140">If the process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="6bca9-141">Wanneer een nieuw proces wordt gestart of als een andere replica primaire wordt, is de waarde van de oude eigenschap wat beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="6bca9-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span></span>

<span data-ttu-id="6bca9-142">Ik kan geen stress genoeg hoe eenvoudig dat het is om te maken van het soort fout hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6bca9-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span></span> <span data-ttu-id="6bca9-143">En u alleen leert over de fout als of wanneer dat het proces wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="6bca9-143">And, you will only learn about the mistake if/when the process goes down.</span></span> <span data-ttu-id="6bca9-144">De juiste manier om de code te schrijven is gewoon omkeren van de twee regels:</span><span class="sxs-lookup"><span data-stu-id="6bca9-144">The correct way to write the code is simply to reverse the two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="6bca9-145">Hier volgt een voorbeeld weergegeven van een algemene fout:</span><span class="sxs-lookup"><span data-stu-id="6bca9-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (user.HasValue) {
      // The line below updates the property’s value in memory only; the
      // new value is NOT serialized, logged, & sent to secondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="6bca9-146">Opnieuw met normale .NET woordenboeken, de bovenstaande code werkt goed samen en is een algemene patroon: de ontwikkelaar een sleutel gebruikt om een waarde te zoeken.</span><span class="sxs-lookup"><span data-stu-id="6bca9-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span></span> <span data-ttu-id="6bca9-147">Als de waarde bestaat, verandert de ontwikkelaar van de waarde van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6bca9-147">If the value exists, the developer changes a property’s value.</span></span> <span data-ttu-id="6bca9-148">Met betrouwbare verzamelingen echter vertoont deze code hetzelfde probleem al besproken: **moet u een object niet wijzigen nadat u deze aan een betrouwbare verzameling hebt gegeven.**</span><span class="sxs-lookup"><span data-stu-id="6bca9-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span></span>

<span data-ttu-id="6bca9-149">De juiste manier om een waarde in een betrouwbare verzameling bijwerken is het een verwijzing naar de bestaande waarde ophalen en houd rekening met het object waarnaar wordt verwezen door deze verwijzing onveranderbaar.</span><span class="sxs-lookup"><span data-stu-id="6bca9-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span></span> <span data-ttu-id="6bca9-150">Vervolgens maakt u een nieuw object dat een exacte kopie van het originele object.</span><span class="sxs-lookup"><span data-stu-id="6bca9-150">Then, create a new object which is an exact copy of the original object.</span></span> <span data-ttu-id="6bca9-151">U kunt nu de status van dit nieuwe object wijzigen en schrijven van het nieuwe object in de verzameling zodat deze wordt geserialiseerd naar byte-matrices toegevoegd aan het lokale bestand en verzonden naar de replica's.</span><span class="sxs-lookup"><span data-stu-id="6bca9-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span></span> <span data-ttu-id="6bca9-152">Nadat de wijzigingen zijn doorgevoerd, hebben de objecten in het geheugen, het lokale bestand en alle replica's dezelfde exact overeen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span></span> <span data-ttu-id="6bca9-153">Goede is.</span><span class="sxs-lookup"><span data-stu-id="6bca9-153">All is good!</span></span>

<span data-ttu-id="6bca9-154">De onderstaande code ziet u de juiste manier om een waarde in een betrouwbare verzameling te werken:</span><span class="sxs-lookup"><span data-stu-id="6bca9-154">The code below shows the correct way to update a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with the same state as the current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In the new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update the key’s value to the updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-to-prevent-programmer-error"></a><span data-ttu-id="6bca9-155">Niet-wijzigbaar gegevenstypen om te voorkomen dat programmeurs fout definiëren</span><span class="sxs-lookup"><span data-stu-id="6bca9-155">Define immutable data types to prevent programmer error</span></span>
<span data-ttu-id="6bca9-156">Willen we graag de compiler fouten rapporteren in het ideale geval wanneer u per ongeluk code die de status van een object dat u moet rekening houden met niet-wijzigbaar mutates produceren.</span><span class="sxs-lookup"><span data-stu-id="6bca9-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span></span> <span data-ttu-id="6bca9-157">Maar de C# compiler heeft niet de mogelijkheid om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-157">But, the C# compiler does not have the ability to do this.</span></span> <span data-ttu-id="6bca9-158">Dus Voorkom mogelijke programmeurs fouten ten zeerste aanbevolen dat u de typen definieert u met betrouwbare verzamelingen om te worden niet-wijzigbaar typen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span></span> <span data-ttu-id="6bca9-159">Dit houdt in dat u Houd u aan de waardetypen core (zoals getallen [Int32, UInt64, enz.], DateTime, Guid, TimeSpan en dergelijke).</span><span class="sxs-lookup"><span data-stu-id="6bca9-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span></span> <span data-ttu-id="6bca9-160">En natuurlijk kunt u ook tekenreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6bca9-160">And, of course, you can also use String.</span></span> <span data-ttu-id="6bca9-161">Het is raadzaam om te voorkomen dat de eigenschappen van de verzameling als serialiseren en een deserialiseren ze kunt vaak kunt lagere prestaties.</span><span class="sxs-lookup"><span data-stu-id="6bca9-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="6bca9-162">Echter, als u gebruiken van eigenschappen van verzameling wilt, we raden het gebruik van. NET van niet-wijzigbaar verzamelingen bibliotheek ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="6bca9-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="6bca9-163">Deze bibliotheek is beschikbaar voor downloaden van http://nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6bca9-163">This library is available for download from http://nuget.org.</span></span> <span data-ttu-id="6bca9-164">Ook wordt aangeraden uw klassen verzegelen en het aanbrengen van velden alleen-lezen indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="6bca9-164">We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="6bca9-165">Het type gebruikersgegevens hieronder laat zien hoe een onveranderbare type profiteren van de hiervoor genoemde aanbevelingen definiëren.</span><span class="sxs-lookup"><span data-stu-id="6bca9-165">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span></span>

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert the deserialized collection to an immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has to set it. So instead, the getter is public and the setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId to the ItemsBidding
   // collection by creating a new immutable UserInfo object with the added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="6bca9-166">Het type ItemId is ook een niet-wijzigbaar type, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6bca9-166">The ItemId type is also an immutable type as shown here:</span></span>

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="6bca9-167">Schemaversies (upgrades)</span><span class="sxs-lookup"><span data-stu-id="6bca9-167">Schema versioning (upgrades)</span></span>
<span data-ttu-id="6bca9-168">Intern serialiseren betrouwbare verzamelingen uw objecten gebruikt. De NET DataContractSerializer.</span><span class="sxs-lookup"><span data-stu-id="6bca9-168">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="6bca9-169">De geserialiseerde objecten zijn opgeslagen op lokale schijf van de primaire replica en de secundaire replica's ook worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="6bca9-169">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span></span> <span data-ttu-id="6bca9-170">Naarmate uw service meer vormt krijgt, is het waarschijnlijk wilt u het type gegevens (schema), die uw service nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-170">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span></span> <span data-ttu-id="6bca9-171">U moet versiebeheer van uw gegevens met uiterst voorzichtig benaderen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-171">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="6bca9-172">Allereerst omdat kunt u moet altijd oude gegevens worden gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-172">First and foremost, you must always be able to deserialize old data.</span></span> <span data-ttu-id="6bca9-173">Dit houdt in uw code deserialisatie oneindig achterwaarts compatibel moet zijn: 333 versie van uw servicecode moet kunnen worden uitgevoerd voor de gegevens worden geplaatst in een betrouwbare verzameling met versie 1 van uw servicecode 5 jaar geleden.</span><span class="sxs-lookup"><span data-stu-id="6bca9-173">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="6bca9-174">Bovendien is de servicecode bijgewerkte één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="6bca9-174">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="6bca9-175">Tijdens een upgrade hebt u dus twee verschillende versies van uw servicecode die tegelijkertijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-175">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="6bca9-176">U moet voorkomen met de nieuwe versie van uw servicecode gebruik van het nieuwe schema oude versies van uw servicecode wordt mogelijk niet kunnen verwerken van het nieuwe schema.</span><span class="sxs-lookup"><span data-stu-id="6bca9-176">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span></span> <span data-ttu-id="6bca9-177">Indien mogelijk moet u elke versie van de service worden voorwaarts compatibel met versie 1 ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="6bca9-177">When possible, you should design each version of your service to be forward compatible by 1 version.</span></span> <span data-ttu-id="6bca9-178">Dit betekent in het bijzonder V1 van uw servicecode moet kunnen schema-elementen die dit niet expliciet verwerkt gewoon negeren.</span><span class="sxs-lookup"><span data-stu-id="6bca9-178">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="6bca9-179">Maar moet deze kunnen gegevens weet niet expliciet over en gewoon schrijven weer uit bij het bijwerken van een woordenboeksleutel of een waarde op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6bca9-179">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="6bca9-180">Terwijl u het schema van een sleutel wijzigen kunt, moet u ervoor zorgen dat uw sleutel hash-code en is gelijk aan algoritmen stabiel zijn.</span><span class="sxs-lookup"><span data-stu-id="6bca9-180">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="6bca9-181">Als u hoe een van deze algoritmen werken wijzigen, kunt u zich niet opzoeken van de sleutel in het woordenboek betrouwbare ooit opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6bca9-181">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="6bca9-182">U kunt ook uitvoeren wat wordt meestal aangeduid als een upgrade van een 2-fase.</span><span class="sxs-lookup"><span data-stu-id="6bca9-182">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span></span> <span data-ttu-id="6bca9-183">Met de upgrade van een 2-fase, upgrade uw service van V1 naar V2: V2 bevat de code die het omgaan met de nieuwe schemawijziging kent, maar deze code wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bca9-183">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="6bca9-184">Wanneer de code V2 V1 gegevens leest, is van invloed op deze en V1-gegevens worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="6bca9-184">When the V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="6bca9-185">Vervolgens, nadat de upgrade voltooid voor alle upgrade-domeinen is, u kunt enigszins signaal aan de actieve V2-exemplaren dat de upgrade voltooid is.</span><span class="sxs-lookup"><span data-stu-id="6bca9-185">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span></span> <span data-ttu-id="6bca9-186">(Eén manier om signaal is dit Implementeer de upgrade van een configuratie; Dit is wat is dit een upgrade van een 2-fase.) Nu kunnen de V2-exemplaren V1-gegevens lezen, converteren naar V2-gegevens, op worden uitgevoerd en uitschrijven als V2-gegevens.</span><span class="sxs-lookup"><span data-stu-id="6bca9-186">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="6bca9-187">Wanneer andere exemplaren V2-gegevens lezen, ze hoeven niet te converteren, worden ze alleen worden uitgevoerd en V2-gegevens schrijven.</span><span class="sxs-lookup"><span data-stu-id="6bca9-187">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bca9-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bca9-188">Next Steps</span></span>
<span data-ttu-id="6bca9-189">Zie voor meer informatie over het maken van voorwaarts compatibel gegevenscontracten, [voorwaarts compatibel gegevenscontracten](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bca9-189">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="6bca9-190">Zie voor meer informatie over aanbevolen procedures op versiebeheer gegevenscontracten, [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bca9-190">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="6bca9-191">Zie voor meer informatie over het implementeren van versie fouttolerante gegevenscontracten, [versie fouttolerante serialisatie retouraanroepen](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bca9-191">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="6bca9-192">Zie voor informatie over het opgeven van een gegevensstructuur die voor de verschillende versies kan samenwerken, [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bca9-192">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
