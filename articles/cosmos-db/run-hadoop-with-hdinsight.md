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
# <a name="Azure Cosmos DB-HDInsight"></a>Voer een Apache Hive, Pig of Hadoop met behulp van Azure DB die Cosmos en HDInsight
Deze zelfstudie leert u hoe toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], en [Apache Hadoop] [ apache-hadoop] MapReduce-taken in Azure HDInsight met Hadoop-connector Cosmos-database. Cosmos DB van Hadoop-connector kunt Cosmos DB tooact als een bron- en sink voor Hive, Pig en MapReduce-taken. Deze zelfstudie gebruikt Cosmos DB Hallo gegevensbron en bestemming voor Hadoop-taken.

Na het voltooien van deze zelfstudie, moet u kunnen tooanswer Hallo vragen te volgen:

* Hoe ik gegevens laden van de Cosmos-database met behulp van een Hive, Pig of MapReduce-taak?
* Hoe kan ik gegevens opslaan in Cosmos-database met behulp van een Hive, Pig of MapReduce-taak?

Het is raadzaam om aan de slag door bekijkt hello volgende video waar we uitvoeren via een met behulp van de Cosmos-DB en HDInsight Hive-taak.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

Keer vervolgens terug toothis artikel, waarin u ontvangt Hallo volledige details over hoe u analytics-taken op uw gegevens Cosmos DB uitvoeren kunt.

> [!TIP]
> Deze zelfstudie wordt ervan uitgegaan dat u ervaring met Apache Hadoop, Hive en/of Pig hebt. Als u nieuwe tooApache Hadoop Hive en Pig, wordt aangeraden bezoeken Hallo [Apache Hadoop-documentatie][apache-hadoop-doc]. Deze zelfstudie wordt ervan uitgegaan dat u ervaring met Cosmos DB hebt en een Cosmos-DB-account hebben. Als u nieuwe tooCosmos DB of u geen een Cosmos-DB-account hebt, check onze [aan de slag] [ getting-started] pagina.
>
>

Hebt u geen tijd toocomplete Hallo zelfstudie en alleen wilt tooget Hallo het volledige voorbeeld PowerShell-scripts voor Hive, Pig en MapReduce? Geen probleem, ze [hier][hdinsight-samples]. Hallo download bevat ook Hallo hql, pig en java-bestanden voor deze voorbeelden.

## <a name="NewestVersion"></a>Meest recente versie
<table border='1'>
    <tr><th>Versie van Hadoop-Connector</th>
        <td>1.2.0</td></tr>
    <tr><th>Script-Uri</th>
        <td>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</td></tr>
    <tr><th>Datum gewijzigd</th>
        <td>04/26/2016</td></tr>
    <tr><th>Ondersteunde HDInsight-versies</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>Wijzigingenlogboek</th>
        <td>Bijgewerkte Azure Cosmos DB Java SDK too1.6.0</br>
            Toegevoegde ondersteuning voor gepartitioneerde verzamelingen op als een bron- en sink</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Vereisten
Zorg ervoor dat u de volgende Hallo hebt voordat Hallo-instructies in deze zelfstudie:

* Een Cosmos-DB-account, een database en een verzameling met documenten in. Zie voor meer informatie [aan de slag met Cosmos DB][getting-started]. Voorbeeldgegevens importeren in uw account Cosmos DB Hello [Cosmos DB import-hulpprogramma][import-data].
* De doorvoer. Leest en schrijft uit HDInsight naar uw toegewezen aanvraageenheden voor uw verzamelingen worden geteld.
* De uitvoer van capaciteit voor een aanvullende opgeslagen procedure binnen elke verzameling. Hallo opgeslagen procedures worden gebruikt voor het overdragen van de resulterende documenten.
* Capaciteit voor de resulterende documenten Hallo uit Hallo Hive, Pig of MapReduce-taken.
* [*Optioneel*] capaciteit voor een aanvullende verzameling.

> [!WARNING]
> Tooavoid hello gemaakt van een nieuwe verzameling tijdens een Hallo taken, kunt u Hallo resultaten toostdout afdrukken, opslaan Hallo uitvoer tooyour WASB container of geef een bestaande verzameling op. In geval van het opgeven van een bestaande verzameling Hallo nieuwe documenten worden gemaakt in de verzameling Hallo en al bestaande documenten alleen worden beïnvloed als er een conflict in *id's*. **Hallo-connector wordt automatisch bestaande documenten overschreven met de ID-conflicten**. U kunt deze functie uitschakelen door in te stellen Hallo upsert optie toofalse. Als upsert ingesteld op false is en een conflict optreedt, mislukt de Hallo Hadoop taak; een id conflict fout wordt gemeld.
>
>

