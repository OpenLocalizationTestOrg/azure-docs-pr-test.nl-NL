---
title: Wijzig de instellingen in Azure microservices FabricTransport | Microsoft Docs
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
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="58050-103">FabricTransport instellingen configureren voor Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="58050-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="58050-104">Hier volgen de instellingen die u kunt configureren:</span><span class="sxs-lookup"><span data-stu-id="58050-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="58050-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="58050-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="58050-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="58050-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="58050-107">U kunt de standaardconfiguratie van FabricTransport wijzigen in de volgende manieren.</span><span class="sxs-lookup"><span data-stu-id="58050-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="58050-108">Assembly-kenmerk</span><span class="sxs-lookup"><span data-stu-id="58050-108">Assembly attribute</span></span>

<span data-ttu-id="58050-109">De [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) kenmerk moet worden toegepast op de actor-client en de assembly's actor-service.</span><span class="sxs-lookup"><span data-stu-id="58050-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="58050-110">Het volgende voorbeeld ziet u hoe de standaardwaarde van FabricTransport OperationTimeout instellingen wijzigen:</span><span class="sxs-lookup"><span data-stu-id="58050-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="58050-111">Tweede voorbeeld wordt standaard waarden van FabricTransport MaxMessageSize en OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="58050-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="58050-112">Configuratiepakket</span><span class="sxs-lookup"><span data-stu-id="58050-112">Config package</span></span>

<span data-ttu-id="58050-113">U kunt een [configuratiepakket](service-fabric-application-model.md) te wijzigen van de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="58050-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="58050-114">Instellingen voor de service actor FabricTransport configureren</span><span class="sxs-lookup"><span data-stu-id="58050-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="58050-115">Een sectie TransportSettings in het bestand settings.xml toevoegen.</span><span class="sxs-lookup"><span data-stu-id="58050-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="58050-116">Standaard actor code zoekt SectionName als '&lt;ActorName&gt;TransportSettings '.</span><span class="sxs-lookup"><span data-stu-id="58050-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="58050-117">Als dat niet wordt gevonden, controleert deze voor SectionName als 'TransportSettings'.</span><span class="sxs-lookup"><span data-stu-id="58050-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

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

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="58050-118">Instellingen voor de assembly van de client actor FabricTransport configureren</span><span class="sxs-lookup"><span data-stu-id="58050-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="58050-119">Als de client wordt niet uitgevoerd als onderdeel van een service, kunt u een '&lt;Client Exe-naam&gt;. settings.xml ' bestand in dezelfde locatie als de client .exe-bestand.</span><span class="sxs-lookup"><span data-stu-id="58050-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="58050-120">Voeg een sectie TransportSettings in dat bestand.</span><span class="sxs-lookup"><span data-stu-id="58050-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="58050-121">SectionName moet 'TransportSettings'.</span><span class="sxs-lookup"><span data-stu-id="58050-121">SectionName should be "TransportSettings".</span></span>

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

  * <span data-ttu-id="58050-122">Instellingen voor veilige Actor Client-Service FabricTransport configureren met secundair certificaat.</span><span class="sxs-lookup"><span data-stu-id="58050-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="58050-123">Secundaire certificaatgegevens kan toegevoegd worden door de parameter CertificateFindValuebySecondary toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="58050-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="58050-124">Hieronder volgt het voorbeeld voor de Listener TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="58050-124">Below is the example for the Listener TransportSettings.</span></span>

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
     <span data-ttu-id="58050-125">Hieronder volgt het voorbeeld voor de Client-TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="58050-125">Below is the example for the Client TransportSettings.</span></span>

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
    * <span data-ttu-id="58050-126">FabricTransport instellingen configureren voor het beveiligen van Actor Service /-Client met behulp van de onderwerpnaam.</span><span class="sxs-lookup"><span data-stu-id="58050-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="58050-127">Gebruiker moet voor het opgeven van findType als findbysubjectname zijn CertificateIssuerThumbprints en CertificateRemoteCommonNames waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="58050-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="58050-128">Hieronder volgt het voorbeeld voor de Listener TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="58050-128">Below is the example for the Listener TransportSettings.</span></span>

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
  <span data-ttu-id="58050-129">Hieronder volgt het voorbeeld voor de Client-TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="58050-129">Below is the example for the Client TransportSettings.</span></span>

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
