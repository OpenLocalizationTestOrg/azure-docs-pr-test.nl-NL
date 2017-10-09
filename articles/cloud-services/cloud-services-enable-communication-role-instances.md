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
# <a name="enable-communication-for-role-instances-in-azure"></a>Communicatie inschakelen voor rolinstanties in azure
Cloud service-rollen communiceren via de interne en externe verbindingen. Externe verbindingen worden genoemd **invoer eindpunten** terwijl interne verbindingen heten **interne eindpunten**. Dit onderwerp wordt beschreven hoe toomodify hello [definitie](cloud-services-model-and-package.md#csdef) toocreate eindpunten.

## <a name="input-endpoint"></a>Invoereindpunt
Hallo-invoereindpunt wordt gebruikt wanneer u een poort toohello buiten tooexpose wilt. U geeft Hallo protocoltype en Hallo-poort van het Hallo-eindpunt dat wordt vervolgens op beide Hallo interne en externe poorten voor het Hallo-eindpunt toegepast. Als u wilt, kunt u een andere interne poort voor het eindpunt Hallo Hello [LokalePoort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) kenmerk.

Hallo-invoereindpunt kunt Hallo volgende protocollen: **http, https, tcp, udp**.

een invoereindpunt toocreate toevoegen Hallo **Invoereindpunt** onderliggende element toohello **eindpunten** element van een web- of worker-rol.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Het invoereindpunt exemplaar
Invoereindpunten exemplaar zijn vergelijkbaar tooinput eindpunten, maar kunt u specifieke openbare poorten voor elke afzonderlijke rolinstantie toewijzen met behulp van poort doorsturen op Hallo load balancer. U kunt één openbare poort of een poortbereik opgeven.

Hallo exemplaar invoereindpunt kan alleen worden gebruikt **tcp** of **udp** als Hallo-protocol.

toocreate een invoereindpunt exemplaar toevoegen Hallo **InstanceInputEndpoint** onderliggende element toohello **eindpunten** element van een web- of worker-rol.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Interne eindpunt
Interne eindpunten zijn beschikbaar voor het exemplaar op exemplaar communicatie. Hallo-poort is optioneel en als u dit weglaat, een dynamische poort toohello eindpunt is toegewezen. Een poortbereik kan worden gebruikt. Er is een limiet van vijf interne eindpunten per rol.

interne eindpunt Hallo kunt Hallo volgende protocollen: **http, tcp, udp, eventuele**.

een interne invoereindpunt toocreate toevoegen Hallo **InternalEndpoint** onderliggende element toohello **eindpunten** element van een web- of worker-rol.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

U kunt ook een poortbereik gebruiken.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Vs worker-rollen. Web-rollen
Er is een klein verschil met eindpunten bij het werken met zowel worker en webservice rollen. Hallo Webrol moet ten minste één invoer eindpunt met behulp van Hallo **HTTP** protocol.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Met behulp van Hallo .NET SDK tooaccess een eindpunt
Hallo beheerde Azure-bibliotheek biedt methoden voor rol exemplaren toocommunicate tijdens runtime. Van de code die wordt uitgevoerd binnen een rolinstantie, kunt u informatie over het bestaan van andere rolinstanties en hun eindpunten hello, evenals informatie over de huidige rolinstantie Hallo ophalen.

> [!NOTE]
> U kunt alleen informatie over rolexemplaren die in uw cloudservice worden uitgevoerd en dat ten minste één interne eindpunt definiëren ophalen. U kunt gegevens over rolinstanties uitgevoerd in een andere service kan niet verkrijgen.
> 
> 

U kunt Hallo [exemplaren](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) eigenschap tooretrieve exemplaren van een rol. Voor het eerst gebruiken Hallo [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn de huidige rol van een verwijzing toohello instantie en gebruik vervolgens Hallo [rol](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) eigenschap tooreturn een verwijzing toohello rol zelf.

Wanneer u verbinding tooa rolinstantie programmatisch via Hallo .NET SDK maakt, is relatief gemakkelijk tooaccess Hallo eindpuntinformatie. Nadat u al tooa specifieke rol omgeving verbonden hebt, kunt u bijvoorbeeld Hallo-poort van een specifieke eindpunt met deze code opvragen:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Hallo **exemplaren** eigenschap retourneert een verzameling **RoleInstance** objecten. Deze verzameling bevat altijd de huidige instantie Hallo. Als u Hallo rol geen een intern eindpunt gedefinieerd, wordt Hallo verzameling bevat Hallo huidige instantie, maar er zijn geen andere exemplaren. het aantal rolinstanties in de verzameling Hallo Hallo is altijd 1 in geval van Hallo waarvoor geen interne eindpunt voor Hallo-rol is gedefinieerd. Hallo-rol is een interne eindpunt gedefinieerd, de exemplaren kunnen worden gevonden tijdens runtime als Hallo aantal exemplaren in de verzameling Hallo toohello aantal instanties dat is opgegeven voor de rol in het serviceconfiguratiebestand Hallo Hallo overeen.

> [!NOTE]
> Hallo beheerde Azure-bibliotheek biedt een manier om te bepalen Hallo status van andere rolinstanties geen, maar u kunt implementeren deze beoordeling health uzelf als de service deze functionaliteit moet. U kunt [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain informatie over het uitvoeren van de rolinstanties.
> 
> 

toodetermine hello poortnummer op voor een intern eindpunt op een rolexemplaar, kunt u Hallo [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) eigenschap tooreturn een Dictionary-object met de namen van eindpunten en hun bijbehorende IP-adressen en poorten. Hallo [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) eigenschap Hallo IP-adres en poort voor een opgegeven eindpunt. Hallo **PublicIPEndpoint** eigenschap Hallo-poort voor een eindpunt met taakverdeling. Hallo IP-adres deel van Hallo **PublicIPEndpoint** eigenschap wordt niet gebruikt.

Hier volgt een voorbeeld waarin rolinstanties doorloopt.

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

Hier volgt een voorbeeld van een werkrol die Hallo eindpunt beschikbaar gesteld via de servicedefinitie Hallo opgehaald en begint met luisteren naar verbindingen.

> [!WARNING]
> Deze code werkt alleen voor een geïmplementeerde service. Wanneer in hello Azure Compute-Emulator wordt uitgevoerd, service-configuratie-elementen die directe poort eindpunten maken (**InstanceInputEndpoint** elementen) worden genegeerd.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Verkeer regels toocontrol rol netwerkcommunicatie
Nadat u interne eindpunten gedefinieerd, kunt u network-verkeer regels (gebaseerd op Hallo-eindpunten die u hebt gemaakt) toocontrol hoe rolinstanties met elkaar communiceren kunnen kunt toevoegen. Hallo volgende diagram ziet u enkele algemene scenario's voor het beheren van rollen:

![Netwerk-verkeer regels scenario's](./media/cloud-services-enable-communication-role-instances/scenarios.png "netwerk verkeer regels scenario's")

Hallo toont volgende codevoorbeeld roldefinities voor Hallo-rollen weergegeven in het vorige diagram Hallo. Elke roldefinitie bevat ten minste één interne eindpunt gedefinieerd:

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
> Beperking van de communicatie tussen rollen kan worden uitgevoerd met interne eindpunten van beide vast en automatisch toegewezen poorten.
> 
> 

Standaard dat nadat een intern eindpunt is gedefinieerd, communicatie kan stromen van elke rol toohello interne eindpunt van een rol zonder beperkingen. toorestrict communicatie, moet u toevoegen een **NetworkTrafficRules** element toohello **ServiceDefinition** element in het servicedefinitiebestand Hallo.

### <a name="scenario-1"></a>Scenario 1
Alleen toestaan netwerkverkeer van **WebRole1** te**WorkerRole1**.

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

### <a name="scenario-2"></a>Scenario 2
Kunt u alleen netwerkverkeer van **WebRole1** te**WorkerRole1** en **WorkerRole2**.

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

### <a name="scenario-3"></a>Scenario 3
Kunt u alleen netwerkverkeer van **WebRole1** te**WorkerRole1**, en **WorkerRole1** te**WorkerRole2**.

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

### <a name="scenario-4"></a>Scenario 4
Kunt u alleen netwerkverkeer van **WebRole1** te**WorkerRole1**, **WebRole1** te**WorkerRole2**, en  **WorkerRole1** te**WorkerRole2**.

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

Een XML-schema-referentie voor Hallo-elementen die worden gebruikt boven vindt [hier](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo Cloudservice [model](cloud-services-model-and-package.md).

