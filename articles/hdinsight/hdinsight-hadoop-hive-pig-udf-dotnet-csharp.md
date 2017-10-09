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
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="4f633-103">C# gebruiker gedefinieerde functies gebruiken met Hive en Pig streaming van Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="4f633-104">Meer informatie over hoe toouse C# gebruiker functies (UDF) met Apache Hive en Pig gedefinieerd op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f633-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f633-105">Hallo stappen in dit document met HDInsight-clusters op basis van Linux en Windows-werken.</span><span class="sxs-lookup"><span data-stu-id="4f633-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4f633-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4f633-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4f633-107">Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f633-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="4f633-108">Beide Hive en Pig tooexternal gegevenstoepassingen voor verwerking kunt doorgeven.</span><span class="sxs-lookup"><span data-stu-id="4f633-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="4f633-109">Dit proces wordt ook wel _streaming_.</span><span class="sxs-lookup"><span data-stu-id="4f633-109">This process is known as _streaming_.</span></span> <span data-ttu-id="4f633-110">Wanneer u een .NET registratieaanvraag ligt, Hallo gegevens worden doorgevoerd toohello toepassing STDIN en Hallo toepassing hello resultaten weer die op STDOUT.</span><span class="sxs-lookup"><span data-stu-id="4f633-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="4f633-111">tooread en write van STDIN en STDOUT, kunt u `Console.ReadLine()` en `Console.WriteLine()` vanuit een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="4f633-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f633-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4f633-112">Prerequisites</span></span>

* <span data-ttu-id="4f633-113">U moet bekend zijn met schrijven en het bouwen van C#-code die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4f633-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="4f633-114">Ongeacht IDE die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4f633-114">Use whatever IDE you want.</span></span> <span data-ttu-id="4f633-115">Het is raadzaam [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, of [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="4f633-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="4f633-116">Hallo stappen in dit document Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4f633-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="4f633-117">Een manier tooupload .exe-bestanden toohello cluster en Pig en Hive-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4f633-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="4f633-118">Beter Hallo Data Lake Tools voor Visual Studio, Azure PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4f633-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="4f633-119">Hallo stappen in dit document gebruiken Hallo Data Lake Tools voor Visual Studio tooupload Hallo bestanden en Voer Hallo voorbeeld Hive-query.</span><span class="sxs-lookup"><span data-stu-id="4f633-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="4f633-120">Zie voor informatie over andere manieren toorun Hive-query's en Pig-taken, Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f633-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="4f633-121">Apache Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="4f633-122">Apache Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="4f633-123">Een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4f633-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="4f633-124">Zie voor meer informatie over het maken van een cluster [maken van een HDInsight-cluster](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4f633-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="4f633-125">.NET in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-125">.NET on HDInsight</span></span>

