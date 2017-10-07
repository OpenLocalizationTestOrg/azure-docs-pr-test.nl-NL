---
title: aaaWorking met betrouwbare verzamelingen | Microsoft Docs
description: Meer informatie over aanbevolen procedures voor het werken met betrouwbare verzamelingen Hallo.
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
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="65114-103">Werken met betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="65114-103">Working with Reliable Collections</span></span>
<span data-ttu-id="65114-104">Service Fabric biedt een stateful programming model beschikbaar too.NET ontwikkelaars via betrouwbare verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="65114-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="65114-105">In het bijzonder biedt Service Fabric betrouwbare woordenlijst en betrouwbare wachtrij klassen.</span><span class="sxs-lookup"><span data-stu-id="65114-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="65114-106">Wanneer u deze klassen gebruikt, wordt uw status gepartitioneerd (voor schaalbaarheid), gerepliceerd (voor beschikbaarheid) en transactionele binnen een partitie (voor ACID-semantiek).</span><span class="sxs-lookup"><span data-stu-id="65114-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="65114-107">Laten we kijken naar het standaardgebruik van een betrouwbare dictionary-object en zien welke ervan daadwerkelijk doen.</span><span class="sxs-lookup"><span data-stu-id="65114-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="65114-108">Alle bewerkingen op betrouwbare dictionary-objecten (met uitzondering van ClearAsync die niet ongedaan maken), vereisen een ITransaction-object.</span><span class="sxs-lookup"><span data-stu-id="65114-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="65114-109">Dit object is gekoppeld en alle wijzigingen die u probeert toomake tooany betrouwbare woordenlijst en/of betrouwbare wachtrij-objecten binnen één partitie.</span><span class="sxs-lookup"><span data-stu-id="65114-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="65114-110">Verkrijgen van een ITransaction object door aan te roepen Hallo partitie de StateManager van CreateTransaction methode.</span><span class="sxs-lookup"><span data-stu-id="65114-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="65114-111">In bovenstaande Hallo code, Hallo ITransaction-object doorgegeven tooa betrouwbare woordenlijst AddAsync methode.</span><span class="sxs-lookup"><span data-stu-id="65114-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="65114-112">Intern woordenlijst methoden die een sleutel accepteert maken gebruik van een lezer/schrijver vergrendeling Hallo sleutel gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="65114-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="65114-113">Als de methode Hallo Hallo sleutelwaarde wijzigt, Hallo methode neemt een schrijfvergrendeling Hallo sleutel en als Hallo-methode alleen uit Hallo sleutelwaarde leest, wordt een leesvergrendeling genomen op Hallo sleutel.</span><span class="sxs-lookup"><span data-stu-id="65114-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="65114-114">Aangezien AddAsync Hallo-sleutel waarde toohello nieuwe wijzigt, doorgegeven waarde schrijfvergrendeling Hallo-sleutel is genomen.</span><span class="sxs-lookup"><span data-stu-id="65114-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="65114-115">Dus als 2 (of hoger) threads tooadd waarden Hello probeert sleutel op Hallo dezelfde tijd, één thread wordt Hallo schrijfvergrendeling verkrijgen en hello andere threads wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="65114-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="65114-116">Standaard blokkeren methoden voor up too4 seconden tooacquire Hallo vergrendeling; Hallo-methoden genereren na 4 seconden een TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="65114-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="65114-117">Methode overloads bestaan waardoor u toopass een expliciete time-outwaarde als u liever.</span><span class="sxs-lookup"><span data-stu-id="65114-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="65114-118">Meestal kunt schrijven u uw code tooreact tooa TimeoutException door het afvangen en u van de hele bewerking Hallo (zoals weergegeven in de bovenstaande Hallo-code).</span><span class="sxs-lookup"><span data-stu-id="65114-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="65114-119">In mijn eenvoudige code alleen gebeld Task.Delay 100 milliseconden elke keer dat wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="65114-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="65114-120">Maar in werkelijkheid is het mogelijk dat beter met een soort exponentiële back-uit vertraging in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="65114-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="65114-121">Zodra Hallo vergrendeling wordt verkregen, AddAsync voegt Hallo-sleutel en waardeobject verwijst naar tooan interne tijdelijke woordenlijst Hallo ITransaction-object is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="65114-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="65114-122">Dit wordt gedaan tooprovide u met lezen-your-eigenaar-schrijven semantiek.</span><span class="sxs-lookup"><span data-stu-id="65114-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="65114-123">Dat wil zeggen, na het aanroepen van AddAsync, een hoger aanroep tooTryGetValueAsync (met behulp van hetzelfde ITransaction object Hallo) wordt retourwaarde Hallo zelfs als u nog geen Hallo transactie hebben gepleegd.</span><span class="sxs-lookup"><span data-stu-id="65114-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="65114-124">Vervolgens AddAsync serialiseert uw sleutel en waarde toobyte matrices objecten en voegt deze byte matrices tooa logboekbestand op het lokale knooppunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="65114-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="65114-125">Ten slotte verzendt AddAsync Hallo byte matrices tooall Hallo secundaire replica's zodat ze hebben dezelfde Hallo sleutel/waarde-informatie.</span><span class="sxs-lookup"><span data-stu-id="65114-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="65114-126">Hoewel Hallo sleutel/waarde-informatie tooa logboekbestand geschreven is, Hallo informatie wordt niet beschouwd als onderdeel van Hallo woordenlijst totdat het Hallo-transactie die ze zijn gekoppeld aan is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="65114-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="65114-127">Hallo aanroep tooCommitAsync voert in bovenstaande Hallo code, alle bewerkingen van Hallo transactie door.</span><span class="sxs-lookup"><span data-stu-id="65114-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="65114-128">In het bijzonder voegt commit informatie toohello logboekbestand op het lokale knooppunt Hallo en verstuurt ook Hallo commit record tooall Hallo secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="65114-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="65114-129">Zodra een quorum (meerderheid) van Hallo replica's al heeft geantwoord, alle gegevens wijzigingen worden beschouwd als permanente en alle sleutels die zijn gemanipuleerd via Hallo ITransaction-object gekoppeld vergrendelingen zijn vrijgegeven zodat andere threads/transacties kunt bewerken Hallo dezelfde sleutels en de waarden.</span><span class="sxs-lookup"><span data-stu-id="65114-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="65114-130">Als CommitAsync (meestal vervaldatum tooan uitzondering wordt veroorzaakt) niet wordt aangeroepen, opgehaald Hallo ITransaction object verwijderd.</span><span class="sxs-lookup"><span data-stu-id="65114-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="65114-131">Wanneer de verwijdering van een niet-doorgevoerde ITransaction-object, Service Fabric voegt logboekbestand afbreken informatie toohello van het lokale knooppunt en hoeft u niets toobe verzonden tooany Hallo secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="65114-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="65114-132">En vervolgens alle sleutels die zijn gemanipuleerd via Hallo transactie gekoppeld vergrendelingen zijn vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="65114-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="65114-133">Veelvoorkomende valkuilen en hoe tooavoid ze</span><span class="sxs-lookup"><span data-stu-id="65114-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="65114-134">Nu dat u hoe Hallo betrouwbare verzamelingen intern werken begrijpt, gaan we verdiepen in enkele algemene misbruik van deze.</span><span class="sxs-lookup"><span data-stu-id="65114-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="65114-135">Zie Hallo-code hieronder:</span><span class="sxs-lookup"><span data-stu-id="65114-135">See hello code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="65114-136">Als u werkt met een normale .NET-woordenlijst, kunt u een sleutel/waarde toohello woordenlijst toevoegen en vervolgens wijzigen Hallo-waarde van een eigenschap (zoals LastLogin).</span><span class="sxs-lookup"><span data-stu-id="65114-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="65114-137">Echter, deze code werkt niet correct met een betrouwbare woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="65114-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="65114-138">Onthouden van Hallo eerdere discussie Hallo aanroep tooAddAsync serialiseert Hallo sleutel/waarde toobyte matrices objecten en vervolgens slaat Hallo matrices tooa lokaal bestand, en verstuurt ook ze toohello secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="65114-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="65114-139">Als u later een eigenschap wijzigt, verandert dit Hallo de waarde van eigenschap in het geheugen. geen gevolgen Hallo lokaal bestand of Hallo gegevens verzonden toohello replica's.</span><span class="sxs-lookup"><span data-stu-id="65114-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="65114-140">Als Hallo proces vastloopt, is wat is er in het geheugen weggegooid.</span><span class="sxs-lookup"><span data-stu-id="65114-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="65114-141">Wanneer een nieuw proces wordt gestart of als een andere replica primaire, wordt vervolgens Hallo oude eigenschapswaarde is wat er beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="65114-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="65114-142">Ik kan geen stress genoeg hoe eenvoudig het is toomake Hallo soort fout hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65114-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="65114-143">En alleen leert u Hallo fout als of wanneer Hallo proces uitvalt.</span><span class="sxs-lookup"><span data-stu-id="65114-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="65114-144">Hallo juiste manier toowrite Hallo code is gewoon tooreverse Hallo twee regels:</span><span class="sxs-lookup"><span data-stu-id="65114-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="65114-145">Hier volgt een voorbeeld weergegeven van een algemene fout:</span><span class="sxs-lookup"><span data-stu-id="65114-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="65114-146">Opnieuw met normale .NET woordenboeken, Hallo bovenstaande code werkt goed samen en is een algemene patroon: Hallo developer maakt gebruik van een sleutel toolook van een waarde.</span><span class="sxs-lookup"><span data-stu-id="65114-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="65114-147">Als Hallo waarde bestaat, verandert Hallo developer waarde van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="65114-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="65114-148">Met betrouwbare verzamelingen echter vertoont deze code Hallo hetzelfde probleem al besproken: **moet u een object niet wijzigen nadat u tooa betrouwbare verzameling hebt gegeven.**</span><span class="sxs-lookup"><span data-stu-id="65114-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="65114-149">Hallo manier tooupdate een waarde in een betrouwbare verzameling is tooget toohello bestaande referentiewaarde en overweeg Hallo-object waarnaar wordt verwezen tooby deze verwijzing onveranderbaar.</span><span class="sxs-lookup"><span data-stu-id="65114-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="65114-150">Vervolgens maakt u een nieuw object dat een exacte kopie van de oorspronkelijke Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="65114-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="65114-151">Nu kunt u Hallo status van dit nieuwe object wijzigen en schrijven Hallo nieuw object in de verzameling Hallo zodat deze wordt geserialiseerd toobyte matrices, lokaal bestand toegevoegde toohello en toohello replica's verzonden.</span><span class="sxs-lookup"><span data-stu-id="65114-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="65114-152">Nadat doorvoeren Hallo Hallo-objecten in het geheugen, Hallo lokaal bestand doorgegeven en alle Hallo-replica's Hallo hebben exact dezelfde status.</span><span class="sxs-lookup"><span data-stu-id="65114-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="65114-153">Goede is.</span><span class="sxs-lookup"><span data-stu-id="65114-153">All is good!</span></span>

