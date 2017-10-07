---
title: aaaGet de slag met Azure Relay WCF-relays in .NET | Microsoft Docs
description: Meer informatie over hoe Azure Relay WCF toouse tooconnect twee toepassingen die worden gehost op verschillende locaties doorstuurt.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Hoe toouse Azure Relay WCF doorstuurt met .NET
Dit artikel wordt beschreven hoe toouse hello Azure Relay-service. Hallo-voorbeelden zijn geschreven in C# en gebruiken van Hallo Windows Communication Foundation (WCF) API met extensies die deel uitmaken Hallo Service Bus-assembly. Zie voor meer informatie over Azure relay Hallo [Azure Relay overzicht](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>Wat is de Relay WCF?

Hello Azure [ *WCF Relay* ](relay-what-is-it.md) service kunt u toobuild hybride toepassingen die worden uitgevoerd in een Azure-datacenter en uw eigen on-premises bedrijfsomgeving. Hallo relay-service dit is mogelijk doordat u toosecurely Windows Communication Foundation (WCF)-services die zich bevinden in een zakelijke enterprise netwerk toohello openbare cloud, zonder dat een firewallverbinding hoeft tooopen of een vereiste weergeven Tussenkomende wijzigingen tooa bedrijfsnetwerkinfrastructuur.