## <a name="ProvisionHDInsight"></a>Stap 1: Maak een nieuw HDInsight-cluster
Deze zelfstudie wordt scriptactie van hello Azure Portal toocustomize uw HDInsight-cluster. In deze zelfstudie gebruiken we hello Azure Portal toocreate uw HDInsight-cluster. Voor instructies over hoe toouse PowerShell-cmdlets of Hallo HDInsight .NET SDK, bekijk de [aanpassen HDInsight-clusters met behulp van de scriptactie] [ hdinsight-custom-provision] artikel.

1. Meld u aan toohello [Azure Portal][azure-portal].
2. Klik op **+ nieuw** zoekt op Hallo bovenaan Hallo linkernavigatiebalk **HDInsight** in de bovenste zoekbalk Hallo op Hallo nieuwe blade.
3. **HDInsight** gepubliceerd door **Microsoft** Hallo boven aan het Hallo-resultaten wordt weergegeven. Klik hierop en klik vervolgens op **maken**.
4. Blade op Hallo nieuwe HDInsight-Cluster te maken, Voer uw **clusternaam** en selecteer Hallo **abonnement** gewenste tooprovision deze bron op onder.

    <table border='1'>
        <tr><td>Clusternaam</td><td>Naam Hallo-cluster.<br/>
DNS-naam moet beginnen en eindigen met een teken alfanumerieke en streepjes kan bevatten.<br/>
Hallo-veld moet een tekenreeks tussen 3 en 63 tekens lang zijn.</td></tr>
        <tr><td>De naam van abonnement</td>
            <td>Als u meer dan één Azure-abonnement hebt, selecteert u Hallo-abonnement dat als voor uw HDInsight-cluster host fungeert. </td></tr>
    </table>
5.Klik op **clustertype Selecteer** en set Hallo eigenschappen toohello na opgegeven waarden.

    <table border='1'>
        <tr><td>Clustertype</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Cluster-laag</td><td><strong>Standard</strong></td></tr>
        <tr><td>Besturingssysteem</td><td><strong>Windows</strong></td></tr>
        <tr><td>Versie</td><td>meest recente versie</td></tr>
    </table>

    Klik nu op **Selecteer**.

    ![Hadoop HDInsight initiële clusterdetails bieden][image-customprovision-page1]
6. Klik op **referenties** tooset uw aanmeldgegevens en referenties voor externe toegang. Kies uw **Cluster aanmelding gebruikersnaam** en **aanmeldingswachtwoord Cluster**.

    Als u wilt dat tooremote in uw cluster, selecteert u *Ja* Hallo Hallo blade onderaan in en geef een gebruikersnaam en wachtwoord.
7. Klik op **gegevensbron** tooset uw primaire locatie voor gegevens openen. Kies Hallo **selectiemethode** en geef een bestaand opslagaccount of maak een nieuwe.
8. Op dezelfde blade hello, geeft u een **standaard Container** en een **locatie**. En klik op **Selecteer**.

   > [!NOTE]
   > Selecteer een locatie sluiten tooyour Cosmos DB accountregio voor betere prestaties
   >
   >
9. Klik op **prijzen** tooselect Hallo aantal en type knooppunten. U kunt de standaardconfiguratie Hallo en schaal Hallo aantal Worker-knooppunten later op houden.
10. Klik op **optionele configuratie**, klikt u vervolgens **scriptacties** in Hallo optionele configuratie-Blade.

     Voer in scriptacties, Hallo informatie toocustomize te volgen in uw HDInsight-cluster.

     <table border='1'>
         <tr><th>Eigenschap</th><th>Waarde</th></tr>
         <tr><td>Naam</td>
             <td>Geef een naam voor de scriptactie Hallo.</td></tr>
         <tr><td>Script-URI</td>
             <td>Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster.</br></br>
