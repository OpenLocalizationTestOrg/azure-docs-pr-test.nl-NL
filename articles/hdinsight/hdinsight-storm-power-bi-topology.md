---
title: Apache Storm gebruiken met Power BI - Azure HDInsight | Microsoft Docs
description: Maak een Power BI-rapport met gegevens uit een C#-topologie uitgevoerd op een Apache Storm-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="02548-103">Power BI gebruiken om gegevens uit een Apache Storm-topologie te visualiseren</span><span class="sxs-lookup"><span data-stu-id="02548-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="02548-104">Power BI kunt u gegevens visueel weergeven als rapporten.</span><span class="sxs-lookup"><span data-stu-id="02548-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="02548-105">Dit document bevat een voorbeeld van hoe u Apache Storm op HDInsight gebruiken om gegevens te genereren voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="02548-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="02548-106">De stappen in dit document, is afhankelijk van een Windows-ontwikkelomgeving met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02548-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="02548-107">Het gecompileerde project kan worden verzonden naar een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02548-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="02548-108">Alleen op basis van Linux-clusters gemaakt na 28-10-2016 ondersteuning SCP.NET topologieën.</span><span class="sxs-lookup"><span data-stu-id="02548-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="02548-109">Als u wilt gebruiken een C#-topologie met een cluster op basis van Linux, werk het Microsoft.SCP.Net.SDK NuGet-pakket gebruikt door uw project naar versie 0.10.0.6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="02548-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="02548-110">De versie van het pakket moet ook overeenkomen met de primaire versie van Storm die op HDInsight is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="02548-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="02548-111">HDInsight-versies 3.3 en 3.4 gebruiken bijvoorbeeld Storm-versie 0.10.x en HDInsight 3.5 gebruikt Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="02548-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="02548-112">C#-topologieën met op Linux gebaseerde clusters moeten .NET 4.5 en Mono gebruiken om op het HDInsight-cluster te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02548-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="02548-113">De meeste dingen werken.</span><span class="sxs-lookup"><span data-stu-id="02548-113">Most things work.</span></span> <span data-ttu-id="02548-114">U moet echter controleren de [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.</span><span class="sxs-lookup"><span data-stu-id="02548-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="02548-115">Zie voor een Java-versie van dit project, met HDInsight op basis van Linux of op basis van Windows werkt, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="02548-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02548-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="02548-116">Prerequisites</span></span>

