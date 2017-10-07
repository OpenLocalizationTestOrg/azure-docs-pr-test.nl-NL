---
title: Service Fabric-services aaaPartitioning | Microsoft Docs
description: Hierin wordt beschreven hoe toopartition Service Fabric stateful services. Partities kunnen de opslag van gegevens op de lokale machines Hallo zodat gegevens en rekencapaciteit samen kunnen worden geschaald.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Betrouwbare partitie Service Fabric-services
Dit artikel bevat een inleiding toohello basisconcepten van Azure Service Fabric betrouwbare services partitioneren. Hallo broncode gebruikt in Hallo artikel is ook beschikbaar op [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Partitionering
Partitioneren is niet uniek tooService Fabric. Het is in feite een patroon core van het bouwen van schaalbare services. We kunnen in een ruimere zin nadenken over partitioneren als een concept van het delen van status (gegevens) en compute in kleinere eenheden toegankelijk tooimprove schaalbaarheid en prestaties. Is een bekende formulier van het partitioneren van [partitioneren van gegevens][wikipartition], ook wel aangeduid als sharding.

### <a name="partition-service-fabric-stateless-services"></a>Partitie Service Fabric stateless services
U kunt een partitie wordt een logische eenheid met een of meer exemplaren van een service bedenken voor stateless services. Afbeelding 1 toont een stateless service met vijf exemplaren verdeeld over een cluster met één partitie.

![Staatloze service](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Er zijn in feite twee soorten stateless Services-oplossingen. Hallo eerst is een een service die de status extern, bijvoorbeeld zich blijft voordoen in een Azure SQL database (zoals een website die Hallo sessie-informatie en gegevens worden opgeslagen). Hallo is tweede alleen-berekeningen services (zoals een miniatuur Rekenmachine of afbeelding) die geen permanente status niet beheren.

Ofwel in geval een stateless service partitioneren is een zeldzame scenario--schaalbaarheid en beschikbaarheid normaal worden bereikt door meer exemplaren toe te voegen. Hallo enige keer dat u wilt dat meerdere partities voor stateless service-exemplaren is wanneer u toomeet speciale routering tooconsider aanvragen.

Een voorbeeld kunt u een aanvraag waarin gebruikers met de id's in een bepaald bereik moeten alleen worden geleverd door een bepaalde service-exemplaar. Een ander voorbeeld van wanneer u een stateless service kan partitioneren is wanneer u een echt gepartitioneerde back-end (bijvoorbeeld een shard SQL-database) en u wilt dat toocontrol welk service-exemplaar moet schrijven toohello database shard-- of andere taken voorbereiding binnen Hallo staatloze service waarvoor Hallo dezelfde partitiegegevens, zoals wordt gebruikt in Hallo back-end. Dergelijke scenario's kunnen ook op verschillende manieren worden opgelost en niet noodzakelijk partitioneren van de service.

Hallo rest van dit scenario ligt de nadruk op stateful services.

### <a name="partition-service-fabric-stateful-services"></a>Partitie Service Fabric stateful services
Service Fabric maakt het eenvoudig toodevelop schaalbare stateful services door het aanbieden van een uitstekende manier toopartition status (gegevens). Conceptueel gezien u over een partitie van een stateful service kunt beschouwen als een schaaleenheid die zeer betrouwbaar via [replica's](service-fabric-availability-services.md) die zijn gedistribueerd en verdeeld zijn over Hallo knooppunten in een cluster.

In de context van Service Fabric stateful services Hallo partitioneren verwijst toohello proces om te bepalen dat een bepaalde service partitie verantwoordelijk voor een deel van de volledige status Hallo van Hallo-service is. (Zoals al eerder vermeld, een partitie is een reeks [replica's](service-fabric-availability-services.md)). Een aardige van Service Fabric is Hallo partities geplaatst op verschillende knooppunten. Hierdoor kunnen ze toogrow tooa knooppunt resource limiet. Wanneer gegevens Hallo groeien behoeften, groeien partities en Service Fabric rebalances partities over knooppunten. Dit zorgt ervoor Hallo voortgezet hardwarebronnen efficiënt worden gebruikt.

toogive u bijvoorbeeld dat u begint met een 5-node cluster en een service die is geconfigureerd toohave 10 partities en een doel van drie replica's. In dit geval Service Fabric zou worden verdeeld en Hallo replica's verdelen over Hallo-cluster en zou u uiteindelijk eindigen met twee primaire [replica's](service-fabric-availability-services.md) per knooppunt.
Als u nu tooscale uit Hallo too10 clusterknooppunten moet, Service Fabric zou opnieuw verdelen Hallo primaire [replica's](service-fabric-availability-services.md) op alle knooppunten van 10. Op dezelfde manier als u back too5 knooppunten uitgebreide, Service Fabric zou opnieuw verdelen alle Hallo-replica's op Hallo 5-knooppunten.  

Afbeelding 2 toont de distributie van de Hallo van 10 partities voor en na het Hallo-cluster schalen.

![Stateful service](./media/service-fabric-concepts-partitioning/partitions.png)

Hallo scale-out wordt hierdoor bereikt omdat aanvragen van clients worden verdeeld over computers, algehele prestaties van de toepassing hello is verbeterd en conflicten op toegang toochunks van gegevens wordt verminderd.

## <a name="plan-for-partitioning"></a>Plan voor het partitioneren
Voordat u een service implementeert, moet u altijd Hallo-strategie is vereist tooscale uit partitioneren overwegen. Er zijn verschillende manieren, maar ze allemaal ligt de nadruk op welke toepassing hello tooachieve moet. Hallo-context van dit artikel, laten we eens enkele Hallo meer belangrijke aspecten.

Een goede benadering is toothink over Hallo-structuur van Hallo status die is gepartitioneerd, als de eerste stap Hallo toobe nodig.

U gaat nu een eenvoudig voorbeeld. Als u een service voor een countywide poll toobuild was, kunt u een partitie voor elke stad in Hallo regio kunt maken. Vervolgens kunt u Hallo stemmen voor elke persoon opslaan in plaats van Hallo in Hallo partitie die overeenkomt met toothat plaats. Afbeelding 3 ziet u een set van mensen en Hallo plaats waar ze zich bevinden.

![Eenvoudige partitie](./media/service-fabric-concepts-partitioning/cities.png)

Als Hallo populatie steden varieert, zou u uiteindelijk met een aantal partities met een grote hoeveelheid gegevens (bijvoorbeeld Haarlem) en andere partities met weinig status (bijvoorbeeld Kirkland). Wat is Hallo impact van partities met ongelijke hoeveelheden status hebben?

Als u opnieuw over Hallo voorbeeld denkt, kunt u eenvoudig hello partitie waarin Hallo stemmen voor Seattle krijgt meer verkeer dan Hallo Kirkland een bekijken. Service Fabric maakt standaard ervoor dat er over Hallo hetzelfde aantal primaire en secundaire replica's op elk knooppunt. Zo zou u uiteindelijk met knooppunten die fungeren als replica's die dienen meer verkeer en anderen die minder verkeer dienen houdt. U zou bij voorkeur wilt tooavoid warme en koude plaatsen zoals deze in een cluster.

In volgorde tooavoid dit, moet u twee dingen doen vanuit het partitionering oogpunt:

* Probeer toopartition Hallo status, zodat deze evenredig verdeeld over alle partities.
* Rapporteren over de belasting van elk van de replica's Hallo voor Hallo-service. (Voor meer informatie over het controleren van dit artikel [metrische gegevens en de belasting](service-fabric-cluster-resource-manager-metrics.md)). Service Fabric bevat Hallo mogelijkheid tooreport load verbruikt door services, zoals de hoeveelheid geheugen of het aantal records. Op basis van Hallo metrische gegevens die zijn gerapporteerd, detecteert Service Fabric dat een aantal partities hogere belasting dan andere fungeren en rebalances Hallo cluster door bewegende replica's toomore geschikte knooppunten, zodat de algemene geen knooppunt is overbelast.

Soms weet u niet kunt hoeveel gegevens worden weergegeven in een bepaalde partitie. Zodat een algemene aanbeveling toodo beide--eerst selecteert door partities die, Hallo gegevens gelijkmatig over Hallo partities en de tweede pagina, met reporting laden.  de eerste methode Hallo voorkomt situaties beschreven in Hallo bijvoorbeeld stemmen terwijl Hallo tweede vloeiend maken tijdelijke verschillen in access of load gedurende een bepaalde periode helpt.

Een ander aspect van de planning van de partitie is toochoose Hallo juiste aantal partities toobegin met.
Vanuit het perspectief van een Service Fabric is er niets dat verhindert dat u begint met een hoger aantal partities dan verwacht voor uw scenario.
Ervan uitgaande dat Hallo kunt u het maximum aantal partities is in feite een geldige benadering.

In zeldzame gevallen, zou u uiteindelijk hoeven meer partities dan u oorspronkelijk hebt gekozen. Zoals u kunt Hallo partitie aantal niet wijzigen nadat Hallo feit, moet u tooapply sommige geavanceerde partitie benaderingen, zoals het maken van een nieuwe service-exemplaar Hallo dezelfde servicetype. U moet tevens tooimplement bepaalde clientzijde logica die Hallo routeert toohello juiste service-exemplaar aanvragen, gebaseerd op kennis van clientzijde die u ervoor dat uw clientcode zorgen moet.

Andere overweging voor het partitioneren van de planning is Hallo beschikbare computerbronnen. Als het Hallo-status moet toobe toegankelijk is en opgeslagen, zijn gebonden toofollow:

* Netwerk bandbreedtelimieten
* Systeem geheugenlimieten
* Schijf opslaglimieten

Wat gebeurt zodat er als u in resourcebeperkingen in een actief cluster uitvoert? Hallo-antwoord is dat u kunt gewoon worden uitgebreid Hallo cluster tooaccommodate Hallo nieuwe vereisten.

[handleiding voor capaciteitsplanning Hallo](service-fabric-capacity-planning.md) biedt richtlijnen voor het toodetermine hoeveel knooppunten uw cluster moet.

## <a name="get-started-with-partitioning"></a>Aan de slag met partitioneren
Deze sectie beschrijft hoe tooget gestart met het partitioneren van uw service.

Service Fabric biedt een keuze uit drie partitieschema's:

* Varieerden partitioneren (anders UniformInt64Partition genoemd).
* Met de naam partitioneren. Toepassingen die gebruikmaken van dit model meestal beschikken over gegevens die kunnen worden bucketed binnen een begrensde set. Enkele algemene voorbeelden van gegevensvelden gebruikt als benoemde partitiesleutels zou worden regio's, postcode codes, klantengroepen of andere zakelijke grenzen.
* Singleton partitioneren. Singleton-partities worden meestal gebruikt wanneer het Hallo-service vereist geen aanvullende routering. Bijvoorbeeld, stateless services deze partitieschema standaard gebruikt.

Met de naam en partitionering Singleton-schema's zijn speciale soorten varieerde partities. Standaard varieerden Hallo Visual Studio-sjablonen voor Service Fabric gebruik partitioneren, omdat deze Hallo veelgebruikte en handige één. Hallo rest van dit artikel is gericht op Hallo varieerde partitieschema.

### <a name="ranged-partitioning-scheme"></a>Partitieschema varieerde
Dit is een geheel getal van gebruikte toospecify bereik (aangeduid met een lage en hoge sleutel) en een aantal partities (n). Het maken van n partities, elke verantwoordelijk is voor een niet-overlappende subbereik Hallo algemene partitie sleutel bereik. Bijvoorbeeld, een ranged partitieschema met een lage sleutel 0, een hoge sleutel 99 en een telling van 4 maakt vier partities zoals hieronder wordt weergegeven.

![Bereik partitioneren](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Een veelgebruikte oplossing is toocreate een hash op basis van een unieke sleutel in Hallo-gegevensset. Enkele algemene voorbeelden van sleutels is een vehicle id-nummer (VIN), een werknemer-ID of een unieke tekenreeks zijn. Met behulp van deze unieke sleutel, zou u vervolgens een hash-code, modulus Hallo sleutel bereik, toouse als uw sleutel gegenereerd. U kunt Hallo bovenste en de ondergrenzen Hallo het toegestane bereik sleutel opgeven.

### <a name="select-a-hash-algorithm"></a>Selecteer een hash-algoritme
Een belangrijk onderdeel van het hash-selecteert hash-algoritme. Overweging is of Hallo doel toogroup vergelijkbare sleutels in de buurt van elkaar (plaats gevoelige hashing)--is of als activiteit moet op grote schaal worden gedistribueerd voor alle partities (hash-distributie), waarmee veelvoorkomende is.

Hallo kenmerken van een goede distributie hash-algoritme zijn dat het eenvoudig toocompute is, enkele conflicten heeft en het Hallo-sleutels gelijkmatig worden verdeeld. Een goed voorbeeld van een efficiënte hash-algoritme is Hallo [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash-algoritme.

Een goede resource voor algemene hash-code algoritme die is Hallo [pagina Wikipedia (Engelstalig) op de hash-functies](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Een stateful service met meerdere partities bouwen
Stel uw eerste betrouwbare stateful service maken met meerdere partities. In dit voorbeeld maakt u een zeer eenvoudige toepassing waar u toostore alle laatste namen die beginnen met dezelfde stationsletter in Hallo Hallo dezelfde partitie.

Voordat u een code te schrijven, moet u toothink over Hallo partities en partitiesleutels. Moet u 26 partities (één voor elke letter in Hallo alfabet), maar wat over lage en hoge sleutels Hallo?
Als we letterlijk toohave één partitie per letter willen, kunt we gebruiken 0 als de lage sleutelwaarde Hallo en 25 als Hallo hoge sleutel, omdat elke letter een eigen sleutel.

> [!NOTE]
> Dit is een vereenvoudigde scenario in werkelijkheid Hallo distributie ongelijke zou zijn. Laatste namen die beginnen met Hallo letters "S" of ''M' komen vaker dan Hallo die beginnen met 'X' of 'Y'.
> 
> 

1. Open **Visual Studio** > **bestand** > **nieuwe** > **Project**.
2. In Hallo **nieuw Project** dialoogvenster Kies Hallo Service Fabric-toepassing.
3. Hallo project 'AlphabetPartitions' aanroepen.
4. In Hallo **maken van een Service** dialoogvenster Kies **Stateful** service en deze aanroepen 'Alphabet.Processing' zoals wordt weergegeven in onderstaande Hallo-afbeelding.
       ![Dialoogvenster voor nieuwe service in Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Het aantal partities Hallo instellen. Open Hallo Applicationmanifest.xml bestand zich in Hallo ApplicationPackageRoot map van Hallo AlphabetPartitions project en update Hallo parameter Processing_PartitionCount too26 zoals hieronder wordt weergegeven.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    U moet ook tooupdate hello LowKey en HighKey eigenschappen van Hallo StatefulService element in Hallo ApplicationManifest.xml zoals hieronder wordt weergegeven.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Voor Hallo service toobe toegankelijk is, opent u een eindpunt op een poort door toe te voegen Hallo eindpuntelement van ServiceManifest.xml (te vinden in Hallo PackageRoot map) voor Hallo Alphabet.Processing service zoals hieronder wordt weergegeven:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Hallo-service is nu geconfigureerd toolisten tooan interne eindpunt met 26 partities.
7. Vervolgens moet u toooverride hello `CreateServiceReplicaListeners()` methode van Hallo verwerking klasse.
   
   > [!NOTE]
   > Voor dit voorbeeld nemen we aan dat u van een eenvoudige HttpCommunicationListener gebruikmaakt. Zie voor meer informatie over betrouwbare servicecommunicatie [Hallo-communicatie van betrouwbare servicemodel](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Een aanbevolen patroon voor Hallo-URL die een replica luistert op Hallo na indeling is: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Zodat u tooconfigure uw communicatie-listener toolisten op de juiste eindpunten Hallo en met dit patroon.
   
    Meerdere replica's van deze service kunnen worden gehost op Hallo dezelfde computer, zodat dit adres toobe unieke toohello replica moet. Daarom partitie-ID + replica-ID in Hallo-URL zijn. HttpListener kan luisteren op meerdere adressen op Hallo die dezelfde poort als Hallo URL-voorvoegsel uniek is.
   
    Hallo die extra GUID is er voor een geavanceerde aanvraag waarop secundaire replica's ook voor alleen-lezen-aanvragen luisteren. Wanneer dit Hallo geval is, wilt u ervoor dat er een nieuw uniek adres wordt gebruikt tijdens het veranderen van primaire toosecondary tooforce clients toore oplossen Hallo adres toomake. '+' wordt gebruikt als Hallo adres hier zodat hello replica op alle beschikbare hosts (IP-, FQDM, ' localhost ', enz.) Hallo code hieronder luistert ziet u een voorbeeld.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    Het verdient aanbeveling ook weten dat Hallo gepubliceerde URL verschilt enigszins van Hallo luisterende URL-voorvoegsel.
    Hallo luisterende URL tooHttpListener krijgt. Hallo die gepubliceerde URL is Hallo-URL die is gepubliceerd toohello Service Fabric Naming Service, die wordt gebruikt voor servicedetectie. Clients vragen voor dit adres via die discovery-service. Hallo-adres dat clients behoeften toohave Hallo werkelijke IP of FQDN van Hallo-knooppunt in de volgorde tooconnect ophalen. Daarom tooreplace '+' met Hallo van het knooppunt IP of FQDN-naam zoals hierboven.
9. de laatste stap Hallo is tooadd Hallo verwerken logica toohello service zoals hieronder wordt weergegeven.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`leesbewerkingen Hallo waarden van Hallo query tekenreeks parameter gebruikt toocall Hallo partitie en aanroepen `AddUserAsync` tooadd Hallo lastname toohello betrouwbare woordenlijst `dictionary`.
10. We voegen een stateless service toohello project toosee hoe u een bepaalde partitie kunt aanroepen.
    
    Deze service fungeert als een eenvoudige webinterface die Hallo lastname als een queryreeksparameter accepteert, bepaalt de partitiesleutel Hallo en verzendt het toohello Alphabet.Processing service voor de verwerking.
11. In Hallo **maken van een Service** dialoogvenster Kies **Stateless** service en deze aanroepen 'Alphabet.Web' zoals hieronder wordt weergegeven.
    
    ![Schermopname van staatloze service](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Hallo eindpuntinformatie in Hallo ServiceManifest.xml van Hallo Alphabet.WebApi service tooopen van een poort zoals hieronder wordt weergegeven bijwerken.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. U moet een verzameling van ServiceInstanceListeners in Hallo klasse Web tooreturn. Nogmaals, kunt u tooimplement een eenvoudige HttpCommunicationListener.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Nu moet u tooimplement Hallo verwerking logica. Hallo HttpCommunicationListener aanroepen `ProcessInputRequest` wanneer een aanvraag binnenkomt. Dus we gaan nu en voeg Hallo code hieronder.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    We doorlopen die deze stap voor stap. Hallo code leest de eerste letter Hallo van Hallo querytekenreeksparameter `lastname` in een tekenset. Vervolgens, bepaalt de partitiesleutel Hallo voor deze brief door af te trekken Hallo hexadecimale waarde van `A` van Hallo hexadecimale waarde van de eerste letter Hallo laatste namen.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Vergeet niet dat voor dit voorbeeld gebruiken we 26 partities met één partitiesleutel per partitie.
    Vervolgens verkrijgen van Hallo service partitie `partition` voor deze sleutel met behulp van Hallo `ResolveAsync` methode op Hallo `servicePartitionResolver` object. `servicePartitionResolver`is gedefinieerd als
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Hallo `ResolveAsync` methode vergt Hallo service URI, Hallo partitiesleutel en een token annulering als parameters. Hallo service-URI voor Hallo verwerking van de service is `fabric:/AlphabetPartitions/Processing`. Vervolgens krijgen we Hallo endpoint van Hallo-partitie.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Ten slotte we Hallo eindpunt-URL plus Hallo querystring bouwen en Hallo verwerking van de service aanroepen.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Zodra het Hallo verwerken is voltooid, terugschrijven we Hallo uitvoer.
15. de laatste stap Hallo is tootest Hallo-service. Visual Studio maakt gebruik van parameters voor de toepassing voor lokale en cloudimplementatie. met lokaal 26 partities tootest Hallo-service, moet u tooupdate hello `Local.xml` bestand in Hallo ApplicationParameters map van Hallo AlphabetPartitions project, zoals hieronder wordt weergegeven:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Wanneer u klaar bent voor implementatie, kunt u Hallo-service en alle van de partities in Service Fabric Explorer Hallo controleren.
    
    ![Schermafbeelding van de service Fabric Explorer](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. In een browser, kunt u testen Hallo logica partitioneren door te voeren `http://localhost:8081/?lastname=somename`. U ziet dat elke achternaam op die begint met dezelfde letter worden opgeslagen in Hallo Hallo dezelfde partitie.
    
    ![Schermafbeelding van de browser](./media/service-fabric-concepts-partitioning/samplerunning.png)

Hallo volledige broncode van Hallo voorbeeld is beschikbaar op [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Volgende stappen
Zie voor informatie over Service Fabric-concepten Hallo volgende:

* [Beschikbaarheid van Service Fabric-services](service-fabric-availability-services.md)
* [Schaalbaarheid van Service Fabric-services](service-fabric-concepts-scalability.md)
* [Capaciteitsplanning voor Service Fabric-toepassingen](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png