<span data-ttu-id="65114-154">Hallo-code hieronder toont Hallo juiste manier tooupdate een waarde in een betrouwbare verzameling:</span><span class="sxs-lookup"><span data-stu-id="65114-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="65114-155">Niet-wijzigbaar typen tooprevent programmeurs gegevensfout definiëren</span><span class="sxs-lookup"><span data-stu-id="65114-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="65114-156">Willen we graag Hallo tooreport compilatiefouten in het ideale geval wanneer u per ongeluk code die de status van een object dat u gewoonlijk tooconsider onveranderbare mutates produceren.</span><span class="sxs-lookup"><span data-stu-id="65114-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="65114-157">Maar Hallo C# compiler heeft geen Hallo mogelijkheid toodo dit.</span><span class="sxs-lookup"><span data-stu-id="65114-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="65114-158">In dat geval tooavoid mogelijke programmeurs fouten, wordt ten zeerste aanbevolen dat u definieert Hallo-typen die u met betrouwbare verzamelingen toobe onveranderbare typen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65114-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="65114-159">Dit houdt in dat u stick toocore waardetypen (zoals getallen [Int32, UInt64, enz.], DateTime, Guid, TimeSpan en Hallo zoals).</span><span class="sxs-lookup"><span data-stu-id="65114-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="65114-160">En natuurlijk kunt u ook tekenreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65114-160">And, of course, you can also use String.</span></span> <span data-ttu-id="65114-161">Het is aanbevolen tooavoid verzamelingseigenschappen als het serialiseren en een bij het deserialiseren van deze kunt vaak kunt lagere prestaties.</span><span class="sxs-lookup"><span data-stu-id="65114-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="65114-162">Echter, als u de eigenschappen van de verzameling toouse wilt, sterk aangeraden Hallo gebruik van. NET van niet-wijzigbaar verzamelingen bibliotheek ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="65114-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="65114-163">Deze bibliotheek is beschikbaar voor downloaden van http://nuget.org. Ook wordt aangeraden uw klassen verzegelen en het aanbrengen van velden alleen-lezen indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="65114-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="65114-164">Hallo gebruikersgegevens type hieronder laat zien hoe toodefine een niet-wijzigbaar typt u profiteert van de hiervoor genoemde aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="65114-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="65114-165">Hallo ItemId type is ook een niet-wijzigbaar type, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="65114-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="65114-166">Schemaversies (upgrades)</span><span class="sxs-lookup"><span data-stu-id="65114-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="65114-167">Intern serialiseren betrouwbare verzamelingen uw objecten gebruikt. De NET DataContractSerializer.</span><span class="sxs-lookup"><span data-stu-id="65114-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="65114-168">Hallo geserialiseerde objecten zijn persistente toohello primaire replica lokale schijf en ook verzonden toohello secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="65114-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="65114-169">Naarmate uw service meer vormt krijgt, is het waarschijnlijk zult u toochange Hallo soort gegevens (schema), die uw service nodig.</span><span class="sxs-lookup"><span data-stu-id="65114-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="65114-170">U moet versiebeheer van uw gegevens met uiterst voorzichtig benaderen.</span><span class="sxs-lookup"><span data-stu-id="65114-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="65114-171">Allereerst omdat, moet u altijd kunt toodeserialize oude gegevens.</span><span class="sxs-lookup"><span data-stu-id="65114-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="65114-172">Dit houdt in uw code deserialisatie oneindig achterwaarts compatibel moet zijn: 333 versie van uw servicecode moet kunnen toooperate op gegevens worden geplaatst in een betrouwbare verzameling met versie 1 van uw servicecode 5 jaar geleden.</span><span class="sxs-lookup"><span data-stu-id="65114-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="65114-173">Bovendien is de servicecode bijgewerkte één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="65114-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="65114-174">Tijdens een upgrade hebt u dus twee verschillende versies van uw servicecode die tegelijkertijd wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65114-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="65114-175">U moet Vermijd Hallo nieuwe versie van uw servicecode Hallo nieuwe schema gebruiken oude versies van uw servicecode wordt mogelijk niet kunnen toohandle Hallo nieuwe schema.</span><span class="sxs-lookup"><span data-stu-id="65114-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="65114-176">Indien mogelijk moet u elke versie van uw service toobe voorwaarts compatibel met versie 1 ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="65114-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="65114-177">In het bijzonder dit betekent dat V1 van uw servicecode kunnen moeten toosimply negeren alle schema-elementen dit expliciet niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="65114-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="65114-178">Het moet wel kunnen toosave alle gegevens die deze niet expliciet te weten over en gewoon schrijven opnieuw bij het bijwerken van een woordenboeksleutel of waarde.</span><span class="sxs-lookup"><span data-stu-id="65114-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="65114-179">Terwijl u Hallo-schema van een sleutel wijzigen kunt, moet u ervoor zorgen dat uw sleutel hash-code en is gelijk aan algoritmen stabiel zijn.</span><span class="sxs-lookup"><span data-stu-id="65114-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="65114-180">Als u hoe een van deze algoritmen werken wijzigen, zich u niet kunnen toolook Hallo sleutel binnen Hallo betrouwbare woordenlijst ooit opnieuw.</span><span class="sxs-lookup"><span data-stu-id="65114-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="65114-181">U kunt ook uitvoeren wat is doorgaans waarnaar wordt verwezen tooas een 2-fase met upgrades.</span><span class="sxs-lookup"><span data-stu-id="65114-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="65114-182">Met de upgrade van een 2-fase u uw service een upgrade van V1 tooV2: V2 bevat Hallo-code die weet hoe toodeal met nieuwe schemawijziging hello, maar deze code niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="65114-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="65114-183">Wanneer Hallo V2 code V1 gegevens leest, is van invloed op deze en V1-gegevens worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="65114-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="65114-184">Vervolgens, nadat het Hallo-upgrade is voltooid voor alle domeinen van de upgrade, u kunt enigszins signaal toohello actieve V2-exemplaren dat die Hallo-upgrade is voltooid.</span><span class="sxs-lookup"><span data-stu-id="65114-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="65114-185">(Eenrichtingssessie toosignal dit tooroll uit een configuratie-upgrade is; dit is wat is dit een upgrade van een 2-fase.) Nu kunnen Hallo V2-exemplaren V1-gegevens lezen, converteert u deze gegevens tooV2 op worden uitgevoerd en uitschrijven als V2-gegevens.</span><span class="sxs-lookup"><span data-stu-id="65114-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="65114-186">Wanneer u andere exemplaren V2-gegevens lezen, hoeven geen tooconvert, ze alleen worden uitgevoerd en V2-gegevens schrijven.</span><span class="sxs-lookup"><span data-stu-id="65114-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65114-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65114-187">Next Steps</span></span>
<span data-ttu-id="65114-188">Zie toolearn over het maken van voorwaarts compatibel gegevenscontracten [voorwaarts compatibel gegevenscontracten](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="65114-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="65114-189">Zie voor aanbevolen procedures toolearn op versiebeheer gegevenscontracten, [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="65114-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="65114-190">toolearn hoe tooimplement versie fouttolerante gegevens contracten, Zie [versie fouttolerante serialisatie retouraanroepen](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="65114-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="65114-191">hoe een gegevensstructuur die voor de verschillende versies kan samenwerken tooprovide zien toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="65114-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
