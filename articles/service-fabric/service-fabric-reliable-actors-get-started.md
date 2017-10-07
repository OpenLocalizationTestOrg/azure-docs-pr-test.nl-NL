---
title: aaaCreate uw eerste actor gebaseerde Azure microservice in C# | Microsoft Docs
description: Deze zelfstudie leert u Hallo van maken, foutopsporing en een eenvoudige actor gebaseerde service met behulp van Service Fabric Reliable Actors implementeren.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
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

In dit artikel wordt uitgelegd Hallo basisbeginselen van Azure Service Fabric Reliable Actors en leidt u door het maken en implementeren van een eenvoudige betrouwbare Actor-toepassing in Visual Studio-foutopsporing.

## <a name="installation-and-setup"></a>Installatie en configuratie
Voordat u begint, zorg ervoor dat u Hallo Service Fabric-ontwikkelomgeving instellen op uw computer.
Als u tooset moet deze, gedetailleerde instructies zien op [hoe tooset van Hallo ontwikkelomgeving](service-fabric-get-started.md).

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

## <a name="create-a-new-project-in-visual-studio"></a>Maak een nieuw project in Visual Studio
Start Visual Studio 2015 of Visual Studio 2017 als beheerder en maak een nieuw project voor Service Fabric-toepassing:

![Service Fabric-tools voor Visual Studio - nieuw project][1]

In het volgende dialoogvenster hello, kunt u Hallo type project dat u wilt dat toocreate.

![Service Fabric-projectsjablonen][5]

Voor Hallo HelloWorld-project, gebruiken we Hallo Reliable Actors van Service Fabric-service.

Nadat u Hallo oplossing hebt gemaakt, ziet u Hallo structuur te volgen:

![De structuur van de service Fabric-project][2]

## <a name="reliable-actors-basic-building-blocks"></a>Betrouwbare actoren bouwstenen
Een typische Reliable Actors oplossing bestaat uit drie projecten:

* **Hallo-toepassingsproject (MyActorApplication)**. Dit is Hallo-project dat alle services samen Hallo voor implementatie van pakketten. Het Hallo bevat *ApplicationManifest.xml* en PowerShell-scripts voor het beheren van de toepassing hello.
* **Hallo-interface-project (MyActor.Interfaces)**. Dit is Hallo-project dat Hallo interfacedefinitie voor Hallo actor bevat. In Hallo MyActor.Interfaces-project kunt u Hallo-interfaces die worden gebruikt door Hallo actoren in Hallo oplossing definiëren. Uw actor-interfaces kunnen worden gedefinieerd in een project met een naam, maar Hallo interface Hallo actor contract dat wordt gedeeld door Hallo actor-implementatie en Hallo-clients aanroepen Hallo acteur, dus het meestal wel zinvol toodefine is wordt gedefinieerd in een assembly die is afzonderlijke uit Hallo actor-implementatie en kan worden gedeeld door meerdere andere projecten.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **Hallo actor service-project (MyActor)**. Dit is Hallo project gebruikt toodefine Hallo Service Fabric-service gaat toohost Hallo actor. Het bevat Hallo-implementatie van Hallo actor. Een actor-implementatie is een klasse die is afgeleid van het basistype Hallo `Actor` en implementeert interface (s) die zijn gedefinieerd in Hallo MyActor.Interfaces project Hallo. Een actor-klasse moet ook een constructor implementeren een `ActorService` exemplaar en een `ActorId` en geeft deze door toohello base `Actor` klasse. Hierdoor constructor afhankelijkheidsinjectie van platform afhankelijkheden.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

Hallo actor-service moet zijn geregistreerd met een servicetype in Hallo Service Fabric-runtime. In volgorde voor Hallo Actor Service toorun uw actor-exemplaren, uw actortype moet ook zijn geregistreerd bij Hallo Actor-Service. Hallo `ActorRuntime` registratiemethode voert dit werk gebruiken.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Als u vanaf een nieuw project in Visual Studio opstarten en hebt u slechts één definitie van actor, is Hallo-registratie standaard opgenomen in Hallo-code die Visual Studio gegenereerd. Als u andere actoren in Hallo service definieert, moet u tooadd Hallo actor registratie met behulp van:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Hallo actoren van Service Fabric-runtime verzendt sommige [gebeurtenissen en prestatiemeteritems gerelateerde tooactor methoden](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Ze zijn nuttig zijn bij de diagnostische gegevens en prestatiebewaking.
> 
> 

## <a name="debugging"></a>Foutopsporing
Hallo Service Fabric-tools voor Visual Studio ondersteuning voor foutopsporing op uw lokale machine. U kunt een sessie voor foutopsporing starten door roept Hallo F5-toets. Visual Studio maakt (indien nodig) pakketten. Ook implementeert de toepassing hello op Hallo lokale Service Fabric-cluster en Hallo foutopsporingsprogramma koppelt.

Tijdens het implementatieproces Hallo ziet u Hallo voortgang in Hallo **uitvoer** venster.

![Service Fabric foutopsporing uitvoervenster][3]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [hoe Reliable Actors Hallo Service Fabric-platform gebruiken](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