* <span data-ttu-id="4f633-126">__HDInsight op basis van Linux__ opslagclusters die gebruikmaken van [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="4f633-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="4f633-127">Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5.</span><span class="sxs-lookup"><span data-stu-id="4f633-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="4f633-128">Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="4f633-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="4f633-129">toouse een specifieke versie van Mono, Zie Hallo [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="4f633-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="4f633-130">__HDInsight op basis van Windows__ clusters Hallo Microsoft .NET CLR toorun .NET-toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4f633-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="4f633-131">Zie voor meer informatie over Hallo-versie van Hallo .NET framework en Mono opgenomen met versies van HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f633-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="4f633-132">Hallo C maken\# projecten</span><span class="sxs-lookup"><span data-stu-id="4f633-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="4f633-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="4f633-133">Hive UDF</span></span>

1. <span data-ttu-id="4f633-134">Open Visual Studio en maak een oplossing.</span><span class="sxs-lookup"><span data-stu-id="4f633-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="4f633-135">Selecteer Hallo projecttype **Console-App (.NET Framework)**, en de naam van Hallo nieuw project **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="4f633-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4f633-136">Selecteer __.NET Framework 4.5__ als u een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4f633-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4f633-137">Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="4f633-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="4f633-138">Vervang de inhoud Hallo van **Program.cs** door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4f633-138">Replace hello contents of **Program.cs** with hello following:</span></span>

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

3. <span data-ttu-id="4f633-139">Hallo-project maken.</span><span class="sxs-lookup"><span data-stu-id="4f633-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="4f633-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="4f633-140">Pig UDF</span></span>

1. <span data-ttu-id="4f633-141">Open Visual Studio en maak een oplossing.</span><span class="sxs-lookup"><span data-stu-id="4f633-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="4f633-142">Selecteer Hallo projecttype **consoletoepassing**, en de naam van Hallo nieuw project **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="4f633-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="4f633-143">Vervang de inhoud Hallo Hallo **Program.cs** bestand met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="4f633-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

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

    <span data-ttu-id="4f633-144">Deze toepassing hello regels die zijn verzonden vanaf de Pig en herformatteren regels die beginnen met parseert `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="4f633-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="4f633-145">Sla **Program.cs**, en vervolgens Hallo-project te bouwen.</span><span class="sxs-lookup"><span data-stu-id="4f633-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="4f633-146">Toostorage uploaden</span><span class="sxs-lookup"><span data-stu-id="4f633-146">Upload toostorage</span></span>

1. <span data-ttu-id="4f633-147">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4f633-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="4f633-148">Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.</span><span class="sxs-lookup"><span data-stu-id="4f633-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="4f633-149">Als u wordt gevraagd, Voer uw referenties in Azure-abonnement en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="4f633-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="4f633-150">Hallo HDInsight-cluster dat u deze toepassing toodeploy wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="4f633-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="4f633-151">Een item met de tekst hello __(Default Storage Account)__ wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="4f633-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Server Explorer Hallo storage-account voor Hallo cluster weergeven](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="4f633-153">Als dit item kan worden uitgebreid, gebruikt u een __Azure Storage-Account__ als standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4f633-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="4f633-154">tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, vouw Hallo vermelding en dubbelklik vervolgens op Hallo __(standaardcontainer)__.</span><span class="sxs-lookup"><span data-stu-id="4f633-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="4f633-155">Als dit item kan niet worden uitgebreid, gebruikt u __Azure Data Lake Store__ als Hallo standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4f633-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="4f633-156">tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, dubbelklikt u op Hallo __(Standaardopslagaccount)__ vermelding.</span><span class="sxs-lookup"><span data-stu-id="4f633-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="4f633-157">tooupload hello .exe-bestanden, een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4f633-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="4f633-158">Als u een __Azure Storage-Account__op Hallo uploaden pictogram en blader vervolgens toohello **bin\debug** map voor Hallo **HiveCSharp** project.</span><span class="sxs-lookup"><span data-stu-id="4f633-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="4f633-159">Tot slot selecteert Hallo **HiveCSharp.exe** -bestand en klik op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="4f633-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![pictogram uploaden](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="4f633-161">Als u __Azure Data Lake Store__, met de rechtermuisknop op een leeg gebied in Hallo bestand aanbieding en selecteer vervolgens __uploaden__.</span><span class="sxs-lookup"><span data-stu-id="4f633-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="4f633-162">Tot slot selecteert Hallo **HiveCSharp.exe** -bestand en klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="4f633-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="4f633-163">Eenmaal Hallo __HiveCSharp.exe__ uploaden is voltooid, herhaalt Hallo uploadproces voor Hallo __PigUDF.exe__ bestand.</span><span class="sxs-lookup"><span data-stu-id="4f633-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="4f633-164">Een Hive-query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4f633-164">Run a Hive query</span></span>

1. <span data-ttu-id="4f633-165">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4f633-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="4f633-166">Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.</span><span class="sxs-lookup"><span data-stu-id="4f633-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="4f633-167">Klik met de rechtermuisknop Hallo cluster die u hebt geïmplementeerd Hallo **HiveCSharp** naar een toepassing en selecteer vervolgens **een Hive-Query schrijven**.</span><span class="sxs-lookup"><span data-stu-id="4f633-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="4f633-168">Gebruik Hallo tekst voor Hallo Hive-query te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f633-168">Use hello following text for hello Hive query:</span></span>

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
    > <span data-ttu-id="4f633-169">Verwijder de opmerkingen in Hallo `add file` instructie die overeenkomt met de Hallo type standaard opslag gebruikt voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="4f633-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="4f633-170">Deze query selecteert Hallo `clientid`, `devicemake`, en `devicemodel` velden uit `hivesampletable`, en worden de velden Hallo toohello HiveCSharp.exe toepassing.</span><span class="sxs-lookup"><span data-stu-id="4f633-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="4f633-171">Hallo-query verwacht Hallo toepassing tooreturn drie velden die worden opgeslagen als `clientid`, `phoneLabel`, en `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="4f633-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="4f633-172">Hallo-query verwacht ook toofind HiveCSharp.exe in de hoofdmap Hallo van Hallo standaard storage-container.</span><span class="sxs-lookup"><span data-stu-id="4f633-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="4f633-173">Klik op **indienen** toosubmit Hallo taak toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4f633-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="4f633-174">Hallo **taakoverzicht Hive** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4f633-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="4f633-175">Klik op **vernieuwen** toorefresh Hallo samenvatting tot **taakstatus** wijzigingen te**voltooid**.</span><span class="sxs-lookup"><span data-stu-id="4f633-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="4f633-176">tooview hello taak uitvoert, klikt u op **Taakuitvoer**.</span><span class="sxs-lookup"><span data-stu-id="4f633-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="4f633-177">Pig-taak uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="4f633-177">Run a Pig job</span></span>

1. <span data-ttu-id="4f633-178">Gebruik een van de Hallo methoden tooconnect tooyour HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f633-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="4f633-179">Als u een __op basis van Linux__ HDInsight-cluster, SSH gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4f633-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="4f633-180">Bijvoorbeeld `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="4f633-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="4f633-181">Zie voor meer informatie [SSH gebruiken withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="4f633-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="4f633-182">Als u een __Windows gebaseerde__ HDInsight-cluster, [Connect toohello cluster met behulp van extern bureaublad](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="4f633-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="4f633-183">Gebruik één Hallo opdracht toostart Hallo Pig vanaf de opdrachtregel te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f633-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="4f633-184">Als u van een cluster met Windows gebruikmaakt, gebruikt u Hallo volgende opdrachten in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="4f633-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="4f633-185">Een `grunt>` prompt wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4f633-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="4f633-186">Voer Hallo toorun een Pig-taak die gebruikmaakt van .NET Framework-toepassing hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f633-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="4f633-187">Hallo `DEFINE` instructie maakt u een alias van `streamer` voor Hallo pigudf.exe toepassingen en `CACHE` geladen uit opslag voor Hallo cluster standaard.</span><span class="sxs-lookup"><span data-stu-id="4f633-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="4f633-188">Later, `streamer` wordt gebruikt met Hallo `STREAM` operator tooprocess Hallo één regels in het logboek- en return Hallo als een reeks kolommen.</span><span class="sxs-lookup"><span data-stu-id="4f633-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4f633-189">Hallo toepassingsnaam die wordt gebruikt voor streaming moet worden omgeven door Hallo \` (backtick) teken als alias, en ' (enkel aanhalingsteken) gebruikt in combinatie met `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="4f633-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="4f633-190">Na het invoeren van de laatste regel Hallo Hallo-taak moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="4f633-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="4f633-191">Deze retourneert uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4f633-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="4f633-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f633-192">Next steps</span></span>

<span data-ttu-id="4f633-193">In dit document hebt u geleerd hoe toouse een .NET Framework-toepassing via Hive en Pig op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f633-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="4f633-194">Als u wilt toolearn hoe toouse Python met Hive en Pig, Zie [gebruik Python met Hive en Pig in HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="4f633-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="4f633-195">Zie voor andere manieren toouse Pig en Hive en toolearn over het gebruik van MapReduce, Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f633-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="4f633-196">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4f633-197">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4f633-198">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f633-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
