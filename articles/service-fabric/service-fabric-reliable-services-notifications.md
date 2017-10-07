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
# <a name="reliable-services-notifications"></a>Betrouwbare Services meldingen
Kennisgevingen kunnen clients tootrack Hallo wijzigingen die tooan-object dat ze geïnteresseerd bent in worden aangebracht. Twee soorten objecten ondersteunen meldingen: *betrouwbare statusbeheer* en *betrouwbare woordenlijst*.

Er zijn veelvoorkomende redenen voor het gebruik van meldingen:

* Gebouw gematerialiseerd weergaven, zoals secundaire indexen of gefilterde weergaven van Hallo replicastatus geaggregeerd. Een voorbeeld is een gesorteerde index van alle sleutels in betrouwbare woordenlijst.
* Verzenden bewakingsgegevens, zoals het aantal gebruikers die zijn toegevoegd in Hallo afgelopen uur Hallo.

Meldingen worden gestart als onderdeel van het toepassen van bewerkingen. Vanwege die worden meldingen zo snel mogelijk en synchrone gebeurtenissen mag niet zijn dure bewerkingen behandeld.

## <a name="reliable-state-manager-notifications"></a>Betrouwbaar status Manager-meldingen
Betrouwbaar status Manager biedt meldingen voor Hallo gebeurtenissen te volgen:

* Transactie
  * Doorvoeren
* Status manager
  * Opnieuw samenstellen
  * Toevoeging van een betrouwbare status
  * Verwijderen van een betrouwbare status

Statusbeheer voor betrouwbaar houdt Hallo huidige inflight transacties. de enige wijziging Hallo in transactiestatus dat ervoor zorgt een melding toobe gestart dat is een transactie wordt doorgevoerd.

Statusbeheer voor betrouwbaar onderhoudt een verzameling van betrouwbare statussen zoals betrouwbare woordenlijst en betrouwbare wachtrij. Statusbeheer voor betrouwbaar meldingen wordt geactiveerd wanneer deze verzameling wordt gewijzigd: een betrouwbare status wordt toegevoegd of verwijderd of de volledige verzameling Hallo opnieuw wordt opgebouwd.
Hallo betrouwbare status Manager-verzameling is opnieuw opgebouwd in drie gevallen:

* Herstel: Wanneer een replica wordt gestart, het herstelt de vorige status van Hallo schijf. Hallo na herstel gebruikt **NotifyStateManagerChangedEventArgs** toofire een gebeurtenis die Hallo set van herstelde betrouwbare statussen bevat.
* Volledige kopiëren: voordat u een replica kunt deelnemen aan configuratieset hello, hieraan toobe gebouwd. Soms moet hiervoor een volledige kopie van de status van het betrouwbare statusbeheer van Hallo primaire replica toobe toegepaste toohello niet-actieve secundaire replica. Statusbeheer voor betrouwbaar op Hallo secundaire replica gebruikt **NotifyStateManagerChangedEventArgs** toofire een gebeurtenis dat het aantal betrouwbare statussen die die is verkregen van de primaire replica Hallo Hallo bevat.
* Herstel: In scenario's voor herstel na noodgevallen, Hallo replicastatus kan worden hersteld vanuit een back-up via **RestoreAsync**. In dergelijke gevallen betrouwbare status Manager op de primaire replica Hallo gebruikt **NotifyStateManagerChangedEventArgs** toofire een gebeurtenis dat het aantal betrouwbare statussen die deze vanuit een back-up Hallo teruggezet Hallo bevat.

tooregister voor transactie meldingen en/of de status manager-meldingen, moet u tooregister Hello **TransactionChanged** of **StateManagerChanged** gebeurtenissen op betrouwbare status Manager. Een algemene plaats tooregister met deze gebeurtenis-handlers Hallo constructor van uw stateful service is. Wanneer u op Hallo constructor registreert, u een melding die wordt veroorzaakt door een wijziging tijdens de levensduur van hello niet naar hun **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Hallo **TransactionChanged** maakt gebruik van gebeurtenis-handler **NotifyTransactionChangedEventArgs** tooprovide details over Hallo-gebeurtenis. Deze eigenschap Hallo-action bevat (bijvoorbeeld **NotifyTransactionChangedAction.Commit**) die aangeeft Hallo type wijziging. Het bevat ook Hallo transactie-eigenschap waarmee een verwijzing toohello transactie die gewijzigd.

> [!NOTE]
> Vandaag de dag **TransactionChanged** gebeurtenissen worden gegenereerd, alleen als Hallo transactie doorgevoerd is. Hallo actie is vervolgens gelijk te**NotifyTransactionChangedAction.Commit**. Maar in toekomstige hello, gebeurtenissen voor andere soorten statuswijzigingen transactie kunnen worden verhoogd. U wordt aangeraden Hallo actie controleren en verwerking van Hallo gebeurtenis alleen als het is een die u verwacht.
> 
> 

Hieronder volgt een voorbeeld **TransactionChanged** gebeurtenis-handler.

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

Hallo **StateManagerChanged** maakt gebruik van gebeurtenis-handler **NotifyStateManagerChangedEventArgs** tooprovide details over Hallo-gebeurtenis.
**NotifyStateManagerChangedEventArgs** twee subklassen: **NotifyStateManagerRebuildEventArgs** en **NotifyStateManagerSingleEntityChangedEventArgs**.
U Hallo actie eigenschap in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello juiste subklasse:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** en **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

