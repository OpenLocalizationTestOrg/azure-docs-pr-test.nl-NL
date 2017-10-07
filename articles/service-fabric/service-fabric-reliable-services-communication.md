---
title: overzicht van de communicatie aaaReliable Services | Microsoft Docs
description: Overzicht van Hallo Reliable Services communicatiemodel, inclusief openen listeners van services, het omzetten van eindpunten en communicatie tussen services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Hoe toouse Hallo Reliable Services communicatie API 's
Azure Service Fabric als platform is volledig agnostisch over de communicatie tussen services. Alle protocollen en stacks zijn aanvaardbaar van UDP-tooHTTP. Is toohello service developer toochoose hoe services moeten communiceren. toepassingsframework voor Hallo Reliable Services biedt ingebouwde communicatie stacks en API's waarmee u toobuild kunt Communicatieonderdelen van uw aangepaste.

## <a name="set-up-service-communication"></a>Servicecommunicatie instellen
Hallo betrouwbare Services-API maakt gebruik van een eenvoudige interface voor servicecommunicatie. een eindpunt voor uw service tooopen gewoon deze interface implementeren:

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

Vervolgens kunt u uw communicatie-listener-implementatie toevoegen door deze terug te geven in een onderdrukking van de methode op basis van een service-klasse.

Voor stateless services:

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

Voor stateful services:

> [!NOTE]
> Stateful betrouwbare services worden nog niet ondersteund in Java.
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

In beide gevallen moet u een verzameling van listeners retourneren. Hierdoor kunnen de toolisten van uw service op meerdere eindpunten, met mogelijk verschillende protocollen, met behulp van meerdere listeners. Bijvoorbeeld, wellicht u een HTTP-listener en een afzonderlijke WebSocket-listener. Elke listener haalt u een naam en de resulterende verzameling Hallo *naam: adres* paren worden weergegeven als een JSON-object als een client Hallo luisterende adressen voor een service-exemplaar of een partitie aanvraagt.

In een stateless service retourneert Hallo onderdrukking een verzameling ServiceInstanceListeners. Een `ServiceInstanceListener` bevat een functie toocreate een `ICommunicationListener(C#) / CommunicationListener(Java)` en hieraan een naam. Voor stateful services retourneert Hallo onderdrukking een verzameling ServiceReplicaListeners. Dit is enigszins afwijken van het bijbehorende equivalent staatloze omdat een `ServiceReplicaListener` heeft een optie tooopen een `ICommunicationListener` op secundaire replica's. Niet alleen kunt u meerdere communicatielisteners gebruiken in een service, maar u kunt ook opgeven welke listeners accepteren van aanvragen op secundaire replica's en welke luistert alleen op primaire replica's.

Bijvoorbeeld, u kunt een ServiceRemotingListener RPC-aanroepen krijgt alleen op primaire replica's hebben en een tweede, aangepaste listener lezen waarmee aanvragen op de secundaire replica's via HTTP:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> Bij het maken van meerdere listeners voor een service wordt elke listener **moet** een unieke naam.
>
>

Ten slotte beschrijven Hallo-eindpunten die vereist voor de service in Hallo Hallo zijn [servicemanifest](service-fabric-application-model.md) onder de sectie Hallo voor eindpunten.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

Hallo communicatie listener toegang tot de Hallo eindpunt systeembronnen toegewezen tooit van Hallo `CodePackageActivationContext` in Hallo `ServiceContext`. Hallo-listener kunt vervolgens luisteren naar aanvragen wanneer deze wordt geopend starten.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Eindpunt resources zijn algemene toohello gehele servicepakket en ze worden toegewezen door de Service Fabric Hallo servicepakket is geactiveerd. Meerdere service replica's die worden gehost in dezelfde ServiceHost kan delen Hallo Hallo dezelfde poort. Dit betekent dat communicatie Hallo listener delen van de poort moet ondersteunen. Hallo aanbevolen manier om dit te doen voor Hallo communicatie listener toouse Hallo partitie-ID en replica-exemplaar-ID is bij het genereren van Hallo luister-adres.
>
>

