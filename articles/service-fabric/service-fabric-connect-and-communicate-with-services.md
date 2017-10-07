---
title: aaaConnect en communiceren met services in Azure Service Fabric | Microsoft Docs
description: Ontdek hoe tooresolve, verbinding maken en communiceren met Service Fabric-services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Verbinding maken en te communiceren met Service Fabric-services
In Service Fabric, een service wordt uitgevoerd ergens in een Service Fabric-cluster, doorgaans verdeeld over meerdere virtuele machines. Het kan worden verplaatst vanaf één locatie-tooanother op Hallo service-eigenaar, hetzij automatisch door Service Fabric. Services is niet statisch gebonden tooa bepaalde machine of het adres.

Een Service Fabric-toepassing in het algemeen bestaat uit veel verschillende services, waarbij elke service een speciale taak uitvoert. Deze services kunnen communiceren met elkaar tooform een volledige functie, zoals de rendering van verschillende onderdelen van een webtoepassing. Er zijn ook toepassingen die verbinding tooand maken met services communiceren client. Dit document wordt beschreven hoe tooset communicatie met en tussen uw services in Service Fabric.

Servicecommunicatie wordt ook beschreven in deze video van Microsoft Virtual Academy:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Breng uw eigen protocol
Service Fabric helpt Hallo levenscyclus van uw services beheren, maar maakt geen nemen van beslissingen over wat uw services doen. Dit omvat communicatie. Wanneer uw service wordt geopend door Service Fabric, dat wil zeggen van uw service kans tooset u een eindpunt voor binnenkomende aanvragen, u ongeacht stack-protocol of communicatie met. Uw service luistert op een normale **IP: poort** adres met behulp van een adresschema gebruiken, zoals een URI. Meerdere service-exemplaren of replica's kunnen een hostproces delen in dat geval ze hetzij toouse verschillende poorten moet of gebruik een mechanisme met delen van de poort, zoals Hallo http.sys kernelstuurprogramma in Windows. In beide gevallen moet elke service-exemplaar of de replica in een hostproces uniek adresseerbaar zijn.

![Service-eindpunten][1]

## <a name="service-discovery-and-resolution"></a>Servicedetectie en oplossing
Services kunnen in een gedistribueerde systeem verplaatsen van één machine tooanother gedurende een bepaalde periode. Dit kan gebeuren om verschillende redenen, waaronder resourceverdeling, upgrades, failovers of scale-out. Dit betekent dat adressen van de service-eindpunten wijzigen, omdat de service Hallo toonodes met verschillende IP-adressen wordt verplaatst en op andere poorten kan openen als Hallo-service een dynamisch geselecteerde poort gebruikt.

![Distributie van services][7]

Service Fabric bevat een detectie en de resolutie service genoemd Hallo Naming Service. Hallo onderhoudt Naming Service een tabel die is toegewezen met de naam service-exemplaren toohello eindpuntadressen die ze luisteren op. Alle benoemde service-exemplaren in Service Fabric unieke namen weergegeven als URI's, bijvoorbeeld hebben `"fabric:/MyApplication/MyService"`. Hallo-naam van Hallo-service wordt niet gewijzigd tijdens de levensduur Hallo van Hallo-service, maar alleen Hallo endpoint-adressen die wijzigen kunnen wanneer services verplaatst. Dit is vergelijkbaar toowebsites die constante URL's, maar waarbij Hallo IP-adres kan worden gewijzigd. En vergelijkbare tooDNS op Hallo web, die wordt omgezet websiteadressen URL's tooIP, Service Fabric heeft een registrar dat is toegewezen adres van de service namen tootheir-eindpunt.

![Service-eindpunten][2]

Op te lossen en verbinding maken met tooservices omvat Hallo volgende stappen uit in een lus uitgevoerd:

* **Los**: Get Hallo eindpunt dat een service is gepubliceerd vanuit Hallo Naming Service.
* **Verbinding maken met**: toohello service verbinding kunnen maken via het protocol ongeacht gebruikt op dat eindpunt.
* **Probeer**: een verbindingspoging kan mislukken voor een willekeurig aantal redenen, bijvoorbeeld als Hallo-service is verplaatst, omdat het eindpuntadres voor Hallo laatste tijd Hallo is opgelost. In dat geval Hallo los voorafgaand aan en maak verbinding stappen moeten toobe opnieuw geprobeerd en deze cyclus wordt herhaald totdat het Hallo-verbinding is geslaagd.

