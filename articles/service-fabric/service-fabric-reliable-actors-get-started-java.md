---
title: aaaCreate uw eerste actor gebaseerde Azure microservice in Java | Microsoft Docs
description: Deze zelfstudie leert u Hallo van maken, foutopsporing en een eenvoudige actor gebaseerde service met behulp van Service Fabric Reliable Actors implementeren.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Aan de slag met Reliable Actors
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-actors-get-started.md)
> * [Java op Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

In dit artikel wordt uitgelegd Hallo basisbeginselen van Azure Service Fabric Reliable Actors en leidt u door het maken en implementeren van een eenvoudige toepassing betrouwbare Actor in Java.

## <a name="installation-and-setup"></a>Installatie en configuratie
Voordat u begint, zorg er dan voor dat u hebt Hallo Service Fabric-ontwikkelomgeving instellen op uw computer.
Als u tooset moet deze, gaat u te[aan de slag op Mac](service-fabric-get-started-mac.md) of [aan de slag op Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Basisconcepten
de slag met Reliable Actors, u alleen tooget moet toounderstand enkele basisbeginselen:

* **Acteur service**. Reliable Actors zijn verpakt in Reliable Services die kunnen worden geïmplementeerd in Hallo Service Fabric-infrastructuur. Actor-exemplaren worden in een benoemd exemplaar geactiveerd.
* **Registratie actor**. Als met Reliable Services een betrouwbare Actor-service moet toobe geregistreerd bij Hallo Service Fabric-runtime. Bovendien moet Hallo actor-type zijn geregistreerd met Hallo Actor runtime toobe.
* **Actor-interface**. Hallo actor-interface is gebruikte toodefine een sterk getypeerde openbare interface van een acteur. In Hallo betrouwbare Actor model terminologie definieert Hallo actor interface Hallo soorten actor Hallo-berichten kunnen begrijpen en verwerken. Hallo actor-interface wordt gebruikt door andere actoren en clienttoepassingen te ' ' (asynchroon verzenden) berichten toohello actor. Reliable Actors kunnen meerdere interfaces implementeren.
* **Klasse ActorProxy**. Hallo ActorProxy klasse wordt gebruikt door de client toepassingen tooinvoke Hallo methoden beschikbaar via het Hallo actor-interface. Hallo ActorProxy klasse biedt twee belangrijke functies:
  
  * Naamomzetting: is kunnen toolocate Hallo actor in Hallo-cluster (Hallo knooppunt zoeken van Hallo cluster waar deze wordt gehost).
  * Afhandeling van taakfouten: kan Probeer methode-aanroepen en opnieuw oplossen Hallo actor locatie na, bijvoorbeeld een fout waarvoor Hallo actor toobe tooanother-knooppunt in Hallo cluster verplaatst.

Hallo volgens de regels die betrekking tooactor interfaces hebben zijn opgemerkt:

* Kan interfacemethoden acteur kunnen niet overbelast.
* Methoden mogen geen uit actor-interface, ref of optionele parameters.
* Algemene interfaces worden niet ondersteund.

## <a name="create-an-actor-service"></a>Maak een actor-service
Begint met het maken van een nieuwe Service Fabric-toepassing. Hallo Service Fabric SDK voor Linux bevat een Yeoman generator tooprovide Hallo steigers voor een Service Fabric-toepassing met een stateless service. Start met Hallo na Yeoman opdracht:

```bash
$ yo azuresfjava
```

Ga als volgt Hallo instructies toocreate een **betrouwbare Actor Service**. Naam voor deze zelfstudie Hallo application 'HelloWorldActorApplication' en Hallo actor 'HelloWorldActor'. Hallo steigers na worden gemaakt:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Betrouwbare actoren bouwstenen
Hallo basisconcepten eerder beschreven vertalen naar bouwstenen Hallo van een betrouwbare Actor-service.

### <a name="actor-interface"></a>Actor-interface
Dit document bevat Hallo interfacedefinitie voor Hallo actor. Deze interface definieert Hallo actor contract dat wordt gedeeld door Hallo actor-implementatie en het aanroepen van Hallo acteur, dus is het meestal wel zinvol toodefine deze op een locatie die is gescheiden van Hallo actor-implementatie en kan worden gedeeld door meerdere andere Hallo-clients client-toepassingen of services.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Actor-service
Dit document bevat uw actor-implementatie en actor registratiecode. Hallo actor-klasse Hallo actor-interface implementeert. Dit is waar uw actor zijn werk doet.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Actor-registratie
Hallo actor-service moet zijn geregistreerd met een servicetype in Hallo Service Fabric-runtime. In volgorde voor Hallo Actor Service toorun uw actor-exemplaren, uw actortype moet ook zijn geregistreerd bij Hallo Actor-Service. Hallo `ActorRuntime` registratiemethode voert dit werk gebruiken.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Testclient
Dit is een eenvoudige test clienttoepassing kunt u afzonderlijk uitvoeren van Hallo Service Fabric-toepassing tootest uw actor-service. Dit is een voorbeeld van waar Hallo ActorProxy worden gebruikte tooactivate en communiceren met actor-exemplaren. Deze wordt geïmplementeerd met uw service.

### <a name="hello-application"></a>Hallo-toepassing
Ten slotte Hallo Hallo toepassingspakketten actor-service en andere services die u wilt in Hallo toekomstige samen voor implementatie toevoegen mogelijk. Het Hallo bevat *ApplicationManifest.xml* en plaats houders voor Hallo actor servicepakket.

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Hallo Yeoman steigers bevat een gradle script toobuild Hallo toepassings- en bash-scripts toodeploy en verwijder de toepassing. toodeploy hello toepassing eerste build Hallo-toepassing met gradle:

```bash
$ gradle
```

Het resultaat is een Service Fabric-toepassingspakket dat kan worden geïmplementeerd met behulp van Service Fabric CLI-hulpprogramma's.

### <a name="deploy-service-fabric-cli"></a>Service Fabric CLI implementeren

Hallo install.sh script bevat Hallo benodigde Service Fabric CLI (sfctl) opdrachten toodeploy Hallo toepassingspakket.
Hallo install.sh script toodeploy Hallo toepassing uitvoeren.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Volgende stappen

* [Aan de slag met de Service Fabric-CLI](service-fabric-cli.md)