* <span data-ttu-id="02548-117">Een Azure Active Directory-gebruiker met [Power BI](https://powerbi.com) toegang.</span><span class="sxs-lookup"><span data-stu-id="02548-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="02548-118">Een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02548-118">An HDInsight cluster.</span></span> <span data-ttu-id="02548-119">Zie voor meer informatie [aan de slag met Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="02548-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="02548-120">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="02548-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="02548-121">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02548-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="02548-122">Visual Studio (een van de volgende versies)</span><span class="sxs-lookup"><span data-stu-id="02548-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="02548-123">Visual Studio 2012 met [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="02548-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="02548-124">Visual Studio 2013 met [update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="02548-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="02548-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="02548-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="02548-126">Visual Studio 2017 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="02548-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="02548-127">De HDInsight Tools voor Visual Studio: Zie [aan de slag met HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) voor meer informatie over installatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="02548-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="02548-128">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="02548-128">How it works</span></span>

<span data-ttu-id="02548-129">In dit voorbeeld bevat een C# Storm-topologie die willekeurig logboekgegevens van Internet Information Services (IIS genereert).</span><span class="sxs-lookup"><span data-stu-id="02548-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="02548-130">Deze gegevens vervolgens naar een SQL-Database is geschreven en van daaruit wordt gebruikt om rapporten te genereren in Power BI.</span><span class="sxs-lookup"><span data-stu-id="02548-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="02548-131">De volgende bestanden implementeren van de belangrijkste functionaliteit van dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="02548-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="02548-132">**SqlAzureBolt.cs**: schrijft informatie in de Storm-topologie met SQL-Database wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="02548-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="02548-133">**IISLogsTable.sql**: gebruikt voor het genereren van de database die de gegevens worden opgeslagen in de Transact-SQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="02548-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="02548-134">De tabel in SQL-Database maken voordat u begint de topologie op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02548-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="02548-135">In het voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="02548-135">Download the example</span></span>

<span data-ttu-id="02548-136">Download de [HDInsight C# Storm Power BI-voorbeeld](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="02548-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="02548-137">Als u wilt downloaden, ofwel fork/kloon met behulp van [git](http://git-scm.com/), of gebruik de **downloaden** koppeling voor het downloaden van een .zip van het archief.</span><span class="sxs-lookup"><span data-stu-id="02548-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="02548-138">Een database maken</span><span class="sxs-lookup"><span data-stu-id="02548-138">Create a database</span></span>

1. <span data-ttu-id="02548-139">Voor het maken van een database gebruikt u de stappen in de [SQL Database-zelfstudie](../sql-database/sql-database-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="02548-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="02548-140">Verbinding maken met de database door de stappen in de [verbinding maken met een SQL-Database met Visual Studio](../sql-database/sql-database-connect-query.md) document.</span><span class="sxs-lookup"><span data-stu-id="02548-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="02548-141">In Object Explorer met de rechtermuisknop op de database en selecteer **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="02548-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="02548-142">Plak de inhoud van de **IISLogsTable.sql** bestand opgenomen in het gedownloade project naar het queryvenster en gebruik vervolgens Ctrl + Shift + E de query uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="02548-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="02548-143">U ontvangt een bericht dat de opdrachten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="02548-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="02548-144">Het voorbeeld configureren</span><span class="sxs-lookup"><span data-stu-id="02548-144">Configure the sample</span></span>

1. <span data-ttu-id="02548-145">Van de [Azure-portal](https://portal.azure.com), selecteert u uw SQL-database.</span><span class="sxs-lookup"><span data-stu-id="02548-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="02548-146">Van de **Essentials** sectie van de SQL-database, selecteer **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="02548-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="02548-147">In de lijst die wordt weergegeven, kopieert u de **ADO.NET (SQL-verificatie)** informatie.</span><span class="sxs-lookup"><span data-stu-id="02548-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="02548-148">Open het voorbeeld in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02548-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="02548-149">Van **Solution Explorer**, open de **App.config** bestand en zoek de volgende vermelding:</span><span class="sxs-lookup"><span data-stu-id="02548-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="02548-150">Vervang de **# TOBEFILLED ##** waarde met de databaseverbindingsreeks in de vorige stap hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="02548-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="02548-151">Vervang **{uw\_username}** en **{uw\_wachtwoord}** met de gebruikersnaam en wachtwoord voor de database.</span><span class="sxs-lookup"><span data-stu-id="02548-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="02548-152">Opslaan en sluiten van de bestanden.</span><span class="sxs-lookup"><span data-stu-id="02548-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="02548-153">Het voorbeeld implementeren</span><span class="sxs-lookup"><span data-stu-id="02548-153">Deploy the sample</span></span>

1. <span data-ttu-id="02548-154">Van **Solution Explorer**, met de rechtermuisknop op de **StormToSQL** project en selecteer **indienen Storm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="02548-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="02548-155">Selecteer het HDInsight-cluster van de **Storm-Cluster** dropdown dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="02548-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02548-156">Kan het enkele seconden duren voor de **Storm-Cluster** dropdown te vullen met servernamen.</span><span class="sxs-lookup"><span data-stu-id="02548-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="02548-157">Als u wordt gevraagd, voert u de aanmeldingsreferenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="02548-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="02548-158">Als u meer dan één abonnement hebt, moet u zich aanmelden bij de database met uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02548-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="02548-159">Wanneer de topologie is ingediend, de __topologie Viewer__ wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02548-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="02548-160">Als u wilt deze topologie weergeven, selecteert u de vermelding SqlAzureWriterTopology in de lijst.</span><span class="sxs-lookup"><span data-stu-id="02548-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![De topologieën, met de topologie die is geselecteerd](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="02548-162">U kunt het gebruik van deze weergave voor informatie over de topologie of dubbelklik op een item (zoals de SqlAzureBolt) voor informatie die specifiek zijn voor een onderdeel in de topologie.</span><span class="sxs-lookup"><span data-stu-id="02548-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="02548-163">Nadat de topologie is uitgevoerd voor een paar minuten, Ga terug naar het SQL-query-venster dat u gebruikt voor het maken van de database.</span><span class="sxs-lookup"><span data-stu-id="02548-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="02548-164">Vervang de bestaande instructies aan de volgende query:</span><span class="sxs-lookup"><span data-stu-id="02548-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="02548-165">Gebruik Ctrl + Shift + E uitvoeren van de query en u ontvangt resultaten vergelijkbaar met de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="02548-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="02548-166">Deze gegevens is uit de Storm-topologie geschreven.</span><span class="sxs-lookup"><span data-stu-id="02548-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="02548-167">Een rapport maken</span><span class="sxs-lookup"><span data-stu-id="02548-167">Create a report</span></span>

1. <span data-ttu-id="02548-168">Verbinding maken met de [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="02548-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="02548-169">Binnen **Databases**, selecteer **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="02548-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="02548-170">Selecteer **Azure SQL Database**, en selecteer vervolgens **Connect**.</span><span class="sxs-lookup"><span data-stu-id="02548-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02548-171">U wordt mogelijk gevraagd om te downloaden van de Power BI Desktop om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="02548-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="02548-172">Als dit het geval is, moet u de volgende stappen gebruiken om verbinding te:</span><span class="sxs-lookup"><span data-stu-id="02548-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="02548-173">Power BI Desktop openen en selecteer __gegevens ophalen__.</span><span class="sxs-lookup"><span data-stu-id="02548-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="02548-174">2 Schakel __Azure__, en vervolgens __Azure SQL-database__.</span><span class="sxs-lookup"><span data-stu-id="02548-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="02548-175">Geef de informatie die verbinding maken met uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="02548-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="02548-176">U kunt deze informatie vinden in via de [Azure-portal](https://portal.azure.com) en de SQL-database te selecteren.</span><span class="sxs-lookup"><span data-stu-id="02548-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02548-177">U kunt ook het vernieuwingsinterval en aangepaste filters instellen met behulp van **geavanceerde opties inschakelen** in het dialoogvenster verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="02548-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="02548-178">Nadat u verbinding hebt gemaakt, ziet u een nieuwe gegevensset met dezelfde naam als de database die u met verbonden.</span><span class="sxs-lookup"><span data-stu-id="02548-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="02548-179">Selecteer de gegevensset om te beginnen met het ontwerpen van een rapport.</span><span class="sxs-lookup"><span data-stu-id="02548-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="02548-180">Van **velden**, vouw de **IISLOGS** vermelding.</span><span class="sxs-lookup"><span data-stu-id="02548-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="02548-181">Schakel het selectievakje voor een rapport te maken met een lijst met de URI-stammen, **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="02548-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Maken van een rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="02548-183">En sleep de **methode** aan het rapport.</span><span class="sxs-lookup"><span data-stu-id="02548-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="02548-184">Het rapport bijwerken in de lijst is en de bijbehorende HTTP-methode gebruikt voor de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="02548-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![de methode gegevens worden toegevoegd](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="02548-186">Van de **visualisaties** kolom, selecteer de **velden** pictogram en selecteer vervolgens de pijl-omlaag naast **methode** in de **waarden** sectie.</span><span class="sxs-lookup"><span data-stu-id="02548-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="02548-187">Als u wilt weergeven in een telling van het aantal keren dat een URI is geopend, selecteer **aantal**.</span><span class="sxs-lookup"><span data-stu-id="02548-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Wijzigen in een aantal methoden](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="02548-189">Selecteer vervolgens de **gestapeld kolomdiagram** wijzigen hoe de gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02548-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Wijzigen naar een gestapelde grafiek](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="02548-191">Sla het rapport, selecteer **opslaan** en voer een naam voor het rapport.</span><span class="sxs-lookup"><span data-stu-id="02548-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="02548-192">De topologie stoppen</span><span class="sxs-lookup"><span data-stu-id="02548-192">Stop the topology</span></span>

<span data-ttu-id="02548-193">De topologie blijft actief totdat u stoppen of verwijderen van de Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02548-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="02548-194">Als u wilt de topologie stoppen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="02548-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="02548-195">Terug naar de topologie-viewer in Visual Studio en selecteer de topologie.</span><span class="sxs-lookup"><span data-stu-id="02548-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="02548-196">Selecteer de **Kill** knop stoppen van de topologie.</span><span class="sxs-lookup"><span data-stu-id="02548-196">Select the **Kill** button to stop the topology.</span></span>

    ![Kill-knop van de topologie samenvatting](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="02548-198">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="02548-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="02548-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02548-199">Next steps</span></span>

<span data-ttu-id="02548-200">In dit document hebt u geleerd hoe gegevens verzenden vanuit een Storm-topologie met SQL-Database en vervolgens de gegevens visualiseren met Power BI.</span><span class="sxs-lookup"><span data-stu-id="02548-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="02548-201">Zie voor informatie over het werken met andere Azure-technologieën met Storm op HDInsight, het volgende document:</span><span class="sxs-lookup"><span data-stu-id="02548-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="02548-202">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="02548-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
