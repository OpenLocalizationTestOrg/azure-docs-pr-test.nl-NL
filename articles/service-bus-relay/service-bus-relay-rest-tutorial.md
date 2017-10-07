---
title: aaaService Bus REST-zelfstudie met Azure Relay | Microsoft Docs
description: Bouw een eenvoudige Azure Service Bus relay-hosttoepassing een REST gebaseerde interface.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Azure WCF Relay REST-zelfstudie

Deze zelfstudie wordt beschreven hoe de toepassing die een REST gebaseerde interface voor het hosten van toobuild een eenvoudige Azure-Relay. REST kan een webclient, zoals een webbrowser, tooaccess Hallo Service Bus-API's via HTTP-aanvragen.

Hallo-zelfstudie wordt gebruikgemaakt van Hallo Windows Communication Foundation (WCF) REST programming model tooconstruct een REST-service op de Service Bus. Zie voor meer informatie [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) en [Services ontwerpen en implementeren](/dotnet/framework/wcf/designing-and-implementing-services) in Hallo WCF-documentatie.

## <a name="step-1-create-a-namespace"></a>Stap 1: Een naamruimte maken

met behulp van toobegin Hallo relay-functies in Azure, moet u eerst een Servicenaamruimte maken. Een naamruimte biedt een scoping container voor het verwerken van Azure-resources in uw toepassing. Ga als volgt Hallo [hier instructies](relay-create-namespace-portal.md) toocreate een Relay-naamruimte.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Stap 2: Een toouse REST gebaseerd WCF-servicecontract met Azure Relay definiëren

Wanneer u een service WCF REST-stijl maakt, moet u Hallo contract definiëren. Hallo contract geeft aan welke bewerkingen Hallo host ondersteunt. Een servicebewerking kan worden beschouwd als een webservicemethode. Contracten worden gemaakt door een C++-, C#- of Visual Basic-interface te definiëren. Elke methode in Hallo interface komt tooa specifieke servicebewerking overeen. Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) -kenmerk moet worden toegepast tooeach interface en Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) kenmerk moet toegepaste tooeach bewerking. Als een methode in een interface met Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) heeft geen Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), die methode niet weergegeven. Hallo-code die wordt gebruikt voor deze taken wordt weergegeven in het Hallo-voorbeeld Hallo procedure te volgen.

