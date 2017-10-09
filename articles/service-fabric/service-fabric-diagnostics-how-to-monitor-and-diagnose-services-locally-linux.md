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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="e7eab-103">Controle en diagnose van services in de instellingen voor een lokale computer-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="e7eab-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7eab-104">Windows</span><span class="sxs-lookup"><span data-stu-id="e7eab-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="e7eab-105">Linux</span><span class="sxs-lookup"><span data-stu-id="e7eab-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="e7eab-106">Wacht tot services toocontinue met minimale onderbrekingen toohello gebruikerservaring bewaking, detecteren, onderzoeken en het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="e7eab-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="e7eab-107">Controle en diagnostische gegevens zijn essentieel in een werkelijke geïmplementeerde productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e7eab-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="e7eab-108">Een vergelijkbaar model overstap tijdens de ontwikkeling van services zorgt ervoor dat Hallo diagnostische pijplijn werkt wanneer u de productieomgeving tooa verplaatst.</span><span class="sxs-lookup"><span data-stu-id="e7eab-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="e7eab-109">Service Fabric eenvoudig service ontwikkelaars tooimplement diagnostics dat naadloos voor zowel lokale ontwikkeling één machine-instellingen als de echte productie cluster instellingen werkt.</span><span class="sxs-lookup"><span data-stu-id="e7eab-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="e7eab-110">Foutopsporing van Service Fabric-Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="e7eab-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="e7eab-111">Voor Java-toepassingen [meerdere frameworks voor logboekregistratie](http://en.wikipedia.org/wiki/Java_logging_framework) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="e7eab-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="e7eab-112">Aangezien `java.util.logging` is de standaardoptie Hallo Hello JRE, wordt ook gebruikt voor Hallo [codevoorbeelden in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e7eab-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="e7eab-113">Hallo bespreking van de volgende wordt uitgelegd hoe tooconfigure hello `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="e7eab-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="e7eab-114">Met behulp van java.util.logging kunt u uw toepassing omleiden registreert toomemory, uitvoerstromen, console-bestanden of sockets.</span><span class="sxs-lookup"><span data-stu-id="e7eab-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="e7eab-115">Er zijn standaard handlers al opgegeven in het Hallo-framework voor elk van deze opties.</span><span class="sxs-lookup"><span data-stu-id="e7eab-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="e7eab-116">Kunt u een `app.properties` bestand tooconfigure Hallo bestandshandler voor uw toepassing tooredirect alle logboeken tooa lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="e7eab-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="e7eab-117">Hallo volgende codefragment bevat de voorbeeldconfiguratie van een:</span><span class="sxs-lookup"><span data-stu-id="e7eab-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="e7eab-118">Hallo map verwijzen tooby hello `app.properties` bestand moet bestaan.</span><span class="sxs-lookup"><span data-stu-id="e7eab-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="e7eab-119">Na het Hallo `app.properties` -bestand wordt gemaakt, moet u tooalso uw script post-punt wijzigen `entrypoint.sh` in Hallo `<applicationfolder>/<servicePkg>/Code/` map tooset Hallo eigenschap `java.util.logging.config.file` te`app.propertes` bestand.</span><span class="sxs-lookup"><span data-stu-id="e7eab-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="e7eab-120">Hallo-vermelding moet eruitzien als Hallo codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="e7eab-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="e7eab-121">Deze configuratie resulteert in Logboeken worden verzameld in een draaiende wijze op `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="e7eab-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="e7eab-122">Hallo logboekbestand in dit geval is de naam mysfapp%u.%g.log waar:</span><span class="sxs-lookup"><span data-stu-id="e7eab-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="e7eab-123">**%u** is een uniek nummer tooresolve conflicten tussen processen gelijktijdig Java.</span><span class="sxs-lookup"><span data-stu-id="e7eab-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="e7eab-124">**%g** Hallo generatie nummer toodistinguish tussen het roteren van Logboeken is.</span><span class="sxs-lookup"><span data-stu-id="e7eab-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="e7eab-125">Standaard als er geen handler expliciet is geconfigureerd, is Hallo console handler geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="e7eab-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="e7eab-126">Een kunt Hallo Logboeken in syslog onder /var/log/syslog weergeven.</span><span class="sxs-lookup"><span data-stu-id="e7eab-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="e7eab-127">Zie voor meer informatie, Hallo [codevoorbeelden in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e7eab-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="e7eab-128">Foutopsporing van Service Fabric C#-toepassingen</span><span class="sxs-lookup"><span data-stu-id="e7eab-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="e7eab-129">Meerdere frameworks er beschikbaar zijn voor het traceren van CoreCLR toepassingen op Linux.</span><span class="sxs-lookup"><span data-stu-id="e7eab-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="e7eab-130">Zie voor meer informatie [GitHub: logboekregistratie](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="e7eab-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="e7eab-131">Aangezien EventSource bekend tooC # ontwikkelaars, is dit artikel EventSource wordt gebruikt voor tracering in CoreCLR voorbeelden op Linux.</span><span class="sxs-lookup"><span data-stu-id="e7eab-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="e7eab-132">de eerste stap Hallo is tooinclude System.Diagnostics.Tracing zodat u kunt uw logboeken toomemory, uitvoerstromen of console-bestanden schrijven.</span><span class="sxs-lookup"><span data-stu-id="e7eab-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="e7eab-133">Voor logboekregistratie met behulp van EventSource, voegt u Hallo project tooyour project.json te volgen:</span><span class="sxs-lookup"><span data-stu-id="e7eab-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="e7eab-134">U kunt een aangepaste EventListener toolisten gebruiken voor Hallo service gebeurtenis en klik vervolgens op de juiste wijze hen omleidt tootrace bestanden.</span><span class="sxs-lookup"><span data-stu-id="e7eab-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="e7eab-135">Hallo toont volgende codefragment een Voorbeeldimplementatie van logboekregistratie met behulp van EventSource en een aangepaste EventListener:</span><span class="sxs-lookup"><span data-stu-id="e7eab-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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


<span data-ttu-id="e7eab-136">Hallo voorgaande codefragment levert Hallo logboeken tooa bestand in `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="e7eab-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="e7eab-137">Deze naam moet toobe op de juiste wijze bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e7eab-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="e7eab-138">Als u wilt dat tooredirect Hallo logboeken tooconsole, gebruikt u Hallo volgende codefragment in uw aangepaste EventListener-klasse:</span><span class="sxs-lookup"><span data-stu-id="e7eab-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="e7eab-139">voorbeelden op Hallo [voorbeelden C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource en een aangepaste EventListener toolog gebeurtenissen tooa bestand gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e7eab-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e7eab-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e7eab-140">Next steps</span></span>
<span data-ttu-id="e7eab-141">Hallo dezelfde tracering code toegevoegd tooyour toepassing werkt ook met Hallo diagnostische gegevens van uw toepassing in een Azure-cluster.</span><span class="sxs-lookup"><span data-stu-id="e7eab-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="e7eab-142">Het uitchecken van deze artikelen die verschillende opties voor hulpprogramma's Hallo Hallo bespreken en beschrijven hoe tooset deze.</span><span class="sxs-lookup"><span data-stu-id="e7eab-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="e7eab-143">Hoe toocollect logboeken met diagnostische Azure-gegevens</span><span class="sxs-lookup"><span data-stu-id="e7eab-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
