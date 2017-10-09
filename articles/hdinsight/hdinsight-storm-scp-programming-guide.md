---
title: Programmeerhandleiding voor aaaSCP.NET | Microsoft Docs
description: "Meer informatie over hoe toouse SCP.NET toocreate. Storm-topologieën op basis van NET voor gebruik met Storm op HDInsight."
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
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="98beb-103">Programmeerhandleiding voor SCP</span><span class="sxs-lookup"><span data-stu-id="98beb-103">SCP programming guide</span></span>
<span data-ttu-id="98beb-104">SCP is een platform toobuild realtime, betrouwbare, consistente en hoge prestaties gegevensverwerking toepassing.</span><span class="sxs-lookup"><span data-stu-id="98beb-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="98beb-105">Het is gebouwd boven [Apache Storm](http://storm.incubator.apache.org/) --een stroom verwerken door Hallo OSS-community's-systeem.</span><span class="sxs-lookup"><span data-stu-id="98beb-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="98beb-106">Storm is ontworpen voor door Nathan Marz en open source door Twitter.</span><span class="sxs-lookup"><span data-stu-id="98beb-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="98beb-107">Hierbij wordt gebruikgemaakt van [Apache ZooKeeper](http://zookeeper.apache.org/), een andere Apache project tooenable uiterst betrouwbare gedistribueerde coördinatie en statusbeheer.</span><span class="sxs-lookup"><span data-stu-id="98beb-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="98beb-108">Niet alleen Hallo SCP project overgebracht Storm op Windows maar ook Hallo project uitbreidingen en de aanpassing voor de Windows-ecosysteem Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="98beb-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="98beb-109">Hallo-uitbreidingen bevatten functionaliteit voor .NET-ontwikkelaars en bibliotheken, Hallo aanpassing omvat implementatie op basis van Windows.</span><span class="sxs-lookup"><span data-stu-id="98beb-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="98beb-110">Hallo-uitbreiding en aanpassing wordt gedaan zodanig dat er hoeven geen toofork Hallo OSS-projecten en we kunnen gebruikmaken van afgeleide ecosystemen gebouwd op Storm.</span><span class="sxs-lookup"><span data-stu-id="98beb-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="98beb-111">Het verwerken van model</span><span class="sxs-lookup"><span data-stu-id="98beb-111">Processing model</span></span>
<span data-ttu-id="98beb-112">Hallo-gegevens in SCP is gemodelleerd als ononderbroken streams van tuples.</span><span class="sxs-lookup"><span data-stu-id="98beb-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="98beb-113">Hallo tuples doorgaans stromen in sommige wachtrij eerst en vervolgens opgenomen en getransformeerd door zakelijke logica gehost binnen een Storm-topologie, ten slotte Hallo uitvoer kan worden doorgegeven als tuples tooanother SCP systeem of worden doorgevoerd toostores gedistribueerd bestandssysteem, zoals of databases als SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98beb-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Een diagram van een wachtrij tooprocessing voor gegevens die een gegevensarchief feeds voeding](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="98beb-115">In Storm definieert u de Toepassingstopologie van een een grafiek van de berekening.</span><span class="sxs-lookup"><span data-stu-id="98beb-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="98beb-116">Elk knooppunt in een topologie bevat de logica voor verwerking en koppelingen tussen knooppunten gegevensstroom aangeven.</span><span class="sxs-lookup"><span data-stu-id="98beb-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="98beb-117">Hallo knooppunten tooinject invoergegevens in de topologie Hallo worden Spouts, wat kunnen gebruikte toosequence Hallo gegevens genoemd.</span><span class="sxs-lookup"><span data-stu-id="98beb-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="98beb-118">Hallo invoergegevens kan zich bevinden in bestand Logboeken, transactionele database, systeem-prestatiemeteritem enzovoort Hallo knooppunten met beide stromen en uitvoergegevens Bolts die Hallo actuele gegevens filteren en selecties en cumulatie-instellingen worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="98beb-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="98beb-119">SCP ondersteunt pogingen op in de minste eenmaal en precies-eenmaal verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="98beb-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="98beb-120">In een gedistribueerde toepassing voor streaming verwerken, kunnen zich voordoen diverse fouten tijdens het verwerken van gegevens, zoals netwerkuitval, machinestoringen of fout in gebruikerscode enzovoort. Op de minste eenmaal verwerken zorgt ervoor dat alle gegevens verwerkt ten minste eenmaal door automatisch Hallo dezelfde gegevens als er treedt een fout.</span><span class="sxs-lookup"><span data-stu-id="98beb-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="98beb-121">Op de minste eenmaal verwerken eenvoudig en betrouwbaar en geschikte goed in veel toepassingen.</span><span class="sxs-lookup"><span data-stu-id="98beb-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="98beb-122">Wanneer de toepassing hello exacte tellen vereist, bijvoorbeeld is op in de minste eenmaal verwerken echter onvoldoende omdat hello dezelfde gegevens kan mogelijk worden afgespeeld in Hallo Toepassingstopologie.</span><span class="sxs-lookup"><span data-stu-id="98beb-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="98beb-123">In dat geval, precies-zodra de verwerking is ontworpen toomake ervoor Hallo resultaat juist is, zelfs wanneer Hallo gegevens kan worden onderschept en meerdere keren verwerkt.</span><span class="sxs-lookup"><span data-stu-id="98beb-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="98beb-124">SCP schakelt .NET-ontwikkelaars toodevelop realtime gegevens process-toepassingen terwijl hefboomwerking Hallo Java Virtual Machine (JVM) op basis van Storm onder Hallo behandeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="98beb-125">Hallo .NET en JVM communiceert via een TCP-lokale socket.</span><span class="sxs-lookup"><span data-stu-id="98beb-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="98beb-126">Elke Spout/Bolt bestaat uit in feite een paar .net/Java-proces waarop Hallo gebruiker logica wordt uitgevoerd in .net-proces als een invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="98beb-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="98beb-127">toobuild een gegevensverwerking van toepassing op SCP verschillende stappen nodig zijn:</span><span class="sxs-lookup"><span data-stu-id="98beb-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="98beb-128">Ontwerpen en implementeren van Hallo Spouts toopull in gegevens uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="98beb-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="98beb-129">Ontwerpen en implementeren van Bolts tooprocess Hallo invoergegevens en tooexternal gegevensarchieven zoals Database opslaan.</span><span class="sxs-lookup"><span data-stu-id="98beb-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="98beb-130">Hallo-topologie ontwerpen, indienen en Hallo topologie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="98beb-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="98beb-131">Hallo topologie definieert hoekpunten en Hallo gegevens stromen tussen Hallo hoekpunten.</span><span class="sxs-lookup"><span data-stu-id="98beb-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="98beb-132">SCP wordt Hallo topologie specificatie nemen en deze implementeren op een Storm-cluster, waarin elk hoekpunt wordt uitgevoerd op één knooppunt van de logische.</span><span class="sxs-lookup"><span data-stu-id="98beb-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="98beb-133">Hallo failover en schalen zal worden afgehandeld door Hallo Storm Taakplanner.</span><span class="sxs-lookup"><span data-stu-id="98beb-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="98beb-134">Dit document maakt gebruik van enkele eenvoudige voorbeelden toowalk hoe toobuild gegevensverwerking toepassing met SCP.</span><span class="sxs-lookup"><span data-stu-id="98beb-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="98beb-135">SCP-invoegtoepassing Interface</span><span class="sxs-lookup"><span data-stu-id="98beb-135">SCP Plugin Interface</span></span>
<span data-ttu-id="98beb-136">SCP-invoegtoepassingen (of toepassingen) zijn zelfstandige exe die beide tijdens kunnen uitvoeren in Visual Studio Hallo ontwikkelingsfase bevindt, en worden aangesloten op Hallo Storm pijplijn na de implementatie in productie.</span><span class="sxs-lookup"><span data-stu-id="98beb-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="98beb-137">Schrijven Hallo SCP-invoegtoepassing wordt nog net Hallo hetzelfde als het schrijven van een andere standaard Windows-consoletoepassingen geweest.</span><span class="sxs-lookup"><span data-stu-id="98beb-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="98beb-138">SCP.NET platform declareert een interface voor spout/bolt en Hallo invoegtoepassing gebruikerscode moet deze interfaces implementeren.</span><span class="sxs-lookup"><span data-stu-id="98beb-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="98beb-139">Hallo belangrijkste doel van dit ontwerp wordt dat die gebruiker Hallo kan zich concentreren op hun eigen logics bedrijven en andere dingen toobe verwerkt door SCP.NET platform verlaten.</span><span class="sxs-lookup"><span data-stu-id="98beb-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="98beb-140">Hallo-invoegtoepassing gebruikerscode een Hallo volgende interfaces te implementeren, is afhankelijk van of Hallo topologie is transactionele of niet-transactionele, en of Hallo onderdeel spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="98beb-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="98beb-141">ISCPSpout</span></span>
* <span data-ttu-id="98beb-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="98beb-142">ISCPBolt</span></span>
* <span data-ttu-id="98beb-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="98beb-143">ISCPTxSpout</span></span>
* <span data-ttu-id="98beb-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="98beb-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="98beb-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="98beb-145">ISCPPlugin</span></span>
<span data-ttu-id="98beb-146">ISCPPlugin is hello algemene interface voor alle soorten van invoegtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="98beb-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="98beb-147">Het is momenteel een dummy-interface.</span><span class="sxs-lookup"><span data-stu-id="98beb-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="98beb-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="98beb-148">ISCPSpout</span></span>
<span data-ttu-id="98beb-149">ISCPSpout is Hallo-interface voor niet-transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="98beb-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="98beb-150">Wanneer `NextTuple()` wordt aangeroepen, Hallo C\# gebruikerscode kan een of meer tuples verzenden.</span><span class="sxs-lookup"><span data-stu-id="98beb-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="98beb-151">Als er niets tooemit, deze methode moet worden geretourneerd zonder dat alles.</span><span class="sxs-lookup"><span data-stu-id="98beb-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="98beb-152">Houd er rekening mee dat `NextTuple()`, `Ack()`, en `Fail()` worden genoemd in een lus in een enkele thread in C\# proces.</span><span class="sxs-lookup"><span data-stu-id="98beb-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="98beb-153">Wanneer er geen tooemit tuples, is het beleefd toohave NextTuple slaapstand voor een korte hoeveelheid tijd (zoals 10 milliseconden) dat niet toowaste te veel CPU.</span><span class="sxs-lookup"><span data-stu-id="98beb-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="98beb-154">`Ack()`en `Fail()` alleen wanneer het ack-mechanisme is ingeschakeld in spec bestand moet worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="98beb-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="98beb-155">Hallo `seqId` gebruikte tooidentify Hallo tuple die bevestigd of mislukt is.</span><span class="sxs-lookup"><span data-stu-id="98beb-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="98beb-156">Dus als ack in niet-transactionele topologie is ingeschakeld, kan Hallo volgen emit functie moet worden gebruikt in Spout:</span><span class="sxs-lookup"><span data-stu-id="98beb-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="98beb-157">Als ack wordt niet ondersteund in niet-transactionele topologie, Hallo `Ack()` en `Fail()` kan blijven als lege functie.</span><span class="sxs-lookup"><span data-stu-id="98beb-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="98beb-158">Hallo `parms` invoerparameters in deze functies zijn alleen lege woordenlijst, zijn gereserveerd voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="98beb-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="98beb-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="98beb-159">ISCPBolt</span></span>
<span data-ttu-id="98beb-160">ISCPBolt is Hallo-interface voor niet-transactionele bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="98beb-161">Wanneer nieuwe tuple beschikbaar is, Hallo `Execute()` functie tooprocess worden aangeroepen wordt.</span><span class="sxs-lookup"><span data-stu-id="98beb-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="98beb-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="98beb-162">ISCPTxSpout</span></span>
<span data-ttu-id="98beb-163">ISCPTxSpout is Hallo-interface voor transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="98beb-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="98beb-164">Net als bij hun niet-transactionele tegenpost `NextTx()`, `Ack()`, en `Fail()` worden genoemd in een lus in een enkele thread in C\# proces.</span><span class="sxs-lookup"><span data-stu-id="98beb-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="98beb-165">Wanneer er geen gegevens tooemit zijn, is het beleefd toohave `NextTx` slaapstand gedurende een korte tijd (10 milliseconden) dat niet toowaste te veel CPU.</span><span class="sxs-lookup"><span data-stu-id="98beb-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="98beb-166">`NextTx()`wordt genoemd, een nieuwe transactie toostart hello parameter `seqId` gebruikte tooidentify Hallo transactie, wordt ook gebruikt in `Ack()` en `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="98beb-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="98beb-167">In `NextTx()`, gebruiker gegevens tooJava kant kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="98beb-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="98beb-168">Hallo-gegevens worden opgeslagen in ZooKeeper toosupport opnieuw afspelen.</span><span class="sxs-lookup"><span data-stu-id="98beb-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="98beb-169">Omdat het Hallo-capaciteit van ZooKeeper is zeer beperkt, moet gebruikers alleen metagegevens, niet bulksgewijs gegevens in een transactionele spout verzenden.</span><span class="sxs-lookup"><span data-stu-id="98beb-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="98beb-170">Storm een transactie automatisch wordt herhaald als het mislukt, dus `Fail()` mag niet worden aangeroepen in normale geval.</span><span class="sxs-lookup"><span data-stu-id="98beb-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="98beb-171">Maar als een SCP kunt Hallo metagegevens die door transactionele spout controleren, kan worden aangeroepen `Fail()` wanneer Hallo metagegevens is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="98beb-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="98beb-172">Hallo `parms` invoerparameters in deze functies zijn alleen lege woordenlijst, zijn gereserveerd voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="98beb-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="98beb-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="98beb-173">ISCPBatchBolt</span></span>
<span data-ttu-id="98beb-174">ISCPBatchBolt is Hallo-interface voor transactionele bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="98beb-175">`Execute()`wordt aangeroepen wanneer er nieuwe tuple dat binnenkomt bij Hallo bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="98beb-176">`FinishBatch()`wordt aangeroepen wanneer deze transactie is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="98beb-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="98beb-177">Hallo `parms` invoerparameter is gereserveerd voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="98beb-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="98beb-178">Voor transactionele topologie is een belangrijke concepten – `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="98beb-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="98beb-179">Deze twee velden heeft `TxId` en `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="98beb-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="98beb-180">`TxId`gebruikte tooidentify is een specifieke transactie en voor een gegeven transactie, kunnen er meerdere poging als Hallo transactie mislukt en wordt opnieuw en nu afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="98beb-181">SCP.NET nieuwe wordt een andere ISCPBatchBolt object tooprocess elke `StormTxAttempt`, net zoals wat Storm moet aan de kant van Java.</span><span class="sxs-lookup"><span data-stu-id="98beb-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="98beb-182">Hallo-doel van dit ontwerp is toosupport parallelle transacties verwerkt.</span><span class="sxs-lookup"><span data-stu-id="98beb-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="98beb-183">Gebruiker moet Houd er rekening mee dat als poging van de transactie is voltooid, wordt het bijbehorende ISCPBatchBolt object Hallo vernietigd en garbage collector zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="98beb-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="98beb-184">Objectmodel</span><span class="sxs-lookup"><span data-stu-id="98beb-184">Object Model</span></span>
<span data-ttu-id="98beb-185">SCP.NET bevat ook een eenvoudige reeks key objecten voor ontwikkelaars tooprogram met.</span><span class="sxs-lookup"><span data-stu-id="98beb-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="98beb-186">Ze zijn **Context**, **StateStore**, en **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="98beb-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="98beb-187">Ze worden in Hallo rest deel uitmaken van deze sectie worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="98beb-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="98beb-188">Context</span><span class="sxs-lookup"><span data-stu-id="98beb-188">Context</span></span>
<span data-ttu-id="98beb-189">Context biedt een actieve omgeving toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="98beb-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="98beb-190">Elk exemplaar ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) heeft een corresponderende contextexemplaar.</span><span class="sxs-lookup"><span data-stu-id="98beb-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="98beb-191">Hallo functionaliteit van Context kan worden onderverdeeld in twee delen: (1) Hallo statische deel die beschikbaar is in de hele C Hallo\# verwerken, (2) Hallo dynamische deel die alleen beschikbaar voor Hallo specifieke Context-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="98beb-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="98beb-192">Statische deel</span><span class="sxs-lookup"><span data-stu-id="98beb-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="98beb-193">`Logger`is beschikbaar voor logboek-doel.</span><span class="sxs-lookup"><span data-stu-id="98beb-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="98beb-194">`pluginType`wordt gebruikt tooindicate Hallo invoegtoepassing type Hallo C\# proces.</span><span class="sxs-lookup"><span data-stu-id="98beb-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="98beb-195">Als Hallo C\# proces wordt uitgevoerd in de lokale testmodus (zonder Java), het Hallo-invoegtoepassing type is `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="98beb-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="98beb-196">`Config`wordt geleverd tooget configuratieparameters van Java-kant.</span><span class="sxs-lookup"><span data-stu-id="98beb-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="98beb-197">Hallo-parameters worden doorgegeven van Java-kant wanneer C\# invoegtoepassing is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="98beb-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="98beb-198">Hallo `Config` parameters worden onderverdeeld in twee delen: `stormConf` en `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="98beb-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="98beb-199">`stormConf`parameters zijn gedefinieerd door Storm is en `pluginConf` Hallo-parameters die zijn gedefinieerd door SCP is.</span><span class="sxs-lookup"><span data-stu-id="98beb-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="98beb-200">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="98beb-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="98beb-201">`TopologyContext`wordt geleverd tooget Hallo topologie context is het meest geschikt voor onderdelen met meerdere parallelle uitvoering is.</span><span class="sxs-lookup"><span data-stu-id="98beb-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="98beb-202">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="98beb-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="98beb-203">Dynamische deel</span><span class="sxs-lookup"><span data-stu-id="98beb-203">Dynamic Part</span></span>
<span data-ttu-id="98beb-204">Hallo volgende interfaces relevante tooa bepaalde contextexemplaar zijn.</span><span class="sxs-lookup"><span data-stu-id="98beb-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="98beb-205">Hallo contextexemplaar is gemaakt door SCP.NET platform en toohello gebruikerscode doorgegeven:</span><span class="sxs-lookup"><span data-stu-id="98beb-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="98beb-206">Voor niet-transactionele spout ack ondersteunen, krijgt u Hallo methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="98beb-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="98beb-207">Voor niet-transactionele bolt ack ondersteunen, moet deze expliciet `Ack()` of `Fail()` Hallo tuple deze ontvangen.</span><span class="sxs-lookup"><span data-stu-id="98beb-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="98beb-208">En bij het genereren van nieuwe tuple, moet deze ook Hallo ankers van nieuwe tuple Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="98beb-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="98beb-209">Hallo volgende methoden zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="98beb-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="98beb-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="98beb-210">StateStore</span></span>
<span data-ttu-id="98beb-211">`StateStore`metagegevens van services, monotone reeks genereren en wacht gratis coördinatie biedt.</span><span class="sxs-lookup"><span data-stu-id="98beb-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="98beb-212">Een hoger niveau gedistribueerde gelijktijdigheid abstracties kunnen worden gebaseerd op `StateStore`, met inbegrip van gedistribueerde vergrendelingen, gedistribueerde wachtrijen, barrières en transactieservices.</span><span class="sxs-lookup"><span data-stu-id="98beb-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="98beb-213">SCP-toepassingen kunt Hallo `State` object toopersist sommige gegevens in ZooKeeper, met name voor transactionele topologie.</span><span class="sxs-lookup"><span data-stu-id="98beb-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="98beb-214">Dit doet, als transactionele spout is vastgelopen en opnieuw start, kunt het Hallo nodig informatie van ZooKeeper ophalen en opnieuw Hallo pijplijn starten.</span><span class="sxs-lookup"><span data-stu-id="98beb-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="98beb-215">Hallo `StateStore` object hoofdzakelijk heeft deze twee methoden:</span><span class="sxs-lookup"><span data-stu-id="98beb-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
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
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="98beb-216">Hallo `State` object hoofdzakelijk heeft deze twee methoden:</span><span class="sxs-lookup"><span data-stu-id="98beb-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="98beb-217">Voor Hallo `Commit()` wanneer u de methode simpleMode tootrue is ingesteld, zullen gewoon worden verwijderd Hallo ZNode in ZooKeeper overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="98beb-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="98beb-218">Anders wordt verwijderd Hallo huidige ZNode en het toevoegen van een nieuw knooppunt in Hallo DOORGEVOERD\_pad.</span><span class="sxs-lookup"><span data-stu-id="98beb-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="98beb-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="98beb-219">SCPRuntime</span></span>
<span data-ttu-id="98beb-220">SCPRuntime biedt de volgende twee methoden Hallo.</span><span class="sxs-lookup"><span data-stu-id="98beb-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="98beb-221">`Initialize()`gebruikte tooinitialize Hallo SCP runtime-omgeving is.</span><span class="sxs-lookup"><span data-stu-id="98beb-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="98beb-222">Bij deze methode Hallo C\# proces maakt verbinding toohello Java kant en de configuratieparameters opgehaald en topologie-context.</span><span class="sxs-lookup"><span data-stu-id="98beb-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="98beb-223">`LaunchPlugin()`gebruikte tookick uit het Hallo-bericht lus verwerkt.</span><span class="sxs-lookup"><span data-stu-id="98beb-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="98beb-224">In deze lus Hallo C\# invoegtoepassing ontvangt berichten formulier Java kant (inclusief signalen tuples en control) en geeft u proces Hallo-berichten, mogelijk aanroepen Hallo interfacemethode door gebruikerscode Hallo.</span><span class="sxs-lookup"><span data-stu-id="98beb-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="98beb-225">Hallo invoerparameter voor methode `LaunchPlugin()` is een gemachtigde die kan resulteren in een object dat ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt-interface implementeren.</span><span class="sxs-lookup"><span data-stu-id="98beb-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="98beb-226">Voor ISCPBatchBolt, krijgen we `StormTxAttempt` van `parms`, en deze toojudge gebruiken of het is een poging tot herhaald.</span><span class="sxs-lookup"><span data-stu-id="98beb-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="98beb-227">Dit gebeurt gewoonlijk op Hallo doorvoeren bolt en dit wordt geïllustreerd in Hallo `HelloWorldTx` voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="98beb-228">Normaal gesproken Hallo SCP plugins uitgevoerd in hier twee modi:</span><span class="sxs-lookup"><span data-stu-id="98beb-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="98beb-229">Lokale testmodus: In deze modus Hallo SCP-invoegtoepassingen (Hallo C\# gebruikerscode) in Visual Studio wordt uitgevoerd tijdens de Hallo ontwikkelingsfase bevindt.</span><span class="sxs-lookup"><span data-stu-id="98beb-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="98beb-230">`LocalContext`kan worden gebruikt in deze modus, die biedt methode tooserialize Hallo verzonden tuples toolocal bestanden en lees deze toomemory terug te zetten.</span><span class="sxs-lookup"><span data-stu-id="98beb-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="98beb-231">Normale modus: In deze modus Hallo SCP plugins worden gestart door storm java-proces.</span><span class="sxs-lookup"><span data-stu-id="98beb-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="98beb-232">Hier volgt een voorbeeld van het SCP-invoegtoepassing te starten:</span><span class="sxs-lookup"><span data-stu-id="98beb-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="98beb-233">Topologie specificatietaal</span><span class="sxs-lookup"><span data-stu-id="98beb-233">Topology Specification Language</span></span>
<span data-ttu-id="98beb-234">SCP-topologie-specificatie is een specifieke taal domein voor het beschrijven en topologieën SCP te configureren.</span><span class="sxs-lookup"><span data-stu-id="98beb-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="98beb-235">Deze is gebaseerd op de Storm Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) en SCP is verlengd.</span><span class="sxs-lookup"><span data-stu-id="98beb-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="98beb-236">Topologie specificaties kunnen worden verzonden, direct toostorm voor de uitvoering van het cluster via Hallo ***runspec*** opdracht.</span><span class="sxs-lookup"><span data-stu-id="98beb-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="98beb-237">SCP.NET heeft toevoegen Volg functies toodefine Hallo transactionele topologie:</span><span class="sxs-lookup"><span data-stu-id="98beb-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="98beb-238">**Nieuwe functies**</span><span class="sxs-lookup"><span data-stu-id="98beb-238">**New Functions**</span></span> | <span data-ttu-id="98beb-239">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="98beb-239">**Parameters**</span></span> | <span data-ttu-id="98beb-240">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="98beb-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98beb-241">**TX topolopy**</span><span class="sxs-lookup"><span data-stu-id="98beb-241">**tx-topolopy**</span></span> |<span data-ttu-id="98beb-242">topologie-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-242">topology-name</span></span><br /><span data-ttu-id="98beb-243">spout-kaart</span><span class="sxs-lookup"><span data-stu-id="98beb-243">spout-map</span></span><br /><span data-ttu-id="98beb-244">bolt-kaart</span><span class="sxs-lookup"><span data-stu-id="98beb-244">bolt-map</span></span> |<span data-ttu-id="98beb-245">Definieer een transactionele-topologie met de naam van de topologie hello, &nbsp;spouts definitie kaart en Hallo bolts definitie-kaart</span><span class="sxs-lookup"><span data-stu-id="98beb-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="98beb-246">**SCP-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="98beb-246">**scp-tx-spout**</span></span> |<span data-ttu-id="98beb-247">exec-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-247">exec-name</span></span><br /><span data-ttu-id="98beb-248">argumenten</span><span class="sxs-lookup"><span data-stu-id="98beb-248">args</span></span><br /><span data-ttu-id="98beb-249">Velden</span><span class="sxs-lookup"><span data-stu-id="98beb-249">fields</span></span> |<span data-ttu-id="98beb-250">Definieer een transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="98beb-250">Define a transactional spout.</span></span> <span data-ttu-id="98beb-251">Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.</span><span class="sxs-lookup"><span data-stu-id="98beb-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="98beb-252">Hallo ***velden*** Hallo uitvoervelden voor spout is</span><span class="sxs-lookup"><span data-stu-id="98beb-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="98beb-253">**SCP-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="98beb-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="98beb-254">exec-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-254">exec-name</span></span><br /><span data-ttu-id="98beb-255">argumenten</span><span class="sxs-lookup"><span data-stu-id="98beb-255">args</span></span><br /><span data-ttu-id="98beb-256">Velden</span><span class="sxs-lookup"><span data-stu-id="98beb-256">fields</span></span> |<span data-ttu-id="98beb-257">Definieer een transactionele Batch Bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="98beb-258">Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten.***</span><span class="sxs-lookup"><span data-stu-id="98beb-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="98beb-259">Hallo is velden Hallo velden uitvoeren voor bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="98beb-260">**SCP-tx-doorvoeren-bolt**</span><span class="sxs-lookup"><span data-stu-id="98beb-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="98beb-261">exec-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-261">exec-name</span></span><br /><span data-ttu-id="98beb-262">argumenten</span><span class="sxs-lookup"><span data-stu-id="98beb-262">args</span></span><br /><span data-ttu-id="98beb-263">Velden</span><span class="sxs-lookup"><span data-stu-id="98beb-263">fields</span></span> |<span data-ttu-id="98beb-264">Definieer een transactionele Committer Bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="98beb-265">Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.</span><span class="sxs-lookup"><span data-stu-id="98beb-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="98beb-266">Hallo ***velden*** Hallo uitvoervelden voor bolt is</span><span class="sxs-lookup"><span data-stu-id="98beb-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="98beb-267">**nontx topolopy**</span><span class="sxs-lookup"><span data-stu-id="98beb-267">**nontx-topolopy**</span></span> |<span data-ttu-id="98beb-268">topologie-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-268">topology-name</span></span><br /><span data-ttu-id="98beb-269">spout-kaart</span><span class="sxs-lookup"><span data-stu-id="98beb-269">spout-map</span></span><br /><span data-ttu-id="98beb-270">bolt-kaart</span><span class="sxs-lookup"><span data-stu-id="98beb-270">bolt-map</span></span> |<span data-ttu-id="98beb-271">Definieer een niet-transactionele-topologie met de naam van de topologie hello,&nbsp; spouts definitie kaart en Hallo bolts definitie-kaart</span><span class="sxs-lookup"><span data-stu-id="98beb-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="98beb-272">**SCP spout**</span><span class="sxs-lookup"><span data-stu-id="98beb-272">**scp-spout**</span></span> |<span data-ttu-id="98beb-273">exec-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-273">exec-name</span></span><br /><span data-ttu-id="98beb-274">argumenten</span><span class="sxs-lookup"><span data-stu-id="98beb-274">args</span></span><br /><span data-ttu-id="98beb-275">Velden</span><span class="sxs-lookup"><span data-stu-id="98beb-275">fields</span></span><br /><span data-ttu-id="98beb-276">parameters</span><span class="sxs-lookup"><span data-stu-id="98beb-276">parameters</span></span> |<span data-ttu-id="98beb-277">Definieer een niet-transactionele spout.</span><span class="sxs-lookup"><span data-stu-id="98beb-277">Define a nontransactional spout.</span></span> <span data-ttu-id="98beb-278">Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.</span><span class="sxs-lookup"><span data-stu-id="98beb-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="98beb-279">Hallo ***velden*** Hallo uitvoervelden voor spout is</span><span class="sxs-lookup"><span data-stu-id="98beb-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="98beb-280">Hallo ***parameters*** is optioneel, met behulp van deze toospecify sommige parameters zoals 'nontransactional.ack.enabled'.</span><span class="sxs-lookup"><span data-stu-id="98beb-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="98beb-281">**SCP-bolt**</span><span class="sxs-lookup"><span data-stu-id="98beb-281">**scp-bolt**</span></span> |<span data-ttu-id="98beb-282">exec-naam</span><span class="sxs-lookup"><span data-stu-id="98beb-282">exec-name</span></span><br /><span data-ttu-id="98beb-283">argumenten</span><span class="sxs-lookup"><span data-stu-id="98beb-283">args</span></span><br /><span data-ttu-id="98beb-284">Velden</span><span class="sxs-lookup"><span data-stu-id="98beb-284">fields</span></span><br /><span data-ttu-id="98beb-285">parameters</span><span class="sxs-lookup"><span data-stu-id="98beb-285">parameters</span></span> |<span data-ttu-id="98beb-286">Definieer een niet-transactionele Bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="98beb-287">Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.</span><span class="sxs-lookup"><span data-stu-id="98beb-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="98beb-288">Hallo ***velden*** Hallo uitvoervelden voor bolt is</span><span class="sxs-lookup"><span data-stu-id="98beb-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="98beb-289">Hallo ***parameters*** is optioneel, met behulp van deze toospecify sommige parameters zoals 'nontransactional.ack.enabled'.</span><span class="sxs-lookup"><span data-stu-id="98beb-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="98beb-290">SCP.NET heeft de volgende codes woorden gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="98beb-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="98beb-291">**Trefwoorden**</span><span class="sxs-lookup"><span data-stu-id="98beb-291">**Key Words**</span></span> | <span data-ttu-id="98beb-292">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="98beb-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="98beb-293">**: de naam**</span><span class="sxs-lookup"><span data-stu-id="98beb-293">**:name**</span></span> |<span data-ttu-id="98beb-294">Hallo-topologie naam definiëren</span><span class="sxs-lookup"><span data-stu-id="98beb-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="98beb-295">**: topologie**</span><span class="sxs-lookup"><span data-stu-id="98beb-295">**:topology**</span></span> |<span data-ttu-id="98beb-296">Definieer Hallo topologie met behulp van Hallo hierboven functies en bouwen in toepassingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="98beb-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="98beb-297">**: p**</span><span class="sxs-lookup"><span data-stu-id="98beb-297">**:p**</span></span> |<span data-ttu-id="98beb-298">Hallo parallelle uitvoering hint op voor elke spout of bolt definiëren.</span><span class="sxs-lookup"><span data-stu-id="98beb-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="98beb-299">**: config**</span><span class="sxs-lookup"><span data-stu-id="98beb-299">**:config**</span></span> |<span data-ttu-id="98beb-300">Definieer parameter configureren of update Hallo bestaande</span><span class="sxs-lookup"><span data-stu-id="98beb-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="98beb-301">**: schema**</span><span class="sxs-lookup"><span data-stu-id="98beb-301">**:schema**</span></span> |<span data-ttu-id="98beb-302">Hallo-Schema van stroom definiëren.</span><span class="sxs-lookup"><span data-stu-id="98beb-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="98beb-303">En veelgebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="98beb-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="98beb-304">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="98beb-304">**Parameter**</span></span> | <span data-ttu-id="98beb-305">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="98beb-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="98beb-306">**'plugin.name'**</span><span class="sxs-lookup"><span data-stu-id="98beb-306">**"plugin.name"**</span></span> |<span data-ttu-id="98beb-307">naam van de exe-bestand van Hallo C#-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="98beb-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="98beb-308">**'plugin.args'**</span><span class="sxs-lookup"><span data-stu-id="98beb-308">**"plugin.args"**</span></span> |<span data-ttu-id="98beb-309">invoegtoepassing argumenten</span><span class="sxs-lookup"><span data-stu-id="98beb-309">plugin args</span></span> |
| <span data-ttu-id="98beb-310">**'output.schema'**</span><span class="sxs-lookup"><span data-stu-id="98beb-310">**"output.schema"**</span></span> |<span data-ttu-id="98beb-311">Uitvoerschema</span><span class="sxs-lookup"><span data-stu-id="98beb-311">Output schema</span></span> |
| <span data-ttu-id="98beb-312">**'nontransactional.ack.enabled'**</span><span class="sxs-lookup"><span data-stu-id="98beb-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="98beb-313">Hiermee wordt aangegeven of ack is ingeschakeld voor niet-transactionele-topologie</span><span class="sxs-lookup"><span data-stu-id="98beb-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="98beb-314">Hallo runspec opdracht samen met de Hallo bits wordt geïmplementeerd, lijkt op het Hallo-gebruik:</span><span class="sxs-lookup"><span data-stu-id="98beb-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="98beb-315">Hallo ***resource dir*** parameter is optioneel, moet u toospecify wanneer u wilt dat een C tooplug\# toepassings- en deze map bevat toepassing hello, Hallo afhankelijkheden en configuraties.</span><span class="sxs-lookup"><span data-stu-id="98beb-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="98beb-316">Hallo ***classpath*** parameter ook is optioneel.</span><span class="sxs-lookup"><span data-stu-id="98beb-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="98beb-317">Het is gebruikte toospecify Hallo Java classpath als spec Hallo-bestand Java Spout of Bolt bevat.</span><span class="sxs-lookup"><span data-stu-id="98beb-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="98beb-318">Diverse functies</span><span class="sxs-lookup"><span data-stu-id="98beb-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="98beb-319">Invoer en uitvoer Schemadeclaratie</span><span class="sxs-lookup"><span data-stu-id="98beb-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="98beb-320">Hallo-gebruiker kunt verzenden tuple in C\# verwerken, hello platform moet tooserialize Hallo tuple in byte [] overdracht tooJava kant en Storm draagt deze tuple toohello doelen.</span><span class="sxs-lookup"><span data-stu-id="98beb-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="98beb-321">Ondertussen in downstream onderdeel Hallo C\# proces wordt tuple terug van java-kant ontvangt en de oorspronkelijke typen toohello per platform converteren, alle deze bewerkingen zijn verborgen door Hallo Platform.</span><span class="sxs-lookup"><span data-stu-id="98beb-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="98beb-322">toosupport hello serialisatie en deserialisatie, moet gebruikerscode toodeclare Hallo schema Hallo en uitgangen.</span><span class="sxs-lookup"><span data-stu-id="98beb-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="98beb-323">Hallo i/o-stroom schema Hallo-sleutel is gedefinieerd als een woordenboek, Hallo StreamId en Hallo waarde Hallo typen Hallo kolommen.</span><span class="sxs-lookup"><span data-stu-id="98beb-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="98beb-324">Hallo-component kan meerdere streams gedeclareerd hebben.</span><span class="sxs-lookup"><span data-stu-id="98beb-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="98beb-325">In de Context-object hebben we Hallo volgende API toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="98beb-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="98beb-326">Gebruikerscode moet ervoor zorgen Hallo tuples verzonden hello schema gedefinieerd voor deze stroom te volgen of Hallo system genereert een runtime-fout.</span><span class="sxs-lookup"><span data-stu-id="98beb-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="98beb-327">Ondersteuning voor meerdere Stream</span><span class="sxs-lookup"><span data-stu-id="98beb-327">Multi-Stream Support</span></span>
<span data-ttu-id="98beb-328">SCP ondersteunt gebruiker tooemit code of ontvangen van meerdere afzonderlijke streams op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="98beb-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="98beb-329">Hallo ondersteuning weerspiegelt in Hallo Context-object als Hallo Emit methode een optionele stroom-ID-parameter moet.</span><span class="sxs-lookup"><span data-stu-id="98beb-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="98beb-330">Twee methoden in Hallo SCP.NET Context-object er zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="98beb-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="98beb-331">Ze zijn gebruikt tooemit Tuple of Tuples toospecify StreamId.</span><span class="sxs-lookup"><span data-stu-id="98beb-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="98beb-332">Hallo StreamId is een tekenreeks en moet u toobe consistent in beide C\# en Hallo topologie definitie-specificatie.</span><span class="sxs-lookup"><span data-stu-id="98beb-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="98beb-333">Hallo importeerbereik tooa niet-bestaande stroom zorgt ervoor dat de runtime-uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="98beb-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="98beb-334">Velden groeperen</span><span class="sxs-lookup"><span data-stu-id="98beb-334">Fields Grouping</span></span>
<span data-ttu-id="98beb-335">Hallo die ingebouwde velden groeperen in Strom niet goed in SCP.NET werkt.</span><span class="sxs-lookup"><span data-stu-id="98beb-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="98beb-336">Alle gegevenstypen van de Hallo-velden zijn daadwerkelijk byte [] op Hallo Java-Proxy aan clientzijde, en Hallo velden groeperen gebruikt Hallo byte [] object hash-code tooperform Hallo groepering.</span><span class="sxs-lookup"><span data-stu-id="98beb-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="98beb-337">Hallo byte [] object hash-code is Hallo-adres van dit object in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="98beb-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="98beb-338">Dus Hallo groepering onjuist voor twee-byte []-objecten die share Hallo dezelfde inhoud, maar niet Hallo hetzelfde adres.</span><span class="sxs-lookup"><span data-stu-id="98beb-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="98beb-339">SCP.NET een groeperingsmethode met aangepaste toegevoegd en het Hallo-inhoud van het Hallo byte [] toodo Hallo groepering gebruikt.</span><span class="sxs-lookup"><span data-stu-id="98beb-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="98beb-340">In **SPEC** bestand Hallo syntaxis is als volgt:</span><span class="sxs-lookup"><span data-stu-id="98beb-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="98beb-341">Hier kunt</span><span class="sxs-lookup"><span data-stu-id="98beb-341">Here,</span></span>

