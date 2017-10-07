---
title: "aaaApache Storm-topologieën met Visual Studio en C# - Azure HDInsight | Microsoft Docs"
description: "Meer informatie over hoe toocreate Storm-topologieën in C#. Een eenvoudige word-count-topologie in Visual Studio maakt met behulp van Hallo Hadoop-hulpprogramma's voor Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>C#-topologieën ontwikkelen voor Apache Storm met behulp van Hallo Data Lake tools voor Visual Studio

Meer informatie over hoe toocreate een C# Storm-topologie met behulp van hello Azure Data Lake (Hadoop) tools voor Visual Studio. Dit document wordt uitgelegd Hallo-proces voor het maken van een Storm-project in Visual Studio, lokaal te testen en implementeren van tooan Apache Storm op Azure HDInsight-cluster.

U leert ook hoe toocreate hybride topologieën die werken met C# en Java-onderdelen.

> [!NOTE]
> Hoewel Hallo stappen in dit document, is afhankelijk van een Windows-ontwikkelomgeving met Visual Studio, zijn gecompileerd Hallo-project ingediende tooeither een Linux- of Windows gebaseerde HDInsight-cluster. Op basis van Linux-clusters die zijn gemaakt na 28 oktober 2016 ondersteunen alleen SCP.NET topologieën.

toouse een C#-topologie met een cluster op basis van Linux, moet u Hallo Microsoft.SCP.Net.SDK NuGet-pakket gebruikt door uw project tooversion 0.10.0.6 of hoger bijwerken. Hallo-versie van het Hallo-pakket moet ook overeenkomen met de Hallo primaire versie van Storm op HDInsight is geïnstalleerd.

| HDInsight-versie | Storm-versie | SCP.NET versie | Standaard Mono-versie |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(alleen op HDInsight op basis van Windows) | N.v.t. |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> C#-topologieën op Linux gebaseerde clusters moeten gebruiken, .NET 4.5 en het gebruik van Mono toorun op Hallo HDInsight-cluster. Controleer [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) voor potentiële compatibiliteitsproblemen.

## <a name="install-visual-studio"></a>Visual Studio installeren

U kunt de C#-topologieën met SCP.NET ontwikkelen met behulp van een van de volgende versies van Visual Studio Hallo:

