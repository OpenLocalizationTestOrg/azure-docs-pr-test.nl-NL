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
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="8d73c-104">Hive query via Hallo JDBC-stuurprogramma in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d73c-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="8d73c-105">Meer informatie over hoe toouse Hallo JDBC-stuurprogramma van een Java-toepassing toosubmit Hive query tooHadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d73c-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="8d73c-106">Hallo-informatie in dit document wordt gedemonstreerd hoe tooconnect programmatisch en van Hallo SQuirrel SQL-client.</span><span class="sxs-lookup"><span data-stu-id="8d73c-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="8d73c-107">Zie voor meer informatie over Hallo Hive JDBC Interface [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="8d73c-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d73c-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d73c-108">Prerequisites</span></span>

* <span data-ttu-id="8d73c-109">Een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="8d73c-110">Linux- of Windows clusters werkt.</span><span class="sxs-lookup"><span data-stu-id="8d73c-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8d73c-111">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8d73c-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8d73c-112">Zie voor meer informatie [HDInsight 3.3 buiten gebruik stellen](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8d73c-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8d73c-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="8d73c-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="8d73c-114">SQuirreL is een JDBC-clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="8d73c-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="8d73c-115">Hallo [Java Developer Kit (JDK) versie 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger.</span><span class="sxs-lookup"><span data-stu-id="8d73c-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="8d73c-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="8d73c-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="8d73c-117">Maven is een project bouwen voor Java-projecten-systeem dat wordt gebruikt door het Hallo-project die zijn gekoppeld aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8d73c-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="8d73c-118">JDBC-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="8d73c-118">JDBC connection string</span></span>

<span data-ttu-id="8d73c-119">JDBC verbindingen tooan HDInsight-cluster in Azure dan 443 zijn aangebracht en Hallo verkeer is beveiligd met SSL.</span><span class="sxs-lookup"><span data-stu-id="8d73c-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="8d73c-120">Hallo openbare gateway die Hallo clusters bevinden zich achter leidt Hallo verkeer toohello poort HiveServer2 daadwerkelijk luistert op.</span><span class="sxs-lookup"><span data-stu-id="8d73c-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="8d73c-121">Hallo Hier volgt een voorbeeld-verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="8d73c-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="8d73c-122">Vervang `CLUSTERNAME` met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="8d73c-123">Authentication</span><span class="sxs-lookup"><span data-stu-id="8d73c-123">Authentication</span></span>

