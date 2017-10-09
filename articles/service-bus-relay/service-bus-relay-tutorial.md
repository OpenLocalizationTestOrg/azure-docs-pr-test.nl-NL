---
title: aaaAzure Service Bus WCF Relay-zelfstudie | Microsoft Docs
description: U een Service Bus-clienttoepassing en met Relay WCF-service.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Azure Relay WCF-zelfstudie

Deze zelfstudie wordt beschreven hoe toobuild een eenvoudige WCF Relay-clienttoepassing en met Azure Relay-service. Voor een vergelijkbare zelfstudie waarin [Service Bus-berichtenservice](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), Zie [aan de slag met Service Bus-wachtrijen](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Het uitvoeren van deze zelfstudie hebt u een goed begrip van Hallo stappen vereist toocreate een Relay WCF-client en service-toepassing zijn. Als de oorspronkelijke WCF is is een service een middel met een of meer eindpunten, die allemaal een of meer servicebewerkingen. Hallo-eindpunt van een service geeft een adres waar de Hallo-service kan worden gevonden, een binding met Hallo-informatie die een client moet communiceren met de Hallo-service en een contract waarin staat Hallo functionaliteit van Hallo service tooits clients. Hallo belangrijkste verschil tussen de WCF- en WCF Relay is dat Hallo-eindpunt wordt weergegeven in de cloud Hallo in plaats van lokaal op uw computer.

Als u Hallo volgorde van onderwerpen in deze zelfstudie doorloopt, hebt u een actieve service en een client die Hallo bewerkingen van Hallo service kan worden aangeroepen. Hallo eerste onderwerp wordt beschreven hoe tooset van een account. Hallo volgende stappen wordt beschreven hoe toodefine een service die gebruikmaakt van een contract, hoe tooimplement Hallo service en hoe tooconfigure Hallo-service in code. Er wordt ook beschreven hoe toohost en Voer Hallo-service. Hallo service die is gemaakt is host zichzelf en Hallo-client en service uitgevoerd op Hallo dezelfde computer. U kunt Hallo service configureren met behulp van code of een configuratiebestand.

Hallo van de laatste drie stappen wordt beschreven hoe toocreate een clienttoepassing Hallo clienttoepassing, configureren en maken en gebruiken van een client die toegang de functionaliteit van de host Hallo Hallo tot.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie hebt u Hallo volgende nodig:

* [Microsoft Visual Studio 2015 of hoger](http://visualstudio.com). Deze zelfstudie wordt Visual Studio 2017.
* Een actief Azure-account. Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.

## <a name="create-a-service-namespace"></a>Een servicenaamruimte maken

de eerste stap Hallo is toocreate een naamruimte en tooobtain een [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) sleutel. Een naamruimte biedt een toepassingsbegrenzing voor elke toepassing die toegankelijk is via Hallo relay-service. Een SAS-sleutel wordt automatisch gegenereerd door Hallo systeem wanneer een Servicenaamruimte wordt gemaakt. Hallo combinatie van Servicenaamruimte en SAS-sleutel biedt Hallo referenties voor Azure tooauthenticate toegang tooan toepassing. Ga als volgt Hallo [hier instructies](relay-create-namespace-portal.md) toocreate een Relay-naamruimte.

## <a name="define-a-wcf-service-contract"></a>Een WCF-servicecontract definiëren

Hallo-servicecontract geeft aan welke bewerkingen (Hallo webserviceterminologie voor methoden of functies) Hallo ondersteunt. Contracten worden gemaakt door een C++-, C#- of Visual Basic-interface te definiëren. Elke methode in Hallo interface komt tooa specifieke servicebewerking overeen. Elke interface moet hebben Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) kenmerk tooit toegepast, en elke bewerking moet Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit kenmerk dat wordt toegepast. Als een methode in een interface met Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) kenmerk heeft geen Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) kenmerk toe, die methode niet weergegeven. Hallo-code voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen. Zie voor meer informatie over contracten en services, [Services ontwerpen en implementeren](https://msdn.microsoft.com/library/ms729746.aspx) in Hallo WCF-documentatie.

### <a name="create-a-relay-contract-with-an-interface"></a>Een relay-contract met een interface maken

1. Open Visual Studio als beheerder door met de rechtermuisknop op Hallo programma in Hallo **Start** menu en selecteer **als administrator uitvoeren**.
2. Maak een nieuw consoletoepassingsproject aan. Klik op Hallo **bestand** menu en selecteer **nieuw**, klikt u vervolgens op **Project**. In Hallo **nieuw Project** dialoogvenster, klikt u op **Visual C#** (als **Visual C#** niet wordt weergegeven, kijkt u onder **andere talen**). Klik op Hallo **Console-App (.NET Framework)** -sjabloon en noem deze **EchoService**. Klik op **OK** toocreate Hallo project.

    ![][2]

3. Hallo Service Bus NuGet-pakketten installeren. Dit pakket wordt automatisch toegevoegd verwijzingen toohello Service Bus-bibliotheken, evenals Hallo WCF **System.ServiceModel**. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is Hallo-naamruimte die u tooprogrammatically toegang Hallo basisfuncties van WCF. Service Bus maakt gebruik van veel van Hallo-objecten en kenmerken van WCF toodefine servicecontracten.

    Klik in Solution Explorer met de rechtermuisknop op het Hallo-project en klik vervolgens op **NuGet-pakketten beheren...** . Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`. Zorg ervoor dat projectnaam Hallo is geselecteerd in Hallo **versie (s)** vak. Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.

    ![][3]
4. Dubbelklik in Solution Explorer op Hallo Program.cs-bestand tooopen deze in de editor Hallo als deze nog niet is geopend.
5. Voeg de volgende Hallo using-instructies Hallo boven aan het Hallo-bestand:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Wijziging Hallo naamruimtenaam van de standaardnaam van **EchoService** te**Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > Deze zelfstudie wordt gebruikgemaakt van Hallo C#-naamruimte **Microsoft.ServiceBus.Samples**, namelijk Hallo-naamruimte van contract gebaseerde Hallo beheerde type dat wordt gebruikt in het Hallo-configuratiebestand in Hallo [configureren Hallo WCF-client](#configure-the-wcf-client) stap. U kunt elke gewenste naamruimte bij het maken van dit voorbeeld; opgeven Hallo-zelfstudie werkt echter niet tenzij u vervolgens Hallo naamruimten van Hallo contract en de service, in het configuratiebestand van de toepassing hello aanpassen. Hallo naamruimte die is opgegeven in het App.config-bestand moet Hallo Hallo dezelfde als Hallo naamruimte die is opgegeven in de C#-bestanden.
   >
   >
7. Direct na Hallo `Microsoft.ServiceBus.Samples` naamruimtedeclaratie, maar in Hallo naamruimte, definieert u een nieuwe interface met de naam `IEchoContract` en toepassing hello `ServiceContractAttribute` kenmerk toohello interface met een naamruimtewaarde van `http://samples.microsoft.com/ServiceModel/Relay/`. Hallo naamruimtewaarde verschilt van Hallo-naamruimte die u gebruiken voor de hele Hallo bereik van uw code. In plaats daarvan Hallo naamruimtewaarde gebruikt als een unieke id voor dit contract. Het expliciet opgeven van Hallo-naamruimte voorkomt u dat standaardnaamruimtewaarde hello toohello contractnaam wordt toegevoegd. Plak de code te volgen na de naamruimtedeclaratie Hallo Hallo:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Hallo naamruimte van het servicecontract bevat meestal een schematische naam die versie-informatie bevat. Inclusief versiegegevens in de naamruimte van het servicecontract hello, kunnen services tooisolate grote wijzigingen door te definiëren van een nieuw servicecontract met een nieuwe naamruimte en het beschikbaar te maken op een nieuw eindpunt. Op deze manier kunnen clients zonder toobe bijgewerkt toouse Hallo oude servicecontract blijven. De versie-informatie kan bestaan uit een datum of een buildnummer. Zie [Serviceversiebeheer](http://go.microsoft.com/fwlink/?LinkID=180498) voor meer informatie. Naamgeving van schema van de servicecontractnaamruimte Hallo Hallo bevat oog op Hallo van deze zelfstudie wordt geen versie-informatie.
   >
   >
8. Binnen Hallo `IEchoContract` interface, declareert u een methode voor het Hallo één bewerking Hallo `IEchoContract` contract zichtbaar gemaakt in Hallo interface en toepassing hello `OperationContractAttribute` kenmerk toohello methode die u wilt dat tooexpose als onderdeel van openbare WCF Relay Hallo contract, als volgt:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Direct na Hallo `IEchoContract` interface definition, declareert u een kanaal dat eigenschappen van overneemt `IEchoContract` en ook toohello `IClientChannel` interface, zoals hier wordt weergegeven:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Een kanaal is Hallo WCF-object waarmee Hallo host en de client informatie tooeach andere doorgeven. Later schrijft u code tegen Hallo kanaal tooecho informatie tussen de twee toepassingen Hallo.
10. Van Hallo **bouwen** menu, klikt u op **Build Solution** of druk op **Ctrl + Shift + B** tooconfirm Hallo juistheid van uw werk tot nu toe.

### <a name="example"></a>Voorbeeld

Hallo volgende code toont een eenvoudige interface die een Relay WCF-contract wordt gedefinieerd.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Nu dat hello interface is gemaakt, kunt u Hallo-interface implementeren.

## <a name="implement-hello-wcf-contract"></a>Hallo WCF-contract implementeren

Maken van een Azure relay, moet eerst de Hallo-contract wordt gedefinieerd door middel van een interface te maken. Zie voor meer informatie over het maken van de interface Hallo Hallo vorige stap. de volgende stap Hallo is tooimplement Hallo-interface. Dit omvat het maken van een klasse met de naam `EchoService` die gebruiker gedefinieerde Hallo implementeert `IEchoContract` interface. Nadat u Hallo-interface implementeert, configureert u Hallo-interface met een App.config-configuratiebestand. Hallo-configuratiebestand bevat de benodigde gegevens voor het Hallo-toepassing, zoals het Hallo-naam van Hallo-service, Hallo-naam van het Hallo-contract en Hallo type protocol dat wordt gebruikt toocommunicate met Hallo relay-service. Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen. Raadpleeg voor algemene informatie over hoe een service tooimplement contract [servicecontracten implementeren](https://msdn.microsoft.com/library/ms733764.aspx) in Hallo WCF-documentatie.

1. Maak een nieuwe klasse met de naam `EchoService` direct na de definitie van Hallo Hallo `IEchoContract` interface. Hallo `EchoService` klasse implementeert Hallo `IEchoContract` interface.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Vergelijkbare tooother interface-implementaties, kunt u Hallo definitie implementeren in een ander bestand. Echter Hallo-implementatie voor deze zelfstudie bevindt zich in hetzelfde bestand als de interfacedefinitie Hallo en Hallo Hallo `Main` methode.
2. Toepassing hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello kenmerk `IEchoContract` interface. Hallo-kenmerk geeft Hallo servicenaam en naamruimte. Hierna moet u Hallo `EchoService` klasse als volgt weergegeven:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Implementeer Hallo `Echo` methode die is gedefinieerd in Hallo `IEchoContract` interface in Hallo `EchoService` klasse.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Klik op **bouwen**, klikt u vervolgens op **Build Solution** tooconfirm Hallo juistheid van uw werk.

### <a name="define-hello-configuration-for-hello-service-host"></a>Hallo-configuratie voor Hallo ServiceHost definiëren

1. Hallo-configuratiebestand is heel vergelijkbaar tooa WCF-configuratiebestand. Het Hallo-servicenaam, eindpunt (dat wil zeggen, Hallo locatie die Azure Relay beschikbaar voor clients en hosts toocommunicate met elkaar maakt) bevat en Hallo binding (Hallo type protocol dat wordt gebruikt toocommunicate). Hallo belangrijkste verschil is dat deze geconfigureerde service-eindpunt tooa verwijst [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding die geen deel van Hallo .NET Framework uitmaakt. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is een Hallo bindingen die is gedefinieerd door Hallo-service.
2. In **Solution Explorer**, dubbelklikt u op Hallo App.config-bestand tooopen in Hallo Visual Studio-editor.
3. In Hallo `<appSettings>` element Hallo tijdelijke aanduidingen vervangen door Hallo-naam van uw Servicenaamruimte en SAS-sleutel die u in een eerdere stap hebt gekopieerd Hallo.
4. Binnen Hallo `<system.serviceModel>` tags, Voeg een `<services>` element. U kunt meerdere relay-toepassingen definiëren in een enkel configuratiebestand. In deze zelfstudie wordt er echter maar één gedefinieerd.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. Binnen Hallo `<services>` element, Voeg een `<service>` toodefine Hallo elementnaam Hallo-service.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. Binnen Hallo `<service>` element Hallo-locatie van het contract Hallo-eindpunt te definiëren en ook Hallo type van de binding voor het Hallo-eindpunt.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    Hallo-eindpunt definieert waar Hallo client zoekt naar de hosttoepassing Hallo. Later, Hallo zelfstudie maakt gebruik van deze stap toocreate een URI die volledig Hallo host via Azure Relay beschrijft. Hallo binding weet u dat we TCP gebruiken zoals Hallo protocol toocommunicate met Hallo relay-service.
7. Van Hallo **bouwen** menu, klikt u op **Build Solution** tooconfirm Hallo juistheid van uw werk.

### <a name="example"></a>Voorbeeld

Hallo toont volgende code Hallo-implementatie van het servicecontract Hallo.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Hallo toont volgende code basisindeling van Hallo App.config-bestand die is gekoppeld aan de ServiceHost Hallo Hallo.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Hosten en uitvoeren van een eenvoudige web service tooregister met Hallo relay-service

Deze stap wordt beschreven hoe toorun een Azure Relay-service.

### <a name="create-hello-relay-credentials"></a>Hallo relay referenties maken

1. In `Main()`, maakt u twee variabelen in welke toostore Hallo-naamruimte en SAS-sleutel die worden gelezen vanuit het consolevenster Hallo Hallo.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    Hallo SAS-sleutel zijn gebruikte hoger tooaccess uw project. Hallo-naamruimte is doorgegeven als parameter te`CreateServiceUri` toocreate een service-URI.
2. Met behulp van een [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, dat u gebruikmaakt van een SAS-sleutel als referentietype Hallo declareren. Hallo volgende code direct na Hallo-code toegevoegd in de laatste stap Hallo toevoegen.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Een basisadres voor Hallo service maken

Nadat u hebt toegevoegd in de laatste stap Hallo Hallo code maakt een `Uri` exemplaar voor het basisadres Hallo van Hallo-service. Deze URI bevat Hallo Service Bus-schema, Hallo-naamruimte en het pad Hallo van Hallo service-interface.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

'sb' is een afkorting van Hallo Service Bus-schema en geeft aan dat we TCP als protocol hello gebruiken. Dit is ook eerder aangegeven in het configuratiebestand hello, wanneer [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) als Hallo-binding is opgegeven.

Voor deze zelfstudie Hallo-URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Maken en configureren van ServiceHost Hallo

1. Stel de connectiviteitsmodus Hallo in te`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    Hallo connectiviteitsmodus beschrijft Hallo protocol Hallo-service gebruikt toocommunicate met Hallo relay-service; via HTTP of TCP. Met behulp van de standaardinstelling Hallo `AutoDetect`, Hallo-service probeert tooconnect tooAzure Relay via TCP als deze beschikbaar is en HTTP als TCP niet beschikbaar is. Dit wijkt af van de protocolservice Hallo Hallo opmerking opgeeft voor clientcommunicatie. Dat protocol wordt bepaald door het Hallo-binding die wordt gebruikt. Bijvoorbeeld, een service kunt Hallo [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding die aangeeft dat het eindpunt met clients via HTTP communiceert. Die dezelfde service kan opgeeft **ConnectivityMode.AutoDetect** zodat Hallo service met Azure Relay via TCP communiceert.
2. Hallo ServiceHost, met behulp van Hallo die URI eerder hebt gemaakt in deze sectie maken.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    Hallo ServiceHost is Hallo WCF-object dat Hallo-service instantieert. Hier kunt u geeft hieraan Hallo type service dat u wilt dat toocreate (een `EchoService` type), en ook toohello adres waarmee u wilt dat tooexpose Hallo service.
3. Toevoegen aan de bovenkant van de Hallo van het bestand Program.cs hello, verwijzingen te[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) en [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. Terug in de `Main()`, Hallo eindpunt tooenable openbare toegang configureren.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Deze stap informeert Hallo relay-service dat uw toepassing openbaar vinden is te door Hallo ATOM-feed voor uw project in. Als u instelt **DiscoveryType** te**persoonlijke**, een client zou kunnen tooaccess Hallo service nog steeds zijn. Hallo service zou niet weergegeven bij het zoeken Hallo Relay-naamruimte. In plaats daarvan heeft Hallo-client tooknow hello eindpuntpad tevoren.
5. Toepassing hello service referenties toohello service-eindpunten gedefinieerd in Hallo App.config-bestand:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Zoals vermeld in de vorige stap hello, kan u hebt gedeclareerd meerdere services en eindpunten in het Hallo-configuratiebestand. Als u had deze code zou passeren Hallo-configuratiebestand en de zoekcriteria voor elk eindpunt toowhich uw referenties kunnen worden toegepast. Voor deze zelfstudie heeft Hallo configuratiebestand echter slechts één eindpunt.

### <a name="open-hello-service-host"></a>De ServiceHost openen Hallo

1. Hallo-service openen.

    ```csharp
    host.Open();
    ```
2. Kennis Hallo-gebruiker die het Hallo-service wordt uitgevoerd en wordt uitgelegd hoe tooshut Hallo-service.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Wanneer u klaar bent, sluit u Hallo ServiceHost.

    ```csharp
    host.Close();
    ```
4. Druk op **Ctrl + Shift + B** toobuild Hallo project.

### <a name="example"></a>Voorbeeld

Uw servicecode voltooide ziet er als volgt. Hallo-code bevat Hallo servicecontract en de implementatie uit de vorige stappen in de zelfstudie Hallo en hosts Hallo service in een consoletoepassing.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Maak een WCF-client voor servicecontract Hallo

de volgende stap Hallo toocreate een clienttoepassing en definiëren Hallo servicecontract u in latere stappen gaat implementeren. Veel van deze stappen lijken op Hallo stappen gebruikt een service toocreate: een contract, bewerkt een App.config-bestand, met behulp van referenties tooconnect toohello relay-service, enzovoort. Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.

1. Maak een nieuw project in de huidige Visual Studio-oplossing Hallo voor Hallo client door Hallo volgende te doen:

   1. Klik in Solution Explorer in Hallo oplossing die Hallo service bevat, met de rechtermuisknop op Hallo huidige oplossing (niet Hallo project) en klikt u op **toevoegen**. Klik vervolgens op **Nieuw project**.
   2. In Hallo **Add New Project** in het dialoogvenster, klikt u op **Visual C#** (als **Visual C#** niet wordt weergegeven, kijkt u onder **andere talen**), selecteer Hallo **Console-App (.NET Framework)** -sjabloon en noem deze **EchoClient**.
   3. Klik op **OK**.
      <br />
2. Dubbelklik in Solution Explorer op Hallo het bestand Program.cs in Hallo **EchoClient** project tooopen deze in de editor Hallo als deze nog niet is geopend.
3. Wijziging Hallo naamruimtenaam van de standaardnaam van `EchoClient` te`Microsoft.ServiceBus.Samples`.
4. Hallo installeren [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus): Klik in Solution Explorer met de rechtermuisknop op Hallo **EchoClient** project en klik vervolgens op **NuGet-pakketten beheren**. Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`. Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.

    ![][3]
5. Voeg een `using` -instructie voor Hallo [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) naamruimte in het bestand Program.cs Hallo.

    ```csharp
    using System.ServiceModel;
    ```
6. Hallo definitie toohello servicecontractnaamruimte, zoals wordt weergegeven in het volgende voorbeeld Hallo toevoegen Houd er rekening mee dat deze definitie identiek toohello definitie gebruikt in Hallo is **Service** project. U moet deze code toevoegen boven Hallo Hallo `Microsoft.ServiceBus.Samples` naamruimte.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Druk op **Ctrl + Shift + B** toobuild Hallo-client.

### <a name="example"></a>Voorbeeld

Hallo volgende code toont Hallo huidige status van het bestand Program.cs Hallo in Hallo **EchoClient** project.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Hallo WCF-client configureren

In deze stap maakt u een App.config-bestand voor een eenvoudige clienttoepassing die toegang heeft tot Hallo service eerder hebt gemaakt in deze zelfstudie. Dit App.config-bestand definieert Hallo contract, binding en de naam van het Hallo-eindpunt. Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.

1. Klik in Solution Explorer in Hallo **EchoClient** project, dubbelklikt u op **App.config** tooopen Hallo-bestand in Visual Studio-editor Hallo.
2. In Hallo `<appSettings>` element Hallo tijdelijke aanduidingen vervangen door Hallo-naam van uw Servicenaamruimte en SAS-sleutel die u in een eerdere stap hebt gekopieerd Hallo.
3. Binnen het element system.serviceModel Hallo toevoegen een `<client>` element.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    Tijdens deze stap wordt aangegeven dat u een clienttoepassing van het type WCF maakt.
4. Binnen Hallo `client` element Hallo-naam, contract en bindingstype voor Hallo eindpunt definiëren.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Deze stap definieert Hallo-naam van eindpunt hello, Hallo contract gedefinieerd in het Hallo-service en Hallo feit die Hallo clienttoepassing TCP toocommunicate met Azure Relay gebruikt. Hallo eindpuntnaam wordt gebruikt in Hallo volgende stap toolink deze eindpuntconfiguratie met Hallo service-URI.
5. Klik op **bestand**, klikt u vervolgens op **Alles opslaan**.

## <a name="example"></a>Voorbeeld

Hallo toont volgende code Hallo App.config-bestand voor Hallo Echo-client.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Hallo WCF-client implementeren
In deze stap maakt implementeren u een eenvoudige clienttoepassing die u eerder hebt gemaakt in deze zelfstudie Hallo-service. Vergelijkbare toohello service, Hallo client voeren veel van Hallo dezelfde bewerkingen tooaccess Azure Relay:

1. Sets Hallo connectiviteitsmodus.
2. Hallo URI die u Hallo host-service zoekt maakt.
3. Hallo beveiligingsreferenties definieert.
4. Van toepassing hello referenties toohello verbinding.
5. Hallo-verbinding wordt geopend.
6. Hallo toepassingsspecifieke taken worden uitgevoerd.
7. Hallo-verbinding gesloten.

Een van de belangrijkste verschillen Hallo is echter dat Hallo-clienttoepassing gebruikmaakt van een kanaal tooconnect toohello relay-service dat het Hallo-service gebruikt een gesprek te**ServiceHost**. Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.

### <a name="implement-a-client-application"></a>Een clienttoepassing implementeren
1. Stel de connectiviteitsmodus Hallo in te**AutoDetect**. Toevoegen van de volgende code in Hallo Hallo `Main()` methode Hallo **EchoClient** toepassing.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Variabelen toohold Hallo waarden opgeven voor het Hallo-Servicenaamruimte en SAS-sleutel die in de console Hallo worden gelezen.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Hallo URI die Hallo-locatie van Hallo host in uw Relay-project definieert maken.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Hallo-referentieobject voor het eindpunt van uw Servicenaamruimte maken.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Maak Hallo kanaal-factory waarin wordt beschreven in de bestand App.config Hallo Hallo-configuratie wordt geladen.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Een kanaalfactory is een WCF-object dat wordt gemaakt van een kanaal dat Hallo-service en clienttoepassingen communiceren.
6. Hallo-referenties zijn van toepassing.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Maak en open Hallo kanaal toohello-service.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Schrijf Hallo algemene gebruikersinterface en functionaliteit voor Hallo echo.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Houd er rekening mee dat Hallo code Hallo exemplaar van Hallo kanaalobject als proxy voor Hallo-service gebruikt.
9. Sluit Hallo kanaal en sluit Hallo factory.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Voorbeeld

De volledige code ziet er als volgt die weergeeft hoe toocreate een clienttoepassing, hoe toocall Hallo bewerkingen van het Hallo-service en hoe tooclose client Hallo na Hallo bewerking aanroepen is voltooid.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren

1. Druk op **Ctrl + Shift + B** toobuild Hallo oplossing. Dit bouwt zowel het clientproject hello en Hallo-serviceproject dat u hebt gemaakt in de vorige stappen Hallo.
2. Voordat u actieve Hallo clienttoepassing, moet u ervoor zorgen dat Hallo-servicetoepassing wordt uitgevoerd. Klik in Solution Explorer in Visual Studio met de rechtermuisknop op Hallo **EchoService** oplossing, klikt u vervolgens op **eigenschappen**.
3. Klik in het Hallo-oplossing het dialoogvenster Eigenschappen op **opstartproject**, klikt u vervolgens op Hallo **meerdere opstartprojecten** knop. Zorg ervoor dat **EchoService** verschijnt eerst in de lijst Hallo.
4. Set Hallo **actie** in voor beide Hallo **EchoService** en **EchoClient** projecten te**Start**.

    ![][5]
5. Klik op **Projectafhankelijkheden**. In Hallo **projecten** de optie **EchoClient**. In Hallo **is afhankelijk van** zorg **EchoService** is ingeschakeld.

    ![][6]
6. Klik op **OK** toodismiss hello **eigenschappen** dialoogvenster.
7. Druk op **F5** toorun beide projecten.
8. Beide consolevensters openen en u vragen om Hallo naamruimtenaam. Hallo service moet eerst uitvoeren, dus in Hallo **EchoService** consolevenster, voert Hallo-naamruimte in en druk vervolgens op **Enter**.
9. U wordt vervolgens nogmaals om uw SAS-sleutel gevraagd. Voer Hallo SAS-sleutel in en druk op ENTER.

    Hier volgt een voorbeeld van uitvoer van Hallo-consolevenster. Houd er rekening mee dat Hallo waarden die hier zijn bijvoorbeeld alleen bedoeld.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    Hallo-servicetoepassing geeft toohello venster Hallo adres van de console waarop luistert, zoals in Hallo voorbeeld te volgen.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. In Hallo **EchoClient** consolevenster, voert u dezelfde informatie die u eerder hebt opgegeven voor de servicetoepassing Hallo Hallo. Ga als volgt Hallo vorige stappen tooenter Hallo dezelfde Servicenaamruimte en SAS waarden voor de clienttoepassing Hallo sleutel.
11. Na het invoeren van deze waarden Hallo client Hiermee opent u een kanaal toohello-service en de prompts tooenter u wat tekst, zoals in de volgende console-Uitvoervoorbeeld Hallo.

    `Enter text tooecho (or [Enter] tooexit):`

    Voer enkele tekst toosend toohello-servicetoepassing en druk op Enter. Deze tekst toohello service via Hallo Echo-servicebewerking is verzonden en wordt weergegeven in het serviceconsolevenster zoals in de volgende voorbeelduitvoer Hallo Hallo.

    `Echoing: My sample text`

    Hallo-clienttoepassing ontvangt de retourwaarde Hallo Hallo `Echo` bewerking, waarmee de oorspronkelijke tekst hello en verwerkt deze tooits consolevenster. Hallo volgt voorbeelduitvoer van Hallo clientconsolevenster.

    `Server echoed: My sample text`
12. U kunt doorgaan met het verzenden van berichten van Hallo client toohello-service op deze manier. Wanneer u klaar bent, drukt u op Enter in Hallo client en service-console windows tooend beide toepassingen.

## <a name="next-steps"></a>Volgende stappen

Deze zelfstudie hebt u geleerd hoe Hallo mogelijkheden van Service Bus Relay WCF toobuild een Azure-Relay-clienttoepassing en het gebruik van de service. Voor een vergelijkbare zelfstudie waarin [Service Bus-berichtenservice](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), Zie [aan de slag met Service Bus-wachtrijen](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn meer informatie over Azure-Relay, Zie Hallo volgende onderwerpen.

* [Overzicht van Azure Service Bus-architectuur](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Overzicht van Azure Relay](relay-what-is-it.md)
* [Hoe toouse Hallo WCF relay-service met .NET](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
