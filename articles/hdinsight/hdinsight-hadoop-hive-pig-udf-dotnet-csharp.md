---
title: Gebruik C# met Hive en Pig met Hadoop in HDInsight - Azure | Microsoft Docs
description: Informatie over het gebruik van C# gebruiker gedefinieerde functies (UDF) met Hive en Pig streaming in Azure HDInsight.
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
ms.openlocfilehash: 58e7af47be71c3e0389e5fb4641e124eb648494e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="fa455-103">C# gebruiker gedefinieerde functies gebruiken met Hive en Pig streaming van Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="fa455-104">Informatie over het gebruik van C# gebruiker gedefinieerde functies (UDF) met Apache Hive en Pig op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa455-104">Learn how to use C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa455-105">De stappen in dit document werken met op basis van Linux en Windows-HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="fa455-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="fa455-106">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="fa455-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fa455-107">Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="fa455-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="fa455-108">Beide Hive en Pig gegevens kan doorgeven bij externe toepassingen voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="fa455-108">Both Hive and Pig can pass data to external applications for processing.</span></span> <span data-ttu-id="fa455-109">Dit proces wordt ook wel _streaming_.</span><span class="sxs-lookup"><span data-stu-id="fa455-109">This process is known as _streaming_.</span></span> <span data-ttu-id="fa455-110">Wanneer u een .NET registratieaanvraag ligt, de gegevens op STDIN wordt doorgegeven aan de toepassing en de toepassing de resultaten weer die op STDOUT.</span><span class="sxs-lookup"><span data-stu-id="fa455-110">When using a .NET applciation, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span></span> <span data-ttu-id="fa455-111">U kunt gebruiken om te lezen en schrijven op STDIN en STDOUT, `Console.ReadLine()` en `Console.WriteLine()` vanuit een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="fa455-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa455-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fa455-112">Prerequisites</span></span>