Voer in: </br> <strong>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</strong>.</td></tr>
         <tr><td>Kop</td>
             <td>Klik op Hallo selectievakje toorun Hallo PowerShell-script op Hallo hoofdknooppunt.</br></br>
             <strong>Schakel dit selectievakje in</strong>.</td></tr>
         <tr><td>Werknemer</td>
             <td>Klik op Hallo selectievakje toorun Hallo PowerShell-script op hello werkrolknooppunt.</br></br>
             <strong>Schakel dit selectievakje in</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Klik op Hallo selectievakje toorun Hallo PowerShell-script op Hallo Zookeeper.</br></br>
             <strong>Niet nodig</strong>.
             </td></tr>
         <tr><td>Parameters</td>
             <td>Geef parameters op Hallo, indien vereist door het Hallo-script.</br></br>
             <strong>Er zijn geen Parameters nodig</strong>.</td></tr>
     </table>
11.Maken van een nieuwe **resourcegroep** of gebruik een bestaande resourcegroep onder uw Azure-abonnement.
12. Controleer nu **pincode toodashboard** tootrack de implementatie en klik op **maken**!

## <a name="InstallCmdlets"></a>Stap 2: Installeer en configureer Azure PowerShell
1. Installeer Azure PowerShell. Instructies hiervoor vindt u [hier][powershell-install-configure].

   > [!NOTE]
   > U kunt ook van HDInsight online Hive-Editor gebruiken voor Hive-query's. toohello toodo dus aanmelden [Azure Portal][azure-portal], klikt u op **HDInsight** op Hallo linkerdeelvenster tooview een lijst met uw HDInsight-clusters. Klik op Hallo cluster u wilt toorun Hive-query's op en klik vervolgens op **Query Console**.
   >
   >
2. Open Azure PowerShell Integrated Scripting Environment Hallo:

   * Op een computer met Windows 8 of WindowsServer 2012 of nieuwer, kunt u de ingebouwde Hallo zoeken. Typ vanuit het startscherm Hallo **powershell ise** en klik op **Enter**.
   * Gebruik op een computer met een besturingssysteem dat ouder dan Windows 8 of Windows Server 2012, Hallo startmenu. Typ vanuit het startmenu hello, **opdrachtprompt** Hallo zoeken in en klik vervolgens in de lijst met resultaten hello, klikt u op **opdrachtprompt**. Typ in het Hallo opdrachtprompt, **powershell_ise** en klik op **Enter**.
3. Uw Azure-Account toevoegen.

   1. Typ in het Hallo-consolevenster, **Add-AzureAccount** en klik op **Enter**.
   2. Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.
   3. Typ in het Hallo-wachtwoord voor uw Azure-abonnement.
   4. Klik op **aanmelden**.