## <a name="connecting-tooother-services"></a>Verbinding maken met tooother services
Services tooeach verbinding maken met andere in een cluster in het algemeen rechtstreeks toegang tot Hallo eindpunten van andere services omdat Hallo knooppunten in een cluster op Hallo hetzelfde lokale netwerk. toomake is eenvoudiger tooconnect tussen services, Service Fabric bevat aanvullende services die gebruikmaken van Hallo Naming Service. Een DNS-service en een omgekeerde proxy-service.


### <a name="dns-service"></a>DNS-service
Aangezien veel services, vooral beperkte services, een bestaande URL-naam hebben kunnen, kunnen tooresolve wordt deze met Hallo standaard DNS-protocol (plaats Hallo Naming Service protocol) is zeer handig, met name in de toepassing 'lift- en verschuiven' scenario's. Dit is precies welke Hallo DNS-service gebruikt. Dit kunt u toomap DNS-namen tooa servicenaam en daarom los eindpunt IP-adressen. 

Als weergegeven in Hallo maps volgende diagram wordt Hallo DNS-service, die wordt uitgevoerd in Hallo Service Fabric-cluster, DNS-namen tooservice namen, die vervolgens door Hallo Naming Service tooreturn Hallo eindpunt adressen tooconnect om te worden opgelost. Hallo DNS-naam voor het Hallo-service is opgegeven op Hallo moment gemaakt. 

![Service-eindpunten][9]

Voor meer informatie over hoe toouse Hallo DNS-service zien [DNS-service in Azure Service Fabric](service-fabric-dnsservice.md) artikel.

### <a name="reverse-proxy-service"></a>Reverse proxy-service
Hallo omgekeerde proxy adressen services in Hallo cluster die beschrijft de HTTP-eindpunten, met inbegrip van HTTPS. Hallo omgekeerde proxy vereenvoudigt het aanroepen van andere services en hun methoden wanneer er een specifieke URI-notatie ingangen Hallo oplossen, verbinding maken, opnieuw proberen stappen die nodig zijn voor één service toocommunicate met het gebruik van een andere Hallo Naming Service. Met andere woorden, verbergt het Hallo Naming Service van u bij het aanroepen van andere services door het maken van dit net zo eenvoudig als het aanroepen van een URL.

![Service-eindpunten][10]

Raadpleeg voor meer informatie over hoe toouse Hallo reverse proxy-service [omgekeerde proxy in Azure Service Fabric](service-fabric-reverseproxy.md) artikel.

## <a name="connections-from-external-clients"></a>Verbindingen met externe clients
Services tooeach verbinding maken met andere in een cluster in het algemeen rechtstreeks toegang tot Hallo eindpunten van andere services omdat Hallo knooppunten in een cluster op Hallo hetzelfde lokale netwerk. In sommige omgevingen echter een cluster mogelijk achter een load balancer waarmee externe inkomend verkeer via een beperkte set van poorten. Services kunnen nog steeds in dergelijke gevallen met elkaar communiceren en -adressen in door Hallo Naming Service, maar extra stappen moeten worden genomen tooallow externe clients tooconnect tooservices oplossen.

## <a name="service-fabric-in-azure"></a>Service Fabric in Azure
Een Service Fabric-cluster in Azure wordt geplaatst achter een Load Balancer van Azure. Alle externe verkeer toohello cluster moet voldoen via Hallo load balancer. Hallo load balancer wordt automatisch doorsturen van verkeer inkomend verkeer op een willekeurige opgegeven poort tooa *knooppunt* die Hallo dezelfde poort open is. Hello Azure Load Balancer alleen bewust van poorten geopend op Hallo *knooppunten*, niet weet over poorten openen door afzonderlijke *services*.

![Azure Load Balancer en Service Fabric-topologie][3]

Bijvoorbeeld, in volgorde tooaccept externe verkeer op poort **80**, Hallo dingen na moet worden geconfigureerd:

1. Schrijven van een service die op poort 80 luistert. Configureren van poort 80 in ServiceManifest.xml Hallo-service en open een listener in Hallo-service, bijvoorbeeld een host zichzelf webserver.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Een Service Fabric-Cluster in Azure maken en Geef poort **80** als aangepaste endpoint-poort voor het knooppunttype Hallo die als host Hallo-service fungeert. Als u meer dan één knooppunttype hebt, kunt u instellen een *plaatsing beperking* op Hallo service tooensure alleen wordt uitgevoerd op Hallo knooppunttype met aangepaste eindpuntpoort Hallo geopend.

    ![Een poort op een knooppunttype openen][4]
