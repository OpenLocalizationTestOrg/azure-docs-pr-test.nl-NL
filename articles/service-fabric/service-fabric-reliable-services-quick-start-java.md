---
title: aaaCreate uw eerste Azure betrouwbare microservice in Java | Microsoft Docs
description: Inleiding toocreating een Microsoft Azure Service Fabric-toepassing met staatloze en stateful services.
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
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

In dit artikel wordt uitgelegd Hallo basisbeginselen van Azure Service Fabric Reliable Services en leidt u door het maken en implementeren van een eenvoudige betrouwbare servicetoepassing geschreven in Java. Deze Microsoft Virtual Academy video ook ziet u hoe toocreate een stateless betrouwbare service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Installatie en configuratie
Voordat u begint, zorg er dan voor dat u hebt Hallo Service Fabric-ontwikkelomgeving instellen op uw computer.
Als u tooset moet deze, gaat u te[aan de slag op Mac](service-fabric-get-started-mac.md) of [aan de slag op Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Basisconcepten
de slag met Reliable Services, u alleen tooget moet toounderstand enkele basisbeginselen:

* **Servicetype**: dit is uw service-implementatie. Dit is gedefinieerd door u schrijft Hallo-klasse die uitgebreider is dan `StatelessService` en andere code of afhankelijkheden gebruikt, samen met een naam en een uniek versienummer.
* **Service-exemplaar met de naam**: toorun uw service u maakt benoemde exemplaren van het servicetype veel zoals u instanties van objecten van het type van een klasse maken. Service-exemplaren zijn in feite objectinstanties van uw serviceklasse die u schrijft.
* **ServiceHost**: Hallo service-exemplaren maken van toorun moeten in een host met de naam. Hallo ServiceHost is alleen een proces waarbij exemplaren van de service kunnen worden uitgevoerd.
* **Service-registratie**: inschrijving brengt alles bij elkaar. Hallo servicetype moet zijn geregistreerd met Hallo Service Fabric runtime in een service hosten tooallow Service Fabric toocreate exemplaren van deze toorun.  

## <a name="create-a-stateless-service"></a>Een stateless service maken
Begint met het maken van een Service Fabric-toepassing. Hallo Service Fabric SDK voor Linux bevat een Yeoman generator tooprovide Hallo steigers voor een Service Fabric-toepassing met een stateless service. Start met Hallo na Yeoman opdracht:

```bash
$ yo azuresfjava
```

Ga als volgt Hallo instructies toocreate een **betrouwbare staatloze Service**. Voor deze zelfstudie naam Hallo application 'HelloWorldApplication' en Hallo "Hallowereld"-service. Hallo resultaat omvat mappen voor Hallo `HelloWorldApplication` en `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Hallo service implementeren
Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Deze klasse definieert Hallo servicetype en code kan worden uitgevoerd. Hallo service API biedt twee toegangspunten voor uw code:

* Een methode met een vermelding point, aangeroepen `runAsync()`, waar u kunt beginnen alle werkbelastingen, met inbegrip van langlopende compute-workloads uitvoeren.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Een communicatie-ingangspunt waar u uw communicatiestack van keuze kunt aansluiten. Dit is waar u ontvangen van aanvragen van gebruikers en andere services kan starten.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

In deze zelfstudie we richten op Hallo `runAsync()` entry point-methode. Dit is waar u kunt onmiddellijk starten uitvoeren van uw code.

### <a name="runasync"></a>RunAsync
Hallo platform roept deze methode wanneer u een exemplaar van een service wordt geplaatst en zijn ze klaar tooexecute. Voor een stateless service betekent dat gewoon wanneer Hallo service-exemplaar wordt geopend. Een token annulering wordt toocoordinate opgegeven als uw service-exemplaar toobe gesloten moet. Deze cyclus openen en sluiten van een service-exemplaar kan in Service Fabric vaak tijdens Hallo-levensduur van Hallo service optreden als geheel. Dit kan gebeuren om verschillende redenen, waaronder:

* Hallo-systeem wordt uw service-exemplaren voor resourceverdeling verplaatst.
* Fouten die voorkomen in uw code.
* Hallo toepassings- of upgrade.
* de onderliggende hardware Hallo optreedt een storing.

Deze indeling wordt beheerd door Service Fabric tookeep uw service maximaal beschikbaar is en goed taakverdeling.

`runAsync()`moet niet synchroon blokkeren. De implementatie van runAsync moet een CompletableFuture tooallow Hallo runtime toocontinue retourneren. Als uw werkbelasting een langlopende taak die moet worden uitgevoerd moet binnen tooimplement Hallo CompletableFuture.

#### <a name="cancellation"></a>Annulering
Annulering van uw werkbelasting is een gezamenlijke inspanning gedirigeerd door Hallo annulering token opgegeven. Hallo-systeem wacht voor uw taak tooend (door met succes is voltooid, geannuleerd of fault) voordat het wordt verplaatst op. Het is belangrijk toohonor Hallo annulering token, voltooien een werken en af te sluiten `runAsync()` zo snel mogelijk wanneer Hallo system annulering aanvraagt. Hallo volgende voorbeeld laat zien hoe een gebeurtenis annulering toohandle:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Registratie van service
Servicetypen moeten zijn geregistreerd met Hallo Service Fabric-runtime. Hallo servicetype is gedefinieerd in Hallo `ServiceManifest.xml` en uw serviceklasse die implementeert `StatelessService`. Registratie van de service wordt uitgevoerd in Hallo proces Hoofdingangspunt is. In dit voorbeeld Hallo proces Hoofdingangspunt is `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Hallo Yeoman steigers bevat een gradle script toobuild Hallo toepassings- en bash-scripts toodeploy en verwijder de toepassing. toorun hello toepassing eerste build Hallo-toepassing met gradle:

```bash
$ gradle
```

Dit resulteert in een Service Fabric-toepassingspakket dat kan worden geïmplementeerd met behulp van Service Fabric CLI.

### <a name="deploy-with-service-fabric-cli"></a>Met Service Fabric CLI implementeren

Hallo install.sh script bevat Hallo benodigde Service Fabric CLI-opdrachten toodeploy Hallo toepassingspakket. Voer de install.sh script toodeploy Hallo-toepassing.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Volgende stappen

* [Aan de slag met de Service Fabric-CLI](service-fabric-cli.md)