* Visual Studio 2012 met [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 met [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 of [Visual Studio 2015-Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (alle versies)

## <a name="install-data-lake-tools-for-visual-studio"></a>Installatie van Data Lake tools voor Visual Studio

tooinstall Data Lake tools voor Visual Studio, Hallo stappen in [aan de slag met Data Lake tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Java installeren

Wanneer u een Storm-topologie vanuit Visual Studio indient, genereert SCP.NET een zip-bestand dat Hallo topologie en afhankelijkheden bevat. Java gebruikte toocreate is deze zip-bestanden, omdat deze gebruikmaakt van een indeling die is beter geschikt voor clusters op basis van Linux.

1. Hallo Java Developer Kit (JDK) 7 of hoger installeren op uw ontwikkelomgeving. U kunt krijgen Hallo Oracle JDK van [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). U kunt ook [andere Java-distributies](http://openjdk.java.net/).

2. Hallo `JAVA_HOME` omgeving variabele moet punt toohello directory met Java.

3. Hallo `PATH` omgevingsvariabele vergezeld Hallo `%JAVA_HOME%\bin` directory.

Hallo volgende C#-console toepassing tooverify Java en Hallo JDK juist zijn geïnstalleerd, kunt u gebruiken:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Storm-sjablonen

Hallo Data Lake tools voor Visual Studio bieden Hallo sjablonen te volgen:

| Projecttype | Demonstreert |
| --- | --- |
| Storm-toepassing |Een leeg Storm-topologie-project. |
| Storm Azure SQL Writer voorbeeld |Hoe toowrite tooAzure SQL-Database. |
| Voorbeeld van storm Azure Cosmos DB lezer |Hoe tooread uit Azure Cosmos-database. |
| Storm Azure Cosmos DB Writer voorbeeld |Hoe toowrite tooAzure Cosmos DB. |
| Voorbeeld van storm EventHub-lezer |Hoe tooread uit Azure Event Hubs. |
| Voorbeeld van storm EventHub-schrijver |Hoe toowrite tooAzure Event Hubs. |
| Voorbeeld van storm-HBase-lezer |Hoe tooread van HBase op HDInsight-clusters. |
| Voorbeeld van storm-HBase-schrijver |Hoe toowrite tooHBase op HDInsight-clusters. |
| Storm hybride voorbeeld |Hoe toouse een Java-component. |
| Storm-voorbeeld |Een basic word-count-topologie. |

> [!WARNING]
> Niet alle sjablonen, werken met HDInsight op basis van Linux. Nuget-pakketten die worden gebruikt door Hallo sjablonen zijn mogelijk niet compatibel met Mono. Controleer Hallo [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) documenteren en gebruik Hallo [.NET draagbaarheid Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potentiële problemen.

In Hallo stappen in dit document gebruikt u Hallo basic Storm-toepassing project type toocreate een topologie.

### <a name="hbase-templates-notes"></a>Opmerkingen bij de HBase-sjablonen

Hallo HBase lezer en writer sjablonen gebruiken Hallo HBase REST API, niet Hallo HBase Java API, toocommunicate met een HBase op HDInsight-cluster.

### <a name="eventhub-templates-notes"></a>Opmerkingen bij de EventHub-sjablonen

> [!IMPORTANT]
> Hallo Java gebaseerde EventHub spout onderdeel van Hallo EventHub lezer sjabloon niet met Storm op HDInsight versie 3.5 of hoger werken mogelijk. Een bijgewerkte versie van dit onderdeel is beschikbaar op [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Zie voor een topologie die gebruikmaakt van dit onderdeel en werkt met Storm op HDInsight 3.5, [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Maak een C#-topologie

1. Open Visual Studio, selecteer **bestand** > **nieuw**, en selecteer vervolgens **Project**.

2. Van Hallo **nieuw Project** venster Vouw **geïnstalleerde** > **sjablonen**, en selecteer **Azure Data Lake**. Selecteer in de lijst met sjablonen Hallo **Storm-toepassing**. Voer Hallo onderaan welkomstscherm in **WordCount** als naam van de toepassing hello Hallo.

    ![Schermopname van nieuw Project-venster](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Nadat u Hallo-project hebt gemaakt, hebt u Hallo volgende bestanden:

   * **Program.cs**: dit bestand definieert het Hallo-topologie voor uw project. Standaard wordt een standaard-topologie die uit één spout en één bolt bestaat gemaakt.

   * **Spout.cs**: een voorbeeld spout die willekeurige getallen verzendt.

   * **Bolt.cs**: een voorbeeld-bolt die een aantal van de getallen die worden verzonden door Hallo spout houdt.

     Wanneer u Hallo-project maakt, NuGet downloads laatste Hallo [SCP.NET pakket](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Implementeer Hallo spout

1. Open **Spout.cs**. Spouts zijn gebruikte tooread gegevens in een topologie van een externe bron. hoofdonderdelen voor een spout Hallo zijn:

   * **NextTuple**: door Storm wordt aangeroepen wanneer de Hallo spout tooemit nieuwe tuples is toegestaan.

   * **ACK** (alleen voor transactionele topologie): bevestigingen geïnitieerd door de andere onderdelen in Hallo-topologie voor verzonden van Hallo spout tuples worden verwerkt. Een tuple zijn bevestigd, kunt Hallo spout weten dat deze is verwerkt door downstream-onderdelen.

   * **Mislukken** (alleen voor transactionele topologie): tuples die zijn mislukt-verwerking van andere onderdelen in de topologie Hallo verwerkt. Implementatie van een methode is mislukt, kunt u toore-tuple Hallo verzenden zodat deze opnieuw kan worden verwerkt.

2. Vervang de inhoud Hallo Hallo **Spout** klasse met de volgende tekst hello. Deze spout verzendt willekeurig een zin in Hallo-topologie.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Hallo bolts implementeren

1. Verwijder bestaande Hallo **Bolt.cs** bestand uit Hallo-project.

2. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **toevoegen** > **nieuw item**. Selecteer in de lijst Hallo **Storm Bolt**, en voer **Splitter.cs** als Hallo-naam. Herhaal dit proces toocreate met de naam een tweede bolt **Counter.cs**.

   * **Splitter.cs**: implementeert een bolt die zinnen splitst in afzonderlijke woorden en verzendt een nieuwe reeks woorden.

   * **Counter.cs**: implementeert een bolt die elk woord telt en verzendt een nieuwe reeks woorden en Hallo telling voor elk woord.

     > [!NOTE]
     > Deze bolts lezen en schrijven toostreams, maar u kunt ook een bolt toocommunicate met bronnen zoals een database of service.

3. Open **Splitter.cs**. Slechts één methode heeft standaard: **Execute**. Hallo Execute-methode wordt aangeroepen wanneer Hallo bolt een tuple voor verwerking ontvangt. Hier vindt u binnenkomende tuples verwerken en verzenden van uitgaande tuples.

4. Vervang de inhoud Hallo Hallo **splitser** klasse Hello code te volgen:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Open **Counter.cs**, en vervang Hallo klasse inhoud door Hallo volgende:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Hallo-topologie definiëren

Spouts en bolts worden gerangschikt in een grafiek, waarmee wordt gedefinieerd hoe Hallo gegevens tussen onderdelen loopt. Voor deze topologie is Hallo grafiek als volgt uit:

![Diagram van hoe onderdelen worden gerangschikt](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Zinnen van Hallo spout worden verzonden en gedistribueerde tooinstances van Hallo splitser bolt zijn. Hallo zinnen Hallo splitser bolt opgesplitst in woorden die gedistribueerd toohello teller bolt zijn.

Omdat het aantal woorden is die lokaal zijn opgeslagen in een exemplaar van prestatiemeteritem hello, willen we zeker van te zijn dat specifieke woorden toohello vloeien toomake hetzelfde exemplaar van prestatiemeteritem bolt. Elk exemplaar houdt van specifieke woorden. Aangezien Hallo splitser bolt geen status onderhoudt, het echt maakt niet uit welke instantie van de splitser Hallo ontvangt welke zin.

Open **Program.cs**. Hallo belangrijke methode is **GetTopologyBuilder**, tooStorm die is gebruikt toodefine Hallo-topologie die is verzonden. Vervang de inhoud Hallo van **GetTopologyBuilder** Hello na code tooimplement Hallo topologie eerder beschreven:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Hallo-topologie verzenden

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.

   > [!NOTE]
   > Als u wordt gevraagd, voert u Hallo referenties voor uw Azure-abonnement. Als u meer dan één abonnement hebt, meld u aan toohello een bestand met uw Storm op HDInsight-cluster.

2. Selecteer uw Storm op HDInsight-cluster in Hallo **Storm-Cluster** vervolgkeuzelijst en selecteer vervolgens **indienen**. U kunt controleren als Hallo verzending is voltooid met Hallo **uitvoer** venster.

3. Wanneer het Hallo-topologie is ingediend, Hallo **Storm-topologieën** voor Hallo cluster moet worden weergegeven. Selecteer Hallo **WordCount** topologie van Hallo lijst tooview informatie over het Hallo-topologie wordt uitgevoerd.

   > [!NOTE]
   > U kunt ook weergeven **Storm-topologieën** van **Server Explorer**. Vouw **Azure** > **HDInsight**, met de rechtermuisknop op een Storm op HDInsight-cluster en selecteer vervolgens **weergave Storm-topologieën**.

    tooview informatie over Hallo-onderdelen in Hallo-topologie, dubbelklik op Hallo-component in Hallo-diagram.

4. Van Hallo **Topology Summary** weergeven, klikt u op **Kill** toostop Hallo topologie.

   > [!NOTE]
   > Storm-topologieën blijven toorun totdat ze worden gedeactiveerd of Hallo-cluster is verwijderd.

## <a name="transactional-topology"></a>Transactionele-topologie

Hallo vorige topologie is niet-transactionele. Hallo-onderdelen in de topologie Hallo functionaliteit tooreplaying berichten niet geïmplementeerd. Voor een voorbeeld van een transactionele topologie, maak een project en selecteer **Storm voorbeeld** als Hallo projecttype.

Transactionele topologieën implementeren Hallo toosupport replay van gegevens te volgen:

* **Metagegevens opslaan in cache**: Hallo spout moet slaan metagegevens over Hallo gegevens verzonden, zodat Hallo gegevens kunnen worden opgehaald en opnieuw verzonden als er een fout optreedt. Omdat het Hallo-gegevens die door Hallo voorbeeld klein is, wordt in een woordenlijst om replaydetectie Hallo onbewerkte gegevens voor elke tuple opgeslagen.

* **ACK**: elke bolt in Hallo topologie kunt aanroepen `this.ctx.Ack(tuple)` tooacknowledge dat deze is een tuple verwerkt. Wanneer alle bolts bevestigd Hallo tuple hebt, Hallo `Ack` hello spout methode wordt aangeroepen. Hallo `Ack` methode kunnen Hallo spout tooremove gegevens om replaydetectie in cache is opgeslagen.

* **Mislukken**: elke bolt kunt aanroepen `this.ctx.Fail(tuple)` tooindicate die verwerking is mislukt voor een tuple. Hallo fout doorgegeven toohello `Fail` methode van Hallo spout, waarbij Hallo-tuple kan worden cookies met behulp van metagegevens in cache.

* **Sequentiëren ID**: bij het genereren van een tuple een unieke reeks-ID kan worden opgegeven. Deze waarde identificeert Hallo tuple voor de verwerking van opnieuw afspelen (Ack en mislukken). Bijvoorbeeld, Hallo spout in Hallo **Storm voorbeeld** Hallo volgende wordt gebruikt bij het genereren van gegevens:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Deze code verzendt een tuple met een zin toohello standaard-stream met Hallo reeks id-waarde is opgenomen in **lastSeqId**. In dit voorbeeld **lastSeqId** voor elke tuple verzonden wordt verhoogd.

Zoals wordt beschreven in Hallo **Storm voorbeeld** project, of een onderdeel is transactionele kan worden ingesteld tijdens runtime, op basis van configuratie.

## <a name="hybrid-topology-with-c-and-java"></a>Hybride topologie met C# en Java

U kunt ook Data Lake tools voor Visual Studio toocreate hybride topologieën, waarin bepaalde onderdelen zijn C# en anderen Java zijn.

Voor een voorbeeld van een hybride-topologie, maak een project en selecteer **Storm hybride voorbeeld**. Dit Voorbeeldtype demonstreert Hallo volgende concepten:

* **Java-spout** en **C# bolt**: gedefinieerd in **HybridTopology_javaSpout_csharpBolt**.

    * Een transactionele versie is gedefinieerd in **HybridTopologyTx_javaSpout_csharpBolt**.

* **C# spout** en **Java bolt**: gedefinieerd in **HybridTopology_csharpSpout_javaBolt**.

    * Een transactionele versie is gedefinieerd in **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Deze versie wordt ook getoond hoe toouse Clojure code uit een tekstbestand als een Java-onderdeel.


tooswitch hello topologie die wordt gebruikt wanneer het Hallo-project wordt ingediend, verplaatst Hallo `[Active(true)]` instructie toohello topologie toouse, voordat het wordt ingediend toohello cluster.

> [!NOTE]
> Alle Hallo Java-bestanden die vereist zijn worden geleverd als onderdeel van dit project in Hallo **JavaDependency** map.

Overweeg Hallo volgende wanneer u maken en verzenden van een hybride-topologie:

* U moet gebruiken **JavaComponentConstructor** toocreate een exemplaar van Hallo Java-klasse voor een spout of bolt.

* U moet gebruiken **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON tooserialize gegevens van of naar Java-onderdelen van Java-objecten.

* Bij het indienen van Hallo topologie toohello server, moet u Hallo **aanvullende configuraties** optie toospecify hello **Java bestandspaden**. Hallo-pad opgegeven moet Hallo directory met Hallo JAR-bestanden die uw Java-klassen bevatten.

### <a name="azure-event-hubs"></a>Azure Event Hubs

SCP.NET versie 0.9.4.203 introduceert een nieuwe klasse en de methode specifiek voor het werken met Hallo Event Hub spout (een Java-spout die uit Event Hubs lezen). Wanneer u een topologie maakt die gebruikmaakt van een Event Hub spout, gebruik Hallo volgende methoden:

* **EventHubSpoutConfig** klasse: maakt een object dat het Hallo-configuratie voor Hallo spout onderdeel bevat.

* **TopologyBuilder.SetEventHubSpout** methode: Hallo Event Hub spout onderdeel toohello topologie worden toegevoegd.

> [!NOTE]
> U moet nog steeds gebruiken Hallo **CustomizedInteropJSONSerializer** tooserialize gegevens geproduceerd door Hallo spout.

## <a id="configurationmanager"></a>Configuration Manager gebruiken

Gebruik geen **ConfigurationManager** tooretrieve configuratiewaarden van Bolts en spout onderdelen. In dat geval kan een uitzondering voor een null-aanwijzer veroorzaken. In plaats daarvan wordt Hallo-configuratie voor uw project in Hallo Storm-topologie doorgegeven als een sleutel-waardepaar in de context van Hallo-topologie. Elk onderdeel dat is afhankelijk van de configuratiewaarden moet deze worden opgehaald van Hallo context tijdens de initialisatie.

Hallo volgende code laat zien hoe tooretrieve deze waarden:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Als u een `Get` methode tooreturn een instantie van het onderdeel, moet u ervoor zorgen dat dit wordt doorgegeven beide Hallo `Context` en `Dictionary<string, Object>` parameters toohello constructor. Hallo volgende voorbeeld is een eenvoudige `Get` methode die deze waarden correct is geslaagd:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Hoe tooupdate SCP.NET

Recente versies van SCP.NET ondersteuning pakketupgrade via NuGet. Wanneer een nieuwe update beschikbaar is, ontvangt u een upgrade melding. toomanually selectievakje voor een upgrade als volgt te werk:

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **NuGet-pakketten beheren**.

2. Selecteer in het Hallo-Pakketbeheer **Updates**. Als een update beschikbaar is, wordt het weergegeven. Klik op **Update** voor Hallo pakket tooinstall deze.

> [!IMPORTANT]
> Als uw project is gemaakt met een eerdere versie van SCP.NET die NuGet niet gebruikt, moet u de volgende stappen tooupdate tooa nieuwere versie Hallo uitvoeren:
>
> 1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **NuGet-pakketten beheren**.
> 2. Met behulp van Hallo **Search** veld, zoeken en vervolgens toevoegt, **Microsoft.SCP.Net.SDK** toohello project.

## <a name="troubleshoot-common-issues-with-topologies"></a>Algemene problemen met topologieën

### <a name="null-pointer-exceptions"></a>Null-aanwijzer uitzonderingen

Wanneer u van een C#-topologie met een Linux gebaseerde HDInsight-cluster gebruikmaakt, Bolts en onderdelen die gebruikmaken van spout **ConfigurationManager** tooread configuratie-instellingen tijdens runtime kunnen null-aanwijzer uitzonderingen retourneren.

Hallo-configuratie voor uw project is doorgegeven aan Hallo Storm-topologie als een sleutel-waardepaar in de context van Hallo-topologie. Het kan worden opgehaald uit Hallo dictionary-object dat wordt doorgegeven tooyour onderdelen wanneer deze worden geïnitialiseerd.

Zie voor meer informatie, Hallo [ConfigurationManager](#configurationmanager) gedeelte van dit document.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Wanneer u van een C#-topologie met een Linux gebaseerde HDInsight-cluster gebruikmaakt, kunnen Hallo volgende fout optreden:

    System.TypeLoadException: Failure has occurred while loading a type.

Deze fout treedt op wanneer u een binair bestand dat niet compatibel met Hallo van .NET-versies die ondersteuning biedt voor Mono gebruiken.

Zorg ervoor dat uw project maakt gebruik van binaire bestanden voor .NET 4.5 compiled Linux gebaseerde HDInsight-clusters.

### <a name="test-a-topology-locally"></a>Een topologie lokaal testen

Hoewel het eenvoudig toodeploy een topologie tooa cluster, in sommige gevallen moet u een topologie lokaal tootest. Gebruik Hallo toorun stappen te volgen en Hallo voorbeeldtopologie testen in deze zelfstudie lokaal in uw ontwikkelomgeving.

> [!WARNING]
> Lokale testen werkt alleen voor basic, C#-topologieën voor alleen. U de lokale testen voor hybride topologieën of topologieën met meerdere streams niet gebruiken.

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **eigenschappen**. Wijzig in de Projecteigenschappen hello, Hallo **type uitvoer** te**consoletoepassing**.

    ![Schermafbeelding van de Projecteigenschappen met uitvoertype gemarkeerd](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Houd er rekening mee toochange Hallo **type uitvoer** back te maken**Class Library** voordat u Hallo topologie tooa cluster implementeert.

2. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer vervolgens **toevoegen** > **Nieuw Item**. Selecteer **klasse**, en voer **LocalTest.cs** als Hallo klassenaam. Tot slot op **toevoegen**.

3. Open **LocalTest.cs**, en voeg de volgende Hallo **met** instructie Hallo boven:

    ```csharp
    using Microsoft.SCP;
    ```

4. Gebruik Hallo volgende code als inhoud Hallo Hallo **LocalTest** klasse:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Een ogenblik tooread via Hallo codeopmerkingen in beslag nemen. Deze code gebruikt **LocalContext** toorun Hallo onderdelen in het Hallo-ontwikkelomgeving en zich blijft voordoen Hallo gegevensstroom tussen onderdelen tootext bestanden op de lokale schijf Hallo.

1. Open **Program.cs**, en Voeg na toohello hello **Main** methode:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Hallo wijzigingen opslaan en klik vervolgens op **F5** of selecteer **Debug** > **foutopsporing starten** toostart Hallo project. Een consolevenster moet worden weergegeven en meld u aan status als Hallo tests uitgevoerd. Wanneer **Tests voltooid** wordt weergegeven, drukt u op een sleutel tooclose Hallo-venster.

3. Gebruik **Windows Verkenner** toolocate Hallo directory met uw project. Bijvoorbeeld: **C:\Users\<gebruikersnaam > \Documents\Visual Studio 2013\Projects\WordCount\WordCount**. Open in deze map **Bin**, en klik vervolgens op **Debug**. U ziet Hallo tekstbestanden die zijn geproduceerd als Hallo tests uitgevoerd: sentences.txt counter.txt en splitter.txt. Open elk tekstbestand en Hallo gegevens controleren.

   > [!NOTE]
   > Tekenreeksgegevens zich blijft voordoen als een matrix met decimale waarden in deze bestanden. Bijvoorbeeld: \[[97,103,111]] in Hallo **splitter.txt** bestand is Hallo word *en*.

> [!NOTE]
> Ervoor tooset Hallo worden **projecttype** back-te**Class Library** voordat u implementeert tooa Storm op HDInsight-cluster.

### <a name="log-information"></a>Logboekgegevens

U kunt eenvoudig gegevens van de onderdelen van uw topologie vastleggen met behulp van `Context.Logger`. Hallo volgende wordt bijvoorbeeld een informatieve logboekvermelding gemaakt:

```csharp
Context.Logger.Info("Component started");
```

Logboekgegevens kan bekeken worden vanuit Hallo **Hadoop-serviceaccount voor aanmelden**, die is gevonden **Server Explorer**. Vouw Hallo-vermelding voor uw Storm op HDInsight-cluster uit en vouw vervolgens **Hadoop-serviceaccount voor aanmelden**. Ten slotte Hallo log-bestand tooview selecteren.

> [!NOTE]
> Hallo-logboeken worden opgeslagen in hello Azure storage-account dat wordt gebruikt door het cluster. tooview hello Logboeken in Visual Studio, moet u in Azure-abonnement dat eigenaar is van het opslagaccount Hallo toohello ondertekenen.

### <a name="view-error-information"></a>Fout-informatie weergeven

tooview fouten die zijn opgetreden in een actieve topologie gebruik Hallo stappen te volgen:

1. Van **Server Explorer**, met de rechtermuisknop op Hallo Storm op HDInsight-cluster en selecteert u **weergave Storm-topologieën**.

2. Voor Hallo **Spout** en **Bolts**, Hallo **laatste fout** kolom bevat informatie over de laatste fout Hallo.

3. Selecteer Hallo **Spout Id** of **Bolt Id** voor Hallo-onderdeel met een fout weergegeven. Op de detailpagina Hallo die wordt weergegeven, extra fout informatie wordt weergegeven in Hallo **fouten** sectie Hallo Hallo pagina onderaan in.

4. tooobtain meer informatie, selecteer een **poort** van Hallo **Executor** sectie van de pagina hello, toosee Hallo Storm worker logboek voor Hallo laatste paar minuten.

### <a name="errors-submitting-topologies"></a>Fouten verzonden topologieën

Als er een topologie-tooHDInsight verzenden fouten optreden, kunt u Logboeken vinden voor Hallo serveronderdelen dat de verzending van de topologie op uw HDInsight-cluster te verwerken. tooretrieve deze zich aanmeldt, gebruik Hallo volgende opdracht uit vanaf een opdrachtregel:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Vervang __sshuser__ Hello SSH gebruikersaccount voor Hallo-cluster. Vervang __clustername__ met de naam van de HDInsight-cluster Hallo Hallo. Voor meer informatie over het gebruik van `scp` en `ssh` met HDInsight, raadpleegt u [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Voorbeelden kunnen om meerdere redenen mislukken:

* JDK is niet geïnstalleerd of is niet in het Hallo-pad.
* Vereiste Java-afhankelijkheden zijn niet opgenomen in Hallo verzending.
* Niet-compatibele afhankelijkheden.
* Dubbele namen van de topologie.

Als hello `hdinsight-scpwebapi.out` logboek bevat een `FileNotFoundException`, dit wordt mogelijk veroorzaakt door Hallo volgende voorwaarden:

* Hallo JDK is niet in Hallo-pad op Hallo-ontwikkelomgeving. Controleer of deze Hallo JDK in Hallo ontwikkelomgeving en die is geïnstalleerd `%JAVA_HOME%/bin` Hallo-pad.
* Ontbreekt er een Java-afhankelijkheid. Zorg ervoor dat u alle vereiste JAR-bestanden als onderdeel van de verzending van hello opneemt.

## <a name="next-steps"></a>Volgende stappen

Zie voor een voorbeeld van het verwerken van gegevens uit Event Hubs, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Zie voor een voorbeeld van een C#-topologie die stroomgegevens in meerdere streams splitst [C# Storm-voorbeeld](https://github.com/Blackmist/csharp-storm-example).

toodiscover meer informatie over het maken van C#-topologieën, Zie [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Zie voor meer manieren toowork met HDInsight en meer Storm op HDInsight voorbeelden Hallo documenten te volgen:

**Microsoft SCP.NET**

* [Programmeerhandleiding voor SCP](hdinsight-storm-scp-programming-guide.md)

**Apache Storm op HDInsight**

* [Implementeren en bewaken topologieën met Apache Storm op HDInsight](hdinsight-storm-deploy-monitor-topology.md)
* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop in HDInsight**

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

**Apache HBase in HDInsight**

* [Aan de slag met HBase in HDInsight](hdinsight-hbase-tutorial-get-started.md)
