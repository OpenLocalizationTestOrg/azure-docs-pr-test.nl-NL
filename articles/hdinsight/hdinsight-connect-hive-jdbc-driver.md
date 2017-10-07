---
title: aaaQuery Hive via Hallo JDBC-stuurprogramma - Azure HDInsight | Microsoft Docs
description: Hallo JDBC-stuurprogramma van een Java-toepassing toosubmit Hive-query's tooHadoop op HDInsight gebruiken. Verbinding maken via een programma en van Hallo SQuirrel SQL-client.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Hive query via Hallo JDBC-stuurprogramma in HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Meer informatie over hoe toouse Hallo JDBC-stuurprogramma van een Java-toepassing toosubmit Hive query tooHadoop in Azure HDInsight. Hallo-informatie in dit document wordt gedemonstreerd hoe tooconnect programmatisch en van Hallo SQuirrel SQL-client.

Zie voor meer informatie over Hallo Hive JDBC Interface [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Vereisten

* Een Hadoop op HDInsight-cluster. Linux- of Windows clusters werkt.

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [HDInsight 3.3 buiten gebruik stellen](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL is een JDBC-clienttoepassing.

* Hallo [Java Developer Kit (JDK) versie 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger.

* [Apache Maven](https://maven.apache.org). Maven is een project bouwen voor Java-projecten-systeem dat wordt gebruikt door het Hallo-project die zijn gekoppeld aan dit artikel.

## <a name="jdbc-connection-string"></a>JDBC-verbindingsreeks

JDBC verbindingen tooan HDInsight-cluster in Azure dan 443 zijn aangebracht en Hallo verkeer is beveiligd met SSL. Hallo openbare gateway die Hallo clusters bevinden zich achter leidt Hallo verkeer toohello poort HiveServer2 daadwerkelijk luistert op. Hallo Hier volgt een voorbeeld-verbindingsreeks:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Vervang `CLUSTERNAME` met Hallo-naam van uw HDInsight-cluster.

## <a name="authentication"></a>Authentication

Bij het maken van Hallo verbinding, moet u Hallo HDInsight-cluster admin naam en het wachtwoord tooauthenticate toohello cluster gateway. Bij het verbinden van clients JDBC zoals SQuirreL SQL, moet u Hallo beheerder naam en het wachtwoord in de clientinstellingen.

Van een Java-toepassing moet u Hallo naam en het wachtwoord gebruiken wanneer een verbinding tot stand brengen. Bijvoorbeeld: hello volgende Java-code opent een nieuwe verbinding met de verbindingsreeks hello, admin-naam en wachtwoord:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Verbinding maken met SQuirreL SQL-client

SQuirreL SQL is een JDBC-client die gebruikt tooremotely uitvoeren Hive-query's met uw HDInsight-cluster worden kan. Hallo volgende stappen wordt ervan uitgegaan dat u SQuirreL SQL al hebt geïnstalleerd.

1. Kopieer Hallo Hive JDBC-stuurprogramma's van uw HDInsight-cluster.

    * Voor **Linux gebaseerde HDInsight**, gebruik Hallo volgende stappen uit toodownload Hallo vereist jar-bestanden.

        1. Maak een map die Hallo bestanden bevat. Bijvoorbeeld `mkdir hivedriver`.

        2. Gebruik Hallo volgende opdrachten vanaf een opdrachtregel toocopy Hallo-bestanden van Hallo HDInsight-cluster:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Vervang `USERNAME` met Hallo SSH gebruikersaccountnaam voor Hallo-cluster. Vervang `CLUSTERNAME` met de naam van een Hallo HDInsight-cluster.

    * Voor **HDInsight op basis van Windows**, gebruik Hallo volgende stappen uit toodownload Hallo jar-bestanden.

        1. In hello Azure-portal, selecteer uw HDInsight-cluster en selecteer vervolgens Hallo **extern bureaublad** pictogram.

            ![Pictogram voor extern bureaublad](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Gebruik op Hallo extern bureaublad-blade Hallo **Connect** knop tooconnect toohello cluster. Als Hallo extern bureaublad is niet ingeschakeld, gebruik Hallo formulier tooprovide een gebruikersnaam en wachtwoord en selecteer vervolgens **inschakelen** tooenable extern bureaublad voor Hallo-cluster.

            ![Extern bureaublad-blade](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Na het selecteren van **Connect**, een RDP-bestand wordt gedownload. Dit bestand toolaunch Hallo extern bureaublad-client gebruiken. Wanneer u wordt gevraagd, gebruiken Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven voor toegang tot extern bureaublad.

        3. Eenmaal zijn verbonden, kopieert u Hallo volgende bestanden van Hallo extern bureaublad-sessie tooyour lokale computer. Plaatsen in een lokale map met de naam `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-JDBC-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > Hallo versie cijfers die zijn opgenomen in het Hallo-paden en bestandsnamen kunnen afwijken voor uw cluster.

        4. Verbinding verbreken Hallo extern bureaublad-sessie wanneer u klaar bent met het Hallo-bestanden zijn gekopieerd.

2. Hallo SQuirreL SQL toepassing starten. Selecteer Hallo linksonder Hallo venster **stuurprogramma's**.

    ![Tabblad stuurprogramma's aan de linkerkant Hallo van Hallo-venster](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Van pictogrammen bovenaan Hallo HALLO hallo **stuurprogramma's** dialoogvenster, selecteer Hallo  **+**  pictogram toocreate een stuurprogramma.

    ![Stuurprogramma's pictogrammen](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. In het dialoogvenster Hallo stuurprogramma toevoegen toevoegen Hallo volgende informatie:

    * **Naam**: Hive
    * **Voorbeeld-URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Extra klassepad**: gebruik Hallo toevoegen knop tooadd Hallo jar-bestanden eerder hebt gedownload
    * **Klassenaam**: org.apache.hive.jdbc.HiveDriver

   ![stuurprogramma-dialoogvenster toevoegen](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Klik op **OK** toosave deze instellingen.

5. Selecteer op Hallo links van Hallo SQuirreL SQL-venster, **aliassen**. Klik vervolgens op Hallo  **+**  pictogram toocreate een alias voor een verbinding.

    ![nieuwe alias toevoegen](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Gebruik Hallo volgende waarden voor Hallo **Alias toevoegen** dialoogvenster.

    * **Naam**: Hive in HDInsight

    * **Stuurprogramma**: gebruik Hallo dropdown tooselect hello **Hive** stuurprogramma

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.

    * **Gebruikersnaam**: Hallo cluster account aanmeldingsnaam voor uw HDInsight-cluster. Hallo standaardwaarde is `admin`.

    * **Wachtwoord**: Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.

 ![dialoogvenster alias toevoegen](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Gebruik Hallo **Test** knop tooverify die Hallo verbinding werkt. Wanneer **verbinding maken met: Hive in HDInsight** dialoogvenster wordt weergegeven, selecteert u **Connect** tooperform Hallo test. Als het Hallo-test is geslaagd, ziet u een **verbinding tot stand gebracht** dialoogvenster.

    toosave hello verbinding gebruik alias, Hallo **Ok** knop onderin Hallo Hallo **Alias toevoegen** dialoogvenster.

7. Van Hallo **verbinding maken met** vervolgkeuzelijst bovenaan Hallo SQuirreL SQL, selecteer **Hive in HDInsight**. Wanneer u wordt gevraagd, selecteert u **Connect**.

    ![het dialoogvenster voor verbinding](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Eenmaal zijn verbonden, Voer Hallo volgende query uitvoeren op dialoogvenster Hallo SQL-query's en selecteer vervolgens Hallo **uitvoeren** pictogram. Hallo resultatengebied Hallo resultaten van Hallo query moet worden weergegeven.

        select * from hivesampletable limit 10;

    ![dialoogvenster voor SQL query's, met inbegrip van resultaten](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Verbinding maken vanaf een voorbeeld van Java-toepassing

Een voorbeeld van het gebruik van een Java-client tooquery Hive in HDInsight is beschikbaar op [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Volg de instructies Hallo in Hallo opslagplaats toobuild en Hallo-voorbeeld uitvoeren.

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Is een onverwachte fout opgetreden tijdens het tooopen een SQL-verbinding

**Symptomen**: wanneer u verbinding maakt tooan HDInsight-cluster die versie 3.3 of 3.4, verschijnt er een fout die is een onverwachte fout opgetreden. Hallo stacktracering voor deze fout begint met de Hallo volgende regels:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Oorzaak**: deze fout wordt veroorzaakt door een niet-overeenkomend in Hallo-versie van Hallo commons codec.jar bestand gebruikt door SQuirreL en Hallo vereist door Hallo JDBC Hive-onderdelen.

**Resolutie**: toofix deze fout, gebruik Hallo volgende stappen:

1. Hallo commons codec jar-bestand downloaden van uw HDInsight-cluster.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. SQuirreL sluiten en gaat u toohello directory waar SQuirreL op uw systeem is geïnstalleerd. In Hallo SquirreL map onder Hallo `lib` directory, vervangen Hallo bestaande commons-codec.jar Hello een gedownload van Hallo HDInsight-cluster.

3. Opnieuw opstarten SQuirreL. Hallo fout kan niet meer optreden bij het verbinden van tooHive op HDInsight.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse JDBC toowork met Hive, gebruik Hallo volgen koppelingen tooexplore andere manieren toowork met Azure HDInsight.

* [Uploaden van gegevens tooHDInsight](hdinsight-upload-data.md)
* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce-taken gebruiken met HDInsight](hdinsight-use-mapreduce.md)
