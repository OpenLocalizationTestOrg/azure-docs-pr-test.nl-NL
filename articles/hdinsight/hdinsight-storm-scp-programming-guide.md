---
title: Programmeerhandleiding voor SCP.NET | Microsoft Docs
description: "Informatie over het gebruik van SCP.NET om te maken. Storm-topologieën op basis van NET voor gebruik met Storm op HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="e28d5-103">Programmeerhandleiding voor SCP</span><span class="sxs-lookup"><span data-stu-id="e28d5-103">SCP programming guide</span></span>
<span data-ttu-id="e28d5-104">SCP is een platform voor het bouwen van realtime, betrouwbare, consistente en hoge prestaties gegevensverwerking toepassing.</span><span class="sxs-lookup"><span data-stu-id="e28d5-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="e28d5-105">Het is gebouwd boven [Apache Storm](http://storm.incubator.apache.org/) --een stroom verwerking door de community's van de OSS-systeem.</span><span class="sxs-lookup"><span data-stu-id="e28d5-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="e28d5-106">Storm is ontworpen voor door Nathan Marz en open source door Twitter.</span><span class="sxs-lookup"><span data-stu-id="e28d5-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="e28d5-107">Hierbij wordt gebruikgemaakt van [Apache ZooKeeper](http://zookeeper.apache.org/), een ander Apache project om in te schakelen uiterst betrouwbare gedistribueerd beheer coördinatie en status.</span><span class="sxs-lookup"><span data-stu-id="e28d5-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="e28d5-108">Niet alleen het SCP-project overgebracht Storm op Windows maar ook het project toegevoegd uitbreidingen en aanpassingen voor het Windows-ecosysteem.</span><span class="sxs-lookup"><span data-stu-id="e28d5-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="e28d5-109">De uitbreidingen functionaliteit voor .NET-ontwikkelaars en bibliotheken bevatten, de aanpassing omvat implementatie op basis van Windows.</span><span class="sxs-lookup"><span data-stu-id="e28d5-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="e28d5-110">De uitbreiding en aanpassing is gedaan zodanig dat we hoeft niet te vertakken de OSS-projecten en we kunnen gebruikmaken van afgeleide ecosystemen gebouwd op Storm.</span><span class="sxs-lookup"><span data-stu-id="e28d5-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="e28d5-111">Het verwerken van model</span><span class="sxs-lookup"><span data-stu-id="e28d5-111">Processing model</span></span>
<span data-ttu-id="e28d5-112">De gegevens in SCP is gemodelleerd als ononderbroken streams van tuples.</span><span class="sxs-lookup"><span data-stu-id="e28d5-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="e28d5-113">De tuples doorgaans stromen in sommige wachtrij eerst en vervolgens opgenomen en getransformeerd door zakelijke logica gehost binnen een Storm-topologie, ten slotte de uitvoer tuples naar een ander SCP-systeem kan de eigenschappen of worden doorgevoerd voor stores, zoals gedistribueerd bestandssysteem of databases zoals SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e28d5-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Een diagram van een wachtrij gegevens op de verwerking die een gegevensarchief feeds voeding](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="e28d5-115">In Storm definieert u de Toepassingstopologie van een een grafiek van de berekening.</span><span class="sxs-lookup"><span data-stu-id="e28d5-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="e28d5-116">Elk knooppunt in een topologie bevat de logica voor verwerking en koppelingen tussen knooppunten gegevensstroom aangeven.</span><span class="sxs-lookup"><span data-stu-id="e28d5-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="e28d5-117">De knooppunten invoergegevens invoeren in de topologie worden Spouts, dat kunnen worden gebruikt voor het sequentiëren van de gegevens worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="e28d5-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="e28d5-118">De ingevoerde gegevens kan zich bevinden in het bestand Logboeken, transactionele database, systeem-prestatiemeteritem enzovoort. De knooppunten met beide stromen en uitvoergegevens heten Bolts, wat de werkelijke gegevens filteren en selecties en cumulatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="e28d5-119">SCP ondersteunt pogingen op in de minste eenmaal en precies-eenmaal verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e28d5-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="e28d5-120">In een gedistribueerde toepassing voor streaming verwerken, kunnen zich voordoen diverse fouten tijdens het verwerken van gegevens, zoals netwerkuitval, machinestoringen of fout in gebruikerscode enzovoort. Op de minste eenmaal verwerken zorgt ervoor dat alle gegevens ten minste één keer wordt verwerkt door automatisch dezelfde gegevens als er treedt een fout.</span><span class="sxs-lookup"><span data-stu-id="e28d5-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="e28d5-121">Op de minste eenmaal verwerken eenvoudig en betrouwbaar en geschikte goed in veel toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="e28d5-122">Wanneer de toepassing exacte tellen vereist, bijvoorbeeld is op in de minste eenmaal verwerken echter onvoldoende omdat dezelfde gegevens kan mogelijk worden afgespeeld in de Toepassingstopologie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="e28d5-123">In dat geval, precies-zodra de verwerking is ontworpen om te controleren of het resultaat juist is zelfs wanneer de gegevens kan worden onderschept en verwerkt meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="e28d5-124">SCP kan .NET-ontwikkelaars realtime gegevens proces om toepassingen te ontwikkelen terwijl hefboomwerking Java Virtual Machine (JVM) gebaseerd Storm onder de behandeld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="e28d5-125">De .NET- en JVM communiceert via een TCP-lokale socket.</span><span class="sxs-lookup"><span data-stu-id="e28d5-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="e28d5-126">Elke Spout/Bolt bestaat uit in feite een paar .net/Java-proces waarin de gebruiker logica wordt uitgevoerd in .net-proces als een invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="e28d5-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="e28d5-127">Als u wilt maken van een toepassing gegevensverwerking bovenop SCP, zijn verschillende stappen nodig:</span><span class="sxs-lookup"><span data-stu-id="e28d5-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="e28d5-128">Ontwerpen en implementeren van de Spouts ophalen van gegevens uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="e28d5-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="e28d5-129">Ontwerpen en implementeren van Bolts voor het verwerken van de invoergegevens en opslaan van gegevens naar externe winkels zoals Database.</span><span class="sxs-lookup"><span data-stu-id="e28d5-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="e28d5-130">De topologie ontwerpen, indienen en uitvoeren van de topologie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="e28d5-131">De topologie definieert hoekpunten en de gegevens stromen tussen de hoekpunten.</span><span class="sxs-lookup"><span data-stu-id="e28d5-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="e28d5-132">SCP zal duren voordat de topologie-specificatie en deze implementeren op een Storm-cluster, waarin elk hoekpunt wordt uitgevoerd op één knooppunt van de logische.</span><span class="sxs-lookup"><span data-stu-id="e28d5-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="e28d5-133">De failover- en vergroten/verkleinen wordt worden afgehandeld door de Storm-Taakplanner.</span><span class="sxs-lookup"><span data-stu-id="e28d5-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="e28d5-134">Dit document gebruiken enkele eenvoudige voorbeelden voor het bouwen van gegevensverwerking toepassing met SCP doorlopen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="e28d5-135">SCP-invoegtoepassing Interface</span><span class="sxs-lookup"><span data-stu-id="e28d5-135">SCP Plugin Interface</span></span>
<span data-ttu-id="e28d5-136">SCP-invoegtoepassingen (of toepassingen) zijn zelfstandige exe die beide tijdens kunnen uitvoeren in Visual Studio de ontwikkelingsfase en worden aangesloten op de Storm-pijplijn na de implementatie in productie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="e28d5-137">Het schrijven van de invoegtoepassing SCP dezelfde manier als andere standaard Windows-consoletoepassingen schrijven is.</span><span class="sxs-lookup"><span data-stu-id="e28d5-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="e28d5-138">SCP.NET platform declareert een interface voor spout/bolt en de code van de invoegtoepassing gebruiker moet deze interfaces implementeren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="e28d5-139">Het belangrijkste doel van dit ontwerp is dat de gebruiker zich op hun eigen logics bedrijven en andere dingen concentreren kan moet worden verwerkt door het platform SCP.NET verlaten.</span><span class="sxs-lookup"><span data-stu-id="e28d5-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="e28d5-140">De code van de invoegtoepassing gebruiker moet een van de volgende interfaces implementeren, afhankelijk van of de topologie is transactionele of niet-transactionele en Hiermee wordt aangegeven of het onderdeel is spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="e28d5-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="e28d5-141">ISCPSpout</span></span>
* <span data-ttu-id="e28d5-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="e28d5-142">ISCPBolt</span></span>
* <span data-ttu-id="e28d5-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="e28d5-143">ISCPTxSpout</span></span>
* <span data-ttu-id="e28d5-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="e28d5-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="e28d5-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="e28d5-145">ISCPPlugin</span></span>
<span data-ttu-id="e28d5-146">ISCPPlugin is de algemene interface voor alle soorten invoegtoepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="e28d5-147">Het is momenteel een dummy-interface.</span><span class="sxs-lookup"><span data-stu-id="e28d5-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="e28d5-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="e28d5-148">ISCPSpout</span></span>
<span data-ttu-id="e28d5-149">ISCPSpout is de interface voor niet-transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="e28d5-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="e28d5-150">Wanneer `NextTuple()` wordt aangeroepen, de C\# gebruikerscode kan een of meer tuples verzenden.</span><span class="sxs-lookup"><span data-stu-id="e28d5-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="e28d5-151">Als er niets om te verzenden, moet deze methode zonder iets tekensetcodering retourneren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="e28d5-152">Houd er rekening mee dat `NextTuple()`, `Ack()`, en `Fail()` worden genoemd in een lus in een enkele thread in C\# proces.</span><span class="sxs-lookup"><span data-stu-id="e28d5-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="e28d5-153">Wanneer er geen tuples verzenden, is het beleefd NextTuple slaapstand gedurende een korte tijd (zoals 10 milliseconden) niet te verspillen te veel CPU hebben.</span><span class="sxs-lookup"><span data-stu-id="e28d5-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="e28d5-154">`Ack()`en `Fail()` alleen wanneer het ack-mechanisme is ingeschakeld in spec bestand moet worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="e28d5-155">De `seqId` wordt gebruikt voor het identificeren van de tuple die bevestigd of is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="e28d5-156">Dus als ack in niet-transactionele topologie is ingeschakeld, kan de volgende emit-functie moet worden gebruikt in Spout:</span><span class="sxs-lookup"><span data-stu-id="e28d5-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="e28d5-157">Als ack wordt niet ondersteund in niet-transactionele topologie de `Ack()` en `Fail()` kan blijven als lege functie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="e28d5-158">De `parms` invoerparameters in deze functies zijn alleen lege woordenlijst, zijn gereserveerd voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="e28d5-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="e28d5-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="e28d5-159">ISCPBolt</span></span>
<span data-ttu-id="e28d5-160">ISCPBolt is de interface voor niet-transactionele bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="e28d5-161">Wanneer nieuwe tuple beschikbaar is, de `Execute()` voor het verwerken van deze functie wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="e28d5-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="e28d5-162">ISCPTxSpout</span></span>
<span data-ttu-id="e28d5-163">ISCPTxSpout is de interface voor transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="e28d5-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="e28d5-164">Net als bij hun niet-transactionele tegenpost `NextTx()`, `Ack()`, en `Fail()` worden genoemd in een lus in een enkele thread in C\# proces.</span><span class="sxs-lookup"><span data-stu-id="e28d5-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="e28d5-165">Wanneer er geen gegevens verzenden, is het beleefd hebben `NextTx` slaapstand gedurende een korte tijd (10 milliseconden) niet te verspillen te veel CPU.</span><span class="sxs-lookup"><span data-stu-id="e28d5-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="e28d5-166">`NextTx()`wordt aangeroepen voor het starten van een nieuwe transactie, de out-parameter `seqId` wordt gebruikt voor het identificeren van de transactie, wordt ook gebruikt in `Ack()` en `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="e28d5-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="e28d5-167">In `NextTx()`, gebruiker gegevens naar Java kant kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="e28d5-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="e28d5-168">De gegevens worden opgeslagen in ZooKeeper ter ondersteuning van opnieuw afspelen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="e28d5-169">Omdat de capaciteit van ZooKeeper zeer beperkt is, moet de gebruiker alleen metagegevens verzenden, geen grote hoeveelheid gegevens in een transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="e28d5-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="e28d5-170">Storm een transactie automatisch wordt herhaald als het mislukt, dus `Fail()` mag niet worden aangeroepen in normale geval.</span><span class="sxs-lookup"><span data-stu-id="e28d5-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="e28d5-171">Maar als een SCP kan de metagegevens die door transactionele spout controleren, kan worden aangeroepen `Fail()` wanneer de metagegevens is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="e28d5-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="e28d5-172">De `parms` invoerparameters in deze functies zijn alleen lege woordenlijst, zijn gereserveerd voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="e28d5-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="e28d5-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="e28d5-173">ISCPBatchBolt</span></span>
<span data-ttu-id="e28d5-174">ISCPBatchBolt is de interface voor transactionele bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="e28d5-175">`Execute()`wordt aangeroepen wanneer er nieuwe tuple die binnenkomen bij de bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="e28d5-176">`FinishBatch()`wordt aangeroepen wanneer deze transactie is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="e28d5-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="e28d5-177">De `parms` invoerparameter is gereserveerd voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="e28d5-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="e28d5-178">Voor transactionele topologie is een belangrijke concepten – `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="e28d5-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="e28d5-179">Deze twee velden heeft `TxId` en `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="e28d5-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="e28d5-180">`TxId`wordt gebruikt om een bepaalde transactie identificeren en voor een gegeven transactie, kunnen er meerdere poging als de transactie mislukt en wordt opnieuw en nu afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="e28d5-181">SCP.NET nieuwe wordt een ander object ISCPBatchBolt verwerken elk `StormTxAttempt`, net zoals wat Storm moet aan de kant van Java.</span><span class="sxs-lookup"><span data-stu-id="e28d5-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="e28d5-182">Het doel van dit ontwerp is ondersteuning voor parallelle transacties verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="e28d5-183">Gebruiker moet het Houd in gedachten als poging van de transactie is voltooid, wordt het bijbehorende ISCPBatchBolt object vernietigd en garbage collector zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="e28d5-184">Objectmodel</span><span class="sxs-lookup"><span data-stu-id="e28d5-184">Object Model</span></span>
<span data-ttu-id="e28d5-185">SCP.NET biedt ook een eenvoudige reeks key objecten voor ontwikkelaars voor het programmeren met.</span><span class="sxs-lookup"><span data-stu-id="e28d5-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="e28d5-186">Ze zijn **Context**, **StateStore**, en **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="e28d5-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="e28d5-187">Ze worden besproken in het gedeelte van de rest van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="e28d5-188">Context</span><span class="sxs-lookup"><span data-stu-id="e28d5-188">Context</span></span>
<span data-ttu-id="e28d5-189">Context biedt een actieve omgeving naar de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e28d5-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="e28d5-190">Elk exemplaar ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) heeft een corresponderende contextexemplaar.</span><span class="sxs-lookup"><span data-stu-id="e28d5-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="e28d5-191">De functionaliteit van Context kan worden onderverdeeld in twee delen: (1) het statische deel die beschikbaar in de hele C is\# verwerken, (2) het dynamische deel die alleen beschikbaar voor het specifieke exemplaar van de Context.</span><span class="sxs-lookup"><span data-stu-id="e28d5-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="e28d5-192">Statische deel</span><span class="sxs-lookup"><span data-stu-id="e28d5-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="e28d5-193">`Logger`is beschikbaar voor logboek-doel.</span><span class="sxs-lookup"><span data-stu-id="e28d5-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="e28d5-194">`pluginType`wordt gebruikt om aan te geven van het type van de invoegtoepassing van de C\# proces.</span><span class="sxs-lookup"><span data-stu-id="e28d5-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="e28d5-195">Als het C\# proces wordt uitgevoerd in de lokale testmodus (zonder Java), het type van de invoegtoepassing is `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="e28d5-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="e28d5-196">`Config`ophalen van parameters voor de configuratie van Java-zijde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e28d5-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="e28d5-197">De parameters worden doorgegeven van Java-kant wanneer C\# invoegtoepassing is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e28d5-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="e28d5-198">De `Config` parameters worden onderverdeeld in twee delen: `stormConf` en `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="e28d5-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="e28d5-199">`stormConf`parameters zijn gedefinieerd door Storm is en `pluginConf` de parameters die zijn gedefinieerd door SCP is.</span><span class="sxs-lookup"><span data-stu-id="e28d5-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="e28d5-200">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e28d5-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="e28d5-201">`TopologyContext`wordt geleverd als u de topologie-context, is het meest geschikt voor onderdelen met meerdere parallelle uitvoering.</span><span class="sxs-lookup"><span data-stu-id="e28d5-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="e28d5-202">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e28d5-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="e28d5-203">Dynamische deel</span><span class="sxs-lookup"><span data-stu-id="e28d5-203">Dynamic Part</span></span>
<span data-ttu-id="e28d5-204">De volgende interfaces zijn relevant zijn voor een bepaald contextexemplaar.</span><span class="sxs-lookup"><span data-stu-id="e28d5-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="e28d5-205">Het Context-exemplaar is gemaakt door SCP.NET platform en doorgegeven aan de gebruikerscode:</span><span class="sxs-lookup"><span data-stu-id="e28d5-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="e28d5-206">Voor niet-transactionele spout ondersteunende ack, krijgt u de volgende methode:</span><span class="sxs-lookup"><span data-stu-id="e28d5-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="e28d5-207">Voor niet-transactionele bolt ack ondersteunen, moet deze expliciet `Ack()` of `Fail()` de tuple deze ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="e28d5-208">En bij het genereren van nieuwe tuple, moet deze ook de ankers van de nieuwe tuple opgeven.</span><span class="sxs-lookup"><span data-stu-id="e28d5-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="e28d5-209">De volgende methoden zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e28d5-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="e28d5-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="e28d5-210">StateStore</span></span>
<span data-ttu-id="e28d5-211">`StateStore`metagegevens van services, monotone reeks genereren en wacht gratis coördinatie biedt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="e28d5-212">Een hoger niveau gedistribueerde gelijktijdigheid abstracties kunnen worden gebaseerd op `StateStore`, met inbegrip van gedistribueerde vergrendelingen, gedistribueerde wachtrijen, barrières en transactieservices.</span><span class="sxs-lookup"><span data-stu-id="e28d5-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="e28d5-213">SCP-toepassingen kunnen gebruikmaken van de `State` object voor het persistent maken van sommige gegevens in ZooKeeper, met name voor transactionele topologie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="e28d5-214">Dit doet, als transactionele spout is vastgelopen en opnieuw start, kunt de benodigde informatie van ZooKeeper ophalen en kunt u de pijplijn opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e28d5-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="e28d5-215">De `StateStore` is hoofdzakelijk deze methoden van object:</span><span class="sxs-lookup"><span data-stu-id="e28d5-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="e28d5-216">De `State` is hoofdzakelijk deze methoden van object:</span><span class="sxs-lookup"><span data-stu-id="e28d5-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="e28d5-217">Voor de `Commit()` methode, wanneer simpleMode is ingesteld op true, deze gewoon, verwijdert u de bijbehorende ZNode in ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="e28d5-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="e28d5-218">Anders wordt de huidige ZNode en het toevoegen van een nieuw knooppunt in de DOORGEVOERD zullen worden verwijderd\_pad.</span><span class="sxs-lookup"><span data-stu-id="e28d5-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="e28d5-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="e28d5-219">SCPRuntime</span></span>
<span data-ttu-id="e28d5-220">SCPRuntime biedt de volgende twee methoden.</span><span class="sxs-lookup"><span data-stu-id="e28d5-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="e28d5-221">`Initialize()`wordt gebruikt voor het initialiseren van de SCP runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e28d5-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="e28d5-222">Bij deze methode wordt de C\# proces maakt verbinding met de Java-zijde en configuratieparameters opgehaald en -topologie-context.</span><span class="sxs-lookup"><span data-stu-id="e28d5-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="e28d5-223">`LaunchPlugin()`wordt gebruikt voor de verwerking berichtenlus starten.</span><span class="sxs-lookup"><span data-stu-id="e28d5-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="e28d5-224">In deze lus, de C\# invoegtoepassing ontvangt berichten formulier Java kant (inclusief signalen tuples en control) en vervolgens verwerken de berichten, bijvoorbeeld het aanroepen van de interfacemethode bieden door de gebruikerscode.</span><span class="sxs-lookup"><span data-stu-id="e28d5-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="e28d5-225">De invoerparameter voor methode `LaunchPlugin()` is een gemachtigde die kan resulteren in een object dat ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt-interface implementeren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="e28d5-226">Voor ISCPBatchBolt, krijgen we `StormTxAttempt` van `parms`, en deze gebruiken om te beoordelen of het is een poging tot herhaald.</span><span class="sxs-lookup"><span data-stu-id="e28d5-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="e28d5-227">Dit gebeurt gewoonlijk op de commit-bolt en dit wordt geïllustreerd in de `HelloWorldTx` voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="e28d5-228">In het algemeen kan het SCP-invoegtoepassingen in twee modi hier worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="e28d5-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="e28d5-229">Lokale testmodus: In deze modus wordt het SCP-invoegtoepassingen (de C\# gebruikerscode) in Visual Studio wordt uitgevoerd tijdens de ontwikkelingsfase bevindt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="e28d5-230">`LocalContext`in deze modus methode biedt voor het serialiseren van de verzonden tuples tot lokale bestanden en ze te lezen in het geheugen kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="e28d5-231">Normale modus: In deze modus wordt het SCP-invoegtoepassingen worden gestart door storm java-proces.</span><span class="sxs-lookup"><span data-stu-id="e28d5-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="e28d5-232">Hier volgt een voorbeeld van het SCP-invoegtoepassing te starten:</span><span class="sxs-lookup"><span data-stu-id="e28d5-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="e28d5-233">Topologie specificatietaal</span><span class="sxs-lookup"><span data-stu-id="e28d5-233">Topology Specification Language</span></span>
<span data-ttu-id="e28d5-234">SCP-topologie-specificatie is een specifieke taal domein voor het beschrijven en topologieën SCP te configureren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="e28d5-235">Deze is gebaseerd op de Storm Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) en SCP is verlengd.</span><span class="sxs-lookup"><span data-stu-id="e28d5-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="e28d5-236">Topologie specificaties kunnen worden verstuurd rechtstreeks naar de storm-cluster voor uitvoering via de ***runspec*** opdracht.</span><span class="sxs-lookup"><span data-stu-id="e28d5-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="e28d5-237">SCP.NET heeft toevoegen Volg-functies voor het definiëren van de transactionele topologie:</span><span class="sxs-lookup"><span data-stu-id="e28d5-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="e28d5-238">**Nieuwe functies**</span><span class="sxs-lookup"><span data-stu-id="e28d5-238">**New Functions**</span></span> | <span data-ttu-id="e28d5-239">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="e28d5-239">**Parameters**</span></span> | <span data-ttu-id="e28d5-240">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e28d5-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e28d5-241">**TX topolopy**</span><span class="sxs-lookup"><span data-stu-id="e28d5-241">**tx-topolopy**</span></span> |<span data-ttu-id="e28d5-242">topologie-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-242">topology-name</span></span><br /><span data-ttu-id="e28d5-243">spout-kaart</span><span class="sxs-lookup"><span data-stu-id="e28d5-243">spout-map</span></span><br /><span data-ttu-id="e28d5-244">bolt-kaart</span><span class="sxs-lookup"><span data-stu-id="e28d5-244">bolt-map</span></span> |<span data-ttu-id="e28d5-245">Definieer een transactionele-topologie met de naam van de topologie &nbsp;spouts definitie kaart en de bolts definitie-kaart</span><span class="sxs-lookup"><span data-stu-id="e28d5-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="e28d5-246">**SCP-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="e28d5-246">**scp-tx-spout**</span></span> |<span data-ttu-id="e28d5-247">exec-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-247">exec-name</span></span><br /><span data-ttu-id="e28d5-248">argumenten</span><span class="sxs-lookup"><span data-stu-id="e28d5-248">args</span></span><br /><span data-ttu-id="e28d5-249">Velden</span><span class="sxs-lookup"><span data-stu-id="e28d5-249">fields</span></span> |<span data-ttu-id="e28d5-250">Definieer een transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="e28d5-250">Define a transactional spout.</span></span> <span data-ttu-id="e28d5-251">Deze wordt uitgevoerd dat de toepassing met ***exec naam*** met ***args***.</span><span class="sxs-lookup"><span data-stu-id="e28d5-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e28d5-252">De ***velden*** wordt de uitvoer-velden voor spout</span><span class="sxs-lookup"><span data-stu-id="e28d5-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="e28d5-253">**SCP-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="e28d5-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="e28d5-254">exec-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-254">exec-name</span></span><br /><span data-ttu-id="e28d5-255">argumenten</span><span class="sxs-lookup"><span data-stu-id="e28d5-255">args</span></span><br /><span data-ttu-id="e28d5-256">Velden</span><span class="sxs-lookup"><span data-stu-id="e28d5-256">fields</span></span> |<span data-ttu-id="e28d5-257">Definieer een transactionele Batch Bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="e28d5-258">Deze wordt uitgevoerd dat de toepassing met ***exec naam*** met ***argumenten.***</span><span class="sxs-lookup"><span data-stu-id="e28d5-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="e28d5-259">De velden is de uitvoer-velden voor bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="e28d5-260">**SCP-tx-doorvoeren-bolt**</span><span class="sxs-lookup"><span data-stu-id="e28d5-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="e28d5-261">exec-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-261">exec-name</span></span><br /><span data-ttu-id="e28d5-262">argumenten</span><span class="sxs-lookup"><span data-stu-id="e28d5-262">args</span></span><br /><span data-ttu-id="e28d5-263">Velden</span><span class="sxs-lookup"><span data-stu-id="e28d5-263">fields</span></span> |<span data-ttu-id="e28d5-264">Definieer een transactionele Committer Bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="e28d5-265">Deze wordt uitgevoerd dat de toepassing met ***exec naam*** met ***args***.</span><span class="sxs-lookup"><span data-stu-id="e28d5-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e28d5-266">De ***velden*** wordt de uitvoer-velden voor bolt</span><span class="sxs-lookup"><span data-stu-id="e28d5-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="e28d5-267">**nontx topolopy**</span><span class="sxs-lookup"><span data-stu-id="e28d5-267">**nontx-topolopy**</span></span> |<span data-ttu-id="e28d5-268">topologie-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-268">topology-name</span></span><br /><span data-ttu-id="e28d5-269">spout-kaart</span><span class="sxs-lookup"><span data-stu-id="e28d5-269">spout-map</span></span><br /><span data-ttu-id="e28d5-270">bolt-kaart</span><span class="sxs-lookup"><span data-stu-id="e28d5-270">bolt-map</span></span> |<span data-ttu-id="e28d5-271">Definieer een niet-transactionele-topologie met de naam van de topologie&nbsp; spouts definitie kaart en de bolts definitie-kaart</span><span class="sxs-lookup"><span data-stu-id="e28d5-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="e28d5-272">**SCP spout**</span><span class="sxs-lookup"><span data-stu-id="e28d5-272">**scp-spout**</span></span> |<span data-ttu-id="e28d5-273">exec-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-273">exec-name</span></span><br /><span data-ttu-id="e28d5-274">argumenten</span><span class="sxs-lookup"><span data-stu-id="e28d5-274">args</span></span><br /><span data-ttu-id="e28d5-275">Velden</span><span class="sxs-lookup"><span data-stu-id="e28d5-275">fields</span></span><br /><span data-ttu-id="e28d5-276">Parameters</span><span class="sxs-lookup"><span data-stu-id="e28d5-276">parameters</span></span> |<span data-ttu-id="e28d5-277">Definieer een niet-transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="e28d5-277">Define a nontransactional spout.</span></span> <span data-ttu-id="e28d5-278">Deze wordt uitgevoerd dat de toepassing met ***exec naam*** met ***args***.</span><span class="sxs-lookup"><span data-stu-id="e28d5-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e28d5-279">De ***velden*** wordt de uitvoer-velden voor spout</span><span class="sxs-lookup"><span data-stu-id="e28d5-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="e28d5-280">De ***parameters*** is optioneel, met bepaalde parameters zoals 'nontransactional.ack.enabled' opgeven.</span><span class="sxs-lookup"><span data-stu-id="e28d5-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="e28d5-281">**SCP-bolt**</span><span class="sxs-lookup"><span data-stu-id="e28d5-281">**scp-bolt**</span></span> |<span data-ttu-id="e28d5-282">exec-naam</span><span class="sxs-lookup"><span data-stu-id="e28d5-282">exec-name</span></span><br /><span data-ttu-id="e28d5-283">argumenten</span><span class="sxs-lookup"><span data-stu-id="e28d5-283">args</span></span><br /><span data-ttu-id="e28d5-284">Velden</span><span class="sxs-lookup"><span data-stu-id="e28d5-284">fields</span></span><br /><span data-ttu-id="e28d5-285">Parameters</span><span class="sxs-lookup"><span data-stu-id="e28d5-285">parameters</span></span> |<span data-ttu-id="e28d5-286">Definieer een niet-transactionele Bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="e28d5-287">Deze wordt uitgevoerd dat de toepassing met ***exec naam*** met ***args***.</span><span class="sxs-lookup"><span data-stu-id="e28d5-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e28d5-288">De ***velden*** wordt de uitvoer-velden voor bolt</span><span class="sxs-lookup"><span data-stu-id="e28d5-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="e28d5-289">De ***parameters*** is optioneel, met bepaalde parameters zoals 'nontransactional.ack.enabled' opgeven.</span><span class="sxs-lookup"><span data-stu-id="e28d5-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="e28d5-290">SCP.NET heeft de volgende codes woorden gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="e28d5-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="e28d5-291">**Trefwoorden**</span><span class="sxs-lookup"><span data-stu-id="e28d5-291">**Key Words**</span></span> | <span data-ttu-id="e28d5-292">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e28d5-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e28d5-293">**: de naam**</span><span class="sxs-lookup"><span data-stu-id="e28d5-293">**:name**</span></span> |<span data-ttu-id="e28d5-294">De naam van de topologie definiëren</span><span class="sxs-lookup"><span data-stu-id="e28d5-294">Define the Topology Name</span></span> |
| <span data-ttu-id="e28d5-295">**: topologie**</span><span class="sxs-lookup"><span data-stu-id="e28d5-295">**:topology**</span></span> |<span data-ttu-id="e28d5-296">Definieer de topologie met behulp van de bovenstaande functies en bouwen in toepassingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="e28d5-297">**: p**</span><span class="sxs-lookup"><span data-stu-id="e28d5-297">**:p**</span></span> |<span data-ttu-id="e28d5-298">Definieer de parallelle uitvoering hint op voor elke spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="e28d5-299">**: config**</span><span class="sxs-lookup"><span data-stu-id="e28d5-299">**:config**</span></span> |<span data-ttu-id="e28d5-300">Definieer de parameter configureren of een bestaande bijwerken</span><span class="sxs-lookup"><span data-stu-id="e28d5-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="e28d5-301">**: schema**</span><span class="sxs-lookup"><span data-stu-id="e28d5-301">**:schema**</span></span> |<span data-ttu-id="e28d5-302">Definieer het Schema van de stroom.</span><span class="sxs-lookup"><span data-stu-id="e28d5-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="e28d5-303">En veelgebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="e28d5-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="e28d5-304">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="e28d5-304">**Parameter**</span></span> | <span data-ttu-id="e28d5-305">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e28d5-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e28d5-306">**'plugin.name'**</span><span class="sxs-lookup"><span data-stu-id="e28d5-306">**"plugin.name"**</span></span> |<span data-ttu-id="e28d5-307">naam van de exe-bestand van de C#-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="e28d5-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="e28d5-308">**'plugin.args'**</span><span class="sxs-lookup"><span data-stu-id="e28d5-308">**"plugin.args"**</span></span> |<span data-ttu-id="e28d5-309">invoegtoepassing argumenten</span><span class="sxs-lookup"><span data-stu-id="e28d5-309">plugin args</span></span> |
| <span data-ttu-id="e28d5-310">**'output.schema'**</span><span class="sxs-lookup"><span data-stu-id="e28d5-310">**"output.schema"**</span></span> |<span data-ttu-id="e28d5-311">Uitvoerschema</span><span class="sxs-lookup"><span data-stu-id="e28d5-311">Output schema</span></span> |
| <span data-ttu-id="e28d5-312">**'nontransactional.ack.enabled'**</span><span class="sxs-lookup"><span data-stu-id="e28d5-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="e28d5-313">Hiermee wordt aangegeven of ack is ingeschakeld voor niet-transactionele-topologie</span><span class="sxs-lookup"><span data-stu-id="e28d5-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="e28d5-314">De opdracht runspec samen met de bits wordt geïmplementeerd, lijkt op het gebruik:</span><span class="sxs-lookup"><span data-stu-id="e28d5-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="e28d5-315">De ***resource dir*** parameter is optioneel, moet u dit opgeven als u wilt een C plug\# toepassings- en deze map bevat de toepassing, de afhankelijkheden en configuraties.</span><span class="sxs-lookup"><span data-stu-id="e28d5-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="e28d5-316">De ***classpath*** parameter ook is optioneel.</span><span class="sxs-lookup"><span data-stu-id="e28d5-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="e28d5-317">Deze wordt gebruikt om het klassepad Java geven als de spec bestand Java Spout of Bolt bevat.</span><span class="sxs-lookup"><span data-stu-id="e28d5-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="e28d5-318">Diverse functies</span><span class="sxs-lookup"><span data-stu-id="e28d5-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="e28d5-319">Invoer en uitvoer Schemadeclaratie</span><span class="sxs-lookup"><span data-stu-id="e28d5-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="e28d5-320">De gebruiker kunt verzenden tuple in C\# proces, het platform moet de tuple serialiseren naar byte [], overdragen naar Java aan clientzijde en Storm deze tuple draagt bij de doelen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="e28d5-321">Ondertussen in de C-downstream component\# proces wordt ontvangen tuple terug vanaf java en converteer deze naar de oorspronkelijke typen per platform, alle deze bewerkingen zijn verborgen door het Platform.</span><span class="sxs-lookup"><span data-stu-id="e28d5-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="e28d5-322">Ter ondersteuning van serialisatie en deserialisatie, moet gebruikerscode het schema van de invoer en uitvoer declareren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="e28d5-323">Het schema i/o-stroom is gedefinieerd als een woordenboek, de sleutel is de StreamId en de waarde is de typen van de kolommen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="e28d5-324">Het onderdeel kan meerdere streams gedeclareerd hebben.</span><span class="sxs-lookup"><span data-stu-id="e28d5-324">The component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="e28d5-325">In de Context-object hebben we de volgende API toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="e28d5-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="e28d5-326">Gebruikerscode moet controleren of de tuples verzonden zich aan het schema is gedefinieerd voor deze stroom of het systeem een runtime-uitzondering genereert.</span><span class="sxs-lookup"><span data-stu-id="e28d5-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="e28d5-327">Ondersteuning voor meerdere Stream</span><span class="sxs-lookup"><span data-stu-id="e28d5-327">Multi-Stream Support</span></span>
<span data-ttu-id="e28d5-328">SCP ondersteunt gebruikerscode om te verzenden of ontvangen van meerdere afzonderlijke streams op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e28d5-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="e28d5-329">De ondersteuning weerspiegelt in de Context-object omdat de methode Emit een optionele stroom-ID-parameter houdt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="e28d5-330">Twee methoden voor het object Context SCP.NET er zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e28d5-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="e28d5-331">Ze worden gebruikt voor het verzenden van Tuple of Tuples om op te geven StreamId.</span><span class="sxs-lookup"><span data-stu-id="e28d5-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="e28d5-332">De StreamId is een tekenreeks en het moet in beide C consistent\# en de topologie definitie-specificaties.</span><span class="sxs-lookup"><span data-stu-id="e28d5-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="e28d5-333">De tekensetcodering naar een niet-bestaande stream wordt runtime-uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="e28d5-334">Velden groeperen</span><span class="sxs-lookup"><span data-stu-id="e28d5-334">Fields Grouping</span></span>
<span data-ttu-id="e28d5-335">De groepering van velden in te bouwen in Strom werkt niet goed in SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="e28d5-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="e28d5-336">De Java-Proxy-zijde alle velden gegevenstypen zijn daadwerkelijk byte [] en de velden groeperen byte [] object hash-code gebruikt voor het uitvoeren van de groepering.</span><span class="sxs-lookup"><span data-stu-id="e28d5-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="e28d5-337">De byte [] object hash-code is het adres van dit object in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="e28d5-338">De groepering worden dus verkeerde voor twee-byte [] objecten die dezelfde inhoud, maar niet hetzelfde adres delen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="e28d5-339">Een groeperingsmethode met de aangepaste SCP.NET toegevoegd en de inhoud van de byte [] wordt gebruikt om de groepering doen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="e28d5-340">In **SPEC** -bestand, de syntaxis is als volgt:</span><span class="sxs-lookup"><span data-stu-id="e28d5-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="e28d5-341">Hier kunt</span><span class="sxs-lookup"><span data-stu-id="e28d5-341">Here,</span></span>