Hallo belangrijkste verschil tussen een WCF-contract en een REST-stijlcontract is Hallo toevoeging van een eigenschap toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Deze eigenschap kunt u een methode in uw interfacemethode tooa op Hallo toomap andere kant van het Hallo-interface. We gebruiken in dit geval [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink een tooHTTP methode GET. Hierdoor kan Service Bus tooaccurately ophalen en interpreteren opdrachten toohello interface verzonden.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate een contract met een interface

1. Open Visual Studio als beheerder: klik met de rechtermuisknop Hallo programma in Hallo **Start** menu en klik vervolgens op **als administrator uitvoeren**.
2. Maak een nieuw consoletoepassingsproject aan. Klik op Hallo **bestand** menu en selecteer **nieuw**, selecteer daarna **Project**. In Hallo **nieuw Project** in het dialoogvenster klikt u op **Visual C#**, selecteer Hallo **consoletoepassing** -sjabloon en noem deze **ImageListener**. Standaard-Hallo **locatie**. Klik op **OK** toocreate Hallo project.
3. Voor een C#-project maakt Visual Studio een `Program.cs`-bestand. Deze klasse bevat een lege `Main()` methode, vereist voor een console application project toobuild correct.
4. Voeg verwijzingen tooService Bus en **System.ServiceModel.dll** toohello project door Hallo Service Bus NuGet-pakket installeert. Dit pakket wordt automatisch toegevoegd verwijzingen toohello Service Bus-bibliotheken, evenals Hallo WCF **System.ServiceModel**. Klik in Solution Explorer met de rechtermuisknop op Hallo **ImageListener** project en klik vervolgens op **NuGet-pakketten beheren**. Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`. Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.
5. U moet expliciet een verwijzing te toevoegen**System.ServiceModel.Web.dll** toohello project:
   
    a. Klik in Solution Explorer met de rechtermuisknop op Hallo **verwijzingen** map onder Hallo projectmap en klik vervolgens op **verwijzing toevoegen**.
   
    b. In Hallo **verwijzing toevoegen** dialoogvenster vak, klikt u op Hallo **Framework** tabblad aan de linkerkant hello en in Hallo **Search** in het vak **System.ServiceModel.Web** . Selecteer Hallo **System.ServiceModel.Web** selectievakje en klik vervolgens op **OK**.
6. Voeg de volgende Hallo `using` instructies Hallo boven aan het bestand Program.cs Hallo.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is Hallo-naamruimte die programmatisch toegang toobasic onderdelen van WCF. Relay WCF maakt gebruik van veel van Hallo-objecten en kenmerken van WCF toodefine servicecontracten. U gebruikt deze naamruimte in de meeste van de relay-toepassingen. Op deze manier [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helpt bij het Hallo-kanaal is Hallo-object waarmee u contact met de Azure-Relay en Hallo clientwebbrowser opnemen definiëren. Ten slotte [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) bevat Hallo typen waarmee u toocreate webtoepassingen.
7. Wijzig de naam van Hallo `ImageListener` naamruimte te**Microsoft.ServiceBus.Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Direct na de Hallo na accolades openen van de naamruimtedeclaratie hello, definiëren een nieuwe interface met de naam **IImageContract** en toepassing hello **ServiceContractAttribute** kenmerk toohello interface met een waarde van `http://samples.microsoft.com/ServiceModel/Relay/`. Hallo naamruimtewaarde verschilt van Hallo-naamruimte die u gebruiken voor de hele Hallo bereik van uw code. Hallo naamruimtewaarde wordt gebruikt als een unieke id voor dit contract en moet versie-informatie. Zie [Serviceversiebeheer](http://go.microsoft.com/fwlink/?LinkID=180498) voor meer informatie. Het expliciet opgeven van Hallo-naamruimte voorkomt u dat standaardnaamruimtewaarde hello toohello contractnaam wordt toegevoegd.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Binnen Hallo `IImageContract` interface, declareert u een methode voor het Hallo één bewerking Hallo `IImageContract` contract zichtbaar gemaakt in Hallo interface en toepassing hello `OperationContractAttribute` toohello methode waarmee u tooexpose als onderdeel van Hallo openbare Service Bus-kenmerk contract.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. In Hallo **OperationContract** kenmerk, het toevoegen van Hallo **WebGet** waarde.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Dit doet, kunnen Hallo relay-service tooroute HTTP GET-te aanvragen`GetImage`, en tootranslate Hallo retourwaarden van `GetImage` in een HTTP GETRESPONSE-antwoord. Later in Hallo zelfstudie gebruikt u een web browser tooaccess deze methode als toodisplay Hallo installatiekopie in de browser Hallo.
11. Direct na Hallo `IImageContract` definitie een kanaal dat eigenschappen van beide Hallo overneemt declareren `IImageContract` en `IClientChannel` interfaces.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Een kanaal is Hallo WCF-object waarmee Hallo-service en de client informatie tooeach andere doorgeven. Later, maakt u Hallo channel in uw hosttoepassing. Azure Relay gebruikt dit kanaal toopass Hallo HTTP GET-aanvragen van Hallo browser tooyour **GetImage** implementatie. Hallo relay gebruikt ook Hallo kanaal tootake hello **GetImage** waarde retourneren en zet deze om naar een HTTP GETRESPONSE voor de clientbrowser Hallo.
12. Van Hallo **bouwen** menu, klikt u op **Build Solution** tooconfirm Hallo juistheid van uw werk tot nu toe.

### <a name="example"></a>Voorbeeld
Hallo volgende code toont een eenvoudige interface die een Relay WCF-contract wordt gedefinieerd.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Stap 3: Een REST gebaseerd WCF-servicecontract toouse Service Bus implementeren
Maken van een REST-stijl WCF Relay-service, moet eerst de Hallo-contract wordt gedefinieerd door middel van een interface te maken. de volgende stap Hallo is tooimplement Hallo-interface. Dit omvat het maken van een klasse met de naam **ImageService** die gebruiker gedefinieerde Hallo implementeert **IImageContract** interface. Nadat u Hallo contract implementeert, configureert u Hallo-interface met een App.config-bestand. Hallo-configuratiebestand bevat de benodigde gegevens voor het Hallo-toepassing, zoals het Hallo-naam van Hallo-service, Hallo-naam van het Hallo-contract en Hallo type protocol dat wordt gebruikt toocommunicate met Hallo relay-service. Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.

Als met de vorige stappen hello, er is weinig verschil tussen het implementeren van een REST-stijlcontract en een Relay WCF-contract.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>Service Bus-contract tooimplement een REST-stijl
1. Maak een nieuwe klasse met de naam **ImageService** direct na de definitie van Hallo Hallo **IImageContract** interface. Hallo **ImageService** klasse implementeert Hallo **IImageContract** interface.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Vergelijkbare tooother interface-implementaties, kunt u Hallo definitie implementeren in een ander bestand. Voor deze zelfstudie Hallo-implementatie wordt weergegeven in hetzelfde bestand als de interfacedefinitie Hallo Hallo en `Main()` methode.
2. Toepassing hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) kenmerk toohello **IImageService** klasse tooindicate die klasse Hallo is een implementatie van een WCF-contract.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Zoals eerder is vermeld, is deze naamruimte geen traditionele naamruimte, In plaats daarvan uitmaakt het deel van Hallo WCF-architectuur waarmee Hallo contract identificeert. Zie voor meer informatie, Hallo [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) onderwerp in Hallo WCF-documentatie.
3. Voeg een jpg-installatiekopie tooyour-project.  
   
    Dit is een afbeelding die Hallo-service wordt weergegeven in Hallo ontvangen van de browser. Klik met de rechtermuisknop op het project en klik op **Toevoegen**. Klik vervolgens op **Bestaand item**. Gebruik Hallo **Add Existing Item** dialoogvenster vak toobrowse tooan geschikt jpg en klik vervolgens op **toevoegen**.
   
    Wanneer u Hallo bestand toevoegt, zorg ervoor dat **alle bestanden** is geselecteerd in de volgende toohello van Hallo vervolgkeuzelijst **bestandsnaam:** veld. Hallo rest van deze handleiding wordt ervan uitgegaan dat Hallo naam van Hallo afbeelding 'image.jpg' is. Als u een ander bestand hebt, wordt toorename Hallo afbeelding, of wijzig uw toocompensate code.
