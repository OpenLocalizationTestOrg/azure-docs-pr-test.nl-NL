---
title: Communicatie voor rollen in Cloudservices | Microsoft Docs
description: Rolinstanties in de Cloud Services kunnen eindpunten (http, https, tcp, udp) gedefinieerd die met de buitenkant of tussen andere rolinstanties communiceren hebben.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="180b7-103">Communicatie inschakelen voor rolinstanties in azure</span><span class="sxs-lookup"><span data-stu-id="180b7-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="180b7-104">Cloud service-rollen communiceren via de interne en externe verbindingen.</span><span class="sxs-lookup"><span data-stu-id="180b7-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="180b7-105">Externe verbindingen worden genoemd **invoer eindpunten** terwijl interne verbindingen heten **interne eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="180b7-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="180b7-106">Dit onderwerp wordt beschreven hoe u wijzigt de [definitie](cloud-services-model-and-package.md#csdef) om eindpunten te maken.</span><span class="sxs-lookup"><span data-stu-id="180b7-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="180b7-107">Invoereindpunt</span><span class="sxs-lookup"><span data-stu-id="180b7-107">Input endpoint</span></span>
<span data-ttu-id="180b7-108">Het invoereindpunt wordt gebruikt wanneer u wilt weergeven van een poort voor de buitenwereld.</span><span class="sxs-lookup"><span data-stu-id="180b7-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="180b7-109">U geeft het protocoltype en de poort van het eindpunt dat voor de interne en externe poorten voor het eindpunt geldt.</span><span class="sxs-lookup"><span data-stu-id="180b7-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="180b7-110">Als u wilt, kunt u een andere interne poort voor het eindpunt met de [LokalePoort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) kenmerk.</span><span class="sxs-lookup"><span data-stu-id="180b7-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="180b7-111">Het invoereindpunt kunt de volgende protocollen: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="180b7-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="180b7-112">Voor het maken van een invoereindpunt toevoegen de **Invoereindpunt** onderliggende element op de **eindpunten** element van een web- of worker-rol.</span><span class="sxs-lookup"><span data-stu-id="180b7-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="180b7-113">Het invoereindpunt exemplaar</span><span class="sxs-lookup"><span data-stu-id="180b7-113">Instance input endpoint</span></span>
<span data-ttu-id="180b7-114">Invoereindpunten exemplaar zijn vergelijkbaar met het invoer-eindpunten, maar kunt u specifieke openbare poorten voor elke afzonderlijke rolinstantie toewijzen met behulp van poort doorsturen op de load balancer.</span><span class="sxs-lookup"><span data-stu-id="180b7-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="180b7-115">U kunt één openbare poort of een poortbereik opgeven.</span><span class="sxs-lookup"><span data-stu-id="180b7-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="180b7-116">Het invoereindpunt exemplaar kan alleen worden gebruikt **tcp** of **udp** als protocol.</span><span class="sxs-lookup"><span data-stu-id="180b7-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="180b7-117">Voor het maken van een invoereindpunt exemplaar toevoegen de **InstanceInputEndpoint** onderliggende element op de **eindpunten** element van een web- of worker-rol.</span><span class="sxs-lookup"><span data-stu-id="180b7-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="180b7-118">Interne eindpunt</span><span class="sxs-lookup"><span data-stu-id="180b7-118">Internal endpoint</span></span>
<span data-ttu-id="180b7-119">Interne eindpunten zijn beschikbaar voor het exemplaar op exemplaar communicatie.</span><span class="sxs-lookup"><span data-stu-id="180b7-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="180b7-120">De poort is optioneel en als u dit weglaat, een dynamische poort is toegewezen aan het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="180b7-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="180b7-121">Een poortbereik kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="180b7-121">A port range can be used.</span></span> <span data-ttu-id="180b7-122">Er is een limiet van vijf interne eindpunten per rol.</span><span class="sxs-lookup"><span data-stu-id="180b7-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="180b7-123">Het interne eindpunt kunt de volgende protocollen: **http, tcp, udp, eventuele**.</span><span class="sxs-lookup"><span data-stu-id="180b7-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="180b7-124">Voor het maken van een interne invoereindpunt toevoegen de **InternalEndpoint** onderliggende element op de **eindpunten** element van een web- of worker-rol.</span><span class="sxs-lookup"><span data-stu-id="180b7-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="180b7-125">U kunt ook een poortbereik gebruiken.</span><span class="sxs-lookup"><span data-stu-id="180b7-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="180b7-126">Vs worker-rollen. Web-rollen</span><span class="sxs-lookup"><span data-stu-id="180b7-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="180b7-127">Er is een klein verschil met eindpunten bij het werken met zowel worker en webservice rollen.</span><span class="sxs-lookup"><span data-stu-id="180b7-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="180b7-128">De functie web moet er op een enkele invoereindpunt met de **HTTP** protocol.</span><span class="sxs-lookup"><span data-stu-id="180b7-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="180b7-129">Voor toegang tot een eindpunt met behulp van de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="180b7-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="180b7-130">De beheerde Azure-bibliotheek biedt methoden voor rolinstanties om te communiceren tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="180b7-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="180b7-131">Van de code die wordt uitgevoerd binnen een rolinstantie, kunt u informatie over de aanwezigheid van andere rolinstanties en hun eindpunten, evenals informatie over het huidige rolexemplaar van ophalen.</span><span class="sxs-lookup"><span data-stu-id="180b7-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="180b7-132">U kunt alleen informatie over rolexemplaren die in uw cloudservice worden uitgevoerd en dat ten minste één interne eindpunt definiëren ophalen.</span><span class="sxs-lookup"><span data-stu-id="180b7-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="180b7-133">U kunt gegevens over rolinstanties uitgevoerd in een andere service kan niet verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="180b7-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="180b7-134">U kunt de [exemplaren](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) eigenschap voor het ophalen van exemplaren van een rol.</span><span class="sxs-lookup"><span data-stu-id="180b7-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="180b7-135">Voor het eerst gebruiken de [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) een verwijzing retourneren naar de huidige instantie en gebruik daarna de [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) eigenschap in op een verwijzing retourneren naar de rol zelf.</span><span class="sxs-lookup"><span data-stu-id="180b7-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="180b7-136">Wanneer u verbinding met een rolinstantie programmatisch via de .NET SDK maakt, is het betrekkelijk eenvoudig toegang tot de eindpuntinformatie.</span><span class="sxs-lookup"><span data-stu-id="180b7-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="180b7-137">Nadat u al met een specifieke rol-omgeving verbonden hebt, kunt u bijvoorbeeld de poort van een specifieke eindpunt met deze code opvragen:</span><span class="sxs-lookup"><span data-stu-id="180b7-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="180b7-138">De **exemplaren** eigenschap retourneert een verzameling **RoleInstance** objecten.</span><span class="sxs-lookup"><span data-stu-id="180b7-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="180b7-139">Deze verzameling bevat altijd de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="180b7-139">This collection always contains the current instance.</span></span> <span data-ttu-id="180b7-140">Als u de rol geen een intern eindpunt gedefinieerd, wordt de verzameling bevat het huidige exemplaar, maar er zijn geen andere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="180b7-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="180b7-141">Het aantal rolinstanties in de verzameling is altijd 1 in het geval waarbij geen interne eindpunt voor de rol is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="180b7-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="180b7-142">Als de functie wordt een intern eindpunt gedefinieerd, de exemplaren kunnen worden gevonden tijdens runtime en het aantal exemplaren in de verzameling komt overeen met het aantal exemplaren dat is opgegeven voor de rol in het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="180b7-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="180b7-143">De beheerde Azure-bibliotheek biedt geen een methode voor het bepalen van de status van andere rolinstanties, maar u kunt implementeren deze beoordeling health uzelf als de service deze functionaliteit moet.</span><span class="sxs-lookup"><span data-stu-id="180b7-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="180b7-144">U kunt [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) verkrijgen van informatie over het uitvoeren van de rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="180b7-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="180b7-145">Om te bepalen het poortnummer voor een intern eindpunt op een rolexemplaar, kunt u de [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) eigenschap retourneren een Dictionary-object met de namen van eindpunten en hun bijbehorende IP-adressen en poorten.</span><span class="sxs-lookup"><span data-stu-id="180b7-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="180b7-146">De [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) eigenschap retourneert de IP-adres en poort voor een opgegeven eindpunt.</span><span class="sxs-lookup"><span data-stu-id="180b7-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="180b7-147">De **PublicIPEndpoint** eigenschap retourneert de poort voor een eindpunt met taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="180b7-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="180b7-148">Het gedeelte van de IP-adres van de **PublicIPEndpoint** eigenschap wordt niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="180b7-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="180b7-149">Hier volgt een voorbeeld waarin rolinstanties doorloopt.</span><span class="sxs-lookup"><span data-stu-id="180b7-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="180b7-150">Hier volgt een voorbeeld van een werkrol die het eindpunt beschikbaar gesteld via de servicedefinitie opgehaald en begint met luisteren naar verbindingen.</span><span class="sxs-lookup"><span data-stu-id="180b7-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="180b7-151">Deze code werkt alleen voor een geïmplementeerde service.</span><span class="sxs-lookup"><span data-stu-id="180b7-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="180b7-152">Wanneer in de Azure Compute-Emulator wordt uitgevoerd, service-configuratie-elementen die directe poort eindpunten maken (**InstanceInputEndpoint** elementen) worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="180b7-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="180b7-153">Regels voor netwerkverkeer rollen beheren</span><span class="sxs-lookup"><span data-stu-id="180b7-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="180b7-154">Nadat u interne eindpunten definieert, kunt u regels voor netwerkverkeer (op basis van de eindpunten die u hebt gemaakt) toevoegen om te bepalen hoe rolinstanties met elkaar kunnen communiceren.</span><span class="sxs-lookup"><span data-stu-id="180b7-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="180b7-155">Het volgende diagram ziet u enkele algemene scenario's voor het beheren van rollen:</span><span class="sxs-lookup"><span data-stu-id="180b7-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="180b7-156">![Netwerk-verkeer regels scenario's](./media/cloud-services-enable-communication-role-instances/scenarios.png "netwerk verkeer regels scenario's")</span><span class="sxs-lookup"><span data-stu-id="180b7-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="180b7-157">Het volgende codevoorbeeld toont roldefinities voor de rollen weergegeven in het vorige diagram.</span><span class="sxs-lookup"><span data-stu-id="180b7-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="180b7-158">Elke roldefinitie bevat ten minste één interne eindpunt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="180b7-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="180b7-159">Beperking van de communicatie tussen rollen kan worden uitgevoerd met interne eindpunten van beide vast en automatisch toegewezen poorten.</span><span class="sxs-lookup"><span data-stu-id="180b7-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="180b7-160">Standaard nadat er is een interne eindpunt gedefinieerd, kan communicatie stromen van alle functies met het interne eindpunt van een rol zonder beperkingen.</span><span class="sxs-lookup"><span data-stu-id="180b7-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="180b7-161">Als u wilt beperken communicatie, moet u toevoegen een **NetworkTrafficRules** element op de **ServiceDefinition** -element in het servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="180b7-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="180b7-162">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="180b7-162">Scenario 1</span></span>
<span data-ttu-id="180b7-163">Alleen toestaan netwerkverkeer van **WebRole1** naar **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="180b7-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="180b7-164">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="180b7-164">Scenario 2</span></span>
<span data-ttu-id="180b7-165">Kunt u alleen netwerkverkeer van **WebRole1** naar **WorkerRole1** en **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="180b7-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="180b7-166">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="180b7-166">Scenario 3</span></span>
<span data-ttu-id="180b7-167">Kunt u alleen netwerkverkeer van **WebRole1** naar **WorkerRole1**, en **WorkerRole1** naar **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="180b7-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="180b7-168">Scenario 4</span><span class="sxs-lookup"><span data-stu-id="180b7-168">Scenario 4</span></span>
<span data-ttu-id="180b7-169">Kunt u alleen netwerkverkeer van **WebRole1** naar **WorkerRole1**, **WebRole1** naar **WorkerRole2**, en **WorkerRole1** naar **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="180b7-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="180b7-170">Een XML-schema-referentie voor de boven-elementen kan worden gevonden [hier](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="180b7-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="180b7-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="180b7-171">Next steps</span></span>
<span data-ttu-id="180b7-172">Meer informatie over de Cloudservice [model](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="180b7-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

