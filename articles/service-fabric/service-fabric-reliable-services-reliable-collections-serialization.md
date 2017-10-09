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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="d8127-103">Betrouwbare verzameling object serialisatie in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d8127-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="d8127-104">Betrouwbare verzamelingen repliceren en hun toomake items controleren of deze duurzame over machine fouten en stroomstoringen behouden.</span><span class="sxs-lookup"><span data-stu-id="d8127-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="d8127-105">Zowel tooreplicate als toopersist items, betrouwbare verzamelingen moeten tooserialize ze.</span><span class="sxs-lookup"><span data-stu-id="d8127-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="d8127-106">Betrouwbare verzamelingen voor het ophalen van de juiste serialisatiefunctie Hallo voor een bepaald type van betrouwbare status Manager.</span><span class="sxs-lookup"><span data-stu-id="d8127-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="d8127-107">Statusbeheer voor betrouwbaar bevat ingebouwde objectserializers en kan aangepaste objectserializers toobe geregistreerd voor een bepaald type.</span><span class="sxs-lookup"><span data-stu-id="d8127-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="d8127-108">Ingebouwde objectserializers</span><span class="sxs-lookup"><span data-stu-id="d8127-108">Built-in Serializers</span></span>

<span data-ttu-id="d8127-109">Statusbeheer voor betrouwbaar bevat ingebouwde serialisatiefunctie voor enkele algemene typen, zodat kan efficiënt standaard worden geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="d8127-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="d8127-110">Voor andere typen betrouwbare statusbeheer terugvalt toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="d8127-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="d8127-111">Ingebouwde objectserializers zijn efficiënter omdat ze weten dat de typen niet wijzigen en ze hoeven niet tooinclude informatie over Hallo type zoals de typenaam.</span><span class="sxs-lookup"><span data-stu-id="d8127-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="d8127-112">Betrouwbaar status Manager beschikt over ingebouwde serialisatiefunctie voor het volgende typen:</span><span class="sxs-lookup"><span data-stu-id="d8127-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="d8127-113">GUID</span><span class="sxs-lookup"><span data-stu-id="d8127-113">Guid</span></span>
- <span data-ttu-id="d8127-114">BOOL</span><span class="sxs-lookup"><span data-stu-id="d8127-114">bool</span></span>
- <span data-ttu-id="d8127-115">Byte</span><span class="sxs-lookup"><span data-stu-id="d8127-115">byte</span></span>
- <span data-ttu-id="d8127-116">SByte</span><span class="sxs-lookup"><span data-stu-id="d8127-116">sbyte</span></span>
- <span data-ttu-id="d8127-117">Byte]</span><span class="sxs-lookup"><span data-stu-id="d8127-117">byte[]</span></span>
- <span data-ttu-id="d8127-118">CHAR</span><span class="sxs-lookup"><span data-stu-id="d8127-118">char</span></span>
- <span data-ttu-id="d8127-119">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d8127-119">string</span></span>
- <span data-ttu-id="d8127-120">Decimale</span><span class="sxs-lookup"><span data-stu-id="d8127-120">decimal</span></span>
- <span data-ttu-id="d8127-121">dubbele</span><span class="sxs-lookup"><span data-stu-id="d8127-121">double</span></span>
- <span data-ttu-id="d8127-122">Float</span><span class="sxs-lookup"><span data-stu-id="d8127-122">float</span></span>
- <span data-ttu-id="d8127-123">int</span><span class="sxs-lookup"><span data-stu-id="d8127-123">int</span></span>
- <span data-ttu-id="d8127-124">uint</span><span class="sxs-lookup"><span data-stu-id="d8127-124">uint</span></span>
- <span data-ttu-id="d8127-125">lang</span><span class="sxs-lookup"><span data-stu-id="d8127-125">long</span></span>
- <span data-ttu-id="d8127-126">ULONG</span><span class="sxs-lookup"><span data-stu-id="d8127-126">ulong</span></span>
- <span data-ttu-id="d8127-127">korte</span><span class="sxs-lookup"><span data-stu-id="d8127-127">short</span></span>
- <span data-ttu-id="d8127-128">USHORT</span><span class="sxs-lookup"><span data-stu-id="d8127-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="d8127-129">Aangepaste serialisatie</span><span class="sxs-lookup"><span data-stu-id="d8127-129">Custom Serialization</span></span>

