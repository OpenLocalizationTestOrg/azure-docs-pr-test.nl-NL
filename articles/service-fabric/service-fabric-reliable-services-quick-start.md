---
title: aaaCreate uw eerste Service Fabric-toepassing in C# | Microsoft Docs
description: Inleiding toocreating een Microsoft Azure Service Fabric-toepassing met staatloze en stateful services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Aan de slag met Reliable Services
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-services-quick-start.md)
> * [Java op Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Een Azure Service Fabric-toepassing bevat een of meer services waarop uw code wordt uitgevoerd. Deze handleiding ontdekt u hoe toocreate staatloze en stateful Service Fabric-toepassingen met [Reliable Services](service-fabric-reliable-services-introduction.md).  Deze Microsoft Virtual Academy video ook ziet u hoe toocreate een stateless betrouwbare service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Basisconcepten
de slag met Reliable Services, u alleen tooget moet toounderstand enkele basisbeginselen:

* **Servicetype**: dit is uw service-implementatie. Dit is gedefinieerd door u schrijft Hallo-klasse die uitgebreider is dan `StatelessService` en andere code of afhankelijkheden gebruikt, samen met een naam en een uniek versienummer.
* **Service-exemplaar met de naam**: toorun uw service u maakt benoemde exemplaren van het servicetype veel zoals u instanties van objecten van het type van een klasse maken. Een service-exemplaar heeft een naam in de vorm van een URI met Hallo Hallo "fabric: / ' schema, zoals" fabric: / MyApp/MijnService '.
* **ServiceHost**: Hallo service-exemplaren maken van toorun moet binnen een hostproces verstrekt met de naam. Hallo ServiceHost is alleen een proces waarbij exemplaren van de service kunnen worden uitgevoerd.
* **Service-registratie**: inschrijving brengt alles bij elkaar. Hallo servicetype moet zijn geregistreerd met Hallo Service Fabric runtime in een service hosten tooallow Service Fabric toocreate exemplaren van deze toorun.  

## <a name="create-a-stateless-service"></a>Een stateless service maken
Een stateless service is een type service dat momenteel is Hallo-norm in de cloud-toepassingen. Dit wordt beschouwd als staatloze omdat Hallo-service zelf bevat geen gegevens die moeten worden toobe betrouwbaar opgeslagen of maximaal beschikbaar is gemaakt. Als u een exemplaar van een staatloze service wordt afgesloten, is alle van de interne status verloren. In dit type van service status persistente tooan externe winkel, zoals Azure-tabellen of een SQL-database, moet voor deze toobe maximaal beschikbare en betrouwbare aangebracht.

Start Visual Studio 2015 of Visual Studio 2017 als beheerder en maak een nieuwe Service Fabric-toepassingsproject met de naam *HelloWorld*:

![Hallo nieuw Project dialoogvenster vak toocreate een nieuwe Service Fabric-toepassing gebruiken](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Maak vervolgens een stateless service-project met de naam *HelloWorldStateless*:

![Hallo tweede in het dialoogvenster een stateless serviceproject maken](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Uw oplossing bevat nu twee projecten:

* *HelloWorld*. Dit is Hallo *toepassing* project met uw *services*. Het bevat ook Hallo-toepassingsmanifest die worden beschreven toepassing hello, evenals een aantal PowerShell-scripts waarmee u toodeploy uw toepassing.
* *HelloWorldStateless*. Dit is het serviceproject Hallo. Het bevat Hallo-implementatie voor stateless service.

## <a name="implement-hello-service"></a>Hallo service implementeren
Open Hallo **HelloWorldStateless.cs** bestand in Hallo serviceproject. Een service kunt eventuele bedrijfslogica uitvoeren in Service Fabric. Hallo service API biedt twee toegangspunten voor uw code:

* Een methode met een vermelding point, aangeroepen *RunAsync*, waar u kunt beginnen alle werkbelastingen, met inbegrip van langlopende compute-workloads uitvoeren.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Een communicatie-ingangspunt waar u uw communicatiestack keuze, zoals ASP.NET Core kunt aansluiten. Dit is waar u ontvangen van aanvragen van gebruikers en andere services kan starten.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

In deze zelfstudie gaan we in op Hallo `RunAsync()` entry point-methode. Dit is waar u kunt onmiddellijk starten uitvoeren van uw code.
Hallo-projectsjabloon bevat een Voorbeeldimplementatie van `RunAsync()` die een aantal rolling verhoogd.

> [!NOTE]
> Zie voor meer informatie over hoe toowork met een mededeling stack [Service Fabric-Web-API-services met OWIN zelf die als host fungeert](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

Hallo platform roept deze methode wanneer u een exemplaar van een service wordt geplaatst en zijn ze klaar tooexecute. Voor een stateless service betekent dat gewoon wanneer Hallo service-exemplaar wordt geopend. Een token annulering wordt toocoordinate opgegeven als uw service-exemplaar toobe gesloten moet. Deze cyclus openen en sluiten van een service-exemplaar kan in Service Fabric vaak tijdens Hallo-levensduur van Hallo service optreden als geheel. Dit kan gebeuren om verschillende redenen, waaronder:

* Hallo-systeem wordt uw service-exemplaren voor resourceverdeling verplaatst.
* Fouten die voorkomen in uw code.
* Hallo toepassings- of upgrade.
* de onderliggende hardware Hallo optreedt een storing.

Deze indeling wordt beheerd door Hallo system tookeep uw service maximaal beschikbaar is en goed taakverdeling.

`RunAsync()`moet niet synchroon blokkeren. De implementatie van RunAsync moet een taak retourneren of op alle bewerkingen langlopende of blokkeringen tooallow Hallo runtime toocontinue await. Let op Hallo `while(true)` lus in het vorige voorbeeld hello, een taak retourneren `await Task.Delay()` wordt gebruikt. Als uw werkbelasting synchroon blokkeert moet, moet u een nieuwe taak plannen `Task.Run()` in uw `RunAsync` implementatie.

Annulering van uw werkbelasting is een gezamenlijke inspanning gedirigeerd door Hallo annulering token opgegeven. Hallo systeem wacht tot de taak tooend (door met succes is voltooid, geannuleerd of fault) voordat het wordt verplaatst op. Het is belangrijk toohonor Hallo annulering token, voltooien een werken en af te sluiten `RunAsync()` zo snel mogelijk wanneer Hallo system annulering aanvraagt.

In dit voorbeeld staatloze service wordt Hallo count opgeslagen in een lokale variabele. Maar omdat dit een stateless service, Hallo-waarde die opgeslagen bestaat alleen voor de huidige levenscyclus Hallo van de service-exemplaar. Wanneer Hallo-service wordt verplaatst of opnieuw wordt opgestart, is Hallo-waarde verloren gegaan.

## <a name="create-a-stateful-service"></a>Een stateful service maken
Service Fabric introduceert een nieuw soort stateful service. Een stateful service te onderhouden op betrouwbare wijze binnen het Hallo-service zelf, CO-locaties met Hallo-code die wordt gebruikt. Status is maximaal beschikbaar is gemaakt door de Service Fabric zonder Hallo nodig toopersist status tooan externe winkel.

een waarde van het prestatiemeteritem van staatloze toohighly beschikbaar is en permanente tooconvert, zelfs wanneer het Hallo-service is verplaatst of opnieuw is opgestart, moet u een stateful service.

Hallo in dezelfde *HelloWorld* toepassing, kunt u een nieuwe service toevoegen door met de rechtermuisknop op Hallo Services verwijzingen in Hallo toepassingsproject en selecteren **toevoegen -> nieuwe Service Fabric-Service**.

![Een service tooyour Service Fabric-toepassing toevoegen](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Selecteer **Stateful Service** en noem deze *HelloWorldStateful*. Klik op **OK**.

![Hallo nieuw Project dialoogvenster vak toocreate een nieuwe stateful Service Fabric-service gebruiken](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

Uw toepassing hebt nu twee services: Hallo staatloze service *HelloWorldStateless* en stateful service Hallo *HelloWorldStateful*.

Een stateful service Hallo heeft dezelfde toegangspunten als een stateless service. het belangrijkste verschil Hallo is Hallo beschikbaarheid van een *state-provider* die de status op betrouwbare wijze kunt opslaan. Service Fabric wordt geleverd met een implementatie van de persistentieprovider status aangeroepen [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md), waarmee u gerepliceerde gegevensstructuren via Hallo betrouwbare status Manager maken. Een stateful betrouwbare Service maakt standaard gebruik van deze state-provider.

Open **HelloWorldStateful.cs** in *HelloWorldStateful*, die Hallo RunAsync-methode volgende bevat:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()`draait op dezelfde manier in stateful en staatloze services. Echter in een stateful service Hallo platform extra werk uitvoert namens jou voordat deze wordt uitgevoerd `RunAsync()`. Deze taak kunt opnemen ervoor te zorgen dat Hallo betrouwbare statusbeheer en betrouwbare verzamelingen toouse gereed zijn.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Betrouwbare verzamelingen en Hallo betrouwbare statusbeheer
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is de implementatie van een woordenlijst waarmee u de archiefstatus tooreliably in Hallo-service kunt. Met Service Fabric en betrouwbare verzamelingen, kunt u gegevens opslaan rechtstreeks in uw service zonder Hallo nodig is voor een externe permanente archief. Betrouwbare verzamelingen uw gegevens maximaal beschikbaar maken. Service Fabric bewerkstelligt dit door het maken en beheren van meerdere *replica's* van uw service voor u. Het bevat ook een API die de complexiteit van het beheer van deze replica's en hun statusovergangen opslag Hallo isoleert.

Betrouwbare verzamelingen kunnen elk type .NET, met inbegrip van uw aangepaste typen, met een aantal aanvullende opmerkingen worden opgeslagen.

* Service Fabric worden uw status maximaal beschikbaar door *repliceren* staat tussen knooppunten en betrouwbare verzamelingen uw toolocal gegevensschijf opslaan op elke replica. Dit betekent dat alles dat is opgeslagen in betrouwbare verzamelingen moet *serialiseerbaar*. Standaard gebruik van betrouwbare verzamelingen [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) voor serialisatie, dus is het belangrijk ervoor dat uw typen toomake [ondersteund door de serialisatiefunctie van het gegevenscontract Hallo](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) wanneer u Hallo standaardwaarde gebruiken serializer.
* Objecten worden gerepliceerd voor hoge beschikbaarheid, wanneer u transacties op betrouwbare verzamelingen doorvoert. Objecten die zijn opgeslagen in betrouwbare verzamelingen worden opgeslagen in het lokale geheugen van uw service. Dit betekent dat u een lokale toohello referentieobject hebt.
  
   Het is belangrijk dat u geen lokale exemplaren van deze objecten muteren zonder dat er een updatebewerking op Hallo betrouwbare verzameling in een transactie. Dit is omdat wijzigingen toolocal exemplaren van objecten worden niet automatisch worden gerepliceerd. U moet steek deze opnieuw Hallo object weer in de woordenlijst Hallo of gebruik een van de Hallo *bijwerken* methoden op Hallo woordenlijst.

Hallo betrouwbare status Manager beheert betrouwbare verzamelingen voor u. U kunt gewoon vragen Hallo betrouwbare status Manager voor een betrouwbare verzameling met de naam op elk gewenst moment en op een willekeurige plaats in uw service. Hallo betrouwbare status Manager zorgt ervoor dat u een verwijzing terug. We raadzaam niet op te slaan verwijzingen tooreliable verzameling exemplaren in Klassenlidvariabelen of eigenschappen. Speciale Wees voorzichtig tooensure die Hallo verwijzing ingesteld tooan exemplaar te allen tijde in Hallo service lifecycle. Hallo betrouwbare statusbeheer dit werk voor u verwerkt en geoptimaliseerd voor herhaaldelijk bezoeken.

### <a name="transactional-and-asynchronous-operations"></a>Transactionele en asynchrone bewerkingen
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Betrouwbare verzamelingen hebben veel Hallo dezelfde bewerkingen die hun `System.Collections.Generic` en `System.Collections.Concurrent` collega's doen, met uitzondering van LINQ. Bewerkingen op betrouwbare verzamelingen zijn asynchroon. Dit is omdat schrijfbewerkingen met betrouwbare verzamelingen tooreplicate van i/o-bewerkingen uitvoeren, zodat gegevens toodisk behouden blijven.

Betrouwbare verzameling bewerkingen zijn *transactionele*, zodat u status consistent voor meerdere betrouwbare verzamelingen en bewerkingen houden kunt. U kunt bijvoorbeeld een werkitem van een betrouwbare wachtrij in wachtrij, een bewerking uitvoeren op deze en Hallo resultaat opslaan in een betrouwbare woordenlijst alle binnen een transactie. Dit wordt beschouwd als een atomic-bewerking en dit zorgt ervoor dat de hele bewerking Hallo slaagt of Hallo hele bewerking wordt teruggedraaid. Als een fout optreedt nadat u uit de wachtrij Hallo item halen maar voordat u Hallo resultaat opslaat, Hallo hele transactie wordt teruggedraaid en Hallo item blijft in Hallo wachtrij voor verwerking.

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
Nu wordt teruggeplaatst toohello *HelloWorld* toepassing. U kunt nu bouwen en implementeren van uw services. Wanneer u drukt op **F5**, uw toepassing worden gebouwd en geïmplementeerde tooyour lokale cluster.

Nadat Hallo-services uitgevoerd worden gestart, kunt u weergeven Hallo gegenereerd Event Tracing voor Windows (ETW) gebeurtenissen in een **diagnostische gebeurtenissen** venster. Merk op dat Hallo gebeurtenissen weergegeven uit Hallo staatloze service en Hallo stateful service in de toepassing hello. U kunt Hallo stroom onderbreken door te klikken op Hallo **onderbreken** knop. U kunt vervolgens Hallo details van een bericht controleren door het uitbreiden van dat bericht.

> [!NOTE]
> Voordat u de toepassing hello uitvoert, zorg ervoor dat er een lokaal ontwikkelcluster uitgevoerd. Bekijk Hallo [instructiehandleiding](service-fabric-get-started.md) voor informatie over het instellen van uw lokale omgeving.
> 
> 

![Diagnostische gebeurtenissen weergeven in Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Volgende stappen
[Fouten opsporen in uw Service Fabric-toepassing in Visual Studio](service-fabric-debugging-your-application.md)

[Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert](service-fabric-reliable-services-communication-webapi.md)

[Meer informatie over betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md)

[Een toepassing implementeren](service-fabric-deploy-remove-applications.md)

[Upgrade van de toepassing](service-fabric-application-upgrade.md)

[Referentie voor ontwikkelaars voor Reliable Services](https://msdn.microsoft.com/library/azure/dn706529.aspx)