1. <span data-ttu-id="98beb-342">"scp-veld-beheergroep" betekent 'Aangepast veld groepering wordt geïmplementeerd door SCP'.</span><span class="sxs-lookup"><span data-stu-id="98beb-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="98beb-343">': tx 'of': niet-tx ' betekent dat als transactionele topologie is.</span><span class="sxs-lookup"><span data-stu-id="98beb-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="98beb-344">Aangezien Hallo vanaf index in tx versus niet tx topologieën verschilt moeten we deze informatie.</span><span class="sxs-lookup"><span data-stu-id="98beb-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="98beb-345">[0,1] betekent een hashset van veld-id's, begint bij 0.</span><span class="sxs-lookup"><span data-stu-id="98beb-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="98beb-346">Hybride topologie</span><span class="sxs-lookup"><span data-stu-id="98beb-346">Hybrid topology</span></span>
<span data-ttu-id="98beb-347">Hallo systeemeigen Storm is geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="98beb-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="98beb-348">En SCP.Net is uitgebreid deze tooenable onze douane toowrite C\# code toohandle hun zakelijke logica.</span><span class="sxs-lookup"><span data-stu-id="98beb-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="98beb-349">Maar we bieden ook ondersteuning voor hybride topologieën die bevat niet alleen C\# spouts/bolts, maar ook Java Spout/Bolts.</span><span class="sxs-lookup"><span data-stu-id="98beb-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="98beb-350">Java Spout/Bolt in spec bestand opgeven</span><span class="sxs-lookup"><span data-stu-id="98beb-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="98beb-351">In spec bestand kunnen 'scp-spout' en 'scp-bolt' ook gebruikte toospecify Java Spouts en Bolts, Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="98beb-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="98beb-352">Hier `microsoft.scp.example.HybridTopology.Generator` heet Hallo Hallo Spout Java-klasse.</span><span class="sxs-lookup"><span data-stu-id="98beb-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="98beb-353">Java-klassenpad in runSpec opdracht opgeven</span><span class="sxs-lookup"><span data-stu-id="98beb-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="98beb-354">Als u met Java Spouts of Bolts toosubmit-topologie wilt, kunt u toofirst compileren Hallo Java Spouts of Bolts nodig en Hallo Jar-bestanden ophalen.</span><span class="sxs-lookup"><span data-stu-id="98beb-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="98beb-355">Vervolgens moet u Hallo java classpath die Hallo Jar-bestanden bevat bij het indienen van de topologie.</span><span class="sxs-lookup"><span data-stu-id="98beb-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="98beb-356">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="98beb-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="98beb-357">Hier **voorbeelden\\HybridTopology\\java\\doel\\**  Hallo-map is waarin Hallo Java Spout/Bolt Jar-bestand.</span><span class="sxs-lookup"><span data-stu-id="98beb-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="98beb-358">Serialisatie en deserialisatie tussen Java en C\\</span><span class="sxs-lookup"><span data-stu-id="98beb-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="98beb-359">Onze SCP-component bevat Java kant- en C\# aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="98beb-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="98beb-360">In de volgorde toointeract met systeemeigen Java Spouts/Bolts, serialisatie/deserialisatie moet worden uitgevoerd tussen Java kant- en C\# zijde, zoals geïllustreerd in de volgende grafiek Hallo.</span><span class="sxs-lookup"><span data-stu-id="98beb-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![diagram van java-component tooSCP onderdeel tooJava onderdeel verzenden verzenden](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="98beb-362">**Serialisatie in Java kant- en deserialisatie in C\# aan clientzijde**</span><span class="sxs-lookup"><span data-stu-id="98beb-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="98beb-363">Eerst bieden we standaardimplementatie voor aan de kant van Java-serialisatie en deserialisatie in C\# aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="98beb-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="98beb-364">Hallo serialisatiemethode in Java aan clientzijde kan worden opgegeven in SPEC bestand:</span><span class="sxs-lookup"><span data-stu-id="98beb-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="98beb-365">Hallo deserialisatie-methode in C\# kant moet worden opgegeven in de C\# gebruikerscode:</span><span class="sxs-lookup"><span data-stu-id="98beb-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="98beb-366">Deze standaardimplementatie afhandelt meestal als Hallo-gegevenstype niet te complex is.</span><span class="sxs-lookup"><span data-stu-id="98beb-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="98beb-367">Voor bepaalde gevallen, ofwel omdat Hallo gebruikersgegevenstype is te complex is of omdat hello prestaties van onze standaardimplementatie voldoet niet aan de Hallo van de gebruiker vereist, gebruiker kan invoegtoepassing hun eigen implementatie.</span><span class="sxs-lookup"><span data-stu-id="98beb-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="98beb-368">Hallo serialiseren interface in java aan clientzijde is gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="98beb-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="98beb-369">Hallo deserialiseren interface in C\# aan clientzijde is gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="98beb-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="98beb-370">openbare interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="98beb-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="98beb-371">**Serialisatie in C\# kant- en deserialisatie in Java gelijktijdige**</span><span class="sxs-lookup"><span data-stu-id="98beb-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="98beb-372">Hallo serialisatiemethode in C\# kant moet worden opgegeven in de C\# gebruikerscode:</span><span class="sxs-lookup"><span data-stu-id="98beb-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="98beb-373">Hallo deserialisatie-methode in Java kant moet worden opgegeven in SPEC bestand:</span><span class="sxs-lookup"><span data-stu-id="98beb-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="98beb-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="98beb-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="98beb-375">Hier 'microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer' Hallo-naam van de Deserializer is en 'microsoft.scp.example.HybridTopology.Person' is Hallo doel klassegegevens hello wordt gedeserialiseerd aan.</span><span class="sxs-lookup"><span data-stu-id="98beb-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="98beb-376">De gebruiker kan ook invoegtoepassing hun eigen implementatie van C\# serialisatiefunctie en Java Deserializer.</span><span class="sxs-lookup"><span data-stu-id="98beb-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="98beb-377">Dit is de interface Hallo voor C\# serialisatiefunctie:</span><span class="sxs-lookup"><span data-stu-id="98beb-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="98beb-378">Dit is Hallo-interface voor Java Deserializer:</span><span class="sxs-lookup"><span data-stu-id="98beb-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="98beb-379">SCP Host modus</span><span class="sxs-lookup"><span data-stu-id="98beb-379">SCP Host Mode</span></span>
<span data-ttu-id="98beb-380">In deze modus gebruiker hun tooDLL codes worden gecompileerd, en gebruik SCPHost.exe geleverd door een SCP toosubmit topologie.</span><span class="sxs-lookup"><span data-stu-id="98beb-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="98beb-381">spec Hallo-bestand ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="98beb-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="98beb-382">Hier `plugin.name` is opgegeven als `SCPHost.exe` geleverd door een SCP-SDK.</span><span class="sxs-lookup"><span data-stu-id="98beb-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="98beb-383">SCPHost.exe die precies drie parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="98beb-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="98beb-384">Hallo eerst een is Hallo dll-naam, die `"HelloWorld.dll"` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="98beb-385">Hallo tweede is Hallo klassenaam, die is `"Scp.App.HelloWorld.Generator"` in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="98beb-386">Hallo derde een Hallo naam is van een openbare statische methode, waarbij aangeroepen tooget een exemplaar van ISCPPlugin worden kan.</span><span class="sxs-lookup"><span data-stu-id="98beb-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="98beb-387">In de modus host gebruikerscode is gecompileerd als dll-bestand en wordt aangeroepen door het SCP-platform.</span><span class="sxs-lookup"><span data-stu-id="98beb-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="98beb-388">SCP-platform kan dus volledig beheer van Hallo hele verwerking logica krijgen.</span><span class="sxs-lookup"><span data-stu-id="98beb-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="98beb-389">Daarom aangeraden voor onze klanten toosubmit topologie in SCP host modus omdat deze kunt Hallo ontwikkeling vereenvoudigen en ons meer flexibiliteit en betere compatibiliteit met eerdere versies van ook latere release zorgen.</span><span class="sxs-lookup"><span data-stu-id="98beb-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="98beb-390">SCP programmering voorbeelden</span><span class="sxs-lookup"><span data-stu-id="98beb-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="98beb-391">Hallo wereld</span><span class="sxs-lookup"><span data-stu-id="98beb-391">HelloWorld</span></span>
<span data-ttu-id="98beb-392">**HelloWorld** is een zeer eenvoudige voorbeeld tooshow een smaak van SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="98beb-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="98beb-393">Wordt een niet-transactionele-topologie met een spout aangeroepen **generator**, en twee bolts aangeroepen **splitser** en **teller**.</span><span class="sxs-lookup"><span data-stu-id="98beb-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="98beb-394">Hallo spout **generator** wordt willekeurig enkele zinnen gegenereerd en deze zinnen te verzenden**splitser**.</span><span class="sxs-lookup"><span data-stu-id="98beb-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="98beb-395">Hallo bolt **splitser** wordt gesplitst Hallo zinnen toowords en deze woorden te verzenden**teller** bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="98beb-396">teller' Hello bout' maakt gebruik van een getal woordenlijst toorecord Hallo exemplaar van elk woord.</span><span class="sxs-lookup"><span data-stu-id="98beb-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="98beb-397">Er zijn twee bestanden spec **HelloWorld.spec** en **HelloWorld\_EnableAck.spec** voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="98beb-398">In Hallo C\# code, het vindt of ack door Hallo pluginConf van Java-kant is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="98beb-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="98beb-399">Als ack is ingeschakeld, is een woordenlijst in Hallo-spout gebruikte toocache Hallo tuples die niet bevestigd zijn.</span><span class="sxs-lookup"><span data-stu-id="98beb-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="98beb-400">Als Fail() wordt aangeroepen, zal hello mislukte tuple worden cookies:</span><span class="sxs-lookup"><span data-stu-id="98beb-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="98beb-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="98beb-401">HelloWorldTx</span></span>
<span data-ttu-id="98beb-402">Hallo **HelloWorldTx** voorbeeld laat zien hoe tooimplement transactionele topologie.</span><span class="sxs-lookup"><span data-stu-id="98beb-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="98beb-403">Er één spout aangeroepen **generator**, een batch bolts aangeroepen **gedeeltelijk aantal**, en een bolt doorvoeren aangeroepen **aantal som**.</span><span class="sxs-lookup"><span data-stu-id="98beb-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="98beb-404">Er zijn ook drie vooraf gemaakte txt-bestanden: **DataSource0.txt**, **DataSource1.txt** en **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="98beb-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="98beb-405">In elke transactie Hallo spout **generator** wordt willekeurig twee bestanden kiezen uit vooraf gemaakte drie bestanden Hallo en verzenden van Hallo twee bestand namen toohello **gedeeltelijk aantal** bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="98beb-406">Hallo bolt **gedeeltelijk aantal** eerst Hallo-bestandsnaam niet ophalen uit Hallo ontvangen tuple vervolgens open Hallo bestands- en aantal Hallo aantal woorden in dit bestand en ten slotte verzenden Hallo word nummer toohello **count-som**bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="98beb-407">Hallo **aantal som** bolt overzicht van het totale aantal Hallo.</span><span class="sxs-lookup"><span data-stu-id="98beb-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="98beb-408">tooachieve **exact één keer** semantiek, Hallo doorvoeren bolt **aantal som** moet toojudge of het om een herhaald transactie.</span><span class="sxs-lookup"><span data-stu-id="98beb-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="98beb-409">In dit voorbeeld heeft een statisch lidvariabele:</span><span class="sxs-lookup"><span data-stu-id="98beb-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="98beb-410">Wanneer een ISCPBatchBolt-exemplaar is gemaakt, krijgt het Hallo `txAttempt` van invoerparameters:</span><span class="sxs-lookup"><span data-stu-id="98beb-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
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

