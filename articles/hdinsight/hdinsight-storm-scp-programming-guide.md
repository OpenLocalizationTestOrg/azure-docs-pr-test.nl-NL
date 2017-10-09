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
# <a name="scp-programming-guide"></a>Programmeerhandleiding voor SCP
SCP is een platform toobuild realtime, betrouwbare, consistente en hoge prestaties gegevensverwerking toepassing. Het is gebouwd boven [Apache Storm](http://storm.incubator.apache.org/) --een stroom verwerken door Hallo OSS-community's-systeem. Storm is ontworpen voor door Nathan Marz en open source door Twitter. Hierbij wordt gebruikgemaakt van [Apache ZooKeeper](http://zookeeper.apache.org/), een andere Apache project tooenable uiterst betrouwbare gedistribueerde coördinatie en statusbeheer. 

Niet alleen Hallo SCP project overgebracht Storm op Windows maar ook Hallo project uitbreidingen en de aanpassing voor de Windows-ecosysteem Hallo toegevoegd. Hallo-uitbreidingen bevatten functionaliteit voor .NET-ontwikkelaars en bibliotheken, Hallo aanpassing omvat implementatie op basis van Windows. 

Hallo-uitbreiding en aanpassing wordt gedaan zodanig dat er hoeven geen toofork Hallo OSS-projecten en we kunnen gebruikmaken van afgeleide ecosystemen gebouwd op Storm.

## <a name="processing-model"></a>Het verwerken van model
Hallo-gegevens in SCP is gemodelleerd als ononderbroken streams van tuples. Hallo tuples doorgaans stromen in sommige wachtrij eerst en vervolgens opgenomen en getransformeerd door zakelijke logica gehost binnen een Storm-topologie, ten slotte Hallo uitvoer kan worden doorgegeven als tuples tooanother SCP systeem of worden doorgevoerd toostores gedistribueerd bestandssysteem, zoals of databases als SQL Server.

![Een diagram van een wachtrij tooprocessing voor gegevens die een gegevensarchief feeds voeding](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

In Storm definieert u de Toepassingstopologie van een een grafiek van de berekening. Elk knooppunt in een topologie bevat de logica voor verwerking en koppelingen tussen knooppunten gegevensstroom aangeven. Hallo knooppunten tooinject invoergegevens in de topologie Hallo worden Spouts, wat kunnen gebruikte toosequence Hallo gegevens genoemd. Hallo invoergegevens kan zich bevinden in bestand Logboeken, transactionele database, systeem-prestatiemeteritem enzovoort Hallo knooppunten met beide stromen en uitvoergegevens Bolts die Hallo actuele gegevens filteren en selecties en cumulatie-instellingen worden genoemd.

SCP ondersteunt pogingen op in de minste eenmaal en precies-eenmaal verwerken van gegevens. In een gedistribueerde toepassing voor streaming verwerken, kunnen zich voordoen diverse fouten tijdens het verwerken van gegevens, zoals netwerkuitval, machinestoringen of fout in gebruikerscode enzovoort. Op de minste eenmaal verwerken zorgt ervoor dat alle gegevens verwerkt ten minste eenmaal door automatisch Hallo dezelfde gegevens als er treedt een fout. Op de minste eenmaal verwerken eenvoudig en betrouwbaar en geschikte goed in veel toepassingen. Wanneer de toepassing hello exacte tellen vereist, bijvoorbeeld is op in de minste eenmaal verwerken echter onvoldoende omdat hello dezelfde gegevens kan mogelijk worden afgespeeld in Hallo Toepassingstopologie. In dat geval, precies-zodra de verwerking is ontworpen toomake ervoor Hallo resultaat juist is, zelfs wanneer Hallo gegevens kan worden onderschept en meerdere keren verwerkt.

SCP schakelt .NET-ontwikkelaars toodevelop realtime gegevens process-toepassingen terwijl hefboomwerking Hallo Java Virtual Machine (JVM) op basis van Storm onder Hallo behandeld. Hallo .NET en JVM communiceert via een TCP-lokale socket. Elke Spout/Bolt bestaat uit in feite een paar .net/Java-proces waarop Hallo gebruiker logica wordt uitgevoerd in .net-proces als een invoegtoepassing.

toobuild een gegevensverwerking van toepassing op SCP verschillende stappen nodig zijn:

* Ontwerpen en implementeren van Hallo Spouts toopull in gegevens uit de wachtrij.
* Ontwerpen en implementeren van Bolts tooprocess Hallo invoergegevens en tooexternal gegevensarchieven zoals Database opslaan.
* Hallo-topologie ontwerpen, indienen en Hallo topologie worden uitgevoerd. Hallo topologie definieert hoekpunten en Hallo gegevens stromen tussen Hallo hoekpunten. SCP wordt Hallo topologie specificatie nemen en deze implementeren op een Storm-cluster, waarin elk hoekpunt wordt uitgevoerd op één knooppunt van de logische. Hallo failover en schalen zal worden afgehandeld door Hallo Storm Taakplanner.

Dit document maakt gebruik van enkele eenvoudige voorbeelden toowalk hoe toobuild gegevensverwerking toepassing met SCP.

## <a name="scp-plugin-interface"></a>SCP-invoegtoepassing Interface
SCP-invoegtoepassingen (of toepassingen) zijn zelfstandige exe die beide tijdens kunnen uitvoeren in Visual Studio Hallo ontwikkelingsfase bevindt, en worden aangesloten op Hallo Storm pijplijn na de implementatie in productie. Schrijven Hallo SCP-invoegtoepassing wordt nog net Hallo hetzelfde als het schrijven van een andere standaard Windows-consoletoepassingen geweest. SCP.NET platform declareert een interface voor spout/bolt en Hallo invoegtoepassing gebruikerscode moet deze interfaces implementeren. Hallo belangrijkste doel van dit ontwerp wordt dat die gebruiker Hallo kan zich concentreren op hun eigen logics bedrijven en andere dingen toobe verwerkt door SCP.NET platform verlaten.

Hallo-invoegtoepassing gebruikerscode een Hallo volgende interfaces te implementeren, is afhankelijk van of Hallo topologie is transactionele of niet-transactionele, en of Hallo onderdeel spout of bolt.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin is hello algemene interface voor alle soorten van invoegtoepassingen. Het is momenteel een dummy-interface.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout is Hallo-interface voor niet-transactionele spout.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Wanneer `NextTuple()` wordt aangeroepen, Hallo C\# gebruikerscode kan een of meer tuples verzenden. Als er niets tooemit, deze methode moet worden geretourneerd zonder dat alles. Houd er rekening mee dat `NextTuple()`, `Ack()`, en `Fail()` worden genoemd in een lus in een enkele thread in C\# proces. Wanneer er geen tooemit tuples, is het beleefd toohave NextTuple slaapstand voor een korte hoeveelheid tijd (zoals 10 milliseconden) dat niet toowaste te veel CPU.

`Ack()`en `Fail()` alleen wanneer het ack-mechanisme is ingeschakeld in spec bestand moet worden aangeroepen. Hallo `seqId` gebruikte tooidentify Hallo tuple die bevestigd of mislukt is. Dus als ack in niet-transactionele topologie is ingeschakeld, kan Hallo volgen emit functie moet worden gebruikt in Spout:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Als ack wordt niet ondersteund in niet-transactionele topologie, Hallo `Ack()` en `Fail()` kan blijven als lege functie.

Hallo `parms` invoerparameters in deze functies zijn alleen lege woordenlijst, zijn gereserveerd voor toekomstig gebruik.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt is Hallo-interface voor niet-transactionele bolt.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Wanneer nieuwe tuple beschikbaar is, Hallo `Execute()` functie tooprocess worden aangeroepen wordt.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout is Hallo-interface voor transactionele spout.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Net als bij hun niet-transactionele tegenpost `NextTx()`, `Ack()`, en `Fail()` worden genoemd in een lus in een enkele thread in C\# proces. Wanneer er geen gegevens tooemit zijn, is het beleefd toohave `NextTx` slaapstand gedurende een korte tijd (10 milliseconden) dat niet toowaste te veel CPU.

`NextTx()`wordt genoemd, een nieuwe transactie toostart hello parameter `seqId` gebruikte tooidentify Hallo transactie, wordt ook gebruikt in `Ack()` en `Fail()`. In `NextTx()`, gebruiker gegevens tooJava kant kunt verzenden. Hallo-gegevens worden opgeslagen in ZooKeeper toosupport opnieuw afspelen. Omdat het Hallo-capaciteit van ZooKeeper is zeer beperkt, moet gebruikers alleen metagegevens, niet bulksgewijs gegevens in een transactionele spout verzenden.

Storm een transactie automatisch wordt herhaald als het mislukt, dus `Fail()` mag niet worden aangeroepen in normale geval. Maar als een SCP kunt Hallo metagegevens die door transactionele spout controleren, kan worden aangeroepen `Fail()` wanneer Hallo metagegevens is ongeldig.

Hallo `parms` invoerparameters in deze functies zijn alleen lege woordenlijst, zijn gereserveerd voor toekomstig gebruik.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt is Hallo-interface voor transactionele bolt.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`wordt aangeroepen wanneer er nieuwe tuple dat binnenkomt bij Hallo bolt. `FinishBatch()`wordt aangeroepen wanneer deze transactie is beëindigd. Hallo `parms` invoerparameter is gereserveerd voor toekomstig gebruik.

Voor transactionele topologie is een belangrijke concepten – `StormTxAttempt`. Deze twee velden heeft `TxId` en `AttemptId`. `TxId`gebruikte tooidentify is een specifieke transactie en voor een gegeven transactie, kunnen er meerdere poging als Hallo transactie mislukt en wordt opnieuw en nu afgespeeld. SCP.NET nieuwe wordt een andere ISCPBatchBolt object tooprocess elke `StormTxAttempt`, net zoals wat Storm moet aan de kant van Java. Hallo-doel van dit ontwerp is toosupport parallelle transacties verwerkt. Gebruiker moet Houd er rekening mee dat als poging van de transactie is voltooid, wordt het bijbehorende ISCPBatchBolt object Hallo vernietigd en garbage collector zijn verzameld.

## <a name="object-model"></a>Objectmodel
SCP.NET bevat ook een eenvoudige reeks key objecten voor ontwikkelaars tooprogram met. Ze zijn **Context**, **StateStore**, en **SCPRuntime**. Ze worden in Hallo rest deel uitmaken van deze sectie worden beschreven.

### <a name="context"></a>Context
Context biedt een actieve omgeving toohello toepassing. Elk exemplaar ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) heeft een corresponderende contextexemplaar. Hallo functionaliteit van Context kan worden onderverdeeld in twee delen: (1) Hallo statische deel die beschikbaar is in de hele C Hallo\# verwerken, (2) Hallo dynamische deel die alleen beschikbaar voor Hallo specifieke Context-exemplaar.

### <a name="static-part"></a>Statische deel
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger`is beschikbaar voor logboek-doel.

`pluginType`wordt gebruikt tooindicate Hallo invoegtoepassing type Hallo C\# proces. Als Hallo C\# proces wordt uitgevoerd in de lokale testmodus (zonder Java), het Hallo-invoegtoepassing type is `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`wordt geleverd tooget configuratieparameters van Java-kant. Hallo-parameters worden doorgegeven van Java-kant wanneer C\# invoegtoepassing is geïnitialiseerd. Hallo `Config` parameters worden onderverdeeld in twee delen: `stormConf` en `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`parameters zijn gedefinieerd door Storm is en `pluginConf` Hallo-parameters die zijn gedefinieerd door SCP is. Bijvoorbeeld:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`wordt geleverd tooget Hallo topologie context is het meest geschikt voor onderdelen met meerdere parallelle uitvoering is. Hier volgt een voorbeeld:

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

### <a name="dynamic-part"></a>Dynamische deel
Hallo volgende interfaces relevante tooa bepaalde contextexemplaar zijn. Hallo contextexemplaar is gemaakt door SCP.NET platform en toohello gebruikerscode doorgegeven:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Voor niet-transactionele spout ack ondersteunen, krijgt u Hallo methode te volgen:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Voor niet-transactionele bolt ack ondersteunen, moet deze expliciet `Ack()` of `Fail()` Hallo tuple deze ontvangen. En bij het genereren van nieuwe tuple, moet deze ook Hallo ankers van nieuwe tuple Hallo opgeven. Hallo volgende methoden zijn beschikbaar.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore`metagegevens van services, monotone reeks genereren en wacht gratis coördinatie biedt. Een hoger niveau gedistribueerde gelijktijdigheid abstracties kunnen worden gebaseerd op `StateStore`, met inbegrip van gedistribueerde vergrendelingen, gedistribueerde wachtrijen, barrières en transactieservices.

SCP-toepassingen kunt Hallo `State` object toopersist sommige gegevens in ZooKeeper, met name voor transactionele topologie. Dit doet, als transactionele spout is vastgelopen en opnieuw start, kunt het Hallo nodig informatie van ZooKeeper ophalen en opnieuw Hallo pijplijn starten.

Hallo `StateStore` object hoofdzakelijk heeft deze twee methoden:

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

Hallo `State` object hoofdzakelijk heeft deze twee methoden:

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

Voor Hallo `Commit()` wanneer u de methode simpleMode tootrue is ingesteld, zullen gewoon worden verwijderd Hallo ZNode in ZooKeeper overeenkomt. Anders wordt verwijderd Hallo huidige ZNode en het toevoegen van een nieuw knooppunt in Hallo DOORGEVOERD\_pad.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime biedt de volgende twee methoden Hallo.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`gebruikte tooinitialize Hallo SCP runtime-omgeving is. Bij deze methode Hallo C\# proces maakt verbinding toohello Java kant en de configuratieparameters opgehaald en topologie-context.

`LaunchPlugin()`gebruikte tookick uit het Hallo-bericht lus verwerkt. In deze lus Hallo C\# invoegtoepassing ontvangt berichten formulier Java kant (inclusief signalen tuples en control) en geeft u proces Hallo-berichten, mogelijk aanroepen Hallo interfacemethode door gebruikerscode Hallo. Hallo invoerparameter voor methode `LaunchPlugin()` is een gemachtigde die kan resulteren in een object dat ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt-interface implementeren.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Voor ISCPBatchBolt, krijgen we `StormTxAttempt` van `parms`, en deze toojudge gebruiken of het is een poging tot herhaald. Dit gebeurt gewoonlijk op Hallo doorvoeren bolt en dit wordt geïllustreerd in Hallo `HelloWorldTx` voorbeeld.

Normaal gesproken Hallo SCP plugins uitgevoerd in hier twee modi:

1. Lokale testmodus: In deze modus Hallo SCP-invoegtoepassingen (Hallo C\# gebruikerscode) in Visual Studio wordt uitgevoerd tijdens de Hallo ontwikkelingsfase bevindt. `LocalContext`kan worden gebruikt in deze modus, die biedt methode tooserialize Hallo verzonden tuples toolocal bestanden en lees deze toomemory terug te zetten.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Normale modus: In deze modus Hallo SCP plugins worden gestart door storm java-proces.
   
    Hier volgt een voorbeeld van het SCP-invoegtoepassing te starten:
   
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

## <a name="topology-specification-language"></a>Topologie specificatietaal
SCP-topologie-specificatie is een specifieke taal domein voor het beschrijven en topologieën SCP te configureren. Deze is gebaseerd op de Storm Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) en SCP is verlengd.

Topologie specificaties kunnen worden verzonden, direct toostorm voor de uitvoering van het cluster via Hallo ***runspec*** opdracht.

SCP.NET heeft toevoegen Volg functies toodefine Hallo transactionele topologie:

| **Nieuwe functies** | **Parameters** | **Beschrijving** |
| --- | --- | --- |
| **TX topolopy** |topologie-naam<br />spout-kaart<br />bolt-kaart |Definieer een transactionele-topologie met de naam van de topologie hello, &nbsp;spouts definitie kaart en Hallo bolts definitie-kaart |
| **SCP-tx-spout** |exec-naam<br />argumenten<br />Velden |Definieer een transactionele spout. Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.<br /><br />Hallo ***velden*** Hallo uitvoervelden voor spout is |
| **SCP-tx-batch-bolt** |exec-naam<br />argumenten<br />Velden |Definieer een transactionele Batch Bolt. Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten.***<br /><br />Hallo is velden Hallo velden uitvoeren voor bolt. |
| **SCP-tx-doorvoeren-bolt** |exec-naam<br />argumenten<br />Velden |Definieer een transactionele Committer Bolt. Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.<br /><br />Hallo ***velden*** Hallo uitvoervelden voor bolt is |
| **nontx topolopy** |topologie-naam<br />spout-kaart<br />bolt-kaart |Definieer een niet-transactionele-topologie met de naam van de topologie hello,&nbsp; spouts definitie kaart en Hallo bolts definitie-kaart |
| **SCP spout** |exec-naam<br />argumenten<br />Velden<br />parameters |Definieer een niet-transactionele spout. Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.<br /><br />Hallo ***velden*** Hallo uitvoervelden voor spout is<br /><br />Hallo ***parameters*** is optioneel, met behulp van deze toospecify sommige parameters zoals 'nontransactional.ack.enabled'. |
| **SCP-bolt** |exec-naam<br />argumenten<br />Velden<br />parameters |Definieer een niet-transactionele Bolt. Deze toepassing hello met uitgevoerd ***exec naam*** met ***argumenten***.<br /><br />Hallo ***velden*** Hallo uitvoervelden voor bolt is<br /><br />Hallo ***parameters*** is optioneel, met behulp van deze toospecify sommige parameters zoals 'nontransactional.ack.enabled'. |

SCP.NET heeft de volgende codes woorden gedefinieerd:

| **Trefwoorden** | **Beschrijving** |
| --- | --- |
| **: de naam** |Hallo-topologie naam definiëren |
| **: topologie** |Definieer Hallo topologie met behulp van Hallo hierboven functies en bouwen in toepassingsgroepen. |
| **: p** |Hallo parallelle uitvoering hint op voor elke spout of bolt definiëren. |
| **: config** |Definieer parameter configureren of update Hallo bestaande |
| **: schema** |Hallo-Schema van stroom definiëren. |

En veelgebruikte parameters:

| **Parameter** | **Beschrijving** |
| --- | --- |
| **'plugin.name'** |naam van de exe-bestand van Hallo C#-invoegtoepassing |
| **'plugin.args'** |invoegtoepassing argumenten |
| **'output.schema'** |Uitvoerschema |
| **'nontransactional.ack.enabled'** |Hiermee wordt aangegeven of ack is ingeschakeld voor niet-transactionele-topologie |

Hallo runspec opdracht samen met de Hallo bits wordt geïmplementeerd, lijkt op het Hallo-gebruik:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Hallo ***resource dir*** parameter is optioneel, moet u toospecify wanneer u wilt dat een C tooplug\# toepassings- en deze map bevat toepassing hello, Hallo afhankelijkheden en configuraties.

Hallo ***classpath*** parameter ook is optioneel. Het is gebruikte toospecify Hallo Java classpath als spec Hallo-bestand Java Spout of Bolt bevat.

## <a name="miscellaneous-features"></a>Diverse functies
### <a name="input-and-output-schema-declaration"></a>Invoer en uitvoer Schemadeclaratie
Hallo-gebruiker kunt verzenden tuple in C\# verwerken, hello platform moet tooserialize Hallo tuple in byte [] overdracht tooJava kant en Storm draagt deze tuple toohello doelen. Ondertussen in downstream onderdeel Hallo C\# proces wordt tuple terug van java-kant ontvangt en de oorspronkelijke typen toohello per platform converteren, alle deze bewerkingen zijn verborgen door Hallo Platform.

toosupport hello serialisatie en deserialisatie, moet gebruikerscode toodeclare Hallo schema Hallo en uitgangen.

Hallo i/o-stroom schema Hallo-sleutel is gedefinieerd als een woordenboek, Hallo StreamId en Hallo waarde Hallo typen Hallo kolommen. Hallo-component kan meerdere streams gedeclareerd hebben.

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


In de Context-object hebben we Hallo volgende API toegevoegd:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Gebruikerscode moet ervoor zorgen Hallo tuples verzonden hello schema gedefinieerd voor deze stroom te volgen of Hallo system genereert een runtime-fout.

### <a name="multi-stream-support"></a>Ondersteuning voor meerdere Stream
SCP ondersteunt gebruiker tooemit code of ontvangen van meerdere afzonderlijke streams op Hallo dezelfde tijd. Hallo ondersteuning weerspiegelt in Hallo Context-object als Hallo Emit methode een optionele stroom-ID-parameter moet.

Twee methoden in Hallo SCP.NET Context-object er zijn toegevoegd. Ze zijn gebruikt tooemit Tuple of Tuples toospecify StreamId. Hallo StreamId is een tekenreeks en moet u toobe consistent in beide C\# en Hallo topologie definitie-specificatie.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

Hallo importeerbereik tooa niet-bestaande stroom zorgt ervoor dat de runtime-uitzonderingen.

### <a name="fields-grouping"></a>Velden groeperen
Hallo die ingebouwde velden groeperen in Strom niet goed in SCP.NET werkt. Alle gegevenstypen van de Hallo-velden zijn daadwerkelijk byte [] op Hallo Java-Proxy aan clientzijde, en Hallo velden groeperen gebruikt Hallo byte [] object hash-code tooperform Hallo groepering. Hallo byte [] object hash-code is Hallo-adres van dit object in het geheugen. Dus Hallo groepering onjuist voor twee-byte []-objecten die share Hallo dezelfde inhoud, maar niet Hallo hetzelfde adres.

SCP.NET een groeperingsmethode met aangepaste toegevoegd en het Hallo-inhoud van het Hallo byte [] toodo Hallo groepering gebruikt. In **SPEC** bestand Hallo syntaxis is als volgt:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Hier kunt

1. "scp-veld-beheergroep" betekent 'Aangepast veld groepering wordt geïmplementeerd door SCP'.
2. ': tx 'of': niet-tx ' betekent dat als transactionele topologie is. Aangezien Hallo vanaf index in tx versus niet tx topologieën verschilt moeten we deze informatie.
3. [0,1] betekent een hashset van veld-id's, begint bij 0.

### <a name="hybrid-topology"></a>Hybride topologie
Hallo systeemeigen Storm is geschreven in Java. En SCP.Net is uitgebreid deze tooenable onze douane toowrite C\# code toohandle hun zakelijke logica. Maar we bieden ook ondersteuning voor hybride topologieën die bevat niet alleen C\# spouts/bolts, maar ook Java Spout/Bolts.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Java Spout/Bolt in spec bestand opgeven
In spec bestand kunnen 'scp-spout' en 'scp-bolt' ook gebruikte toospecify Java Spouts en Bolts, Hier volgt een voorbeeld:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Hier `microsoft.scp.example.HybridTopology.Generator` heet Hallo Hallo Spout Java-klasse.

### <a name="specify-java-classpath-in-runspec-command"></a>Java-klassenpad in runSpec opdracht opgeven
Als u met Java Spouts of Bolts toosubmit-topologie wilt, kunt u toofirst compileren Hallo Java Spouts of Bolts nodig en Hallo Jar-bestanden ophalen. Vervolgens moet u Hallo java classpath die Hallo Jar-bestanden bevat bij het indienen van de topologie. Hier volgt een voorbeeld:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Hier **voorbeelden\\HybridTopology\\java\\doel\\**  Hallo-map is waarin Hallo Java Spout/Bolt Jar-bestand.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Serialisatie en deserialisatie tussen Java en C\
Onze SCP-component bevat Java kant- en C\# aan clientzijde. In de volgorde toointeract met systeemeigen Java Spouts/Bolts, serialisatie/deserialisatie moet worden uitgevoerd tussen Java kant- en C\# zijde, zoals geïllustreerd in de volgende grafiek Hallo.

![diagram van java-component tooSCP onderdeel tooJava onderdeel verzenden verzenden](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Serialisatie in Java kant- en deserialisatie in C\# aan clientzijde**
   
   Eerst bieden we standaardimplementatie voor aan de kant van Java-serialisatie en deserialisatie in C\# aan clientzijde. Hallo serialisatiemethode in Java aan clientzijde kan worden opgegeven in SPEC bestand:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Hallo deserialisatie-methode in C\# kant moet worden opgegeven in de C\# gebruikerscode:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Deze standaardimplementatie afhandelt meestal als Hallo-gegevenstype niet te complex is. Voor bepaalde gevallen, ofwel omdat Hallo gebruikersgegevenstype is te complex is of omdat hello prestaties van onze standaardimplementatie voldoet niet aan de Hallo van de gebruiker vereist, gebruiker kan invoegtoepassing hun eigen implementatie.
   
   Hallo serialiseren interface in java aan clientzijde is gedefinieerd als:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Hallo deserialiseren interface in C\# aan clientzijde is gedefinieerd als:
   
   openbare interface ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Serialisatie in C\# kant- en deserialisatie in Java gelijktijdige**
   
   Hallo serialisatiemethode in C\# kant moet worden opgegeven in de C\# gebruikerscode:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   Hallo deserialisatie-methode in Java kant moet worden opgegeven in SPEC bestand:
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Hier 'microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer' Hallo-naam van de Deserializer is en 'microsoft.scp.example.HybridTopology.Person' is Hallo doel klassegegevens hello wordt gedeserialiseerd aan.
   
   De gebruiker kan ook invoegtoepassing hun eigen implementatie van C\# serialisatiefunctie en Java Deserializer. Dit is de interface Hallo voor C\# serialisatiefunctie:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Dit is Hallo-interface voor Java Deserializer:
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>SCP Host modus
In deze modus gebruiker hun tooDLL codes worden gecompileerd, en gebruik SCPHost.exe geleverd door een SCP toosubmit topologie. spec Hallo-bestand ziet er als volgt:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

Hier `plugin.name` is opgegeven als `SCPHost.exe` geleverd door een SCP-SDK. SCPHost.exe die precies drie parameters accepteert:

1. Hallo eerst een is Hallo dll-naam, die `"HelloWorld.dll"` in dit voorbeeld.
2. Hallo tweede is Hallo klassenaam, die is `"Scp.App.HelloWorld.Generator"` in dit voorbeeld.
3. Hallo derde een Hallo naam is van een openbare statische methode, waarbij aangeroepen tooget een exemplaar van ISCPPlugin worden kan.

In de modus host gebruikerscode is gecompileerd als dll-bestand en wordt aangeroepen door het SCP-platform. SCP-platform kan dus volledig beheer van Hallo hele verwerking logica krijgen. Daarom aangeraden voor onze klanten toosubmit topologie in SCP host modus omdat deze kunt Hallo ontwikkeling vereenvoudigen en ons meer flexibiliteit en betere compatibiliteit met eerdere versies van ook latere release zorgen.

## <a name="scp-programming-examples"></a>SCP programmering voorbeelden
### <a name="helloworld"></a>Hallo wereld
**HelloWorld** is een zeer eenvoudige voorbeeld tooshow een smaak van SCP.Net. Wordt een niet-transactionele-topologie met een spout aangeroepen **generator**, en twee bolts aangeroepen **splitser** en **teller**. Hallo spout **generator** wordt willekeurig enkele zinnen gegenereerd en deze zinnen te verzenden**splitser**. Hallo bolt **splitser** wordt gesplitst Hallo zinnen toowords en deze woorden te verzenden**teller** bolt. teller' Hello bout' maakt gebruik van een getal woordenlijst toorecord Hallo exemplaar van elk woord.

Er zijn twee bestanden spec **HelloWorld.spec** en **HelloWorld\_EnableAck.spec** voor dit voorbeeld. In Hallo C\# code, het vindt of ack door Hallo pluginConf van Java-kant is ingeschakeld.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

Als ack is ingeschakeld, is een woordenlijst in Hallo-spout gebruikte toocache Hallo tuples die niet bevestigd zijn. Als Fail() wordt aangeroepen, zal hello mislukte tuple worden cookies:

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

### <a name="helloworldtx"></a>HelloWorldTx
Hallo **HelloWorldTx** voorbeeld laat zien hoe tooimplement transactionele topologie. Er één spout aangeroepen **generator**, een batch bolts aangeroepen **gedeeltelijk aantal**, en een bolt doorvoeren aangeroepen **aantal som**. Er zijn ook drie vooraf gemaakte txt-bestanden: **DataSource0.txt**, **DataSource1.txt** en **DataSource2.txt**.

In elke transactie Hallo spout **generator** wordt willekeurig twee bestanden kiezen uit vooraf gemaakte drie bestanden Hallo en verzenden van Hallo twee bestand namen toohello **gedeeltelijk aantal** bolt. Hallo bolt **gedeeltelijk aantal** eerst Hallo-bestandsnaam niet ophalen uit Hallo ontvangen tuple vervolgens open Hallo bestands- en aantal Hallo aantal woorden in dit bestand en ten slotte verzenden Hallo word nummer toohello **count-som**bolt. Hallo **aantal som** bolt overzicht van het totale aantal Hallo.

tooachieve **exact één keer** semantiek, Hallo doorvoeren bolt **aantal som** moet toojudge of het om een herhaald transactie. In dit voorbeeld heeft een statisch lidvariabele:

    public static long lastCommittedTxId = -1; 

Wanneer een ISCPBatchBolt-exemplaar is gemaakt, krijgt het Hallo `txAttempt` van invoerparameters:

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

Wanneer `FinishBatch()` wordt aangeroepen, hello `lastCommittedTxId` update zijn als het is niet een herhaald transactie.

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


### <a name="hybridtopology"></a>HybridTopology
Deze topologie bevat een Java-Spout en een C\# Bolt. Hallo serialisatie en deserialisatie standaardimplementatie geleverd door een SCP platform wordt gebruikt. Voer ref Hallo **HybridTopology.spec** in **voorbeelden\\HybridTopology** map voor Hallo spec bestandsgegevens, en **SubmitTopology.bat** voor het Java-klassenpad toospecify.

### <a name="scphostdemo"></a>SCPHostDemo
In dit voorbeeld is in wezen hetzelfde als Hallo wereld Hallo. Hallo alleen verschil is dat Hallo gebruikerscode wordt gecompileerd als dll-bestand en Hallo-topologie wordt ingediend via SCPHost.exe. Maak ref Hallo sectie 'SCP Host modus' voor meer gedetailleerde uitleg.

## <a name="next-steps"></a>Volgende stappen
Zie voor voorbeelden van Storm-topologieën die zijn gemaakt met behulp van SCP Hallo volgende:

* [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Maken van meerdere gegevensstromen in een C# Storm-topologie](hdinsight-storm-twitter-trending.md)
* [Power Bi toovisualize gegevens uit een Storm-topologie gebruiken](hdinsight-storm-power-bi-topology.md)
* [Verwerken van sensorgegevens vehicle van Event Hubs met behulp van Storm op HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Uitpakken, transformeren en Load (ETL) van Azure Event Hubs tooHBase](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Gebeurtenissen met Storm en HBase op HDInsight correleren](hdinsight-storm-correlation-topology.md)