### <a name="service-address-registration"></a>Registratie van de service-adres
Een systeemservice aangeroepen Hallo *Naming Service* wordt uitgevoerd op de Service Fabric-clusters. Hallo is Naming Service een registrar voor services en de adressen die elk exemplaar of de replica van Hallo service luistert op. Wanneer Hallo `OpenAsync(C#) / openAsync(Java)` methode van een `ICommunicationListener(C#) / CommunicationListener(Java)` is voltooid, wordt de return-waarde opgehaald in Hallo Naming Service geregistreerd. Deze waarde die wordt gepubliceerd in Hallo Naming Service is een tekenreeks waarvan de waarde van alles op alle zijn kan retourneren. Deze waarde is wat clients zien wanneer ze voor een adres voor de service Hallo van Hallo Naming Service vragen.

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

Service Fabric bevat API's waarmee de clients en andere services toothen vragen voor dit adres met de servicenaam. Dit is belangrijk omdat Hallo-serviceadres niet statisch is. Services worden in Hallo cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst. Dit is Hallo-mechanisme waarmee clients tooresolve Hallo adres voor een service luistert.

> [!NOTE]
> Voor een volledig overzicht van hoe toowrite een listener communicatie zien [Service Fabric-Web-API-services met OWIN zelf hosting](service-fabric-reliable-services-communication-webapi.md) voor C#, dat u uw eigen HTTP-server-implementatie voor Java schrijven kunt, Zie EchoServer toepassing voorbeeld op https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Communicatie met een service
Hallo betrouwbare Services API biedt Hallo bibliotheken toowrite clients die met de services communiceren te volgen.

### <a name="service-endpoint-resolution"></a>Service-eindpunt resolutie
eerste stap toocommunication Hallo met een service is tooresolve een eindpuntadres van Hallo partitie of het exemplaar van de gewenste tootalk op Hallo-service. Hallo `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` hulpprogrammaklasse is een eenvoudige primitief waarmee clients bepalen Hallo-eindpunt van een service tijdens runtime. In de Service Fabric-terminologie Hallo bepalen Hallo-eindpunt van een service wordt waarnaar wordt verwezen tooas hello *service-eindpunt resolutie*.

tooconnect tooservices binnen een cluster, ServicePartitionResolver kunnen worden gemaakt met de standaardinstellingen. Dit is Hallo-gebruik voor de meeste gevallen aanbevolen:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooconnect tooservices in een ander cluster, een ServicePartitionResolver kan worden gemaakt met een reeks cluster gateway eindpunten. Gateway-eindpunten zijn alleen verschillende eindpunten voor het verbinden van toohello hetzelfde cluster. Bijvoorbeeld:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

U kunt ook `ServicePartitionResolver` kan een functie worden opgegeven voor het maken van een `FabricClient` toouse intern:

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

`FabricClient`Hallo-object dat is gebruikt toocommunicate met Hallo Service Fabric-cluster voor verschillende bewerkingen op Hallo-cluster is. Dit is handig als u meer controle wilt over de interactie van een service-omzetter partitie met het cluster. `FabricClient`voert caching intern en is meestal dure toocreate, dus is het belangrijk tooreuse `FabricClient` exemplaren zo veel mogelijk.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Gebruikte tooretrieve Hallo-adres van een service of de partitie van een service voor gepartitioneerde services is een methode oplossen.

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

Een serviceadres kan worden omgezet eenvoudig met een ServicePartitionResolver, maar er is meer werk vereist tooensure Hallo opgelost adres correct kan worden gebruikt. De client moet toodetect of Hallo verbindingspoging is mislukt vanwege een tijdelijke fout en kan opnieuw worden uitgevoerd (bijv, service verplaatst of is tijdelijk niet beschikbaar), of een permanente fout (bijv, service is verwijderd of hello aangevraagde resource bestaat niet meer). Service-exemplaren of replica's kunnen verplaatsen van knooppunt toonode op elk gewenst moment om verschillende redenen. Hallo-serviceadres omgezet via ServicePartitionResolver mogelijk verlopen door de clientcode tooconnect probeert Hallo-tijd. In dat geval opnieuw Hallo-client moet toore oplossen Hallo adres. Hallo vorige bieden `ResolvedServicePartition` geeft aan dat omzetter behoeften tootry opnieuw Hallo plaats gewoon een cache-adres ophalen.

Normaal gesproken moet Hallo clientcode niet rechtstreeks met werken Hallo ServicePartitionResolver. Het is gemaakt en toocommunication client fabrieken in Hallo betrouwbare Services API doorgegeven. Hallo fabrieken Hallo conflictoplosser intern gebruiken toogenerate een client-object dat gebruikt toocommunicate met services worden kan.

