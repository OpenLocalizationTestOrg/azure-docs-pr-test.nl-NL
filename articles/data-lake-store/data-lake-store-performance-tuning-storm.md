---
title: aaaAzure Data Lake Store Storm prestaties afstemmen richtlijnen | Microsoft Docs
description: Azure Data Lake Store Storm prestaties afstemmen richtlijnen
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Prestaties afstemmen richtlijnen voor Storm op HDInsight en Azure Data Lake Store

Begrijpen factoren Hallo die u overwegen moeten wanneer u Hallo prestaties van een Azure-Storm-topologie afstemmen. Bijvoorbeeld, is het belangrijk toounderstand Hallo kenmerken van Hallo-werk dat door Hallo spouts en Hallo bolts (of werk Hallo is voor i/o- of geheugenintensief). In dit artikel bevat informatie over een reeks prestaties afstemmen richtlijnen over het oplossen van veelvoorkomende problemen.

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Een Azure HDInsight-cluster** met toegang tooa Data Lake Store-account. Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Zorg ervoor dat u extern bureaublad inschakelen voor Hallo-cluster.
* **Een Storm-cluster op Data Lake Store met**. Zie voor meer informatie [Storm op HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Prestaties afstemmen richtlijnen voor het Data Lake Store**.  Raadpleeg voor algemene prestaties concepten, [Data Lake Store prestaties afstemmen richtlijnen](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Hallo parallelle uitvoering van de topologie Hallo afstemmen

Mogelijk kunnen tooimprove prestaties door toenemende Hallo gelijktijdigheid van Hallo i/o-tooand van Data Lake Store. Een Storm-topologie bevat een set met configuraties die Hallo parallelle uitvoering bepalen:
* Het aantal werkprocessen (Hallo werknemers worden evenredig verdeeld over Hallo VM's).
* Aantal spout executor exemplaren.
* Aantal bolt executor exemplaren.
* Aantal spout taken.
* Het aantal taken dat bolt.

Denk bijvoorbeeld op een cluster met 4 VM's en 4 werkprocessen, 32 spout Executor en 32 spout taken en 256 bolt Executor en 512 bolt taken, Hallo volgende:

Elke supervisor, dat een werkrolknooppunt is, heeft één werknemer proces van de virtuele machine (JVM) Java. Dit proces JVM beheert 4 spout threads en 64 bolt threads. Binnen elke thread worden taken worden opeenvolgend uitgevoerd. Elke thread spout is 1 taak met Hallo voorafgaand aan de configuratie, en elke thread bolt 2 taken heeft.

In Storm, hier verschillende onderdelen die zijn betrokken zijn hello en hoe ze invloed hebben op Hallo niveau van parallelle uitvoering die u hebt:
* Hallo-hoofdknooppunt (aangeroepen Nimbus in Storm) is gebruikte toosubmit en beheren van taken. Deze knooppunten hebben geen invloed op Hallo mate van parallelle uitvoering.
* Hallo supervisor knooppunten. In HDInsight, komt dit overeen tooa werkrolknooppunt Azure VM.
* Hallo worker taken zijn Storm processen in Hallo virtuele machines. Elke taak worker correspondeert tooa JVM-exemplaar. Storm distribueert Hallo-nummer van werkprocessen u toohello worker-knooppunten opgeven zo gelijkmatig mogelijk.
* Spout en Bolts executor-exemplaren. Elk exemplaar executor komt overeen tooa thread is uitgevoerd binnen Hallo werknemers (JVMs).
* Storm-taken. Dit zijn logische taken dat elk van deze threads uitgevoerd. Hierdoor niet gewijzigd Hallo van parallelle uitvoering, zodat u evalueren moet als u meerdere taken per executor of niet nodig.

### <a name="get-hello-best-performance-from-data-lake-store"></a>De beste prestaties Hallo ophalen uit Data Lake Store

Als u werkt met Data Lake Store, krijgt u de beste prestaties Hallo als u het volgende Hallo:
* Coalesce uw kleine voegt in grotere (bij voorkeur 4 MB).
* Als veel gelijktijdige aanvragen, zoals u kunt doen. Omdat elke thread bolt blokkerende leest doet, wilt u toohave ergens in Hallo bereik van 8-12-threads per core. Dit houdt Hallo NIC en Hallo CPU goed worden gebruikt. Een grotere virtuele machine kunt meer gelijktijdige aanvragen.  

### <a name="example-topology"></a>Voorbeeldtopologie

Stel dat u hebt een 8 worker-knooppunten met een D13v2 Azure VM. Deze VM is 8 kernen, dus tussen Hallo 8 worker-knooppunten, hebt u de 64-totaal aantal kernen.

Stel, dat we 8 bolt threads per core doen. Gegeven 64 kernen betekent dit dat we willen 512 totale bolt executor exemplaren (dat wil zeggen, threads). Stel dat in dit geval we beginnen met een JVM per VM en hoofdzakelijk gebruiken Hallo thread gelijktijdigheid binnen Hallo JVM tooachieve gelijktijdigheid van taken. Dit betekent dat moet 8 worker-taken (één per virtuele machine van Azure) en 512 bolt Executor. In deze configuratie probeert Storm toodistribute de werknemers Hallo gelijkmatig over worker-knooppunten (ook wel bekend als supervisor knooppunten), zodat elk werkrolknooppunt 1 JVM. Nu binnen Hallo toezichthouders, Storm toodistribute Hallo Executor gelijkmatig tussen toezichthouders probeert, threads geeft elke supervisor (dat wil zeggen, JVM) 8 elk.

## <a name="tune-additional-parameters"></a>Extra parameters optimaliseren
Nadat u de basistopologie Hallo hebt, kunt u overwegen of u wilt dat tootweak Hallo parameters:
* **Aantal JVMs per werkrolknooppunt.** Als er een grote hoeveelheden gegevensstructuur (bijvoorbeeld een opzoektabel) is een afzonderlijk exemplaar in die u als host fungeren in elke JVM-geheugen vereist. U kunt ook kunt u Hallo gegevensstructuur in veel threads hebt u minder JVMs. Voor Hallo bolt van i/o maakt het aantal JVMs Hallo geen zoveel mogelijk van een verschil als het aantal threads dat is toegevoegd via deze JVMs Hallo. Eenvoud, is het een goed idee toohave een JVM per worker. Afhankelijk van wat uw bolt doet of welke toepassingen u verwerking vereist, hoewel u toochange dit nummer wellicht.
* **Het aantal spout Executor.** Omdat hello voorgaande voorbeeld bolts gebruikt voor het schrijven van tooData Lake Store, wordt het aantal spouts Hallo is niet rechtstreeks relevante toohello bolt prestaties. Echter, afhankelijk van Hallo hoeveelheid verwerking of i/o-gebeurt er in Hallo spout, is het een goed idee spouts tootune hello voor de beste prestaties. Zorg ervoor dat er voldoende spouts toobe kunnen tookeep Hallo bolts bezet. Hallo uitvoer frequenties van Hallo spouts moeten overeenkomen met de Hallo doorvoer van Hallo bolts. Hallo werkelijke configuratie, is afhankelijk van Hallo spout.
* **Het aantal taken.** Elke bolt wordt uitgevoerd met één thread. Extra taken per bolt bieden niet extra gelijktijdigheid van taken. Hallo enige keer dat ze van het voordeel zijn is als het proces van het Hallo-tuple zijn bevestigd dat een groot deel van uw uitvoeringstijd bolt. Het is een goed idee toogroup die veel tuples in een grotere toevoegen voordat u een bevestiging vanuit Hallo bolt verzenden. In de meeste gevallen dus bieden meerdere taken geen extra voordelen.
* **Lokaal of groepering in willekeurige volgorde.** Wanneer deze instelling is ingeschakeld, tuples toobolts binnen Hallo worden verzonden hetzelfde werkproces. Dit vermindert tussen processen aanroepen voor communicatie en netwerken. Dit wordt aanbevolen voor de meeste topologieën.

Dit eenvoudige scenario is een goed uitgangspunt. Testen door uw eigen gegevens tootweak hello voorafgaand aan parameters tooachieve optimale prestaties.

## <a name="tune-hello-spout"></a>Hallo spout afstemmen

Hallo instellingen tootune hello spout te volgen, kunt u wijzigen.

- **Tuple time-out: topology.message.timeout.secs**. Deze instelling bepaalt Hallo hoeveelheid duurt voordat een bericht toocomplete en bevestiging, ontvangen voordat het wordt beschouwd als mislukt.

- **Maximaal geheugen per werkproces: worker.childopts**. Deze instelling kunt u aanvullende opdrachtregelparameters toohello Java werknemers opgeven. Hallo meest gebruikte instelling hier is XmX waarmee wordt bepaald Hallo maximaal geheugen toegewezen tooa JVM van heap.

- **Maximum aantal spout in behandeling: topology.max.spout.pending**. Deze instelling bepaalt het aantal tuples die in vlucht (nog niet op alle knooppunten op Hallo topologie bevestigd) per thread spout op elk gewenst moment Hallo.

 Een goede berekening toodo is tooestimate Hallo grootte van elk van uw tuples. Vervolgens bepalen hoeveel geheugen een spout thread heeft. Hallo Totaal geheugen toegewezen tooa thread, gedeeld door deze waarde geeft de bovengrens Hallo voor Hallo max spout in behandeling zijnde parameter.

## <a name="tune-hello-bolt"></a>Hallo bolt afstemmen
Wanneer u tooData Lake Store schrijft, een synchronisatiebeleid grootte (buffer aan clientzijde Hallo) ingesteld too4 MB. Een domeincontrollerlocaties leeg of hsync() wordt vervolgens alleen uitgevoerd wanneer de buffergrootte Hallo Hallo op deze waarde is. Hallo Data Lake Store-stuurprogramma op Hallo worker VM komt automatisch deze buffering, tenzij u expliciet een hsync() uitvoeren.

Hallo default Data Lake Store Storm bolt heeft een grootte sync Beleidsparameter (fileBufferSize), die gebruikt tootune worden kan deze parameter.

In de I/O-intensieve topologieën, is het een goed idee toohave elke thread bolt tooits eigen bestands- en tooset een bestand rotatie-beleid schrijven (fileRotationSize). Hallo-bestand een bepaalde grootte bereikt, Hallo stroom wordt automatisch gewist als een nieuw bestand wordt geschreven naar. Hallo aanbevolen grootte voor rotatie is 1 GB.

### <a name="handle-tuple-data"></a>Tuple gegevens verwerken

In de Storm bevat een spout op tooa tuple totdat het expliciet is bevestigd door Hallo bolt. Als een tuple door Hallo bolt is gelezen, maar is niet zijn bevestigd, Hallo spout mogelijk niet hebben permanent opgeslagen in Data Lake Store back-end. Nadat een tuple is bevestigd, Hallo spout persistentie kan worden gegarandeerd door Hallo bolt en kunt Hallo brongegevens vervolgens verwijderen uit welke bron is het lezen van.  

Voor optimale prestaties op Data Lake Store, hebt u Hallo bolt buffer is 4 MB aan gegevens van de tuple. Vervolgens schrijven toohello Data Lake Store weer beëindigen als één 4 MB geheugen schrijven. Nadat de Hallo gegevens zijn met succes geschreven toohello store (door de aanroepende hflush()) hello bolt kunt erken Hallo gegevens back toohello spout. Dit is wat voorbeeld Hallo Bolts opgegeven hier heeft. Het is ook acceptabele toohold een groter aantal tuples voordat Hallo hflush() aanroep en Hallo tuples bevestigd. Dit verhoogt echter Hallo aantal tuples in vlucht dat Hallo spout toohold moet en daarom toeneemt Hallo per JVM vereiste hoeveelheid geheugen.

> [!NOTE]
Toepassingen hebben een vereiste tooacknowledge tuples vaker (op gegevensgroottes minder dan 4 MB) om andere redenen voor slechte prestaties. Echter, die invloed kunnen zijn op Hallo i/o doorvoer toohello opslag de back-end. Weeg zorgvuldig deze afweging tegen Hallo bolt van i/o-prestaties.

Hallo frequentie van binnenkomst van tuples niet groot zodat Hallo 4 MB buffer een toofill lang duurt, dan kunt u dit door beperkende:
* Minder buffers toofill vermindert het aantal bolts hello, dus er zijn.
* Elke x leegmaakacties of elk y milliseconden met een beleid op basis van tijd of het aantal is gebaseerd, waarbij een hflush() is geactiveerd en Hallo tuples samengevoegd tot nu toe back zijn bevestigd.

Houd er rekening mee dat Hallo doorvoer in dit geval lager is, maar met een langzame snelheid van gebeurtenissen, maximale doorvoer niet de grootste doelstelling Hallo toch is. Deze oplossingen te beperken Hallo totale tijd die het duurt voordat een tuple tooflow via toohello store. Dit kan van belang als u wilt dat een realtime pijplijn zelfs met een snelheid van de lage gebeurtenissen. Ook Opmerking Als uw tuple frequentie van binnenkomst laag is, aan te Hallo topology.message.timeout_secs parameter, passen moet zodat Hallo tuples geen time-out terwijl ze in de buffer opgeslagen of verwerkt.

## <a name="monitor-your-topology-in-storm"></a>Uw Storm-topologie bewaken  
Terwijl uw topologie wordt uitgevoerd, kunt u het bewaken in Hallo Storm-gebruikersinterface. Hier volgen Hallo belangrijkste parameters toolook op:

* **Latentie van totale proces worden uitgevoerd.** Dit is de gemiddelde tijd Hallo tuple voor tuple toobe verzonden door Hallo spout duurt, verwerkt door de bolt hello en bevestigd.

* **Totaal aantal bolt proces latentie.** Dit is Hallo van de gemiddelde tijd besteed aan het Hallo-tuple van Hallo bolt totdat het ontvangt een bevestiging.

* **Totaal aantal bolt uitvoeren latentie.** Dit is Hallo gemiddelde tijd besteed door Hallo bolt in Hallo methode uitvoeren.

* **Aantal fouten.** Dit verwijst aantal tuples die niet volledig verwerkt voordat ze time-out toobe toohello.

* **De capaciteit.** Dit is een meting van hoeveel van uw systeem is. Als dit nummer 1 is, worden uw bolts snel ze kunnen werken. Als deze kleiner dan 1 is, verhoogt u Hallo parallelle uitvoering. Als deze groter dan 1 is, verlaagt u Hallo parallelle uitvoering.

## <a name="troubleshoot-common-problems"></a>Algemene problemen
Hier volgen enkele algemene probleemoplossing-scenario's.
* **Er zijn veel tuples time-out opgetreden.** Elk knooppunt in het Hallo-topologie toodetermine kijken waar Hallo knelpunt is. Hallo meest voorkomende reden hiervoor is dat Hallo bolts niet kunnen tookeep up met Hallo spouts zijn. Dit leidt tootuples vertraging Hallo interne buffers tijdens het wachten op toobe verwerkt. Overweeg het Hallo-time-outwaarde oplopende of aflopende volgorde van maximale spout Hallo in behandeling.

* **Er is een latentie van hoge totale proces worden uitgevoerd, maar een proces bolt lage latentie.** In dit geval is het mogelijk dat Hallo tuples worden niet wordt bevestigd snel genoeg. Controleer of er een voldoende aantal acknowledgers zijn. Een andere mogelijkheid is dat ze nog in de wachtrij hello te lang voordat Hallo bolts start deze worden verwerkt. Hallo max spout in behandeling zijnde afnemen.

* **Er is een bolt hoge latentie uitvoeren.** Dit betekent dat Hallo execute() methode van uw bolt duurt te lang is. Hallo-code optimaliseren of bekijk schrijven grootten en gedrag leegmaken.

### <a name="data-lake-store-throttling"></a>Beperking van Data Lake Store
Als u op Hallo limieten van de bandbreedte die worden geleverd door de Data Lake Store, kunt u taakfouten ziet. Controleer de logboeken van de taak voor de beperking van fouten. U kunt Hallo parallelle uitvoering verlagen door het vergroten van de container.    

toocheck als u ophalen beperkt, Hallo foutopsporing aan clientzijde Hallo logboekregistratie inschakelen:

1. In **Ambari** > **Storm** > **Config** > **geavanceerde storm-worker-log4j**, wijzigen  **&lt;root niveau = 'info'&gt;**  te**&lt;root niveau = 'debug'&gt;**. Alle Hallo knooppunten/service Hallo configuratie tootake effect opnieuw starten.
2. Monitor Hallo Storm-topologie logboeken op de worker-knooppunten (onder /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;poort&gt;/worker.log) voor Data Lake Store uitzonderingen beperking.

## <a name="next-steps"></a>Volgende stappen
Aanvullende prestaties afstemmen voor Storm in kan worden verwezen [deze blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Zie voor een toorun nog een voorbeeld [zo'n op GitHub](https://github.com/hdinsight/storm-performance-automation).