![WCF Relay-concepten](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Azure Relay kunt u toohost WCF-services in uw bestaande bedrijfsomgeving. U kunt vervolgens delegeren luisteren naar binnenkomende sessies en aanvragen toothese WCF services toohello relay-service actief is in Azure. Hierdoor kunt u tooexpose deze services tooapplication code die wordt uitgevoerd in Azure, of toomobile werknemers of extranetpartneromgevingen. Relay kunt u toosecurely bepalen wie toegang deze services heel nauwkeurig tot. Het biedt een krachtige en veilige manier tooexpose functies en gegevens van uw bestaande bedrijfsoplossingen en profiteren van deze vanuit Hallo cloud.

Dit artikel wordt beschreven hoe toouse Azure Relay toocreate een WCF-webservice weergegeven met behulp van een TCP-kanaalbinding waarmee een beveiligde communicatie tussen twee partijen wordt geïmplementeerd.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Hallo Service Bus NuGet-pakket
Hallo [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is Hallo gemakkelijkste manier tooget Hallo Service Bus-API en tooconfigure uw toepassing met alle Hallo Service Bus-afhankelijkheden. tooinstall hello NuGet-pakket in uw project Hallo te volgen:

1. Klik in Solution Explorer met de rechtermuisknop op **Verwijzingen** en klik vervolgens op **NuGet-pakketten beheren**.
2. Zoek naar 'Service Bus' en selecteer Hallo **Microsoft Azure Service Bus** item. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens Hallo in het dialoogvenster te volgen:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Weergeven en gebruiken van een SOAP-webservice met TCP
een bestaande WCF SOAP-webservice voor extern verbruik tooexpose, moet u wijzigingen toohello servicebindingen en -adressen. Hiervoor wijzigingen tooyour configuratiebestand of codewijzigingen nodig codewijzigingen, afhankelijk van hoe u hebt ingesteld en de WCF-services zijn geconfigureerd. Houd er rekening mee dat WCF u toohave kunt meerdere netwerkeindpunten via dezelfde service Hallo, zodat u kunt behouden Hallo bestaande interne eindpunten tijdens het toevoegen van de relay-eindpunten voor externe toegang op Hallo dezelfde tijd.

In deze taak bouwen van een eenvoudige WCF-service en een relay-listener tooit toevoegen. In deze oefening wordt ervan uitgegaan dat enigszins bekend bent met Visual Studio en daarom komt niet in detail behandeld alle Hallo details van een project maken. In plaats daarvan ligt de nadruk op Hallo-code.

Voordat u deze stappen begint, voert u hello te volgen procedure tooset van uw omgeving:

1. Maak in Visual Studio een consoletoepassing die twee projecten 'Client' en 'Service' binnen de oplossing Hallo bevat.
2. Hallo Service Bus NuGet-pakket tooboth projecten toevoegen. Dit pakket voegt alle Hallo vereiste assembly-verwijzingen tooyour projecten.

### <a name="how-toocreate-hello-service"></a>Hoe toocreate Hallo service
Maak eerst Hallo-service zelf. Een WCF-service bestaat uit ten minste drie onderdelen:

* De definitie van een contract waarmee wordt beschreven welke berichten worden uitgewisseld en welke bewerkingen zijn toobe aangeroepen.
* Implementatie van deze overeenkomst.
* Host die als host fungeert voor Hallo WCF-service en beschrijft de verschillende eindpunten.

Hallo-codevoorbeelden in deze sectie hebben betrekking op elk van deze onderdelen.

Hallo-contract wordt één bewerking gedefinieerd `AddNumbers`, die twee getallen worden opgeteld en Hallo resultaat retourneert. Hallo `IProblemSolverChannel` interface schakelt Hallo client toomore eenvoudig hello proxy levensduur beheren. Het wordt aanbevolen een dergelijke interface te maken. Het is een goed idee tooput dit contract definitie in een afzonderlijk bestand, zodat u kunt verwijzen naar dit bestand uit uw 'Client' en de 'Service'-projecten, maar u kunt ook Hallo code naar beide projecten kopiëren.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

Met Hallo contract aanwezig is Hallo-implementatie als volgt uit:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Een servicehost via een programma configureren
U kunt nu Hallo service hosten met Hallo contract en implementatie in plaats. Hosting vindt plaats in een [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, die zorgt voor het beheren van exemplaren van Hallo-service en hosts Hallo eindpunten die naar berichten luisteren. Hallo volgende code wordt geconfigureerd voor Hallo met zowel een regulier lokaal eindpunt als een relay eindpunt tooillustrate Hallo uiterlijk, naast elkaar van interne en externe eindpunten. Vervang de tekenreeks Hallo *naamruimte* met de naamruimtenaam van uw en *yourKey* met Hallo SAS-sleutel die u hebt verkregen in de vorige instellingsstap Hallo.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

In voorbeeld hello, maakt u twee eindpunten die op Hallo dezelfde implementatie contract. Een lokale is en een eindpunt is geprojecteerd via Azure Relay. Hallo belangrijke verschillen tussen deze twee zijn Hallo bindingen; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) voor Hallo lokale en [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) voor Hallo relay eindpunt en hello-mailadressen. Hallo lokale eindpunt heeft een lokaal netwerkadres met een afzonderlijke poort. Hallo relay-eindpunt heeft een eindpuntadres samengesteld van Hallo tekenreeks `sb`, uw naamruimtenaam en Hallo pad 'Solver '.' Dit resulteert in Hallo URI `sb://[serviceNamespace].servicebus.windows.net/solver`, service-eindpunt Hallo identificeren als een Service Bus (relais) TCP-eindpunt met een volledig gekwalificeerde externe DNS-naam. Als u Hallo code Hallo tijdelijke aanduidingen vervangt in Hallo plaatsen `Main` functie Hallo **Service** toepassing, hebt u een functionele service. Als u wilt dat uw toolisten service uitsluitend op Hallo relay, verwijdert u Hallo lokaal eindpunt declaratie.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Een ServiceHost configureren in Hallo App.config-bestand
U kunt ook configureren Hallo-host met behulp van Hallo App.config-bestand. Hallo servicehostingcode in dit geval wordt weergegeven in het volgende voorbeeld Hallo.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

Hallo-eindpuntdefinities worden verplaatst naar Hallo App.config-bestand. Hallo NuGet-pakket is al een reeks definities toohello App.config-bestand toegevoegd die zijn vereist Hallo configuratie-extensies voor Azure Relay. Hallo volgende voorbeeld met Hallo exacte equivalent van de vorige code Hallo moet worden weergegeven direct onder Hallo **system.serviceModel** element. In dit voorbeeld wordt ervan uitgegaan dat uw project C#-naamruimte de naam **Service** heeft.
Vervang de tijdelijke aanduidingen Hallo met de naam van de relay-naamruimte en SAS-sleutel.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

Nadat u deze wijzigingen aanbrengt, Hallo-service wordt gestart als voorheen maar met twee live eindpunten: een lokaal en één luisteren in Hallo cloud.

### <a name="create-hello-client"></a>Hallo-client maken
#### <a name="configure-a-client-programmatically"></a>Een client via een programma configureren
tooconsume Hallo-service, kunt u een WCF-client met samenstellen een [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object. Service Bus maakt gebruik van een beveiligingsmodel op basis van tokens dat wordt geïmplementeerd met SAS. Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) klasse vertegenwoordigt een beveiligingstokenprovider met ingebouwde factorymethoden waarmee een aantal bekende token providers retourneren. Hallo volgende voorbeeld wordt Hallo [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) methode toohandle Hallo verkrijging van Hallo juiste SAS-token. Hallo-naam en sleutel zijn verkregen via Hallo beheerportal, zoals beschreven in de vorige sectie Hallo.

Eerste, verwijzing of copy Hallo `IProblemSolver` Contractcode van Hallo-service in uw clientproject.

Vervang vervolgens Hallo-code in Hallo `Main` methode voor het Hallo-client opnieuw Hallo tijdelijke aanduiding voor tekst vervangen door uw relay-naamruimte en SAS-sleutel.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

U kunt nu opbouwen Hallo-client en Hallo-service, ze uit te voeren (Hallo service eerst uitvoeren), Hallo client roept Hallo-service en wordt afgedrukt **9**. U kunt Hallo-client en server op verschillende computers uitvoeren zelfs in netwerken en Hallo communicatie nog steeds werken. Hallo-clientcode kunt ook in Hallo cloud of lokaal uitvoeren.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Een client in Hallo App.config-bestand configureren
Hallo volgende code toont hoe tooconfigure Hallo client met Hallo App.config-bestand.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Hallo-eindpuntdefinities worden verplaatst naar Hallo App.config-bestand. Hallo volgende voorbeeld is hetzelfde als Hallo code eerder is vermeld, hello, ziet er direct onder Hallo `<system.serviceModel>` element. Hier, als voorheen, moet u vervangen Hallo tijdelijke aanduidingen door uw relay-naamruimte en SAS-sleutel.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>Volgende stappen
Nu u de basisbeginselen van Azure Relay Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.

* [Wat is Azure Relay?](relay-what-is-it.md)
* [Overzicht van Azure Service Bus-architectuur](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Download Service Bus-voorbeelden van [Azure-voorbeelden] [ Azure samples] of Raadpleeg Hallo [overzicht van Service Bus-voorbeelden][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
