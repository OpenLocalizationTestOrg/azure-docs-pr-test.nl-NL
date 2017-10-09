---
title: aaaUse Apache Storm met Power BI - Azure HDInsight | Microsoft Docs
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="41672-103">Gebruik Power BI toovisualize gegevens uit een Apache Storm-topologie</span><span class="sxs-lookup"><span data-stu-id="41672-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="41672-104">Power BI kunt u toovisually weergavegegevens als rapporten.</span><span class="sxs-lookup"><span data-stu-id="41672-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="41672-105">Dit document bevat een voorbeeld van hoe toouse Apache Storm op HDInsight toogenerate gegevens voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="41672-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="41672-106">Hallo stappen in dit document zijn afhankelijk van een Windows-ontwikkelomgeving met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41672-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="41672-107">Hallo gecompileerd project kan worden verzonden tooa Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="41672-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="41672-108">Alleen op basis van Linux-clusters gemaakt na 28-10-2016 ondersteuning SCP.NET topologieën.</span><span class="sxs-lookup"><span data-stu-id="41672-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="41672-109">toouse een C#-topologie met een update Hallo Microsoft.SCP.Net.SDK NuGet-pakket gebruikt door uw project tooversion 0.10.0.6 of hoger van het cluster op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="41672-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="41672-110">Hallo-versie van het Hallo-pakket moet ook overeenkomen met de Hallo primaire versie van Storm op HDInsight is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="41672-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="41672-111">HDInsight-versies 3.3 en 3.4 gebruiken bijvoorbeeld Storm-versie 0.10.x en HDInsight 3.5 gebruikt Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="41672-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="41672-112">C#-topologieën op Linux gebaseerde clusters moeten gebruiken, .NET 4.5 en het gebruik van Mono toorun op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="41672-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="41672-113">De meeste dingen werken.</span><span class="sxs-lookup"><span data-stu-id="41672-113">Most things work.</span></span> <span data-ttu-id="41672-114">U moet echter Hallo controleren [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.</span><span class="sxs-lookup"><span data-stu-id="41672-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="41672-115">Zie voor een Java-versie van dit project, met HDInsight op basis van Linux of op basis van Windows werkt, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="41672-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41672-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="41672-116">Prerequisites</span></span>