<span data-ttu-id="d8127-130">Aangepaste objectserializers zijn vaak gebruikte tooincrease prestatie- of tooencrypt Hallo gegevens via de kabel Hallo en op schijf.</span><span class="sxs-lookup"><span data-stu-id="d8127-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="d8127-131">Van andere redenen zijn aangepaste objectserializers meestal efficiënter dan algemene serialisatiefunctie, omdat niet tooserialize informatie over het Hallo-type hoeven.</span><span class="sxs-lookup"><span data-stu-id="d8127-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="d8127-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) gebruikte tooregister is geen aangepaste serialisatiefunctie voor het betreffende type T. Hallo Deze registratie bij Hallo constructie van Hallo StatefulServiceBase tooensure moet gebeuren voordat het herstel wordt gestart, wordt alle betrouwbare verzamelingen hebben toegang tot toohello relevante serialisatiefunctie tooread hun persistente gegevens.</span><span class="sxs-lookup"><span data-stu-id="d8127-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

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
> <span data-ttu-id="d8127-133">Aangepaste objectserializers krijgen voorrang boven ingebouwde objectserializers.</span><span class="sxs-lookup"><span data-stu-id="d8127-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="d8127-134">Bijvoorbeeld wanneer een aangepaste serialisatiefunctie voor int is geregistreerd, is het gebruikte tooserialize gehele getallen in plaats van ingebouwde serialisatiefunctie Hallo voor int.</span><span class="sxs-lookup"><span data-stu-id="d8127-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="d8127-135">Hoe tooimplement geen aangepaste serialisatiefunctie</span><span class="sxs-lookup"><span data-stu-id="d8127-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="d8127-136">Geen aangepaste serialisatiefunctie moet tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span><span class="sxs-lookup"><span data-stu-id="d8127-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="d8127-137">IStateSerializer<T> bevat een overbelasting voor schrijven en lezen die in een extra T basiswaarde aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d8127-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="d8127-138">Deze API is voor de differentiële serialisatie.</span><span class="sxs-lookup"><span data-stu-id="d8127-138">This API is for differential serialization.</span></span> <span data-ttu-id="d8127-139">Differentiële serialisatie-functie is momenteel niet beschikbaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d8127-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="d8127-140">Daarom zijn deze twee overloads niet aangeroepen totdat differentiële serialisatie is beschikbaar gemaakt en ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d8127-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="d8127-141">Hieronder volgt een voorbeeld van een aangepast type aangeroepen OrderKey met vier eigenschappen</span><span class="sxs-lookup"><span data-stu-id="d8127-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="d8127-142">Hieronder volgt een voorbeeld van de implementatie van IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="d8127-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="d8127-143">Merk op dat in lezen en schrijven overloads die baseValue, hun respectieve overload-aanroep voor doorsturen compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="d8127-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="d8127-144">Kunnen</span><span class="sxs-lookup"><span data-stu-id="d8127-144">Upgradability</span></span>
<span data-ttu-id="d8127-145">In een [rolling upgrade van de toepassing](service-fabric-application-upgrade.md), Hallo-upgrade is toegepaste tooa deelverzameling met knooppunten, één upgradedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="d8127-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="d8127-146">Tijdens dit proces wordt een aantal upgradedomeinen worden uitgevoerd in een nieuwere versie van uw toepassing hello en een aantal upgradedomeinen worden op een oudere versie van uw toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d8127-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="d8127-147">Tijdens het Hallo-implementatie, nieuwe versie van uw toepassing hello moet kunnen tooread Hallo oude versie van uw gegevens en Hallo oude versie van uw toepassing moet kunnen tooread Hallo nieuwe versie van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="d8127-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="d8127-148">Als Hallo-gegevensindeling niet voorwaarts en achterwaarts compatibel zijn, Hallo upgrade mogelijk niet werkt of slechter, gegevens mogelijk verloren of beschadigd.</span><span class="sxs-lookup"><span data-stu-id="d8127-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="d8127-149">Als u van ingebouwde serializer gebruikmaakt, hebt u geen tooworry over de compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="d8127-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="d8127-150">Echter, als u een aangepaste serialisatiefunctie of Hallo DataContractSerializer gebruikt, Hallo gegevens toobe oneindig achterwaartse hebben en voorwaarts compatibel.</span><span class="sxs-lookup"><span data-stu-id="d8127-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="d8127-151">Met andere woorden, elke versie van de serialisatiefunctie moet toobe kunnen tooserialize en een willekeurige versie van het Hallo-type niet deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="d8127-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="d8127-152">Data Contract-gebruikers dienen Hallo goed gedefinieerde versieregels voor toevoegen, verwijderen en wijzigen van de velden te volgen.</span><span class="sxs-lookup"><span data-stu-id="d8127-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="d8127-153">Gegevenscontract biedt ook ondersteuning voor het omgaan met onbekende velden en omgaan met klassenovername in Hallo serialisatie en deserialisatie proces vereist.</span><span class="sxs-lookup"><span data-stu-id="d8127-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="d8127-154">Zie voor meer informatie [gegevenscontract met behulp van](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8127-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="d8127-155">Aangepaste serialisatiefunctie gebruikers moeten toohello richtlijnen Hallo serialisatiefunctie die ze gebruiken achterwaartse is en voorwaarts compatibel toomake voldoen.</span><span class="sxs-lookup"><span data-stu-id="d8127-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="d8127-156">Algemene manier voor het ondersteunen van alle versies is het toevoegen van informatie over de grootte aan Hallo begin- en alleen optionele eigenschappen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d8127-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="d8127-157">Op deze manier elke versie kunt zoveel kan en over het resterende deel van de stroom Hallo Hallo springen lezen.</span><span class="sxs-lookup"><span data-stu-id="d8127-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8127-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d8127-158">Next steps</span></span>
  * [<span data-ttu-id="d8127-159">Serialisatie en upgrade</span><span class="sxs-lookup"><span data-stu-id="d8127-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="d8127-160">Referentie voor ontwikkelaars voor betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="d8127-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="d8127-161">[Een upgrade van uw toepassing met behulp van Visual Studio](service-fabric-application-upgrade-tutorial.md) begeleidt u bij een upgrade van de toepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8127-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="d8127-162">[Een upgrade van uw toepassing met behulp van Powershell](service-fabric-application-upgrade-tutorial-powershell.md) begeleidt u bij een upgrade van de toepassing met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8127-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="d8127-163">Bepalen hoe uw toepassing wordt bijgewerkt met behulp van [Parameters Upgrade](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="d8127-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="d8127-164">Meer informatie over hoe toouse geavanceerde functies tijdens het bijwerken van uw toepassing door ernaar te verwijzen[geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="d8127-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="d8127-165">Veelvoorkomende problemen oplossen in toepassingsupgrades door te verwijzen toohello stappen in [toepassingsupgrades probleemoplossing](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d8127-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