<span data-ttu-id="98beb-411">Wanneer `FinishBatch()` wordt aangeroepen, hello `lastCommittedTxId` update zijn als het is niet een herhaald transactie.</span><span class="sxs-lookup"><span data-stu-id="98beb-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="98beb-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="98beb-412">HybridTopology</span></span>
<span data-ttu-id="98beb-413">Deze topologie bevat een Java-Spout en een C\# Bolt.</span><span class="sxs-lookup"><span data-stu-id="98beb-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="98beb-414">Hallo serialisatie en deserialisatie standaardimplementatie geleverd door een SCP platform wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="98beb-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="98beb-415">Voer ref Hallo **HybridTopology.spec** in **voorbeelden\\HybridTopology** map voor Hallo spec bestandsgegevens, en **SubmitTopology.bat** voor het Java-klassenpad toospecify.</span><span class="sxs-lookup"><span data-stu-id="98beb-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="98beb-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="98beb-416">SCPHostDemo</span></span>
<span data-ttu-id="98beb-417">In dit voorbeeld is in wezen hetzelfde als Hallo wereld Hallo.</span><span class="sxs-lookup"><span data-stu-id="98beb-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="98beb-418">Hallo alleen verschil is dat Hallo gebruikerscode wordt gecompileerd als dll-bestand en Hallo-topologie wordt ingediend via SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="98beb-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="98beb-419">Maak ref Hallo sectie 'SCP Host modus' voor meer gedetailleerde uitleg.</span><span class="sxs-lookup"><span data-stu-id="98beb-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98beb-420">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98beb-420">Next Steps</span></span>
<span data-ttu-id="98beb-421">Zie voor voorbeelden van Storm-topologieën die zijn gemaakt met behulp van SCP Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="98beb-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="98beb-422">C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98beb-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="98beb-423">Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="98beb-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="98beb-424">Maken van meerdere gegevensstromen in een C# Storm-topologie</span><span class="sxs-lookup"><span data-stu-id="98beb-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="98beb-425">Power Bi toovisualize gegevens uit een Storm-topologie gebruiken</span><span class="sxs-lookup"><span data-stu-id="98beb-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="98beb-426">Verwerken van sensorgegevens vehicle van Event Hubs met behulp van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="98beb-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="98beb-427">Uitpakken, transformeren en Load (ETL) van Azure Event Hubs tooHBase</span><span class="sxs-lookup"><span data-stu-id="98beb-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="98beb-428">Gebeurtenissen met Storm en HBase op HDInsight correleren</span><span class="sxs-lookup"><span data-stu-id="98beb-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

