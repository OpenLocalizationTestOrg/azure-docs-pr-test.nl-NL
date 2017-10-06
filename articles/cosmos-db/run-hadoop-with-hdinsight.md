---
title: aaaRun een Hadoop-taak met behulp van Azure DB die Cosmos en HDInsight | Microsoft Docs
description: Meer informatie over hoe toorun een eenvoudige Hive, Pig en MapReduce taak met Azure Cosmos DB en Azure HDInsight.
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
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="ef1b6-103"><a name="Azure Cosmos DB-HDInsight"></a>Voer een Apache Hive, Pig of Hadoop met behulp van Azure DB die Cosmos en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef1b6-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="ef1b6-104">Deze zelfstudie leert u hoe toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], en [Apache Hadoop] [ apache-hadoop] MapReduce-taken in Azure HDInsight met Hadoop-connector Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="ef1b6-105">Cosmos DB van Hadoop-connector kunt Cosmos DB tooact als een bron- en sink voor Hive, Pig en MapReduce-taken.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="ef1b6-106">Deze zelfstudie gebruikt Cosmos DB Hallo gegevensbron en bestemming voor Hadoop-taken.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="ef1b6-107">Na het voltooien van deze zelfstudie, moet u kunnen tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="ef1b6-108">Hoe ik gegevens laden van de Cosmos-database met behulp van een Hive, Pig of MapReduce-taak?</span><span class="sxs-lookup"><span data-stu-id="ef1b6-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="ef1b6-109">Hoe kan ik gegevens opslaan in Cosmos-database met behulp van een Hive, Pig of MapReduce-taak?</span><span class="sxs-lookup"><span data-stu-id="ef1b6-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="ef1b6-110">Het is raadzaam om aan de slag door bekijkt hello volgende video waar we uitvoeren via een met behulp van de Cosmos-DB en HDInsight Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="ef1b6-111">Keer vervolgens terug toothis artikel, waarin u ontvangt Hallo volledige details over hoe u analytics-taken op uw gegevens Cosmos DB uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="ef1b6-112">Deze zelfstudie wordt ervan uitgegaan dat u ervaring met Apache Hadoop, Hive en/of Pig hebt.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="ef1b6-113">Als u nieuwe tooApache Hadoop Hive en Pig, wordt aangeraden bezoeken Hallo [Apache Hadoop-documentatie][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="ef1b6-114">Deze zelfstudie wordt ervan uitgegaan dat u ervaring met Cosmos DB hebt en een Cosmos-DB-account hebben.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="ef1b6-115">Als u nieuwe tooCosmos DB of u geen een Cosmos-DB-account hebt, check onze [aan de slag] [ getting-started] pagina.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="ef1b6-116">Hebt u geen tijd toocomplete Hallo zelfstudie en alleen wilt tooget Hallo het volledige voorbeeld PowerShell-scripts voor Hive, Pig en MapReduce?</span><span class="sxs-lookup"><span data-stu-id="ef1b6-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="ef1b6-117">Geen probleem, ze [hier][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="ef1b6-118">Hallo download bevat ook Hallo hql, pig en java-bestanden voor deze voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="ef1b6-119"><a name="NewestVersion"></a>Meest recente versie</span><span class="sxs-lookup"><span data-stu-id="ef1b6-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="ef1b6-120">Versie van Hadoop-Connector</span><span class="sxs-lookup"><span data-stu-id="ef1b6-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="ef1b6-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="ef1b6-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="ef1b6-122">Script-Uri</span><span class="sxs-lookup"><span data-stu-id="ef1b6-122">Script Uri</span></span></th>
        <td><span data-ttu-id="ef1b6-123">https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="ef1b6-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="ef1b6-124">Datum gewijzigd</span><span class="sxs-lookup"><span data-stu-id="ef1b6-124">Date Modified</span></span></th>
        <td><span data-ttu-id="ef1b6-125">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="ef1b6-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="ef1b6-126">Ondersteunde HDInsight-versies</span><span class="sxs-lookup"><span data-stu-id="ef1b6-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="ef1b6-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="ef1b6-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="ef1b6-128">Wijzigingenlogboek</span><span class="sxs-lookup"><span data-stu-id="ef1b6-128">Change Log</span></span></th>
        <td><span data-ttu-id="ef1b6-129">Bijgewerkte Azure Cosmos DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="ef1b6-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="ef1b6-130">Toegevoegde ondersteuning voor gepartitioneerde verzamelingen op als een bron- en sink</span><span class="sxs-lookup"><span data-stu-id="ef1b6-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="ef1b6-131"><a name="Prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="ef1b6-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="ef1b6-132">Zorg ervoor dat u de volgende Hallo hebt voordat Hallo-instructies in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="ef1b6-133">Een Cosmos-DB-account, een database en een verzameling met documenten in.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="ef1b6-134">Zie voor meer informatie [aan de slag met Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="ef1b6-135">Voorbeeldgegevens importeren in uw account Cosmos DB Hello [Cosmos DB import-hulpprogramma][import-data].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="ef1b6-136">De doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-136">Throughput.</span></span> <span data-ttu-id="ef1b6-137">Leest en schrijft uit HDInsight naar uw toegewezen aanvraageenheden voor uw verzamelingen worden geteld.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="ef1b6-138">De uitvoer van capaciteit voor een aanvullende opgeslagen procedure binnen elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="ef1b6-139">Hallo opgeslagen procedures worden gebruikt voor het overdragen van de resulterende documenten.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="ef1b6-140">Capaciteit voor de resulterende documenten Hallo uit Hallo Hive, Pig of MapReduce-taken.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="ef1b6-141">[*Optioneel*] capaciteit voor een aanvullende verzameling.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="ef1b6-142">Tooavoid hello gemaakt van een nieuwe verzameling tijdens een Hallo taken, kunt u Hallo resultaten toostdout afdrukken, opslaan Hallo uitvoer tooyour WASB container of geef een bestaande verzameling op.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="ef1b6-143">In geval van het opgeven van een bestaande verzameling Hallo nieuwe documenten worden gemaakt in de verzameling Hallo en al bestaande documenten alleen worden beïnvloed als er een conflict in *id's*.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="ef1b6-144">**Hallo-connector wordt automatisch bestaande documenten overschreven met de ID-conflicten**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="ef1b6-145">U kunt deze functie uitschakelen door in te stellen Hallo upsert optie toofalse.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="ef1b6-146">Als upsert ingesteld op false is en een conflict optreedt, mislukt de Hallo Hadoop taak; een id conflict fout wordt gemeld.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="ef1b6-147"><a name="ProvisionHDInsight"></a>Stap 1: Maak een nieuw HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="ef1b6-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="ef1b6-148">Deze zelfstudie wordt scriptactie van hello Azure Portal toocustomize uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="ef1b6-149">In deze zelfstudie gebruiken we hello Azure Portal toocreate uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="ef1b6-150">Voor instructies over hoe toouse PowerShell-cmdlets of Hallo HDInsight .NET SDK, bekijk de [aanpassen HDInsight-clusters met behulp van de scriptactie] [ hdinsight-custom-provision] artikel.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="ef1b6-151">Meld u aan toohello [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="ef1b6-152">Klik op **+ nieuw** zoekt op Hallo bovenaan Hallo linkernavigatiebalk **HDInsight** in de bovenste zoekbalk Hallo op Hallo nieuwe blade.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="ef1b6-153">**HDInsight** gepubliceerd door **Microsoft** Hallo boven aan het Hallo-resultaten wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="ef1b6-154">Klik hierop en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="ef1b6-155">Blade op Hallo nieuwe HDInsight-Cluster te maken, Voer uw **clusternaam** en selecteer Hallo **abonnement** gewenste tooprovision deze bron op onder.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="ef1b6-156">Clusternaam</span><span class="sxs-lookup"><span data-stu-id="ef1b6-156">Cluster name</span></span></td><td><span data-ttu-id="ef1b6-157">Naam Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="ef1b6-158">DNS-naam moet beginnen en eindigen met een teken alfanumerieke en streepjes kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="ef1b6-159">Hallo-veld moet een tekenreeks tussen 3 en 63 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="ef1b6-160">De naam van abonnement</span><span class="sxs-lookup"><span data-stu-id="ef1b6-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="ef1b6-161">Als u meer dan één Azure-abonnement hebt, selecteert u Hallo-abonnement dat als voor uw HDInsight-cluster host fungeert.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="ef1b6-162">
5.Klik op **clustertype Selecteer** en set Hallo eigenschappen toohello na opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="ef1b6-163">Clustertype</span><span class="sxs-lookup"><span data-stu-id="ef1b6-163">Cluster type</span></span></td><td><span data-ttu-id="ef1b6-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="ef1b6-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="ef1b6-165">Cluster-laag</span><span class="sxs-lookup"><span data-stu-id="ef1b6-165">Cluster tier</span></span></td><td><span data-ttu-id="ef1b6-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="ef1b6-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="ef1b6-167">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="ef1b6-167">Operating System</span></span></td><td><span data-ttu-id="ef1b6-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="ef1b6-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="ef1b6-169">Versie</span><span class="sxs-lookup"><span data-stu-id="ef1b6-169">Version</span></span></td><td><span data-ttu-id="ef1b6-170">meest recente versie</span><span class="sxs-lookup"><span data-stu-id="ef1b6-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="ef1b6-171">Klik nu op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-171">Now, click **SELECT**.</span></span>

    ![Hadoop HDInsight initiële clusterdetails bieden][image-customprovision-page1]
6. <span data-ttu-id="ef1b6-173">Klik op **referenties** tooset uw aanmeldgegevens en referenties voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="ef1b6-174">Kies uw **Cluster aanmelding gebruikersnaam** en **aanmeldingswachtwoord Cluster**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="ef1b6-175">Als u wilt dat tooremote in uw cluster, selecteert u *Ja* Hallo Hallo blade onderaan in en geef een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="ef1b6-176">Klik op **gegevensbron** tooset uw primaire locatie voor gegevens openen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="ef1b6-177">Kies Hallo **selectiemethode** en geef een bestaand opslagaccount of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="ef1b6-178">Op dezelfde blade hello, geeft u een **standaard Container** en een **locatie**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="ef1b6-179">En klik op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef1b6-180">Selecteer een locatie sluiten tooyour Cosmos DB accountregio voor betere prestaties</span><span class="sxs-lookup"><span data-stu-id="ef1b6-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="ef1b6-181">Klik op **prijzen** tooselect Hallo aantal en type knooppunten.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="ef1b6-182">U kunt de standaardconfiguratie Hallo en schaal Hallo aantal Worker-knooppunten later op houden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="ef1b6-183">Klik op **optionele configuratie**, klikt u vervolgens **scriptacties** in Hallo optionele configuratie-Blade.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="ef1b6-184">Voer in scriptacties, Hallo informatie toocustomize te volgen in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="ef1b6-185">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ef1b6-185">Property</span></span></th><th><span data-ttu-id="ef1b6-186">Waarde</span><span class="sxs-lookup"><span data-stu-id="ef1b6-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="ef1b6-187">Naam</span><span class="sxs-lookup"><span data-stu-id="ef1b6-187">Name</span></span></td>
             <td><span data-ttu-id="ef1b6-188">Geef een naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="ef1b6-189">Script-URI</span><span class="sxs-lookup"><span data-stu-id="ef1b6-189">Script URI</span></span></td>
             <td><span data-ttu-id="ef1b6-190">Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="ef1b6-191">Voer in:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-191">Please enter:</span></span> </br> <span data-ttu-id="ef1b6-192"><strong>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="ef1b6-193">Kop</span><span class="sxs-lookup"><span data-stu-id="ef1b6-193">Head</span></span></td>
             <td><span data-ttu-id="ef1b6-194">Klik op Hallo selectievakje toorun Hallo PowerShell-script op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="ef1b6-195">
             <strong>Schakel dit selectievakje in</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="ef1b6-196">Werknemer</span><span class="sxs-lookup"><span data-stu-id="ef1b6-196">Worker</span></span></td>
             <td><span data-ttu-id="ef1b6-197">Klik op Hallo selectievakje toorun Hallo PowerShell-script op hello werkrolknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="ef1b6-198">
             <strong>Schakel dit selectievakje in</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="ef1b6-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="ef1b6-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="ef1b6-200">Klik op Hallo selectievakje toorun Hallo PowerShell-script op Hallo Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="ef1b6-201">
             <strong>Niet nodig</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="ef1b6-202">Parameters</span><span class="sxs-lookup"><span data-stu-id="ef1b6-202">Parameters</span></span></td>
             <td><span data-ttu-id="ef1b6-203">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="ef1b6-204">
             <strong>Er zijn geen Parameters nodig</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="ef1b6-205">
11.Maken van een nieuwe **resourcegroep** of gebruik een bestaande resourcegroep onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="ef1b6-206">12.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-206">12.</span></span> <span data-ttu-id="ef1b6-207">Controleer nu **pincode toodashboard** tootrack de implementatie en klik op **maken**!</span><span class="sxs-lookup"><span data-stu-id="ef1b6-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="ef1b6-208"><a name="InstallCmdlets"></a>Stap 2: Installeer en configureer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef1b6-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="ef1b6-209">Installeer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-209">Install Azure PowerShell.</span></span> <span data-ttu-id="ef1b6-210">Instructies hiervoor vindt u [hier][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef1b6-211">U kunt ook van HDInsight online Hive-Editor gebruiken voor Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="ef1b6-212">toohello toodo dus aanmelden [Azure Portal][azure-portal], klikt u op **HDInsight** op Hallo linkerdeelvenster tooview een lijst met uw HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="ef1b6-213">Klik op Hallo cluster u wilt toorun Hive-query's op en klik vervolgens op **Query Console**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="ef1b6-214">Open Azure PowerShell Integrated Scripting Environment Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="ef1b6-215">Op een computer met Windows 8 of WindowsServer 2012 of nieuwer, kunt u de ingebouwde Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="ef1b6-216">Typ vanuit het startscherm Hallo **powershell ise** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="ef1b6-217">Gebruik op een computer met een besturingssysteem dat ouder dan Windows 8 of Windows Server 2012, Hallo startmenu.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="ef1b6-218">Typ vanuit het startmenu hello, **opdrachtprompt** Hallo zoeken in en klik vervolgens in de lijst met resultaten hello, klikt u op **opdrachtprompt**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="ef1b6-219">Typ in het Hallo opdrachtprompt, **powershell_ise** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="ef1b6-220">Uw Azure-Account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="ef1b6-221">Typ in het Hallo-consolevenster, **Add-AzureAccount** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="ef1b6-222">Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="ef1b6-223">Typ in het Hallo-wachtwoord voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="ef1b6-224">Klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="ef1b6-225">Hallo volgende diagram identificeert Hallo belangrijke onderdelen van uw omgeving Azure PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagram voor Azure PowerShell][azure-powershell-diagram]

## <span data-ttu-id="ef1b6-227"><a name="RunHive"></a>Stap 3: Voer een Hive-taak met Cosmos DB en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef1b6-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ef1b6-228">Alle variabelen aangegeven door een combinatie moeten worden ingevuld met behulp van uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="ef1b6-229">Stel Hallo variabelen in het deelvenster van de PowerShell-Script te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="ef1b6-230">Laten we beginnen construeren van de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="ef1b6-231">We moet een Hive-query die wordt het systeem gegenereerde tijdstempels (_ts) en de unieke id's (_rid) uit een verzameling Azure Cosmos DB alle documenten, telt alle documenten van Hallo minuut en slaat vervolgens Hallo resultaten weer in een nieuwe Azure DB die Cosmos-verzameling schrijven.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="ef1b6-232">Eerst gaan we een Hive-tabel maken van onze Azure DB die Cosmos-verzameling.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="ef1b6-233">Hallo na code codefragment toohello deelvenster van de PowerShell-Script toevoegen <strong>nadat</strong> codefragment Hallo van #1.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="ef1b6-234">Zorg ervoor dat u Hallo optionele DocumentDB.query parameter t trim onze documenten toojust _ts en _rid.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="ef1b6-235">**Naamgeving van DocumentDB.inputCollections is niet een fout.**</span><span class="sxs-lookup"><span data-stu-id="ef1b6-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="ef1b6-236">Ja, kunnen we meerdere verzamelingen als invoer toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="ef1b6-237">Vervolgens maken we een Hive-tabel voor de verzameling van Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="ef1b6-238">Hallo uitvoer documenteigenschappen worden Hallo maand, dag, uur, minuut en Hallo kunt u het totale aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef1b6-239">**Naamgeving van DocumentDB.outputCollections was nog opnieuw niet een fout.**</span><span class="sxs-lookup"><span data-stu-id="ef1b6-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="ef1b6-240">Ja, kunnen we meerdere verzamelingen toe te voegen als uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="ef1b6-241">'*DocumentDB.outputCollections*'='*\<DocumentDB verzameling uitvoernaam 1\>*,*\<DocumentDB verzameling uitvoernaam 2\>* '</span><span class="sxs-lookup"><span data-stu-id="ef1b6-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="ef1b6-242">Hallo verzamelingsnamen worden zonder spaties, met slechts een enkele komma gescheiden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="ef1b6-243">Documenten worden gedistribueerde round robin in meerdere verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="ef1b6-244">Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="ef1b6-245">Tot slot uitvoer gaan we tally Hallo documenten per maand, dag, uur en minuut en insert Hallo resultaten weer in Hallo Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="ef1b6-246">Na het script codefragment toocreate de definitie van een Hive-taak uit de vorige query Hallo Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="ef1b6-247">U kunt ook Hallo - bestand overschakelen toospecify een scriptbestand HiveQL op HDFS.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="ef1b6-248">Na de begintijd van codefragment toosave Hallo Hallo toevoegen en het verzenden van Hallo Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="ef1b6-249">Hallo na toowait voor Hallo Hive-taak toocomplete toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="ef1b6-250">Toevoegen Hallo na tooprint Hallo standaard uitvoer en Hallo begin- en eindtijden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="ef1b6-251">**Voer** het nieuwe script!</span><span class="sxs-lookup"><span data-stu-id="ef1b6-251">**Run** your new script!</span></span> <span data-ttu-id="ef1b6-252">**Klik op** Hallo groene knop uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="ef1b6-253">Hallo resultaten controleren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-253">Check hello results.</span></span> <span data-ttu-id="ef1b6-254">Meld u aan bij Hallo [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="ef1b6-255">Klik op <strong>Bladeren</strong> op Hallo aan de linkerkant Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="ef1b6-256">Klik op <strong>Alles</strong> op Hallo rechtsboven van Hallo bladeren paneel.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="ef1b6-257">Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="ef1b6-258">Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de opgegeven de verzameling van de Hallo uitvoer uw Hive-query.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="ef1b6-259">Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="ef1b6-260">Hier ziet u Hallo resultaten van uw Hive-query.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-260">You will see hello results of your Hive query.</span></span>

   ![De resultaten van de hive-query][image-hive-query-results]

## <span data-ttu-id="ef1b6-262"><a name="RunPig"></a>Stap 4: Een Pig-taak met Cosmos DB en HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ef1b6-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ef1b6-263">Alle variabelen aangegeven door een combinatie moeten worden ingevuld met behulp van uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="ef1b6-264">Stel Hallo variabelen in het deelvenster van de PowerShell-Script te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="ef1b6-265">Laten we beginnen construeren van de queryreeks.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="ef1b6-266">We moet een Pig-query die wordt het systeem gegenereerde tijdstempels (_ts) en de unieke id's (_rid) uit een verzameling Azure Cosmos DB alle documenten, telt alle documenten van Hallo minuut en slaat vervolgens Hallo resultaten weer in een nieuwe Azure DB die Cosmos-verzameling schrijven.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="ef1b6-267">Documenten van de Cosmos-database eerst laden in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="ef1b6-268">Hallo na code codefragment toohello deelvenster van de PowerShell-Script toevoegen <strong>nadat</strong> codefragment Hallo van #1.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="ef1b6-269">Zorg ervoor dat een DocumentDB tooadd toohello optionele DocumentDB query parameter tootrim query onze documenten toojust _ts en _rid.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="ef1b6-270">Ja, kunnen we meerdere verzamelingen als invoer toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="ef1b6-271">'*\<DocumentDB verzameling invoernaam 1\>*,*\<DocumentDB verzameling invoernaam 2\>*'</span><span class="sxs-lookup"><span data-stu-id="ef1b6-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="ef1b6-272">Hallo verzamelingsnamen worden zonder spaties, met slechts een enkele komma gescheiden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="ef1b6-273">Documenten worden gedistribueerde round robin in meerdere verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="ef1b6-274">Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="ef1b6-275">Vervolgens laten we tally Hallo documenten door Hallo maand, dag, uur, minuut en Hallo kunt u het totale aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="ef1b6-276">Stel ten slotte Hallo resultaten opslaan in onze nieuwe uitvoer-verzameling.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef1b6-277">Ja, kunnen we meerdere verzamelingen toe te voegen als uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="ef1b6-278">'\<DocumentDB verzameling uitvoernaam 1\>,\<DocumentDB verzameling uitvoernaam 2\>'</span><span class="sxs-lookup"><span data-stu-id="ef1b6-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="ef1b6-279">Hallo verzamelingsnamen worden zonder spaties, met slechts een enkele komma gescheiden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="ef1b6-280">Documenten worden zijn gedistribueerde round robin via Hallo meerdere verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="ef1b6-281">Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="ef1b6-282">Na het script codefragment toocreate de definitie van een Pig-taak uit de vorige query Hallo Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="ef1b6-283">U kunt ook Hallo - bestand overschakelen toospecify een Pig-scriptbestand op HDFS.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="ef1b6-284">Na de begintijd van codefragment toosave Hallo Hallo toevoegen en het verzenden van Hallo Pig-taak.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="ef1b6-285">Hallo na toowait voor Hallo Pig-taak toocomplete toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="ef1b6-286">Toevoegen Hallo na tooprint Hallo standaard uitvoer en Hallo begin- en eindtijden.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="ef1b6-287">**Voer** het nieuwe script!</span><span class="sxs-lookup"><span data-stu-id="ef1b6-287">**Run** your new script!</span></span> <span data-ttu-id="ef1b6-288">**Klik op** Hallo groene knop uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="ef1b6-289">Hallo resultaten controleren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-289">Check hello results.</span></span> <span data-ttu-id="ef1b6-290">Meld u aan bij Hallo [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="ef1b6-291">Klik op <strong>Bladeren</strong> op Hallo aan de linkerkant Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="ef1b6-292">Klik op <strong>Alles</strong> op Hallo rechtsboven van Hallo bladeren paneel.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="ef1b6-293">Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="ef1b6-294">Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de opgegeven de verzameling van de Hallo uitvoer uw query Pig.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="ef1b6-295">Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="ef1b6-296">Hier ziet u Hallo resultaten van de Pig-query.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-296">You will see hello results of your Pig query.</span></span>

    ![Pig-queryresultaten][image-pig-query-results]

## <span data-ttu-id="ef1b6-298"><a name="RunMapReduce"></a>Stap 5: Een MapReduce-taak met behulp van Azure DB die Cosmos en HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ef1b6-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="ef1b6-299">Stel Hallo variabelen in het deelvenster van de PowerShell-Script te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="ef1b6-300">We je een MapReduce-taak die Hallo aantal exemplaren voor elke eigenschap van het Document uit de verzameling van uw Azure Cosmos DB telt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="ef1b6-301">In dit fragment script toevoegen **nadat** Hallo codefragment hierboven.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="ef1b6-302">TallyProperties v01.jar wordt geleverd met aangepaste installatie Hallo Hallo Cosmos DB Hadoop-Connector.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="ef1b6-303">Hallo na de opdracht toosubmit hello MapReduce-taak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="ef1b6-304">Bovendien toohello taakdefinitie MapReduce, u ook opgeven naam Hallo HDInsight cluster waar u toorun hello MapReduce-taak en Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="ef1b6-305">Hallo Start AzureHDInsightJob is een aanroep van asynchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="ef1b6-306">toocheck hello voltooiing van de taak hello, gebruik Hallo *wacht AzureHDInsightJob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="ef1b6-307">Hallo opdracht toocheck na of er fouten met actieve Hallo MapReduce-taak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="ef1b6-308">**Voer** het nieuwe script!</span><span class="sxs-lookup"><span data-stu-id="ef1b6-308">**Run** your new script!</span></span> <span data-ttu-id="ef1b6-309">**Klik op** Hallo groene knop uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="ef1b6-310">Hallo resultaten controleren.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-310">Check hello results.</span></span> <span data-ttu-id="ef1b6-311">Meld u aan bij Hallo [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="ef1b6-312">Klik op <strong>Bladeren</strong> op Hallo aan de linkerkant Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="ef1b6-313">Klik op <strong>Alles</strong> op Hallo rechtsboven van Hallo bladeren paneel.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="ef1b6-314">Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="ef1b6-315">Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de opgegeven de verzameling van de Hallo uitvoer uw MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="ef1b6-316">Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="ef1b6-317">Hier ziet u Hallo resultaten van de MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-317">You will see hello results of your MapReduce job.</span></span>

      ![MapReduce-queryresultaten][image-mapreduce-query-results]

## <span data-ttu-id="ef1b6-319"><a name="NextSteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef1b6-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="ef1b6-320">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-320">Congratulations!</span></span> <span data-ttu-id="ef1b6-321">U hebt zojuist uw eerste Hive, Pig en MapReduce-taken met behulp van Azure DB die Cosmos en HDInsight uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="ef1b6-322">We hebben onze Hadoop-Connector die afkomstig zijn geopend.</span><span class="sxs-lookup"><span data-stu-id="ef1b6-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="ef1b6-323">Als u geïnteresseerd bent, u kunt bijdragen op [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="ef1b6-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="ef1b6-324">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef1b6-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="ef1b6-325">[Een Java-toepassing met Documentdb ontwikkelen][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="ef1b6-326">[Het ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="ef1b6-327">[Aan de slag met Hadoop Hive in HDInsight tooanalyze mobiele telefoon gebruiken][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="ef1b6-328">[MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="ef1b6-329">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="ef1b6-330">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ef1b6-331">[HDInsight-clusters met behulp van de scriptactie aanpassen][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="ef1b6-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
