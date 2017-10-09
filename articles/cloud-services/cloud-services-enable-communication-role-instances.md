---
title: aaaCommunication voor rollen in Cloudservices | Microsoft Docs
description: Rolinstanties in de Cloud Services kunnen eindpunten (http, https, tcp, udp) gedefinieerd die met de Hallo buiten of tussen andere rolinstanties communiceren hebben.
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
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="42f60-103">Communicatie inschakelen voor rolinstanties in azure</span><span class="sxs-lookup"><span data-stu-id="42f60-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="42f60-104">Cloud service-rollen communiceren via de interne en externe verbindingen.</span><span class="sxs-lookup"><span data-stu-id="42f60-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="42f60-105">Externe verbindingen worden genoemd **invoer eindpunten** terwijl interne verbindingen heten **interne eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="42f60-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="42f60-106">Dit onderwerp wordt beschreven hoe toomodify hello [definitie](cloud-services-model-and-package.md#csdef) toocreate eindpunten.</span><span class="sxs-lookup"><span data-stu-id="42f60-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="42f60-107">Invoereindpunt</span><span class="sxs-lookup"><span data-stu-id="42f60-107">Input endpoint</span></span>
<span data-ttu-id="42f60-108">Hallo-invoereindpunt wordt gebruikt wanneer u een poort toohello buiten tooexpose wilt.</span><span class="sxs-lookup"><span data-stu-id="42f60-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="42f60-109">U geeft Hallo protocoltype en Hallo-poort van het Hallo-eindpunt dat wordt vervolgens op beide Hallo interne en externe poorten voor het Hallo-eindpunt toegepast.</span><span class="sxs-lookup"><span data-stu-id="42f60-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="42f60-110">Als u wilt, kunt u een andere interne poort voor het eindpunt Hallo Hello [LokalePoort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) kenmerk.</span><span class="sxs-lookup"><span data-stu-id="42f60-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="42f60-111">Hallo-invoereindpunt kunt Hallo volgende protocollen: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="42f60-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="42f60-112">een invoereindpunt toocreate toevoegen Hallo **Invoereindpunt** onderliggende element toohello **eindpunten** element van een web- of worker-rol.</span><span class="sxs-lookup"><span data-stu-id="42f60-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="42f60-113">Het invoereindpunt exemplaar</span><span class="sxs-lookup"><span data-stu-id="42f60-113">Instance input endpoint</span></span>
<span data-ttu-id="42f60-114">Invoereindpunten exemplaar zijn vergelijkbaar tooinput eindpunten, maar kunt u specifieke openbare poorten voor elke afzonderlijke rolinstantie toewijzen met behulp van poort doorsturen op Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="42f60-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="42f60-115">U kunt één openbare poort of een poortbereik opgeven.</span><span class="sxs-lookup"><span data-stu-id="42f60-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="42f60-116">Hallo exemplaar invoereindpunt kan alleen worden gebruikt **tcp** of **udp** als Hallo-protocol.</span><span class="sxs-lookup"><span data-stu-id="42f60-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="42f60-117">toocreate een invoereindpunt exemplaar toevoegen Hallo **InstanceInputEndpoint** onderliggende element toohello **eindpunten** element van een web- of worker-rol.</span><span class="sxs-lookup"><span data-stu-id="42f60-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="42f60-118">Interne eindpunt</span><span class="sxs-lookup"><span data-stu-id="42f60-118">Internal endpoint</span></span>
<span data-ttu-id="42f60-119">Interne eindpunten zijn beschikbaar voor het exemplaar op exemplaar communicatie.</span><span class="sxs-lookup"><span data-stu-id="42f60-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="42f60-120">Hallo-poort is optioneel en als u dit weglaat, een dynamische poort toohello eindpunt is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="42f60-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="42f60-121">Een poortbereik kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="42f60-121">A port range can be used.</span></span> <span data-ttu-id="42f60-122">Er is een limiet van vijf interne eindpunten per rol.</span><span class="sxs-lookup"><span data-stu-id="42f60-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="42f60-123">interne eindpunt Hallo kunt Hallo volgende protocollen: **http, tcp, udp, eventuele**.</span><span class="sxs-lookup"><span data-stu-id="42f60-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="42f60-124">een interne invoereindpunt toocreate toevoegen Hallo **InternalEndpoint** onderliggende element toohello **eindpunten** element van een web- of worker-rol.</span><span class="sxs-lookup"><span data-stu-id="42f60-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="42f60-125">U kunt ook een poortbereik gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42f60-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="42f60-126">Vs worker-rollen. Web-rollen</span><span class="sxs-lookup"><span data-stu-id="42f60-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="42f60-127">Er is een klein verschil met eindpunten bij het werken met zowel worker en webservice rollen.</span><span class="sxs-lookup"><span data-stu-id="42f60-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="42f60-128">Hallo Webrol moet ten minste één invoer eindpunt met behulp van Hallo **HTTP** protocol.</span><span class="sxs-lookup"><span data-stu-id="42f60-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="42f60-129">Met behulp van Hallo .NET SDK tooaccess een eindpunt</span><span class="sxs-lookup"><span data-stu-id="42f60-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="42f60-130">Hallo beheerde Azure-bibliotheek biedt methoden voor rol exemplaren toocommunicate tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="42f60-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="42f60-131">Van de code die wordt uitgevoerd binnen een rolinstantie, kunt u informatie over het bestaan van andere rolinstanties en hun eindpunten hello, evenals informatie over de huidige rolinstantie Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="42f60-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="42f60-132">U kunt alleen informatie over rolexemplaren die in uw cloudservice worden uitgevoerd en dat ten minste één interne eindpunt definiëren ophalen.</span><span class="sxs-lookup"><span data-stu-id="42f60-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="42f60-133">U kunt gegevens over rolinstanties uitgevoerd in een andere service kan niet verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="42f60-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="42f60-134">U kunt Hallo [exemplaren](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) eigenschap tooretrieve exemplaren van een rol.</span><span class="sxs-lookup"><span data-stu-id="42f60-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="42f60-135">Voor het eerst gebruiken Hallo [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn de huidige rol van een verwijzing toohello instantie en gebruik vervolgens Hallo [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) eigenschap tooreturn een verwijzing toohello rol zelf.</span><span class="sxs-lookup"><span data-stu-id="42f60-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="42f60-136">Wanneer u verbinding tooa rolinstantie programmatisch via Hallo .NET SDK maakt, is relatief gemakkelijk tooaccess Hallo eindpuntinformatie.</span><span class="sxs-lookup"><span data-stu-id="42f60-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="42f60-137">Nadat u al tooa specifieke rol omgeving verbonden hebt, kunt u bijvoorbeeld Hallo-poort van een specifieke eindpunt met deze code opvragen:</span><span class="sxs-lookup"><span data-stu-id="42f60-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="42f60-138">Hallo **exemplaren** eigenschap retourneert een verzameling **RoleInstance** objecten.</span><span class="sxs-lookup"><span data-stu-id="42f60-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="42f60-139">Deze verzameling bevat altijd de huidige instantie Hallo.</span><span class="sxs-lookup"><span data-stu-id="42f60-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="42f60-140">Als u Hallo rol geen een intern eindpunt gedefinieerd, wordt Hallo verzameling bevat Hallo huidige instantie, maar er zijn geen andere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="42f60-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="42f60-141">het aantal rolinstanties in de verzameling Hallo Hallo is altijd 1 in geval van Hallo waarvoor geen interne eindpunt voor Hallo-rol is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="42f60-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="42f60-142">Hallo-rol is een interne eindpunt gedefinieerd, de exemplaren kunnen worden gevonden tijdens runtime als Hallo aantal exemplaren in de verzameling Hallo toohello aantal instanties dat is opgegeven voor de rol in het serviceconfiguratiebestand Hallo Hallo overeen.</span><span class="sxs-lookup"><span data-stu-id="42f60-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="42f60-143">Hallo beheerde Azure-bibliotheek biedt een manier om te bepalen Hallo status van andere rolinstanties geen, maar u kunt implementeren deze beoordeling health uzelf als de service deze functionaliteit moet.</span><span class="sxs-lookup"><span data-stu-id="42f60-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="42f60-144">U kunt [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain informatie over het uitvoeren van de rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="42f60-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="42f60-145">toodetermine hello poortnummer op voor een intern eindpunt op een rolexemplaar, kunt u Hallo [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) eigenschap tooreturn een Dictionary-object met de namen van eindpunten en hun bijbehorende IP-adressen en poorten.</span><span class="sxs-lookup"><span data-stu-id="42f60-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="42f60-146">Hallo [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) eigenschap Hallo IP-adres en poort voor een opgegeven eindpunt.</span><span class="sxs-lookup"><span data-stu-id="42f60-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="42f60-147">Hallo **PublicIPEndpoint** eigenschap Hallo-poort voor een eindpunt met taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="42f60-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="42f60-148">Hallo IP-adres deel van Hallo **PublicIPEndpoint** eigenschap wordt niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="42f60-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="42f60-149">Hier volgt een voorbeeld waarin rolinstanties doorloopt.</span><span class="sxs-lookup"><span data-stu-id="42f60-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="42f60-150">Hier volgt een voorbeeld van een werkrol die Hallo eindpunt beschikbaar gesteld via de servicedefinitie Hallo opgehaald en begint met luisteren naar verbindingen.</span><span class="sxs-lookup"><span data-stu-id="42f60-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="42f60-151">Deze code werkt alleen voor een geïmplementeerde service.</span><span class="sxs-lookup"><span data-stu-id="42f60-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="42f60-152">Wanneer in hello Azure Compute-Emulator wordt uitgevoerd, service-configuratie-elementen die directe poort eindpunten maken (**InstanceInputEndpoint** elementen) worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="42f60-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
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
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="42f60-153">Verkeer regels toocontrol rol netwerkcommunicatie</span><span class="sxs-lookup"><span data-stu-id="42f60-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="42f60-154">Nadat u interne eindpunten gedefinieerd, kunt u network-verkeer regels (gebaseerd op Hallo-eindpunten die u hebt gemaakt) toocontrol hoe rolinstanties met elkaar communiceren kunnen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="42f60-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="42f60-155">Hallo volgende diagram ziet u enkele algemene scenario's voor het beheren van rollen:</span><span class="sxs-lookup"><span data-stu-id="42f60-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="42f60-156">![Netwerk-verkeer regels scenario's](./media/cloud-services-enable-communication-role-instances/scenarios.png "netwerk verkeer regels scenario's")</span><span class="sxs-lookup"><span data-stu-id="42f60-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="42f60-157">Hallo toont volgende codevoorbeeld roldefinities voor Hallo-rollen weergegeven in het vorige diagram Hallo.</span><span class="sxs-lookup"><span data-stu-id="42f60-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="42f60-158">Elke roldefinitie bevat ten minste één interne eindpunt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="42f60-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="42f60-159">Beperking van de communicatie tussen rollen kan worden uitgevoerd met interne eindpunten van beide vast en automatisch toegewezen poorten.</span><span class="sxs-lookup"><span data-stu-id="42f60-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="42f60-160">Standaard dat nadat een intern eindpunt is gedefinieerd, communicatie kan stromen van elke rol toohello interne eindpunt van een rol zonder beperkingen.</span><span class="sxs-lookup"><span data-stu-id="42f60-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="42f60-161">toorestrict communicatie, moet u toevoegen een **NetworkTrafficRules** element toohello **ServiceDefinition** element in het servicedefinitiebestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="42f60-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="42f60-162">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="42f60-162">Scenario 1</span></span>
<span data-ttu-id="42f60-163">Alleen toestaan netwerkverkeer van **WebRole1** te**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="42f60-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="42f60-164">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="42f60-164">Scenario 2</span></span>
<span data-ttu-id="42f60-165">Kunt u alleen netwerkverkeer van **WebRole1** te**WorkerRole1** en **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="42f60-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="42f60-166">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="42f60-166">Scenario 3</span></span>
<span data-ttu-id="42f60-167">Kunt u alleen netwerkverkeer van **WebRole1** te**WorkerRole1**, en **WorkerRole1** te**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="42f60-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="42f60-168">Scenario 4</span><span class="sxs-lookup"><span data-stu-id="42f60-168">Scenario 4</span></span>
<span data-ttu-id="42f60-169">Kunt u alleen netwerkverkeer van **WebRole1** te**WorkerRole1**, **WebRole1** te**WorkerRole2**, en  **WorkerRole1** te**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="42f60-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="42f60-170">Een XML-schema-referentie voor Hallo-elementen die worden gebruikt boven vindt [hier](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="42f60-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f60-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42f60-171">Next steps</span></span>
<span data-ttu-id="42f60-172">Meer informatie over Hallo Cloudservice [model](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="42f60-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

