---
title: aaaUse C# met Hive en Pig met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse C# gebruiker gedefinieerde functies (UDF) met Hive en Pig streaming in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>C# gebruiker gedefinieerde functies gebruiken met Hive en Pig streaming van Hadoop in HDInsight

Meer informatie over hoe toouse C# gebruiker functies (UDF) met Apache Hive en Pig gedefinieerd op HDInsight.

> [!IMPORTANT]
> Hallo stappen in dit document met HDInsight-clusters op basis van Linux en Windows-werken. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).

Beide Hive en Pig tooexternal gegevenstoepassingen voor verwerking kunt doorgeven. Dit proces wordt ook wel _streaming_. Wanneer u een .NET registratieaanvraag ligt, Hallo gegevens worden doorgevoerd toohello toepassing STDIN en Hallo toepassing hello resultaten weer die op STDOUT. tooread en write van STDIN en STDOUT, kunt u `Console.ReadLine()` en `Console.WriteLine()` vanuit een consoletoepassing.

## <a name="prerequisites"></a>Vereisten

* U moet bekend zijn met schrijven en het bouwen van C#-code die gericht is op .NET Framework 4.5.

    * Ongeacht IDE die u wilt gebruiken. Het is raadzaam [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, of [Visual Studio Code](https://code.visualstudio.com/). Hallo stappen in dit document Visual Studio 2017.

* Een manier tooupload .exe-bestanden toohello cluster en Pig en Hive-taken uitvoeren. Beter Hallo Data Lake Tools voor Visual Studio, Azure PowerShell en Azure CLI. Hallo stappen in dit document gebruiken Hallo Data Lake Tools voor Visual Studio tooupload Hallo bestanden en Voer Hallo voorbeeld Hive-query.

    Zie voor informatie over andere manieren toorun Hive-query's en Pig-taken, Hallo documenten te volgen:

    * [Apache Hive gebruiken met HDInsight](hdinsight-use-hive.md)

    * [Apache Pig gebruiken met HDInsight](hdinsight-use-pig.md)

* Een Hadoop op HDInsight-cluster. Zie voor meer informatie over het maken van een cluster [maken van een HDInsight-cluster](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET in HDInsight

* __HDInsight op basis van Linux__ opslagclusters die gebruikmaken van [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET-toepassingen. Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5.

    Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse een specifieke versie van Mono, Zie Hallo [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.

* __HDInsight op basis van Windows__ clusters Hallo Microsoft .NET CLR toorun .NET-toepassingen gebruiken.

Zie voor meer informatie over Hallo-versie van Hallo .NET framework en Mono opgenomen met versies van HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Hallo C maken\# projecten

### <a name="hive-udf"></a>Hive UDF

1. Open Visual Studio en maak een oplossing. Selecteer Hallo projecttype **Console-App (.NET Framework)**, en de naam van Hallo nieuw project **HiveCSharp**.

    > [!IMPORTANT]
    > Selecteer __.NET Framework 4.5__ als u een Linux gebaseerde HDInsight-cluster. Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Vervang de inhoud Hallo van **Program.cs** door Hallo volgende:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Hallo-project maken.

### <a name="pig-udf"></a>Pig UDF

1. Open Visual Studio en maak een oplossing. Selecteer Hallo projecttype **consoletoepassing**, en de naam van Hallo nieuw project **PigUDF**.

2. Vervang de inhoud Hallo Hallo **Program.cs** bestand met de volgende code Hallo:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Deze toepassing hello regels die zijn verzonden vanaf de Pig en herformatteren regels die beginnen met parseert `java.lang.Exception`.

3. Sla **Program.cs**, en vervolgens Hallo-project te bouwen.

## <a name="upload-toostorage"></a>Toostorage uploaden

1. Open in Visual Studio **Server Explorer**.

2. Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.

3. Als u wordt gevraagd, Voer uw referenties in Azure-abonnement en klik vervolgens op **aanmelden**.

4. Hallo HDInsight-cluster dat u deze toepassing toodeploy wilt uitbreiden. Een item met de tekst hello __(Default Storage Account)__ wordt vermeld.

    ![Server Explorer Hallo storage-account voor Hallo cluster weergeven](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Als dit item kan worden uitgebreid, gebruikt u een __Azure Storage-Account__ als standaard opslag voor Hallo-cluster. tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, vouw Hallo vermelding en dubbelklik vervolgens op Hallo __(standaardcontainer)__.

    * Als dit item kan niet worden uitgebreid, gebruikt u __Azure Data Lake Store__ als Hallo standaard opslag voor Hallo-cluster. tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, dubbelklikt u op Hallo __(Standaardopslagaccount)__ vermelding.

6. tooupload hello .exe-bestanden, een van de volgende methoden hello gebruiken:

    * Als u een __Azure Storage-Account__op Hallo uploaden pictogram en blader vervolgens toohello **bin\debug** map voor Hallo **HiveCSharp** project. Tot slot selecteert Hallo **HiveCSharp.exe** -bestand en klik op **Ok**.

        ![pictogram uploaden](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Als u __Azure Data Lake Store__, met de rechtermuisknop op een leeg gebied in Hallo bestand aanbieding en selecteer vervolgens __uploaden__. Tot slot selecteert Hallo **HiveCSharp.exe** -bestand en klik op **Open**.

    Eenmaal Hallo __HiveCSharp.exe__ uploaden is voltooid, herhaalt Hallo uploadproces voor Hallo __PigUDF.exe__ bestand.

## <a name="run-a-hive-query"></a>Een Hive-query uitvoeren

1. Open in Visual Studio **Server Explorer**.

2. Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.

3. Klik met de rechtermuisknop Hallo cluster die u hebt geïmplementeerd Hallo **HiveCSharp** naar een toepassing en selecteer vervolgens **een Hive-Query schrijven**.

4. Gebruik Hallo tekst voor Hallo Hive-query te volgen:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Verwijder de opmerkingen in Hallo `add file` instructie die overeenkomt met de Hallo type standaard opslag gebruikt voor uw cluster.

    Deze query selecteert Hallo `clientid`, `devicemake`, en `devicemodel` velden uit `hivesampletable`, en worden de velden Hallo toohello HiveCSharp.exe toepassing. Hallo-query verwacht Hallo toepassing tooreturn drie velden die worden opgeslagen als `clientid`, `phoneLabel`, en `phoneHash`. Hallo-query verwacht ook toofind HiveCSharp.exe in de hoofdmap Hallo van Hallo standaard storage-container.

5. Klik op **indienen** toosubmit Hallo taak toohello HDInsight-cluster. Hallo **taakoverzicht Hive** venster wordt geopend.

6. Klik op **vernieuwen** toorefresh Hallo samenvatting tot **taakstatus** wijzigingen te**voltooid**. tooview hello taak uitvoert, klikt u op **Taakuitvoer**.

## <a name="run-a-pig-job"></a>Pig-taak uitgevoerd

1. Gebruik een van de Hallo methoden tooconnect tooyour HDInsight-cluster te volgen:

    * Als u een __op basis van Linux__ HDInsight-cluster, SSH gebruiken. Bijvoorbeeld `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Zie voor meer informatie [SSH gebruiken withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * Als u een __Windows gebaseerde__ HDInsight-cluster, [Connect toohello cluster met behulp van extern bureaublad](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Gebruik één Hallo opdracht toostart Hallo Pig vanaf de opdrachtregel te volgen:

        pig

    > [!IMPORTANT]
    > Als u van een cluster met Windows gebruikmaakt, gebruikt u Hallo volgende opdrachten in plaats daarvan:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    Een `grunt>` prompt wordt weergegeven.

3. Voer Hallo toorun een Pig-taak die gebruikmaakt van .NET Framework-toepassing hello te volgen:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Hallo `DEFINE` instructie maakt u een alias van `streamer` voor Hallo pigudf.exe toepassingen en `CACHE` geladen uit opslag voor Hallo cluster standaard. Later, `streamer` wordt gebruikt met Hallo `STREAM` operator tooprocess Hallo één regels in het logboek- en return Hallo als een reeks kolommen.

    > [!NOTE]
    > Hallo toepassingsnaam die wordt gebruikt voor streaming moet worden omgeven door Hallo \` (backtick) teken als alias, en ' (enkel aanhalingsteken) gebruikt in combinatie met `SHIP`.

4. Na het invoeren van de laatste regel Hallo Hallo-taak moet worden gestart. Deze retourneert uitvoer vergelijkbare toohello volgende tekst:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Volgende stappen

In dit document hebt u geleerd hoe toouse een .NET Framework-toepassing via Hive en Pig op HDInsight. Als u wilt toolearn hoe toouse Python met Hive en Pig, Zie [gebruik Python met Hive en Pig in HDInsight](hdinsight-python.md).

Zie voor andere manieren toouse Pig en Hive en toolearn over het gebruik van MapReduce, Hallo documenten te volgen:

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)
