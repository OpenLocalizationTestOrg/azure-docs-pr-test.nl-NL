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
# <a name="working-with-reliable-collections"></a>Werken met betrouwbare verzamelingen
Service Fabric biedt een stateful programming model beschikbaar too.NET ontwikkelaars via betrouwbare verzamelingen. In het bijzonder biedt Service Fabric betrouwbare woordenlijst en betrouwbare wachtrij klassen. Wanneer u deze klassen gebruikt, wordt uw status gepartitioneerd (voor schaalbaarheid), gerepliceerd (voor beschikbaarheid) en transactionele binnen een partitie (voor ACID-semantiek). Laten we kijken naar het standaardgebruik van een betrouwbare dictionary-object en zien welke ervan daadwerkelijk doen.

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

Alle bewerkingen op betrouwbare dictionary-objecten (met uitzondering van ClearAsync die niet ongedaan maken), vereisen een ITransaction-object. Dit object is gekoppeld en alle wijzigingen die u probeert toomake tooany betrouwbare woordenlijst en/of betrouwbare wachtrij-objecten binnen één partitie. Verkrijgen van een ITransaction object door aan te roepen Hallo partitie de StateManager van CreateTransaction methode.

In bovenstaande Hallo code, Hallo ITransaction-object doorgegeven tooa betrouwbare woordenlijst AddAsync methode. Intern woordenlijst methoden die een sleutel accepteert maken gebruik van een lezer/schrijver vergrendeling Hallo sleutel gekoppeld. Als de methode Hallo Hallo sleutelwaarde wijzigt, Hallo methode neemt een schrijfvergrendeling Hallo sleutel en als Hallo-methode alleen uit Hallo sleutelwaarde leest, wordt een leesvergrendeling genomen op Hallo sleutel. Aangezien AddAsync Hallo-sleutel waarde toohello nieuwe wijzigt, doorgegeven waarde schrijfvergrendeling Hallo-sleutel is genomen. Dus als 2 (of hoger) threads tooadd waarden Hello probeert sleutel op Hallo dezelfde tijd, één thread wordt Hallo schrijfvergrendeling verkrijgen en hello andere threads wordt geblokkeerd. Standaard blokkeren methoden voor up too4 seconden tooacquire Hallo vergrendeling; Hallo-methoden genereren na 4 seconden een TimeoutException. Methode overloads bestaan waardoor u toopass een expliciete time-outwaarde als u liever.

Meestal kunt schrijven u uw code tooreact tooa TimeoutException door het afvangen en u van de hele bewerking Hallo (zoals weergegeven in de bovenstaande Hallo-code). In mijn eenvoudige code alleen gebeld Task.Delay 100 milliseconden elke keer dat wordt doorgegeven. Maar in werkelijkheid is het mogelijk dat beter met een soort exponentiële back-uit vertraging in plaats daarvan.

Zodra Hallo vergrendeling wordt verkregen, AddAsync voegt Hallo-sleutel en waardeobject verwijst naar tooan interne tijdelijke woordenlijst Hallo ITransaction-object is gekoppeld. Dit wordt gedaan tooprovide u met lezen-your-eigenaar-schrijven semantiek. Dat wil zeggen, na het aanroepen van AddAsync, een hoger aanroep tooTryGetValueAsync (met behulp van hetzelfde ITransaction object Hallo) wordt retourwaarde Hallo zelfs als u nog geen Hallo transactie hebben gepleegd. Vervolgens AddAsync serialiseert uw sleutel en waarde toobyte matrices objecten en voegt deze byte matrices tooa logboekbestand op het lokale knooppunt Hallo. Ten slotte verzendt AddAsync Hallo byte matrices tooall Hallo secundaire replica's zodat ze hebben dezelfde Hallo sleutel/waarde-informatie. Hoewel Hallo sleutel/waarde-informatie tooa logboekbestand geschreven is, Hallo informatie wordt niet beschouwd als onderdeel van Hallo woordenlijst totdat het Hallo-transactie die ze zijn gekoppeld aan is toegewezen.

Hallo aanroep tooCommitAsync voert in bovenstaande Hallo code, alle bewerkingen van Hallo transactie door. In het bijzonder voegt commit informatie toohello logboekbestand op het lokale knooppunt Hallo en verstuurt ook Hallo commit record tooall Hallo secundaire replica's. Zodra een quorum (meerderheid) van Hallo replica's al heeft geantwoord, alle gegevens wijzigingen worden beschouwd als permanente en alle sleutels die zijn gemanipuleerd via Hallo ITransaction-object gekoppeld vergrendelingen zijn vrijgegeven zodat andere threads/transacties kunt bewerken Hallo dezelfde sleutels en de waarden.

