---
title: aaaReliable verzameling object serialisatie in Azure Service Fabric | Microsoft Docs
description: Azure Service Fabric betrouwbare verzamelingen object serialisatie
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Betrouwbare verzameling object serialisatie in Azure Service Fabric
Betrouwbare verzamelingen repliceren en hun toomake items controleren of deze duurzame over machine fouten en stroomstoringen behouden.
Zowel tooreplicate als toopersist items, betrouwbare verzamelingen moeten tooserialize ze.

Betrouwbare verzamelingen voor het ophalen van de juiste serialisatiefunctie Hallo voor een bepaald type van betrouwbare status Manager.
Statusbeheer voor betrouwbaar bevat ingebouwde objectserializers en kan aangepaste objectserializers toobe geregistreerd voor een bepaald type.

## <a name="built-in-serializers"></a>Ingebouwde objectserializers

Statusbeheer voor betrouwbaar bevat ingebouwde serialisatiefunctie voor enkele algemene typen, zodat kan efficiënt standaard worden geserialiseerd. Voor andere typen betrouwbare statusbeheer terugvalt toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Ingebouwde objectserializers zijn efficiënter omdat ze weten dat de typen niet wijzigen en ze hoeven niet tooinclude informatie over Hallo type zoals de typenaam.

Betrouwbaar status Manager beschikt over ingebouwde serialisatiefunctie voor het volgende typen: 
- GUID
- BOOL
- Byte
- SByte
- Byte]
- CHAR
- Tekenreeks
- Decimale
- dubbele
- Float
- int
- uint
- lang
- ULONG
- korte
- USHORT

## <a name="custom-serialization"></a>Aangepaste serialisatie

Aangepaste objectserializers zijn vaak gebruikte tooincrease prestatie- of tooencrypt Hallo gegevens via de kabel Hallo en op schijf. Van andere redenen zijn aangepaste objectserializers meestal efficiënter dan algemene serialisatiefunctie, omdat niet tooserialize informatie over het Hallo-type hoeven. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) gebruikte tooregister is geen aangepaste serialisatiefunctie voor het betreffende type T. Hallo Deze registratie bij Hallo constructie van Hallo StatefulServiceBase tooensure moet gebeuren voordat het herstel wordt gestart, wordt alle betrouwbare verzamelingen hebben toegang tot toohello relevante serialisatiefunctie tooread hun persistente gegevens.

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> Aangepaste objectserializers krijgen voorrang boven ingebouwde objectserializers. Bijvoorbeeld wanneer een aangepaste serialisatiefunctie voor int is geregistreerd, is het gebruikte tooserialize gehele getallen in plaats van ingebouwde serialisatiefunctie Hallo voor int.

### <a name="how-tooimplement-a-custom-serializer"></a>Hoe tooimplement geen aangepaste serialisatiefunctie

Geen aangepaste serialisatiefunctie moet tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.

> [!NOTE]
> IStateSerializer<T> bevat een overbelasting voor schrijven en lezen die in een extra T basiswaarde aangeroepen. Deze API is voor de differentiële serialisatie. Differentiële serialisatie-functie is momenteel niet beschikbaar gemaakt. Daarom zijn deze twee overloads niet aangeroepen totdat differentiële serialisatie is beschikbaar gemaakt en ingeschakeld.

Hieronder volgt een voorbeeld van een aangepast type aangeroepen OrderKey met vier eigenschappen

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

Hieronder volgt een voorbeeld van de implementatie van IStateSerializer<OrderKey>.
Merk op dat in lezen en schrijven overloads die baseValue, hun respectieve overload-aanroep voor doorsturen compatibiliteit.

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a>Kunnen
In een [rolling upgrade van de toepassing](service-fabric-application-upgrade.md), Hallo-upgrade is toegepaste tooa deelverzameling met knooppunten, één upgradedomein tegelijk. Tijdens dit proces wordt een aantal upgradedomeinen worden uitgevoerd in een nieuwere versie van uw toepassing hello en een aantal upgradedomeinen worden op een oudere versie van uw toepassing hello. Tijdens het Hallo-implementatie, nieuwe versie van uw toepassing hello moet kunnen tooread Hallo oude versie van uw gegevens en Hallo oude versie van uw toepassing moet kunnen tooread Hallo nieuwe versie van uw gegevens. Als Hallo-gegevensindeling niet voorwaarts en achterwaarts compatibel zijn, Hallo upgrade mogelijk niet werkt of slechter, gegevens mogelijk verloren of beschadigd.

Als u van ingebouwde serializer gebruikmaakt, hebt u geen tooworry over de compatibiliteit.
Echter, als u een aangepaste serialisatiefunctie of Hallo DataContractSerializer gebruikt, Hallo gegevens toobe oneindig achterwaartse hebben en voorwaarts compatibel.
Met andere woorden, elke versie van de serialisatiefunctie moet toobe kunnen tooserialize en een willekeurige versie van het Hallo-type niet deserialiseren.

Data Contract-gebruikers dienen Hallo goed gedefinieerde versieregels voor toevoegen, verwijderen en wijzigen van de velden te volgen. Gegevenscontract biedt ook ondersteuning voor het omgaan met onbekende velden en omgaan met klassenovername in Hallo serialisatie en deserialisatie proces vereist. Zie voor meer informatie [gegevenscontract met behulp van](https://msdn.microsoft.com/library/ms733127.aspx).

Aangepaste serialisatiefunctie gebruikers moeten toohello richtlijnen Hallo serialisatiefunctie die ze gebruiken achterwaartse is en voorwaarts compatibel toomake voldoen.
Algemene manier voor het ondersteunen van alle versies is het toevoegen van informatie over de grootte aan Hallo begin- en alleen optionele eigenschappen toe te voegen.
Op deze manier elke versie kunt zoveel kan en over het resterende deel van de stroom Hallo Hallo springen lezen.

## <a name="next-steps"></a>Volgende stappen
  * [Serialisatie en upgrade](service-fabric-application-upgrade-data-serialization.md)
  * [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.
  * [Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.
  * Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).
  * Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).
  * Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing](service-fabric-application-upgrade-troubleshooting.md).