3. Nadat u Hallo-cluster is gemaakt, configureert u hello Azure Load Balancer in van het cluster Hallo resourcegroep tooforward verkeer op poort 80. Wanneer u een cluster via hello Azure-portal, is deze ingesteld automatisch voor elke aangepaste endpoint-poort die is geconfigureerd.

    ![Doorsturen van verkeer in hello Azure Load Balancer][5]
4. maakt gebruik van Azure Load Balancer of een test-toodetermine Hallo of niet toosend verkeer tooa bepaald knooppunt. Hallo-test regelmatig controles een eindpunt op elk knooppunt toodetermine of Hallo knooppunt reageert. Als tooreceive een antwoord Hallo test na een geconfigureerde aantal keren mislukt, stopt Hallo load balancer verkeer toothat knooppunt verzenden. Bij het maken van een cluster via hello Azure-portal is een test automatisch ingesteld voor elke aangepaste endpoint-poort die is geconfigureerd.

    ![Doorsturen van verkeer in hello Azure Load Balancer][8]

Het is belangrijk tooremember die hello Azure Load Balancer- en Hallo test alleen Hallo kent *knooppunten*, niet Hallo *services* uitgevoerd op Hallo knooppunten. Hello Azure Load Balancer wordt altijd verkeer toonodes die toohello test reageren verzenden, dus wees voorzichtig tooensure services beschikbaar zijn op Hallo knooppunten die kunnen toorespond toohello test.

## <a name="reliable-services-built-in-communication-api-options"></a>Betrouwbare Services: Opties van de ingebouwde communicatie API
Hallo Reliable Services framework wordt geleverd met verschillende vooraf samengestelde communicatieopties. Hallo beslissing over welke een voor u geschikt is afhankelijk van Hallo keuze Hallo programming model, Hallo communicatie framework en Hallo programmeertaal die uw services zijn geschreven in.

* **Er is geen specifieke protocol:** als u niet een bepaalde keuze van communicatie framework hebt, maar u wilt dat tooget iets up-to-date en actieve snel, is Hallo ideale oplossing voor u [remoting service](service-fabric-reliable-services-communication-remoting.md), waardoor externe procedure sterk getypeerde roept voor Reliable Services en Reliable Actors. Dit is Hallo eenvoudigste en snelste manier tooget gestart met servicecommunicatie. Service voor externe toegang zorgt omzetting van de service-adressen, verbinding, probeer het opnieuw en foutafhandeling. Dit is beschikbaar voor zowel C# en Java-toepassingen.
* **HTTP**: voor taal networkdirect communicatie, HTTP biedt een keuze industriestandaard met hulpprogramma's en HTTP-servers die beschikbaar zijn in verschillende talen, geheel ondersteund door Service Fabric. Services kunnen elke beschikbaar is, met inbegrip van HTTP-stack gebruiken [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) voor C#-toepassingen. Hallo kunnen gebruikmaken van clients die zijn geschreven in C# `ICommunicationClient` en `ServicePartitionClient` klassen, terwijl voor Java, gebruik Hallo `CommunicationClient` en `FabricServicePartitionClient` klassen, [voor omzetting van de service, HTTP-verbindingen en probeer het opnieuw lussen](service-fabric-reliable-services-communication.md).
* **WCF**: als u bestaande code die gebruikmaakt van WCF als uw communicatie-framework hebt, dan kunt u Hallo `WcfCommunicationListener` voor serverzijde Hallo en `WcfCommunicationClient` en `ServicePartitionClient` klassen voor het Hallo-client. Dit echter is alleen beschikbaar voor C#-toepassingen op Windows gebaseerde clusters. Zie voor meer informatie in dit artikel over [WCF-gebaseerde implementatie van Hallo communicatiestack](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Met behulp van aangepaste protocollen en andere frameworks communicatie
Services kunnen gebruiken elke protocol of elk framework voor communicatie gebruikt, ongeacht of dit een aangepast binaire protocol via TCP-sockets of streaming-gebeurtenissen via [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) of [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/). Service Fabric bevat communicatie API's die u uw communicatiestack in, sluit kunt terwijl alle Hallo toodiscover werken en verbinding maken is gescheiden van u. Raadpleeg dit artikel over Hallo [betrouwbare Service communicatiemodel](service-fabric-reliable-services-communication.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over concepten Hallo en beschikbare API's in Hallo [Reliable Services communicatiemodel](service-fabric-reliable-services-communication.md), vervolgens snel aan de slag met [remoting service](service-fabric-reliable-services-communication-remoting.md) of gedetailleerde toolearn hoe ga toowrite een communicatie-listener met [Web-API met OWIN zelf host](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