4. er zeker die Hallo waarop service wordt uitgevoerd in Hallo installatiekopiebestand kan vinden toomake **Solution Explorer** met de rechtermuisknop op het Hallo-afbeeldingsbestand en klik vervolgens op **eigenschappen**. In Hallo **eigenschappen** deelvenster ingesteld **tooOutput Directory kopiëren** te**kopiëren indien nieuwer**.
5. Voeg een verwijzing toohello **System.Drawing.dll** assembly toohello project en ook toevoegen Hallo volgende gekoppelde `using` instructies.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. In Hallo **ImageService** klasse, het toevoegen van Hallo volgende constructor dat geladen bitmap Hallo en toosend bereidt het toohello clientbrowser.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Direct na de vorige code hello, voeg de volgende Hallo **GetImage** methode in Hallo **ImageService** klasse tooreturn een HTTP-bericht dat de installatiekopie Hallo bevat.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Maakt gebruik van deze implementatie **MemoryStream** tooretrieve Hallo installatiekopie en voorbereiden voor streaming toohello browser. Het Hallo stroompositie bij nul wordt gestart, declareert Hallo stroominhoud als jpeg en streams Hallo informatie.
8. Van Hallo **bouwen** menu, klikt u op **Build Solution**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>toodefine hello configuratie voor het uitvoeren van Hallo-webservice in Service Bus
1. In **Solution Explorer**, dubbelklikt u op **App.config** tooopen in Hallo Visual Studio-editor.
   
    Hallo **App.config** -bestand bevat de servicenaam hello, eindpunt (dat wil zeggen, Hallo locatie Azure Relay voor clients en hosts toocommunicate met elkaar biedt) en binding (Hallo type protocol dat wordt gebruikt toocommunicate). Hallo hier het belangrijkste verschil is dat Hallo geconfigureerd service-eindpunt verwijst tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.
