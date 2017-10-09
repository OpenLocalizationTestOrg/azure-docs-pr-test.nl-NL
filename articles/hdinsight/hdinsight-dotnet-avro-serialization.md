---
title: gegevens in Azure Hadoop - Library Microsoft Avro - aaaSerialize | Microsoft Docs
description: Meer informatie over hoe tooserialize en deserialiseren van gegevens in Hadoop in HDInsight met Hallo Microsoft Avro Library toopersist toomemory, een database of een bestand.
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Gegevens in Hadoop Hello Microsoft Avro Library serialiseren

>[!NOTE]
>Hallo Avro SDK wordt niet langer ondersteund door Microsoft. Hallo-bibliotheek is open-source community ondersteund. Hallo-bronnen voor Hallo bibliotheek bevinden zich in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

Dit onderwerp wordt beschreven hoe toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objecten en andere gegevens structuren in streams toopersist ze toomemory, een database of een bestand. U ziet ook hoe toodeserialize ze toorecover Hallo originele objecten.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Hallo <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements Hallo systeem voor serialisatie Apache Avro voor Hallo Microsoft.NET-omgeving. Apache Avro biedt een compacte binaire gegevens DIF-indeling voor serialisatie. Hierbij <a href="http://www.json.org" target="_blank">JSON</a> toodefine een taal networkdirect-schema dat taalherkenning interoperabiliteit van talen. Gegevens die zijn geserialiseerd in één taal kan worden gelezen in een andere. C, C++ C#, Java, PHP, Python en Ruby worden momenteel ondersteund. Gedetailleerde informatie over het Hallo-indeling vindt u in Hallo <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro-specificatie</a>. 

>[!NOTE]
>Hallo Microsoft Avro Library biedt geen ondersteuning voor Hallo externe procedureaanroepen (RPC's)-aanroepen deel van deze specificatie.
>

Hallo geserialiseerd representatie van een object in Hallo Avro-systeem bestaat uit twee delen: schema en de werkelijke waarde. Hallo Avro-schema beschrijft Hallo taalonafhankelijke gegevensmodel van Hallo geserialiseerd gegevens met JSON. Deze functionaliteit wordt weergegeven naast een binaire voorstelling van gegevens. Hallo-schema is gescheiden van de binaire voorstelling Hallo met staat elk object toobe geschreven met de overhead van geen per waarde, waardoor serialisatie snel en hello weergave kleine.

## <a name="hello-hadoop-scenario"></a>Hallo Hadoop-scenario
Hallo Apache Avro serialisatie-indeling wordt veel gebruikt in Azure HDInsight en andere Apache Hadoop-omgevingen. Avro biedt een handige manier toorepresent complexe gegevensstructuren binnen een Hadoop-MapReduce-taak. Hallo-indeling van het Avro-bestanden (Avro object container-bestand) is ontworpen toosupport Hallo gedistribueerde MapReduce-programmeermodel. Hallo belangrijke functie waarmee Hallo gedistribueerd is dat bestanden Hallo 'splittable' in de zin Hallo één kunt elk punt in een bestand en beginnen met lezen van een bepaald blok zijn.

## <a name="serialization-in-avro-library"></a>Serialisatie in de bibliotheek voor Avro
Hallo .NET-bibliotheek voor Avro ondersteunt serialiseren objecten op twee manieren:

* **Reflectie** -Hallo JSON-schema voor Hallo typen automatisch gebouwd van Hallo gegevens contract kenmerken van Hallo .NET typen toobe geserialiseerd.
* **algemene record** -een JSON-schema expliciet is opgegeven in een record die wordt vertegenwoordigd door Hallo [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) wanneer er geen .NET-typen aanwezig toodescribe Hallo-schema voor Hallo gegevens toobe zijn klasse geserialiseerd.

Hallo gegevensschema is bekend tooboth Hallo writer en lezer van de stroom hello, kan Hallo gegevens kunnen worden verzonden zonder dat het schema. In gevallen dat wanneer een Avro-object container-bestand wordt gebruikt, Hallo schema wordt opgeslagen in Hallo-bestand. Andere parameters, zoals Hallo codec gebruikt voor de compressie van gegevens kunnen worden opgegeven. Deze scenario's zijn in meer detail beschreven en wordt geïllustreerd in de volgende codevoorbeelden Hallo:

## <a name="install-avro-library"></a>Bibliotheek voor Avro installeren
Hallo volgende is vereist voordat u Hallo bibliotheek installeert:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 of hoger)