### <a name="communication-clients-and-factories"></a>Communicatie-clients en fabrieken
Hallo communicatie factory bibliotheek implementeert een typische opnieuw patroon voor afhandeling van fouten die gemakkelijker is bezig met opnieuw verbindingen tooresolved service-eindpunten. Hallo factory-bibliotheek biedt een mechanisme voor opnieuw proberen Hallo terwijl u fout-handlers Hallo bieden.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Hiermee definieert u base Hallo-interface geïmplementeerd door een client-factory van communicatie waarmee clients die tooa Service Fabric-service communiceren kunnen wordt geproduceerd. implementatie van CommunicationClientFactory is afhankelijk van Hallo communicatiestack gebruikt door de Service Fabric-service Hallo waar Hallo client wil toocommunicate Hallo Hallo. Hallo betrouwbare Services API biedt een `CommunicationClientFactoryBase<TCommunicationClient>`. Dit biedt een basisimplementatie van Hallo CommunicationClientFactory interface en taken die algemene tooall Hallo communicatie stacks zijn worden uitgevoerd. (Deze taken omvatten het gebruik van een ServicePartitionResolver toodetermine Hallo service-eindpunt). Clients implementeren meestal Hallo abstracte CommunicationClientFactoryBase klasse toohandle logica die specifieke toohello communicatie-stack is.

Hallo communicatie-client wordt alleen een adres ontvangt en gebruikt deze tooconnect tooa service. Hallo-client kan elk protocol dat deze wil gebruiken.

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

de clientfabriek van Hallo is primair verantwoordelijk is voor het maken van clients voor communicatie. Voor clients die een permanente verbinding, zoals een HTTP-client niet onderhouden moet Hallo factory alleen toocreate en return Hallo-client. Andere protocollen die een permanente verbinding, zoals sommige binaire protocollen onderhoudt moeten ook worden gevalideerd door Hallo factory toodetermine of Hallo verbinding toobe opnieuw gemaakt moet.  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

Ten slotte is een uitzonderings-handler verantwoordelijk voor het bepalen welke actie tootake wanneer er een uitzondering optreedt. Uitzonderingen worden onderverdeeld in **herstelbare** en **niet-herstelbare**.

* **Niet-herstelbare** uitzonderingen gewoon back toohello aanroeper ophalen opnieuw.
* **herstelbare** uitzonderingen kunnen verder worden onderverdeeld in **tijdelijke** en **tijdelijke**.
  * **Tijdelijke** uitzonderingen zijn die eenvoudig kunnen worden verwerkt zonder het eindpuntadres Hallo-service opnieuw op te lossen. Hierbij gaat het tijdelijke netwerkproblemen of service-foutberichten dan degene die aangeven welke eindpuntadres Hallo-service bestaat niet.
  * **Niet-tijdelijke** uitzonderingen zijn die Hallo service-eindpunt adres toobe opnieuw opgelost vereisen. Het gaat hierbij om uitzonderingen die wijzen op Hallo service-eindpunt kan niet worden bereikt, die aangeeft Hallo-service heeft tooa ander knooppunt verplaatst.

Hallo `TryHandleException` maakt een beslissing over een bepaalde uitzondering. Als het **niet weet** welke toomake beslissingen over een uitzondering moet retourneren **false**. Als het **weet** welke toomake besluit moet dienovereenkomstig Hallo resultaat ingesteld en geretourneerd **true**.

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a>Kort samengevat
Met een `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, en `IExceptionHandler(C#) / ExceptionHandler(Java)` gebaseerd op een communicatieprotocol een `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` helemaal verpakt en biedt Hallo afhandeling van fouten en service partitie adres resolutie lus rond deze onderdelen.

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a>Volgende stappen
* Een voorbeeld bekijken van HTTP-communicatie tussen services in een [C#-voorbeeldproject op GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) of [Java-voorbeeldproject op GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Externe procedureaanroepen weer dat met Reliable Services voor externe toegang](service-fabric-reliable-services-communication-remoting.md)
* [Web-API die gebruikmaakt van OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [WCF-communicatie met behulp van Reliable Services](service-fabric-reliable-services-communication-wcf.md)