1. <span data-ttu-id="e28d5-342">"scp-veld-beheergroep" betekent 'Aangepast veld groepering wordt geïmplementeerd door SCP'.</span><span class="sxs-lookup"><span data-stu-id="e28d5-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="e28d5-343">': tx 'of': niet-tx ' betekent dat als transactionele topologie is.</span><span class="sxs-lookup"><span data-stu-id="e28d5-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="e28d5-344">Aangezien de startIndex in tx versus niet tx topologieën verschilt moeten we deze informatie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="e28d5-345">[0,1] betekent een hashset van veld-id's, begint bij 0.</span><span class="sxs-lookup"><span data-stu-id="e28d5-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="e28d5-346">Hybride topologie</span><span class="sxs-lookup"><span data-stu-id="e28d5-346">Hybrid topology</span></span>
<span data-ttu-id="e28d5-347">De systeemeigen Storm is geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="e28d5-347">The native Storm is written in Java.</span></span> <span data-ttu-id="e28d5-348">En SCP.Net is uitgebreid om het inschakelen van onze douane schrijven C\# code voor het verwerken van hun zakelijke logica.</span><span class="sxs-lookup"><span data-stu-id="e28d5-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="e28d5-349">Maar we bieden ook ondersteuning voor hybride topologieën die bevat niet alleen C\# spouts/bolts, maar ook Java Spout/Bolts.</span><span class="sxs-lookup"><span data-stu-id="e28d5-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="e28d5-350">Java Spout/Bolt in spec bestand opgeven</span><span class="sxs-lookup"><span data-stu-id="e28d5-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="e28d5-351">In spec bestand 'scp-spout' en 'scp-bolt' kunnen ook worden gebruikt om Java Spouts en Bolts te geven, Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e28d5-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="e28d5-352">Hier `microsoft.scp.example.HybridTopology.Generator` is de naam van de Spout van Java-klasse.</span><span class="sxs-lookup"><span data-stu-id="e28d5-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="e28d5-353">Java-klassenpad in runSpec opdracht opgeven</span><span class="sxs-lookup"><span data-stu-id="e28d5-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="e28d5-354">Als u verzenden met Java Spouts of Bolts topologie wilt, moet u eerst de Java Spouts of Bolts compileren en ophalen van de Jar-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e28d5-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="e28d5-355">Vervolgens moet u de java-klassenpad met de Jar-bestanden bij het indienen van de topologie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="e28d5-356">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e28d5-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="e28d5-357">Hier **voorbeelden\\HybridTopology\\java\\doel\\**  is de map waarin de Java-Spout/Bolt Jar-bestand.</span><span class="sxs-lookup"><span data-stu-id="e28d5-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="e28d5-358">Serialisatie en deserialisatie tussen Java en C\\</span><span class="sxs-lookup"><span data-stu-id="e28d5-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="e28d5-359">Onze SCP-component bevat Java kant- en C\# aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="e28d5-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="e28d5-360">Om te communiceren met systeemeigen Java Spouts/Bolts, serialisatie/deserialisatie moet worden uitgevoerd tussen Java kant- en C\# zijde, zoals geïllustreerd in de volgende grafiek.</span><span class="sxs-lookup"><span data-stu-id="e28d5-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![diagram van java-component verzenden naar SCP onderdeel verzenden naar Java-onderdeel](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="e28d5-362">**Serialisatie in Java kant- en deserialisatie in C\# aan clientzijde**</span><span class="sxs-lookup"><span data-stu-id="e28d5-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="e28d5-363">Eerst bieden we standaardimplementatie voor aan de kant van Java-serialisatie en deserialisatie in C\# aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="e28d5-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="e28d5-364">De serialisatiemethode in Java aan clientzijde kan worden opgegeven in SPEC bestand:</span><span class="sxs-lookup"><span data-stu-id="e28d5-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="e28d5-365">De methode deserialisatie in C\# kant moet worden opgegeven in de C\# gebruikerscode:</span><span class="sxs-lookup"><span data-stu-id="e28d5-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="e28d5-366">Deze standaardimplementatie kunnen de meeste gevallen moet verwerken als het gegevenstype niet te complex.</span><span class="sxs-lookup"><span data-stu-id="e28d5-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="e28d5-367">Voor bepaalde gevallen, omdat het gegevenstype van de gebruiker is te complex is of omdat de prestaties van onze standaardimplementatie voldoet niet aan voor de gebruiker vereiste, gebruiker kan invoegtoepassing hun eigen implementatie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="e28d5-368">De interface serialiseren in java aan clientzijde wordt gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="e28d5-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="e28d5-369">De interface deserialize in C\# aan clientzijde is gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="e28d5-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="e28d5-370">openbare interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="e28d5-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="e28d5-371">**Serialisatie in C\# kant- en deserialisatie in Java gelijktijdige**</span><span class="sxs-lookup"><span data-stu-id="e28d5-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="e28d5-372">De serialisatiemethode in C\# kant moet worden opgegeven in de C\# gebruikerscode:</span><span class="sxs-lookup"><span data-stu-id="e28d5-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="e28d5-373">De methode deserialisatie in Java kant moet worden opgegeven in SPEC bestand:</span><span class="sxs-lookup"><span data-stu-id="e28d5-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="e28d5-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="e28d5-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="e28d5-375">Hier 'microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer' is de naam van Deserializer en 'microsoft.scp.example.HybridTopology.Person' is dat de doelklasse van de gegevens voor wordt gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e28d5-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="e28d5-376">De gebruiker kan ook invoegtoepassing hun eigen implementatie van C\# serialisatiefunctie en Java Deserializer.</span><span class="sxs-lookup"><span data-stu-id="e28d5-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="e28d5-377">Dit is de interface voor C\# serialisatiefunctie:</span><span class="sxs-lookup"><span data-stu-id="e28d5-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="e28d5-378">Dit is de interface voor Java Deserializer:</span><span class="sxs-lookup"><span data-stu-id="e28d5-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="e28d5-379">SCP Host modus</span><span class="sxs-lookup"><span data-stu-id="e28d5-379">SCP Host Mode</span></span>
<span data-ttu-id="e28d5-380">In deze modus kan gebruiker hun codes naar dll-bestand te compileren en geleverd door een SCP SCPHost.exe gebruikt voor het verzenden van topologie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="e28d5-381">Het spec bestand ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="e28d5-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="e28d5-382">Hier `plugin.name` is opgegeven als `SCPHost.exe` geleverd door een SCP-SDK.</span><span class="sxs-lookup"><span data-stu-id="e28d5-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="e28d5-383">SCPHost.exe die precies drie parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="e28d5-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="e28d5-384">De eerste is de DLL-naam, die is `"HelloWorld.dll"` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="e28d5-385">Het tweede is de klassenaam, die is `"Scp.App.HelloWorld.Generator"` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="e28d5-386">Het derde is de naam van een openbare statische methode, waarbij kan worden aangeroepen om een exemplaar van ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="e28d5-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="e28d5-387">In de modus host gebruikerscode is gecompileerd als dll-bestand en wordt aangeroepen door het SCP-platform.</span><span class="sxs-lookup"><span data-stu-id="e28d5-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="e28d5-388">SCP-platform kan dus volledig beheer over de hele verwerking logica krijgen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="e28d5-389">We raden u dus aan onze klanten verzenden topologie in de modus voor SCP-host, omdat deze kunt de ervaring voor de ontwikkeling vereenvoudigen en bring ons meer flexibiliteit en betere achterwaartse compatibiliteit voor latere release ook.</span><span class="sxs-lookup"><span data-stu-id="e28d5-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="e28d5-390">SCP programmering voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e28d5-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="e28d5-391">Hallo wereld</span><span class="sxs-lookup"><span data-stu-id="e28d5-391">HelloWorld</span></span>
<span data-ttu-id="e28d5-392">**HelloWorld** is een zeer eenvoudige voorbeeld om een smaak van SCP.Net weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e28d5-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="e28d5-393">Wordt een niet-transactionele-topologie met een spout aangeroepen **generator**, en twee bolts aangeroepen **splitser** en **teller**.</span><span class="sxs-lookup"><span data-stu-id="e28d5-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="e28d5-394">De spout **generator** wordt willekeurig enkele zinnen gegenereerd en verzenden van deze zinnen naar **splitser**.</span><span class="sxs-lookup"><span data-stu-id="e28d5-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="e28d5-395">De bolt **splitser** wordt gesplitst zinnen woorden en deze woorden om naar te verzenden **teller** bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="e28d5-396">De bout 'teller' maakt gebruik van een woordenboek voor het vastleggen van het nummer van het exemplaar van elk woord.</span><span class="sxs-lookup"><span data-stu-id="e28d5-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="e28d5-397">Er zijn twee bestanden spec **HelloWorld.spec** en **HelloWorld\_EnableAck.spec** voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e28d5-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="e28d5-398">In de C\# code, het vindt of ack is ingeschakeld door de pluginConf van Java-kant.</span><span class="sxs-lookup"><span data-stu-id="e28d5-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="e28d5-399">Als ack is ingeschakeld, wordt een woordenlijst in de spout gebruikt in de cache van de tuples die niet bevestigd zijn.</span><span class="sxs-lookup"><span data-stu-id="e28d5-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="e28d5-400">Als Fail() wordt aangeroepen, wordt er de mislukte tuple replay:</span><span class="sxs-lookup"><span data-stu-id="e28d5-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="e28d5-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="e28d5-401">HelloWorldTx</span></span>
<span data-ttu-id="e28d5-402">De **HelloWorldTx** voorbeeld laat zien hoe transactionele topologie implementeren.</span><span class="sxs-lookup"><span data-stu-id="e28d5-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="e28d5-403">Er één spout aangeroepen **generator**, een batch bolts aangeroepen **gedeeltelijk aantal**, en een bolt doorvoeren aangeroepen **aantal som**.</span><span class="sxs-lookup"><span data-stu-id="e28d5-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="e28d5-404">Er zijn ook drie vooraf gemaakte txt-bestanden: **DataSource0.txt**, **DataSource1.txt** en **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="e28d5-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="e28d5-405">In elke transactie, de spout **generator** wordt willekeurig twee bestanden kiezen uit de vooraf gemaakte drie bestanden en verzenden van de namen van de twee bestanden naar de **gedeeltelijk aantal** bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="e28d5-406">De bolt **gedeeltelijk aantal** wordt eerst de naam van het ophalen van de ontvangen tuple vervolgens opent u het bestand en tel het aantal woorden in dit bestand en ten slotte verzenden het woord dat de **aantal som** bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="e28d5-407">De **aantal som** bolt overzicht van het totale aantal.</span><span class="sxs-lookup"><span data-stu-id="e28d5-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="e28d5-408">Als u de **exact één keer** semantiek, de commit-bolt **aantal som** moet te beoordelen of het is een herhaald transactie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="e28d5-409">In dit voorbeeld heeft een statisch lidvariabele:</span><span class="sxs-lookup"><span data-stu-id="e28d5-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="e28d5-410">Wanneer een ISCPBatchBolt-exemplaar is gemaakt, krijgt deze de `txAttempt` van invoerparameters:</span><span class="sxs-lookup"><span data-stu-id="e28d5-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="e28d5-411">Wanneer `FinishBatch()` wordt aangeroepen, de `lastCommittedTxId` update zijn als het is niet een herhaald transactie.</span><span class="sxs-lookup"><span data-stu-id="e28d5-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="e28d5-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="e28d5-412">HybridTopology</span></span>
<span data-ttu-id="e28d5-413">Deze topologie bevat een Java-Spout en een C\# Bolt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="e28d5-414">De serialisatie en deserialisatie standaardimplementatie geleverd door een SCP platform wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e28d5-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="e28d5-415">Voer de ref de **HybridTopology.spec** in **voorbeelden\\HybridTopology** map voor de spec bestandsgegevens en **SubmitTopology.bat** voor opgeven Java-klassenpad.</span><span class="sxs-lookup"><span data-stu-id="e28d5-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="e28d5-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="e28d5-416">SCPHostDemo</span></span>
<span data-ttu-id="e28d5-417">In dit voorbeeld is hetzelfde als HelloWorld in wezen.</span><span class="sxs-lookup"><span data-stu-id="e28d5-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="e28d5-418">Het enige verschil is dat de gebruikerscode wordt gecompileerd als dll-bestand en de topologie wordt ingediend via SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="e28d5-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="e28d5-419">Maak ref de sectie 'SCP Host modus' voor meer gedetailleerde uitleg.</span><span class="sxs-lookup"><span data-stu-id="e28d5-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e28d5-420">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e28d5-420">Next Steps</span></span>
<span data-ttu-id="e28d5-421">Zie de volgende onderwerpen voor voorbeelden van Storm-topologieën die zijn gemaakt met behulp van de SCP's:</span><span class="sxs-lookup"><span data-stu-id="e28d5-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="e28d5-422">C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e28d5-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="e28d5-423">Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="e28d5-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="e28d5-424">Maken van meerdere gegevensstromen in een C# Storm-topologie</span><span class="sxs-lookup"><span data-stu-id="e28d5-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="e28d5-425">Power Bi gebruiken om gegevens van een Storm-topologie te visualiseren</span><span class="sxs-lookup"><span data-stu-id="e28d5-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="e28d5-426">Verwerken van sensorgegevens vehicle van Event Hubs met behulp van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="e28d5-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="e28d5-427">Uitpakken, transformeren en laden (ETL) uit Azure Event Hubs voor HBase</span><span class="sxs-lookup"><span data-stu-id="e28d5-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="e28d5-428">Gebeurtenissen met Storm en HBase op HDInsight correleren</span><span class="sxs-lookup"><span data-stu-id="e28d5-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