* <span data-ttu-id="41672-117">Een Azure Active Directory-gebruiker met [Power BI](https://powerbi.com) toegang.</span><span class="sxs-lookup"><span data-stu-id="41672-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="41672-118">Een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="41672-118">An HDInsight cluster.</span></span> <span data-ttu-id="41672-119">Zie voor meer informatie [aan de slag met Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="41672-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="41672-120">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="41672-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="41672-121">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="41672-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="41672-122">Visual Studio (een van de volgende versies Hallo)</span><span class="sxs-lookup"><span data-stu-id="41672-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="41672-123">Visual Studio 2012 met [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="41672-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="41672-124">Visual Studio 2013 met [update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="41672-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="41672-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="41672-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="41672-126">Visual Studio 2017 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="41672-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="41672-127">Hallo HDInsight Tools voor Visual Studio: Zie [aan de slag met Hallo HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) voor meer informatie over installatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="41672-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="41672-128">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="41672-128">How it works</span></span>

<span data-ttu-id="41672-129">In dit voorbeeld bevat een C# Storm-topologie die willekeurig logboekgegevens van Internet Information Services (IIS genereert).</span><span class="sxs-lookup"><span data-stu-id="41672-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="41672-130">Deze gegevens worden vervolgens tooa SQL-Database geschreven en van daaruit is gebruikte toogenerate rapporten in Power BI.</span><span class="sxs-lookup"><span data-stu-id="41672-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="41672-131">Hallo bestanden implementeren Hallo belangrijkste functionaliteit van dit voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="41672-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="41672-132">**SqlAzureBolt.cs**: schrijft informatie in Hallo Storm-topologie tooSQL Database geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="41672-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="41672-133">**IISLogsTable.sql**: Hallo Transact-SQL-instructies gebruikt toogenerate Hallo database die Hallo gegevens worden opgeslagen in.</span><span class="sxs-lookup"><span data-stu-id="41672-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="41672-134">Hallo-tabel maken in SQL-Database voordat het Hallo-topologie op uw HDInsight-cluster wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="41672-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="41672-135">Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="41672-135">Download hello example</span></span>

<span data-ttu-id="41672-136">Hallo downloaden [HDInsight C# Storm Power BI-voorbeeld](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="41672-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="41672-137">toodownload, ofwel fork/kloon met behulp van [git](http://git-scm.com/), of gebruik Hallo **downloaden** koppeling toodownload een .zip van Hallo-archief.</span><span class="sxs-lookup"><span data-stu-id="41672-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="41672-138">Een database maken</span><span class="sxs-lookup"><span data-stu-id="41672-138">Create a database</span></span>

1. <span data-ttu-id="41672-139">een database toocreate Hallo stappen in hello gebruiken [SQL Database-zelfstudie](../sql-database/sql-database-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="41672-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="41672-140">Verbinding maken met toohello database door de volgende Hallo stappen voor het Hallo [tooa SQL-Database met Visual Studio verbinding](../sql-database/sql-database-connect-query.md) document.</span><span class="sxs-lookup"><span data-stu-id="41672-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="41672-141">In Object Explorer met de rechtermuisknop op het Hallo-database en selecteer **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="41672-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="41672-142">Plak de inhoud Hallo Hallo **IISLogsTable.sql** op Hallo bestand project gedownload naar het queryvenster Hallo en vervolgens met Ctrl + Shift + E tooexecute Hallo query.</span><span class="sxs-lookup"><span data-stu-id="41672-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="41672-143">U ontvangt een bericht dat Hallo opdrachten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="41672-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="41672-144">Hallo voorbeeld configureren</span><span class="sxs-lookup"><span data-stu-id="41672-144">Configure hello sample</span></span>

1. <span data-ttu-id="41672-145">Van Hallo [Azure-portal](https://portal.azure.com), selecteert u uw SQL-database.</span><span class="sxs-lookup"><span data-stu-id="41672-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="41672-146">Van Hallo **Essentials** sectie van Hallo SQL-database, selecteer **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="41672-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="41672-147">Kopiëren van Hallo lijst die wordt weergegeven, Hallo **ADO.NET (SQL-verificatie)** informatie.</span><span class="sxs-lookup"><span data-stu-id="41672-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="41672-148">Hallo voorbeeld openen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41672-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="41672-149">Van **Solution Explorer**Open Hallo **App.config** bestand en zoek Hallo vermelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="41672-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="41672-150">Vervang Hallo **# TOBEFILLED ##** waarde met de tekenreeks voor databaseverbinding Hallo in Hallo vorige stap hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="41672-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="41672-151">Vervang **{uw\_username}** en **{uw\_wachtwoord}** met Hallo gebruikersnaam en wachtwoord voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="41672-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="41672-152">Opslaan en sluiten Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="41672-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="41672-153">Hallo voorbeeld implementeren</span><span class="sxs-lookup"><span data-stu-id="41672-153">Deploy hello sample</span></span>

1. <span data-ttu-id="41672-154">Van **Solution Explorer**, klik met de rechtermuisknop Hallo **StormToSQL** project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="41672-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="41672-155">Selecteer Hallo HDInsight-cluster van Hallo **Storm-Cluster** dropdown dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="41672-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41672-156">Het kan enkele seconden duren voor Hallo **Storm-Cluster** dropdown toopopulate met servernamen.</span><span class="sxs-lookup"><span data-stu-id="41672-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="41672-157">Als u wordt gevraagd, voert u Hallo aanmeldingsreferenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="41672-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="41672-158">Als u meer dan één abonnement hebt, meldt u zich in toohello een bestand met uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="41672-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="41672-159">Wanneer het Hallo-topologie is ingediend, Hallo __topologie Viewer__ wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="41672-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="41672-160">tooview deze topologie, selecteer Hallo SqlAzureWriterTopology vermelding uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="41672-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![Hallo-topologieën met Hallo-topologie die zijn geselecteerd](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="41672-162">U kunt gebruiken deze informatie weergeven toosee op Hallo topologie of dubbelklik op een vermelding (zoals hello SqlAzureBolt) toosee specifieke tooa onderdeel van de gegevens in Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="41672-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="41672-163">Na het Hallo is topologie uitgevoerd voor een paar minuten return toohello SQL query-venster toocreate Hallo database die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="41672-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="41672-164">De bestaande instructies Hallo vervangen door Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="41672-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="41672-165">Gebruik Ctrl + Shift + E tooexecute Hallo query, en u ontvangt resultaten vergelijkbare toohello gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="41672-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="41672-166">Deze gegevens is geschreven van Hallo Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="41672-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="41672-167">Een rapport maken</span><span class="sxs-lookup"><span data-stu-id="41672-167">Create a report</span></span>

1. <span data-ttu-id="41672-168">Verbinding maken met toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) voor Power BI.</span><span class="sxs-lookup"><span data-stu-id="41672-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="41672-169">Binnen **Databases**, selecteer **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="41672-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="41672-170">Selecteer **Azure SQL Database**, en selecteer vervolgens **Connect**.</span><span class="sxs-lookup"><span data-stu-id="41672-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="41672-171">U wordt mogelijk gevraagd toodownload Hallo Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="41672-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="41672-172">Als dit het geval is, gebruikt u Hallo tooconnect stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="41672-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="41672-173">Power BI Desktop openen en selecteer __gegevens ophalen__.</span><span class="sxs-lookup"><span data-stu-id="41672-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="41672-174">2 Schakel __Azure__, en vervolgens __Azure SQL-database__.</span><span class="sxs-lookup"><span data-stu-id="41672-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="41672-175">Voer Hallo informatie tooconnect tooyour Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="41672-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="41672-176">U vindt deze informatie Hallo [Azure-portal](https://portal.azure.com) en de SQL-database te selecteren.</span><span class="sxs-lookup"><span data-stu-id="41672-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41672-177">U kunt ook het vernieuwingsinterval Hallo en aangepaste filters instellen met behulp van **geavanceerde opties inschakelen** van Hallo dialoogvenster voor verbinden.</span><span class="sxs-lookup"><span data-stu-id="41672-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="41672-178">Nadat u verbinding hebt gemaakt, ziet u een nieuwe gegevensset met dezelfde naam als de database Hallo u verbonden met Hallo.</span><span class="sxs-lookup"><span data-stu-id="41672-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="41672-179">Hallo gegevensset toobegin ontwerpen van een rapport selecteren.</span><span class="sxs-lookup"><span data-stu-id="41672-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="41672-180">Van **velden**, vouw Hallo **IISLOGS** vermelding.</span><span class="sxs-lookup"><span data-stu-id="41672-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="41672-181">een rapport dat een lijst met URI Hallo komen voort, toocreate Hallo selectievakje selecteert voor **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="41672-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Maken van een rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="41672-183">En sleep de **methode** toohello rapport.</span><span class="sxs-lookup"><span data-stu-id="41672-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="41672-184">Hallo rapport updates toolist Hallo komen voort en Hallo bijbehorende HTTP-methode gebruikt voor Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="41672-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![Hallo methode gegevens toe te voegen](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="41672-186">Van Hallo **visualisaties** kolom, selecteer Hallo **velden** pictogram en selecteer vervolgens Hallo pijl-omlaag naast te**methode** in Hallo **waarden**sectie.</span><span class="sxs-lookup"><span data-stu-id="41672-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="41672-187">toodisplay een telling van hoe vaak een URI is geopend, selecteer **aantal**.</span><span class="sxs-lookup"><span data-stu-id="41672-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Het aantal methoden tooa wijzigen](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="41672-189">Selecteer vervolgens Hallo **gestapeld kolomdiagram** toochange hoe Hallo informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="41672-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Veranderende tooa gestapelde grafiek](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="41672-191">toosave hello rapport, selecteer **opslaan** en voer een naam voor het Hallo-rapport.</span><span class="sxs-lookup"><span data-stu-id="41672-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="41672-192">Hallo-topologie stoppen</span><span class="sxs-lookup"><span data-stu-id="41672-192">Stop hello topology</span></span>

<span data-ttu-id="41672-193">Hallo-topologie wordt toorun vervolgd totdat u stoppen of verwijderen van Hallo Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="41672-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="41672-194">toostop Hallo topologie, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="41672-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="41672-195">In Visual Studio toohello topologie viewer terug en selecteer Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="41672-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="41672-196">Selecteer Hallo **Kill** knop toostop Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="41672-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill-knop op Hallo topologie samenvatting](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="41672-198">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="41672-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="41672-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41672-199">Next steps</span></span>

<span data-ttu-id="41672-200">In dit document hebt u geleerd hoe toosend gegevens van een Storm-topologie tooSQL Database, klikt u vervolgens Hallo gegevens visualiseren met Power BI.</span><span class="sxs-lookup"><span data-stu-id="41672-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="41672-201">Voor meer informatie over toowork met andere Azure technologieën met Storm op HDInsight, Zie Hallo document te volgen:</span><span class="sxs-lookup"><span data-stu-id="41672-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="41672-202">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="41672-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