Als CommitAsync (meestal vervaldatum tooan uitzondering wordt veroorzaakt) niet wordt aangeroepen, opgehaald Hallo ITransaction object verwijderd. Wanneer de verwijdering van een niet-doorgevoerde ITransaction-object, Service Fabric voegt logboekbestand afbreken informatie toohello van het lokale knooppunt en hoeft u niets toobe verzonden tooany Hallo secundaire replica's. En vervolgens alle sleutels die zijn gemanipuleerd via Hallo transactie gekoppeld vergrendelingen zijn vrijgegeven.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Veelvoorkomende valkuilen en hoe tooavoid ze
Nu dat u hoe Hallo betrouwbare verzamelingen intern werken begrijpt, gaan we verdiepen in enkele algemene misbruik van deze. Zie Hallo-code hieronder:

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

Als u werkt met een normale .NET-woordenlijst, kunt u een sleutel/waarde toohello woordenlijst toevoegen en vervolgens wijzigen Hallo-waarde van een eigenschap (zoals LastLogin). Echter, deze code werkt niet correct met een betrouwbare woordenlijst. Onthouden van Hallo eerdere discussie Hallo aanroep tooAddAsync serialiseert Hallo sleutel/waarde toobyte matrices objecten en vervolgens slaat Hallo matrices tooa lokaal bestand, en verstuurt ook ze toohello secundaire replica's. Als u later een eigenschap wijzigt, verandert dit Hallo de waarde van eigenschap in het geheugen. geen gevolgen Hallo lokaal bestand of Hallo gegevens verzonden toohello replica's. Als Hallo proces vastloopt, is wat is er in het geheugen weggegooid. Wanneer een nieuw proces wordt gestart of als een andere replica primaire, wordt vervolgens Hallo oude eigenschapswaarde is wat er beschikbaar is.

Ik kan geen stress genoeg hoe eenvoudig het is toomake Hallo soort fout hierboven weergegeven. En alleen leert u Hallo fout als of wanneer Hallo proces uitvalt. Hallo juiste manier toowrite Hallo code is gewoon tooreverse Hallo twee regels:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Hier volgt een voorbeeld weergegeven van een algemene fout:

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

Opnieuw met normale .NET woordenboeken, Hallo bovenstaande code werkt goed samen en is een algemene patroon: Hallo developer maakt gebruik van een sleutel toolook van een waarde. Als Hallo waarde bestaat, verandert Hallo developer waarde van de eigenschap. Met betrouwbare verzamelingen echter vertoont deze code Hallo hetzelfde probleem al besproken: **moet u een object niet wijzigen nadat u tooa betrouwbare verzameling hebt gegeven.**

Hallo manier tooupdate een waarde in een betrouwbare verzameling is tooget toohello bestaande referentiewaarde en overweeg Hallo-object waarnaar wordt verwezen tooby deze verwijzing onveranderbaar. Vervolgens maakt u een nieuw object dat een exacte kopie van de oorspronkelijke Hallo-object. Nu kunt u Hallo status van dit nieuwe object wijzigen en schrijven Hallo nieuw object in de verzameling Hallo zodat deze wordt geserialiseerd toobyte matrices, lokaal bestand toegevoegde toohello en toohello replica's verzonden. Nadat doorvoeren Hallo Hallo-objecten in het geheugen, Hallo lokaal bestand doorgegeven en alle Hallo-replica's Hallo hebben exact dezelfde status. Goede is.

Hallo-code hieronder toont Hallo juiste manier tooupdate een waarde in een betrouwbare verzameling:

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Niet-wijzigbaar typen tooprevent programmeurs gegevensfout definiëren
Willen we graag Hallo tooreport compilatiefouten in het ideale geval wanneer u per ongeluk code die de status van een object dat u gewoonlijk tooconsider onveranderbare mutates produceren. Maar Hallo C# compiler heeft geen Hallo mogelijkheid toodo dit. In dat geval tooavoid mogelijke programmeurs fouten, wordt ten zeerste aanbevolen dat u definieert Hallo-typen die u met betrouwbare verzamelingen toobe onveranderbare typen gebruikt. Dit houdt in dat u stick toocore waardetypen (zoals getallen [Int32, UInt64, enz.], DateTime, Guid, TimeSpan en Hallo zoals). En natuurlijk kunt u ook tekenreeks gebruiken. Het is aanbevolen tooavoid verzamelingseigenschappen als het serialiseren en een bij het deserialiseren van deze kunt vaak kunt lagere prestaties. Echter, als u de eigenschappen van de verzameling toouse wilt, sterk aangeraden Hallo gebruik van. NET van niet-wijzigbaar verzamelingen bibliotheek ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Deze bibliotheek is beschikbaar voor downloaden van http://nuget.org. Ook wordt aangeraden uw klassen verzegelen en het aanbrengen van velden alleen-lezen indien mogelijk.