Hieronder volgt een voorbeeld **StateManagerChanged** meldings-handler.

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

## <a name="reliable-dictionary-notifications"></a>Betrouwbare woordenlijst meldingen
Betrouwbare woordenlijst biedt meldingen voor Hallo gebeurtenissen te volgen:

* Opnieuw maken: Aangeroepen wanneer **ReliableDictionary** heeft de status is hersteld van een herstelde of gekopieerde lokale staat of de back-up.
* Wissen: Aangeroepen wanneer Hallo status van **ReliableDictionary** is gewist via Hallo **ClearAsync** methode.
* Toevoegen: Wordt aangeroepen wanneer een item is toegevoegd te**ReliableDictionary**.
* Update: Wordt aangeroepen wanneer een item in **IReliableDictionary** is bijgewerkt.
* Verwijderen: Wordt aangeroepen wanneer een item in **IReliableDictionary** is verwijderd.

tooget betrouwbare woordenlijst meldingen, moet u tooregister Hello **DictionaryChanged** gebeurtenis-handler op **IReliableDictionary**. Een algemene plaats tooregister met deze gebeurtenis-handlers wordt Hallo **ReliableStateManager.StateManagerChanged** melding toevoegen.
Wanneer u registreert **IReliableDictionary** te wordt toegevoegd**IReliableStateManager** zorgt ervoor dat u meldingen niet naar hun.

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
> **ProcessStateManagerSingleEntityNotification** is Hallo voorbeeldmethode die voorgaande Hallo **OnStateManagerChangedHandler** voorbeeld aanroepen.
> 
> 

Hallo voorafgaande code ingesteld Hallo **IReliableNotificationAsyncCallback** interface, samen met **DictionaryChanged**. Omdat **NotifyDictionaryRebuildEventArgs** bevat een **IAsyncEnumerable** interface--moeten toobe asynchroon--opgesomd meldingen opnieuw worden gestart via  **RebuildNotificationAsyncCallback** in plaats van **OnDictionaryChangedHandler**.

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
> In Hallo voorafgaand aan code, als onderdeel van verwerking Hallo rebuild melding onderhouden eerste Hallo geaggregeerde status is uitgeschakeld. Omdat Hallo betrouwbare verzameling wordt opnieuw opgebouwd met een nieuwe status, zijn alle eerdere meldingen niet relevant.
> 
> 

Hallo **DictionaryChanged** maakt gebruik van gebeurtenis-handler **NotifyDictionaryChangedEventArgs** tooprovide details over Hallo-gebeurtenis.
**NotifyDictionaryChangedEventArgs** vijf subklassen. Hallo actie eigenschap gebruiken in een **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello juiste subklasse:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** en **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

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

## <a name="recommendations"></a>Aanbevelingen
* *Voer* meldingsgebeurtenissen zo snel mogelijk te voltooien.
* *Geen* dure bewerkingen (bijvoorbeeld i/o-bewerkingen) worden uitgevoerd als onderdeel van synchrone gebeurtenissen.
* *Voer* Hallo actietype controleren voordat u Hallo gebeurtenis verwerkt. Nieuwe actietypen kunnen in toekomstige Hallo worden toegevoegd.

Hier volgen enkele dingen tookeep rekening:

* Meldingen worden gestart als onderdeel van Hallo uitvoering van een bewerking. Bijvoorbeeld, een melding terugzetten als laatste stap van een herstelbewerking Hallo gestart. Een herstelpunt wordt niet voltooien totdat een meldingsgebeurtenis Hallo is verwerkt.
* Omdat meldingen worden gestart als onderdeel van Hallo bewerkingen zijn toegepast, wordt door clients alleen meldingen voor lokaal doorgevoerd bewerkingen zien. En omdat operations gegarandeerd alleen toobe lokaal toegewezen (met andere woorden, aangemelde) ze kunnen wel of kan niet ongedaan in toekomstige Hallo worden gemaakt.
* Op Hallo opnieuw pad, wordt één melding geactiveerd voor elke toegepaste bewerking. Dit betekent dat als transactie T1 Create(X) Delete(X) en Create(X) bevat, u een melding voor Hallo maken van X, één voor Hallo verwijdering en één voor het maken van Hallo opnieuw in die volgorde krijgt.
* Voor transacties die meerdere bewerkingen bevatten, worden bewerkingen in Hallo volgorde waarin ze zijn ontvangen op de primaire replica Hallo van Hallo gebruiker toegepast.
* Als onderdeel van de verwerking van false voortgang bepaalde bewerkingen mogelijk ongedaan worden gemaakt. Meldingen worden gegenereerd voor deze bewerkingen ongedaan maken, rolling Hallo status van Hallo replica back tooa stabiel punt. Een belangrijk verschil van meldingen voor ongedaan maken is dat de gebeurtenissen die dubbele sleutels hebben worden geaggregeerd. Bijvoorbeeld, als T1 transactie wordt ongedaan wordt gemaakt, ziet u een tooDelete(X) één melding.

## <a name="next-steps"></a>Volgende stappen
* [Betrouwbare verzamelingen](service-fabric-work-with-reliable-collections.md)
* [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
* [Betrouwbare Services back-up en herstel (herstel na noodgevallen)](service-fabric-reliable-services-backup-restore.md)
* [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