* <span data-ttu-id="fa455-113">U moet bekend zijn met schrijven en het bouwen van C#-code die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="fa455-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="fa455-114">Ongeacht IDE die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa455-114">Use whatever IDE you want.</span></span> <span data-ttu-id="fa455-115">Het is raadzaam [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, of [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fa455-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="fa455-116">De stappen in dit document gebruikt u Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fa455-116">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="fa455-117">Een manier .exe-bestanden uploaden naar het cluster en Pig en Hive-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fa455-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="fa455-118">Beter Data Lake Tools voor Visual Studio, Azure PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fa455-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="fa455-119">De stappen in dit document Data Lake Tools voor Visual Studio voor het uploaden van de bestanden en het voorbeeld uitvoert Hive-query.</span><span class="sxs-lookup"><span data-stu-id="fa455-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span></span>

    <span data-ttu-id="fa455-120">Hive-query's en Pig-taken, raadpleegt u de volgende documenten voor meer informatie over andere manieren om uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="fa455-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span></span>

    * [<span data-ttu-id="fa455-121">Apache Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="fa455-122">Apache Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="fa455-123">Een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="fa455-124">Zie voor meer informatie over het maken van een cluster [maken van een HDInsight-cluster](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="fa455-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="fa455-125">.NET in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-125">.NET on HDInsight</span></span>

* <span data-ttu-id="fa455-126">__HDInsight op basis van Linux__ opslagclusters die gebruikmaken van [Mono (https://mono-project.com)](https://mono-project.com) .NET-toepassingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fa455-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="fa455-127">Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5.</span><span class="sxs-lookup"><span data-stu-id="fa455-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="fa455-128">Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="fa455-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="fa455-129">Zie voor het gebruik van een specifieke versie van Mono de [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="fa455-129">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="fa455-130">__HDInsight op basis van Windows__ clusters gebruiken de Microsoft .NET CLR .NET-toepassingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fa455-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span></span>

<span data-ttu-id="fa455-131">Zie voor meer informatie over de versie van .NET framework en Mono opgenomen met versies van HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="fa455-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-the-c-projects"></a><span data-ttu-id="fa455-132">Maken van de C\# projecten</span><span class="sxs-lookup"><span data-stu-id="fa455-132">Create the C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="fa455-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="fa455-133">Hive UDF</span></span>

1. <span data-ttu-id="fa455-134">Open Visual Studio en maak een oplossing.</span><span class="sxs-lookup"><span data-stu-id="fa455-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="fa455-135">Selecteer voor het projecttype **Console-App (.NET Framework)**, en de naam van het nieuwe project **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="fa455-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fa455-136">Selecteer __.NET Framework 4.5__ als u een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="fa455-137">Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="fa455-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="fa455-138">Vervang de inhoud van **Program.cs** door het volgende:</span><span class="sxs-lookup"><span data-stu-id="fa455-138">Replace the contents of **Program.cs** with the following:</span></span>

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
                    // Parse the string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data to stdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for the given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array to hex string
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

3. <span data-ttu-id="fa455-139">Maak het project.</span><span class="sxs-lookup"><span data-stu-id="fa455-139">Build the project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="fa455-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="fa455-140">Pig UDF</span></span>

1. <span data-ttu-id="fa455-141">Open Visual Studio en maak een oplossing.</span><span class="sxs-lookup"><span data-stu-id="fa455-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="fa455-142">Selecteer voor het projecttype **consoletoepassing**, en de naam van het nieuwe project **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="fa455-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span></span>

2. <span data-ttu-id="fa455-143">Vervang de inhoud van de **Program.cs** bestand met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="fa455-143">Replace the contents of the **Program.cs** file with the following code:</span></span>

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
                        // Trim the error info off the beginning and add a note to the end of the line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split the fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="fa455-144">Deze toepassing parseert de regels die zijn verzonden vanaf Pig en herformatteren regels die beginnen met `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="fa455-144">This application parses the lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="fa455-145">Sla **Program.cs**, en vervolgens het project te bouwen.</span><span class="sxs-lookup"><span data-stu-id="fa455-145">Save **Program.cs**, and then build the project.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="fa455-146">Uploaden naar de opslag</span><span class="sxs-lookup"><span data-stu-id="fa455-146">Upload to storage</span></span>

1. <span data-ttu-id="fa455-147">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fa455-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="fa455-148">Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.</span><span class="sxs-lookup"><span data-stu-id="fa455-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="fa455-149">Als u wordt gevraagd, Voer uw referenties in Azure-abonnement en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="fa455-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="fa455-150">Vouw het HDInsight-cluster die u wilt deze toepassing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="fa455-150">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="fa455-151">Een item met de tekst __(Default Storage Account)__ wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="fa455-151">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Server Explorer met de storage-account voor het cluster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="fa455-153">Als dit item kan worden uitgebreid, gebruikt u een __Azure Storage-Account__ als standaard opslag voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="fa455-154">Als u de bestanden op de standaard-opslag voor het cluster, vouw de vermelding en dubbelklikt u vervolgens op de __(standaardcontainer)__.</span><span class="sxs-lookup"><span data-stu-id="fa455-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="fa455-155">Als dit item kan niet worden uitgebreid, gebruikt u __Azure Data Lake Store__ als de opslag van de standaard voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="fa455-156">Als u wilt weergeven van de bestanden op de standaard-opslag voor het cluster, dubbelklikt u op de __(Standaardopslagaccount)__ vermelding.</span><span class="sxs-lookup"><span data-stu-id="fa455-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="fa455-157">Als u wilt de .exe-bestanden uploaden, moet u een van de volgende methoden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fa455-157">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="fa455-158">Als u een __Azure Storage-Account__, klik op het pictogram uploaden en blader vervolgens naar de **bin\debug** map voor de **HiveCSharp** project.</span><span class="sxs-lookup"><span data-stu-id="fa455-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span></span> <span data-ttu-id="fa455-159">Tot slot selecteert u de **HiveCSharp.exe** -bestand en klik op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="fa455-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![pictogram uploaden](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="fa455-161">Als u __Azure Data Lake Store__, met de rechtermuisknop op een leeg gebied in de lijst en selecteer vervolgens __uploaden__.</span><span class="sxs-lookup"><span data-stu-id="fa455-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="fa455-162">Tot slot selecteert u de **HiveCSharp.exe** -bestand en klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="fa455-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="fa455-163">Eenmaal de __HiveCSharp.exe__ upload is voltooid, herhaalt het uploadproces voor de __PigUDF.exe__ bestand.</span><span class="sxs-lookup"><span data-stu-id="fa455-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="fa455-164">Een Hive-query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fa455-164">Run a Hive query</span></span>

1. <span data-ttu-id="fa455-165">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fa455-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="fa455-166">Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.</span><span class="sxs-lookup"><span data-stu-id="fa455-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="fa455-167">Met de rechtermuisknop op het cluster dat u hebt geïmplementeerd de **HiveCSharp** naar een toepassing en selecteer vervolgens **een Hive-Query schrijven**.</span><span class="sxs-lookup"><span data-stu-id="fa455-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="fa455-168">Gebruik de volgende tekst voor de Hive-query:</span><span class="sxs-lookup"><span data-stu-id="fa455-168">Use the following text for the Hive query:</span></span>

    ```hiveql
    -- Uncomment the following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment the following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="fa455-169">Opmerkingen bij de `add file` instructie die overeenkomt met het type standaard opslag gebruikt voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span></span>

    <span data-ttu-id="fa455-170">Deze query selecteert de `clientid`, `devicemake`, en `devicemodel` velden uit `hivesampletable`, en geeft u de velden aan de toepassing HiveCSharp.exe.</span><span class="sxs-lookup"><span data-stu-id="fa455-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span></span> <span data-ttu-id="fa455-171">De query verwacht dat de toepassing om terug te keren drie velden die worden opgeslagen als `clientid`, `phoneLabel`, en `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="fa455-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="fa455-172">De query verwacht ook HiveCSharp.exe vinden in de hoofdmap van de standaard storage-container.</span><span class="sxs-lookup"><span data-stu-id="fa455-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span></span>

5. <span data-ttu-id="fa455-173">Klik op **indienen** voor het verzenden van de taak met de HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-173">Click **Submit** to submit the job to the HDInsight cluster.</span></span> <span data-ttu-id="fa455-174">De **taakoverzicht Hive** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="fa455-174">The **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="fa455-175">Klik op **vernieuwen** vernieuwen van de samenvatting tot **taakstatus** wijzigingen in **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="fa455-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span></span> <span data-ttu-id="fa455-176">Als u wilt weergeven van de taakuitvoer **Taakuitvoer**.</span><span class="sxs-lookup"><span data-stu-id="fa455-176">To view the job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="fa455-177">Pig-taak uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="fa455-177">Run a Pig job</span></span>

1. <span data-ttu-id="fa455-178">Gebruik een van de volgende methoden om verbinding maken met uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="fa455-178">Use one of the following methods to connect to your HDInsight cluster:</span></span>

    * <span data-ttu-id="fa455-179">Als u een __op basis van Linux__ HDInsight-cluster, SSH gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa455-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="fa455-180">Bijvoorbeeld `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="fa455-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="fa455-181">Zie voor meer informatie [SSH gebruiken withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="fa455-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="fa455-182">Als u een __Windows gebaseerde__ HDInsight-cluster, [verbinding maken met het cluster met behulp van extern bureaublad](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="fa455-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="fa455-183">Gebruik een de volgende opdracht om te beginnen de Pig-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="fa455-183">Use one the following command to start the Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="fa455-184">Als u een cluster met Windows gebruikt, kunt u de volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="fa455-184">If you are using a Windows-based cluster, use the following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="fa455-185">Een `grunt>` prompt wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa455-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="fa455-186">Voer de volgende als u wilt uitvoeren van een Pig-taak die gebruikmaakt van de .NET Framework-toepassing:</span><span class="sxs-lookup"><span data-stu-id="fa455-186">Enter the following to run a Pig job that uses the .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="fa455-187">De `DEFINE` instructie maakt u een alias van `streamer` voor de toepassingen pigudf.exe en `CACHE` geladen uit opslag standaard voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="fa455-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span></span> <span data-ttu-id="fa455-188">Later, `streamer` wordt gebruikt met de `STREAM` operator voor het verwerken van de regels die zijn opgenomen in een logboek en de gegevens worden geretourneerd als een reeks kolommen.</span><span class="sxs-lookup"><span data-stu-id="fa455-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa455-189">De naam van de toepassing die wordt gebruikt voor streaming moet worden omgeven door de \` (backtick) teken als alias, en ' (enkel aanhalingsteken) gebruikt in combinatie met `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="fa455-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="fa455-190">De taak na het invoeren van de laatste regel moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="fa455-190">After entering the last line, the job should start.</span></span> <span data-ttu-id="fa455-191">Deze retourneert uitvoer vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="fa455-191">It returns output similar to the following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="fa455-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa455-192">Next steps</span></span>

<span data-ttu-id="fa455-193">In dit document hebt u geleerd hoe een toepassing .NET Framework via Hive en Pig op HDInsight gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa455-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="fa455-194">Als u meer informatie over het wilt gebruik van Python met Hive en Pig, Zie [Python gebruiken met Hive en Pig in HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="fa455-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="fa455-195">Zie de volgende documenten voor andere manieren om te gebruiken, Pig en Hive, en voor meer informatie over het gebruik van MapReduce:</span><span class="sxs-lookup"><span data-stu-id="fa455-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="fa455-196">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fa455-197">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fa455-198">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa455-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