Hallo gebruikersgegevens type hieronder laat zien hoe toodefine een niet-wijzigbaar typt u profiteert van de hiervoor genoemde aanbevelingen.

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

Hallo ItemId type is ook een niet-wijzigbaar type, zoals hier wordt weergegeven:

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

## <a name="schema-versioning-upgrades"></a>Schemaversies (upgrades)
Intern serialiseren betrouwbare verzamelingen uw objecten gebruikt. De NET DataContractSerializer. Hallo geserialiseerde objecten zijn persistente toohello primaire replica lokale schijf en ook verzonden toohello secundaire replica's. Naarmate uw service meer vormt krijgt, is het waarschijnlijk zult u toochange Hallo soort gegevens (schema), die uw service nodig. U moet versiebeheer van uw gegevens met uiterst voorzichtig benaderen. Allereerst omdat, moet u altijd kunt toodeserialize oude gegevens. Dit houdt in uw code deserialisatie oneindig achterwaarts compatibel moet zijn: 333 versie van uw servicecode moet kunnen toooperate op gegevens worden geplaatst in een betrouwbare verzameling met versie 1 van uw servicecode 5 jaar geleden.

Bovendien is de servicecode bijgewerkte één upgradedomein tegelijk. Tijdens een upgrade hebt u dus twee verschillende versies van uw servicecode die tegelijkertijd wordt uitgevoerd. U moet Vermijd Hallo nieuwe versie van uw servicecode Hallo nieuwe schema gebruiken oude versies van uw servicecode wordt mogelijk niet kunnen toohandle Hallo nieuwe schema. Indien mogelijk moet u elke versie van uw service toobe voorwaarts compatibel met versie 1 ontwerpen. In het bijzonder dit betekent dat V1 van uw servicecode kunnen moeten toosimply negeren alle schema-elementen dit expliciet niet verwerkt. Het moet wel kunnen toosave alle gegevens die deze niet expliciet te weten over en gewoon schrijven opnieuw bij het bijwerken van een woordenboeksleutel of waarde.

> [!WARNING]
> Terwijl u Hallo-schema van een sleutel wijzigen kunt, moet u ervoor zorgen dat uw sleutel hash-code en is gelijk aan algoritmen stabiel zijn. Als u hoe een van deze algoritmen werken wijzigen, zich u niet kunnen toolook Hallo sleutel binnen Hallo betrouwbare woordenlijst ooit opnieuw.
>
>

U kunt ook uitvoeren wat is doorgaans waarnaar wordt verwezen tooas een 2-fase met upgrades. Met de upgrade van een 2-fase u uw service een upgrade van V1 tooV2: V2 bevat Hallo-code die weet hoe toodeal met nieuwe schemawijziging hello, maar deze code niet uitvoeren. Wanneer Hallo V2 code V1 gegevens leest, is van invloed op deze en V1-gegevens worden geschreven. Vervolgens, nadat het Hallo-upgrade is voltooid voor alle domeinen van de upgrade, u kunt enigszins signaal toohello actieve V2-exemplaren dat die Hallo-upgrade is voltooid. (Eenrichtingssessie toosignal dit tooroll uit een configuratie-upgrade is; dit is wat is dit een upgrade van een 2-fase.) Nu kunnen Hallo V2-exemplaren V1-gegevens lezen, converteert u deze gegevens tooV2 op worden uitgevoerd en uitschrijven als V2-gegevens. Wanneer u andere exemplaren V2-gegevens lezen, hoeven geen tooconvert, ze alleen worden uitgevoerd en V2-gegevens schrijven.

## <a name="next-steps"></a>Volgende stappen
Zie toolearn over het maken van voorwaarts compatibel gegevenscontracten [voorwaarts compatibel gegevenscontracten](https://msdn.microsoft.com/library/ms731083.aspx).

Zie voor aanbevolen procedures toolearn op versiebeheer gegevenscontracten, [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn hoe tooimplement versie fouttolerante gegevens contracten, Zie [versie fouttolerante serialisatie retouraanroepen](https://msdn.microsoft.com/library/ms733734.aspx).

hoe een gegevensstructuur die voor de verschillende versies kan samenwerken tooprovide zien toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