4. Hallo volgende diagram identificeert Hallo belangrijke onderdelen van uw omgeving Azure PowerShell-scripts.

    ![Diagram voor Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Stap 3: Voer een Hive-taak met Cosmos DB en HDInsight
> [!IMPORTANT]
> Alle variabelen aangegeven door een combinatie moeten worden ingevuld met behulp van uw configuratie-instellingen.
>
>

1. Stel Hallo variabelen in het deelvenster van de PowerShell-Script te volgen.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Laten we beginnen construeren van de queryreeks. We moet een Hive-query die wordt het systeem gegenereerde tijdstempels (_ts) en de unieke id's (_rid) uit een verzameling Azure Cosmos DB alle documenten, telt alle documenten van Hallo minuut en slaat vervolgens Hallo resultaten weer in een nieuwe Azure DB die Cosmos-verzameling schrijven.</p>

    <p>Eerst gaan we een Hive-tabel maken van onze Azure DB die Cosmos-verzameling. Hallo na code codefragment toohello deelvenster van de PowerShell-Script toevoegen <strong>nadat</strong> codefragment Hallo van #1. Zorg ervoor dat u Hallo optionele DocumentDB.query parameter t trim onze documenten toojust _ts en _rid.</p>

   > [!NOTE]
   > **Naamgeving van DocumentDB.inputCollections is niet een fout.** Ja, kunnen we meerdere verzamelingen als invoer toe te voegen: </br>
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

1. Vervolgens maken we een Hive-tabel voor de verzameling van Hallo uitvoer. Hallo uitvoer documenteigenschappen worden Hallo maand, dag, uur, minuut en Hallo kunt u het totale aantal exemplaren.

   > [!NOTE]
   > **Naamgeving van DocumentDB.outputCollections was nog opnieuw niet een fout.** Ja, kunnen we meerdere verzamelingen toe te voegen als uitvoer: </br>
   > '*DocumentDB.outputCollections*'='*\<DocumentDB verzameling uitvoernaam 1\>*,*\<DocumentDB verzameling uitvoernaam 2\>* ' </br> Hallo verzamelingsnamen worden zonder spaties, met slechts een enkele komma gescheiden. </br></br>
   > Documenten worden gedistribueerde round robin in meerdere verzamelingen. Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling hello, enzovoort.
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
2. Tot slot uitvoer gaan we tally Hallo documenten per maand, dag, uur en minuut en insert Hallo resultaten weer in Hallo Hive-tabel.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Na het script codefragment toocreate de definitie van een Hive-taak uit de vorige query Hallo Hallo toevoegen.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    U kunt ook Hallo - bestand overschakelen toospecify een scriptbestand HiveQL op HDFS.
4. Na de begintijd van codefragment toosave Hallo Hallo toevoegen en het verzenden van Hallo Hive-taak.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Hallo na toowait voor Hallo Hive-taak toocomplete toevoegen.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Toevoegen Hallo na tooprint Hallo standaard uitvoer en Hallo begin- en eindtijden.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Voer** het nieuwe script! **Klik op** Hallo groene knop uitvoeren.
8. Hallo resultaten controleren. Meld u aan bij Hallo [Azure Portal][azure-portal].

   1. Klik op <strong>Bladeren</strong> op Hallo aan de linkerkant Configuratiescherm. </br>
   2. Klik op <strong>Alles</strong> op Hallo rechtsboven van Hallo bladeren paneel. </br>
   3. Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>. </br>
   4. Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de opgegeven de verzameling van de Hallo uitvoer uw Hive-query.</br>
   5. Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</br></p>

   Hier ziet u Hallo resultaten van uw Hive-query.

   ![De resultaten van de hive-query][image-hive-query-results]

## <a name="RunPig"></a>Stap 4: Een Pig-taak met Cosmos DB en HDInsight uitvoeren
> [!IMPORTANT]
> Alle variabelen aangegeven door een combinatie moeten worden ingevuld met behulp van uw configuratie-instellingen.
>
>

1. Stel Hallo variabelen in het deelvenster van de PowerShell-Script te volgen.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Laten we beginnen construeren van de queryreeks. We moet een Pig-query die wordt het systeem gegenereerde tijdstempels (_ts) en de unieke id's (_rid) uit een verzameling Azure Cosmos DB alle documenten, telt alle documenten van Hallo minuut en slaat vervolgens Hallo resultaten weer in een nieuwe Azure DB die Cosmos-verzameling schrijven.</p>
    <p>Documenten van de Cosmos-database eerst laden in HDInsight. Hallo na code codefragment toohello deelvenster van de PowerShell-Script toevoegen <strong>nadat</strong> codefragment Hallo van #1. Zorg ervoor dat een DocumentDB tooadd toohello optionele DocumentDB query parameter tootrim query onze documenten toojust _ts en _rid.</p>

   > [!NOTE]
   > Ja, kunnen we meerdere verzamelingen als invoer toe te voegen: </br>
   > '*\<DocumentDB verzameling invoernaam 1\>*,*\<DocumentDB verzameling invoernaam 2\>*'</br> Hallo verzamelingsnamen worden zonder spaties, met slechts een enkele komma gescheiden. </b>
   >
   >

    Documenten worden gedistribueerde round robin in meerdere verzamelingen. Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling hello, enzovoort.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Vervolgens laten we tally Hallo documenten door Hallo maand, dag, uur, minuut en Hallo kunt u het totale aantal exemplaren.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Stel ten slotte Hallo resultaten opslaan in onze nieuwe uitvoer-verzameling.

   > [!NOTE]
   > Ja, kunnen we meerdere verzamelingen toe te voegen als uitvoer: </br>
   > '\<DocumentDB verzameling uitvoernaam 1\>,\<DocumentDB verzameling uitvoernaam 2\>'</br> Hallo verzamelingsnamen worden zonder spaties, met slechts een enkele komma gescheiden.</br>
   > Documenten worden zijn gedistribueerde round robin via Hallo meerdere verzamelingen. Een batch van documenten worden opgeslagen in één verzameling en vervolgens een tweede reeks documenten worden opgeslagen in de volgende verzameling hello, enzovoort.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Na het script codefragment toocreate de definitie van een Pig-taak uit de vorige query Hallo Hallo toevoegen.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    U kunt ook Hallo - bestand overschakelen toospecify een Pig-scriptbestand op HDFS.
6. Na de begintijd van codefragment toosave Hallo Hallo toevoegen en het verzenden van Hallo Pig-taak.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Hallo na toowait voor Hallo Pig-taak toocomplete toevoegen.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Toevoegen Hallo na tooprint Hallo standaard uitvoer en Hallo begin- en eindtijden.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Voer** het nieuwe script! **Klik op** Hallo groene knop uitvoeren.
10. Hallo resultaten controleren. Meld u aan bij Hallo [Azure Portal][azure-portal].

    1. Klik op <strong>Bladeren</strong> op Hallo aan de linkerkant Configuratiescherm. </br>
    2. Klik op <strong>Alles</strong> op Hallo rechtsboven van Hallo bladeren paneel. </br>
    3. Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>. </br>
    4. Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de opgegeven de verzameling van de Hallo uitvoer uw query Pig.</br>
    5. Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.</br></p>

    Hier ziet u Hallo resultaten van de Pig-query.

    ![Pig-queryresultaten][image-pig-query-results]

## <a name="RunMapReduce"></a>Stap 5: Een MapReduce-taak met behulp van Azure DB die Cosmos en HDInsight uitvoeren
1. Stel Hallo variabelen in het deelvenster van de PowerShell-Script te volgen.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. We je een MapReduce-taak die Hallo aantal exemplaren voor elke eigenschap van het Document uit de verzameling van uw Azure Cosmos DB telt uitvoeren. In dit fragment script toevoegen **nadat** Hallo codefragment hierboven.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar wordt geleverd met aangepaste installatie Hallo Hallo Cosmos DB Hadoop-Connector.
   >
   >
3. Hallo na de opdracht toosubmit hello MapReduce-taak toevoegen.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Bovendien toohello taakdefinitie MapReduce, u ook opgeven naam Hallo HDInsight cluster waar u toorun hello MapReduce-taak en Hallo-referenties. Hallo Start AzureHDInsightJob is een aanroep van asynchrone uitvoering. toocheck hello voltooiing van de taak hello, gebruik Hallo *wacht AzureHDInsightJob* cmdlet.
4. Hallo opdracht toocheck na of er fouten met actieve Hallo MapReduce-taak toevoegen.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Voer** het nieuwe script! **Klik op** Hallo groene knop uitvoeren.
6. Hallo resultaten controleren. Meld u aan bij Hallo [Azure Portal][azure-portal].

   1. Klik op <strong>Bladeren</strong> op Hallo aan de linkerkant Configuratiescherm.
   2. Klik op <strong>Alles</strong> op Hallo rechtsboven van Hallo bladeren paneel.
   3. Zoek en klik op <strong>Azure Cosmos DB Accounts</strong>.
   4. Zoek vervolgens uw <strong>Azure Cosmos-DB Account</strong>, klikt u vervolgens <strong>Azure Cosmos DB Database</strong> en uw <strong>Azure Cosmos DB verzameling</strong> die zijn gekoppeld aan de opgegeven de verzameling van de Hallo uitvoer uw MapReduce-taak.
   5. Tot slot op <strong>documentverkenner</strong> onder <strong>hulpprogramma's voor ontwikkelaars</strong>.

      Hier ziet u Hallo resultaten van de MapReduce-taak.

      ![MapReduce-queryresultaten][image-mapreduce-query-results]

## <a name="NextSteps"></a>Volgende stappen
Gefeliciteerd. U hebt zojuist uw eerste Hive, Pig en MapReduce-taken met behulp van Azure DB die Cosmos en HDInsight uitgevoerd.

We hebben onze Hadoop-Connector die afkomstig zijn geopend. Als u geïnteresseerd bent, u kunt bijdragen op [GitHub][github].

toolearn Zie meer Hallo artikelen te volgen:

* [Een Java-toepassing met Documentdb ontwikkelen][documentdb-java-application]
* [Het ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]
* [Aan de slag met Hadoop Hive in HDInsight tooanalyze mobiele telefoon gebruiken][hdinsight-get-started]
* [MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [HDInsight-clusters met behulp van de scriptactie aanpassen][hdinsight-hadoop-customize-cluster]

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
