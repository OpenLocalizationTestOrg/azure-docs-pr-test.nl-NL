---
title: aaaChange FabricTransport instellingen in Azure microservices | Microsoft Docs
description: Meer informatie over het configureren van Azure Service Fabric actor communicatie-instellingen.
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="f407c-103">FabricTransport instellingen configureren voor Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f407c-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="f407c-104">Hier volgen Hallo-instellingen die u kunt configureren:</span><span class="sxs-lookup"><span data-stu-id="f407c-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="f407c-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="f407c-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="f407c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="f407c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="f407c-107">U kunt de standaardconfiguratie Hallo van FabricTransport wijzigen in de volgende manieren.</span><span class="sxs-lookup"><span data-stu-id="f407c-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="f407c-108">Assembly-kenmerk</span><span class="sxs-lookup"><span data-stu-id="f407c-108">Assembly attribute</span></span>

<span data-ttu-id="f407c-109">Hallo [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) moet het kenmerk toobe toegepast op Hallo actor-client en actor service assembly's.</span><span class="sxs-lookup"><span data-stu-id="f407c-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="f407c-110">Hallo volgende voorbeeld ziet u hoe toochange Hallo standaardwaarde FabricTransport OperationTimeout-instellingen:</span><span class="sxs-lookup"><span data-stu-id="f407c-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="f407c-111">Tweede voorbeeld wordt standaard waarden van FabricTransport MaxMessageSize en OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="f407c-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="f407c-112">Configuratiepakket</span><span class="sxs-lookup"><span data-stu-id="f407c-112">Config package</span></span>

<span data-ttu-id="f407c-113">U kunt een [configuratiepakket](service-fabric-application-model.md) toomodify Hallo standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f407c-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="f407c-114">Instellingen voor Hallo actor service FabricTransport configureren</span><span class="sxs-lookup"><span data-stu-id="f407c-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="f407c-115">Een sectie TransportSettings in Hallo settings.xml bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f407c-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="f407c-116">Standaard actor code zoekt SectionName als '&lt;ActorName&gt;TransportSettings '.</span><span class="sxs-lookup"><span data-stu-id="f407c-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="f407c-117">Als dat niet wordt gevonden, controleert deze voor SectionName als 'TransportSettings'.</span><span class="sxs-lookup"><span data-stu-id="f407c-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="f407c-118">Instellingen voor Hallo actor client assembly FabricTransport configureren</span><span class="sxs-lookup"><span data-stu-id="f407c-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="f407c-119">Als het Hallo-client wordt niet uitgevoerd als onderdeel van een service, kunt u een '&lt;Client Exe-naam&gt;. settings.xml ' bestand in Hallo dezelfde locatie als Hallo client .exe-bestand.</span><span class="sxs-lookup"><span data-stu-id="f407c-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="f407c-120">Voeg een sectie TransportSettings in dat bestand.</span><span class="sxs-lookup"><span data-stu-id="f407c-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="f407c-121">SectionName moet 'TransportSettings'.</span><span class="sxs-lookup"><span data-stu-id="f407c-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="f407c-122">Instellingen voor veilige Actor Client-Service FabricTransport configureren met secundair certificaat.</span><span class="sxs-lookup"><span data-stu-id="f407c-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="f407c-123">Secundaire certificaatgegevens kan toegevoegd worden door de parameter CertificateFindValuebySecondary toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f407c-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="f407c-124">Hieronder vindt u voorbeeld Hallo voor Hallo Listener TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="f407c-124">Below is hello example for hello Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="f407c-125">Hieronder vindt u voorbeeld Hallo voor Hallo Client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="f407c-125">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="f407c-126">FabricTransport instellingen configureren voor het beveiligen van Actor Service /-Client met behulp van de onderwerpnaam.</span><span class="sxs-lookup"><span data-stu-id="f407c-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="f407c-127">Gebruiker moet tooprovide findType als findbysubjectname zijn, CertificateIssuerThumbprints en CertificateRemoteCommonNames waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f407c-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="f407c-128">Hieronder vindt u voorbeeld Hallo voor Hallo Listener TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="f407c-128">Below is hello example for hello Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="f407c-129">Hieronder vindt u voorbeeld Hallo voor Hallo Client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="f407c-129">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