<span data-ttu-id="8d73c-124">Bij het maken van Hallo verbinding, moet u Hallo HDInsight-cluster admin naam en het wachtwoord tooauthenticate toohello cluster gateway.</span><span class="sxs-lookup"><span data-stu-id="8d73c-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="8d73c-125">Bij het verbinden van clients JDBC zoals SQuirreL SQL, moet u Hallo beheerder naam en het wachtwoord in de clientinstellingen.</span><span class="sxs-lookup"><span data-stu-id="8d73c-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="8d73c-126">Van een Java-toepassing moet u Hallo naam en het wachtwoord gebruiken wanneer een verbinding tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="8d73c-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="8d73c-127">Bijvoorbeeld: hello volgende Java-code opent een nieuwe verbinding met de verbindingsreeks hello, admin-naam en wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="8d73c-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="8d73c-128">Verbinding maken met SQuirreL SQL-client</span><span class="sxs-lookup"><span data-stu-id="8d73c-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="8d73c-129">SQuirreL SQL is een JDBC-client die gebruikt tooremotely uitvoeren Hive-query's met uw HDInsight-cluster worden kan.</span><span class="sxs-lookup"><span data-stu-id="8d73c-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="8d73c-130">Hallo volgende stappen wordt ervan uitgegaan dat u SQuirreL SQL al hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8d73c-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="8d73c-131">Kopieer Hallo Hive JDBC-stuurprogramma's van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="8d73c-132">Voor **Linux gebaseerde HDInsight**, gebruik Hallo volgende stappen uit toodownload Hallo vereist jar-bestanden.</span><span class="sxs-lookup"><span data-stu-id="8d73c-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="8d73c-133">Maak een map die Hallo bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="8d73c-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="8d73c-134">Bijvoorbeeld `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="8d73c-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="8d73c-135">Gebruik Hallo volgende opdrachten vanaf een opdrachtregel toocopy Hallo-bestanden van Hallo HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="8d73c-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="8d73c-136">Vervang `USERNAME` met Hallo SSH gebruikersaccountnaam voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="8d73c-137">Vervang `CLUSTERNAME` met de naam van een Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="8d73c-138">Voor **HDInsight op basis van Windows**, gebruik Hallo volgende stappen uit toodownload Hallo jar-bestanden.</span><span class="sxs-lookup"><span data-stu-id="8d73c-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="8d73c-139">In hello Azure-portal, selecteer uw HDInsight-cluster en selecteer vervolgens Hallo **extern bureaublad** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d73c-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Pictogram voor extern bureaublad](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="8d73c-141">Gebruik op Hallo extern bureaublad-blade Hallo **Connect** knop tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="8d73c-142">Als Hallo extern bureaublad is niet ingeschakeld, gebruik Hallo formulier tooprovide een gebruikersnaam en wachtwoord en selecteer vervolgens **inschakelen** tooenable extern bureaublad voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Extern bureaublad-blade](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="8d73c-144">Na het selecteren van **Connect**, een RDP-bestand wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="8d73c-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="8d73c-145">Dit bestand toolaunch Hallo extern bureaublad-client gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8d73c-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="8d73c-146">Wanneer u wordt gevraagd, gebruiken Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven voor toegang tot extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="8d73c-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="8d73c-147">Eenmaal zijn verbonden, kopieert u Hallo volgende bestanden van Hallo extern bureaublad-sessie tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8d73c-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="8d73c-148">Plaatsen in een lokale map met de naam `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="8d73c-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="8d73c-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-JDBC-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="8d73c-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="8d73c-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="8d73c-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="8d73c-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="8d73c-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="8d73c-152">Hallo versie cijfers die zijn opgenomen in het Hallo-paden en bestandsnamen kunnen afwijken voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="8d73c-153">Verbinding verbreken Hallo extern bureaublad-sessie wanneer u klaar bent met het Hallo-bestanden zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="8d73c-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="8d73c-154">Hallo SQuirreL SQL toepassing starten.</span><span class="sxs-lookup"><span data-stu-id="8d73c-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="8d73c-155">Selecteer Hallo linksonder Hallo venster **stuurprogramma's**.</span><span class="sxs-lookup"><span data-stu-id="8d73c-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Tabblad stuurprogramma's aan de linkerkant Hallo van Hallo-venster](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="8d73c-157">Van pictogrammen bovenaan Hallo HALLO hallo **stuurprogramma's** dialoogvenster, selecteer Hallo  **+**  pictogram toocreate een stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="8d73c-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Stuurprogramma's pictogrammen](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="8d73c-159">In het dialoogvenster Hallo stuurprogramma toevoegen toevoegen Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8d73c-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="8d73c-160">**Naam**: Hive</span><span class="sxs-lookup"><span data-stu-id="8d73c-160">**Name**: Hive</span></span>
    * <span data-ttu-id="8d73c-161">**Voorbeeld-URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="8d73c-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="8d73c-162">**Extra klassepad**: gebruik Hallo toevoegen knop tooadd Hallo jar-bestanden eerder hebt gedownload</span><span class="sxs-lookup"><span data-stu-id="8d73c-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="8d73c-163">**Klassenaam**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="8d73c-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![stuurprogramma-dialoogvenster toevoegen](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="8d73c-165">Klik op **OK** toosave deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="8d73c-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="8d73c-166">Selecteer op Hallo links van Hallo SQuirreL SQL-venster, **aliassen**.</span><span class="sxs-lookup"><span data-stu-id="8d73c-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="8d73c-167">Klik vervolgens op Hallo  **+**  pictogram toocreate een alias voor een verbinding.</span><span class="sxs-lookup"><span data-stu-id="8d73c-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![nieuwe alias toevoegen](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="8d73c-169">Gebruik Hallo volgende waarden voor Hallo **Alias toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="8d73c-170">**Naam**: Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d73c-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="8d73c-171">**Stuurprogramma**: gebruik Hallo dropdown tooselect hello **Hive** stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="8d73c-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="8d73c-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="8d73c-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="8d73c-173">Vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="8d73c-174">**Gebruikersnaam**: Hallo cluster account aanmeldingsnaam voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="8d73c-175">Hallo standaardwaarde is `admin`.</span><span class="sxs-lookup"><span data-stu-id="8d73c-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="8d73c-176">**Wachtwoord**: Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-176">**Password**: hello password for hello cluster login account.</span></span>

 ![dialoogvenster alias toevoegen](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="8d73c-178">Gebruik Hallo **Test** knop tooverify die Hallo verbinding werkt.</span><span class="sxs-lookup"><span data-stu-id="8d73c-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="8d73c-179">Wanneer **verbinding maken met: Hive in HDInsight** dialoogvenster wordt weergegeven, selecteert u **Connect** tooperform Hallo test.</span><span class="sxs-lookup"><span data-stu-id="8d73c-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="8d73c-180">Als het Hallo-test is geslaagd, ziet u een **verbinding tot stand gebracht** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="8d73c-181">toosave hello verbinding gebruik alias, Hallo **Ok** knop onderin Hallo Hallo **Alias toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="8d73c-182">Van Hallo **verbinding maken met** vervolgkeuzelijst bovenaan Hallo SQuirreL SQL, selecteer **Hive in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8d73c-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="8d73c-183">Wanneer u wordt gevraagd, selecteert u **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8d73c-183">When prompted, select **Connect**.</span></span>

    ![het dialoogvenster voor verbinding](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="8d73c-185">Eenmaal zijn verbonden, Voer Hallo volgende query uitvoeren op dialoogvenster Hallo SQL-query's en selecteer vervolgens Hallo **uitvoeren** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d73c-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="8d73c-186">Hallo resultatengebied Hallo resultaten van Hallo query moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8d73c-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![dialoogvenster voor SQL query's, met inbegrip van resultaten](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="8d73c-188">Verbinding maken vanaf een voorbeeld van Java-toepassing</span><span class="sxs-lookup"><span data-stu-id="8d73c-188">Connect from an example Java application</span></span>

<span data-ttu-id="8d73c-189">Een voorbeeld van het gebruik van een Java-client tooquery Hive in HDInsight is beschikbaar op [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="8d73c-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="8d73c-190">Volg de instructies Hallo in Hallo opslagplaats toobuild en Hallo-voorbeeld uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8d73c-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8d73c-191">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="8d73c-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="8d73c-192">Is een onverwachte fout opgetreden tijdens het tooopen een SQL-verbinding</span><span class="sxs-lookup"><span data-stu-id="8d73c-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="8d73c-193">**Symptomen**: wanneer u verbinding maakt tooan HDInsight-cluster die versie 3.3 of 3.4, verschijnt er een fout die is een onverwachte fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="8d73c-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="8d73c-194">Hallo stacktracering voor deze fout begint met de Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="8d73c-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="8d73c-195">**Oorzaak**: deze fout wordt veroorzaakt door een niet-overeenkomend in Hallo-versie van Hallo commons codec.jar bestand gebruikt door SQuirreL en Hallo vereist door Hallo JDBC Hive-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="8d73c-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="8d73c-196">**Resolutie**: toofix deze fout, gebruik Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="8d73c-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="8d73c-197">Hallo commons codec jar-bestand downloaden van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="8d73c-198">SQuirreL sluiten en gaat u toohello directory waar SQuirreL op uw systeem is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8d73c-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="8d73c-199">In Hallo SquirreL map onder Hallo `lib` directory, vervangen Hallo bestaande commons-codec.jar Hello een gedownload van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8d73c-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="8d73c-200">Opnieuw opstarten SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="8d73c-200">Restart SQuirreL.</span></span> <span data-ttu-id="8d73c-201">Hallo fout kan niet meer optreden bij het verbinden van tooHive op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d73c-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d73c-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d73c-202">Next steps</span></span>

<span data-ttu-id="8d73c-203">U hebt geleerd hoe toouse JDBC toowork met Hive, gebruik Hallo volgen koppelingen tooexplore andere manieren toowork met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d73c-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="8d73c-204">Uploaden van gegevens tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="8d73c-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="8d73c-205">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d73c-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8d73c-206">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d73c-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8d73c-207">MapReduce-taken gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d73c-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