Houd er rekening mee dat Hallo Newtonsoft.Json.dll afhankelijkheid wordt automatisch gedownload met de installatie Hallo Hallo Microsoft Avro Library. Hallo-procedure is opgegeven in de volgende sectie Hallo:

Hallo Microsoft Avro Library wordt gedistribueerd als een NuGet-pakket dat kan worden geïnstalleerd vanuit Visual Studio via Hallo procedure te volgen:

1. Selecteer Hallo **Project** tabblad -> **NuGet-pakketten beheren...**
2. Zoek naar 'Microsoft.Hadoop.Avro' in hello **Online zoeken** vak.
3. Klik op Hallo **installeren** knop naast te**Avro-bibliotheek van Microsoft Azure HDInsight**.

Houd er rekening mee dat Hallo Newtonsoft.Json.dll (> = 6.0.4) afhankelijkheid ook automatisch wordt gedownload Hello Microsoft Avro Library.

Hallo Microsoft Avro Library broncode is beschikbaar op [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Schema's met behulp van de bibliotheek voor Avro compileren
Hallo Microsoft Avro Library bevat een codegeneratie hulpprogramma waarmee het maken van C#-typen automatisch op basis van Hallo eerder JSON-schema is gedefinieerd. Hallo code generatie hulpprogramma niet is gedistribueerd als een binair uitvoerbaar bestand, maar kan eenvoudig worden opgebouwd via Hallo procedure te volgen:

1. Hallo ZIP-bestand met de meest recente versie Hallo van broncode HDInsight SDK uit downloaden <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK voor Hadoop</a>. (Klik op Hallo **downloaden** pictogram, niet Hallo **downloadt** tabblad.)
2. Pak Hallo HDInsight SDK tooa map op de machine Hallo met .NET Framework 4 geïnstalleerd en toohello Internet verbonden voor het downloaden van de vereiste afhankelijkheid NuGet-pakketten. Hieronder, gaan we ervan uit dat de broncode Hallo uitgepakte tooC:\SDK is.
3. Ga toohello map C:\SDK\src\Microsoft.Hadoop.Avro.Tools en build.bat uitvoeren. (Hallo bestandsaanroepen MSBuild van Hallo 32-bits distributie van Hallo .NET Framework. Indien toouse Hallo 64-bits versie gewenst, bewerk build.bat, Hallo opmerkingen in Hallo-bestand te volgen.) Zorg ervoor dat Hallo build geslaagd. (Op sommige systemen MSBuild kan leiden tot waarschuwingen. Deze waarschuwingen hebben geen invloed op Hallo hulpprogramma, zolang er geen fouten build zijn.)
4. Hallo gecompileerd hulpprogramma bevindt zich in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget bekend bent met de opdrachtregelsyntaxis Hallo Hallo volgende opdracht uit Hallo map bevindt Hallo code generatie hulpprogramma uitvoeren:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

tootest hello hulpprogramma, kunt u C#-klassen genereren van het Hallo JSON-schema voorbeeldbestand Hallo broncode voorzien. Hallo volgende opdracht uitvoeren:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Dit moet tooproduce twee C#-bestanden in de huidige map Hallo: SensorData.cs en Location.cs.

toounderstand hello logica die Hallo code generatie hulpprogramma wordt gebruikt tijdens het converteren van typen tooC # Hallo JSON-schema, Zie Hallo bestand GenerationVerification.feature in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Naamruimten worden opgehaald uit Hallo-JSON-schema met behulp van Hallo logica in factoren in de vorige alinea Hallo Hallo-bestand. Naamruimten die worden opgehaald uit Hallo schema hebben voorrang op wat wordt geleverd bij Hallo/n parameter in opdrachtregel Hallo-hulpprogramma. Als u toooverride Hallo naamruimten die zich in het Hallo-schema wilt, gebruikt u Hallo /nf parameter. Bijvoorbeeld toochange alle naamruimten van Hallo SampleJSONSchema.avsc toomy.own.nspace, uitvoeren Hallo volgende opdracht:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Over het Hallo-voorbeelden
Zes voorbeelden vindt u in dit onderwerp ziet u verschillende scenario's die worden ondersteund door Hallo Microsoft Avro Library. Hallo Microsoft Avro Library is ontworpen toowork met elke andere stroom. In deze voorbeelden wordt gegevens gemanipuleerd via geheugen gegevensstromen in plaats van bestand streams of databases voor eenvoud en consistentie. Hallo aanpak in een productieomgeving, is afhankelijk van de exacte scenariovereisten hello, gegevensbron en volume, prestaties beperkingen en andere factoren.

eerste twee voorbeelden kunt u zien hoe Hallo tooserialize en gegevens in geheugenbuffers stroom deserialiseren via reflectie en algemene records. Hallo schema in beide gevallen wordt aangenomen dat toobe gedeeld tussen hello en schrijfprogramma out-of-band.

Hallo derde en vierde voorbeelden kunt u zien hoe tooserialize en deserialiseren van gegevens met behulp van Hallo Avro object containerbestanden. Wanneer gegevens worden opgeslagen in een Avro-container-bestand, wordt het schema is altijd met het opgeslagen omdat Hallo schema moet worden gedeeld voor deserialisatie.

Hallo voorbeeld waarin Hallo eerste vier voorbeelden kunnen worden gedownload vanuit Hallo <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure codevoorbeelden</a> site.

Hallo vijfde voorbeeld ziet u hoe een aangepaste compressiecodec voor Avro toouse containerbestanden object. Een voorbeeld van een met Hallo-code voor dit voorbeeld kan worden gedownload vanaf Hallo <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure codevoorbeelden</a> site.

Hallo zesde voorbeeld toont hoe toouse Avro serialisatie tooupload gegevens tooAzure Blob storage en vervolgens te analyseren met behulp van Hive met een HDInsight (Hadoop)-cluster. Het kan worden gedownload vanaf Hallo <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure codevoorbeelden</a> site.

Hier vindt u koppelingen toohello zes voorbeelden in Hallo onderwerp besproken:

* <a href="#Scenario1">**Serialisatie met reflectie** </a> -Hallo JSON-schema voor typen toobe geserialiseerd automatisch gebouwd van Hallo gegevens contract kenmerken.
* <a href="#Scenario2">**Serialisatie met algemene record** </a> -Hallo JSON-schema is expliciet worden opgegeven in een record wanneer er geen .NET-type beschikbaar voor reflectie is.
* <a href="#Scenario3">**Gebruik van object containerbestanden met reflectie serialisatie** </a> -Hallo JSON-schema automatisch is gemaakt en gedeeld samen met de Hallo geserialiseerd gegevens via een Avro-object container-bestand.
* <a href="#Scenario4">**Serialisatie in object containerbestanden met algemene record** </a> -Hallo JSON-schema expliciet is opgegeven voordat Hallo serialisatie en gedeeld samen met de Hallo gegevens via een Avro-object container-bestand.
* <a href="#Scenario5">**Gebruik van object containerbestanden met een aangepaste compressiecodec serialisatie** </a> -Hallo voorbeeld ziet u hoe een Avro toocreate containerbestand met een aangepaste .NET-implementatie van Hallo Deflate gegevens compressiecodec object.
* <a href="#Scenario6">**Met behulp van Avro tooupload gegevens voor Microsoft Azure HDInsight-service Hallo** </a> -Hallo voorbeeld ziet u hoe de Avro-serialisatie samenwerkt met Hallo HDInsight-service. Een actief Azure-abonnement en toegang tooan Azure HDInsight-cluster vereist toorun in dit voorbeeld.

## <a name="Scenario1"></a>Voorbeeld 1: Serialisatie met reflectie
Hallo JSON-schema voor Hallo-typen kan worden automatisch gebouwd door Hallo Microsoft Avro Library via reflectie uit Hallo gegevens contract kenmerken van Hallo C#-objecten toobe geserialiseerd. Hallo Microsoft Avro Library maakt een [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify Hallo velden toobe geserialiseerd.

In dit voorbeeld objecten (een **SensorData** klasse met een lid **locatie** struct) geserialiseerde tooa geheugenstroom zijn en deze stroom op zijn beurt wordt gedeserialiseerd. Hallo resultaat wordt vervolgens vergeleken toohello in eerste instantie tooconfirm die Hallo **SensorData** hersteld-object is identiek toohello oorspronkelijke.

Hallo-schema in dit voorbeeld wordt uitgegaan van toobe gedeeld tussen hello en schrijfprogramma, dus containerindeling van Hallo Avro-object niet vereist is. Voor een voorbeeld van hoe tooserialize en deserialiseren van gegevens in geheugenbuffers via reflectie met containerindeling Hallo-object als Hallo schema moet worden gedeeld met Hallo gegevens, Zie <a href="#Scenario3">serialisatie in object containerbestanden met reflectie</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Voorbeeld 2: Serialisatie met algemene record
Een JSON-schema kan expliciet worden opgegeven in een algemene record wanneer reflectie kan niet worden gebruikt omdat het Hallo-gegevens via .NET-klassen met een gegevenscontract kan niet worden weergegeven. Deze methode is langzamer dan met behulp van reflectie. In dergelijke gevallen kan Hallo-schema voor Hallo gegevens ook worden dynamisch is, dat wil zeggen, niet bekend bij het compileren. Gegevens weergegeven als door komma's gescheiden waarden (CSV)-bestanden waarvan het schema onbekend is totdat deze is omgezet toohello Avro-indeling tijdens de uitvoering is een voorbeeld van dit soort dynamische scenario.

Dit voorbeeld ziet u hoe toocreate en gebruik een [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly Geef een JSON-schema, hoe toopopulate met Hallo gegevens en vervolgens het tooserialize en te deserialiseren. Hallo resultaat wordt vervolgens vergeleken toohello initiële exemplaar tooconfirm die record hersteld Hallo identieke toohello oorspronkelijke is.

Hallo-schema in dit voorbeeld wordt uitgegaan van toobe gedeeld tussen hello en schrijfprogramma, dus containerindeling van Hallo Avro-object niet vereist is. Voor een voorbeeld van hoe tooserialize en deserialiseren van gegevens in geheugenbuffers met behulp van een algemene record met Hallo object containerindeling wanneer Hallo schema toegevoegd aan gegevens Hallo geserialiseerd worden moet, Zie Hallo <a href="#Scenario4">serialisatie met objectcontainer bestanden met algemene record</a> voorbeeld.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Voorbeeld 3: Serialisatie object containerbestanden en serialisatie gebruiken met reflectie
In dit voorbeeld is vergelijkbaar toohello scenario in Hallo <a href="#Scenario1"> eerste voorbeeld</a>, waarbij Hallo schema impliciet met reflectie is opgegeven. Hallo verschil is dat u hier Hallo-schema niet bekend toohello lezer die deze deserializes toobe wordt verondersteld. Hallo **SensorData** objecten toobe geserialiseerd en hun impliciet opgegeven schema worden opgeslagen in een Avro-object container-bestand dat wordt vertegenwoordigd door Hallo [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) de klasse.

Hallo-gegevens is geserialiseerd in dit voorbeeld met [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) en gedeserialiseerd met [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). Hallo resultaat wordt vergeleken toohello initiële exemplaren tooensure identiteit.

Hallo in Hallo gegevensobject containerbestand is gecomprimeerd via Hallo standaard [ **Deflate** ] [ deflate-100] compressiecodec van .NET Framework 4. Zie Hallo <a href="#Scenario5"> vijfde voorbeeld</a> in dit onderwerp toolearn hoe toouse een meer recente en hogere versie van Hallo [ **Deflate** ] [ deflate-110] compressie de codec is beschikbaar in .NET Framework 4.5.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Voorbeeld 4: Serialisatie object containerbestanden en serialisatie gebruiken met algemene record
In dit voorbeeld is vergelijkbaar toohello scenario in Hallo <a href="#Scenario2"> tweede voorbeeld</a>, waarbij Hallo schema expliciet is opgegeven met JSON. Hallo verschil is dat u hier Hallo-schema niet bekend toohello lezer die deze deserializes toobe wordt verondersteld.

Hallo testset gegevens verzameld in een lijst met [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objecten via een expliciet gedefinieerde JSON-schema en vervolgens wordt opgeslagen in een container-bestand van het object dat wordt vertegenwoordigd door Hallo [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) klasse. Dit containerbestand maakt een writer is gebruikte tooserialize Hallo gegevens, decomprimeren tooa geheugenstroom die wordt vervolgens tooa bestand opgeslagen. Hallo [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter die wordt gebruikt voor het maken van de lezer Hallo geeft aan dat deze gegevens niet worden gecomprimeerd.

Hallo-gegevens worden vervolgens lezen uit het Hallo-bestand en gedeserialiseerd tot een verzameling van objecten. Deze verzameling is de initiële lijst vergeleken toohello van Avro records tooconfirm dat ze identiek zijn.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Voorbeeld 5: Serialisatie object container-bestanden gebruiken in een aangepaste compressiecodec
Hallo vijfde voorbeeld ziet u hoe een aangepaste compressiecodec voor Avro toouse containerbestanden object. Een voorbeeld van een met Hallo-code voor dit voorbeeld kan worden gedownload vanaf Hallo [Azure codevoorbeelden](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.

Hallo [Avro-specificatie](http://avro.apache.org/docs/current/spec.html#Required+Codecs) kunt u informatie over het gebruik van een optionele compressiecodec (bovendien te**Null** en **Deflate** standaardwaarden). In dit voorbeeld wordt een nieuwe codec zoals Snappy niet implementeren (vermeld als een ondersteunde optionele codec in Hallo [Avro-specificatie](http://avro.apache.org/docs/current/spec.html#snappy)). Er wordt weergegeven hoe toouse .NET Framework 4.5-implementatie van Hallo Hallo [ **Deflate** ] [ deflate-110] codec een betere compressiealgoritme op basis van Hallo biedt[zlib](http://zlib.net/) compressiebibliotheek dan Hallo standaard .NET Framework 4-versie.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Voorbeeld 6: Met behulp van Avro tooupload gegevens voor Hallo Microsoft Azure HDInsight-service
Hallo zesde voorbeeld ziet u enkele programming technieken gerelateerde toointeracting met hello Azure HDInsight-service. Een voorbeeld van een met Hallo-code voor dit voorbeeld kan worden gedownload vanaf Hallo [Azure codevoorbeelden](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.

Hallo voorbeeld Hallo volgende taken:

* Maakt verbinding tooan bestaand HDInsight-service-cluster.
* Meerdere CSV-bestanden serialiseert en uploadt Hallo resultaat tooAzure Blob-opslag. (Hallo CSV-bestanden samen met de Hallo voorbeeld zijn gedistribueerd en vertegenwoordigen een uitpakken uit bijlage aandelen historische gegevens worden verspreid door [Infochimps](http://www.infochimps.com/) Hallo gedurende 1970 2010. Hallo voorbeeld leest gegevens uit een CSV-bestand, converteert Hallo records tooinstances Hallo **Stock** klasse en serialiseert u ze via reflectie. Voorraad typedefinitie wordt gemaakt van een JSON-schema via Hallo Microsoft Avro Library code generatie hulpprogramma.
* Maakt een nieuwe externe tabel aangeroepen **voorraden** in Hive, en koppelt u deze toohello gegevens geüpload in de vorige stap Hallo.
* Een query uitvoert met behulp van Hive via Hallo **voorraden** tabel.

Hallo voorbeeld voert bovendien een procedure opschonen voor en na het uitvoeren van belangrijke bewerkingen. Tijdens het Hallo opschonen, alle Hallo betrekking Azure Blob-gegevens en mappen worden verwijderd en Hallo Hive-tabel is verwijderd. U kunt ook Hallo opschonen procedure vanaf Hallo voorbeeldopdrachtregel aanroepen.

Hallo voorbeeld heeft Hallo volgende vereisten:

* Een actief Microsoft Azure-abonnement en de abonnement-ID.
* Een beheercertificaat voor Hallo-abonnement met de bijbehorende persoonlijke sleutel Hallo. Hallo-certificaat moet worden geïnstalleerd in Hallo huidige gebruiker persoonlijke opslag op Hallo gebruikt machine toorun Hallo voorbeeld.
* Een actief HDInsight-cluster.
* Een Azure Storage-account gekoppeld toohello HDInsight-cluster van de vorige vereiste Hallo samen met de Hallo bijbehorende primaire of secundaire toegangssleutel.

Alle informatie Hallo van Hallo vereisten moet worden ingevoerd toohello voorbeeldconfiguratiebestand voordat Hallo voorbeeld wordt uitgevoerd. Er zijn twee manieren toodo het:

* Hallo app.config-bestand in de hoofdmap Hallo-voorbeeld bewerken en vervolgens Hallo-voorbeeld
* Hallo voorbeeld eerst te bouwen en bewerk vervolgens AvroHDISample.exe.config in Hallo build directory

In beide gevallen moeten alle bewerkingen worden uitgevoerd in Hallo  **<appSettings>**  gedeelte instellingen. Ga als volgt Hallo opmerkingen in Hallo-bestand.
Hallo wordt voorbeeld uitgevoerd vanaf de opdrachtregel Hallo door het uitvoeren van de volgende opdracht (waarbij hello ZIP-bestand met Hallo voorbeeld wordt uitgegaan van een toobe uitgepakt tooC:\AvroHDISample; als anders gebruik Hallo relevante bestandspad) Hallo:

    AvroHDISample run C:\AvroHDISample\Data

tooclean Hallo-cluster, Hallo volgende opdracht uitvoeren:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
