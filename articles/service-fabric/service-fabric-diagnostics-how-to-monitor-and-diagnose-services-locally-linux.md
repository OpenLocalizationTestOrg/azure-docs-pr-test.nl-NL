---
title: aaaDebug Azure microservices in Linux | Microsoft Docs
description: Meer informatie over hoe toomonitor en onderzoeken van uw services die zijn geschreven met behulp van Microsoft Azure Service Fabric op een lokale ontwikkelcomputer.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Controle en diagnose van services in de instellingen voor een lokale computer-ontwikkeling


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Wacht tot services toocontinue met minimale onderbrekingen toohello gebruikerservaring bewaking, detecteren, onderzoeken en het oplossen van problemen. Controle en diagnostische gegevens zijn essentieel in een werkelijke geïmplementeerde productie-omgeving. Een vergelijkbaar model overstap tijdens de ontwikkeling van services zorgt ervoor dat Hallo diagnostische pijplijn werkt wanneer u de productieomgeving tooa verplaatst. Service Fabric eenvoudig service ontwikkelaars tooimplement diagnostics dat naadloos voor zowel lokale ontwikkeling één machine-instellingen als de echte productie cluster instellingen werkt.


## <a name="debugging-service-fabric-java-applications"></a>Foutopsporing van Service Fabric-Java-toepassingen

Voor Java-toepassingen [meerdere frameworks voor logboekregistratie](http://en.wikipedia.org/wiki/Java_logging_framework) beschikbaar zijn. Aangezien `java.util.logging` is de standaardoptie Hallo Hello JRE, wordt ook gebruikt voor Hallo [codevoorbeelden in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Hallo bespreking van de volgende wordt uitgelegd hoe tooconfigure hello `java.util.logging` framework.

Met behulp van java.util.logging kunt u uw toepassing omleiden registreert toomemory, uitvoerstromen, console-bestanden of sockets. Er zijn standaard handlers al opgegeven in het Hallo-framework voor elk van deze opties. Kunt u een `app.properties` bestand tooconfigure Hallo bestandshandler voor uw toepassing tooredirect alle logboeken tooa lokaal bestand.

Hallo volgende codefragment bevat de voorbeeldconfiguratie van een:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Hallo map verwijzen tooby hello `app.properties` bestand moet bestaan. Na het Hallo `app.properties` -bestand wordt gemaakt, moet u tooalso uw script post-punt wijzigen `entrypoint.sh` in Hallo `<applicationfolder>/<servicePkg>/Code/` map tooset Hallo eigenschap `java.util.logging.config.file` te`app.propertes` bestand. Hallo-vermelding moet eruitzien als Hallo codefragment te volgen:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Deze configuratie resulteert in Logboeken worden verzameld in een draaiende wijze op `/tmp/servicefabric/logs/`. Hallo logboekbestand in dit geval is de naam mysfapp%u.%g.log waar:
* **%u** is een uniek nummer tooresolve conflicten tussen processen gelijktijdig Java.
* **%g** Hallo generatie nummer toodistinguish tussen het roteren van Logboeken is.

Standaard als er geen handler expliciet is geconfigureerd, is Hallo console handler geregistreerd. Een kunt Hallo Logboeken in syslog onder /var/log/syslog weergeven.

Zie voor meer informatie, Hallo [codevoorbeelden in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Foutopsporing van Service Fabric C#-toepassingen


Meerdere frameworks er beschikbaar zijn voor het traceren van CoreCLR toepassingen op Linux. Zie voor meer informatie [GitHub: logboekregistratie](http:/github.com/aspnet/logging).  Aangezien EventSource bekend tooC # ontwikkelaars, is dit artikel EventSource wordt gebruikt voor tracering in CoreCLR voorbeelden op Linux.

de eerste stap Hallo is tooinclude System.Diagnostics.Tracing zodat u kunt uw logboeken toomemory, uitvoerstromen of console-bestanden schrijven.  Voor logboekregistratie met behulp van EventSource, voegt u Hallo project tooyour project.json te volgen:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

U kunt een aangepaste EventListener toolisten gebruiken voor Hallo service gebeurtenis en klik vervolgens op de juiste wijze hen omleidt tootrace bestanden. Hallo toont volgende codefragment een Voorbeeldimplementatie van logboekregistratie met behulp van EventSource en een aangepaste EventListener:


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


Hallo voorgaande codefragment levert Hallo logboeken tooa bestand in `/tmp/MyServiceLog.txt`. Deze naam moet toobe op de juiste wijze bijgewerkt. Als u wilt dat tooredirect Hallo logboeken tooconsole, gebruikt u Hallo volgende codefragment in uw aangepaste EventListener-klasse:

```csharp
public static TextWriter Out = Console.Out;
```

voorbeelden op Hallo [voorbeelden C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource en een aangepaste EventListener toolog gebeurtenissen tooa bestand gebruiken.



## <a name="next-steps"></a>Volgende stappen
Hallo dezelfde tracering code toegevoegd tooyour toepassing werkt ook met Hallo diagnostische gegevens van uw toepassing in een Azure-cluster. Het uitchecken van deze artikelen die verschillende opties voor hulpprogramma's Hallo Hallo bespreken en beschrijven hoe tooset deze.
* [Hoe toocollect logboeken met diagnostische Azure-gegevens](service-fabric-diagnostics-how-to-setup-lad.md)