2. Hallo `<system.serviceModel>` XML-element is een WCF-element dat een of meer services definieert. Hier is het gebruikte toodefine Hallo servicenaam en -eindpunt. Hallo Hallo onderaan in `<system.serviceModel>` element (maar nog steeds binnen `<system.serviceModel>`), Voeg een `<bindings>` -element waarvoor Hallo inhoud na. Hiermee definieert u Hallo bindingen in de toepassing hello gebruikt. U kunt meerdere bindingen definiëren, maar in deze zelfstudie definieert u er slechts één.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    Hallo vorige code definieert een Relay WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding met **relayClientAuthenticationType** instellen te**geen**. Met deze instelling geeft u aan dat voor een eindpunt dat deze binding gebruikt, geen clientreferentie is vereist.
3. Na het Hallo `<bindings>` element, Voeg een `<services>` element. Soortgelijke toohello bindingen kunt u meerdere services definiëren in een enkel configuratiebestand. In deze zelfstudie definieert u slechts een service.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Deze stap configureert u een service die gebruikmaakt van standaard Hallo eerder gedefinieerd **webHttpRelayBinding**. Gebruikt ook Hallo standaard **sbTokenProvider**, die is gedefinieerd in de volgende stap Hallo.
4. Na Hallo `<services>` element, maakt een `<behaviors>` element met Hallo inhoud te volgen, Vervang 'sas_key ' vervangen door Hallo *Shared Access Signature* (SAS)-sleutel die u eerder hebt verkregen via Hallo [Azure-portal ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Nog steeds in App.config in Hallo `<appSettings>` vervangen Hallo gehele gegevensbronwaarde met verbindingsreeks die u eerder hebt verkregen via de portal Hallo Hallo-element. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. Van Hallo **bouwen** menu, klikt u op **Build Solution** toobuild Hallo hele oplossing.

### <a name="example"></a>Voorbeeld
Hallo volgende code toont Hallo contract en de service-implementatie voor een op REST gebaseerde service die wordt uitgevoerd op de Service Bus met Hallo **WebHttpRelayBinding** binding.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hallo ziet volgende voorbeeld Hallo App.config-bestand dat is gekoppeld met Hallo-service.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Stap 4: Host Hallo REST gebaseerd WCF-service toouse Relay in Azure
Deze stap wordt beschreven hoe toorun een web service met een consoletoepassing met WCF Relay. Een volledig overzicht van Hallo code die is geschreven in deze stap wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.

### <a name="toocreate-a-base-address-for-hello-service"></a>een basisadres voor Hallo service toocreate
1. In Hallo `Main()` declaratie van de functie, maakt u een variabele toostore Hallo-naamruimte van uw project. Zorg ervoor dat tooreplace `yourNamespace` met Hallo-naam van Hallo Relay naamruimte die u eerder hebt gemaakt.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Service Bus maakt gebruik van Hallo-naam van uw naamruimte toocreate een unieke URI.
2. Maak een `Uri` exemplaar voor het basisadres Hallo van Hallo-service die is gebaseerd op Hallo-naamruimte.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate en Hallo WebServiceHost configureren
* Hallo web ServiceHost, met behulp van de URI-adres Hallo eerder hebt gemaakt in deze sectie maken.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    Hallo ServiceHost is Hallo WCF-object dat Hallo-hosttoepassing instantieert. In dit voorbeeld wordt doorgegeven Hallo type host dat u wilt dat toocreate (een **ImageService**), en ook Hallo-mailadres waarmee u tooexpose Hallo-hosttoepassing.

### <a name="toorun-hello-web-service-host"></a>toorun hello WebServiceHost
1. Hallo-service openen.
   
    ```csharp
    host.Open();
    ```
    Hallo-service wordt nu uitgevoerd.
2. Een bericht waarin staat dat Hallo-service wordt uitgevoerd en hoe toostop Hallo service weergegeven.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Wanneer u klaar bent, sluit u Hallo ServiceHost.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld bevat Hallo servicecontract en de implementatie uit de vorige stappen in Hallo zelfstudie en hosts Hallo service in een consoletoepassing. Compileren Hallo na de code in een uitvoerbaar bestand met de naam ImageListener.exe.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Hallo code compileren
Na het Hallo-oplossing bouwen, Hallo na toorun Hallo toepassing:

1. Druk op **F5**, of blader toohello uitvoerbaar bestandslocatie (ImageListener\bin\Debug\ImageListener.exe) toorun Hallo-service. Houd Hallo app wordt uitgevoerd, wordt dit tooperform Hallo volgende stap is vereist.
2. Kopieer en plak Hallo-adres van de opdrachtprompt Hallo in een browser toosee Hallo-installatiekopie.
3. Wanneer u klaar bent, drukt u op **Enter** in Hallo opdrachtprompt venster tooclose Hallo-app.

## <a name="next-steps"></a>Volgende stappen
Nu u een toepassing die gebruikmaakt van Hallo Service Bus relay-service hebt gemaakt, gaat u naar Hallo toolearn meer artikelen over Azure Relay te volgen:

* [Overzicht van Azure Service Bus-architectuur](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Overzicht van Azure Relay](relay-what-is-it.md)
* [Hoe toouse Hallo WCF relay-service met .NET](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
