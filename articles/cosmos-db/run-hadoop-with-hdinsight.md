---
title: Voer een met behulp van Azure DB die Cosmos en HDInsight Hadoop | Microsoft Docs
description: Ontdek hoe u een eenvoudige Hive, Pig en MapReduce-taak uitvoert met Azure Cosmos DB en Azure HDInsight.
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="221f3-103"><a name="Azure Cosmos DB-HDInsight"></a>Voer een Apache Hive, Pig of Hadoop met behulp van Azure DB die Cosmos en HDInsight</span><span class="sxs-lookup"><span data-stu-id="221f3-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="221f3-104">Deze zelfstudie leert u hoe u uitvoert [Apache Hive][apache-hive], [Apache Pig][apache-pig], en [Apache Hadoop] [ apache-hadoop] MapReduce-taken in Azure HDInsight met Hadoop-connector Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="221f3-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="221f3-105">Hadoop-connector cosmos-database kunt Cosmos DB om te fungeren als een bron- en sink voor Hive, Pig en MapReduce-taken.</span><span class="sxs-lookup"><span data-stu-id="221f3-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="221f3-106">Deze zelfstudie gaat Cosmos DB gebruiken als de gegevensbron en de bestemming voor Hadoop-taken.</span><span class="sxs-lookup"><span data-stu-id="221f3-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="221f3-107">Na het voltooien van deze zelfstudie, hebt u mogelijk de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="221f3-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="221f3-108">Hoe ik gegevens laden van de Cosmos-database met behulp van een Hive, Pig of MapReduce-taak?</span><span class="sxs-lookup"><span data-stu-id="221f3-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="221f3-109">Hoe kan ik gegevens opslaan in Cosmos-database met behulp van een Hive, Pig of MapReduce-taak?</span><span class="sxs-lookup"><span data-stu-id="221f3-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="221f3-110">Het is raadzaam om aan de slag door de volgende video, waar we uitvoeren via een met behulp van de Cosmos-DB en HDInsight Hive-taak kijken.</span><span class="sxs-lookup"><span data-stu-id="221f3-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="221f3-111">Keer vervolgens terug naar dit artikel, waar u de volledige informatie over hoe u analytics-taken op uw gegevens Cosmos DB uitvoeren kunt hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="221f3-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="221f3-112">Deze zelfstudie wordt ervan uitgegaan dat u ervaring met Apache Hadoop, Hive en/of Pig hebt.</span><span class="sxs-lookup"><span data-stu-id="221f3-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="221f3-113">Als u niet bekend met Apache Hadoop Hive en Pig bent, raden wij aan via de [Apache Hadoop-documentatie][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="221f3-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="221f3-114">Deze zelfstudie wordt ervan uitgegaan dat u ervaring met Cosmos DB hebt en een Cosmos-DB-account hebben.</span><span class="sxs-lookup"><span data-stu-id="221f3-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="221f3-115">Als u niet bekend met Cosmos DB bent of u beschikt niet over een Cosmos-DB-account, check onze [aan de slag] [ getting-started] pagina.</span><span class="sxs-lookup"><span data-stu-id="221f3-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="221f3-116">Geen tijd om de zelfstudie te voltooien en wilt ophalen van de PowerShell-scripts voor het volledige voorbeeld voor Hive, Pig en MapReduce?</span><span class="sxs-lookup"><span data-stu-id="221f3-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="221f3-117">Geen probleem, ze [hier][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="221f3-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="221f3-118">De download bevat ook de hql, pig en java-bestanden voor deze voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="221f3-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="221f3-119"><a name="NewestVersion"></a>Meest recente versie</span><span class="sxs-lookup"><span data-stu-id="221f3-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="221f3-120">Versie van Hadoop-Connector</span><span class="sxs-lookup"><span data-stu-id="221f3-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="221f3-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="221f3-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="221f3-122">Script-Uri</span><span class="sxs-lookup"><span data-stu-id="221f3-122">Script Uri</span></span></th>
        <td><span data-ttu-id="221f3-123">https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="221f3-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="221f3-124">Datum gewijzigd</span><span class="sxs-lookup"><span data-stu-id="221f3-124">Date Modified</span></span></th>
        <td><span data-ttu-id="221f3-125">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="221f3-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="221f3-126">Ondersteunde HDInsight-versies</span><span class="sxs-lookup"><span data-stu-id="221f3-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="221f3-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="221f3-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="221f3-128">Wijzigingenlogboek</span><span class="sxs-lookup"><span data-stu-id="221f3-128">Change Log</span></span></th>
        <td><span data-ttu-id="221f3-129">Bijgewerkt Azure Cosmos DB Java SDK voor 1.6.0</span><span class="sxs-lookup"><span data-stu-id="221f3-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="221f3-130">Toegevoegde ondersteuning voor gepartitioneerde verzamelingen op als een bron- en sink</span><span class="sxs-lookup"><span data-stu-id="221f3-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="221f3-131"><a name="Prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="221f3-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="221f3-132">Voordat u de instructies in deze zelfstudie, zorg ervoor dat u het volgende hebt:</span><span class="sxs-lookup"><span data-stu-id="221f3-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="221f3-133">Een Cosmos-DB-account, een database en een verzameling met documenten in.</span><span class="sxs-lookup"><span data-stu-id="221f3-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="221f3-134">Zie voor meer informatie [aan de slag met Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="221f3-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="221f3-135">Voorbeeldgegevens importeren in een Cosmos-DB-account met de [Cosmos DB import-hulpprogramma][import-data].</span><span class="sxs-lookup"><span data-stu-id="221f3-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="221f3-136">De doorvoer.</span><span class="sxs-lookup"><span data-stu-id="221f3-136">Throughput.</span></span> <span data-ttu-id="221f3-137">Leest en schrijft uit HDInsight naar uw toegewezen aanvraageenheden voor uw verzamelingen worden geteld.</span><span class="sxs-lookup"><span data-stu-id="221f3-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="221f3-138">De uitvoer van capaciteit voor een aanvullende opgeslagen procedure binnen elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="221f3-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="221f3-139">De opgeslagen procedures worden gebruikt voor het overdragen van de resulterende documenten.</span><span class="sxs-lookup"><span data-stu-id="221f3-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="221f3-140">Capaciteit voor de resulterende documenten uit de Hive, Pig of MapReduce-taken.</span><span class="sxs-lookup"><span data-stu-id="221f3-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="221f3-141">[*Optioneel*] capaciteit voor een aanvullende verzameling.</span><span class="sxs-lookup"><span data-stu-id="221f3-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="221f3-142">Om te voorkomen dat het maken van een nieuwe verzameling tijdens een van de taken, kunt u de resultaten naar stdout afdrukken, sla de uitvoer naar de container WASB of geef een bestaande verzameling op.</span><span class="sxs-lookup"><span data-stu-id="221f3-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="221f3-143">In het geval van een bestaande verzameling geven, nieuwe documenten gemaakt in de verzameling en de al bestaande documenten alleen worden beïnvloed als er een conflict in *id's*.</span><span class="sxs-lookup"><span data-stu-id="221f3-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="221f3-144">**De connector wordt automatisch bestaande documenten overschreven met de ID-conflicten**.</span><span class="sxs-lookup"><span data-stu-id="221f3-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="221f3-145">U kunt deze functie uitschakelen door de optie upsert op false.</span><span class="sxs-lookup"><span data-stu-id="221f3-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="221f3-146">Als upsert ingesteld op false is en een conflict optreedt, mislukt de taak Hadoop; een id conflict fout wordt gemeld.</span><span class="sxs-lookup"><span data-stu-id="221f3-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="221f3-147"><a name="ProvisionHDInsight"></a>Stap 1: Maak een nieuw HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="221f3-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="221f3-148">Deze zelfstudie wordt scriptactie vanuit de Azure Portal voor het aanpassen van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="221f3-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="221f3-149">In deze zelfstudie gebruiken we de Azure Portal om uw HDInsight-cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="221f3-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="221f3-150">Voor instructies over het gebruik van PowerShell-cmdlets of de HDInsight-SDK voor .NET, bekijk de [aanpassen HDInsight-clusters met behulp van de scriptactie] [ hdinsight-custom-provision] artikel.</span><span class="sxs-lookup"><span data-stu-id="221f3-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="221f3-151">Aanmelden bij de [Azure-Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="221f3-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="221f3-152">Klik op **+ nieuw** zoekt boven aan het linkernavigatiegedeelte **HDInsight** in de bovenste zoekbalk op de nieuwe blade.</span><span class="sxs-lookup"><span data-stu-id="221f3-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="221f3-153">**HDInsight** gepubliceerd door **Microsoft** aan de bovenkant van de resultaten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="221f3-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="221f3-154">Klik hierop en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="221f3-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="221f3-155">Blade maken op het nieuwe HDInsight-Cluster, Voer uw **clusternaam** en selecteer de **abonnement** wilt u deze bron op onder inrichten.</span><span class="sxs-lookup"><span data-stu-id="221f3-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="221f3-156">Clusternaam</span><span class="sxs-lookup"><span data-stu-id="221f3-156">Cluster name</span></span></td><td><span data-ttu-id="221f3-157">De naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="221f3-157">Name the cluster.</span></span><br/>
<span data-ttu-id="221f3-158">DNS-naam moet beginnen en eindigen met een teken alfanumerieke en streepjes kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="221f3-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="221f3-159">Het veld moet een tekenreeks tussen 3 en 63 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="221f3-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="221f3-160">De naam van abonnement</span><span class="sxs-lookup"><span data-stu-id="221f3-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="221f3-161">Als u meer dan één Azure-abonnement hebt, selecteert u het abonnement dat als voor uw HDInsight-cluster host fungeert.</span><span class="sxs-lookup"><span data-stu-id="221f3-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="221f3-162">
5.Klik op **clustertype Selecteer** en de volgende eigenschappen instellen op de opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="221f3-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="221f3-163">Clustertype</span><span class="sxs-lookup"><span data-stu-id="221f3-163">Cluster type</span></span></td><td><span data-ttu-id="221f3-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="221f3-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="221f3-165">Cluster-laag</span><span class="sxs-lookup"><span data-stu-id="221f3-165">Cluster tier</span></span></td><td><span data-ttu-id="221f3-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="221f3-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="221f3-167">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="221f3-167">Operating System</span></span></td><td><span data-ttu-id="221f3-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="221f3-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="221f3-169">Versie</span><span class="sxs-lookup"><span data-stu-id="221f3-169">Version</span></span></td><td><span data-ttu-id="221f3-170">meest recente versie</span><span class="sxs-lookup"><span data-stu-id="221f3-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="221f3-171">Klik nu op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="221f3-171">Now, click **SELECT**.</span></span>

    ![Hadoop HDInsight initiële clusterdetails bieden][image-customprovision-page1]
6. <span data-ttu-id="221f3-173">Klik op **referenties** uw aanmeldgegevens en referenties voor externe toegang instellen.</span><span class="sxs-lookup"><span data-stu-id="221f3-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="221f3-174">Kies uw **Cluster aanmelding gebruikersnaam** en **aanmeldingswachtwoord Cluster**.</span><span class="sxs-lookup"><span data-stu-id="221f3-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="221f3-175">Als u wilt dat extern in uw cluster, selecteert u *Ja* onderaan de blade en geef een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="221f3-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="221f3-176">Klik op **gegevensbron** instellen van uw primaire locatie voor toegang tot gegevens.</span><span class="sxs-lookup"><span data-stu-id="221f3-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="221f3-177">Kies de **selectiemethode** en geef een bestaand opslagaccount of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="221f3-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="221f3-178">Geef op de blade dezelfde een **standaard Container** en een **locatie**.</span><span class="sxs-lookup"><span data-stu-id="221f3-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="221f3-179">En klik op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="221f3-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="221f3-180">Selecteer een locatie dicht bij uw regio Cosmos-DB-account voor betere prestaties</span><span class="sxs-lookup"><span data-stu-id="221f3-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="221f3-181">Klik op **prijzen** selecteren van het aantal en type van knooppunten.</span><span class="sxs-lookup"><span data-stu-id="221f3-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="221f3-182">U kunt de standaardconfiguratie houden en schalen het aantal Worker-knooppunten later op.</span><span class="sxs-lookup"><span data-stu-id="221f3-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="221f3-183">Klik op **optionele configuratie**, klikt u vervolgens **acties Script** in de Blade optionele configuratie.</span><span class="sxs-lookup"><span data-stu-id="221f3-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="221f3-184">Voer de volgende informatie voor het aanpassen van uw HDInsight-cluster in Script-acties.</span><span class="sxs-lookup"><span data-stu-id="221f3-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="221f3-185">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="221f3-185">Property</span></span></th><th><span data-ttu-id="221f3-186">Waarde</span><span class="sxs-lookup"><span data-stu-id="221f3-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="221f3-187">Naam</span><span class="sxs-lookup"><span data-stu-id="221f3-187">Name</span></span></td>
             <td><span data-ttu-id="221f3-188">Geef een naam voor de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="221f3-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="221f3-189">Script-URI</span><span class="sxs-lookup"><span data-stu-id="221f3-189">Script URI</span></span></td>
             <td><span data-ttu-id="221f3-190">Geef de URI moet het script dat wordt opgeroepen voor het aanpassen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="221f3-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="221f3-191">Voer in:</span><span class="sxs-lookup"><span data-stu-id="221f3-191">Please enter:</span></span> </br> <span data-ttu-id="221f3-192"><strong>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="221f3-193">Kop</span><span class="sxs-lookup"><span data-stu-id="221f3-193">Head</span></span></td>
             <td><span data-ttu-id="221f3-194">Klik op het selectievakje in om te worden uitgevoerd op het hoofdknooppunt van het PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="221f3-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="221f3-195">
             <strong>Schakel dit selectievakje in</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="221f3-196">Werknemer</span><span class="sxs-lookup"><span data-stu-id="221f3-196">Worker</span></span></td>
             <td><span data-ttu-id="221f3-197">Klik op het selectievakje in als u wilt uitvoeren van het PowerShell-script op het werkrolknooppunt.</span><span class="sxs-lookup"><span data-stu-id="221f3-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="221f3-198">
             <strong>Schakel dit selectievakje in</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="221f3-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="221f3-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="221f3-200">Klik op het selectievakje in als u wilt uitvoeren van het PowerShell-script op de Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="221f3-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="221f3-201">
             <strong>Niet nodig</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="221f3-202">Parameters</span><span class="sxs-lookup"><span data-stu-id="221f3-202">Parameters</span></span></td>
             <td><span data-ttu-id="221f3-203">Geef de parameters op, indien vereist door het script.</span><span class="sxs-lookup"><span data-stu-id="221f3-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="221f3-204">
             <strong>Er zijn geen Parameters nodig</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="221f3-205">
11.Maken van een nieuwe **resourcegroep** of gebruik een bestaande resourcegroep onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="221f3-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="221f3-206">12.</span><span class="sxs-lookup"><span data-stu-id="221f3-206">12.</span></span> <span data-ttu-id="221f3-207">Controleer nu **vastmaken aan dashboard** bijhouden van de implementatie en klikt u op **maken**!</span><span class="sxs-lookup"><span data-stu-id="221f3-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="221f3-208"><a name="InstallCmdlets"></a>Stap 2: Installeer en configureer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="221f3-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="221f3-209">Installeer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="221f3-209">Install Azure PowerShell.</span></span> <span data-ttu-id="221f3-210">Instructies hiervoor vindt u [hier][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="221f3-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="221f3-211">U kunt ook van HDInsight online Hive-Editor gebruiken voor Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="221f3-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="221f3-212">Om dit te doen, moet u zich aanmelden bij de [Azure Portal][azure-portal], klikt u op **HDInsight** in het linkerdeelvenster om een lijst met uw HDInsight-clusters weer te geven.</span><span class="sxs-lookup"><span data-stu-id="221f3-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="221f3-213">Klik op het cluster dat u wilt uitvoeren van Hive-query's op en klik vervolgens op **Query Console**.</span><span class="sxs-lookup"><span data-stu-id="221f3-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="221f3-214">Open de Azure PowerShell Integrated Scripting Environment:</span><span class="sxs-lookup"><span data-stu-id="221f3-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="221f3-215">Op een computer met Windows 8 of WindowsServer 2012 of nieuwer, kunt u de ingebouwde zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="221f3-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="221f3-216">Typ in het startscherm **powershell ise** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="221f3-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="221f3-217">Gebruik het menu Start op een computer met een besturingssysteem dat ouder dan Windows 8 of Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="221f3-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="221f3-218">Typ in het menu Start **opdrachtprompt** in het zoekvak en vervolgens in de lijst met resultaten, klikt u op **opdrachtprompt**.</span><span class="sxs-lookup"><span data-stu-id="221f3-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="221f3-219">Typ in het opdrachtpromptvenster **powershell_ise** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="221f3-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="221f3-220">Uw Azure-Account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="221f3-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="221f3-221">Typ in het consolevenster **Add-AzureAccount** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="221f3-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="221f3-222">Typ in het e-mailadres dat is gekoppeld aan uw Azure-abonnement en klikt u op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="221f3-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="221f3-223">Typ in het wachtwoord voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="221f3-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="221f3-224">Klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="221f3-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="221f3-225">Het volgende diagram worden de belangrijke onderdelen van uw omgeving Azure PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="221f3-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagram voor Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="221f3-227"><a name="RunHive"></a>Stap 3: Voer een Hive-taak met Cosmos DB en HDInsight</span><span class="sxs-lookup"><span data-stu-id="221f3-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="221f3-228">Alle variabelen aangegeven door een combinatie moeten worden ingevuld met behulp van uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="221f3-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="221f3-229">De volgende variabelen instellen in het deelvenster van de PowerShell-Script.</span><span class="sxs-lookup"><span data-stu-id="221f3-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="221f3-230">Laten we beginnen construeren van de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="221f3-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="221f3-231">We moet een Hive-query die wordt het systeem gegenereerde tijdstempels (_ts) en de unieke id's (_rid) uit een verzameling Azure Cosmos DB alle documenten, telt alle documenten per minuut en slaat vervolgens de resultaten weer in een nieuwe Azure DB die Cosmos-verzameling schrijven.</span><span class="sxs-lookup"><span data-stu-id="221f3-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="221f3-232">Eerst gaan we een Hive-tabel maken van onze Azure DB die Cosmos-verzameling.</span><span class="sxs-lookup"><span data-stu-id="221f3-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="221f3-233">Het volgende codefragment toevoegen aan het deelvenster met PowerShell-Script <strong>nadat</strong> het codefragment van #1.</span><span class="sxs-lookup"><span data-stu-id="221f3-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="221f3-234">Zorg ervoor dat u de beperkende optionele DocumentDB.query parameter t onze documenten kunnen alleen _ts en _rid.</span><span class="sxs-lookup"><span data-stu-id="221f3-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="221f3-235">**Naamgeving van DocumentDB.inputCollections is niet een fout.**</span><span class="sxs-lookup"><span data-stu-id="221f3-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="221f3-236">Ja, kunnen we meerdere verzamelingen als invoer toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="221f3-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="221f3-237">Vervolgens maken we een Hive-tabel voor de uitvoer-verzameling.</span><span class="sxs-lookup"><span data-stu-id="221f3-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="221f3-238">De eigenschappen van de uitvoer is de maand, dag, uur, minuut en het totale aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="221f3-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="221f3-239">**Naamgeving van DocumentDB.outputCollections was nog opnieuw niet een fout.**</span><span class="sxs-lookup"><span data-stu-id="221f3-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="221f3-240">Ja, kunnen we meerdere verzamelingen toe te voegen als uitvoer:</span><span class="sxs-lookup"><span data-stu-id="221f3-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="221f3-241">'*DocumentDB.outputCollections*'='*\<DocumentDB verzameling uitvoernaam 1\>*,*\<DocumentDB verzameling uitvoernaam 2\>* '</span><span class="sxs-lookup"><span data-stu-id="221f3-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="221f3-242">De verzamelingsnamen van de worden zonder spaties, met slechts een enkele komma gescheiden.</span><span class="sxs-lookup"><span data-stu-id="221f3-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="221f3-243">Documenten worden gedistribueerde round robin in meerdere verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="221f3-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="221f3-244">Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="221f3-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="221f3-245">Tot slot gaan we de documenten tally per maand, dag, uur en minuut en invoegen van de resultaten weer in de uitvoer van de Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="221f3-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="221f3-246">Voeg het volgende fragment script voor het maken van de definitie van een Hive-taak uit de vorige query.</span><span class="sxs-lookup"><span data-stu-id="221f3-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="221f3-247">U kunt ook gebruiken om op te geven van een scriptbestand HiveQL op HDFS-schakeloptie in het bestand.</span><span class="sxs-lookup"><span data-stu-id="221f3-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="221f3-248">Voeg het volgende codefragment voor het opslaan van de begintijd en verzenden van de Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="221f3-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="221f3-249">Voeg de volgende wachten tot de Hive-taak te voltooien.</span><span class="sxs-lookup"><span data-stu-id="221f3-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="221f3-250">Voeg de volgende om de standaarduitvoer en de begin- en eindtijden te drukken.</span><span class="sxs-lookup"><span data-stu-id="221f3-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="221f3-251">**Voer** het nieuwe script!</span><span class="sxs-lookup"><span data-stu-id="221f3-251">**Run** your new script!</span></span> <span data-ttu-id="221f3-252">**Klik op** de knop groen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="221f3-253">Controleer de resultaten.</span><span class="sxs-lookup"><span data-stu-id="221f3-253">Check the results.</span></span> <span data-ttu-id="221f3-254">Meld u aan bij de [Azure-Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="221f3-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="221f3-255">Klik op <strong>Bladeren</strong> in het paneel aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="221f3-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="221f3-256">Klik op <strong>Alles</strong> in de rechterbovenhoek van het paneel bladeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="221f3-257">Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="221f3-258">Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de verzameling uitvoer is opgegeven in uw Hive-query.</span><span class="sxs-lookup"><span data-stu-id="221f3-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="221f3-259">Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="221f3-260">Hier ziet u de resultaten van uw Hive-query.</span><span class="sxs-lookup"><span data-stu-id="221f3-260">You will see the results of your Hive query.</span></span>

   ![De resultaten van de hive-query][image-hive-query-results]

## <span data-ttu-id="221f3-262"><a name="RunPig"></a>Stap 4: Een Pig-taak met Cosmos DB en HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="221f3-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="221f3-263">Alle variabelen aangegeven door een combinatie moeten worden ingevuld met behulp van uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="221f3-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="221f3-264">De volgende variabelen instellen in het deelvenster van de PowerShell-Script.</span><span class="sxs-lookup"><span data-stu-id="221f3-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="221f3-265">Laten we beginnen construeren van de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="221f3-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="221f3-266">We moet een Pig-query die wordt het systeem gegenereerde tijdstempels (_ts) en de unieke id's (_rid) uit een verzameling Azure Cosmos DB alle documenten, telt alle documenten per minuut en slaat vervolgens de resultaten weer in een nieuwe Azure DB die Cosmos-verzameling schrijven.</span><span class="sxs-lookup"><span data-stu-id="221f3-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="221f3-267">Documenten van de Cosmos-database eerst laden in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="221f3-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="221f3-268">Het volgende codefragment toevoegen aan het deelvenster met PowerShell-Script <strong>nadat</strong> het codefragment van #1.</span><span class="sxs-lookup"><span data-stu-id="221f3-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="221f3-269">Zorg ervoor dat u een DocumentDB-query toevoegen aan de optionele parameter van de query DocumentDB om onze documenten kunnen alleen _ts trim en _rid.</span><span class="sxs-lookup"><span data-stu-id="221f3-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="221f3-270">Ja, kunnen we meerdere verzamelingen als invoer toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="221f3-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="221f3-271">'*\<DocumentDB verzameling invoernaam 1\>*,*\<DocumentDB verzameling invoernaam 2\>*'</span><span class="sxs-lookup"><span data-stu-id="221f3-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="221f3-272">De verzamelingsnamen van de worden zonder spaties, met slechts een enkele komma gescheiden.</span><span class="sxs-lookup"><span data-stu-id="221f3-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="221f3-273">Documenten worden gedistribueerde round robin in meerdere verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="221f3-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="221f3-274">Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="221f3-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="221f3-275">Vervolgens laten we de documenten tally door de maand, dag, uur, minuut en het totale aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="221f3-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="221f3-276">Stel ten slotte de resultaten opslaan in onze nieuwe uitvoer-verzameling.</span><span class="sxs-lookup"><span data-stu-id="221f3-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="221f3-277">Ja, kunnen we meerdere verzamelingen toe te voegen als uitvoer:</span><span class="sxs-lookup"><span data-stu-id="221f3-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="221f3-278">'\<DocumentDB verzameling uitvoernaam 1\>,\<DocumentDB verzameling uitvoernaam 2\>'</span><span class="sxs-lookup"><span data-stu-id="221f3-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="221f3-279">De verzamelingsnamen van de worden zonder spaties, met slechts een enkele komma gescheiden.</span><span class="sxs-lookup"><span data-stu-id="221f3-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="221f3-280">Documenten worden over meerdere verzamelingen gedistribueerde round robin.</span><span class="sxs-lookup"><span data-stu-id="221f3-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="221f3-281">Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="221f3-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="221f3-282">Voeg het volgende fragment script voor het maken van de definitie van een Pig-taak uit de vorige query.</span><span class="sxs-lookup"><span data-stu-id="221f3-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="221f3-283">U kunt ook gebruiken om op te geven van een scriptbestand Pig op HDFS-schakeloptie in het bestand.</span><span class="sxs-lookup"><span data-stu-id="221f3-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="221f3-284">Voeg het volgende codefragment voor het opslaan van de begintijd en verzenden van de Pig-taak.</span><span class="sxs-lookup"><span data-stu-id="221f3-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="221f3-285">Voeg de volgende wachten tot de Pig-taak te voltooien.</span><span class="sxs-lookup"><span data-stu-id="221f3-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="221f3-286">Voeg de volgende om de standaarduitvoer en de begin- en eindtijden te drukken.</span><span class="sxs-lookup"><span data-stu-id="221f3-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="221f3-287">**Voer** het nieuwe script!</span><span class="sxs-lookup"><span data-stu-id="221f3-287">**Run** your new script!</span></span> <span data-ttu-id="221f3-288">**Klik op** de knop groen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="221f3-289">Controleer de resultaten.</span><span class="sxs-lookup"><span data-stu-id="221f3-289">Check the results.</span></span> <span data-ttu-id="221f3-290">Meld u aan bij de [Azure-Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="221f3-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="221f3-291">Klik op <strong>Bladeren</strong> in het paneel aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="221f3-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="221f3-292">Klik op <strong>Alles</strong> in de rechterbovenhoek van het paneel bladeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="221f3-293">Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="221f3-294">Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de verzameling uitvoer is opgegeven in uw Pig-query.</span><span class="sxs-lookup"><span data-stu-id="221f3-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="221f3-295">Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="221f3-296">Hier ziet u de resultaten van uw query Pig.</span><span class="sxs-lookup"><span data-stu-id="221f3-296">You will see the results of your Pig query.</span></span>

    ![Pig-queryresultaten][image-pig-query-results]

## <span data-ttu-id="221f3-298"><a name="RunMapReduce"></a>Stap 5: Een MapReduce-taak met behulp van Azure DB die Cosmos en HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="221f3-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="221f3-299">De volgende variabelen instellen in het deelvenster van de PowerShell-Script.</span><span class="sxs-lookup"><span data-stu-id="221f3-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="221f3-300">Er moet een MapReduce-taak die het aantal exemplaren voor elke eigenschap van het Document uit de verzameling van uw Azure Cosmos DB telt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="221f3-301">In dit fragment script toevoegen **nadat** het bovenstaande codefragment.</span><span class="sxs-lookup"><span data-stu-id="221f3-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="221f3-302">TallyProperties v01.jar wordt geleverd met de aangepaste installatie van de Cosmos DB Hadoop-Connector.</span><span class="sxs-lookup"><span data-stu-id="221f3-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="221f3-303">Voeg de volgende opdracht om het verzenden van de MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="221f3-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="221f3-304">Naast de taakdefinitie MapReduce, moet u ook de naam van het HDInsight-cluster waarop u wilt uitvoeren van de MapReduce-taak en de referenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="221f3-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="221f3-305">De begin-AzureHDInsightJob is een aanroep van asynchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="221f3-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="221f3-306">Gebruiken om te controleren op de voltooiing van de taak, de *wacht AzureHDInsightJob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="221f3-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="221f3-307">Voeg de volgende opdracht om te controleren of er fouten met de MapReduce-taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="221f3-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="221f3-308">**Voer** het nieuwe script!</span><span class="sxs-lookup"><span data-stu-id="221f3-308">**Run** your new script!</span></span> <span data-ttu-id="221f3-309">**Klik op** de knop groen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="221f3-310">Controleer de resultaten.</span><span class="sxs-lookup"><span data-stu-id="221f3-310">Check the results.</span></span> <span data-ttu-id="221f3-311">Meld u aan bij de [Azure-Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="221f3-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="221f3-312">Klik op <strong>Bladeren</strong> in het paneel aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="221f3-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="221f3-313">Klik op <strong>Alles</strong> in de rechterbovenhoek van het paneel bladeren.</span><span class="sxs-lookup"><span data-stu-id="221f3-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="221f3-314">Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="221f3-315">Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de verzameling uitvoer is opgegeven in uw MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="221f3-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="221f3-316">Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</span><span class="sxs-lookup"><span data-stu-id="221f3-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="221f3-317">Hier ziet u de resultaten van uw MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="221f3-317">You will see the results of your MapReduce job.</span></span>

      ![MapReduce-queryresultaten][image-mapreduce-query-results]

## <span data-ttu-id="221f3-319"><a name="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="221f3-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="221f3-320">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="221f3-320">Congratulations!</span></span> <span data-ttu-id="221f3-321">U hebt zojuist uw eerste Hive, Pig en MapReduce-taken met behulp van Azure DB die Cosmos en HDInsight uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="221f3-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="221f3-322">We hebben onze Hadoop-Connector die afkomstig zijn geopend.</span><span class="sxs-lookup"><span data-stu-id="221f3-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="221f3-323">Als u geïnteresseerd bent, u kunt bijdragen op [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="221f3-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="221f3-324">Zie voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="221f3-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="221f3-325">[Een Java-toepassing met Documentdb ontwikkelen][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="221f3-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="221f3-326">[Het ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="221f3-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="221f3-327">[Aan de slag met Hadoop Hive in HDInsight analyseren mobiele telefoon gebruiken][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="221f3-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="221f3-328">[MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="221f3-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="221f3-329">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="221f3-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="221f3-330">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="221f3-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="221f3-331">[HDInsight-clusters met behulp van de scriptactie aanpassen][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="221f3-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
